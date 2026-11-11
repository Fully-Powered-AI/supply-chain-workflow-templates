# Order size comparison: trial on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example in `public/example.md` (its settings, offer, twelve months of demand and notes). No client data was used. The model did not write the template. It read the template and only the example's inputs, followed the fenced instruction block and the output format, and compared its result with the example's output afterwards.

## What came out

ORDER SIZE COMPARISON: BOT-500 Stainless water bottle 500 ml, Supplier A

- For: the inventory planner. Prepared Tuesday 10 November 2026 from: offer (3 options), demand history (12 months, 2025-11 to 2026-10), settings, notes.
- Column check: all headers matched.
- Settings: holding rate 24% a year; cost of placing and receiving one order 45.00; standard option Standard; stock expected on hand when an order arrives 40; storage limit 800 units; shelf life not given; demand-drop test 25%; seasonal flag at a month above 1.5 times or below 0.5 times the average. Defaults used: the demand-drop test and the seasonal flag.
- Demand: 1,200 units in 12 months = 100.0 a month, 1,200 a year. Pattern: stable (highest month 105, lowest 92; none above 150.0 or below 50.0). No change in demand expected (notes).
- Summary: 3 options compared; 2 fit the storage limit. Lowest yearly cost of the options that fit: Mid, $10,446.00, $356.40 below Standard. Lowest yearly cost overall: Pallet, $10,409.40, which does not fit (440 units over). Conditions not priced: 1.

Standard (the standard option): 300 units at $8.40, freight $60.00 per order.
- Orders a year: 1,200 ÷ 300 = 4.0.
- Goods: 1,200 × $8.40 = $10,080.00.
- Ordering: 4.0 × ($45.00 + $60.00) = $420.00.
- Holding: (300 ÷ 2) × $8.40 × 24% = $302.40.
- Yearly cost: $10,802.40 ($9.00 a unit).
- Against the standard option: this is the standard option.
- Cash tied up in goods on arrival: 300 × $8.40 = $2,520.00.
- Cover: 3.0 months; 4.0 months if demand is 25% lower (75.0 a month).
- Storage: 40 + 300 = 340 of 800 units; fits, 460 units to spare.
- Shelf life: not given.

Mid: 600 units at $8.00, freight $90.00 per order.
- Orders a year: 1,200 ÷ 600 = 2.0.
- Goods: 1,200 × $8.00 = $9,600.00.
- Ordering: 2.0 × ($45.00 + $90.00) = $270.00.
- Holding: (600 ÷ 2) × $8.00 × 24% = $576.00.
- Yearly cost: $10,446.00 ($8.71 a unit).
- Against the standard option: $356.40 a year lower. Extra cash tied up on arrival: $4,800.00 − $2,520.00 = $2,280.00. Saving per $1,000 of extra cash: $156.32. Break-even holding rate: 55.3% (($10,500.00 − $9,870.00) ÷ ($2,400.00 − $1,260.00)); above that rate Standard costs less.
- Cash tied up in goods on arrival: 600 × $8.00 = $4,800.00.
- Cover: 6.0 months; 8.0 months if demand is 25% lower (75.0 a month).
- Storage: 40 + 600 = 640 of 800 units; fits, 160 units to spare.
- Shelf life: not given.

Pallet: 1,200 units at $7.60, freight $150.00 per order. DOES NOT FIT STORAGE.
- Orders a year: 1,200 ÷ 1,200 = 1.0.
- Goods: 1,200 × $7.60 = $9,120.00.
- Ordering: 1.0 × ($45.00 + $150.00) = $195.00.
- Holding: (1,200 ÷ 2) × $7.60 × 24% = $1,094.40.
- Yearly cost: $10,409.40 ($8.67 a unit).
- Against the standard option: $393.00 a year lower. Extra cash tied up on arrival: $9,120.00 − $2,520.00 = $6,600.00. Saving per $1,000 of extra cash: $59.55. Break-even holding rate: 35.9% (($10,500.00 − $9,315.00) ÷ ($4,560.00 − $1,260.00)); above that rate Standard costs less.
- Cash tied up in goods on arrival: 1,200 × $7.60 = $9,120.00.
- Cover: 12.0 months; 16.0 months if demand is 25% lower (75.0 a month).
- Storage: 40 + 1,200 = 1,240 of 800 units; does not fit, 440 units over.
- Shelf life: not given.

Not priced
- The Pallet price holds only if the order is confirmed by Friday 20 November 2026 (notes), 10 days from today.

Questions for the inventory planner
1. Pallet needs room for 1,240 units against a limit of 800, 440 over. Is there space for the 440 units?

Draft for the inventory planner's decision. The planner selects the quantity. Nothing has been ordered, sent or changed in any system.

## What was observed

These observations describe the invented example as it stood at the time of the run. The example has since been edited: its shelf-life setting now reads "not given", its Not priced line and questions were cut back to what the notes support, its closing lines match the output format, and it shows the lower-demand cover figure for every option. The record of the output above is unchanged. The run also showed the cost per order as 45.00 with no currency sign, where the example shows $45.00; the output format now says amounts in the Settings line carry the currency sign.

- Every required part was produced: header lines, a block for each of the three options, Not priced, Questions and the closing line. Nothing in the template made the run stop.
- Every figure matched the example's output, including the yearly costs, per-unit costs, saving per $1,000, break-even rates, cover and storage lines. The figures also match the template's acceptance tests 1, 2 and 4.
- Differences from the published example, all in wording:
  - The example's Not priced line adds "The yearly cost above does not include any cost of finding space for it." That is not in the inputs and is not asked for by the template.
  - The example puts the "ten days from today" in a second question; this run put the days in the Not priced line, as step 9 says.
  - The example's first question also asks what overflow space would cost a month and says "Without it, Pallet cannot be selected". The cost question goes past the inputs, and the second half comes close to a verdict.
  - The example's second question asks whether the supplier attaches a commitment to the deadline. The notes do not say so. This run left it out, because step 10 asks only for notes that need an answer.
  - The example names the months of the highest reading (105 in November 2025 and March 2026) and the lowest month; this run gave the values only, as the format shows.
- Where the instructions were ambiguous and a guess was needed:
  - The settings said "Shelf life: none". The template's words are "not given". This run treated "none" as not given.
  - The demand-drop test and seasonal flag were absent from the settings, so the template's defaults were used and named on the "Defaults used" line. That worked as designed.
  - Step 10 includes "anything in the notes that needs an answer", but nothing says whether a dated deadline already listed under Not priced also needs a question. This run did not add one.
  - The format puts "Cover" with a rate in brackets for the lower-demand case, and the example shows it only for the standard option. This run gave it for all three.
- Nothing contradicted the inputs: no fact in this run's output was outside them. The example's output adds one small fact not in the inputs (the cost of finding space, and a possible commitment attached to the deadline).
- Shortcoming: the template is long and its arithmetic has many steps, so the run depended on careful recomputation. The template says to recompute, and the figures held.
- This was one run by one model on one invented example. It shows the template can be followed to the expected figures here. It does not show how the template behaves with real data, a seasonal item, a short history or a stop condition.
