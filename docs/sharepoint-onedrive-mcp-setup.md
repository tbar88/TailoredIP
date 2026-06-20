# SharePoint / OneDrive MCP setup walkthrough

> **Status:** This is the one setup item that is not point-and-click. It needs a one-time Microsoft Entra (Azure AD) app registration. Everything below is GUI (Azure portal), no coding. Budget ~20-30 minutes when you have time. Until then, the easy alternative is to attach SharePoint/OneDrive files directly to a Copilot Space (see the end of this doc).

## Why this step exists
There is no turnkey, hosted SharePoint/OneDrive MCP server for the GitHub Copilot coding agent today. To let the agent read your SharePoint/OneDrive content, you register a small Microsoft "app" that grants scoped access to Microsoft Graph (the API behind SharePoint and OneDrive), then point an MCP connector at it. The credentials are stored as repository secrets, never in files.

## Before you start
- You are the tenant admin (confirmed), so you can grant the permissions yourself.
- Have the TailoredIP repo open in another tab for the final secret-saving step.

## Step 1 - Register the app (Azure portal GUI)
1. Go to <https://portal.azure.com> and sign in.
2. Search for and open **Microsoft Entra ID** (formerly Azure Active Directory).
3. Left menu: **App registrations** > **+ New registration**.
4. Name it something like `TailoredIP Copilot SharePoint Connector`.
5. Supported account types: **Accounts in this organizational directory only (single tenant)**.
6. Leave Redirect URI blank. Click **Register**.
7. On the app's **Overview** page, copy these two values somewhere temporary:
   - **Application (client) ID**
   - **Directory (tenant) ID**

## Step 2 - Create a client secret
1. In the app, left menu: **Certificates & secrets** > **Client secrets** > **+ New client secret**.
2. Description: `copilot-mcp`. Expiry: choose 12 or 24 months.
3. Click **Add**, then immediately copy the **Value** column (not the Secret ID). You cannot see it again after leaving the page.

## Step 3 - Grant Microsoft Graph permissions (least privilege)
1. Left menu: **API permissions** > **+ Add a permission** > **Microsoft Graph** > **Application permissions**.
2. Add only what you need. Recommended read-only set to start:
   - `Sites.Read.All` (read SharePoint sites)
   - `Files.Read.All` (read OneDrive/SharePoint files)
3. Click **Add permissions**.
4. Click **Grant admin consent for [your tenant]** and confirm. The status should turn to a green check.

> Add write permissions (`Sites.ReadWrite.All`, `Files.ReadWrite.All`) only later, if you actually want the agent to modify SharePoint content. Start read-only.

## Step 4 - Find your SharePoint site ID (optional but recommended)
To scope the connector to specific sites rather than everything:
1. In a browser, open the SharePoint site you want to use.
2. The site ID can be retrieved via the Microsoft Learn MCP server (already enabled in this repo) by asking Copilot: "Using the Microsoft Learn docs, how do I get a SharePoint site ID for `<your site URL>`?" — or via the Graph Explorer GUI at <https://developer.microsoft.com/graph/graph-explorer>.

## Step 5 - Store the three secrets in GitHub (GUI)
1. TailoredIP repo > **Settings** > **Secrets and variables** > **Actions** > **Secrets** tab.
2. Click **New repository secret** three times and add:
   - `COPILOT_MCP_AZURE_TENANT_ID` = the Directory (tenant) ID from Step 1
   - `COPILOT_MCP_AZURE_CLIENT_ID` = the Application (client) ID from Step 1
   - `COPILOT_MCP_AZURE_CLIENT_SECRET` = the secret **Value** from Step 2

These names match the placeholders already in `.github/copilot-mcp.json`.

## Step 6 - Enable the connector
1. Repo > **Settings** > **Copilot** > **Coding agent** > **MCP servers**.
2. Set the `microsoft-graph-sharepoint` server to enabled and, if you found one, put your site ID in the `sites` list.
3. Save and let GitHub validate.

## Easy alternative (zero setup)
If you don't want to do the Azure steps now: create a **Copilot Space** and attach the specific SharePoint/OneDrive files you care about directly. The agent then has that content as context without any app registration. This covers most day-to-day needs; reserve the full MCP route for when you want the agent to browse SharePoint live.

## Security notes
- Keep permissions read-only until you have a clear reason to allow writes.
- Client secrets expire — note the expiry date you chose in Step 2 and renew before then.
- Never paste the secret value into a file, issue, or chat. It belongs only in repo **Settings > Secrets**.
