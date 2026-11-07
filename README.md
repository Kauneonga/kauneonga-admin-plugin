# Kauneonga Admin — connect your AI assistant

Use an AI assistant with your answering service's Kauneonga Admin Portal to review messages and reports, manage on-call calendars, update call scripts, configure phone lines, and help set up clients.

**For answering-service operators and authorized administrators.** This [plugin repository](https://github.com/Kauneonga/kauneonga-admin-plugin) is public. Sign in with your own Admin Portal account; the connector respects your existing account permissions.

## Choose your AI assistant

**MCP-only connection safety:** The full guided plugin teaches the AI to ask before making changes, but a direct MCP connection may not inherit those instructions. **Start with read-only tools.** Before allowing live-call, dispatch, phone-number, account, script, or other write actions, verify that the AI client enforces explicit confirmation of the exact target and effect, followed by result verification. If the AI client cannot restrict write tools or enforce these protections, **do not connect it to the production Admin MCP server**; use the approved full plugin or Admin Portal instead. Portal role permissions alone do not prevent unintended but authorized changes.

You **do not need to write code** to use the Claude or ChatGPT instructions below. Other applications may require an administrator to complete the connection first.

| AI assistant | How to connect | What you get |
| --- | --- | --- |
| **Claude** | Install **kauneonga-admin** from an approved plugin marketplace | **Full plugin**, including guided skills and the MCP connection |
| **ChatGPT** | Install the workspace's approved plugin, or have a ChatGPT admin add the custom MCP server | **MCP tools**; a separately distributed full plugin is needed for bundled skills |
| **Gemini Enterprise** | Ask a Gemini Enterprise administrator to connect the MCP server | **MCP tools** after OAuth and tools are configured and validated |
| **Personal Gemini** | Eligible personal accounts may add a custom app using the MCP URL | **MCP tools only**, subject to account eligibility and company security policy |
| **Gemini CLI, Codex, Cursor and other compatible agents** | Connect the MCP URL; install compatible skills separately | Tool access, with skills only where the agent supports them |

**Important:** A **full plugin** bundles task-specific skills *and* the MCP connection. An **MCP-only connection** can expose tools, but does **not automatically install** the same guided skills in every AI assistant. Exact features depend on each application's support. Installation or live sign-in in every client has not been independently verified.

**Admin MCP address:** `https://mcp-admins.kauneonga.com/api/v2/mcp`

**Before starting:** Have the normal web address for your Admin Portal, your own login, and any required two-factor authentication available. Use only AI accounts and workspaces approved by your organization for client information.

## Claude — full plugin (recommended if you want guided skills)

**Plan requirement:** Claude plugins are available on paid Claude plans (Pro, Max, Ultra, Team, or Enterprise). If you use Claude Free, you may not see the Plugins menu.

**For individual users:** the public GitHub repository can be added directly to Claude. If your Claude organization has already distributed the plugin, it may be available under **Customize > Plugins > Discover** instead.

1. Open [Claude](https://claude.ai) and select **Customize > Plugins**.
2. Select **Add > Add marketplace > Add from a repository**.
3. Enter `Kauneonga/kauneonga-admin-plugin` and add the marketplace.
4. Find **kauneonga-admin** and select **Add**. Or, if your organization already provides it, find it under **Discover**.
5. Start a chat and ask, "Which clients had the most messages this week?"
6. If prompted, connect the plugin. Enter the **web address of your usual Admin Portal** if requested, then sign in with your own credentials and complete two-factor authentication if required.

After signing in, try: **"Show me messages that still need follow-up."**

[Claude's plugin setup guide](https://support.claude.com/en/articles/13837440-use-plugins-in-claude)

## ChatGPT — connect with the MCP server

**If your ChatGPT workspace already provides Kauneonga Admin:**

1. Open [ChatGPT](https://chatgpt.com) and find the approved plugin under **Settings > Plugins** (or the **Plugins** directory).
2. Install or enable it if needed, then connect it with your **own Admin Portal login** when prompted.
3. Start a chat, type **@**, choose the Kauneonga Admin plugin, and ask a reporting question.

**If the plugin is not available:** A ChatGPT Business or Enterprise/Edu **workspace administrator** (or an authorized Enterprise/Edu developer) can set it up:

1. In ChatGPT on the web, open **Plugins**, select **+ > Add custom MCP server**.
2. Set the name to **Kauneonga Admin** and enter `https://mcp-admins.kauneonga.com/api/v2/mcp` as the server URL.
3. Set up the server's OAuth authentication, review the security warning, and select **Create as a plugin**.
4. Review the discovered tools and test the connection with an authorized Admin Portal account. Confirm read and write permissions before enabling them.
5. A workspace **admin/owner** publishes the approved connection for permitted team members.

This is **not** the same as importing the GitHub repository's guided skills. To distribute the **full** portable plugin in ChatGPT, the plugin package needs a supported OpenAI installation or distribution route; do not assume that adding the MCP URL imports its skills.

ChatGPT custom MCP support and permission controls vary by plan and workspace. [ChatGPT setup instructions](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt) · [Plugin packaging](https://developers.openai.com/plugins/build/plugins)

## Gemini — Google AI options

### Gemini Enterprise (recommended route for managed business use)

This requires setup by an **authorized Gemini Enterprise / Google Cloud administrator**, rather than an individual user simply installing the GitHub plugin.

1. In Gemini Enterprise, configure a **custom MCP server data store** for `Kauneonga Admin` using `https://mcp-admins.kauneonga.com/api/v2/mcp`.
2. Configure a supported **OAuth 2.0** integration. Google requires the relevant authorization and token URLs, client registration, scopes, and any required redirects. These must be confirmed against the server's actual OAuth configuration.
3. Verify authentication, choose which MCP tools/actions to enable, and limit access to authorized administrators.
4. Test a read-only reporting request using a permitted account before enabling administrative write actions.

**The connection is not yet confirmed as a one-click supported integration.** Your technical administrator must test the Gemini Enterprise OAuth flow and tool compatibility.

[Gemini Enterprise custom MCP setup](https://docs.cloud.google.com/gemini/enterprise/docs/connectors/custom-mcp-server/set-up-custom-mcp-server)

### Personal Gemini custom apps (eligibility and policy restrictions)

Google offers custom MCP connections in the Gemini web app for eligible **US adults using a personal Google Account** with **Keep Activity enabled**. It is **not currently available with work or school Google accounts**. This route does not install this repository's guided skills.

For an account that is both **eligible and expressly approved for the intended data**, go to [gemini.google.com](https://gemini.google.com), open **Settings > Connected Apps > Add a custom app**, enter `https://mcp-admins.kauneonga.com/api/v2/mcp`, and follow the authentication prompts. You can then select the connected app using **@** in Gemini.

**Do not connect live customer or employee information through a personal AI account without company authorization and a privacy/security review.** If approval is not in place, use a managed Claude/ChatGPT workspace or evaluate Gemini Enterprise instead. OAuth compatibility still needs testing.

[Google's Gemini custom-app instructions](https://support.google.com/gemini/answer/17209137)

## Other assistants (technical setup)

These are alternatives for people already comfortable configuring agent tools.

### Gemini CLI

Gemini CLI supports remote Streamable HTTP MCP servers with OAuth discovery. To add this connection:

```bash
gemini mcp add -t http -s user kauneonga-admin https://mcp-admins.kauneonga.com/api/v2/mcp
```

Then run `gemini mcp list` or `/mcp` and complete any prompted authorization. Gemini CLI also supports compatible Agent Skills, but those skills are separate from connecting this MCP server.

[Gemini CLI MCP documentation](https://geminicli.com/docs/tools/mcp-server/)

### Claude Code

```text
/plugin install kauneonga-admin --marketplace Kauneonga/kauneonga-admin-plugin
```

On older Claude Code versions, add the marketplace first:

```text
/plugin marketplace add Kauneonga/kauneonga-admin-plugin
/plugin install kauneonga-admin@kauneonga-admin
```

The GitHub repository is public.

### Install guided skills in compatible coding agents (npx)

If you use Codex, Cursor, or another local agent with Agent Skills support, you can install this repository's guided skills with [the skills CLI](https://github.com/vercel-labs/skills/blob/main/docs/commands.md) (Node.js required):

```bash
npx skills add Kauneonga/kauneonga-admin-plugin
```

The CLI installs skills for compatible agents; it does **not** configure the MCP server or OAuth. These instructions do not replace tool-level confirmation, access checks, or readback verification. Configure the MCP connection separately and test only read-only tools until approved.

### Cursor, Codex, and other MCP-compatible agents

Only configure production access after a security review. Add an MCP server named `kauneonga-admin`, choose **remote Streamable HTTP**, and enter `https://mcp-admins.kauneonga.com/api/v2/mcp`. Complete OAuth sign-in when supported. Follow the chosen agent's documentation for separately installing compatible skills from `skills/` in this repository. Support for remote OAuth, tool confirmations, and skill import varies by agent.

**If you only want the MCP tools in Claude**, use **Settings > Connectors > Add custom connector** and enter the same server URL. That does not install the full plugin's guided skills.

## What you can ask

- "Which clients had the most messages this week?"
- "Compare service levels this week with last week."
- "Find messages and To Dos that still need follow-up."
- "Who is on call for this client's line tonight?"
- "Help me draft a new call script."
- "Help me set up a new client account."

Start with **read-only** tasks until you are comfortable with the connection.

## Security and troubleshooting

- **Your Admin Portal permissions still apply.** Connecting an AI app does not make you an administrator or grant new privileges.
- **Review every proposed change.** Purchases, number changes, dispatch, live calls, and irreversible actions deserve extra care. Confirm the details in the Admin Portal if necessary.
- **Protect credentials.** Enter passwords and two-factor codes only in the secure sign-in flow, never in chat. Do not paste payment card information, porting PINs, or customer secrets into a conversation.
- **Can't find the plugin in Claude or ChatGPT?** Ask your organization's AI workspace administrator to publish or approve it.
- **Can't sign in?** Check the Admin Portal web address, OAuth approval and allowed client settings with your administrator; do not work around access restrictions.
- **A tool is unavailable?** The AI application may support MCP but not that specific tool, write operation, or bundled skill. Test it on a nonproduction or read-only task first.

## For Claude organization owners (one-time setup)

1. This GitHub repository is **public**. Claude currently **does not accept public github.com repositories for organization-synced marketplaces**.
2. The simplest organization-wide option is **Organization settings > Plugins & skills > Add > Upload a plugin**, using a reviewed ZIP of the plugin.
3. Alternatively, create a **private/internal marketplace repository** containing the approved plugin, then sync that private repository through **Marketplaces > Add plugins > Sync from GitHub**. Automatic sync requires GitHub Admin permission plus the Claude GitHub App's approved webhook permission; manual updates use **Re-sync**.
4. In **Inventory**, make the plugin available to the intended users or groups and verify installation under **Customize > Plugins > Discover**.

[Claude organization setup reference](https://support.claude.com/en/articles/13837433-manage-plugins-for-your-organization)


## Included guided skills

These skills are packaged with the repository; their availability in your AI assistant depends on its skill/plugin support.

| Skill | What it does |
| --- | --- |
| `kauneonga-admin` | Routes requests to the right guided workflow |
| `setup` | Checks connection and available permissions |
| `new-client` | Helps set up new client accounts |
| `numbers-and-porting` | Manages and ports phone numbers |
| `phone-lines` | Changes phone line settings |
| `call-scripts` | Writes and updates call scripts |
| `on-call-setup` | Manages on-call schedules |
| `ai-receptionists` | Builds and tests AI receptionists |
| `message-triage` | Reviews messages and To Dos |
| `reports-and-quality` | Analyzes activity and service quality |

## Privacy

See Kauneonga's [privacy policy](https://www.kauneonga.com/privacy-policy/) and [terms](https://www.kauneonga.com/terms-and-conditions/).

---

Maintaining this repository? See [docs/MAINTAINING.md](docs/MAINTAINING.md). Licensed under the [MIT License](LICENSE).
