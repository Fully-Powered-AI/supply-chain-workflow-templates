# Supplier delivery date check: trial on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example in [example.md](example.md): the five input blocks (settings, open lines, supplier replies, follow-ups, dependent orders). No client data was used. The run was done by a model that did not write the template. It read the template and the inputs first, followed the fenced instruction block and the output format, produced the comparison, and only then read the published example's output and the reviewer checklist. The instruction block was read from the file as written; it was not pasted into a separate chat, so this trial does not test the pasting step.

## What came out

All twelve parts of the format were produced. Nothing in the inputs triggered a stop: the column check passed, no basis was unknown, no date was invalid, no line was duplicated and no same-day confirmed replies disagreed.

```
SUPPLIER DELIVERY DATE CHECK: the Company, Tuesday 10 November 2026

For: the supply planner. Prepared Tuesday 10 November 2026 from: open orders (8 lines), supplier replies (9 rows), follow-ups (5 rows), dependent orders (11 rows), settings.
Column check: all headers matched.
Settings: receiving days 2, counted in calendar days. Defaults used: receiving days.
Summary: 8 open lines. Moved later 2, moved earlier 1, as promised 2, estimate only 1, no confirmed date 2. Past due: 2. Orders on the list: 10; late on the date relied on 4; not late yet but resting on an unconfirmed date 3; spare days on a confirmed date, not listed 3. Unanswered follow-ups: 3. Lines needing a follow-up with none open: 1.

Data checks
- Reply for PO-2099 line 1 (Supplier A, logged Monday 2 November) is not on the open orders. Left out; read as closed or mistyped.

Date comparison
Supplier A
- PO-2101-1 FRM-10 Steel frame set, 120 open. MOVED LATER. Original Monday 2 November. Confirmed Monday 16 November (written confirmation, logged Wednesday 28 October). Moved 14 days later. Orders on this line: CO-5301 (late 5 days), CO-5302 (7 spare days), CO-5307 (6 spare days).
- PO-2101-2 BRK-04 Brake caliper pair, 300 open. AS PROMISED. Original Monday 2 November. Confirmed Monday 2 November (written confirmation, logged Wednesday 28 October). Moved 0 days. PAST DUE 8 days; the earliest it can arrive is today. Orders on this line: CO-5303 (late 1 day).
Supplier B
- PO-2102-1 SAD-22 Saddle, 500 open. MOVED LATER. Original Friday 20 November. Confirmed Friday 27 November (call record, logged Tuesday 3 November). Moved 7 days later. Estimate, not confirmed: Friday 4 December, 7 days later than the confirmed date, logged Monday 9 November. Orders on this line: CO-5304 (late 2 days; late 9 days on the estimate), CO-5305 (11 spare days; 4 spare days on the estimate).
- PO-2103-1 GRP-07 Handlebar grip set, 800 open. NO CONFIRMED DATE. Original Tuesday 24 November. No reply logged. Orders on this line: CO-5308 (0 spare days).
Supplier C
- PO-2104-1 WHL-31 Wheel rim 26in, 240 open. ESTIMATE ONLY. Original Thursday 12 November. Estimate, not confirmed: Thursday 19 November, 7 days later than the original, logged Friday 6 November. Orders on this line: CO-5306 (4 spare days; late 3 days on the estimate).
- PO-2105-1 CHN-02 Chain, 400 open. MOVED EARLIER. Original Monday 30 November. Confirmed Monday 23 November (written confirmation, logged Thursday 5 November). Moved 7 days earlier. Orders on this line: CO-5307 (late 1 day).
Supplier D
- PO-2106-1 PED-15 Pedal pair, 260 open. AS PROMISED. Original Tuesday 1 December. Confirmed Tuesday 1 December (written confirmation, logged Wednesday 4 November). Moved 0 days. Orders on this line: CO-5310 (1 spare day).
- PO-2107-1 TYR-09 Tyre 26in, 600 open. NO CONFIRMED DATE. Original Friday 6 November. A reply was logged Monday 9 November (call record) without a date. PAST DUE 4 days; the earliest it can arrive is today. Orders on this line: CO-5309 (1 spare day).

Orders affected
Late on the date relied on: 4
- CO-5301, ship by Friday 13 November: late 5 days. PO-2101-1 (Supplier A, written confirmation, Monday 16 November); ready to ship Wednesday 18 November.
- CO-5304, ship by Friday 27 November: late 2 days. PO-2102-1 (Supplier B, call record, Friday 27 November); ready to ship Sunday 29 November. On the unconfirmed estimate of Friday 4 December: ready Sunday 6 December, late 9 days.
- CO-5303, ship by Wednesday 11 November: late 1 day. PO-2101-2 (Supplier A, written confirmation, Monday 2 November, past due so counted from today); ready to ship Thursday 12 November.
- CO-5307, ship by Tuesday 24 November: late 1 day. PO-2105-1 (Supplier C, written confirmation, Monday 23 November); ready to ship Wednesday 25 November. Its other line, PO-2101-1, leaves 6 spare days.
Not late yet, resting on a date nobody has confirmed: 3
- CO-5306, ship by Wednesday 18 November: PO-2104-1 (Supplier C, ESTIMATE ONLY; original Thursday 12 November); ready to ship Saturday 14 November, 4 spare days. On the estimate of Thursday 19 November: ready Saturday 21 November, late 3 days.
- CO-5308, ship by Thursday 26 November: PO-2103-1 (Supplier B, NO CONFIRMED DATE; original Tuesday 24 November); ready to ship Thursday 26 November, 0 spare days.
- CO-5309, ship by Friday 13 November: PO-2107-1 (Supplier D, NO CONFIRMED DATE; original Friday 6 November); ready to ship Thursday 12 November, 1 spare day.
Spare days on a confirmed date, not listed: 3. CO-5302 (7 spare days); CO-5305 (11 spare days); CO-5310 (1 spare day).

Unanswered follow-ups
- Supplier A, PO-2101-2, asked Thursday 5 November: "Has the shipment left". Waiting 5 days.
- Supplier C, PO-2104-1, asked Friday 6 November: "Is the estimate a firm date". Waiting 4 days.
- Supplier D, PO-2107-1, asked Monday 9 November: "What is the delivery date and the reason for the delay". Waiting 1 day.
Lines that need a follow-up and have none open: 1
- PO-2103-1 (Supplier B): NO CONFIRMED DATE. Last follow-up: none logged.

Questions for the supply planner
1. PO-2101-1 (Supplier A, Steel frame set). Original Monday 2 November; relied on Monday 16 November (written confirmation), 14 days later. Not past due. No follow-up open. CO-5301 is late 5 days; CO-5302 and CO-5307 have 7 and 6 spare days. Do you want to chase Supplier A, and what will you tell the customer on CO-5301?
2. PO-2101-2 (Supplier A, Brake caliper pair). Original and confirmed Monday 2 November (written confirmation); PAST DUE 8 days. Open follow-up asked Thursday 5 November, waiting 5 days. CO-5303 is late 1 day. Do you want to chase Supplier A, and what will you tell the customer on CO-5303?
3. PO-2102-1 (Supplier B, Saddle). Original Friday 20 November; relied on Friday 27 November (call record). Informal estimate Friday 4 December, logged Monday 9 November, 7 days later. Not past due. No follow-up open. CO-5304 is late 2 days (9 on the estimate); CO-5305 has 11 spare days (4 on the estimate). Do you want to chase Supplier B, and what will you tell the customer on CO-5304?
4. PO-2103-1 (Supplier B, Handlebar grip set). Original Tuesday 24 November; no reply logged; NO CONFIRMED DATE. No follow-up logged. CO-5308 has 0 spare days. Do you want to chase Supplier B, and what will you tell the customer on CO-5308?
5. PO-2104-1 (Supplier C, Wheel rim 26in). Original Thursday 12 November; only an informal estimate of Thursday 19 November, logged Friday 6 November. Open follow-up asked Friday 6 November, waiting 4 days. CO-5306 has 4 spare days on the original and is late 3 days on the estimate. Do you want to chase Supplier C, and what will you tell the customer on CO-5306?
6. PO-2105-1 (Supplier C, Chain). Original Monday 30 November; relied on Monday 23 November (written confirmation), 7 days earlier. No follow-up open. CO-5307 is late 1 day. Do you want to chase Supplier C, and what will you tell the customer on CO-5307?
7. PO-2107-1 (Supplier D, Tyre 26in). Original Friday 6 November; a call record logged Monday 9 November named no date; PAST DUE 4 days. Open follow-up asked Monday 9 November, waiting 1 day. CO-5309 has 1 spare day if the goods arrive today. Do you want to chase Supplier D, and what will you tell the customer on CO-5309?
A request to a supplier for a part-delivery, faster freight or a price change is the buyer's decision and none is proposed.

Draft for the supply planner's decisions. No supplier has been contacted, nothing has been sent to a customer, and no order, date or record has been changed.
```

