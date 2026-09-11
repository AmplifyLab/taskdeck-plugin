# TaskDeck for Claude Code

`/taskdeck:track` puts your work on a [TaskDeck](https://taskdeck.me) board. Run it once in a repository or a workspace and every task Claude does there becomes a card, with the reasons, the criteria and the verification on it.

## What is what

| Piece | What it is | What it is for |
|---|---|---|
| **TaskDeck connector** | The connection between Claude and your TaskDeck account, added once to your Claude account | Gives Claude the TaskDeck tools (boards, cards, Autotrack) in every Claude app: the desktop app's Chat and Code tabs, the terminal and mobile |
| **TaskDeck plugin** (this repository) | A Claude Code add-on | Adds `/taskdeck:track`, the setup command. It connects TaskDeck first if the connector is missing |
| **`/taskdeck:track`** | The setup, run once per folder | Picks or creates the board, turns Autotrack on and writes a short block into the folder's CLAUDE.md |

## Quick start

1. Install the plugin:

   ```bash
   claude plugin marketplace add AmplifyLab/taskdeck-plugin
   claude plugin install taskdeck@taskdeck
   ```

2. In the folder you want tracked, run:

   ```
   /taskdeck:track
   ```

   If TaskDeck is not connected yet, it opens Claude's "Add custom connector" dialog with TaskDeck filled in. Click **Add**, then sign in to TaskDeck and approve. The setup continues on its own and asks at most a few questions: which board, how it should look, when finished cards leave it, and whose name Claude's work carries.

`/taskdeck:track Web` tracks the folder on an existing board called Web without asking which.

## Manual install

Do the same steps by hand to see what each one does:

1. **Connect TaskDeck.** In Claude, open Customize → Connectors, choose Add custom connector, name it TaskDeck and use `https://mcp.taskdeck.me/mcp`. Click Connect and approve in TaskDeck. The TaskDeck tools now work in every Claude app.
2. **Install the plugin** with the two commands above. `/taskdeck:track` appears in Claude Code.
3. **Run `/taskdeck:track`** in the folder.

Signed in to Claude Code with an API key instead of a Claude account? Connectors from claude.ai are not available there. Add the connection to Claude Code directly, then start a new session:

```bash
claude mcp add --transport http taskdeck https://mcp.taskdeck.me/mcp
claude mcp login taskdeck
```

## After setup

Ask Claude for work the way you always do. It calls `start-work` before changing anything, comments on the card as it goes, and calls `finish-work` when the work is verified.
