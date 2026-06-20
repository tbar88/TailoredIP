# Setup & Operations TODO

> Single home base for everything that needs **your** hands. Tomasz is the sole admin/user, so every item here is yours to do — but each is point-and-click (GUI), no coding. Items the agent could do for you have already been done in the repo; only the things requiring your login, a credential, or an external account are left here.
>
> Suggested approach: do the 🔴 items in one ~10-minute sitting to turn the system on, then pick off the rest whenever you have time.

## 🔴 Turn the system on (do first, ~10 min)
- [ ] **Enable the coding agent.** Org **Settings > Copilot** > enable coding agent for TailoredIP. Then repo **Settings > Copilot** > allow it to create branches, commit, and open pull requests.
- [ ] **Confirm the bot is assignable.** Open any Issue; check that **Copilot** appears in the **Assignees** box.
- [ ] **Set the assignment variable.** Repo **Settings > Secrets and variables > Actions > Variables > New repository variable**: name `COPILOT_AGENT_ASSIGNMENT_ENABLED`, value `true`. (Do this only after the bot is assignable.)
- [ ] **Smoke-test the automation.** Repo **Actions** tab > if prompted, click **I understand my workflows, enable them** > open **Weekly target and signal scan** > **Run workflow**. After ~1 min, check the **Issues** tab for a new issue assigned to Copilot.

## 🟡 Connect your tools
- [ ] **Notion (easy, GUI).** Repo **Settings > Copilot > Coding agent > MCP servers** > add the Notion server > click to **authorize / sign in** to your Notion workspace (OAuth — nothing to paste) > set it enabled. Endpoint is already filled in `.github/copilot-mcp.json`.
- [ ] **SharePoint / OneDrive (defer if busy).** Follow `docs/sharepoint-onedrive-mcp-setup.md` — a one-time Azure app registration. Easy interim alternative: attach SharePoint/OneDrive files to a Copilot Space instead (zero setup).

## 🟢 Context & visibility
- [ ] **Create 10 Copilot Spaces** at <https://github.com/copilot/spaces>, one per row in `state/09_templates_prompts/spaces-mirror-register.csv`. Attach the matching `state/` folder to each. Then paste each Space link back into that CSV (replace `TODO_SPACE_LINK`, set status to `Active`) — or hand the links to the agent and it will update the file for you.
- [ ] **Projects board.** Repo **Projects > New project > Board**. Add fields: Workstream, Status, Priority, Next Action, Follow-Up Date, Owner, Revenue Impact. Add views: Revenue now, Intake triage, Active delivery, Growth backlog. Use it for visibility only; the `state/` files stay the system of record.
- [ ] **Notifications + mobile app.** Turn on notifications (avatar > **Settings > Notifications**) and install the GitHub mobile app, so you can review and merge AI pull requests from your phone.

## Light-touch safety net (recommended config)
Your preference: protect against risky/broken changes, but don't gate every minor edit. Here is the setup that matches that.

**Already done for you (automated, no clicks):**
- A validation workflow (`.github/workflows/validate-scaffolding.yml`) runs on every pull request and automatically rejects changes that break JSON, YAML, or the Spaces register. Routine content edits pass on their own — so minor changes never wait on you.

- [ ] **Add a light branch-protection rule on `main` (one-time GUI, ~2 min).** Repo **Settings > Branches > Add branch ruleset** (or **Add rule**), target branch `main`, and enable **only**:
  - ✅ **Require status checks to pass** > select the **Validate scaffolding** check. (This is the automated gate — broken changes are blocked, good ones flow through.)
  - ✅ **Require a pull request before merging**, but set **Required approvals = 0**. This keeps a clean PR trail and lets you set work in motion without approving each minor change.
  - ❌ Do **not** enable "Require approval of the most recent push" or multiple required reviewers — those are the annoying gates you want to avoid.
- [ ] **Optional - turn on auto-merge** (repo **Settings > General > Pull Requests > Allow auto-merge**). Then the agent can mark a PR auto-merge, and it merges itself the moment the validation check passes — fully hands-off for low-risk work, while still blocked if something is broken.

> Net effect: things you "set into motion" run to completion automatically; only genuinely broken or risky changes stop and ask for you.

## Deferred / decide later
- [ ] **Promote the agent team org-wide** so every repo you own inherits the same orchestrator + sub-agents. See `docs/orchestration-and-subagents.md` (create an org-level `.github` repo; the agent can prepare the files for you to copy in).
- [ ] **GitHub Pages publishing** (for approved marketing content): pick a theme, branch, and publish path when you first want to publish something public. Not needed to operate the system.
- [ ] **SharePoint write access**: only add Graph write permissions later if you want the agent to modify SharePoint content (start read-only).

## Admin reference (what's already configured in the repo)
- Verified Notion MCP endpoint + OAuth note, and the free Microsoft Learn MCP server: `.github/copilot-mcp.json`
- Pre-filled Spaces register: `state/09_templates_prompts/spaces-mirror-register.csv`
- Setup guide: `docs/copilot-setup-guide.md`
- SharePoint walkthrough: `docs/sharepoint-onedrive-mcp-setup.md`
- Automated validation gate: `.github/workflows/validate-scaffolding.yml`
