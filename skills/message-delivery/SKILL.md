---
name: message-delivery
description: Work out why a message didn't reach the right person, or reached them late - each delivery attempt, who was on call at that time on every escalation level, and how each person is set up to be reached - then propose the fix. Use when a client says someone never got a message, got it late, or the wrong person got it.
---

# Trace a message that didn't arrive

Ask, in one question if anything is missing: the client or line, roughly when the call
came in and in which time zone, the caller's name or number, who should have got the
message, and the message's short code if they have the link.

## Check, in this order

1. **Find the message:** `search_messages` by caller, number or words in it, or
   `get_message_by_short_code` from the link in a delivered message. If several match,
   list them briefly and ask which one. Don't open it with `get_message` just to trace
   it: opening a message marks it read, which changes the record you're looking into.
   If there's no message at all, the call may never have reached an agent: use
   `call-troubleshoot`.
2. **Each delivery attempt:** `list_message_activities` for its history: who it went to,
   how (call, text, email and others), when, and whether it was read, picked up or
   acknowledged. `list_message_notes` for anything agents or staff added.
3. **Who was on call then:** `list_escalation_levels` for the line, then
   `list_calendar_events` for a period covering the message's time, once for each
   level's id, including every backup level. Omitting the level id returns only the
   first level. Never substitute who's on call now for a past message.
4. **How each person is reached:** `list_delivery_methods` for each person on shift at
   that time: the number, email and method on file.

## Known causes

No message was taken, so nobody was reached:
- **Inactive account:** `get_account`. Callers to an inactive account hear a busy signal.
- **Forwarding set to always:** `get_number`. Every call is sent away before the service
  sees it.
- **An Enhanced IVR branch with nothing on it:** `get_phone_ivr`. A days, times, holidays
  or caller ID branch with nothing on it hangs up the call.
- **Spam blocker:** a caller on the blocked list is rejected before the call is answered,
  and if the account has a spam blocker turned on (`list_account_features`), callers it
  treats as spam don't reach an agent.
- **An IVR calls limit of 0:** `get_phone_ivr`. A `calls_limit` of 0 turns away every call
  dialed straight to that number with a busy signal.

A message was taken but reached the wrong person, or no one:
- **Call order:** on a shared escalation level, calls go to people in each shift's Order
  number on the calendar; shifts with no number go in the order they were added. Texts,
  emails and app alerts go to everyone on the level at once, so order only matters for
  calls. Editing a person's phone number or a shift doesn't change their place: set the
  shift's Order number (`on-call-setup`).
- **A person with no delivery method:** on shift, but nothing to reach them by.
- **A level with no shifts at that time:** nobody on that level is reached.
- **A text that never arrives:** the person may have replied STOP to the number texts come
  from. Only they can lift it, by texting START to that number.

## Report

What happened, step by step, with times in the line's time zone: whether the message was
sent, to whom, how and when, whether anyone acknowledged it, and whether that matches who
was on call and how they're set up to be reached. Keep what the records show apart from
what's likely. If the records show it went to the right person the right way but never
arrived, say so and ask support to look into delivery, rather than changing settings to
test it.

## Fix

Propose the change and hand off to the skill that makes it: `on-call-setup` for shifts,
levels, call order or how someone is reached, `call-scripts` if the script sent the
message to the wrong level, and `callbacks-and-to-dos` if a follow-up is still owed.
Confirm before any change. To check the fix, offer a test message with `create_message`,
say who it will reach, and send it only after a yes.
