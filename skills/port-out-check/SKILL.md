---
name: port-out-check
description: Check numbers leaving for another carrier - match the winning carrier's orders to your port-out requests, find numbers that don't belong on the order, and draft replies for the porting team, the carrier and the client. Use when a carrier or client asks whether a port-out was received or approved, when a port date doesn't match what was requested, or when an order seems to be missing.
---

# Check a port-out

Port-outs can't be approved, re-dated or rejected from here. This skill finds the facts and
drafts the follow-ups; the porting team makes the decision.

## 1. What's in flight

- `list_port_outs` for every request: its support key (PO_xxxx), status, port date, when
  it was created, and its numbers.
- Match the carrier's order numbers to the support keys by the numbers on each order. The
  carrier's own order ids aren't stored.
- Count numbers with a script, never by eye, and compare with the count the carrier gave.
- The port date comes back as midnight UTC. Report it as a date, not a time.

## 2. An order the carrier says was sent but isn't listed

- `get_number` on two or three numbers from the carrier's list, and on any number the
  carrier or porting team flagged: whether it's held here, which account, whether a line
  uses it.
- `search_accounts` with a flagged number to see whose account it's on. A number on a
  different account, or not held here at all, turns the order into a partial port, and
  it's rejected.
- Say this every time: a toll-free order rejected automatically at the RespOrg may never
  appear in `list_port_outs`. A missing request doesn't prove nothing arrived, so ask the
  porting team to check the RespOrg side.

## Report

A table: carrier order, support key, number count, status, port date. Then what's
missing, numbers that don't belong on the order, dates that differ from what the carrier
requested, and the risk to the port date, especially when only part of a client's numbers
would move. Say what time the check was made.

## Drafts

Draft these when asked, and never send them without a yes:
- **To the porting team:** what you found, the exact question, and the deadline.
- **To the client and the winning carrier:** where each order stands, what's needed from
  them (their order number and its status, confirmation that a mismatched number was
  removed, the expected count), and when they'll hear back. Don't promise an approval or a
  date the porting team hasn't confirmed, and never name another client's account.
