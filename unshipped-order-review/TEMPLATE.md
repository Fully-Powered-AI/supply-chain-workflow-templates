# Unshipped order review

Workflow template, version 0.1.0.

## Purpose

Prepare the daily review of orders that have not gone out, whole or in part: every open order with its age in calendar days, its promised date, what is still to ship, each hold on it and how long that hold has stood, and the next step with its owner. Orders with no usable next step, holds past the business's limit, part-shipped orders with no recent shipment and statuses that disagree with the order lines each get their own list, and each order that needs a decision becomes a numbered question for the fulfilment lead. Every figure traces to the orders, order lines or holds export. The assistant prepares; it never releases a hold, ships, reassigns or cancels an order, changes a record, contacts a customer or decides a priority.

## When to use it and when not to

Use it at the start of each working day, or whenever the daily order review is due. Run it again after the lead has set the day's priorities if the exports have changed.

Do not use it:

- to review support tickets, which is the stale ticket sweep;
- to judge when a supplier will deliver, which is the supplier delivery date check. A hold reason such as "awaiting stock" is shown as given and never tested;
- to decide what to reorder, which is the inventory reorder plan;
- to write messages to customers. It lists what the lead may want to decide; the customer-service lead writes and sends;
- to decide whether a hold may be lifted. A hold stays in force until a person with authority releases it.

## Roles

- **Runs it:** a fulfilment coordinator, a customer-service lead or the fulfilment lead.
- **Sets priorities, and authorises any release or reassignment:** the fulfilment lead. Always a person.
- **Owns each hold and each next step:** the role named in the holds export.
- **Decides what customers are told:** the customer-service lead, or [your customer contact owner].
- **Releases a hold or changes an order in the order system:** the people the business names. The assistant never does.

## Inputs

The assistant works only from the files the person supplies. It needs no connection to the order system and never asks for a password or a login code. It works with any order system that can export these three lists. Dates in the files are written YYYY-MM-DD. The settings may give today's date in words; the assistant reads it as that date and, like every other date in the review, writes it as YYYY-MM-DD.

1. **The orders.** One row per order in the export, including any marked shipped or cancelled. Default column headers: `order_number`, `order_date`, `customer`, `promised_date`, `order_status`.
2. **The order lines.** One row per line of those orders. Default column headers: `order_number`, `line`, `item_code`, `qty_ordered`, `qty_shipped`, `last_ship_date`. A blank `qty_shipped` means unknown, not zero. `last_ship_date` is blank where nothing has shipped.
3. **The active holds.** One row per hold now in force. Default column headers: `order_number`, `hold_reason`, `hold_placed_date`, `hold_owner`, `next_step`, `next_step_owner`. An order with no row has no hold recorded. An order with two rows has two holds.
4. **The settings,** typed: the business; today's date; the name or role of the fulfilment lead; the age bands; which `order_status` words mean shipped and which mean cancelled; the hold limit; the part-shipment limit. Defaults when a setting is not given:
   - age bands in whole calendar days from the order date: 0 to 2, 3 to 5, 6 to 10, over 10, with the first (youngest) band as the grace band;
   - shipped status: `shipped`. Cancelled status: `cancelled`. Any other word means open;
   - hold limit, default 5 days: a hold is past the limit when it has stood for more than 5 days;
   - part-shipment limit, default 3 days: a part-shipped order is past the limit when its last shipment was more than 3 days ago.

   The Settings line names, after "Defaults used", each setting that came from a default.

**Column check.** Before anything else, compare each file's headers with the defaults, or with [your column headers] if the business has set its own. If a header is missing or named differently, stop. List, for each file, the headers expected and the headers found, ask which column is which, and prepare nothing else. Never guess a column.

## The procedure

1. **Check the columns,** as above.
2. **Check the rows.** Stop, list every problem row, ask, and prepare nothing else when: an order number is blank or appears twice in the orders file; an `order_date` is blank, is not a date or is after today; a `promised_date`, `last_ship_date` or `hold_placed_date` is filled in but is not a date; a `qty_ordered` is blank, negative or not a whole number; or a filled-in `qty_shipped` is negative or not a whole number. A blank `promised_date` or `hold_placed_date` is allowed and is reported as "promise not given" or "date not given".
3. **Run the data checks.** These do not stop the work. List each under Data checks and say what was done:
   - a line or a hold whose order is not in the orders file is left out;
   - a line whose `qty_shipped` is above `qty_ordered` is treated as shipped in full for that line;
   - two holds on one order are both shown;
   - a hold row on an order that is left out as shipped in full or cancelled is not shown on the aged list; it is listed here with its reason and date, for the lead to see;
   - a hold with no `hold_placed_date` has no age that can be worked out: it is listed here, and it is never put under Holds past the limit.
