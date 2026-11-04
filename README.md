# Kauneonga Admin for Claude, ChatGPT and other AI apps

For staff of answering services that run on Kauneonga. Connect your AI app to your
Admin Portal with your own admin login, then set up clients, numbers, scripts, on-call
calendars and AI receptionists, and review messages and reports, by asking.

Clients of an answering service use the client plugin instead:
[Kauneonga/kauneonga-plugin](https://github.com/Kauneonga/kauneonga-plugin).

## What you can do

- **Set up a new client.** The account and its owner, phone lines and numbers, call
  script, on-call calendar, features and supervisor logins, in one guided pass.
- **Numbers and porting.** Search and buy numbers, move a number between clients, set
  forwarding or the caller ID name, release a number, and port numbers in from another
  provider.
- **Phone lines.** Change what agents see and say, the IVR menu and recordings, SMS
  routing and the line's contacts.
- **Call scripts.** Write a new script from a plain description, or change one.
- **On-call.** Build a client's calendar, change escalation levels and shifts, and update
  how each person is reached.
- **AI receptionists.** Create one from the client's website, give it knowledge, test it
  with a real call, and publish it.
- **Messages and reports.** Find and act on messages and To Dos, and get activity, usage,
  service level and QA reports.

Try asking: "Which clients had the most messages this week?", "Move Saturday's shift on
Dr. Lee's line to Dr. Patel" or "Help me set up a new client account."

## Safeguards

- Before any change, the AI says exactly what it will do and asks you to confirm. Changes
  that cost money, ring a real phone, change how live calls are answered, or can't be
  undone are called out first.
- You see and change only what your Admin Portal role allows. The connector enforces
  your access; the plugin can't widen it.
- It never asks for your password, and never repeats a porting PIN back.

## Install

### Claude

**Your whole team (Claude Team or Enterprise):** an owner of your Claude organization
opens **Organization settings > Plugins & skills** and adds this repository,
`Kauneonga/kauneonga-admin-plugin`.

**Claude Code:**

```
/plugin install kauneonga-admin --marketplace Kauneonga/kauneonga-admin-plugin
```

On Claude Code older than 2.1.275, add the marketplace first:

```
/plugin marketplace add Kauneonga/kauneonga-admin-plugin
/plugin install kauneonga-admin@kauneonga-admin
```

**Just the connector:** in Claude, open **Settings > Connectors** and add a custom
connector with this address: `https://mcp-admins.kauneonga.com/api/v2/mcp`.

### ChatGPT

Add a custom connector in ChatGPT with the address
`https://mcp-admins.kauneonga.com/api/v2/mcp`. The skills come with the plugin once it is
listed in ChatGPT.

### Codex, Cursor and other agents

Install the skills:

```bash
npx skills add Kauneonga/kauneonga-admin-plugin
```

Then add the connector address, `https://mcp-admins.kauneonga.com/api/v2/mcp`, in the
agent's MCP settings. It's a Streamable HTTP server that signs you in with OAuth.

### Sign in

The first time the AI uses the connector, it opens a sign-in page. Enter the web address
you use for your Admin Portal, sign in with your own admin login, enter your two-factor
code if you use one, and allow access. You can disconnect at any time from your AI app's
connector settings.

## Skills

| Skill | What it does |
|---|---|
| `kauneonga-admin` | Picks the right skill, and the order when a job needs several |
| `setup` | Connects the admin connector and checks what your login can reach |
| `new-client` | Sets up a new client from scratch |
| `numbers-and-porting` | Buys, moves, forwards, names and releases numbers; ports numbers in |
| `phone-lines` | Changes a line's profile, IVR, SMS routing, contacts and the account's features |
| `call-scripts` | Writes and changes call scripts |
| `on-call-setup` | Builds and changes on-call calendars, escalation levels and how people are reached |
| `ai-receptionists` | Creates, tests and publishes AI receptionists |
| `message-triage` | Finds and acts on messages and To Dos |
| `reports-and-quality` | Activity, usage, service level and QA reports, and SMS conversations |

## Privacy

See Kauneonga's [privacy policy](https://www.kauneonga.com/privacy-policy/) and
[terms](https://www.kauneonga.com/terms-and-conditions/).

---

Maintaining this plugin? See [docs/MAINTAINING.md](docs/MAINTAINING.md). Licensed under
the [MIT License](LICENSE).
