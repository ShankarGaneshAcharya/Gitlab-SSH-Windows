## Copilot / AI Agent Instructions for this repo

This repository is a small documentation project that explains how to set up SSH keys and a GitLab Personal Access Token (PAT) on Windows. The guidance below is tailored to make an AI coding agent immediately productive when editing or extending these docs.

Key files
- `README.md` — top-level landing doc with links to the two guides.
- `SSH Key.md` — step-by-step Windows/Git Bash SSH setup (primary content).
- `PAT.md` — Personal Access Token guidance referenced from the README.

Big picture
- Purpose: documentation only — no build, test, or service runtime. Primary edits will be to markdown content and small metadata updates.
- Audience: Windows developers using Git Bash and VS Code with GitLab. Examples in the repo use Git Bash path syntax (`/c/Users/...`).

Developer workflows & useful commands
- Use Git Bash for the SSH commands (the docs intentionally use `/c/Users/...` paths). Example commands found in `SSH Key.md`:
  - `ssh-keygen -t ed25519 -C "your_email@example.com"`
  - `cat ~/.ssh/id_ed25519.pub | clip`
  - `eval $(ssh-agent -s)` then `ssh-add ~/.ssh/id_ed25519`
  - `ssh -T git@gitlab.com` to test connectivity
- Repo-level quick git task (workspace task visible in the environment):
  - `git add .; git commit -m 'Auto-commit'; git push origin main` (label: "Auto Git Commit and Push")

Conventions and patterns in this repo
- Markdown-first: keep output as Markdown with fenced code blocks. Some existing files include an HTML-style header (`<h1 style="text-align:center;">`) — preserve intent but prefer plain Markdown headings when adding new content.
- Filenames include spaces (e.g., `SSH Key.md`). Reference them exactly or URL-encode links in README if needed.
- Keep Windows-specific instructions (Git Bash vs PowerShell) together. If adding alternative commands for PowerShell, state clearly which shell the command targets.
- Prefer ED25519 in examples (this repo recommends it explicitly). If you add RSA examples, mark them as legacy/fallback.

Integration points
- External services referenced: `gitlab.com` (SSH keys, PATs) and VS Code GitLab Workflow extension. When modifying docs, do not change the target host unless adding an optional section for private GitLab instances — then show how to set `Host gitlab.company.com` in `~/.ssh/config`.

Editing guidelines for AI
- Preserve example commands and Windows/Git Bash nuances. If you normalize paths, include both `/c/Users/...` (Git Bash) and `C:\Users\...` (PowerShell) variants.
- When modifying a command example, run a quick sanity check: ensure flags and filenames match the rest of the doc (e.g., if `id_ed25519` is used earlier, keep using that name).
- Keep commits descriptive (avoid replacing the existing workspace 'Auto-commit' task). Use conventional messages like `docs: improve SSH setup instructions`.

When to create code vs docs
- This repo is docs-only. If you add scripts (helper PowerShell/Git Bash scripts), place them in a new `scripts/` folder and update README with usage examples. Add a short license header to any scripts matching `LICENSE` terms.

Examples from the codebase
- Reference the exact lines in `SSH Key.md` for SSH flow: key generation, adding to clipboard, starting ssh-agent, `ssh-add`, and `ssh -T git@gitlab.com`.

If something isn't discoverable
- There are no tests or build steps in the repo. If a task requires running or testing a script you added, include the exact shell to use and a single command example in the doc.

Ask for clarification
- If a section needs Windows-specific automation (PowerShell modules, scheduled tasks, or VS Code tasks), ask which target shell the maintainer expects to support first.

Thanks — leave a short note in the PR describing the tested shell and any local checks you performed.
