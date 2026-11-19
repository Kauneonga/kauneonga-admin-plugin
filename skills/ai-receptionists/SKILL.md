---
name: ai-receptionists
description: Create, change, test and publish an AI receptionist that answers a client's calls or web chats - its greeting, instructions, voice, languages, knowledge base, workflow and tools - and review its conversations. Use when a client wants an AI receptionist or a change to one. When a live one is answering badly, use ai-receptionist-fix.
---

# AI receptionists

## What reaches callers, and when

Most changes are drafts until the next publish. Some reach callers at once.

| Change | Tools | Callers get it |
|---|---|---|
| Greeting, instructions, voice, language, other settings | `create_ai_assistant`, `update_ai_assistant` | On the next publish |
| Knowledge base | `create_ai_assistant_kb_file`, `delete_ai_assistant_kb_file`, `build_ai_assistant_knowledge_base` | On the next publish |
| Adding or removing a shared tool | `add_ai_assistant_shared_tool`, `remove_ai_assistant_shared_tool` | On the next publish |
| A tool card: transfer, webhooks, hang up, call logging, keypad, handoff | `update_ai_assistant_tool` | **At once**, on every assistant that uses the tool. Turning a tool on or off waits for the next publish |
| Workflow on, off or deleted | `enable_ai_assistant_workflow`, `disable_ai_assistant_workflow`, `delete_ai_assistant_workflow` | **At once** |
| Publish, unpublish, archive, restore | `publish_ai_assistant`, `unpublish_ai_assistant`, `archive_ai_assistant`, `restore_ai_assistant` | **At once** |

Before an "at once" change, say what callers will notice and on which number, and wait for
a yes. A reply saying a change is waiting for approval or was not executed changed nothing:
say so and don't retry it.

## Find the assistant

1. `search_accounts` with a short part of the name, such as "North" for Northwind Dental, or
   the phone number. A full name can miss a different spelling or spacing.
2. `get_phone` gives `ai_assistant_id`, the line's main assistant. Or call
   `list_ai_assistants` with `phone_id` (get_phone's numeric `id`, not its uuid),
   `account_id` or `name`. Don't read the unfiltered list: it covers every client and gets
   cut off.
3. If neither shows it, ask the admin for the number at the end of the assistant's address
   in the AI assistant builder.

`list_archived_ai_assistants` finds a retired one.

## Read before you change

`get_ai_assistant` returns everything, including `message_recipients` (who gets the line's
messages). `update_ai_assistant` merges `settings` into the current ones, but a list inside
them is replaced whole: send only what changes, and when you edit a list, send all of it.
`update_ai_assistant_tool` needs the whole card: copy `settings.tools.<section>` from
`get_ai_assistant` and change only what was asked.

## Create

1. Check the line doesn't already have one (above).
2. `scan_website_for_ai_assistant` reads the client's site for services, hours and contact
   details. It saves nothing.
3. `list_ai_assistant_voices`, filtered by language.
4. `create_ai_assistant` makes a draft that answers nothing. Write the greeting and
   instructions for the ear (below).
5. `get_ai_assistant_review` ranks what to fix, such as no way to reach a person, or prices
   it shouldn't quote. Run it before publishing.

## Write for the ear

Callers hear every word, and can't skim.

- The greeting is one or two sentences, with no lists.
- The instructions say to keep answers to a sentence or two and to ask one question at a
  time.
- Never read a list aloud. When a caller asks what's available (menu, products, services,
  times), the assistant names two or three and asks one question to narrow it down, or
  offers to text the full list. Say this in the instructions whenever the knowledge base or
  a tool can return a catalog.
- Keep prices, callback times and promises out unless the client agreed to them.
- `improve_ai_assistant_prompt` rewrites instructions in general terms; it doesn't know what
  went wrong on a call. Show its suggestion and save only what the admin accepts.

## Knowledge, workflow and tools

- Knowledge: `create_ai_assistant_kb_file` adds a web page or a text document,
  `delete_ai_assistant_kb_file` removes one, then `build_ai_assistant_knowledge_base`
  indexes them.
- Workflow: `generate_ai_assistant_workflow` drafts the steps a call moves through. Save it
  as `settings.conversation_flow` with `update_ai_assistant`.
- Tools: `list_ai_assistant_shared_tools`, `add_ai_assistant_shared_tool`,
  `remove_ai_assistant_shared_tool` and `update_ai_assistant_tool`.
  `register_ai_assistant_mcp_server` connects one of the client's own MCP servers; its token
  is stored securely, never in the chat.
- Webhook tools can call a client's own API, such as opening a ticket in their CRM:
  `{name}` in the address for a value in the path, query and body fields (dotted body
  names nest), and fixed values sent on every call that the assistant never sees, such
  as a ticket type. The shape is in `update_ai_assistant_tool`'s description. An API key
  is stored by an admin in the builder (the endpoint's Authentication tab, Stored key);
  never ask for one in the chat or put one in the settings. Before going live, run
  `test_ai_assistant_webhook` with sample values (confirm first: the client's system
  acts on it), then a test call.

## Other languages

- **One voice:** language `auto` answers callers in the language they speak.
- **A native voice per language:** one assistant per language, such as "Front Desk
  Spanish" with language `es` and a voice from `list_ai_assistant_voices`. Publish each
  language assistant first (a handoff assistant only syncs), then save the main
  assistant's `agent_handoff` card with `update_ai_assistant_tool`, naming each language
  assistant and when to hand over (the caller speaks that language). Handoff targets must
  be active assistants on the same line. The main greeting can invite callers to speak
  those languages.

## Test

`test_call_ai_assistant` rings the number the admin gives and connects it to the
**published** assistant, so a draft change can't be heard until it's published. Use the
admin's own phone and confirm first.

Every call the assistant logs becomes a message to whoever gets the line's messages, test
calls included. Check `message_recipients` on `get_phone` first. If it's the client, say so
and offer to point the line's messages to your own staff first (`on-call-setup`, "Cover
for a while").

## Publish

1. `assign_ai_assistant` makes it the line's main assistant. Nothing changes for callers
   yet.
2. Publish any handoff assistants first, so the main one can reach them.
3. Re-read it with `get_ai_assistant`. Show the greeting and the start of the
   instructions callers will get, the number that will start being answered by the AI,
   and who will get its messages. `publish_ai_assistant` only after a yes.
4. If publishing is refused with problems to fix, such as placeholder text (TODO, TBD) or
   an API key typed into a webhook card, fix each one and publish again. The connector
   can't skip this check. Pass on any warnings a successful publish returns.
5. `unpublish_ai_assistant` takes it off the number. `archive_ai_assistant` and
   `restore_ai_assistant` put a retired assistant away or bring it back.

## How it's doing

- `list_ai_assistant_conversations` and `get_ai_assistant_conversation` for what callers
  asked and how it answered. Caller details are personal data: summarize.
- `get_ai_assistant_knowledge_gaps` lists questions it couldn't answer. Offer to add the
  answers to its knowledge.
- `forget_ai_assistant_caller_memory` erases what it remembers about one caller's number,
  for a "forget me" request. It can't be undone.
