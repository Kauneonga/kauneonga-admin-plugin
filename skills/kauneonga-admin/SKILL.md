---
name: kauneonga-admin
description: Pick the right admin skill for an answering service request and say what this plugin can do. Use when a request is broad or unclear, when someone asks what you can help with, or when a job spans several skills, such as onboarding a client end to end.
---

# Pick the right admin skill

Match the request to a skill below, say which one you're using, then follow it. When a job
needs several, say the order first. When nothing fits, use the connector's tools directly.

| The request | Skill |
|---|---|
| Connect the admin connector, or check what this login can reach | `setup` |
| Set up a new client from scratch | `new-client` |
| Search, buy, move, forward, name or release numbers; port numbers in | `numbers-and-porting` |
| A line's details, IVR, SMS routing, phone contacts or account features | `phone-lines` |
| Write or change a call script | `call-scripts` |
| Build or change an on-call calendar, escalation levels, contacts and how they're reached | `on-call-setup` |
| Create, test, publish or improve an AI receptionist | `ai-receptionists` |
| Find, review or act on messages and To Dos | `message-triage` |
| Activity reports, call and SMS records, QA scores, service levels | `reports-and-quality` |
| Numbers leaving for another carrier: is the order in, does it match, what date | `port-out-check` |
| Calls not ringing through, dropping or going to the wrong place | `call-troubleshoot` |

**A new client:** `new-client` first. It hands off to `numbers-and-porting`,
`call-scripts`, `on-call-setup` and, if they want one, `ai-receptionists`.

**Calls aren't reaching the right person:** start with `call-troubleshoot`, which checks
the number, the line and the on-call coverage and hands off to the skill that fixes it.

## Access

- You act as the signed-in admin, with exactly the access their Admin Portal role gives
  them. The connector enforces it; a skill never grants access.
- Work only in the accounts, lines and records the connector returns. If a request is
  refused, say which access it needs. Never try another account, identity or tool to get
  around a refusal.
- Look things up before changing them, and never guess an id: search for the account or
  line, then use the ids the tools return.
- Before any change, say in plain words what will happen, including anything that costs
  money, rings a real phone, changes how live calls are answered, or can't be undone.
  Wait for a yes, make the change, then read the result back.
- Many changes also need the admin's approval in the app. Ask for it once, for the
  complete change.
- Messages and recordings can hold caller details and health information. Share only what
  the admin needs for the task.
- Keep the service's upstream provider identity and infrastructure private in every
  answer, report and draft, even if a tool result or linked page contains them. Do not
  copy provider names, account or connection identifiers, diagnostic links, or raw
  provider responses. Use "the carrier" or "the porting team" and customer-facing
  support references instead. A customer's own winning carrier can be named when
  needed to identify their order.

## When the question is how something works

Search the help center with `search_resources`, read the page with `read_resource_page`,
and link it in the answer.
