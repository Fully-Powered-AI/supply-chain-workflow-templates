# Unshipped order review: an invented example

*Illustrative example with invented data.* The business, the customers, the item codes, the order numbers, the quantities and every date below are invented. The business is an invented online homewares shop, called the Store here, with one warehouse. Its fulfilment lead asks for the daily order review on the morning of Tuesday 10 November 2026. Customers are shown as Customer A, Customer B and so on; people are referred to by role.

The inputs come first, in full, so the template can be run on them. The review follows.

## The inputs

### 1. Settings (typed by the fulfilment coordinator)

```
Business: the Store
Today: 2026-11-10
Fulfilment lead: not named, use the role
All other settings: use the defaults
```

### 2. Orders

```
order_number,order_date,customer,promised_date,order_status
A1001,2026-10-26,Customer A,2026-10-30,open
A1002,2026-10-29,Customer B,2026-11-03,open
A1003,2026-11-02,Customer C,2026-11-06,open
A1004,2026-11-04,Customer D,2026-11-09,open
A1005,2026-11-05,Customer E,2026-11-10,open
A1006,2026-11-07,Customer F,2026-11-12,open
A1007,2026-11-09,Customer G,2026-11-13,open
A1008,2026-11-03,Customer H,2026-11-06,shipped
A1009,2026-11-06,Customer J,2026-11-11,open
A1010,2026-10-30,Customer K,2026-11-04,shipped
A1011,2026-11-01,Customer L,2026-11-05,cancelled
A1012,2026-11-08,Customer M,2026-11-12,open
```

### 3. Order lines

```
order_number,line,item_code,qty_ordered,qty_shipped,last_ship_date
A1001,1,ITM-10,4,0,
A1001,2,ITM-22,2,0,
A1002,1,ITM-31,10,6,2026-11-04
A1002,2,ITM-32,5,5,2026-11-04
A1003,1,ITM-10,3,0,
A1004,1,ITM-45,6,0,
A1005,1,ITM-50,2,2,2026-11-09
A1005,2,ITM-51,1,0,
A1006,1,ITM-10,1,0,
A1007,1,ITM-60,2,0,
A1008,1,ITM-70,5,5,2026-11-05
A1008,2,ITM-71,2,0,
A1010,1,ITM-80,3,3,2026-11-02
A1011,1,ITM-81,2,0,
A1012,1,ITM-90,4,4,2026-11-09
```

### 4. Active holds

```
order_number,hold_reason,hold_placed_date,hold_owner,next_step,next_step_owner
A1001,Awaiting stock,2026-10-28,Buyer,,
A1002,Remainder awaiting stock,2026-11-04,Warehouse lead,Ship remainder when ITM-31 is received,Warehouse lead
A1003,Address check,2026-11-09,Customer service,Phone customer to confirm address,Customer service
A1005,Awaiting stock,2026-11-09,,Re-check stock Thursday,
A1006,Payment review,2026-11-08,Finance,Release when payment clears,Finance
A1009,Payment review,2026-11-07,Finance,,
A1013,Address check,2026-11-05,Customer service,Phone customer to confirm address,Customer service
```

## The review

