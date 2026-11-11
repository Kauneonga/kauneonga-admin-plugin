---
name: setup
description: Help an answering service admin connect Claude, ChatGPT or another AI app to their Admin Portal, and check which accounts and tools their login can reach. Use after installing the plugin, when the connection fails, or when the admin asks what the plugin can do with their login.
---

# Connect the admin connector

1. Ask the admin to connect the **Kauneonga Admin** connector through the app's own sign-in
   flow. The connector address is `https://mcp-admins.kauneonga.com/api/v2/mcp`. Never ask
   for a password, access token or API key in chat.
2. On the sign-in page they enter the web address they use for their Admin Portal, sign in
   with their own admin login, enter their two-factor code if they use one, and allow
   access.
3. Run a harmless read first: `search_accounts` or `list_accounts` with a small page, and
   show a few accounts the login can see.
4. Explain that what they can see and change follows their Admin Portal role. Buying
   numbers, porting, publishing AI receptionists and editing scripts may each need a
   permission their role doesn't have; the connector says so when it refuses.

## When it doesn't work

- **Sign-in page doesn't open or fails:** have them disconnect and reconnect the connector
  in the app's settings, then sign in again.
- **Signed in but nothing comes back:** their login may have no accounts in this area.
  Check with their administrator rather than trying another login.
- **They are a client, not an admin:** this is the wrong connector. Clients use the client
  connector, `https://mcp.kauneonga.com/api/v2/mcp`, with their client portal login.

## Connecting without sign-in

A script, a scheduled job or an AI app that can't complete the sign-in can use an **MCP
service key** instead. This plugin's connector always signs in; a key is a separate
connection the admin sets up themselves.

- **Create it:** in the Admin Portal, **My Profile > API Keys > Add New Key > MCP Service
  Key** (older portals show an **Add Admin MCP Service Key** button). Their role needs
  **MCP Connector** with Edit. Tick only the permissions the job needs, and copy the key
  right away: it is shown once.
- **Connect it:** in the app's or script's own connector settings, use their Admin Portal
  address followed by `/api/v2/mcp`, not `mcp-admins.kauneonga.com`, with the header
  `Authorization: Bearer <key>`. Never ask them to paste the key into chat.
- **What it can't do:** it works only on the platform where it was made, acts as the admin
  who made it, and always refuses bulk changes, bulk deletes and edits to a whole repeating
  series.
- **Stop it:** delete the key on the **API Keys** tab. It stops working at once.
