---
name: agents-and-queues
description: Work out why callers wait too long, hang up before an agent answers, or don't reach an agent, or why service levels dropped - from agents and their skills, the line's skill and queue limit, the service level and agent performance reports, and coaching cases - then propose the fix. Use when callers wait too long, calls are abandoned, an agent isn't getting calls, or service levels fall.
---

# Agents and queues

If `list_agents`, `list_skills` or the report tools below aren't in the tool list yet, say
this connection doesn't offer them yet and check the same reports in the portal instead.

Ask, in one question if anything is missing: which line, skill or agent, the date range
and time zone, and what went wrong in numbers if they have them (a wait time, how many
calls were abandoned).

## Check, in this order

1. **The line:** for one line, `get_phone` shows the skill its calls need, and
   `get_phone_ivr` its queue limit (`calls_limit`). `list_skills` shows how many active
   agents and lines use each skill.
2. **Who can take those calls:** `list_agents` filtered by that skill's id and by
   `available`, then `get_agent` for one person: their skills and whether they're
   available to take calls.
3. **Service level:** `get_service_level_report` for the date range: per skill, average
   wait, talk and hold time, calls, abandoned calls and calls that waited over 60 seconds.
   Compare with the same days a week earlier.
4. **Agents:** `get_agent_performance_report`: time signed in and available, ready
   percentage, and talk, hold and wrap minutes per agent. It comes a page at a time: for
   one person pass `agent` (part of their name); for the best or worst, `sort` by that
   number instead of reading every page.
5. **Client feedback and coaching:** `get_supervisor_analytics` and
   `get_supervisor_leaderboards` for client ratings by agent and account, and
   `list_feedback_cases` and `get_feedback_case` for coaching cases on an agent.

## Known causes

- **Not enough agents with the skill:** a line's skill that few agents have, or none
  available at the time, waits even when other agents are free.
- **Agents signed in but not available:** a low ready percentage, or long hold and wrap
  time keeping agents off the next call.
- **More calls than usual:** a spike on one skill compared with the same day last week.
- **The queue limit:** when `calls_limit` callers are already waiting, the next caller
  hears a busy signal or the queue-full message. A limit of 0 turns away every call
  dialed straight to that number.

## Report

The numbers with the date range and time zone, by skill and agent. Keep what the reports
show apart from what's likely. These reports are totals: they don't name callers. Don't
judge or rank an agent on a handful of calls.

## Fix

Propose the change and hand off to the skill that makes it: `phone-lines` for a line's
skill or its queue limit, and `call-troubleshoot` when one caller's call needs tracing.
Agents' skills, schedules and coaching cases are changed in the portal; this connection
can't change them. Confirm before any change.
