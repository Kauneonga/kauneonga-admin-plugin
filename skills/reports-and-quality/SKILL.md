---
name: reports-and-quality
description: Answer questions about activity and quality - a client's message volume and trends, call, chat, SMS and To Do records, call recordings, usage, service levels, agent performance, QA scores, coaching cases and SMS conversations. Use for reporting, billing preparation, quality reviews, or looking into what happened on a call.
---

# Reports and quality

Everything here reads data, except closing or marking SMS conversations. Say the date
range and time zone with every number, and say when a result was cut off.

## A client's activity

- `get_report_overview` and `get_report_trend` for an account's totals and trend.
- `get_report_call_messages`, `get_report_chat_messages` and `get_report_sms_messages`
  for messages by channel.
- Records for billing or disputes: `list_call_detail_records`,
  `list_chat_detail_records`, `list_sms_detail_records` and
  `list_to_do_detail_records`.

## Calls

`list_recent_calls`, `list_calls`, `list_inbound_calls` and `list_outbound_calls`, then
`get_call` for one. `list_call_recordings` for recordings. Recordings can hold health
information; share only what's needed.

## Across the answering service

- `get_usage_summary`: counts and minutes for calls, chats, SMS or To Dos, grouped by
  client, agent, skill or period.
- `get_service_level_report`: wait, talk and hold times and abandoned calls by skill.
- `get_agent_performance_report`, `get_supervisor_analytics` and
  `get_supervisor_leaderboards` for how agents are doing.
- Usage summaries and agent performance come back a page at a time. Follow `next_page`
  before adding up or ranking. For one agent, pass `agent` (part of their name); for the
  best or worst, `sort` by that number instead of reading every page.
- `list_agents` and `get_agent` for who's working and their skills.

## Quality

- QA scores: `list_qa_ai_overview`, `list_qa_ai_stats`, `list_qa_ai_trends`,
  `list_qa_ai_leaderboard`, `list_qa_ai_score_distribution`, `list_qa_ai_agents`,
  `get_qa_ai_agent`, `list_qa_ai_evaluations` and `get_qa_ai_evaluation`.
- Coaching: `list_feedback_cases` and `get_feedback_case`.

Report scores with how many calls they're based on, and don't rank agents on a handful of
calls.

## SMS conversations

`list_open_sms_conversations`, `list_closed_sms_conversations` or
`list_sms_conversations`, then `get_sms_conversation` and
`list_sms_conversation_messages`. `mark_sms_message_read` and `close_sms_conversation`
change them; confirm before closing one.
