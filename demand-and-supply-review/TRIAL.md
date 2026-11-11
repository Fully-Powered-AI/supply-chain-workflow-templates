# Demand and supply review: tried on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs are the invented example in `public/example.md` (Company A, four items, the settings and five files). No client data was used. This is the second recorded pass. An independent review of the first pass found two blocking faults and a list of gaps in the instruction block; the template, the example and the profile were then corrected, and the template was run again from its instruction block and output format. The model that made the corrections ran this pass by hand, without a script, and had already read the example's review, so this pass is not independent of it. Nothing was changed to make a figure agree.

## Inputs used

The six inputs under "The inputs" in `public/example.md`: settings, stock, demand plan, supply commitments, capacity and earlier decisions.

## What came out

```
DEMAND AND SUPPLY REVIEW: December 2026

For: Operations lead, for the monthly review on Tuesday 1 December 2026. Periods: 2026-12 to 2027-02. Units as supplied; values at unit cost from the stock file.
Inputs: demand plan demand.csv; supply supply.csv; stock stock.csv; capacity capacity.csv; earlier decisions decisions.csv.
Items: 4 reviewed, 0 not tested.

Summary
Short on confirmed demand: C1, largest shortfall 20 units in 2027-02.
Short on likely demand: A1, largest shortfall 200 units in 2027-02; C1, largest shortfall 20 units in 2027-02.
Below safety stock but not short: none.
Excess stock: A2, 300 units, $3,450.
Short if sales ambition is added: A1, largest shortfall 550 units in 2027-02; C1, largest shortfall 510 units in 2027-02.

Gaps: demand the supply plan cannot cover
A1 Large planter
Balance by period, confirmed demand: 2026-12 350; 2027-01 300; 2027-02 300.
Balance by period, likely demand: 2026-12 200; 2027-01 0; 2027-02 -200.
Balance by period, with sales ambition: 2026-12 100; 2027-01 -200; 2027-02 -550.
Confirmed demand: covered, lowest balance 300 in 2027-01.
Likely demand: first short 2027-02, largest shortfall 200 in 2027-02. Below safety stock of 150 first in 2027-01.
Sales ambition: 350 units over the periods; first short 2027-01, largest shortfall 550 in 2027-02.
Supply requested, not confirmed: 100 in 2027-01 from Own production. Largest likely shortfall if all were confirmed: 100 in 2027-02.
Capacity room by period: 2026-12 50; 2027-01 0; 2027-02 100.

C1 Self-watering insert
Balance by period, confirmed demand: 2026-12 120; 2027-01 40; 2027-02 -20.
Balance by period, likely demand: 2026-12 120; 2027-01 40; 2027-02 -20.
Balance by period, with sales ambition: 2026-12 -80; 2027-01 -310; 2027-02 -510.
Confirmed demand: first short 2027-02, largest shortfall 20 in 2027-02.
Likely demand: first short 2027-02, largest shortfall 20 in 2027-02. Below safety stock of 60 first in 2027-01.
Sales ambition: 490 units over the periods; first short 2026-12, largest shortfall 510 in 2027-02. Supported units moved to ambition for lack of a basis: 40 in 2027-02.
Supply requested, not confirmed: 100 in 2027-01 from Supplier A. Largest likely shortfall if all were confirmed: none.
Capacity room by period: 2026-12 0; 2027-01 50; 2027-02 150.

Inventory implications
A1: below safety stock from 2027-01 (balance 0 against 150), then short by 200 in 2027-02.
C1: below safety stock from 2027-01 (balance 40 against 60), then short by 20 in 2027-02.
A2: excess. Likely balance in 2027-02 is 800 against an allowance of 500 (safety stock 200 plus average monthly likely demand 300): 300 units over, $3,450 at $11.50 a unit.
No other item is below safety stock or holds excess.

Not tested
None.

Decisions needed from each function head
Sales head (4)
1. A1. Likely demand exceeds confirmed supply by 200 units in 2027-02; confirmed demand is covered. Supported units for A1 are 150, 150 and 200 across the three periods. Do those supported units still stand, and if supply stays as it is, whose supported volume is met first?
2. C1. Confirmed orders exceed supply by 20 units in 2027-02 (60 units confirmed, none supplied; the 40 units left over from 2027-01 cover part of them). Could any of the confirmed C1 orders for 2027-02 be met in a later period?
3. C1. The 40 supported units in 2027-02 have no basis in the demand plan, so they are counted as sales ambition. What is the basis for them, or should they stay as ambition?
4. A1 and C1. Sales ambition is 350 units for A1 and 490 for C1 and is untested against any order or stated basis. If it were added, A1 would be short by 550 units and C1 by 510, both in 2027-02. Should any of it be given a basis and counted as supported demand? (A2 also carries 100 ambition units and stays covered.)
Production lead (2)
5. A1. Confirmed production is 250, 200 and 200 units; 100 more is requested for 2027-01. Capacity is 300 a month, so the room left is 50, 0 and 100 units. If the request were confirmed, the largest likely shortfall would be 100 units in 2027-02. Can the 100 requested units for 2027-01 be confirmed, and can production in 2027-02 go above the 200 now confirmed, up to the stated 300?
6. A2. Confirmed production is 300, 300 and 200 units. With 900 on hand, the likely balance in 2027-02 is 800. Do the confirmed A2 runs stay as they are?
Purchasing lead (1)
7. C1. Confirmed supply is 100 units in 2026-12 and none after; 100 units from Supplier A are requested for 2027-01. Capacity leaves room of 0, 50 and 150 units. If the request were confirmed the likely balances would be 120, 140 and 80. Can the January request be confirmed, and is any supply to be requested for 2027-02? Earlier decision D07 covers the January request.
Finance lead (1)
8. A2. The likely balance in 2027-02 is 300 units over the allowance, worth $3,450 at unit cost. Is that stock acceptable to carry through the periods covered?

Carried from earlier reviews
D07, C1, Ask Supplier A for a firm January delivery, Purchasing lead, due 2026-11-27, open. The January supply for C1 is still marked requested (100 units), not confirmed. The due date is before the review date.
Decisions recorded as done: 1.

Check lines
Confirmed demand: opening 1,720 + confirmed supply 2,000 - confirmed demand 2,040 = 1,680, the sum of the closing balances.
Likely demand: opening 1,720 + confirmed supply 2,000 - likely demand 2,990 = 730, the sum of the closing balances.

Draft for the Operations lead. Nothing has been ordered, promised, sent or changed. Each function head decides their own response.
```

