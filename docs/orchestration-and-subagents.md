# Orchestration & sub-agents

> Plain-language explanation of the "one model oversees a team of sub-agents" setup (the Perplexity Comet / "computer" style you asked for), how it already works in this repo, how to use it, and where its limits are. No coding required.

## Short answer
You already have this. The repo is built as an **orchestrator-oversees-sub-agents** system:
- **The orchestrator** = `.github/copilot-instructions.md` (the "Business Orchestrator"). This is the supervising model that talks to you, breaks a request into parts, hands parts to specialists, reconciles their work, and gives you one answer.
- **The sub-agents** = the eight specialist files in `.github/agents/` (pipeline, target research, intake, delivery, marketing, practice support, career, refinement). Each has its own focus and its own model, and each returns findings only — they never talk to you directly.
- **The independent checker** = `.github/agents/validator.agent.md`, which runs on a *different* model and reviews the work against your rules before anything is final.

GitHub Copilot natively supports this pattern: agent files in `.github/agents/` are auto-discovered, the main agent can delegate to them by intent or call them explicitly, they can run in parallel, and there is a "Mission Control" view for watching multiple runs at once.

## How it maps to what you described
| What you asked for | How it's set up here |
| --- | --- |
| A model overseeing the work | The Business Orchestrator in `copilot-instructions.md` |
| Sub-agents that get used when they help | The 8 capability agents in `.github/agents/`, delegated to only when a request benefits |
| Parallel work where it makes sense | Orchestrator runs independent sub-agents in parallel, then merges findings (now stated explicitly in the operating model) |
| Quality oversight | The separate-model Validator does a final independent check |
| One clean result to you | Only the orchestrator's single reconciled response reaches you |

## How to use it (you don't manage the sub-agents)
You never have to assign or coordinate sub-agents yourself — that's the orchestrator's job. You just make a request the normal way:
- **In a Copilot Space or chat:** describe the outcome you want (e.g., "Scan for new target clients in AI-search marketing and update the pipeline with the best fits"). The orchestrator decides which sub-agents to involve.
- **Via the Task Spec issue form:** Issues > New issue > Task Spec. The `active_agents` field lets you (optionally) name which specialists should be involved; leaving it general lets the orchestrator choose.
- **Via the recurring workflows:** the weekly scans already list the sub-agents they expect (`target-client-research`, `consulting-pipeline`, `validator`) so they run hands-off.

## What's available now vs. what needs a toggle
- **Available now (already in the repo):** the orchestrator, the 8 sub-agents, the validator, the delegation rules, and the explicit supervisory loop. Nothing to build.
- **Needs the one-time on switch:** the coding agent must be enabled (see `docs/setup-and-operations-todo.md`, the 🔴 items) for the agent to run autonomously on issues and open PRs.
- **Optional upgrade — make the agent team available across all your repos:** copy the `.github/agents/` folder (and `copilot-instructions.md`) into an organization-level `.github` repository. Then every repo you own inherits the same orchestrator + sub-agents. Left as a TODO below.
- **Optional — richer "Mission Control" multi-run monitoring:** available in the latest VS Code Copilot and Copilot CLI if you ever want a live dashboard of parallel agent runs. Not required for the GitHub-website flow.

## Honest limits
- Sub-agents return findings to the orchestrator, not to you — by design, so you get one consolidated answer rather than a noisy group chat.
- True parallel fan-out depends on the Copilot surface you use; the GitHub coding agent handles delegation well, and VS Code/CLI add live multi-run monitoring. The behavior is the same either way from your side: you ask once, you get one reconciled result.
- The system favors doing the simplest thing that works — it won't spin up the whole team for a small request, which keeps runs fast and credit-efficient.

## TODO (optional, your call)
- [ ] **Promote the agent team org-wide (GUI + simple file copy).** Create an org-level repository named `.github`, then copy this repo's `.github/agents/` folder and `.github/copilot-instructions.md` into it so all your repositories share the same orchestrator and sub-agents. Hand this to the agent and it can prepare the files for you; you just create the repo.

## Reference files
- Orchestrator: `.github/copilot-instructions.md` (see "Operating model" and "Sub-agent supervision")
- Sub-agents: `.github/agents/*.agent.md`
- Independent checker: `.github/agents/validator.agent.md`
- Task intake: `.github/ISSUE_TEMPLATE/task-spec.yml` and `templates/task-spec.template.json`
- Recurring runs: `.github/workflows/`
