# Toast Inventory Management Redesign

UX case study for a date-based stocking redesign in Toast POS.

---

## Windows Setup

### What you need

| Tool | Purpose | Install |
|------|---------|---------|
| Git for Windows | Clone and sync the repo | https://git-scm.com/download/win |
| Node.js (LTS) | Required by Claude Code | https://nodejs.org |
| Claude Code | AI assistant + runs the MCP | `npm install -g @anthropic-ai/claude-code` |
| Backlog.md MCP | Task board and management | See below |

---

### Step 1 — Git for Windows

During installation, when asked about line endings, choose:
> **"Checkout as-is, commit as-is"**

The `.gitattributes` file in this repo handles normalization automatically — you don't need Git to convert anything.

---

### Step 2 — Clone the repo

```powershell
git clone <your-remote-url> toast-inventory-management-redesign
cd toast-inventory-management-redesign
```

---

### Step 3 — Install Claude Code

```powershell
npm install -g @anthropic-ai/claude-code
```

Then authenticate:
```powershell
claude
```

Follow the login prompt. Once authenticated, Claude Code is ready.

---

### Step 4 — Set up the Backlog.md MCP

The Backlog.md MCP server lets Claude Code read and write tasks in the `backlog/` folder.

Install it globally via npm:
```powershell
npm install -g backlog-md
```

Then register it with Claude Code by editing `%APPDATA%\claude\claude.json`
(or creating it if it doesn't exist):

```json
{
  "mcpServers": {
    "backlog": {
      "command": "npx",
      "args": ["backlog-md", "--project-root", "C:\\path\\to\\toast-inventory-management-redesign"]
    }
  }
}
```

Replace the path with the actual location where you cloned the repo.

> **Note:** Verify the exact package name and MCP server command from the Backlog.md documentation, as it may differ from `backlog-md`.

---

### Step 5 — Open the task board

Start the browser-based board from the repo root:
```powershell
npx backlog-md board
```

This opens `http://localhost:6420` in your browser. If Windows Firewall prompts you, allow it on private networks.

---

### Step 6 — Open in Claude Code

```powershell
cd C:\path\to\toast-inventory-management-redesign
claude
```

Claude Code will pick up the MCP configuration and the `.claude/settings.local.json` permissions automatically.

---

## Project structure

```
backlog/
  config.yml          # Board configuration (port, statuses, etc.)
  tasks/              # One markdown file per task
CLAUDE.md             # Instructions for Claude Code
readme.md             # This file
toast-inventory-case-study-notes.md
Inventory Management in Toast.md
```

---

## Syncing changes

Tasks are plain markdown files tracked in git. To sync after editing:
```powershell
git add backlog/tasks/
git commit -m "update task status"
git push
```