## What was observed

Compared with the published example's output after the run:

- **Every figure matched.** Statuses, days moved, past-due counts, ready-to-ship dates, spare and late days, the three order groups and their order, the three unanswered follow-ups with their waits, the one line needing a follow-up, the seven questions and the summary counts were the same as the example's. The three order counts (4, 3, 3) add up to the ten orders.
- **Every required part was produced,** and the reviewer checklist's eight points held on this output.
- **Wording differences only.** The example prints the header as a bulleted list; I used the format block as written. My questions give the facts line by line; the example's are more narrative, and the example's question 2 adds that CO-5303 "cannot be ready before Thursday 12 November" and question 7 adds "fewer for each day after". Those two additions are arithmetic from the inputs, not new facts, but they go beyond what the format asks for. I wrote "Moved 0 days" for the two AS PROMISED lines; the example writes "Not moved". I also asked "what will you tell" where the example asks "what do you tell". The example also prints ", past due" on the CO-5309 line in the second group, which my run left off (the PO-2107-1 line already says PAST DUE 4 days), and gives CO-5305's estimate result (4 spare days) in the "not listed" line, which my run left off too.
- **No fact outside the inputs** appeared in my output. In the example, the only content not stated in the inputs is derived arithmetic (the two additions above) and the weekday names, which follow from the calendar.
- **Nothing in the template told me to stop.** The stop conditions were not exercised by this example, so this trial says nothing about them. The same goes for a blank follow-up line meaning the whole purchase order, a vague date in a note, a reply logged before its order date and a missing dependent-orders file.

