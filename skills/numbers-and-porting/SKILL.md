---
name: numbers-and-porting
description: Search for and buy phone numbers, move a number between clients or back to the pool, set call forwarding or the caller ID name, release a number, and port numbers in from another provider. Use for any phone number change, or when a client wants to keep the number they already have.
---

# Numbers and porting

Numbers cost money every month and changes reach live calls, so look first, show the
effect, and wait for a yes before every change.

## Buy

1. `list_available_numbers` by area code, city or pattern.
2. Show the numbers and their prices. Each one is billed monthly until it's released.
3. `buy_numbers` once approved. Bought numbers go to the Unassigned pool. Put one on a
   line with `create_account` or `create_account_phone` (see `new-client`).
4. If the answer says the order may not have finished, check with `get_number` before
   buying again.

## Move

1. Always `preview_number_move` first and show the admin the result: where the number is,
   where it would go, what moves with it and what stays behind.
2. `move_number` once approved. Calls, messages, recordings and billing records stay with
   whoever had the number at the time.

## Forwarding and caller ID name

- `update_number_forwarding`: always say which type. **Always** sends every call away
  before the answering service sees it; **on failure** forwards only calls that can't
  reach the service. Warn before choosing always.
- `update_number_caller_id_name` for the name shown on outbound calls.

## Release

`release_number` gives the number back for good: it stops working and billing, and it may
go to someone else. Confirm the exact number digit by digit. A number still on a line is
refused; move the line to another number first.

## Port numbers in

1. `check_portability` for the numbers.
2. `create_port_request` opens a draft. Nothing reaches the other provider yet.
3. `get_port_request` for what's still needed and the open port dates.
4. `update_port_request` saves the details: the account holder's name, the authorized
   person, billing phone, account number, PIN, service address, full or partial port, the
   date, and the signed letter of authorization and a recent invoice as PDFs. Show every
   value before saving, but never repeat the PIN back.
5. Submit with `update_port_request` only when the admin says to. That starts the real
   port.
6. Follow up with `get_port_request` or `list_port_requests`. Message the porting team
   with `create_port_request_comment`. `cancel_port_request` stops one that hasn't
   completed.

`list_port_outs` shows numbers leaving for another provider.
