---
name: texting-troubleshoot
description: Work out why texts to or from a client's number aren't arriving, are going to the wrong place, or stopped after someone opted out - from the line's SMS routing, its SMS conversations and the SMS records - then propose the fix. Use when a client or caller says texts aren't getting through or are reaching the wrong people.
---

# Troubleshoot texting

Ask, in one question if anything is missing: the client's number, the other person's
number, which way the texts went (to the line or from it), and roughly when, in which time
zone.

## Check, in this order

1. **Opt-out:** if the person ever texted STOP to this number, texts to them are blocked
   until they text START to that same number. Ask them to do that first; it's the most
   common cause. Opt-out status can't be read from here, so say that, and if START
   doesn't fix it, ask support to check.
2. **Routing:** find the line (`search_accounts` with the number, then `get_phone`), then
   `list_phone_sms_routing`: whether texts to this number go to the client's inbox, to
   the agents, or to a schedule that switches between them by day and time.
3. **The conversation:** `list_open_sms_conversations` and
   `list_closed_sms_conversations`, or `list_sms_conversations`, for the line, matched on
   the other person's number and the time. Then `get_sms_conversation` and
   `list_sms_conversation_messages` for what was sent and received, and when.
4. **The records:** `list_sms_detail_records` for the account and time window: whether
   each text was recorded at all. A text with no record probably never reached the
   service: say so, and ask support to check it with the carrier.

## Known causes

- **STOP:** the person opted out of this number. Only they can lift it, by texting START.
- **Routing goes somewhere else:** set to the client's inbox when they expected agents to
  answer, or the other way round.
- **Schedule times:** older windows, and any saved through this connection, run in the
  answering service's time zone rather than the line's, so a window can look hours off.
  Outside every window, texts go to the client's inbox.
- **A conversation already under way:** a routing change applies to new conversations.
  One already with the agents stays with them.
- **The wrong line:** the number is on a different line or account than the client
  thinks. `get_number` shows where it is.

## Report

What happened to each text, with times in the line's time zone: whether it was recorded,
which conversation it's in, where routing sent it, and who answered. Keep what the records
show apart from what's likely.

## Fix

- **Routing:** show the current routing and the new one in plain words: where texts will
  go, on which days and at which times. Times you send are read in the answering
  service's time zone: convert from the line's and say both. After a yes,
  `update_phone_sms_routing` with each schedule window's id as `list_phone_sms_routing`
  returns it, then read it back with `list_phone_sms_routing`. A line with no routing yet
  is set up in `phone-lines`.
- **STOP:** nothing to change here. The person texts START to the number.
- **Anything the records can't explain:** support.

Confirm before any change.