Where the instructions were ambiguous and I had to choose:

1. **What "result" means in "Orders on this line".** For an order that waits on two lines, the format does not say whether each line shows the order's worst result or that line's own result. I showed the line's own result (CO-5307 is "6 spare days" under PO-2101-1 and "late 1 day" under PO-2105-1), as the example does. A reader could take it the other way.
2. **Estimate results in the "not listed" group.** The format for that line has room only for the order and its spare days. The example adds the estimate's effect for CO-5305 ("4 on the estimate"). I left it out, since step 9 does not ask for it, but it is useful information and the template should say whether to include it.
3. **Group 2's third condition.** CO-5305 has a shown estimate that does not make it late, so it falls into the "not listed" group. The rule reads correctly, but only after thinking through "an estimate that would make the order late" for each order. A short worked case in the template would help.
4. **"Tight" in step 11.** The question asks about "each late or tight order", and "tight" is not defined. I read it as an order in the second group or with few spare days. The example treats the orders in the second group as the tight ones.
5. **Date format.** The format block says "[weekday date]" without a pattern. I took "Tuesday 10 November 2026" from the settings line. Another run could write "Tue 10 Nov".
6. **Wording of status in the groups.** The format shows "[status]" in the second group; I used the capitalised status words, which fits, but the format does not say.
7. **Header layout.** The format block shows the header as plain lines, and the example shows bullets. Both are consistent with the template; the instruction block says "use the output format exactly", which favours plain lines.

Shortcomings of this trial: it is one run, by one model, on one invented example, in one product; the instruction block was followed from the file and not pasted into a fresh chat with the files attached; and the checks that the template says must stop the work were not triggered. It is not a test in a client environment.

## After the trial

The recorded run above is unchanged. After the trial runner's comparison with the published example (the "What was observed" section above), and again after a later independent review, the template and the published example were edited. The first edit settled the ambiguities listed above and the differences from the example: the format now says that a multi-line order shows each line's own result, allows an estimate's result on the "not listed" line, removes the undefined word "tight" and names the second group directly (not late yet, resting on a date nobody has confirmed), gives the weekday date pattern, says the second group uses the capitalised status words, and shows "Not moved" for a zero move. The example now follows the format (plain header lines, the basis and date on the late-group lines, no derived phrases in questions 2 and 7, and the status words in capitals). The later edits capitalised the status words in the example's second group and its follow-up line, added to questions 1, 3 and 6 the other orders on the line with their results, moved the format conventions into the instruction block, and added to the instruction block the optional dependent-orders file, the confirmed date before the order date and the words of a vague phrase. The template was not re-run on the edited wording, so this record describes the earlier wording; the edits are clarifications that this example's inputs already followed, but that is my reading and not a second run.