4. **Settle what has shipped, from the lines.** The order lines decide what has shipped; the `order_status` word never says that an order has shipped. It decides one thing only: an order whose status is a cancelled word is taken out before its lines are sorted.
   - An order whose status is a cancelled word is left out and counted. If any of its lines shows units shipped, it is also put under Status to confirm (step 5).
   - An order with no line rows, or with any line whose `qty_shipped` is blank, is **status unknown**. It is never read as shipped.
   - An order whose every line has `qty_ordered` 0 is also **status unknown**, written "no units ordered"; it is never read as shipped in full.
   - Otherwise, an order whose every line has `qty_shipped` at or above `qty_ordered` is **shipped in full**: left out of the aged list and counted.
   - Otherwise, an order with no unit shipped on any line is **unshipped**.
   - Otherwise it is **part-shipped**.
5. **Find the statuses to confirm.** An order goes under Status to confirm when: its status is a shipped word but the lines show it unshipped, part-shipped or unknown; its lines show shipped in full but its status is not a shipped word; or it is status unknown (including no units ordered). A cancelled order with any line showing units shipped goes there too. Say what the status word says and what the lines show. The lines still decide where an open order is listed: shipped in full stays off the aged list, and a cancelled order stays off it. So the Status to confirm count is not a subset of the open orders listed: it can include orders that are shipped in full or cancelled and so are not on the aged list.
6. **Age every open order.** Age = today − `order_date`, in calendar days. Put it in its band. Days past promise = today − `promised_date` when that is a date before today; an order promised today or later is not past its promise.
7. **Attach the holds.** Show each hold row on its order: reason, date placed, days stood (today − `hold_placed_date`) and owner, or "owner not named". A hold with no `hold_placed_date` is shown as "date placed not given, days not known". A hold is past the limit when it has stood longer than the hold limit; one with no date placed cannot be judged and is not put under Holds past the limit. An order with two holds shows both, in the order of the holds file. Never treat a hold as expired because of its age.
8. **Find the missing next steps.** An order has a usable next step only when it has at least one hold row and every hold row has both a `next_step` and a `next_step_owner`. Otherwise it is missing one, and the kind is:
   - "no hold recorded, no next step", when there is no hold row;
   - "hold without a next step", when a hold row has no `next_step`;
   - "next step without an owner", when a hold row has a `next_step` and no `next_step_owner`.

   When an order has two holds and they differ, name every kind that applies, in the order above, separated by semicolons, once each. Show any step text given on either hold.

   An order in the grace band with no hold row is not missing a next step; it is shown as "within the first band with no hold". An order in the grace band that has a hold row is checked like any other.
9. **Work out what is still to ship,** for each unshipped or part-shipped order: for each line, `qty_ordered` − `qty_shipped` where that is above zero, listed by item code. For a part-shipped order, "[n] of [n] units shipped" is the sum of `qty_shipped` over all its lines (each line counted no higher than its `qty_ordered`) against the sum of `qty_ordered` over all its lines; lines already complete are included. Days since the last shipment = today − the latest `last_ship_date`; it is past the part-shipment limit when that is more than the limit. If no shipped line has a date, write "last shipment date not given". For a status-unknown order, write "units not known".
10. **Order everything.** The aged list runs from the oldest band to the youngest, and within a band by age, oldest first, ties by order number. Every other list uses the same order.
11. **Write the decisions.** One numbered decision for each order that appears under Missing next step, Holds past the limit, Part-shipped with no recent shipment or Status to confirm, in the order of the aged list, then any order that is only under Status to confirm and not on the aged list, by order number. Give the facts briefly, then one to three questions for the fulfilment lead, asking only those the facts raise: who owns the next step, whether the hold stays in force, whether the lines or the status word are right, whether the customer is to be told, who takes over. Recommend nothing. Never suggest that a hold be released.
12. **Write the header and summary.** Count the open orders listed and their kinds, those left out, the orders in each band, the orders with and without a hold, those missing a next step, those within the grace band with no hold, those past their promised date, the units still to ship and the orders they cover, the orders whose units are not known, the orders with a hold past the limit, the part-shipped orders past the limit and the orders under Status to confirm; that last count may include orders that are not on the aged list (shipped in full, or cancelled with units shipped), so it is not a subset of the open orders listed. The unshipped, part-shipped and status-unknown counts add up to the open orders listed, and so do the band counts.
13. **Return the draft** to the person who ran it. A person decides each action and takes it.

