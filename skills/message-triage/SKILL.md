---
name: message-triage
description: Find and review the messages your agents took for clients, separate what needs action now from what can wait, and record what was done with notes, status changes and follow-up To Dos. Use when catching up on a client's messages, looking for a specific call, or checking for anything urgent.
---

# Messages and To Dos

Work from what was recorded, not from assumptions about what a caller meant.

## Find

- A client's recent messages: `list_recent_messages` or `list_messages`, filtered by
  account.
- A specific caller or subject: `search_messages`. A message's short code:
  `get_message_by_short_code`.
- One message in full: `get_message`, its notes with `list_message_notes`, its history
  with `list_message_activities`, and its recording with `list_message_call_recording`.

Messages carry caller details and, for medical clients, health information. Share only
what the admin needs, and keep it out of tool calls and messages that don't need it.

## Sort

Lead with what needs action now: anything flagged as an emergency, a caller whose situation
gets worse with time, a second call from the same person, or a message nobody has
acknowledged past its escalation window. Then what needs a reply today, then the rest as
counts. Point out patterns: repeat callers, a spike from one number, messages that should
have paged someone but didn't.

## Act

- `create_message_note` to record what was done. `delete_message_note` removes one.
- `update_message`, `mark_message_read`, `mark_message_unread`, `acknowledge_message`,
  and `create_message` for a new one.
- Follow-ups: `list_to_dos` first so you don't duplicate one, then `create_to_do` or
  `delete_to_do`. A To Do can place real calls or send texts and emails, so say who it
  reaches and when, and get a yes.

Confirm each change, then read the result back. Never report a change that didn't succeed.
