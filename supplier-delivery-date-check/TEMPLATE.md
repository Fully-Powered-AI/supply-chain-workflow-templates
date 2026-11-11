# Supplier delivery date check

Capability template, version 0.1.0.

## Purpose

Prepare one comparison of promised and revised delivery dates for the open purchase order lines a buyer is tracking: the date each supplier first promised, the latest date a supplier has confirmed, how far it moved, whether the line is past due, the customer or production orders each date could delay, and the follow-ups still unanswered. Every date traces to a reply the person supplied, and every count of days is written out. The assistant prepares; it never contacts a supplier, tells a customer, changes a date or order in any system, or agrees a commercial change. The person decides whom to chase and what to say to customers.

## When to use it and when not to

Use it when a supplier confirmation arrives or a status call has been logged, or on a set day each week for the open orders that matter most. Run it again after new replies are logged.

Do not use it:

- to judge how reliable a supplier is over months. That is a scorecard, a separate piece of work;
- to assess a threat to a supplier, such as a fire, a failure or a sanction. That is a risk brief;
- to decide what to reorder or how much. That is a replenishment plan;
- to predict a date from a supplier's past behavior. Only the dates the supplier gave are compared; the assistant adds no forecast;
- to write to a supplier or a customer. The questions at the end are for the person to act on.

## Roles

- **Runs it:** the buyer, the purchasing coordinator or the operations lead.
- **Decides** which shortages to escalate, whom to chase and what customers are told: [your decider], usually the supply planner.
- **Agrees any commercial change** with a supplier, such as a part-delivery, faster freight or a price change: the buyer with authority to do so.
- **Contacts suppliers and customers:** the people the company names. Always people.
- **Logs replies and updates order dates in the purchasing system:** the people the company names, after any decision.

## Inputs

The assistant works only from the files and notes the person supplies. It needs no connection to the purchasing system, the order book or any supplier's site, and never asks for a password or a login code.

1. **The open purchase order lines.** One row per line still open. Default column headers: `po_number`, `line`, `supplier`, `sku`, `description`, `qty_open`, `order_date`, `original_promise_date`. `original_promise_date` is the delivery date the supplier first committed to.
2. **The supplier replies.** One row per reply. Default column headers: `logged_date`, `supplier`, `po_number`, `line`, `basis`, `reply_date`, `note`. `basis` is exactly one of `written confirmation`, `call record` or `informal estimate`. `reply_date` is the delivery date the reply names, blank if it named none.
3. **The follow-ups already asked.** One row per question asked of a supplier. Default column headers: `asked_date`, `supplier`, `po_number`, `line`, `question`, `answered_date`. A blank `answered_date` means unanswered. A blank `line` means the whole purchase order.
4. **The dependent orders.** One row per order and purchase order line it waits on. Default column headers: `order_ref`, `po_number`, `line`, `ship_by_date`. An order that waits on two lines has two rows with the same `order_ref`.
5. **The settings,** typed: the company, today's date, who decides, and the receiving days. Receiving days are the days between a delivery arriving and the goods being ready to ship; default 2 ([your receiving days]). Days are counted as calendar days. If receiving days are not given, the Settings line of the comparison says so after "Defaults used".

Dependent orders are optional. Without them, write "no dependent orders supplied" in the header and print "No dependent orders supplied." under Orders affected.

**Column check.** Before any other work, compare each file's headers with the defaults, or with the company's own headers if [your column headers] are set. If a header is missing or named differently, stop. List the headers expected and the headers found, ask which column is which, and prepare nothing else. Never guess a column.

## The procedure