## Exceptions and stop conditions

- **A column header is missing or named differently:** stop; list expected and found headers; ask.
- **A row fails the checks in step 2:** stop; list the rows; prepare nothing else.
- **An order has no line rows, or a blank shipped quantity:** never read it as shipped. List it as status unknown.
- **A hold is old:** it stays in force. Report its age and leave it for the lead.
- **Asked to release or add a hold, ship, cancel or reassign an order, change a status, or send or write a message to a customer:** decline. Say that the lead decides and the named people act.
- **Asked to say which order a customer should be favoured on, or to rank by customer value:** decline; the lead sets priorities. The list is ordered by age only.
- **Asked to say when a supplier will deliver, or whether stock will arrive:** decline; point to the supplier delivery date check.
- **The files contain card numbers, bank details, a password or a login code:** do not repeat them; tell the person to remove them from the source.

## Output format

```
UNSHIPPED ORDER REVIEW: [business], [weekday] [YYYY-MM-DD]

For: [fulfilment lead]. Prepared from: orders ([n] rows), order lines ([n] rows), holds ([n] rows), settings.
Column check: all headers matched. / Stopped: [file]: expected [headers]; found [headers].
Settings: age bands [bands], first band [band] needs no explanation; shipped status [words]; cancelled status [words]; hold limit [n] days; part-shipment limit [n] days. Defaults used: [settings taken from a default / none].
Summary: [n] open orders listed: unshipped [n], part-shipped [n], status unknown [n]. Left out: shipped in full [n], cancelled [n]. By age: [band] [n], [band] [n], [band] [n], [band] [n]. With a hold [n]; no hold [n]. Next step missing [n]; within the first band with no hold [n]. Past promised date [n]. Still to ship [n] units across [n] orders; units not known for [n]. Holds past the limit [n]. Part-shipped with no recent shipment [n]. Status to confirm [n].

Data checks
[Finding; what was done.]
/ No problems found.

Aged list
[Band] ([n])
[Order] [customer]. Ordered [YYYY-MM-DD], [n] days. Promised [YYYY-MM-DD], [n] days past. / Promised [YYYY-MM-DD]. / Promise not given. [Unshipped: [n] units to ship, [item] [n]. / Part-shipped: [n] of [n] units shipped, last shipment [YYYY-MM-DD], [n] days ago / last shipment date not given; still to ship [item] [n]. / Status unknown: [no order line rows / a blank shipped quantity on line [n] / no units ordered]; units not known.] [Hold: [reason], placed [YYYY-MM-DD], [n] days, owner [role / owner not named]. / Hold: [reason], date placed not given, days not known, owner [role / owner not named].] [A second hold, if the order has one, in the same form after the first.] / No hold recorded. [Next step: [step], [owner]. (one for each hold) / Next step missing: [kind, or kinds separated by semicolons][ ("[step]" where one is given)]. / Within the first band with no hold.]
/ None.

Missing next step
[Order]: [kind, or kinds separated by semicolons]; [n] days old. See decision [n].
/ None.

Holds past the limit
[Order]: [reason], [n] days against a limit of [n]; owner [role / owner not named]. See decision [n].
/ None.

Part-shipped with no recent shipment
[Order]: last shipment [YYYY-MM-DD], [n] days ago against a limit of [n]; still to ship [item] [n]. See decision [n].
/ None.

Status to confirm
[Order]: status says [word]; the lines show [shipped in full / unshipped / part-shipped / units shipped / no line rows / a blank shipped quantity / no units ordered]. See decision [n].
/ None.

Decisions for [fulfilment lead]
[n]. [The facts, briefly. The question or questions, one to three.]
/ None.

Draft for [fulfilment lead]'s decision. Nothing has been released, shipped, reassigned, changed or sent, and no hold has been lifted. Ages are in calendar days to [YYYY-MM-DD].
```

Under "Aged list" print every band from the oldest to the youngest, each with its count, and "None." under a band with no orders. If the work stops, print the header lines that are known, the reason on the Column check line or under Data checks, and the closing line, and leave out the other sections.

## Reviewer checklist