## What was observed

- **Every required part was produced.** Header, summary, gaps, inventory implications, not tested, decisions, carried decisions and both check lines. Both tie-outs held (1,680 and 730).
- **No stop condition applied.** The supply rows for A1 in 2027-01 share an item, period and source but differ in status ("confirmed" and "requested"), so the repeated-row check, which now uses item, period, source and status, did not stop the run. The first pass applied the older, narrower check and did not notice that these rows would have triggered it. No other stop path was exercised.
- **The figures matched the example.** Every balance, shortfall, capacity room, excess value and check line was the same.
- **The new rules were used.** The A1 balance of exactly 0 in 2027-01 was treated as not short. C1 in 2027-02 was treated as zero confirmed supply. The 40 moved units were counted in C1's ambition total of 490. The unconfirmed A1 request from Own production went to the production lead. The average monthly likely demand for A2 was 300 exactly, so the rounding rule was not needed. D07 was flagged as past its due date. Both items short if ambition is added got the sales decision the instructions now require.
- **Wording.** The run printed the source name as supplied ("Own production") and chose between the format's alternatives without printing a slash, as the instructions now say.
- **Facts not in the inputs.** None. The purchasing decision speaks of capacity, not supplier allocation, which is all the inputs support.

## What the first pass found, and what was done

The first pass found the faults and gaps below. Each was addressed in the template wording, and this pass used that wording.

- The example's repeated supply rows and the stop condition disagreed; the stop key is now item, period, source and status.
- The example called capacity a supplier allocation; the example now says capacity.
- The instruction block lacked an inventory implications step, a rule for confirmed supply with no source, a rule for supply with no demand or stock row, a rule for moved supported units, and the meanings of the three "short on" labels; these were added.
- Open ambiguities (a balance of exactly 0, a period with no supply row, moved units in the ambition total, who owns an own-production request, the capacity line for an item with no capacity rows, rounding the average) now each have a sentence in the procedure and the instruction block.
- Whether sales ambition always gets a sales decision, and whether an overdue earlier decision is flagged, are now stated.

## Shortcomings still met

1. The rounding rule and the capacity-line wording for an item with no capacity rows were written but not exercised: A2's average was whole, and every item in the gaps section has capacity rows. They are untested.
2. The instructions do not say how to write dollar amounts; this pass wrote whole dollars ($3,450). The first pass wrote $3,450.00. Either is faithful to the inputs.
3. The wording of each decision's question is still the assistant's own, so two runs will word them differently even where the same decisions are required.
4. The instruction block is still shorter than the procedure, and its step numbers differ from the procedure's.

Nothing in the run asked for a password or a login code, and nothing was sent, ordered or changed.

## Changes made after this run

After a further review, the instruction block gained rules for a blank unit cost, for returning the draft to the supply planning lead only, for the missing-capacity and missing-earlier-decisions wording, for which layers earn an inventory-implications line, and for writing money in whole dollars. The default of three months when no periods are given was removed, so missing periods now stop the run. The recorded output and observations above are unchanged and were not rerun; the changed rules do not alter any figure in this example. Shortcoming 2 above is closed by the whole-dollar rule; the others remain.
