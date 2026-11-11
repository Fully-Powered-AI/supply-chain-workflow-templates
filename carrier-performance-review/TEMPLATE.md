# Carrier performance review

Capability template, version 0.1.0.

## Purpose

Compare carriers lane by lane from a period's shipment export and freight charges: on-time delivery, damage, tracking gaps and freight cost, each with the shipments behind it, set side by side only where the comparison is fair. The shipping lead uses it to decide whether to raise issues with a carrier or change carrier on a lane. The assistant prepares; it never grades a carrier beyond the data supplied, picks a carrier, contacts one, disputes a charge or changes a record.

## When to use it and when not to

Use it when the agreed carrier review is due, once the period's deliveries are recorded and the carriers' charges have been entered.

Do not use it to check an invoice against agreed rates (that needs the rates, which this capability does not read), to rate the suppliers of goods (see supplier performance scorecard), to work out a product's full landed cost (see product landed cost worksheet), or to write to a carrier. Do not use it when the shipment export is missing or the headers do not match.

## Roles

- **Runs it:** the logistics planner, shipping lead or an operations analyst.
- **Reviews and decides:** the shipping lead, who decides what to raise with a carrier and whether to change carrier on a lane.
- **Approves any commitment to a carrier:** procurement, as the company sets it.
- **Raises points with a carrier:** the person who owns that relationship, outside this capability.

## Inputs

1. **Settings.** Company, review period (label, first and last ship date), today's date, the role that runs the review, the decision-maker, currency, grace days (default 0), the fewest shipments worth comparing (default 5), and the gaps worth a decision (defaults: on time 10.0 points, damage 5.0 points, tracking gaps 10.0 points, cost per kg 10.0 percent). If a setting is missing, use its default and say so under Not supplied or not checked; if the period or today's date is missing, stop and ask. The role that runs the review has no default: if it is missing, write "not stated" for it and say so under Not supplied or not checked.
2. **Shipment export,** one row per shipment, with these headers exactly: `shipment_id, ship_date, carrier, lane, service, promised_date, delivered_date, weight_kg, damage, tracking_gap`. Dates are YYYY-MM-DD. `damage` and `tracking_gap` are yes, no or blank. A blank `delivered_date` means not delivered or not recorded; a blank `promised_date` means no promise on file. If a header is missing, renamed or in doubt, stop and ask which column is which; never guess.
3. **Freight charges export,** one row per charge, with these headers exactly: `invoice, shipment_id, carrier, charge_type, amount`. `charge_type` is freight, fuel, accessorial or other; any other value, stop and ask. `amount` is a number in the one currency; a negative amount is a credit.

Lane, service and carrier names are taken exactly as written. If two spellings look like the same name, ask before grouping them.

## The procedure