1. Every header matched, or the work stopped. (Fulfilment coordinator)
2. Each order's age is today minus its order date, and sits in the right band. (Fulfilment coordinator)
3. Every order is listed once, or left out as shipped in full or cancelled, and the kinds and the bands each add up to the open orders listed. (Fulfilment coordinator)
4. No order is shown as shipped on the strength of a status word, or of a missing record. (Fulfilment lead)
5. Every hold in the holds export appears on its order with its age, and none is described as released or expired. (Fulfilment lead)
6. Every order without a usable next step, every hold past the limit and every part-shipped order past the limit is in its list. (Fulfilment lead)
7. Every status to confirm matches the lines. (Fulfilment lead)
8. Each decision is a question, recommends nothing and suggests no release. (Fulfilment lead)
9. Nothing is ranked by customer or value, and no customer message is drafted. (Customer-service lead)

## Acceptance tests

Proposed tests. None has been run.

1. **Normal morning.** Nine open orders across all four bands, some part-shipped. Expected: every order once, band counts and kind counts both add to nine, and the sections complete.
2. **Renamed column.** The lines file has `shipped_qty` instead of `qty_shipped`. Expected: stops; lists expected and found headers.
3. **Marked shipped, line open.** Status `shipped`, one line with units still to go. Expected: listed as part-shipped from the lines and under Status to confirm.
4. **No line rows.** An order in the orders file with no lines. Expected: status unknown, listed, units not known, under Status to confirm; not read as shipped.
5. **Lines complete, status open.** Expected: left out of the aged list, counted as shipped in full, under Status to confirm.
6. **Hold with no next step.** Expected: "hold without a next step"; in Missing next step; a decision.
7. **Next step with no owner.** Expected: "next step without an owner".
8. **Old hold.** A hold placed 13 days ago with a limit of 5. Expected: under Holds past the limit; still shown as in force; the decision does not suggest releasing it.
9. **Two holds on one order.** One has a next step and an owner, the other has none. Expected: both holds shown; the order is missing a next step, with the kind of the hold that lacks one.
10. **Youngest band, no hold.** Expected: "within the first band with no hold"; not in Missing next step.
11. **Order date in the future.** Expected: stops; lists the row.
12. **Hold for an unknown order.** Expected: left out and listed under Data checks.
13. **Asked to release the oldest hold.** Expected: declines; the lead decides.
14. **Asked to rank by customer.** Expected: declines; the list stays in age order.
15. **Cancelled, but shipped.** Status `cancelled`, one line with units shipped. Expected: left out of the aged list and counted as cancelled, and under Status to confirm with a decision.
16. **Hold on an order that is shipped in full or cancelled.** Expected: the hold is not on the aged list and is named under Data checks.
17. **Every line ordered 0.** Expected: status unknown, "no units ordered", under Status to confirm; not read as shipped.
18. **Hold with no date placed.** Expected: shown as "date placed not given, days not known"; not under Holds past the limit; named under Data checks.
19. **Two holds that differ.** One lacks a next step, the other lacks an owner for its step. Expected: both kinds named, separated by a semicolon.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare the daily unshipped order review: the orders not yet sent,
whole or in part, aged, with what holds them and who owns the next step.
You prepare; people decide. You never release or add a hold, ship,
cancel or reassign an order, change a status or any record, contact a
customer, or decide a priority. Anything that sends, posts, pays or
changes a record waits for a person's approval. You need no access to
any system and never ask for a password or a login code.

Inputs: orders (order_number, order_date, customer, promised_date,
order_status); order lines (order_number, line, item_code, qty_ordered,
qty_shipped, last_ship_date; a blank qty_shipped is unknown, not zero);
active holds (order_number, hold_reason, hold_placed_date, hold_owner,
next_step, next_step_owner; no row means no hold recorded); settings
(business, today, fulfilment lead, age bands default 0 to 2, 3 to 5,
6 to 10, over 10 calendar days with the first as the grace band, shipped
status word default "shipped", cancelled status word default
"cancelled", hold limit default 5 days, part-shipment limit default 3
days). Dates are YYYY-MM-DD; write every date in the review that
way, and read a written date in the settings as that date. Name, after
"Defaults used", each setting taken from a default, or say none.

1. Column check: compare every header with the list above, or with the
   business's own headers if given. If any is missing or named
   differently, stop, list expected and found headers, ask, and prepare
   nothing else.
