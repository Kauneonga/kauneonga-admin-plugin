---
name: on-call-setup
description: Build or change a client's on-call calendar - escalation levels and their timing, who is on call when, people and how they are reached, copying a level's schedule, and answering who is on call. Use when setting up a new client's on-call coverage or making changes for a client.
---

# On-call setup

Messages go through a line's escalation levels in order. Each level has shifts, and each
shift reaches a person through their delivery methods (call, text, email and others).
Changes here decide who gets paged on real calls.

## Who's on call

`list_phone_events_on_call` for the line, or `list_escalation_levels` and then
`list_calendar_events` for each level in turn, so backup levels aren't missed. Answer with
names, levels and times in the line's time zone.

**Who gets the line's messages right now:** `get_phone`'s `message_recipients`. That is
what delivery uses: the default level's current shifts and how each person is reached.
`list_phone_events_on_call` lists only shifts marked on call, so it can show no one
while someone still gets every message.

## Cover for a while

To send a line's messages to other people until a set time (testing before go-live, a
vacation): give them shifts on the default level that end at the handback time, and take
the regular person off only those covered times (skip whole days with `excluded_dates`;
for part of a day, change that one occurrence's times). The handback then happens on its
own. Show who gets the messages before and after with `message_recipients`, and say when
it switches back.

## A new calendar

Use `build_on_call_calendar` rather than building levels, people, delivery methods and
shifts one call at a time. Gather the levels and how long each waits, the people and how
each is reached, and the rotation. Show the result in plain words, then save it once
approved.

## Escalation levels

- `list_escalation_level_reference_data` first: the existing levels, suggested wait
  times and the line's default level.
- `create_escalation_level` or `update_escalation_level`. Read the level order back after.
- **Delete:** `list_escalation_level_dependents` first and tell the admin what depends on
  the level: shifts, people, other levels and scripts. Then `delete_escalation_level`
  only with explicit approval. The line's default level can't be deleted. If the level is
  still in use, change the script or routing first.
- `clone_phone_escalation_level` copies one level's shifts onto another level.
  `delete_escalation_level_events` removes every shift on a level and keeps the level.

## Shifts

`list_calendar_event_reference_data` for valid values, then `create_calendar_event`,
`update_calendar_event`, `copy_calendar_event`, `delete_calendar_event` or
`delete_calendar_events`. For a repeating shift, ask whether the change is for one
occurrence or the whole series; never assume the series.

## People and how they're reached

- `list_calendar_contact_reference_data`, `list_calendar_contacts`, then
  `create_calendar_contact` or `update_calendar_contact`.
- `list_delivery_method_reference_data`, `list_delivery_methods`, then
  `create_delivery_method`, `update_delivery_method` or `delete_delivery_method`. A
  delivery method belongs to the person, so a change applies on every shift they have.
  Make sure they keep at least one.
- `merge_phone_calendar_contacts` for a person listed twice. It can't be undone here.
- `delete_calendar_contact` removes every shift that person has. Prefer ending their
  shifts unless the admin is sure.

Repeat every phone number back in full before saving it.