1. **Check the data before any arithmetic.** Stop and report if: a header does not match; a `shipment_id` appears twice; a date cannot be read; `weight_kg` is not a number and not blank; `amount` is not a number; a `charge_type` is not one of the four; a charge row's carrier differs from its shipment's carrier. List the rows and ask. A delivered date earlier than the ship date is not a stop: list the shipment under Data checks and leave it out of on time.
2. **Fix the period.** Shipments with a ship date outside the period are counted under Data checks and left out of everything else. Charge lines for a shipment outside the period are counted under Data checks, with their total amount, and left out.
3. **Form the groups.** A group is one carrier on one lane and one service. Compare carriers only within the same lane and the same service. Never add groups from different lanes or services into a carrier total, and never compare them. The shipment count printed for a group is every shipment of that group in the period, whether or not it is in the on-time or cost figures.
4. **Match charges to shipments** by `shipment_id`. A charge line whose shipment is not in the export is unmatched: list the invoice, shipment and amount, and leave it out of every figure. A shipment with no charge line is listed and left out of cost.
5. **On time.** A shipment counts when it has both a promised and a delivered date, and the delivered date is not before the ship date. It is on time when the delivered date is no later than the promised date plus the grace days; early is on time. A shipment with no delivered date, or no promised date, is not on time and not late: count it under Data checks and leave it out of the figure's denominator. Print on time as shipments on time out of shipments counted, and the percentage to one decimal place. A late shipment is listed with its promised date, delivered date and days late, counted in calendar days after the promised date, grace days included in the allowance and not subtracted from the days shown.
6. **Damage.** Shipments marked yes out of shipments with a yes or no entry. Blank entries are listed under Data checks and left out of the denominator.
7. **Tracking gaps.** The same, from `tracking_gap`. The assistant does not decide what a gap is; it counts the flag the export carries.
8. **Cost.** For each group: total charges (credits netted) on invoiced shipments; the count of invoiced shipments; cost per shipment (total over invoiced shipments); and cost per kg. For cost per kg, use only the invoiced shipments that have a weight: their charges over their weight. An invoiced shipment with a blank weight keeps its charges in the total and in cost per shipment, but its charges and its weight are both left out of cost per kg; list it under No weight, and write "per kg on [n] shipments with a weight" after the per kg amount. Add up the exact figures and round each printed amount to two decimal places; every difference and percentage in step 10 is worked from the printed figures, never from the unrounded ones. Also print the charges by type for each group, with a zero for a type with no charges.
9. **Small groups.** A group with fewer shipments than the fewest worth comparing is shown with its figures and counts and marked "too few to compare"; it has no entry in Compared and no decision.
10. **Compare within each lane and service.** Where two or more groups are large enough, name on each of four measures the group with the best printed figure, then print the difference between each other large-enough group and that best figure, from the printed figures: on time (higher is better, difference in points), damage (lower is better, in points), tracking gaps (lower is better, in points) and cost per kg (lower is better, the difference in amount and as a percentage of the lower printed figure, one decimal place). With three or more carriers on a lane and service, write one clause for each other carrier. Where a carrier's figure equals the best, write "level" for it; where two carriers share the best figure, name both. Cost per shipment is shown only for information: shipments of different weight are not like for like, so only cost per kg is compared. Where a lane and service has one carrier or only one large enough group, write "no comparison" and the reason. Never rank carriers, give a score, or total the measures into one.
11. **Points to raise.** Per group, in order of lane, then carrier: the late shipments, the damaged shipments, the shipments with a tracking gap, and any accessorial or other charges, each listed by shipment. Write "none" for an empty list.
12. **Decisions for the decision-maker.** Write a decision for a lane and service only when a comparison has at least one measure whose difference is at or above its gap. Give the facts, naming the carrier that is behind on each, then the question: whether to raise the points with that carrier, or to change the carrier on this lane. Where different measures point to different carriers, say so in the facts. One decision per lane and service. Recommend nothing.
13. **Say what was not checked,** and trace the figures. Return the review to the person who runs it only.

## Exceptions and stop conditions

- **A header does not match,** a shipment is repeated, a value cannot be read, or a charge's carrier differs from its shipment's: stop; list the rows; ask.
- **No charge export:** produce the delivery, damage and tracking comparison, leave cost as "not supplied" and say so; do not estimate charges.
- **Fewer than two carriers on every lane:** produce the figures per group and say that no comparison is possible.
- **Asked to rank the carriers, name the best, or recommend one:** decline; show the differences; the shipping lead decides.
- **Asked to check an invoice against agreed rates, dispute a charge, email a carrier, change a carrier setting or update a record:** decline; name the role that does it.
- **Asked to change a flag or a date so that a figure improves:** decline.

## Output format

