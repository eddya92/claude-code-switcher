# claude-switch

Switch between multiple Claude Code accounts instantly — no re-authentication needed.

```
Claude Code — Account Switcher
──────────────────────────────────────────
  Active:  personal@gmail.com (Alice)

  Other saved accounts:
  [1] work@company.com (Alice - Work)

  Switch to work@company.com? [y/N]
```

## How it works

Claude Code stores OAuth tokens in macOS Keychain and account metadata in `~/.claude.json`.  
`claude-switch` saves snapshots of both for each account and swaps them on demand.

> **macOS only** — relies on the `security` CLI for Keychain access.

## Install

```bash
git clone https://github.com/eddya92/claude-code-switcher.git
cd claude-code-switcher
chmod +x claude-switch
sudo ln -s "$PWD/claude-switch" /usr/local/bin/claude-switch
```

## First-time setup

**Step 1 — close Claude Code, then save your current account (account A)**
```bash
claude-switch save
```

**Step 2 — open Claude Code and log out**

Run `claude` to open Claude Code, then type `/logout` inside the session.

**Step 3 — log in as account B**

While still in Claude Code, type `/login` and authenticate with your second account.

**Step 4 — close Claude Code, then save account B**
```bash
claude-switch save
```

**Done — switch any time**
```bash
claude-switch
```

## Usage

```
claude-switch                        Interactive switcher — switches and launches Claude here
claude-switch --new-window           Switch and open Claude in a new terminal window
claude-switch --no-window            Switch and print the command to run manually
claude-switch usage                  Show token usage (current session + last 7 days)
claude-switch statusline             Add usage bars to Claude Code (run once per machine)
claude-switch save                   Save current account credentials as a profile
claude-switch list                   List all saved profiles
claude-switch use <email>            Switch non-interactively (launches in this terminal)
claude-switch use <email> --new-window  Switch and open Claude in a new terminal window
claude-switch --help                 Show help
```

By default, `claude-switch` replaces the current terminal process with `claude` (or `claude --resume <session>` if a session is saved for the current project). Use `--new-window` to open a separate iTerm2 or Terminal window instead.

## Session resume

Run `claude-switch save` inside a project directory to snapshot the current session ID. When you switch back to that account, `claude-switch` automatically resumes where you left off.

## Where profiles are stored

Account metadata (email, display name) is saved as JSON files in `~/.claude-switcher/accounts/` with `600` permissions.  
OAuth tokens are stored exclusively in macOS Keychain under the service name `Claude Code-switcher`, one entry per account — they never touch the filesystem.

## Requirements

- macOS (uses `security` CLI)
- Python 3 (pre-installed on macOS)
- Claude Code

## License

MIT
