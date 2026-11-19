---
name: callbacks-and-to-dos
description: Work out why a callback or follow-up didn't happen - a caller who asked to be called back while waiting, a To Do that didn't call, text or email, or a follow-up on a message that nobody did - from the call, the To Dos and their records, and the message's history - then propose the fix. Use when a client says someone was promised a call back or a follow-up that never came.
---

# A callback or follow-up that didn't happen

Ask, in one question if anything is missing: the client or line, who should have been
contacted and at which number or email, roughly when, and what was promised: a callback
the caller asked for while waiting, a To Do, or a follow-up on a message.

## Check, in this order

1. **A callback the caller asked for:** `list_inbound_calls` for the line in a tight time
   window, matched on the caller's number, then `get_call`. Its status and callback times
   show whether it was waiting for a callback, was canceled, or the call back didn't
   reach the caller. If it was canceled, look for another call from the same number just
   before.
2. **A To Do:** `list_to_dos` for the account: whether it exists, its schedule, how it
   reaches people (call, text or email) and whom. A To Do that was never set up never
   ran. Then `list_to_do_detail_records` for the time window: whether it ran, when, and
   for how long.
3. **A follow-up on a message:** find the message (`search_messages` or
   `get_message_by_short_code`), then `list_message_activities` for each delivery attempt
   and status change, and `list_message_notes` for what agents or staff wrote.

## Known causes

- **A shared caller ID:** where several accounts or callers share one caller ID, a new
  call from that number can cancel another account's pending callback. A callback
  canceled minutes after another call from the same number points to this; say so and ask
  support to look into it.
- **A To Do texting someone who opted out:** if they texted STOP to the number it sends
  from, only they can lift it, by texting START to that number.
- **Nobody was asked to follow up:** the message was delivered and acknowledged, but no
  note or To Do records a follow-up. That's a process gap, not a fault.

## Report

What was promised, what the records show happened, and when, in the line's time zone. Keep
what the records show apart from what's likely.

## Fix

- **A follow-up that's still owed:** `list_to_dos` first so you don't duplicate one, then
  offer `create_to_do`. Say who it reaches, how (call, text or email), what it says and
  when, and get a yes. It places real calls or sends real texts and emails from the
  client's own number, so never use one to test alerts; to test delivery, use
  `message-delivery`.
- **Coverage or routing:** `on-call-setup` for who's reached, `phone-lines` for the
  line's menu and queue.

Confirm before any change.
