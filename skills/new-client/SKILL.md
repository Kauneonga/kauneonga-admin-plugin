---
name: new-client
description: Set up a new answering service client from scratch - the account and its owner, phone lines, numbers, call script, on-call calendar, features and supervisor logins. Use when an admin is onboarding a client or adding a line to an existing one.
---

# Set up a new client

Collect everything first, confirm it once, then build in this order. Each step reads back
what it created before the next one starts.

## 1. Gather

1. Check the client doesn't already exist: `search_accounts` by company name and main
   phone number. If it does, add a line to it instead (step 3).
2. `list_account_creation_reference_data`. Its `required_fields` say exactly what this
   site needs, along with the time zones, industries, skills and available numbers.
3. Ask for every missing value in **one** question: company name and phone, owner name and
   email, each line's company name, time zone, industry, skill, and its number (an
   available one, or a new one to buy or port).

## 2. Create the account

Show the complete account and its lines in plain words, then `create_account` once it's
approved. Read back the account and its lines with `get_account` and
`list_account_phones`.

Then say who gets each new line's messages: the reply's `message_recipients`. With the
on-call calendar on, a new line makes the account owner its on-call contact by text and
email, every day, all day, so the owner gets every message from the first call, test calls
included. Before any test call, offer to point the line's messages to your own staff
(`on-call-setup`, "Cover for a while") and back to the client at go-live.

## 3. Lines and numbers

- **Another line on an existing account:** `create_account_phone`.
- **A number they don't have yet:** buy it or port it in with `numbers-and-porting`, then
  put it on the line.

## 4. How calls are answered

- **Call script:** `call-scripts`, built with `build_agent_script`.
- **On-call calendar:** `on-call-setup`, built with `build_on_call_calendar`.
- **AI receptionist,** if the client wants one: `ai-receptionists`.

## 5. Features and logins

- `list_account_features`, then `update_account_features` for what the client bought.
  Say which features add charges (AI Assistant, AMD, AMD Premium) before turning one on.
  Secure Messaging means recipients sign in to read each message.
- Supervisor logins for the client's staff: check `list_supervisors`, then
  `create_supervisor`. Never ask for or set a password; the new supervisor gets an email
  to set their own.

## Finish

Summarize what exists now: the account, each line and its number, its script, its on-call
levels and who's on them, features turned on, and anything still open, such as a port
that hasn't completed.
