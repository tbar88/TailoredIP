# AGENTS.md

## Repository purpose
This repository hosts a Copilot-native orchestration layer for Tailored IP Solutions. It is designed to keep business state, recurring workflows, and agent instructions in version-controlled files so GitHub Copilot can coordinate revenue-first work against a shared source of truth.

## Workstreams
| Workstream | Canonical path | Primary outcome |
| --- | --- | --- |
| Command Center | `state/00_command_center/` | Weekly operating summary and priorities |
| Consulting Pipeline | `state/01_consulting_pipeline/` | Revenue pipeline tracking and next actions |
| Target Clients | `state/02_target_clients/` | Research-backed target development |
| Intake & Qualification | `state/03_intake_qualification/` | Rapid triage and fit decisions |
| Marketing Content | `state/04_marketing_content/` | Business-development content pipeline |
| Consulting Delivery | `state/05_consulting_delivery/` | Delivery scope, deadlines, and blockers |
| Practice Support | `state/06_practice_support/` | General practice-support matters |
| Career Opportunities | `state/07_career_opportunities/` | Financially relevant firm/role opportunities |
| Business Growth | `state/08_business_growth/` | Strategic growth initiatives |
| Templates & Prompts | `state/09_templates_prompts/` | Space mirrors, templates, prompt inventory |
| Work-Product Refinement | `state/10_work_product_refinement/` | Non-substantive cleanup and formatting queue |
| Archive | `state/11_archive/` | Completed or inactive records |

## State model
- `state/` is canonical and version-controlled.
- Mirror each active workstream into one Copilot Space.
- Keep cross-workstream summaries in `state/00_command_center/current-command-center.md`.
- Register Space mirrors and reusable prompt coverage in `state/09_templates_prompts/spaces-mirror-register.csv`.

## Core workflows
- `/triage` — turns a new inquiry into a revenue-first intake Task Spec
- `/pipeline-review` — reviews pipeline rows, blockers, and next actions
- `/target-scan` — proposes new target-client and pipeline additions
- `/draft-content` — develops business-development content from approved source material
- `/delivery` — coordinates consulting delivery artifacts and blockers
- `/refine` — performs non-substantive cleanup subject to the guardrail
- `/command-center` — regenerates the weekly operating summary

## Setup commands
Run these after cloning or after editing the scaffolding:

```bash
cd /home/runner/work/TailoredIP/TailoredIP
python3 -m json.tool templates/task-spec.template.json >/dev/null
python3 -m json.tool templates/artifact-spec.template.json >/dev/null
python3 -m json.tool .github/copilot-mcp.json >/dev/null
ruby -e 'require "yaml"; Dir[".github/workflows/*.yml", ".github/ISSUE_TEMPLATE/*.yml"].each { |f| YAML.load_file(f) }'
```

## How to run recurring workflows
- Manual target scan: `gh workflow run weekly-target-signal-scan.yml`
- Manual command-center regeneration: `gh workflow run weekly-command-center-regeneration.yml`
- Weekly schedules are already defined in `.github/workflows/`.
- The workflows create GitHub Issues and try to assign `copilot-swe-agent` only when that assignee is enabled and assignable.

## Admin setup notes
- Enable the Copilot coding agent at the org and repo level.
- Enable or connect the MCP servers listed in `.github/copilot-mcp.json`.
- Copy `docs/org-github-repo/.github/copilot-instructions.md` into the org-level `.github` repo.
- Create one Copilot Space per workstream and attach the listed `state/` files.
- Map pipeline and intake trackers to a GitHub Projects board.

## Non-negotiable guardrail
Formatting, cleanup, conversion, and polish must never alter legal meaning, holdings, citations, factual claims, data values, prospect/client information, or strategy. If a requested refinement would change substance, flag it instead of applying it.
