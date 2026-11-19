---
name: portal-access
description: Work out why a client's portal login can't see an account, a line or its messages, or can't make a change - which users the account has and what each may do, whether the account and line are where they expect, and which features change what they see - then propose the fix. Use when a client says someone can't see something in their portal or can't do something they should be able to.
---

# Client portal access

Ask, in one question if anything is missing: the client, the person's name or email, and
exactly what they can't see or do (an account, a line, messages from a certain date, a
report, a recording, the on-call calendar, billing).

## Check, in this order

1. **The account:** `search_accounts`, then `get_account`: the right account, and whether
   it's active.
2. **The person:** `list_account_user_access` for that account: whether they're a user on
   it, whether they're active (`include_inactive` also lists deactivated users), and what
   they may do: owner, billing, account management, on-call calendar, reports,
   integrations, call recordings and referrals. Access is set per account, so check each
   of the client's accounts they expect to see.
3. **The line:** `list_account_phones`: whether the line is on this account. For a number,
   `get_number` shows which account and line it's on now.
4. **Features:** `list_account_features`: for example, with Secure Messaging on,
   recipients sign in to read each message instead of getting its text.

## Known causes

- **Not a user on that account,** or their login was deactivated.
- **Their access doesn't cover it:** billing, account changes, on-call calendar changes,
  reports, integrations and call recordings are each a separate access on the account.
- **The number moved:** calls and messages stay with the account that had the number at
  the time, so messages from before a move aren't on the new account.
- **The wrong account:** the client has several accounts and the line is on another one.

There's no sign-in history here. If they can't sign in at all, or get an error signing in,
say so and send them to support with the time it happened and the email they used. Never
ask for their password.

## Report

Who the person is on each account, what they may do, where the line and its messages are,
and what's missing. Keep what the records show apart from what's likely.

## Fix

- **Adding or removing a user, or changing what a user may do:** done in the Admin Portal;
  this connection can't change them. Say exactly what to change and where.
- **Account features:** `phone-lines`. Say which features add charges before turning one
  on.
- **A number on the wrong account:** `numbers-and-porting`, which previews a move first.

Confirm before any change.
