# Supplier delivery date check: an invented example

*Illustrative example with invented data.* The company, the four suppliers, the purchase orders, the replies, the customer orders and every date below are invented, and the suppliers are named Supplier A to D. The company, called the Company here, assembles bicycles. Its buyer runs the check on Tuesday 10 November 2026 and the supply planner decides what to do. People are referred to by role.

The inputs come first, in full, so the template can be run on them. The comparison follows.

## The inputs

### 1. Settings (typed by the buyer)

```
Company: the Company
Today: Tuesday 10 November 2026
Decides: the supply planner
```

Receiving days were not given, so the default of 2 is used. Days are counted as calendar days.

### 2. Open purchase order lines

```
po_number,line,supplier,sku,description,qty_open,order_date,original_promise_date
PO-2101,1,Supplier A,FRM-10,Steel frame set,120,2026-09-14,2026-11-02
PO-2101,2,Supplier A,BRK-04,Brake caliper pair,300,2026-09-14,2026-11-02
PO-2102,1,Supplier B,SAD-22,Saddle,500,2026-10-05,2026-11-20
PO-2103,1,Supplier B,GRP-07,Handlebar grip set,800,2026-10-12,2026-11-24
PO-2104,1,Supplier C,WHL-31,Wheel rim 26in,240,2026-10-01,2026-11-12
PO-2105,1,Supplier C,CHN-02,Chain,400,2026-10-20,2026-11-30
PO-2106,1,Supplier D,PED-15,Pedal pair,260,2026-10-26,2026-12-01
PO-2107,1,Supplier D,TYR-09,Tyre 26in,600,2026-09-28,2026-11-06
```

### 3. Supplier replies

```
logged_date,supplier,po_number,line,basis,reply_date,note
2026-10-28,Supplier A,PO-2101,1,written confirmation,2026-11-16,Tubing delayed at the mill
2026-10-28,Supplier A,PO-2101,2,written confirmation,2026-11-02,Ships with the first batch
2026-11-02,Supplier A,PO-2099,1,written confirmation,2026-11-09,Earlier order
2026-11-03,Supplier B,PO-2102,1,call record,2026-11-27,Call with the supplier's sales desk
2026-11-09,Supplier B,PO-2102,1,informal estimate,2026-12-04,Sales rep said probably first week of December
2026-11-06,Supplier C,PO-2104,1,informal estimate,2026-11-19,Rep said about a week late in passing
2026-11-05,Supplier C,PO-2105,1,written confirmation,2026-11-23,Production slot moved up
2026-11-04,Supplier D,PO-2106,1,written confirmation,2026-12-01,Acknowledgement of the order
2026-11-09,Supplier D,PO-2107,1,call record,,Supplier will confirm after speaking to its warehouse
```

### 4. Follow-ups already asked

```
asked_date,supplier,po_number,line,question,answered_date
2026-10-22,Supplier A,PO-2101,1,Please confirm a ship date,2026-10-28
2026-11-02,Supplier B,PO-2102,1,Please confirm the date,2026-11-03
2026-11-05,Supplier A,PO-2101,2,Has the shipment left,
2026-11-06,Supplier C,PO-2104,1,Is the estimate a firm date,
2026-11-09,Supplier D,PO-2107,1,What is the delivery date and the reason for the delay,
```

### 5. Dependent orders

```
order_ref,po_number,line,ship_by_date
CO-5301,PO-2101,1,2026-11-13
CO-5302,PO-2101,1,2026-11-25
CO-5303,PO-2101,2,2026-11-11
CO-5304,PO-2102,1,2026-11-27
CO-5305,PO-2102,1,2026-12-10
CO-5306,PO-2104,1,2026-11-18
CO-5307,PO-2101,1,2026-11-24
CO-5307,PO-2105,1,2026-11-24
CO-5308,PO-2103,1,2026-11-26
CO-5309,PO-2107,1,2026-11-13
CO-5310,PO-2106,1,2026-12-04
```

## The output

**SUPPLIER DELIVERY DATE CHECK: the Company, Tuesday 10 November 2026**

