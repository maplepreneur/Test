# GitHub Copilot CLI Best Practices: A Beginner's Guide to Agentic Coding

GitHub Copilot CLI brings the Copilot coding agent to your terminal, so you can build, debug, and understand code without leaving the command line. This guide is a blog-style walkthrough for complete beginners who want practical best practices, plus a tour of advanced features like MCPs, custom agents, and plan mode.

## Why Copilot CLI feels different

Copilot CLI is not just chat in a terminal. It can:
- Read and edit files in your repo (with your approval)
- Run tools like tests or formatters (with your approval)
- Interact with GitHub via the built-in MCP server
- Plan multi-step changes before writing code

That makes it an "agentic" tool: it can act, not just answer.

## Quick start: install and sign in

Prerequisites:
- A GitHub Copilot subscription
- PowerShell 6+ on Windows

Install (choose one):
```bash
brew install copilot-cli
```
```bash
npm install -g @github/copilot
```
```bash
curl -fsSL https://gh.io/copilot-install | bash
```

Launch:
```bash
copilot
```

If prompted, run:
```
/login
```

You can also authenticate with a fine-grained PAT that has the "Copilot Requests" permission set, using `GH_TOKEN` or `GITHUB_TOKEN`.

## Your first session (what to expect)

1. Start Copilot CLI in a repository folder.
2. Approve the trust prompt. You can allow access once, remember the folder, or exit.
3. Enter a prompt like: "Explain the project structure" or "Fix the failing tests."
4. When Copilot asks to use a tool (like `node`, `sed`, or `chmod`), approve or reject it.

Best practice: approve only the tools you actually want to run. Use session-only approvals when possible.

## Permissions and safety: the guardrails

Copilot CLI uses explicit permissions for paths and URLs:
- **Path permissions**: by default, Copilot can access the current working directory and its subdirectories, plus the system temp directory.
- **URL permissions**: external URLs require approval unless you allow them.

Useful flags:
```bash
copilot --allow-all-paths
copilot --allow-all-urls
copilot --allow-url github.com
```

You can also enable all permissions with `--allow-all` or `--yolo`, but use those only in trusted environments.

## Best practices for great results

### 1) Start with a focused prompt
Describe the task and expected outcome:
> "Add a CLI flag that enables debug logs and update the help text."

### 2) Use plan mode for non-trivial work
Press **Shift+Tab** to toggle plan mode. Ask for an implementation plan before any code changes.

### 3) Bring the right context
Use `@` to include specific files in your prompt:
```
Fix the bug in @src/app.js
```

### 4) Approve tools with intent
Approve only the exact tools needed. If Copilot suggests a risky command, reject it and say what you'd prefer.

### 5) Keep context healthy
Use `/context`, `/usage`, and `/compact` to manage token usage and avoid stale context.

### 6) Review changes before committing
Use `/diff` to inspect edits and `/review` for a quick code review pass.

## MCPs: extend Copilot CLI beyond GitHub

Copilot CLI ships with the **GitHub MCP server** already configured, which enables GitHub actions like viewing issues and PRs. You can add custom MCP servers to extend capabilities.

### Add an MCP server (interactive)
1. Run:
   ```
   /mcp add
   ```
2. Fill in the fields (use **Tab** to move between fields).
3. Press **Ctrl+S** to save.

Your MCP configuration is stored in:
```
~/.copilot/mcp-config.json
```

You can manage MCP servers with:
```
/mcp show
/mcp add
/mcp edit
/mcp delete
/mcp disable
/mcp enable
```

For the JSON schema of MCP servers, refer to the official MCP configuration docs.

## Advanced features tour

### Experimental mode and autopilot
Enable experimental mode with:
```
copilot --experimental
```
Or toggle inside the CLI:
```
/experimental
```

Experimental mode includes **autopilot**, a mode you can reach by cycling with **Shift+Tab**. Autopilot encourages Copilot to keep working until the task is done.

### Switch models
Copilot CLI defaults to **Claude Sonnet 4.5**. Switch models with:
```
/model
```

### Resume sessions
Resume sessions with:
```
copilot --resume
```
Or:
```
/resume
```
Quickly continue the last local session with:
```
copilot --continue
```

### Delegate work to Copilot coding agent
Hand off a task to the cloud agent:
```
/delegate complete the API integration tests and fix any failing edge cases
```
Or prefix a prompt with `&`:
```
& complete the API integration tests and fix any failing edge cases
```

### Custom instructions
Add repository-wide guidance in:
```
.github/copilot-instructions.md
```
Or path-specific instructions in:
```
.github/instructions/**/*.instructions.md
```
You can also use `AGENTS.md` for agent-specific guidance.

### Custom agents
Custom agents live in:
- `~/.copilot/agents` (user-level)
- `.github/agents` (repo-level)
- `/agents` directory in the `.github-private` repository (org/enterprise-level)

Use them via `/agent`, or by referencing them in a prompt. You can also set one at launch:
```
copilot --agent=refactor-agent --prompt "Refactor this code block"
```

### Skills
Skills are reusable resources that improve agent performance. See the "Agent Skills" docs for details.

### LSP support
Copilot CLI can use Language Server Protocol (LSP) servers for richer code intelligence. Configure LSPs in:
- `~/.copilot/lsp-config.json` (user-level)
- `.github/lsp.json` (repo-level)

Example:
```json
{
  "lspServers": {
    "typescript": {
      "command": "typescript-language-server",
      "args": ["--stdio"],
      "fileExtensions": {
        ".ts": "typescript",
        ".tsx": "typescript"
      }
    }
  }
}
```

Check status with:
```
/lsp
```

## Everyday shortcuts that save time

- `@` include a file in context
- `!` run a local shell command directly
- `Esc` cancel a running operation
- `Ctrl+T` toggle reasoning visibility
- `Ctrl+X` then `/` to run a slash command

## Troubleshooting and help

Need help inside the CLI?
- `?` shows command options
- `copilot help` shows full CLI help
- `/feedback` sends feedback

## Final tips for beginners

1. Start small: use Copilot for explanations and single-file changes first.
2. Use plan mode for larger tasks to stay in control.
3. Review every change and tool invocation.
4. Treat Copilot like a teammate: clear goals and tight feedback yield the best results.

Each prompt uses a premium request, so use `/usage` to monitor your usage.

---

If you want even more depth, explore the official GitHub Copilot CLI documentation and command reference.
