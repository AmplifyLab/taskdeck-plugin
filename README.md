# TaskDeck for Claude Code

One command puts your work on a [TaskDeck](https://taskdeck.me) board: `/taskdeck:track` turns Autotrack on for the folder you are in, and from then on every task Claude does there is a card, with the reasons, the criteria and the verification on it.

The plugin is deliberately small. It bundles the TaskDeck connector and one skill that starts the setup. Everything the setup asks and everything the tools do comes from the TaskDeck server, so the plugin never goes out of date.

## Install

```bash
claude plugin marketplace add AmplifyLab/taskdeck-plugin
claude plugin install taskdeck@taskdeck
```

Start a new session. The first TaskDeck call asks you to sign in to your TaskDeck account in the browser; approve the connection as yourself.

If you already added TaskDeck as a connector or with `claude mcp add`, the plugin's server is a second copy of the same thing. Keep whichever you prefer.

## Use

In the folder you want tracked, a single repository or a workspace holding several:

```
/taskdeck:track
```

You answer at most a few questions: which board, how the board should look, when finished cards leave it, and whose name Claude's work carries. The setup writes a short block into the folder's CLAUDE.md and confirms. After that, ask Claude for work the way you always do. It calls `start-work` before changing anything, comments on the card as it goes, and calls `finish-work` when the work is verified.

`/taskdeck:track Web` tracks the folder on an existing board called Web without asking which.

## What is in the box

- `.mcp.json`: the TaskDeck connector, `https://mcp.taskdeck.me/mcp`.
- `skills/track`: the skill behind `/taskdeck:track`.