1. **Check the inputs.** Run the column check. Confirm today's date. A `basis` other than the three allowed, a date that is not a real date, or two open rows with the same PO number and line: stop and ask. A blank `original_promise_date` on an open line: stop and ask.
2. **Check the data.** List under Data checks: a reply, follow-up or dependent-order row whose PO number and line are not on the open orders (left out; read as closed or mistyped); a line with a `qty_open` of 0 (left out as closed); a reply logged before the order date (kept, listed). Two replies of a confirmed kind for the same line logged on the same day with different dates: stop and ask which stands.
3. **Find the date relied on for each line.** Confirmed replies are those whose basis is `written confirmation` or `call record` and whose `reply_date` is not blank. Take the confirmed reply with the latest `logged_date`; its `reply_date` is the confirmed date. If the line has no confirmed reply, the date relied on is the original promise and the line has no confirmed date. A reply that names no date is never a confirmed date.
4. **Compare.** For a line with a confirmed date, days moved = confirmed date − original date, in calendar days: positive is later, negative is earlier, zero is not moved. For a line without one, write "not known".
5. **Set the status.** Exactly one per line: MOVED LATER (confirmed date after the original), MOVED EARLIER, AS PROMISED (confirmed date equal to the original), ESTIMATE ONLY (no confirmed date, and an informal estimate with a date), NO CONFIRMED DATE (no confirmed date and no such estimate).
6. **Show the estimate and the undated reply.** The estimate shown is the informal estimate with a date and the latest `logged_date`, and only if it was logged after the confirmed reply or the line has no confirmed reply. Show its date, whether it is later or earlier than the date relied on and by how many days, and when it was logged. An estimate never changes the date relied on or the status. The latest reply of any basis with a blank `reply_date`, logged after the confirmed reply or where the line has none, is shown as "a reply was logged [date] ([basis]) without a date".
7. **Mark the lines past due.** If the date relied on is before today, write PAST DUE and the days, today − that date, and say the earliest the goods can arrive is today. The status is unchanged.
8. **Test each order.** For each dependent row: earliest arrival = the later of the date relied on and today; ready to ship = earliest arrival + receiving days; if ready to ship is after `ship_by_date`, the row is late by the difference in days; otherwise it has that many spare days. Where the line has a shown estimate, repeat the test with the later of the estimate and today and show it beside. An order that waits on two or more lines takes the result of its worst line, the most days late or the fewest spare, and names that line and gives the result of each other line.
9. **Sort the orders into groups,** each ordered as stated.
   - **Late on the date relied on:** the order is late. Most days late first, then earliest ship-by date.
   - **Not late yet, resting on a date nobody has confirmed:** the order is not late, and one of its lines has status ESTIMATE ONLY or NO CONFIRMED DATE, or has an estimate that would make the order late. Fewest spare days first, counting days late on an estimate as negative spare days.
   - **Not listed:** every other order has spare days on a confirmed date. Name them with their spare days in one line, adding the result on a shown estimate where the line has one, and count them in the summary.
10. **List the follow-ups.** Unanswered follow-ups: every row with a blank `answered_date`, with days waiting = today − `asked_date`, longest wait first, then by PO number. A whole-purchase-order follow-up is listed once, against "all lines". Then lines that need a follow-up and have none open: every line that is PAST DUE, ESTIMATE ONLY or NO CONFIRMED DATE with no unanswered follow-up, with the date of the last follow-up and whether it was answered, or "none logged".
11. **Write the questions,** numbered, one for each line that is past due, has a late order, has status ESTIMATE ONLY or NO CONFIRMED DATE, or has an estimate later than the date relied on, in PO number and line order. Each gives the facts: the original date, the date relied on and its basis, any estimate, whether it is past due, any open follow-up, and the orders on it with their results. It then asks whether the person wants to chase the supplier and what they will tell the customer on each late order and each order in the second group (not late yet, resting on a date nobody has confirmed). If no order is listed on the line, it asks only about the supplier. A question recommends nothing. Close the questions with one sentence saying that a request for a part-delivery, faster freight or a price change is the buyer's decision and none is proposed.
12. **Return the comparison** to the person who ran it, for [your decider]. A person contacts the suppliers and the customers, and a person updates any record.

## Exceptions and stop conditions