For: the supply planner. Prepared Tuesday 10 November 2026 from: open orders (8 lines), supplier replies (9 rows), follow-ups (5 rows), dependent orders (11 rows), settings.  
Column check: all headers matched.  
Settings: receiving days 2, counted in calendar days. Defaults used: receiving days.  
Summary: 8 open lines. Moved later 2, moved earlier 1, as promised 2, estimate only 1, no confirmed date 2. Past due: 2. Orders on the list: 10; late on the date relied on 4; not late yet but resting on an unconfirmed date 3; spare days on a confirmed date, not listed 3. Unanswered follow-ups: 3. Lines needing a follow-up with none open: 1.  

**Data checks**

- A reply for PO-2099 line 1 (Supplier A, logged Monday 2 November) has no line on the open orders. Left out; read as closed or mistyped.

**Date comparison**

*Supplier A*

- **PO-2101-1** FRM-10 Steel frame set, 120 open. MOVED LATER. Original Monday 2 November. Confirmed Monday 16 November (written confirmation, logged Wednesday 28 October). Moved 14 days later. Orders on this line: CO-5301 (late 5 days), CO-5302 (7 spare days), CO-5307 (6 spare days).
- **PO-2101-2** BRK-04 Brake caliper pair, 300 open. AS PROMISED. Original Monday 2 November. Confirmed Monday 2 November (written confirmation, logged Wednesday 28 October). Not moved. PAST DUE 8 days; the earliest it can arrive is today. Orders on this line: CO-5303 (late 1 day).

*Supplier B*

- **PO-2102-1** SAD-22 Saddle, 500 open. MOVED LATER. Original Friday 20 November. Confirmed Friday 27 November (call record, logged Tuesday 3 November). Moved 7 days later. Estimate, not confirmed: Friday 4 December, 7 days later than the confirmed date, logged Monday 9 November. Orders on this line: CO-5304 (late 2 days; late 9 days on the estimate), CO-5305 (11 spare days; 4 spare days on the estimate).
- **PO-2103-1** GRP-07 Handlebar grip set, 800 open. NO CONFIRMED DATE. Original Tuesday 24 November. No reply logged. Orders on this line: CO-5308 (0 spare days).

*Supplier C*

- **PO-2104-1** WHL-31 Wheel rim 26in, 240 open. ESTIMATE ONLY. Original Thursday 12 November. Estimate, not confirmed: Thursday 19 November, 7 days later than the original, logged Friday 6 November. Orders on this line: CO-5306 (4 spare days on the original; late 3 days on the estimate).
- **PO-2105-1** CHN-02 Chain, 400 open. MOVED EARLIER. Original Monday 30 November. Confirmed Monday 23 November (written confirmation, logged Thursday 5 November). Moved 7 days earlier. Orders on this line: CO-5307 (late 1 day).

*Supplier D*

- **PO-2106-1** PED-15 Pedal pair, 260 open. AS PROMISED. Original Tuesday 1 December. Confirmed Tuesday 1 December (written confirmation, logged Wednesday 4 November). Not moved. Orders on this line: CO-5310 (1 spare day).
- **PO-2107-1** TYR-09 Tyre 26in, 600 open. NO CONFIRMED DATE. Original Friday 6 November. A reply was logged Monday 9 November (call record) without a date. PAST DUE 4 days; the earliest it can arrive is today. Orders on this line: CO-5309 (1 spare day).

**Orders affected**

*Late on the date relied on: 4*

- **CO-5301**, ship by Friday 13 November: late 5 days. PO-2101-1 (Supplier A, written confirmation, Monday 16 November); ready to ship Wednesday 18 November.
- **CO-5304**, ship by Friday 27 November: late 2 days. PO-2102-1 (Supplier B, call record, Friday 27 November); ready to ship Sunday 29 November. On the unconfirmed estimate of Friday 4 December: ready Sunday 6 December, late 9 days.
- **CO-5303**, ship by Wednesday 11 November: late 1 day. PO-2101-2 (Supplier A, written confirmation, Monday 2 November, past due, so measured from today); ready to ship Thursday 12 November.
- **CO-5307**, ship by Tuesday 24 November: late 1 day. PO-2105-1 (Supplier C, written confirmation, Monday 23 November); ready to ship Wednesday 25 November. Its other line, PO-2101-1, leaves 6 spare days.

*Not late yet, resting on a date nobody has confirmed: 3*

