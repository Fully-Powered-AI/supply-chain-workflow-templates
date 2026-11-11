# Carrier performance review: trial on the invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5). It revised this template after review; it did not write the first version.
- **Date:** 2026-11-10

This is the second run. The first run, on the first version, was made the same day by a model that had not written the template. It found that the published example's Data checks line left out two items the format requires, that the example's settings gave no first and last ship date and no role that runs the review, and several places where the instructions left room to guess. After the first run, the example's settings were corrected, the Data checks line in the example was completed, and the template was changed as listed under "What changed since the first run". This record is of the second run, made on the revised version by the model that revised it, so it is not an independent run.

The inputs were the invented example in `public/example.md` (Larkfield Candle Works, Carrier A and Carrier B, October 2026, 14 shipments, 28 charge lines). No client data was used. The assistant followed the revised instruction block and output format in `member/template.md`. The figures were recomputed with a short script over the two exports as a cross-check, and the output below was written from them and compared line by line with the published example.

## What came out

```
CARRIER PERFORMANCE REVIEW: October 2026

For: Dana Ortiz, shipping lead; run by the logistics planner. Ship dates 2026-10-01 to 2026-10-31; deliveries and charges as supplied on 2026-11-04.

Data checks: 14 shipments in the period; 0 outside it, with 0 charge lines totalling 0.00 left out. Charge lines: 27 matched to a shipment, 1 unmatched (INV-B-2207, S199, 40.00). Shipments with no charge line: S114. No delivery date: S109. No promised date: S114. Delivered before shipped: none. No damage entry: none. No tracking entry: none. No weight: none.

Lane comparison

Warehouse to Phoenix (ground)
- Carrier A: 4 shipments. On time 2 of 4 (50.0%). Damaged 1 of 4 (25.0%). Tracking gaps 2 of 4 (50.0%). Charges 285.25 on 4 invoiced shipments: 71.31 per shipment, 1.90 per kg.
- Carrier B: 5 shipments. On time 3 of 4 (75.0%). Damaged 0 of 5 (0.0%). Tracking gaps 1 of 5 (20.0%). Charges 312.40 on 5 invoiced shipments: 62.48 per shipment, 1.64 per kg.
- Compared with the best on each measure: on time, Carrier B highest; Carrier A lower by 25.0 points. Damage, Carrier B lowest; Carrier A higher by 25.0 points. Tracking gaps, Carrier B lowest; Carrier A higher by 30.0 points. Cost per kg, Carrier B lowest; Carrier A higher by 0.26 (15.9% of the lower printed figure).

Warehouse to Seattle (ground)
- Carrier A: 5 shipments. On time 3 of 4 (75.0%). Damaged 1 of 5 (20.0%). Tracking gaps 0 of 5 (0.0%). Charges 364.55 on 4 invoiced shipments: 91.14 per shipment, 1.73 per kg.
- Compared: no comparison, one carrier on this lane and service.

Charges by type
- Warehouse to Phoenix (ground), Carrier A: freight 235.00, fuel 35.25, accessorial 15.00, other 0.00; total 285.25.
- Warehouse to Phoenix (ground), Carrier B: freight 284.00, fuel 28.40, accessorial 0.00, other 0.00; total 312.40.
- Warehouse to Seattle (ground), Carrier A: freight 317.00, fuel 47.55, accessorial 0.00, other 0.00; total 364.55.

Points to raise
- Warehouse to Phoenix (ground), Carrier A: Late: S102, promised 2026-10-09, delivered 2026-10-10, 1 day; S104, promised 2026-10-24, delivered 2026-10-27, 3 days. Damaged: S104. Tracking gaps: S102, S104. Accessorial charges: S104, 15.00.
- Warehouse to Phoenix (ground), Carrier B: Late: S108, promised 2026-10-26, delivered 2026-10-28, 2 days. Damaged: none. Tracking gaps: S109. Accessorial charges: none.
- Warehouse to Seattle (ground), Carrier A: Late: S112, promised 2026-10-23, delivered 2026-10-24, 1 day. Damaged: S113. Tracking gaps: none. Accessorial charges: none.

Decisions for Dana Ortiz (1)
1. Warehouse to Phoenix (ground): Carrier A is behind Carrier B on on-time delivery by 25.0 points, on damage by 25.0 points, on tracking gaps by 30.0 points and on cost per kg by 0.26 (15.9%); each difference is at or above its gap. Whether to raise these with Carrier A, or to change the carrier on this lane.

Not supplied or not checked: no agreed rates, so the charges are not checked against them. No earlier period, so there is no trend. Damage and tracking gaps are as flagged in the export; no claim records were supplied.

Every figure traces to the shipment export for ship dates 2026-10-01 to 2026-10-31 and the charge export supplied on 2026-11-04. The review changes no records, contacts no carrier and sends nothing.
```

## What changed since the first run

- The example's settings now give the first and last ship date (2026-10-01 to 2026-10-31) and the role that runs the review (the logistics planner). The format now prints the role on the "For" line.
- The example's Data checks line now has "Delivered before shipped: none" and "No weight: none".
- The Data checks line has a slot for charge lines left out because their shipment is outside the period, and the instruction block counts them there with their amount.
- Rounding is stated once: amounts are added up exactly and printed to two decimal places, and every difference and percentage is worked from the printed figures.
- The weight rule in the cost step now says that a shipment with a blank weight keeps its charges in the total and in cost per shipment, and is left out of cost per kg on both sides.
- The Compared line now names the best carrier on each measure and gives one clause for each other carrier, and the percentage wording is "of the lower printed figure" in both the format and the procedure.
- Decisions are printed as a count followed by numbered lines.

## What was observed

- Every part of the output format was produced, and nothing in the instructions told the assistant to stop. The inputs had no unreadable value, repeated shipment, unknown charge type or carrier mismatch.
- The output is the same as the published example. Every figure was recomputed from the exports and matches.
- Every fact in the output is in the inputs or follows from them. The example's "How the figures were reached" section matches the figures this run reached.
- The percentage is worked from the printed figures, 0.26 over 1.64, which is 15.9%, as the template now says. Worked from the unrounded figures it would be 15.7%, so the rule about printed figures decides the answer here.
- Where the template still leaves room to guess:
  - It is not stated whether a group's shipment count in the lane line (for example "5 shipments") includes shipments left out of on time or cost. This run counted all shipments in the group, as the example does. (Added after this run, without re-running it: the template now states that the count is every shipment of the group in the period. Also added after this run: a blank weight is not a stop, and the instruction block now carries the standing lines, the "None." rule, and the no-charge-export, "no comparison" and blank damage or tracking entry rules, and says to recommend nothing. None of these changes alters the example's inputs or its output.)
- Not exercised by this example: grace days other than zero, credits, delivered-before-shipped, a blank weight, shipments outside the period, two services on one lane, three carriers on one lane, a group below the fewest shipments, and any request to rank or contact a carrier. The rules for these were rewritten but have not been run.