```
CARRIER PERFORMANCE REVIEW: [period label]

For: [decision-maker]; run by [role that runs the review]. Ship dates [first] to [last]; deliveries and charges as supplied on [today].

Data checks: [n] shipments in the period; [n] outside it, with [n] charge lines totalling [amount] left out. Charge lines: [n] matched to a shipment, [n] unmatched ([invoice, shipment, amount]). Shipments with no charge line: [ids or none]. No delivery date: [ids or none]. No promised date: [ids or none]. Delivered before shipped: [ids or none]. No damage entry: [ids or none]. No tracking entry: [ids or none]. No weight: [ids or none].

Lane comparison

[Lane] ([service])
- [Carrier]: [n] shipments. On time [x] of [y] ([pct]%). Damaged [x] of [y] ([pct]%). Tracking gaps [x] of [y] ([pct]%). Charges [amount] on [n] invoiced shipments: [amount] per shipment, [amount] per kg[ on [n] shipments with a weight, only when a shipment has no weight].
- Compared with the best on each measure: on time, [best carrier] highest; [other carrier] lower by [points] points [one clause for each other carrier; or level]. Damage, [best carrier] lowest; [other carrier] higher by [points] points. Tracking gaps, [best carrier] lowest; [other carrier] higher by [points] points. Cost per kg, [best carrier] lowest; [other carrier] higher by [amount] ([pct]% of the lower printed figure). [Or: no comparison, [reason].] [Or: too few to compare: [carrier].]

Charges by type
- [Lane] ([service]), [carrier]: freight [amount], fuel [amount], accessorial [amount], other [amount]; total [amount].

Points to raise
- [Lane] ([service]), [carrier]: Late: [shipment, promised date, delivered date, days] or none. Damaged: [ids or none]. Tracking gaps: [ids or none]. Accessorial charges: [shipment, amount] or none.

Decisions for [decision-maker] ([n])
[Number]. [Lane (service)]: [the facts, naming the carrier that is behind on each measure]. Whether to raise these with [carrier], or to change the carrier on this lane.
[One numbered line for each decision. Or, with no decision: Decisions for [decision-maker]: None.]

Not supplied or not checked: [what was not supplied; settings taken from defaults; the standing lines below].

Every figure traces to the shipment export for ship dates [first] to [last] and the charge export supplied on [today]. The review changes no records, contacts no carrier and sends nothing.
```

Standing lines for Not supplied or not checked, used when they apply: "no agreed rates, so the charges are not checked against them"; "no earlier period, so there is no trend"; "damage and tracking gaps are as flagged in the export; no claim records were supplied". If a section has nothing to report, write "None." in its place.

## Reviewer checklist

1. Every percentage and amount matches the exports when recomputed. (Shipping lead)
2. Shipments with no delivery date or no promised date are counted under Data checks and are in no on-time figure. (Logistics planner)
3. Every comparison is within one lane and one service; no figure adds lanes together. (Shipping lead)
4. Every late, damaged and tracking-gap figure lists its shipments. (Logistics planner)
5. Unmatched charges and shipments with no charge are listed and left out of cost. (Logistics planner)
6. Each decision's trigger is met by the printed figures and its gap, and no carrier is ranked, scored or recommended. (Shipping lead)
7. The review states what was not supplied or not checked. (Shipping lead)

## Acceptance tests

Proposed tests. None has been run.

1. **Normal period.** Two carriers on one lane, one carrier on another, each at or above the fewest shipments. Expected: every section complete; the second lane says "no comparison"; figures recompute from the exports.
2. **Renamed column.** `promised_date` appears as `promise`. Expected: stops, names the header, asks which column it is; no figures.
3. **Two services on one lane.** Carrier A on ground and Carrier B on express over the same lane. Expected: two separate lane-and-service groups, no comparison between them.
4. **Missing delivery date.** A shipment with a blank `delivered_date`. Expected: listed under Data checks; not counted as on time or late; the denominator is one smaller.
5. **Delivered before shipped.** Expected: listed under Delivered before shipped; left out of on time.
6. **Unmatched charge.** A charge for a shipment not in the export. Expected: listed with its amount; in no total.
7. **Shipment with no charge.** Expected: listed; left out of cost per shipment and per kg.
8. **Small group.** A carrier with two shipments when the fewest is five. Expected: figures shown, marked too few to compare, no decision.
9. **Duplicate shipment.** The same `shipment_id` twice. Expected: stops and lists both rows.
10. **Credit.** A negative freight amount. Expected: netted in the total and in freight by type.
11. **Asked to rank the carriers and pick one.** Expected: declines; shows the differences.
12. **Asked to email a carrier or dispute a charge.** Expected: declines; names the role that does it.
13. **Blank weight.** An invoiced shipment with no `weight_kg`. Expected: listed under No weight; its charges stay in the total and per shipment, but it is in neither side of cost per kg, and the line says "per kg on [n] shipments with a weight".
14. **Three carriers on one lane and service.** Expected: the best carrier is named on each measure and each of the other two has its own clause; no ranking.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a carrier performance review for a shipping lead from a
shipment export and a freight charges export. You prepare; people
decide. You never grade a carrier beyond the data supplied, rank
carriers, name a best carrier overall or recommend one. You never send anything,
contact a carrier, dispute a charge, approve a commitment or change a
record or a setting. A person approves any such step. You never ask for
a password, a login code or any access to a system.

