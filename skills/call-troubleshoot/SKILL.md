---
name: call-troubleshoot
description: Work out why calls to a client's number didn't ring through, dropped, or went to the wrong place - from the number, the line and its menu, the call records and recordings, and who was on call - then propose the fix. Use when a client says callers couldn't reach them or calls went to the wrong person.
---

# Troubleshoot a call

Ask, in one question if anything is missing: the number dialed, roughly when and in which
time zone, the caller's number, and any call id the client has.

## Check, in this order

1. **The number:** `get_number` - whether it's active, which line uses it, and its
   forwarding. Forwarding set to always sends every call away before the service sees it.
2. **The line:** `search_accounts` with the number, then `get_phone`, and `get_phone_ivr`
   if callers go through a menu.
3. **The call:** with a call id, `list_calls` with `call_sid` finds it at any age.
   Otherwise `list_inbound_calls` or `list_recent_calls` for the account in a tight time
   window, matched on the caller's number and time. `get_call` for one call, and
   `list_call_recordings` if hearing it would settle the question.
4. **Who should have been reached:** for current coverage, use
   `list_phone_events_on_call`. For a historical call, first `list_escalation_levels`
   for the line, then `list_calendar_events` for a period covering the call's time,
   once for each returned level's id, including every backup level. Omitting the level
   id returns only the first level. Check `list_delivery_methods` for each person on
   shift at that time. Report names, levels and times in the line's time zone. If
   historical coverage cannot be established, say so rather than substituting who's
   on call now.

## Report

Keep the service's upstream provider identity and infrastructure private. Summarize
tool findings in service terms; do not copy provider names, raw responses, diagnostic
links, or provider account and connection identifiers into answers or drafts. Use
customer-facing call references; send provider-side investigation to support.

What happened, step by step, with call ids and times in the line's time zone. Keep what
the records show apart from what's likely. If there's no record of the call at all, it
probably never reached the service: say so, and ask support to check it with the carrier.

## Fix

Propose the change and hand off to the skill that makes it: `numbers-and-porting` for
forwarding, `phone-lines` for the menu or routing, `on-call-setup` for coverage or how
someone is reached. Confirm before any change.
