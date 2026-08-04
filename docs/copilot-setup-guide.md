# Copilot setup guide

> You are the admin and sole user of the org/enterprise/repo, so you can perform every step below yourself — no separate admin is needed. Steps are written for the GitHub website (point-and-click). Do them in order; Steps 1-3 are the minimum to get the automation running.

## Quick start order (do these first)
1. Enable the Copilot coding agent (Step 1).
2. Set the assignment variable `COPILOT_AGENT_ASSIGNMENT_ENABLED=true` (Step 2 below / inside Step 1).
3. Test the automation by running a workflow by hand (Actions tab > Weekly target and signal scan > Run workflow).
4. Create one Copilot Space per workstream (Step 3) and connect Notion (Step 2 - MCP).
Everything after that is enhancement.

## 1. Enable the Copilot coding agent
1. Organization page > **Settings** > **Copilot** > enable the coding agent for the TailoredIP repository.
2. TailoredIP repo > **Settings** > **Copilot** > allow the coding agent to create branches, commit changes, and open pull requests.
3. Repo > **Settings** > **Secrets and variables** > **Actions** > **Variables** tab > **New repository variable**: name `COPILOT_AGENT_ASSIGNMENT_ENABLED`, value `true`. Do this only after the bot appears as assignable.
4. Confirm: open any Issue and check that **Copilot** shows up in the **Assignees** box.

## 2. Enable MCP servers
- GitHub and Playwright MCP are assumed to be available by default.
- Configure servers for the coding agent in repo **Settings > Copilot > Coding agent > MCP servers** (paste/validate JSON there). The repo file `.github/copilot-mcp.json` is the canonical scaffold to copy from.
- **Microsoft Learn MCP** is already enabled in the scaffold (public, no credentials, endpoint `https://learn.microsoft.com/api/mcp`). It grounds Microsoft 365/SharePoint setup answers.
- **Notion**: endpoint is `https://mcp.notion.com/mcp` and uses interactive **OAuth** sign-in. In the MCP UI, add the Notion server and authorize it (sign in to your Notion workspace) — there is no token to paste into a file. Then set `enabled` to `true`.
- **SharePoint/OneDrive**: there is no turnkey hosted MCP for the coding agent yet. It needs an Entra (Azure AD) app registration with Microsoft Graph permissions plus a Graph MCP endpoint. Store credentials as repo secrets prefixed `COPILOT_MCP_` (for example `COPILOT_MCP_AZURE_CLIENT_SECRET`). Treat this as a later step.
- Any coding-agent credential must be a repository secret whose name starts with `COPILOT_MCP_`.

## 3. Create one Copilot Space per workstream
Create Spaces that mirror these folders:
- Command Center -> `state/00_command_center/`
- Consulting Pipeline -> `state/01_consulting_pipeline/`
- Target Clients -> `state/02_target_clients/`
- Intake & Qualification -> `state/03_intake_qualification/`
- Marketing Content -> `state/04_marketing_content/`
- Consulting Delivery -> `state/05_consulting_delivery/`
- Practice Support -> `state/06_practice_support/`
- Career Opportunities -> `state/07_career_opportunities/`
- Business Growth -> `state/08_business_growth/`
- Work-Product Refinement -> `state/10_work_product_refinement/`

Update `state/09_templates_prompts/spaces-mirror-register.csv` with the Space owner and mirror status once created.

## 4. Map pipeline and intake onto a GitHub Projects board
Suggested fields:
- Workstream
- Status
- Priority
- Next Action
- Follow-Up Date
- Owner
- Revenue Impact

Suggested views:
- Revenue now
- Intake triage
- Active delivery
- Growth backlog

Link items back to the canonical CSV trackers and only use Projects for workflow visibility, not as the system of record.

## 5. Publish approved content via GitHub Pages
1. Keep approved content source material in `state/04_marketing_content/` and supporting drafts in the relevant issue or PR.
2. Use a Pages-enabled branch or `docs/` publishing flow only after content is approved.
3. Reserve the publishing step for assets that have passed the Validator and PR checklist.
4. TODO: Pick the actual Pages theme, branch, and publish path.

## 6. Model and data routing note
- Client-confidential inputs should stay on approved models, agents, connectors, and storage paths.
- Use retention-heavy or wide-sharing paths only for Tomasz's own work product, approved marketing assets, or intentionally public materials.
- If a task mixes confidential and public materials, split the work so sensitive inputs do not travel through the public path.