- **CO-5306**, ship by Wednesday 18 November: PO-2104-1 (Supplier C, ESTIMATE ONLY; original Thursday 12 November); ready to ship Saturday 14 November, 4 spare days. On the estimate of Thursday 19 November: ready Saturday 21 November, late 3 days.
- **CO-5308**, ship by Thursday 26 November: PO-2103-1 (Supplier B, NO CONFIRMED DATE; original Tuesday 24 November); ready to ship Thursday 26 November, 0 spare days.
- **CO-5309**, ship by Friday 13 November: PO-2107-1 (Supplier D, NO CONFIRMED DATE, past due; original Friday 6 November); ready to ship Thursday 12 November, 1 spare day.

*Spare days on a confirmed date, not listed: 3.* CO-5302 (7 spare days), CO-5305 (11 spare days; 4 spare days on the estimate), CO-5310 (1 spare day).

**Unanswered follow-ups**

- Supplier A, PO-2101-2, asked Thursday 5 November: "Has the shipment left". Waiting 5 days.
- Supplier C, PO-2104-1, asked Friday 6 November: "Is the estimate a firm date". Waiting 4 days.
- Supplier D, PO-2107-1, asked Monday 9 November: "What is the delivery date and the reason for the delay". Waiting 1 day.

*Lines that need a follow-up and have none open: 1.*

- PO-2103-1 (Supplier B): NO CONFIRMED DATE. Last follow-up: none logged.

**Questions for the supply planner**

1. PO-2101-1 (Supplier A, frame sets). Moved from Monday 2 November to Monday 16 November by a written confirmation, 14 days later. CO-5301 ships by Friday 13 November and would be ready Wednesday 18 November, 5 days late. On the same line, CO-5302 has 7 spare days and CO-5307 has 6 spare days. No follow-up is open. Do you want to chase Supplier A, and what do you tell the customer on CO-5301?
2. PO-2101-2 (Supplier A, brake calipers). Confirmed for Monday 2 November and still open 8 days later; the follow-up asked on Thursday 5 November has no answer after 5 days. CO-5303 ships by Wednesday 11 November and would be ready Thursday 12 November, 1 day late. Do you want to chase Supplier A again, and what do you tell the customer on CO-5303?
3. PO-2102-1 (Supplier B, saddles). Moved from Friday 20 November to Friday 27 November by a call record, with a later informal estimate of Friday 4 December that is not confirmed. CO-5304 ships by Friday 27 November: 2 days late on the confirmed date, 9 on the estimate. CO-5305 has 11 spare days on the confirmed date and 4 on the estimate. No follow-up is open; the one asked on Monday 2 November was answered on Tuesday 3 November. Do you want to chase Supplier B for a confirmed date, and what do you tell the customer on CO-5304?
4. PO-2103-1 (Supplier B, handlebar grip sets). No reply is logged and no follow-up has been asked. The original date is Tuesday 24 November. CO-5308 ships by Thursday 26 November, with 0 spare days if that date holds. Do you want to chase Supplier B, and what do you tell the customer on CO-5308?
5. PO-2104-1 (Supplier C, wheel rims). Only an informal estimate of Thursday 19 November, logged Friday 6 November; the original date is Thursday 12 November. The follow-up asked on Friday 6 November has no answer after 4 days. CO-5306 ships by Wednesday 18 November: 4 spare days on the original, 3 days late on the estimate. Do you want to chase Supplier C again, and what do you tell the customer on CO-5306?
6. PO-2105-1 (Supplier C, chains). Moved earlier, from Monday 30 November to Monday 23 November, by a written confirmation. CO-5307 ships by Tuesday 24 November and would be ready Wednesday 25 November, 1 day late even on the earlier date; its other line, PO-2101-1, leaves 6 spare days. No follow-up is open. Do you want to chase Supplier C, and what do you tell the customer on CO-5307?
7. PO-2107-1 (Supplier D, tyres). The original date of Friday 6 November passed 4 days ago. A call on Monday 9 November produced no date, and the follow-up asked that day has no answer after 1 day. CO-5309 ships by Friday 13 November: 1 spare day if the tyres arrive today. Do you want to chase Supplier D, and what do you tell the customer on CO-5309?

Any request to a supplier for a part-delivery, faster freight or a price change is a buyer's decision; none is proposed here.

Draft for the supply planner's decisions. No supplier has been contacted, nothing has been sent to a customer, and no order, date or record has been changed.
