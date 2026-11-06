---
name: phone-lines
description: Change a client's phone line - its company profile and what agents see and say, its IVR menu, greeting and recordings, its SMS routing, its contact list, and the account's features and client logins. Use when a client's details, call menu or text routing need to change.
---

# Phone lines

Agents and callers see these settings on live calls. Read the current setting, change only
what was asked, show the difference, and wait for a yes.

## Find the line

`search_accounts` or `get_account`, then `list_account_phones` and `get_phone`. If the
account has several lines, ask which one.

## Company profile and what agents see

`update_phone` with only the fields that change: company name shown to agents, business
phone, address, time zone, website, company info, opening and closing messages, special
instructions, agent notes, or its skill. Read the line back with `get_phone`.

**Skill:** `get_phone` shows the line's current skill by name. To change it, send
`skill_name` with the name exactly as `list_skills` shows it (or `skill_id`). A name
that matches no skill, or more than one, comes back with the choices.

## IVR

1. `get_phone_ivr` first.
2. **Classic menu:** `update_phone_ivr`. The menu keys you send replace every key, so
   send the complete list. A key can go to a line, to voicemail or to an outside number.
3. **Enhanced IVR flow:** `update_phone_ivr_flow` replaces the whole flow. Change only
   the nodes asked for and send the complete flow back. A spoken greeting is the node's
   text.
4. **A recording:** if the admin attached the file in the chat, use
   `update_phone_ivr_audio`. Otherwise `get_phone_ivr_audio_upload_link` gives them a
   link to upload it themselves, valid for 30 minutes.

These change how live calls are answered. Say exactly which callers are affected and when.

## SMS routing

`list_phone_sms_routing`, then `create_phone_sms_routing` or `update_phone_sms_routing`.
Say where texts to this number will go before changing it.

## The line's contacts

`list_phone_contacts`, `get_phone_contact`, then `create_phone_contact`,
`update_phone_contact` or `delete_phone_contact`. Repeat every phone number back in full
before saving it. On-call contacts are different; use `on-call-setup` for them.

## Account details, features and client logins

- `update_account` for the account's own details.
- `list_account_features` and `update_account_features`. Say which features add charges
  before turning one on.
- `list_account_user_access` shows the client's portal users and what each may change.
  Use it to check whether someone asking for a change is allowed to ask.
- Account contacts: `search_account_contacts`, `create_account_contact`,
  `update_account_contact`.
