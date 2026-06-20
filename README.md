# TailoredIP Copilot Orchestration Layer

This repository now scaffolds a GitHub Copilot Enterprise-native orchestration layer for Tailored IP Solutions. The design keeps business state in version-controlled files, uses repo instructions plus custom agents for coordination, and routes recurring work through issue-driven automation.

## What this repo contains
- `AGENTS.md` — operator README for human and Copilot agents
- `.github/copilot-instructions.md` — repo-wide Business Orchestrator instructions
- `.github/instructions/` — path-scoped rules for each workstream in `state/`
- `.github/agents/` — capability-based custom agents plus a validator agent on a different model
- `.github/prompts/` — reusable Copilot prompt files for recurring workflows
- `.github/ISSUE_TEMPLATE/task-spec.yml` — canonical Task Spec issue form
- `.github/pull_request_template.md` — Artifact Spec validation checklist
- `.github/workflows/` — weekly issue-creation automations that can assign `copilot-swe-agent`
- `.github/copilot-mcp.json` — repo-scoped MCP server scaffold with explicit TODO placeholders
- `state/` — canonical business trackers and command-center files
- `templates/` — Task Spec, Artifact Spec, and command-center templates
- `docs/` — setup and operating guidance, including the org-level instructions copy scaffold

## Build order followed
1. Repo-wide orchestration instructions
2. Revenue-first capability agents
3. Canonical state trackers and templates
4. Task intake and artifact validation templates
5. MCP and recurring workflow scaffolding
6. Operating documentation and sample issues

## How it fits together
1. Capture work through the Task Spec issue form.
2. Let the Business Orchestrator load the right `state/` context.
3. Delegate findings-only work to the relevant capability agents.
4. Validate outputs with the Validator agent and PR checklist.
5. Mirror the active `state/` folders into one Copilot Space per workstream.
6. Use scheduled workflows to open recurring issues and, when enabled, assign them to `copilot-swe-agent`.

## Key constraints
- The repo is the source of truth; Spaces are mirrors.
- Revenue stabilization wins ties.
- Work-product refinement is supportive only.
- Formatting and polish may not change legal meaning, citations, facts, data, prospect/client information, or strategy.

## Start here
- Read `AGENTS.md` for setup and workflow usage.
- **Open `docs/setup-and-operations-todo.md` — the single checklist of everything that still needs you (all point-and-click).**
- Review `docs/copilot-setup-guide.md` for org/repo admin TODOs.
- For SharePoint/OneDrive access, follow `docs/sharepoint-onedrive-mcp-setup.md`.
- Copy `docs/org-github-repo/.github/copilot-instructions.md` into the org-level `.github` repository to make the same standing instructions global.