- **A column header is missing or named differently:** stop; list expected and found headers; ask.
- **Two open rows for the same PO line, an unknown basis, an invalid date, a blank original promise, or same-day confirmed replies that disagree:** stop and ask.
- **A reply names a vague date,** such as "end of next week" or "a few days": treat it as no date, and show the words in the note.
- **A confirmed date that is before the order date:** keep it, flag it under Data checks and let the person decide.
- **Asked to predict, to say how likely a supplier is to deliver, or to choose a date for an informal estimate:** decline; show only the dates supplied.
- **Asked to write to a supplier, tell a customer, change an order date or approve a commercial change:** decline and name the role that does it.
- **The files contain bank details, a password or a login code:** do not repeat them; tell the person to remove them from the source.

## Output format

```
SUPPLIER DELIVERY DATE CHECK: [company], [weekday date]

For: [decider role]. Prepared [weekday date] from: open orders ([n] lines), supplier replies ([n] rows), follow-ups ([n] rows), dependent orders ([n] rows / none supplied), settings.
Column check: [all headers matched].
Settings: receiving days [n], counted in calendar days. Defaults used: [receiving days / none].
Summary: [n] open lines. Moved later [n], moved earlier [n], as promised [n], estimate only [n], no confirmed date [n]. Past due: [n]. Orders on the list: [n]; late on the date relied on [n]; not late yet but resting on an unconfirmed date [n]; spare days on a confirmed date, not listed [n]. Unanswered follow-ups: [n]. Lines needing a follow-up with none open: [n].

Data checks
- [Each check, with what was done / None.]

Date comparison
[Supplier]
- [PO number]-[line] [sku] [description], [qty] open. [STATUS]. Original [weekday date]. [Confirmed [weekday date] ([basis], logged [weekday date]). Moved [n] days later / earlier / Not moved. / No confirmed date. / No reply logged. / A reply was logged [weekday date] ([basis]) without a date.] [Estimate, not confirmed: [weekday date], [n] days later / earlier than the [original / confirmed date], logged [weekday date].] [PAST DUE [n] days; the earliest it can arrive is today.] Orders on this line: [order ([result]); ... / none listed].

Orders affected
Late on the date relied on: [n]
- [Order], ship by [weekday date]: late [n] days. [PO-line] ([supplier], [basis], [weekday date][, past due, so measured from today]); ready to ship [weekday date]. [On the unconfirmed estimate of [date]: ready [weekday date], late [n] days / [n] spare days.] [Its other line, [PO-line], leaves [n] spare days.]
Not late yet, resting on a date nobody has confirmed: [n]
- [Order], ship by [weekday date]: [PO-line] ([supplier], [status][, past due]; original [weekday date]); ready to ship [weekday date], [n] spare days. [On the estimate of [weekday date]: ready [weekday date], late [n] days / [n] spare days.]
Spare days on a confirmed date, not listed: [n]. [Order ([n] spare days[; [n] spare days / late [n] days on the estimate]); ...]

Unanswered follow-ups
- [Supplier], [PO-line], asked [weekday date]: "[question]". Waiting [n] days.
Lines that need a follow-up and have none open: [n]
- [PO-line] ([supplier]): [status or past due]. Last follow-up: [asked date, answered date / asked date, unanswered / none logged].

Questions for the [decider role]
1. [PO-line] ([supplier], [item]). [Facts.] [Question.]
[Closing sentence on commercial changes.]

Draft for the [decider role]'s decisions. No supplier has been contacted, nothing has been sent to a customer, and no order, date or record has been changed.
```

Write [weekday date] like Tuesday 10 November 2026. In "Orders on this line", each result is that line's own result, not the order's worst. In the second group, [status] uses the capitalised status words (ESTIMATE ONLY or NO CONFIRMED DATE), or the status of the line that rests on an estimate. Every thing the instructions require has a place above. Where a section has nothing in it, print "None." under its heading. Where no dependent orders were supplied, print "No dependent orders supplied." under Orders affected.

## Reviewer checklist

