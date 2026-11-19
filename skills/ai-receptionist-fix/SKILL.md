---
name: ai-receptionist-fix
description: Fix a live AI receptionist that answers badly - talks too long, reads out long lists, gets facts wrong, repeats itself, won't transfer, or takes the wrong message - by finding the call that went wrong, working out why, making one targeted change, then publishing and test-calling it. Use when a client or one of your staff says the AI said or did the wrong thing.
---

# Fix an AI receptionist that answers badly

Ask, in one question if anything is missing: the client or number, roughly when, what the
caller said, and what the AI did wrong.

## 1. Find the assistant and the call

1. Find the assistant as in `ai-receptionists` ("Find the assistant"): `search_accounts`
   with a short part of the name, then `ai_assistant_id` from `get_phone`, or
   `list_ai_assistants` with `phone_id`.
2. `get_ai_assistant`: its greeting, instructions, language, tool cards
   (`settings.tools`) and knowledge base files.
3. `list_ai_assistant_conversations`, then `get_ai_assistant_conversation` for the call
   that matches the time and what was said. Caller details are personal data: summarize,
   and quote only the lines that show the problem.

## 2. Work out why

| What went wrong | Usually comes from | Fix with |
|---|---|---|
| Talks too long, reads out a long list | No rule on answer length or lists, while the knowledge base or a tool returns a whole catalog | A rule in the instructions (below) |
| Wrong or made-up facts | The fact is missing from the instructions or knowledge base | Add it. `get_ai_assistant_knowledge_gaps` shows other gaps |
| Won't transfer, or transfers to the wrong place | The transfer card's target or when-to-transfer wording | `update_ai_assistant_tool` on `transfer`. Goes live at once |
| Asks the same thing twice, or loops | The instructions ask it in two places, or a workflow step | The instructions, or the workflow |
| Wrong language or voice | `language` or `voice` | `update_ai_assistant` |
| Message missing details | The message fields in the instructions | The instructions |
| Message reached the wrong person | The line's on-call setup, not the AI | `on-call-setup` |
| A lookup or booking failed | The webhook endpoint | `test_ai_assistant_webhook` (confirm first: the client's system acts on it) |

`get_ai_assistant_review` lists other build problems. Show the admin the transcript line
where it went wrong and the setting or instruction that caused it. If the call shows nothing
wrong, say so rather than changing anything.

## 3. Propose one change

Show the exact text to add or replace and what callers will notice. Change only what fixes
this problem; don't rewrite the instructions or run `improve_ai_assistant_prompt` on them.
Wait for a yes.

A rule for long lists, to adapt: "When a caller asks what you have, name two or three
popular choices in one sentence, then ask one question to narrow it down. Never read more
than three items. Offer to text the full list."

## 4. Make it live and check it

1. Save it (`update_ai_assistant`, or `update_ai_assistant_tool` for a card) and read it
   back with `get_ai_assistant`.
2. Instructions and settings reach callers only on publish. Say which number, confirm,
   then `publish_ai_assistant`. A tool card is already live.
3. `test_call_ai_assistant` to the admin's own phone (confirm first), and repeat what the
   caller said. The test call creates a message for whoever gets the line's messages
   (`message_recipients` on `get_phone`).
4. Report what changed and what the test call showed. If it's still wrong, go back to step 2.
   If callers are being hurt in the meantime, `unpublish_ai_assistant` sends the line back to
   the normal call flow: confirm first.
