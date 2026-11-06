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
- Webhook tools can call a client's own API, such as opening a ticket in their CRM:
  `{name}` in the address for a value in the path, query and body fields (dotted body
  names nest), and fixed values sent on every call that the assistant never sees, such
  as a ticket type. The shape is in `update_ai_assistant_tool`'s description. An API key
  is stored by an admin in the builder (the endpoint's Authentication tab, Stored key);
  never ask for one in the chat or put one in the settings. Before going live, run
  `test_ai_assistant_webhook` with sample values (confirm first: the client's system
  acts on it), then a test call.
- `get_ai_assistant_review` ranks what to fix, such as no way to reach a person, or
  prices it shouldn't quote. Run it before publishing.

## Test

`test_call_ai_assistant` places a real call to the number the admin gives, from the
assistant's number. Use the admin's own phone and confirm it first.

## Publish

1. `assign_ai_assistant` makes it the line's main assistant. Nothing changes for callers
   yet.
2. Publish any handoff assistants first, so the main one can reach them.
3. Say exactly which number will start being answered by the AI, then
   `publish_ai_assistant` only once the admin confirms.
4. `unpublish_ai_assistant` takes it off the number. `archive_ai_assistant` and
   `restore_ai_assistant` put a retired assistant away or bring it back.

## How it's doing

- `list_ai_assistant_conversations` and `get_ai_assistant_conversation` for what callers
  asked and how it answered.
- `get_ai_assistant_knowledge_gaps` lists questions it couldn't answer. Offer to add the
  answers to its knowledge.
- `forget_ai_assistant_caller_memory` erases what it remembers about one caller's number,
  for a "forget me" request. It can't be undone.