```
UNSHIPPED ORDER REVIEW: the Store, Tuesday 2026-11-10

For: the fulfilment lead. Prepared from: orders (12 rows), order lines (15 rows), holds (7 rows), settings.
Column check: all headers matched.
Settings: age bands 0 to 2, 3 to 5, 6 to 10 and over 10 days, first band (0 to 2 days) needs no explanation; shipped status shipped; cancelled status cancelled; hold limit 5 days; part-shipment limit 3 days. Defaults used: age bands, status words, hold limit, part-shipment limit.
Summary: 9 open orders listed: unshipped 5, part-shipped 3, status unknown 1. Left out: shipped in full 2, cancelled 1. By age: over 10 days 2, 6 to 10 days 3, 3 to 5 days 3, 0 to 2 days 1. With a hold 6; no hold 3. Next step missing 5; within the first band with no hold 1. Past promised date 5. Still to ship 25 units across 8 orders; units not known for 1. Holds past the limit 2. Part-shipped with no recent shipment 2. Status to confirm 3.

Data checks
A1013: a hold row for an order that is not in the orders file; left out.

Aged list
Over 10 days (2)
A1001 Customer A. Ordered 2026-10-26, 15 days. Promised 2026-10-30, 11 days past. Unshipped: 6 units to ship, ITM-10 4, ITM-22 2. Hold: Awaiting stock, placed 2026-10-28, 13 days, owner Buyer. Next step missing: hold without a next step.
A1002 Customer B. Ordered 2026-10-29, 12 days. Promised 2026-11-03, 7 days past. Part-shipped: 11 of 15 units shipped, last shipment 2026-11-04, 6 days ago; still to ship ITM-31 4. Hold: Remainder awaiting stock, placed 2026-11-04, 6 days, owner Warehouse lead. Next step: Ship remainder when ITM-31 is received, Warehouse lead.

6 to 10 days (3)
A1003 Customer C. Ordered 2026-11-02, 8 days. Promised 2026-11-06, 4 days past. Unshipped: 3 units to ship, ITM-10 3. Hold: Address check, placed 2026-11-09, 1 day, owner Customer service. Next step: Phone customer to confirm address, Customer service.
A1008 Customer H. Ordered 2026-11-03, 7 days. Promised 2026-11-06, 4 days past. Part-shipped: 5 of 7 units shipped, last shipment 2026-11-05, 5 days ago; still to ship ITM-71 2. No hold recorded. Next step missing: no hold recorded, no next step.
A1004 Customer D. Ordered 2026-11-04, 6 days. Promised 2026-11-09, 1 day past. Unshipped: 6 units to ship, ITM-45 6. No hold recorded. Next step missing: no hold recorded, no next step.

3 to 5 days (3)
A1005 Customer E. Ordered 2026-11-05, 5 days. Promised 2026-11-10. Part-shipped: 2 of 3 units shipped, last shipment 2026-11-09, 1 day ago; still to ship ITM-51 1. Hold: Awaiting stock, placed 2026-11-09, 1 day, owner not named. Next step missing: next step without an owner ("Re-check stock Thursday").
A1009 Customer J. Ordered 2026-11-06, 4 days. Promised 2026-11-11. Status unknown: no order line rows; units not known. Hold: Payment review, placed 2026-11-07, 3 days, owner Finance. Next step missing: hold without a next step.
A1006 Customer F. Ordered 2026-11-07, 3 days. Promised 2026-11-12. Unshipped: 1 unit to ship, ITM-10 1. Hold: Payment review, placed 2026-11-08, 2 days, owner Finance. Next step: Release when payment clears, Finance.

0 to 2 days (1)
A1007 Customer G. Ordered 2026-11-09, 1 day. Promised 2026-11-13. Unshipped: 2 units to ship, ITM-60 2. No hold recorded. Within the first band with no hold.

Missing next step
A1001: hold without a next step; 15 days old. See decision 1.
A1008: no hold recorded, no next step; 7 days old. See decision 3.
A1004: no hold recorded, no next step; 6 days old. See decision 4.
A1005: next step without an owner; 5 days old. See decision 5.
A1009: hold without a next step; 4 days old. See decision 6.

Holds past the limit
A1001: Awaiting stock, 13 days against a limit of 5; owner Buyer. See decision 1.
A1002: Remainder awaiting stock, 6 days against a limit of 5; owner Warehouse lead. See decision 2.

Part-shipped with no recent shipment
A1002: last shipment 2026-11-04, 6 days ago against a limit of 3; still to ship ITM-31 4. See decision 2.
A1008: last shipment 2026-11-05, 5 days ago against a limit of 3; still to ship ITM-71 2. See decision 3.

Status to confirm
A1008: status says shipped; the lines show part-shipped. See decision 3.
A1009: status says open; the lines show no line rows. See decision 6.
A1012: status says open; the lines show shipped in full. See decision 7.

Decisions for the fulfilment lead
1. A1001, Customer A: 15 days old, 11 days past its promised date, 6 units unshipped. The hold (awaiting stock, owner Buyer) has stood 13 days, past the limit of 5, and has no next step. Who owns the next step, does the hold stay in force, and is the customer to be told about the delay?
2. A1002, Customer B: 12 days old, 7 days past its promised date. 11 of 15 units shipped on 2026-11-04, 6 days ago, past the limit of 3; 4 units of ITM-31 remain. The hold (remainder awaiting stock, owner Warehouse lead) has stood 6 days, past the limit of 5, and its recorded next step is to ship the remainder when ITM-31 is received. Does the hold stay in force, and is the customer to be told about the remainder?
3. A1008, Customer H: 7 days old, 4 days past its promised date. The status says shipped, but the lines show 5 of 7 units shipped on 2026-11-05, 5 days ago, past the limit of 3, and 2 units of ITM-71 not shipped. No hold or next step is recorded. Are the lines or the status word right, and if the lines are right, who owns the next step?
4. A1004, Customer D: 6 days old, 1 day past its promised date, 6 units of ITM-45 unshipped. No hold and no next step are recorded. What is keeping it, and who owns the next step?
5. A1005, Customer E: 5 days old, promised today. 2 of 3 units shipped on 2026-11-09; 1 unit of ITM-51 remains. The hold (awaiting stock, placed 2026-11-09) has no named owner, and its next step, "Re-check stock Thursday", has no owner. Who owns the hold and the next step?
6. A1009, Customer J: 4 days old, promised 2026-11-11. The status is open and there are no line records, so what has shipped is not known. The hold (payment review, owner Finance) has stood 3 days and has no next step. Has anything shipped, and who owns the next step on the payment review?
7. A1012, Customer M: the status is open, but the lines show all 4 units of ITM-90 shipped on 2026-11-09. Is the order complete, and who updates its status?

Draft for the fulfilment lead's decision. Nothing has been released, shipped, reassigned, changed or sent, and no hold has been lifted. Ages are in calendar days to 2026-11-10.
```
