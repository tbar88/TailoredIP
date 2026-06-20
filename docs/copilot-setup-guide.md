# Copilot setup guide

## 1. Enable the Copilot coding agent
1. In the organization settings, enable GitHub Copilot Enterprise and confirm coding-agent access for the TailoredIP repository.
2. In repository settings, allow the Copilot coding agent to create branches, commit changes, and open pull requests.
3. Set a repository or organization variable named `COPILOT_AGENT_ASSIGNMENT_ENABLED=true` once `copilot-swe-agent` can be assigned to issues.
4. TODO: Confirm the bot appears as an assignable user on repository issues.

## 2. Enable MCP servers
- GitHub and Playwright MCP are assumed to be available by default.
- Review `.github/copilot-mcp.json` and replace each `TODO_...` placeholder with the real connector details.
- For Notion and Microsoft Graph / SharePoint, store credentials in repo or org secrets rather than committing them.
- TODO: Verify each MCP server is enabled in the GitHub Copilot admin UI for the org and repository.

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