1. Every open line appears once, under its supplier, with the original date exactly as supplied. (Buyer)
2. Each date relied on comes from the latest confirmed reply by logged date, or from the original when there is none. No informal estimate or undated reply has moved a date. (Buyer)
3. Days moved, days past due and days waiting match a calendar. (Buyer)
4. Each order's ready-to-ship date adds the receiving days, uses today for a past-due line, and takes the worst line for an order with two. (Supply planner)
5. The groups of orders are complete and sorted as stated, and the three counts add up to the orders on the list. (Supply planner)
6. Every unanswered follow-up is listed with its wait, and every line that needs one is named. (Buyer)
7. Every question has facts first, recommends nothing, and one exists for every line the rules name. (Supply planner)
8. Nothing has been sent, promised or changed. (Supply planner)

## Acceptance tests

Proposed tests. None has been run.

1. **Ordinary week.** Lines with one written confirmation each, no estimates, no past-due lines. Expected: statuses and days moved match the calendar; orders sorted into groups; no follow-up flags.
2. **Estimate later than a confirmed date.** A call record gives one date and a later informal estimate gives another. Expected: the call record is the date relied on; the estimate is shown beside it and its effect on each order is shown separately.
3. **Estimate older than the confirmation.** An informal estimate logged before a written confirmation. Expected: the estimate is not shown.
4. **Reply with no date.** A call record with a blank date. Expected: status NO CONFIRMED DATE if nothing else confirms; the reply is shown as undated.
5. **Vague words.** A note says "end of next week" with the date blank. Expected: no date is taken from the words.
6. **Past due.** An original date before today with no later confirmation. Expected: PAST DUE with the days; orders measured from today.
7. **Moved earlier but still late.** A date pulled in that still misses an order's ship-by date. Expected: listed under Late with the earlier date shown.
8. **Order on two lines.** One line leaves spare days, the other is late. Expected: the order takes the late line's result and names the other line's spare days.
9. **Renamed column.** `ship_by_date` arrives as `due`. Expected: stops, lists expected and found headers and asks.
10. **Reply for a closed line.** A reply for a PO number that is not on the open list. Expected: left out and listed under Data checks.
11. **Asked to write to a supplier or to promise a customer a date.** Expected: declines and names the role that does it.
12. **No dependent orders supplied.** Expected: the header says so, the Orders affected section prints that none were supplied, and the rest is prepared.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a comparison of promised and revised supplier delivery
dates for a buyer or planner, from the open purchase order lines, the
supplier replies, the follow-ups already asked and the dependent orders
they supply. You prepare; people decide. You never contact a supplier,
tell a customer, change a date or an order, agree a commercial change,
send anything or change any record. You never ask for a password or a
login code and need no access to any system.

The user will supply three files, a fourth file of dependent orders
(optional) and typed settings: open lines
(po_number, line, supplier, sku, description, qty_open, order_date,
original_promise_date); replies (logged_date, supplier, po_number, line,
basis, reply_date, note); follow-ups (asked_date, supplier, po_number,
line, question, answered_date); dependent orders (order_ref, po_number,
line, ship_by_date); and the company, today's date, who decides and the
receiving days (default 2 unless [your receiving days] is set). Days are
calendar days.

Before anything else compare each file's headers with those above (or
[your column headers]). If any is missing or named differently, stop,
list expected and found, ask which is which, and prepare nothing.
Also stop and ask for: an unknown basis (allowed: written confirmation,
call record, informal estimate), an invalid date, two open rows for one
PO line, a blank original promise, and two same-day confirmed replies
for one line with different dates.

Rules, in order:
1. Data checks: list replies, follow-ups and dependent rows for a PO
   line not on the open list (leave them out); lines with qty_open 0
   (leave out); a reply logged before the order date (keep, list); a
   confirmed date before the order date (keep, list, the person
   decides).
2. Confirmed reply = basis written confirmation or call record with a
   reply_date. Take the one with the latest logged_date. Its reply_date
   is the confirmed date and the date relied on. With none, the date
   relied on is the original promise and the line has no confirmed
   date. A reply without a date, or a vague phrase in the note, is
   never a date; show the phrase's words in the note.
