# Unshipped order review: tried on its example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs for this run are the invented example in `public/example.md` (the settings, orders, order lines and active holds under "The inputs"). No client data was used. This is the third run. The first was made by a model that did not write the template; it found nine small ambiguities, and the template was edited to remove them (date format, the bracketed defaults, the wording of an unknown status, the units sum, the Status to confirm count, the number of questions per decision, the wrapping of the instruction block, cancelled orders with shipped units, and the version notes). The second run checked those edits. An independent review then found that the rule said each decision asks one or two questions while decision 1 asked three, and that the format asked for the facts in one or two sentences while several decisions used three. The template was changed so that the facts are given briefly and each decision asks one to three questions, a rule for what to print when the work stops was added to the instruction block, and the description of the orders file was corrected. This third run was made by the model that made those edits, in the same session, not by an independent reader: it read the edited template and the example's inputs, followed the instruction block and the output format, and compared its result with the review printed in the example. The review in the example did not need to change, so the two agree; that agreement is not independent evidence. Earlier runs' outputs are not reproduced here. After that run, a second independent review asked for small edits, which the same model (Claude Sonnet 5.5, in a later step of the same session) then made: the format now says how to print a second hold, how to name two differing missing-next-step kinds, and what to print for a hold with no date placed; the procedure now names a hold on a shipped-in-full or cancelled order, and an order whose lines all have a quantity ordered of 0, rather than dropping them silently; and one wrapped line was tidied. None of those cases is in the example. The example's inputs and the review printed above did not change, and the editor re-read the example's review against the edited format and found it still matches line for line, but the output above was not produced again after these edits. No run since the last edits has been made by a model that did not write the template.

## What came out

All parts of the output format were produced, in the right order, with every age band printed and no section empty by omission. The review was not stopped: the column check passed and no row failed the row checks. The full output follows.

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

## What was observed

- **Every required part was produced.** Header, column check, settings, summary, data checks, the aged list with all four bands, the four lists, the decisions and the closing line.
- **The counts add up.** The kinds (5, 3, 1) and the bands (2, 3, 3, 1) each add to the nine open orders listed. Status to confirm is 3, of which one (A1012, shipped in full) is not on the aged list, as step 12 now says.
- **Nothing was said that is not in the inputs.** Every order number, customer letter, item code, quantity, date and hold detail comes from the example. The calculated values (ages, days past promise, days on hold, days since last shipment, unit counts) were rechecked by hand against the dates.
- **The edits worked as intended on this input.** Dates came out as YYYY-MM-DD throughout; the unknown status was worded "no order line rows"; "11 of 15 units shipped" and "5 of 7" are sums over all lines, complete ones included; each decision gives its facts briefly and asks one to three questions the facts raise (decision 1 asks three, the rest one or two).
- **No hold was called released or expired.** The two holds past the limit are described as in force, and no decision suggests releasing one.
- **Not exercised.** The example has no cancelled order with units shipped, no blank shipped quantity, no written date typed into the settings, no two holds on one order, no hold with no date placed, no hold on a cancelled or shipped-in-full order, no order whose lines are all ordered 0, and no stop condition (a renamed column or a bad row), so the wording for those was not run. The acceptance tests in the template are still proposals and none was run here.

This was one further run on one clean example, made by the editor of the template, and it predates the last small edits described above. The new stop-condition sentence in the instruction block was not exercised, because the run did not stop. It shows the edited instructions can be followed to a complete review on clean data, not how the template behaves on messy exports, and it is not an independent check.
