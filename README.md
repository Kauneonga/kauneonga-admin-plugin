# Kauneonga Admin plugin

Use Claude to work with your answering service's Kauneonga Admin Portal in plain English. You can review messages and reports, manage on-call schedules and call scripts, configure phone lines, set up clients, and more.

**For authorized answering-service administrators.** This plugin works with your own Admin Portal login and cannot grant permissions beyond the role you already have.

Are you an answering-service **client** rather than an administrator? Use the separate [Kauneonga client plugin](https://github.com/Kauneonga/kauneonga-plugin) instead.

## Set up in Claude (no technical experience needed)

You do **not** need to install software, use a terminal, or write code. The plugin's [GitHub repository](https://github.com/Kauneonga/kauneonga-admin-plugin) is public, so you do not need an invitation to view it.

**Before you start**, have your usual Admin Portal web address and login ready. You need a Claude account with plugin support.

### 1. Add Kauneonga Admin to Claude

1. Open [Claude](https://claude.ai) and sign in.
2. In the left sidebar, select **Customize > Plugins**.
3. Click **Add > Add marketplace > Add from a repository**.
4. Paste this repository name:

   `Kauneonga/kauneonga-admin-plugin`

5. Add the marketplace. Find **kauneonga-admin** in its plugin list and click **Add** to install it.

If your Claude organization has already made the plugin available, you may find it under **Customize > Plugins > Discover** instead. In that case, just click **Add**.

### 2. Connect your Admin Portal

1. Start a new conversation in Claude.
2. Ask: **"Which clients had the most messages this week?"**
3. When asked to connect Kauneonga Admin, choose **Connect** or **Allow**.
4. If prompted, enter the **web address you normally use to access your Admin Portal**.
5. Sign in on the secure Admin Portal sign-in page using **your own** credentials, complete two-factor authentication if required, and authorize access.

Only enter your password on the Admin Portal sign-in page, **not** in a Claude chat.

### 3. Try a few questions

- "Which clients had the most messages this week?"
- "How have our service levels changed this week?"
- "Who is on call for this client's line tonight?"
- "Find messages that still need follow-up."
- "Help me create a call script for a new client."

You can start with reports and message searches before asking Claude to make changes.

### If something isn't working

- **Can't find "Add marketplace"?** Your Claude organization may restrict custom marketplaces. Ask your Claude account owner to approve or distribute the plugin.
- **Added the marketplace, but don't see Kauneonga Admin?** Return to **Customize > Plugins**, open the added marketplace, and add **kauneonga-admin** from its list.
- **Sign-in asks for a portal address?** Use your normal Admin Portal web address, not the GitHub link or the MCP connector address.
- **Access denied or data missing?** Your Admin Portal permissions still apply. Ask your portal administrator to verify your account's access.
- **Asked to confirm a change?** Review what Claude is about to do before approving it.

See Anthropic's [Use plugins in Claude](https://support.claude.com/en/articles/13837440-use-plugins-in-claude) help article for the latest interface instructions.

## For Claude organization owners: making it available to staff

You can offer the plugin to your team so employees do not have to add the GitHub marketplace individually.

**Important:** This repository is **public**. Anthropic currently **does not allow public GitHub repositories to be used directly as organization-synced marketplaces**. That restriction is different from adding the public repository as a *personal* marketplace above.

Organization owners have two options:

1. **Manual organization installation:** Prepare a Claude-compatible plugin ZIP from the approved repository contents. In Claude, go to **Organization settings > Plugins & skills**, choose **Add > Upload a plugin**, and distribute it to authorized members or groups.
2. **GitHub-synced organization marketplace:** Maintain an approved **private or internal** marketplace repository, then use **Organization settings > Plugins & skills > Marketplaces > Add plugins > Sync from GitHub** with that repository. Do not try to sync this public repository directly.

For option 2, Claude starts with **Sync automatically** enabled. Turning that on or off requires **GitHub Admin access** to the synced repository and the Claude GitHub App's approved **Webhooks (Read & Write)** permission for automatic syncing. If you only have GitHub Read access, **turn off "Sync automatically"** during setup and use **Re-sync** manually for future updates.

After distributing the plugin, confirm that an authorized employee can find it under **Customize > Plugins > Discover** and sign in with their own Admin Portal account.

See Anthropic's [Manage plugins for your organization](https://support.claude.com/en/articles/13837433-manage-plugins-for-your-organization) guide for setup and permission requirements.

## What you can do

- **Reports and quality:** Review activity, usage, service levels, QA reports, and SMS conversations.
- **Messages:** Find and act on messages and To Dos.
- **On-call:** Review and update on-call shifts, escalation levels, and contact methods.
- **Phone lines and scripts:** Manage line settings, IVR, SMS routing, contacts, features, and call scripts.
- **New clients:** Set up an account, phone numbers, a script, an on-call calendar, and authorized users.
- **Numbers and porting:** Search, buy, move, forward, release, and port phone numbers.
- **AI receptionists:** Create, test, and publish an AI receptionist.

## Safeguards

- **Your Admin Portal role controls access.** The connector cannot increase your permissions.
- **Changes require confirmation.** Claude calls out actions involving cost, live calls, or changes that may be difficult to reverse.
- **Use your own credentials.** Never share passwords, two-factor codes, or porting PINs in chat.
- **Do not enter payment card information into a chat.**

## Other ways to connect (technical users)

These options are for users who already work with developer tools. If you just want to use Claude chat, follow **Set up in Claude** above.

### Claude Code

```text
/plugin install kauneonga-admin --marketplace Kauneonga/kauneonga-admin-plugin
```

On Claude Code versions older than 2.1.275, add the marketplace first:

```text
/plugin marketplace add Kauneonga/kauneonga-admin-plugin
/plugin install kauneonga-admin@kauneonga-admin
```

### MCP connector only (without the plugin's guided skills)

In Claude, open **Settings > Connectors**, add a custom connector, and enter:

`https://mcp-admins.kauneonga.com/api/v2/mcp`

This connects Claude to the Admin Portal, but does not include the plugin's guided skills.

### ChatGPT

Add a custom connector in ChatGPT with the address above. The plugin's skills can be included when the full plugin package is supported and installed.

### Codex, Cursor, and other agents

Install the skills:

```bash
npx skills add Kauneonga/kauneonga-admin-plugin
```

Then add `https://mcp-admins.kauneonga.com/api/v2/mcp` in the agent's MCP settings. The server uses OAuth for sign-in.

## Plugin skills

| Skill | What it does |
| --- | --- |
| `kauneonga-admin` | Picks the right skill and coordinates multiple steps |
| `setup` | Connects and checks Admin Portal access |
| `new-client` | Sets up new clients |
| `numbers-and-porting` | Manages and ports phone numbers |
| `phone-lines` | Changes line settings |
| `call-scripts` | Writes and updates scripts |
| `on-call-setup` | Manages on-call schedules |
| `ai-receptionists` | Creates, tests, and publishes AI receptionists |
| `message-triage` | Reviews messages and To Dos |
| `reports-and-quality` | Provides reporting and quality analysis |

## Privacy

See Kauneonga's [privacy policy](https://www.kauneonga.com/privacy-policy/) and [terms](https://www.kauneonga.com/terms-and-conditions/).

---

Maintaining this plugin? See [docs/MAINTAINING.md](docs/MAINTAINING.md). Licensed under the [MIT License](LICENSE).
