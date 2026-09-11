---
name: track
description: Turn on TaskDeck Autotrack for the folder you are working in, a single repository or a workspace that holds several, so every task from then on becomes a card on a TaskDeck board. Use it whenever the person asks to track this repo or workspace on TaskDeck, to use TaskDeck for this project, to set up TaskDeck, or to connect their work to a board, even if they do not say "Autotrack". Not for day-to-day card work; once tracking is on, the TaskDeck tools start-work and finish-work do that.
argument-hint: [board]
---

Turn on TaskDeck Autotrack for the folder the session is working in. The TaskDeck server runs the wizard; this skill only gets it started. Ask the person only the questions the server's guide lists, each as a multiple-choice question with the default pre-selected where this client has one, plain text otherwise.

0. Make sure TaskDeck is connected. If the TaskDeck tools (`who-am-i`, `track-repository`) are available in this session, go to step 1. If they are not:
   - Open Claude's "Add custom connector" dialog with TaskDeck filled in, using the system's open command (`open` on macOS, `xdg-open` on Linux, `start ""` on Windows): `https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=TaskDeck&connectorUrl=https%3A%2F%2Fmcp.taskdeck.me%2Fmcp`
   - Tell the person in one sentence: click Add in that dialog, then sign in to TaskDeck and approve. That is the only thing they do.
   - Wait for the TaskDeck tools: search your tools for `who-am-i` every 15 seconds for up to 3 minutes, and go on to step 1 as soon as it is there.
   - If it does not arrive, tell the person to start a new session and run /taskdeck:track again. If they use Claude Code with an API key rather than a Claude account, connectors from claude.ai are not available to them: run `claude mcp add --transport http taskdeck https://mcp.taskdeck.me/mcp` and `claude mcp login taskdeck` instead, then ask them to start a new session.
1. Call the TaskDeck tool `who-am-i`. If the connection acts as an AI agent, stop and tell the person: setup needs the connection to act as them, so they reconnect as themselves or ask a project admin to create the board and grant it.
2. Look at the folder. If it is a git repository, read its remote (`git remote get-url origin`) and count the distinct authors (`git shortlog -sn --all`). If it is not one but its subfolders are, collect every one of them, name and remote, and count authors across them: they are one workspace and share one board. Take the folder name as well. No git anywhere is fine: use the folder name and pass has_git: false.
3. Call the TaskDeck tool `track-repository` with preview: true, name and has_git, plus remote for one repository or repositories (a list of name and remote) for a workspace. If the person gave an argument, pass it as board: "$ARGUMENTS".
4. Follow the `guide` in the preview result to the letter: the questions in their order and only the ones it says are undecided, the second `track-repository` call with the answers, the returned block written into CLAUDE.md at the root of the folder (and into AGENTS.md when that file exists) between the taskdeck:autotrack markers, and the confirmation in a few sentences.