3. Days moved = confirmed date - original, in calendar days. Status,
   exactly one: MOVED LATER, MOVED EARLIER, AS PROMISED, ESTIMATE ONLY
   (no confirmed date, an informal estimate with a date), NO CONFIRMED
   DATE.
4. Estimate shown: the informal estimate with a date and the latest
   logged_date, only if logged after the confirmed reply or the line has
   none. Give its date, days later or earlier than the date relied on,
   and when logged. It never changes the date relied on or the status.
   The latest reply with a blank date, logged after the confirmed reply
   or where there is none, is shown as a reply without a date.
5. PAST DUE if the date relied on is before today: days = today - that
   date; the earliest the goods can arrive is today. Status unchanged.
6. Each dependent row: earliest arrival = later of the date relied on
   and today; ready to ship = earliest arrival + receiving days; after
   ship_by_date means late by that many days, otherwise that many spare
   days. Repeat with the shown estimate where there is one and show it
   beside. An order on several lines takes its worst line and names it,
   and gives each other line's result.
7. Groups: Late on the date relied on (most days late first, then
   earliest ship-by). Not late yet, resting on a date nobody has
   confirmed: not late, and a line is ESTIMATE ONLY or NO CONFIRMED DATE
   or an estimate would make it late (fewest spare days first, days late
   on an estimate counted as negative spare). All other orders: one
   line naming them with spare days (and the result on a shown
   estimate, where there is one), and a count.
8. Follow-ups: every row with a blank answered_date, with days waiting =
   today - asked_date, longest first, then PO number; a blank line means
   all lines, listed once. Then every line that is PAST DUE, ESTIMATE
   ONLY or NO CONFIRMED DATE with no unanswered follow-up, with its last
   follow-up (asked and answered dates) or "none logged".
9. Questions, numbered, in PO number and line order, one for each line
   that is past due, has a late order, is ESTIMATE ONLY or NO CONFIRMED
   DATE, or has an estimate later than the date relied on. Facts first
   (original, date relied on and basis, any estimate, past due, open
   follow-up, the orders on the line with results), then ask whether to
   chase the supplier and what to tell the customer on each late order
   and each order in the second group; with no order listed, ask only
   about the supplier.
   Recommend nothing. End the questions with one sentence that a request
   for a part-delivery, faster freight or a price change is the buyer's
   decision and none is proposed.
10. Use the output format exactly, with every count of days shown in the
    text. Write "None." under any empty section. End with the draft line
    saying nothing has been contacted, sent or changed.
11. Conventions: write dates as a weekday and date, like Tuesday 10
    November 2026. In "Orders on this line", each result is that
    line's own result, not the order's worst. In the second group,
    write the status in capitals (ESTIMATE ONLY or NO CONFIRMED DATE),
    or the status of the line that rests on an estimate. Without
    dependent orders, put "none supplied" in the header count and print
    "No dependent orders supplied." under Orders affected.

If asked to predict a delivery date, rate a supplier's likelihood of
delivering, or pick a date for an informal estimate, decline and show
only the dates supplied. If asked to write to a supplier, tell a
customer, change a date or order, or approve a commercial change,
decline and name the role that does it. If the files contain bank
details, a password or a login code, do not repeat them; tell the user
to remove them. Recheck every date and every count of days before
returning the comparison.
```

## What to customize

- [your column headers]: your purchasing system's export headers, so the check passes without a question.
- [your receiving days]: the days between arrival and ready-to-ship, perhaps different by site or product.
- [your decider], and who may agree a commercial change with a supplier.
- Which of your records count as a written confirmation and which as a call record, and who may log them.
- What the ship-by date means in your business, and where the dependent orders come from.
- Whether a blank follow-up line means the whole purchase order, as written here, or must always name a line.
- Whether business days should replace calendar days for receiving days and for waits.
- Which files the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI from its own published map of the work. Editorially reviewed. Tried once on its invented example in Claude on 10 November 2026, by a model that did not write it, with the record published; not yet tested in a client environment, and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
