---
name: ai-receptionists
description: Create, improve, test and publish an AI receptionist that answers a client's calls or web chats - its greeting, instructions, voice, knowledge base, workflow and tools - and review its conversations. Use when a client wants an AI receptionist, or when an existing one needs to change or isn't answering well.
---

# AI receptionists

Everything you change is a draft until it's published. Publishing points the client's real
number at the AI right away, so it's the one step that reaches callers.

## Create

1. Find the line, then `list_ai_assistants` (and `list_archived_ai_assistants`) to see
   whether it already has one.
2. `scan_website_for_ai_assistant` reads the client's website for services, hours and
   contact details. It saves nothing.
3. `list_ai_assistant_voices` for the voice.
4. `create_ai_assistant` makes a draft that isn't answering anything. Set the greeting
   (the first thing callers hear) and the instructions.

## Improve

- `update_ai_assistant` edits the draft: name, greeting, instructions, voice, language
  and other settings.
- `improve_ai_assistant_prompt` suggests better instructions.
- Knowledge: `list_ai_assistant_kb_files` shows what it knows.
  `create_ai_assistant_kb_file` adds a web page or a text document,
  `delete_ai_assistant_kb_file` removes one, then `build_ai_assistant_knowledge_base`
  indexes them.
- Workflow: `generate_ai_assistant_workflow` drafts the steps a call moves through.
  Save it with `update_ai_assistant`, then turn it on or off with
  `enable_ai_assistant_workflow` or `disable_ai_assistant_workflow`.
  `delete_ai_assistant_workflow` removes it.
- Tools: `list_ai_assistant_shared_tools`, `add_ai_assistant_shared_tool`,
  `remove_ai_assistant_shared_tool` and `update_ai_assistant_tool`.
  `test_ai_assistant_webhook` checks a webhook tool. `register_ai_assistant_mcp_server`
  connects one of the client's own MCP servers; its token is stored securely, never in
  the chat.
- `get_ai_assistant_review` ranks what to fix, such as no way to reach a person, or
  prices it shouldn't quote. Run it before publishing.

## Test

`test_call_ai_assistant` places a real call to the number the admin gives, from the
assistant's number. Use the admin's own phone and confirm it first.

Every call the assistant logs becomes a message to whoever is on call for the line, test
calls included. Before a test call, `get_phone` shows who that is (`message_recipients`).
If it's the client, say so and offer to point the line's messages to your own staff first
(`on-call-setup`, "Cover for a while").

## Publish

1. `assign_ai_assistant` makes it the line's main assistant. Nothing changes for callers
   yet.
2. Publish any handoff assistants first, so the main one can reach them.
3. Say exactly which number will start being answered by the AI and who will get its
   messages (`message_recipients` on `get_phone` or `get_ai_assistant`), then
   `publish_ai_assistant` only once the admin confirms.
4. `unpublish_ai_assistant` takes it off the number. `archive_ai_assistant` and
   `restore_ai_assistant` put a retired assistant away or bring it back.

## Other languages

- **One voice:** language `auto` answers callers in the language they speak.
- **A native voice per language:** one assistant per language, such as "Front Desk
  Spanish" with language `es` and a voice from `list_ai_assistant_voices`. Publish each
  language assistant first (a handoff assistant only syncs), then save the main
  assistant's `agent_handoff` tool card with `update_ai_assistant_tool`, naming each
  language assistant and when to hand over (the caller speaks that language). Handoff
  targets must be active assistants on the same line. The main greeting can invite
  callers to speak those languages.

## How it's doing

- `list_ai_assistant_conversations` and `get_ai_assistant_conversation` for what callers
  asked and how it answered.
- `get_ai_assistant_knowledge_gaps` lists questions it couldn't answer. Offer to add the
  answers to its knowledge.
- `forget_ai_assistant_caller_memory` erases what it remembers about one caller's number,
  for a "forget me" request. It can't be undone.