The user will supply: settings (company, period label with first and
last ship date, today's date, the role that runs the review, currency,
decision-maker, grace days, fewest shipments worth comparing, gaps
worth a decision; defaults: 0
grace days, 5 shipments, on time 10.0 points, damage 5.0 points,
tracking gaps 10.0 points, cost per kg 10.0 percent); a shipment export
with headers shipment_id, ship_date, carrier, lane, service,
promised_date, delivered_date, weight_kg, damage, tracking_gap; and a
charges export with headers invoice, shipment_id, carrier, charge_type,
amount. If the period or today's date is missing, or a header does not
match, stop and ask. Never guess a column. If the role that runs the
review is missing, write "not stated" for it and say so.

1. Check first. Stop and list the rows if a shipment_id repeats, a
   value cannot be read (a weight may be blank), a charge_type is not freight, fuel, accessorial
   or other, or a charge's carrier differs from its shipment's.
2. Leave out shipments shipped outside the period, and their charges,
   counting both, with the charges' total amount, under Data checks.
3. A group is one carrier on one lane and one service, names exactly as
   written. Compare only within a lane and service. Never add lanes or
   services together. A group's printed shipment count is every shipment
   of the group in the period, whether or not it is in the on-time or
   cost figures.
4. Match charges by shipment_id. List unmatched charges and shipments
   with no charge; leave both out of cost. With no charges export, print
   cost as "not supplied"; estimate nothing.
5. On time: delivered date not later than promised date plus grace days;
   early counts. A shipment with no delivered or no promised date, or
   delivered before shipped, is in no on-time figure; list it. List
   every late shipment with promised date, delivered date and days late.
6. Damage and tracking gaps: yes out of shipments with a yes or no
   entry. List blank entries under Data checks and leave them out of the
   denominator; list the damaged and tracking-gap shipments.
7. Cost: total charges with credits netted, per invoiced shipment and
   per kg. For per kg, use only invoiced shipments that have a weight:
   their charges over their weight; a shipment with no weight keeps its
   charges in the total and per shipment, is left out of per kg, and is
   listed under No weight. Add up exact figures, round each printed
   amount to two decimals, and work every later difference and
   percentage from the printed figures. Show charges by type.
8. Mark groups under the fewest shipments "too few to compare". Where
   two or more groups qualify, name the group with the best printed
   figure on each of on time, damage, tracking gaps and cost per kg, and
   print every other group's difference from it, from the printed
   figures; cost per kg is also shown as a percentage of the lower
   printed figure. Write level for an equal figure. Show cost per
   shipment but do not compare it. Never rank, score or total the
   measures. Where a lane and service has one carrier or only one group
   large enough, write "no comparison" and the reason.
9. Points to raise per group by shipment. Write a decision only where a
   difference reaches its gap; state the facts, then ask whether to
   raise them with that carrier or change carrier on that lane, one
   numbered line for each decision. Recommend nothing.
10. Use the output format exactly. Say what was not supplied or not
   checked, using these standing lines where they apply: "no agreed
   rates, so the charges are not checked against them"; "no earlier
   period, so there is no trend"; "damage and tracking gaps are as
   flagged in the export; no claim records were supplied". Where a
   section has nothing to report, write "None." in its place. End with
   the trace line.

If asked to rank carriers, check charges against agreed rates, email a
carrier, dispute a charge or alter a figure, flag or date, decline and
name the role that does it.
```

## What to customize

- Your export's column headers, and how lanes and services are named.
- Grace days, the fewest shipments worth comparing and the gaps worth a decision.
- What counts as a tracking gap, and where that flag comes from.
- The decision-maker, and who approves a change of carrier.
- Whether your charges include taxes or surcharges that should be a separate type.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI from its own published map of the work. Tried on its invented example in Claude on 10 November 2026; the record of that run is published with it. After the first run the example's settings gained the first and last ship date and the role that runs the review, its Data checks line gained the two items the format requires, and the template was tried again on that version. Not yet tested in a client environment.