2. Stop, list the rows and prepare nothing else if: an order number is
   blank or repeated in the orders file; an order_date is blank, not a
   date or after today; a filled-in promised_date, last_ship_date or
   hold_placed_date is not a date; qty_ordered is blank, negative or not
   a whole number; a filled-in qty_shipped is negative or not a whole
   number. A blank promised_date or hold_placed_date is allowed: write
   "promise not given" or "date not given".
3. Data checks, which do not stop the work: leave out lines and holds
   for an order not in the orders file; treat a line shipped above its
   ordered quantity as shipped in full; show two holds on one order;
   name any hold on an order left out as shipped in full or cancelled;
   name any hold with no date placed.
4. The lines decide what has shipped; a status word never says that an
   order has shipped. Cancelled status: leave out and count. No line
   rows, or any blank qty_shipped: status unknown, never shipped. Every
   line with qty_ordered 0: status unknown, "no units ordered". Every
   line at or above its ordered quantity: shipped in full, leave out and
   count. No unit shipped: unshipped. Otherwise part-shipped.
5. Status to confirm: a shipped status word with lines that show
   unshipped, part-shipped or unknown; lines shipped in full with a
   status that is not a shipped word; a cancelled status with any line
   showing units shipped; any status-unknown order. Say what the word
   says and what the lines show.
6. Age = today - order_date in calendar days, in its band. Days past
   promise = today - promised_date when that date is before today.
7. Show every hold row on its order: reason, date placed, days stood,
   owner or "owner not named". A hold with no date placed: "date placed not given,
   days not known"; it is never past the limit. Past the limit means
   stood longer than the hold limit. A hold stays in force however old it is; never
   describe one as expired or suggest releasing one.
8. A usable next step needs at least one hold row, and every hold row
   needs a next_step and a next_step_owner. Otherwise the order is
   missing one (show any step text that was given): "no hold recorded,
   no next step", "hold without a next step" or "next step without an
   owner". With two holds that differ,
   name each kind once, separated by semicolons. An order in the grace
   band with no hold row is "within the first band with no hold", not
   missing; with a hold row it is checked like any other.
9. Still to ship: qty_ordered - qty_shipped where above zero, by item
   code. Part-shipped: days since the latest last_ship_date, past the
   limit when more than the part-shipment limit; if no date, "last
   shipment date not given". "n of n units shipped" sums all lines,
   complete ones included, each shipped figure capped at its ordered
   quantity. Status unknown: write "no order line rows", "a blank
   shipped quantity on line n" or "no units ordered", then "units not known".
10. Order the aged list oldest band first, then oldest age, ties by order
   number; every other list in the same order.
11. Decisions: one numbered decision for each order under Missing next
   step, Holds past the limit, Part-shipped with no recent shipment or
   Status to confirm, in aged-list order, then orders only under Status
   to confirm by order number. The facts, briefly, then one to
   three questions for the fulfilment lead, only those the facts raise.
   Recommend nothing. Do not rank by customer or value
   and do not draft a customer message.
12. Summary: the kinds add up to the open orders listed, and so do the
   bands. The Status to confirm count may include orders not on the
   aged list (shipped in full, or cancelled with units shipped). Use the
   output format exactly. Print every band, with "None." under an empty
   one, and "None." under any empty section. End with the draft line.
   Recheck every age and count before returning the draft.
13. If the work stops (step 1 or 2), print only the header lines that
   are known, the reason on the Column check line or under Data checks,
   and the closing line; leave out every other section.

If asked to release or add a hold, ship, cancel, reassign, change a
status, or write or send a message, decline and say the lead decides. If
asked to judge a supplier's date, decline. If the files contain card
numbers, bank details, a password or a login code, do not repeat them;
tell the user to remove them.
```

## What to customize

- [your column headers]: the headers your order system exports, so the column check passes without a question.
- Your age bands, and which band is young enough to need no explanation.
- Your shipped and cancelled status words. Any other status that should leave the list needs a step added to the procedure, which as written drops only the shipped and cancelled words.
- Your hold limit and your part-shipment limit (the defaults are 5 days and 3 days).
- How your holds are recorded, and whether a hold may have several owners.
- Who may release a hold, who may reassign an order, and who tells the customer.
- Counting ages in working days instead of calendar days. The procedure counts calendar days only, so this needs the procedure and the output format edited, not just a setting.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Editorially reviewed. Tried on its invented example on 10 November 2026 in Claude; the record is published with it. Not yet tested in a client environment.
