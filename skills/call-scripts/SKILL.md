---
name: call-scripts
description: Write a new call script for a client's line or change an existing one - the questions agents ask, branches, which escalation level each kind of call goes to, and closing actions. Use when a client's call handling needs to change or a new line needs its script.
---

# Call scripts

Agents read these on live calls. Never hand-write the script structure: build it with the
tool, show it, and save it only once it's approved.

## Before writing

1. Find the line (`list_account_phones`) and its current scripts with
   `list_agent_scripts` and `get_agent_script`.
2. `list_agent_script_reference_data` for the line: its escalation levels, closing actions,
   recipients and the question types it supports. Use only the values it returns. If a
   script needs an escalation level the line doesn't have yet, create it with
   `on-call-setup` first.
3. Ask what the client wants: who calls, what to ask, what's urgent, where each kind of
   call goes, and how calls end.

## A new script

1. `build_agent_script` from that description. It assembles a valid script and saves
   nothing.
2. Show the admin the script in plain words: each question, each branch, and the
   escalation level each branch sends to.
3. `create_agent_script` once approved. Read it back with `get_agent_script`.

## Changing a script

1. `get_agent_script` for the current version.
2. Change only what was asked. `update_agent_script` replaces the whole script, so send
   the complete script back.
3. Show exactly what changes, then save once approved.
4. Making a script the line's default replaces the current default, and a default script
   can't also have a schedule. Say so before saving.

## Checking a script

`get_agent_scripts_ai_data` shows the script for a number the way the AI reads it. Use it
to answer what agents are asked to do on that line.
