# Setup & Operations TODO — Master Checklist

> **Single home base for everything that needs your hands.** Tomasz is the sole admin/user, so every item here is yours to do — but each is point-and-click (GUI), no coding. Items the agent could do for you have already been done in the repo; only the things requiring your login, a credential, or an external account are left here.
>
> Suggested approach: do the 🔴 items in one ~10-minute sitting to turn the system on, then pick off the rest whenever you have time.
>
> **Link note:** the org-settings link in item 1 assumes your organization is named `TailoredIP`. If your org name differs, swap it in the URL. All repo/personal links are correct as-is.

## 🔴 Turn the system on (do first, ~10 min)
| Done | Task | Where to do it |
|------|------|----------------|
| [ ] | **Enable the coding agent** — allow it to create branches, commit, and open pull requests | Org [Settings → Copilot](https://github.com/organizations/TailoredIP/settings/copilot/features), then repo [Settings → Copilot → Coding agent](https://github.com/tbar88/TailoredIP/settings/copilot/coding_agent) |
| [ ] | **Confirm the bot is assignable** — "Copilot" appears in the **Assignees** box | Open any [Issue](https://github.com/tbar88/TailoredIP/issues) |
| [ ] | **Set the assignment variable** — new repository variable `COPILOT_AGENT_ASSIGNMENT_ENABLED` = `true` (only after the bot is assignable) | [Settings → Actions Variables](https://github.com/tbar88/TailoredIP/settings/variables/actions) |
| [ ] | **Smoke-test the automation** — enable workflows if prompted, run **Weekly target and signal scan**, then check for a new Issue assigned to Copilot (~1 min) | [Actions tab](https://github.com/tbar88/TailoredIP/actions) → then [Issues](https://github.com/tbar88/TailoredIP/issues) |

## 🟡 Connect your tools
| Done | Task | Where |
|------|------|-------|
| [ ] | **Notion** — add the Notion server and **authorize / sign in** (OAuth, nothing to paste; endpoint pre-filled in `.github/copilot-mcp.json`), then set it enabled | Repo [Settings → Copilot → Coding agent → MCP servers](https://github.com/tbar88/TailoredIP/settings/copilot/coding_agent) |
| [ ] | **SharePoint / OneDrive** (*defer if busy*) — one-time Azure app registration. Easy interim alternative: attach SharePoint/OneDrive files to a Copilot Space instead (zero setup) | Follow [`docs/sharepoint-onedrive-mcp-setup.md`](./sharepoint-onedrive-mcp-setup.md) |

## 🟢 Context & visibility
| Done | Task | Where |
|------|------|-------|
| [ ] | **Create 10 Copilot Spaces** — one per row in the register, attach the matching `state/` folder, then paste each link back into the CSV (replace `TODO_SPACE_LINK`, set status to `Active`) — or hand the links to the agent and it will update the file for you | [github.com/copilot/spaces](https://github.com/copilot/spaces) · register: [`spaces-mirror-register.csv`](../state/09_templates_prompts/spaces-mirror-register.csv) |
| [ ] | **Projects board** — add fields (Workstream, Status, Priority, Next Action, Follow-Up Date, Owner, Revenue Impact) and views (Revenue now, Intake triage, Active delivery, Growth backlog). Visibility only; the `state/` files stay the system of record | Repo [Projects → New project → Board](https://github.com/tbar88/TailoredIP/projects) |
| [ ] | **Notifications + mobile app** — turn on notifications and install the GitHub mobile app, so you can review and merge AI pull requests from your phone | [Notification settings](https://github.com/settings/notifications) + GitHub mobile app |

## 🛡️ Light-touch safety net (recommended config)
Your preference: protect against risky/broken changes, but don't gate every minor edit. Here is the setup that matches that.

**Already done for you (automated, no clicks):**
- A validation workflow (`.github/workflows/validate-scaffolding.yml`) runs on every pull request and automatically rejects changes that break JSON, YAML, or the Spaces register. Routine content edits pass on their own — so minor changes never wait on you.

| Done | Task | Where |
|------|------|-------|
| [ ] | **Add a light branch-protection rule on `main`** (~2 min). Target branch `main`, enable **only**: ✅ Require status checks → select **Validate scaffolding**; ✅ Require a pull request before merging with **Required approvals = 0**. ❌ Do **not** enable "Require approval of the most recent push" or multiple required reviewers | [Settings → Branches](https://github.com/tbar88/TailoredIP/settings/branches) |
| [ ] | **Optional — turn on auto-merge.** Then the agent can mark a PR auto-merge and it merges itself the moment the validation check passes — hands-off for low-risk work, still blocked if something is broken | [Settings → General → Pull Requests](https://github.com/tbar88/TailoredIP/settings) |

> Net effect: things you "set into motion" run to completion automatically; only genuinely broken or risky changes stop and ask for you.

## ⏭️ Deferred / decide later
| Done | Task | Reference |
|------|------|-----------|
| [ ] | **Promote the agent team org-wide** so every repo you own inherits the same orchestrator + sub-agents (create an org-level `.github` repo; the agent can prepare the files for you to copy in) | [`docs/orchestration-and-subagents.md`](./orchestration-and-subagents.md) |
| [ ] | **GitHub Pages publishing** (for approved marketing content): pick a theme, branch, and publish path when you first want to publish something public. Not needed to operate the system | [`docs/copilot-setup-guide.md`](./copilot-setup-guide.md) §5 |
| [ ] | **SharePoint write access**: only add Graph write permissions later if you want the agent to modify SharePoint content (start read-only) | [`docs/sharepoint-onedrive-mcp-setup.md`](./sharepoint-onedrive-mcp-setup.md) |

## Admin reference (what's already configured in the repo)
- Verified Notion MCP endpoint + OAuth note, and the free Microsoft Learn MCP server: `.github/copilot-mcp.json`
- Pre-filled Spaces register: `state/09_templates_prompts/spaces-mirror-register.csv`
- Setup guide: `docs/copilot-setup-guide.md`
- SharePoint walkthrough: `docs/sharepoint-onedrive-mcp-setup.md`
- Automated validation gate: `.github/workflows/validate-scaffolding.yml`
