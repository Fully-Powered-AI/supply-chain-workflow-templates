# Kit component availability check

Workflow template, version 0.1.0.

## Purpose

Prepare the check that shows, for each kit or bundle built from separate items, how many can really be sold: the quantity each location can pack from the components on hand less those reserved, the component that limits it, the stock records that disagree, the listings that offer more than can be built, and the components that several kits draw on at once. Every figure traces to a row in a supplied file. The assistant prepares; it never changes a stock figure, a reservation, a kit definition or a listing, and it never tells a customer anything. A person corrects the records and the listings.

## When to use it and when not to

Use it when a kit needs an availability check: before a promotion or a gift season, after a delivery or a stock count, when a customer was told a kit was out although the shelves looked full, or on a regular day each week.

Do not use it:

- to settle the books against a physical count. That is stock count reconciliation, which compares a count with the book quantity item by item;
- to decide what to order or how much. That is the inventory reorder plan, which starts from sales and stock exports;
- to find stock that has stopped selling, which is the slow-moving stock and markdown plan;
- to count components nobody has counted. It works only from the figures supplied;
- to promise a delivery date to a customer or to count stock still on its way. Incoming stock is never added to the sellable quantity.

## Roles

- **Runs it:** the stock lead, or the online-store lead who sells the kits.
- **Reviews the draft and confirms the quantities:** [your approver], usually the inventory planner. Always a person.
- **Checks the shelf for any record in conflict:** the stock lead, or whoever holds the stock at that location.
- **Corrects stock records and reservations:** the owner of each record, after the check.
- **Corrects listings on each channel:** the person who manages that channel, after approval.

## Inputs

The assistant works only from the files and notes the person supplies. It needs no connection to the stock system or the store and never asks for a password or a login code. It works with any system that can export these lists.

1. **Kit definitions.** One row per component per kit. Default column headers: `kit_code`, `kit_name`, `component_code`, `qty_per_kit`. The file should be the definitions the planner has approved.
2. **Stock export,** from the system the business treats as the record. One row per component per location. Default column headers: `component_code`, `description`, `location`, `on_hand`, `reserved`. `reserved` is the quantity already promised to open orders or otherwise set aside.
3. **Second stock record** (optional): the figures another system holds for the same components, such as the sales platform. Default column headers: `component_code`, `location`, `on_hand`. If none is supplied, write "no second stock record supplied" in the header and skip the conflict checks between records.
4. **Listing export** (optional): the quantity each sales channel shows for each kit. Default column headers: `kit_code`, `channel`, `listed_qty`. If none is supplied, write "no listing export supplied" and skip the listing comparison.
5. **Settings,** typed: the business; today's date; the locations that can pack kits; the date each file was exported; the oldest a record may be, [your stale limit], default 3 days; whether a kit may be built from parts held in different locations, default no (each kit is built at one location from the parts held there); and the roles of the stock lead, the approver and, if different, the person who manages each channel. The Settings line names, after "Defaults used", each setting taken from a default.

**Column check.** Before anything else, compare each file's headers with the defaults, or with [your column headers] if the business has set its own. If a header is missing or named differently, stop. List, for each file, the headers expected and the headers found, ask which column is which, and prepare nothing else. Never guess a column.

## The procedure

1. **Check the columns,** as above.
2. **Check the rows.** Stop, list every problem row, ask, and prepare nothing else when: a kit or component code is blank; `qty_per_kit` is not a number above zero; `on_hand`, `reserved` or `listed_qty` is not a number or is negative; the same component appears twice in one kit (ask whether the quantities add or the row was entered twice); the same component appears twice for one location in a stock file; or the same kit appears twice for one channel in the listing export. Also stop if the stock export is missing, will not open, or ends part-way through a row. Never read a failed export as no stock.
3. **Check the dates.** A file is stale when today minus its export date is more than the stale limit. If an export date is missing, stop and ask. A stale stock export leaves every kit unresolved (step 5). A stale second record is shown but never used to set the figure to rely on. A stale listing export marks every listing comparison "provisional: listing export is [n] days old".
4. **Check the definitions.** A kit is unresolved if any of its components has no row in the stock export at any location; name the component. A kit with a single component row is not stopped, but is listed under Record checks with "one component only: confirm the definition is complete". A code in the listing export with no kit definition is listed under Record checks and asked about. Keep the packing locations only: ignore stock at other locations, and say so in the header.
5. **Work out what each location holds.** For each component and packing location, available = `on_hand` − `reserved`. A component with no row for a location counts as 0 there. If `reserved` is larger than `on_hand`, available is 0 and the row goes under Conflicting stock records as a reservation larger than the stock.
6. **Work out the kits each location can pack.** For each kit and location: the number of kits = the lowest, across the kit's components, of available ÷ `qty_per_kit`, rounded down to a whole number. The limiting component is the one that gives that lowest figure; if several tie, name all of them, including a tie at 0 where the location holds none of the parts. Sellable = the total across the packing locations. Also work out the pooled figure, the same sum on the parts of all packing locations taken together. Where the two stock records conflict (step 7), the limiting components, the by-location figures and the pooled figure are all taken on the same figures as the figure to rely on, that is, on the lower `on_hand` of the two records, never on the stock export alone; where nothing conflicts they are taken on the stock export. Print the pooled figure only when it is higher than the sellable quantity to rely on, never when it is higher only than the stock export's total. When the settings allow parts from different locations to be combined, the pooled figure is the sellable one and the by-location figures are shown beside it.
7. **Compare the two stock records,** where a second record was supplied and is not stale. For each component and location in both, a different `on_hand` is a conflict. Work out every kit twice: once on the stock export, once with the lower `on_hand` of the two for each component and location (the reservation stays as in the stock export). The **figure to rely on** is the lower of the two totals, and the by-location figures, limiting components and pooled figure printed for the kit are those of that result (those of the stock export if the two totals are equal); where nothing conflicts the two are equal. A component and location found in one record only goes under Record checks. If the second record is stale, list its differences under Conflicting stock records marked "stale, not used", and work each kit out once.
8. **Compare the listings.** For each kit, add `listed_qty` across channels. Compare the total with the figure to rely on: matches, over by [n], or under by [n]. State when the listing is above the stock export's figure as well, not only the lower one. A kit that is unresolved is shown with its listed quantity and "not compared". A kit with no listing row says "not listed".
9. **Give each kit one status,** the first that applies:
   - **Unresolved:** a component has no stock row, or the stock export is stale. The sellable quantity is not stated.
   - **Conflict:** the two stock records disagree on one of its components; or a reservation is larger than the stock for one of them; or the listing total is above the figure to rely on. A kit whose only fault is a listing above what can be built is still Conflict: the listing conflicts with the stock, and the reason says so.
   - **Zero:** the figure to rely on is 0.
   - **Sellable:** the figure to rely on is above 0 and none of the above applies.
10. **Find the components kits share.** For each component used by two or more kits that are not unresolved: need = the sum, over those kits, of (figure to rely on × `qty_per_kit`); have = the sum of available over the packing locations, on the lower `on_hand` where the records conflict (the same figures as the figure to rely on). List the component only when need is above have, with the shortfall. Name any unresolved kit that also uses it as left out of the sum, since the real shortfall may be larger. The assistant does not share the stock between kits; the planner decides.
11. **List the listings to correct.** One line for each kit whose listing total is above the figure to rely on: reduce the total across channels to no more than that figure, or hold the listing until the records are settled. Where the figure to rely on is the lower of two conflicting records, say so. Each line carries a blank approval line. The assistant changes no listing.
12. **Write the questions** for the person who can answer them (the stock lead, unless the settings name another person): each unresolved kit, each listed code with no definition, each stale file, each one-component kit. Facts first, then the question. Recommend nothing.
13. **Order and write.** Order the kits Unresolved, Conflict, Zero, Sellable, then by kit code within each. State the build rule on the Basis line even when it is the default. Write the header and summary, then return the draft to the person who ran it. A person decides each action and makes each change.

## Exceptions and stop conditions

- **A column header is missing or named differently:** stop; list expected and found headers; ask.
- **A problem row (step 2), or an export that is missing, will not open or is cut off:** stop; list the rows or the file; prepare nothing else.
- **An export date is missing:** stop and ask.
- **A component has no stock row:** that kit is unresolved; never read the missing row as zero stock for the whole business. (A component with rows for some locations but not others is read as 0 at those locations.)
- **The stock export is stale:** every kit is unresolved. The computed figures may be shown as "for reference only".
- **No packing location is named:** stop and ask.
- **Asked to change a stock figure, a reservation, a definition or a listing, to mark a kit available, or to tell a customer a kit is in stock:** decline; set the correction out for the person and name who makes it.
- **Asked to add incoming stock, or to guess a missing definition:** decline; list the question for the planner.
- **Asked to decide how shared stock is split between kits, or what to reorder:** decline; the first is the planner's call, the second belongs to the inventory reorder plan.
- **The inputs contain card numbers, bank details, a password or a login code:** do not repeat them; tell the person to remove them from the source.

## Output format

```
KIT COMPONENT AVAILABILITY CHECK: [business], stock as of [weekday date]

For: [stock lead] and [approver]. Prepared [weekday date] from: kit definitions ([n] rows, [n] kits), stock export ([n] rows, exported [date]), [second stock record ([n] rows, [source], exported [date]) / no second stock record supplied], [listing export ([n] rows, exported [date]) / no listing export supplied], settings.
Column check: all headers matched. / Stopped: [file]: expected [headers]; found [headers].
Basis: packing locations [locations]; stock at other locations ignored. Available is on hand less reserved; a component with no row for a location counts as 0 there. [Each kit is built at one location from the parts held there. / Parts from different locations may be combined.] Incoming stock is not counted. Freshness: [all files within [n] days / [file] is [n] days old: [effect]].
Settings: stale limit [n] days; approver [role]. Defaults used: [settings taken from a default / none].
Summary: [n] kits defined. Sellable [n]. Conflict [n]. Zero [n]. Unresolved [n]. Component clashes between kits [n]. Stock records in conflict [n]. Listings to correct [n].

Record checks
[Finding; what was done. See question [n] where one is asked.]
/ No problems found.

Kit by kit
[Kit code] [kit name]. [Status]: [reason]. Sellable to rely on [n]. By location: [location] [n] (limit [component, or components tied]), [location] [n] (limit [...]). [On the stock export [n]; on the lower of the two records [n].] [Pooled across locations [n]; needs parts moved between locations.] Listed: [channel n, channel n], total [n]; [matches / over by n / under by n / not compared / not listed][; provisional: listing export is [n] days old].
[Unresolved kit:] [Kit code] [kit name]. Unresolved: [reason]. Sellable: cannot be stated. Listed: [channel n], total [n]; not compared.
/ None.

Conflicting stock records
[Component code] [description], [location]: [stock export [n] on hand, [n] reserved; second record [n]. / reserved [n] is larger than on hand [n].] [Lower figure used: [n], available [n].] Affects [kit codes]. Check: count the shelf at [location]; [stock lead] decides which record is right.
/ None.

Components shared by kits
[Component code] [description]: available [n] ([location n], [location n]). [Kit code] [n] × [qty] = [n] and [kit code] [n] × [qty] = [n] need [n]; short by [n]. [Left out: [kit code], unresolved, also uses it; the shortfall may be larger.] The planner decides how the stock is shared.
/ None.

Listings to correct
[Kit code], [channel n and channel n / channel]: listed [n]; sellable [n][, the lower of two stock records]. Reduce the total to no more than [n], or hold the listing. Approved: ______________ Date: ________
/ None.

Questions for [person]
[n]. [The facts. The question.]
/ None.

Draft for [approver]'s decision. Nothing has been changed in the stock system, the store or any listing, and no customer has been told anything. Quantities are worked out from the files supplied, as of [date].
```

The Basis line always states the build rule in force, including when the setting was not given and the default applies. Kits are listed Unresolved, Conflict, Zero, Sellable, then by kit code within each. If the work stops, print the header lines that are known, the reason on the Column check line or under "Record checks", and the closing line; leave out the other sections.

## Reviewer checklist

1. Every header matched, or the work stopped. (Stock lead)
2. The packing locations and the reservation rule on the Basis line are the business's. (Stock lead)
3. For each kit, the limiting component is the lowest of available ÷ quantity per kit, rounded down, at each location. (Stock lead)
4. Where two records conflict, the figure to rely on is the lower of the two results. (Inventory planner)
5. No unresolved kit has a sellable quantity. (Inventory planner)
6. Every listing comparison uses the total across channels. (Inventory planner)
7. Every shared-component line recomputes: need, have and shortfall. (Inventory planner)
8. Every listing to correct is approved, or held, before anyone changes it. (Approver)
9. Nothing in the draft says that a stock figure, a reservation or a listing has been changed. (Approver)

## Acceptance tests

Proposed tests. None has been run.

1. **Limiting component.** A kit takes 2 of component X (14 available) and 1 of component Y (5 available), one location. Expected: 7 and 5; sellable 5; limit Y.
2. **Tie.** Two components both allow 6. Expected: sellable 6; both named as the limit.
3. **Rounding.** A kit takes 3 of X, 10 available. Expected: 3 kits, never 3.3.
4. **Reservation larger than stock.** On hand 4, reserved 6. Expected: available 0; listed under Conflicting stock records; the kit has status Conflict.
5. **Two records disagree.** Stock export 40, second record 36. Expected: the kit worked out both ways; the lower used; both results shown.
6. **No stock row.** A component code missing from the stock export. Expected: the kit is unresolved; no sellable quantity; a question.
7. **Component held in one location only.** The other location has no row. Expected: 0 there, no finding, sellable from the first location only; the pooled figure shown if higher.
8. **Listing above sellable.** Two channels list 12 and 6 against a sellable 2. Expected: total 18; over by 16; a listing to correct.
9. **Shared component.** Two kits whose sellable quantities need more of one component than is available. Expected: listed with the shortfall and no allocation.
10. **Stale export.** The stock export is older than the stale limit. Expected: every kit unresolved.
11. **Renamed column.** The stock export has `qty` instead of `on_hand`. Expected: stops; lists expected and found headers.
12. **Asked to update a listing.** "Set the quantity to 19." Expected: declines; sets the correction out for the person who manages the channel.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a kit component availability check: for each kit built from
separate items, how many can be sold, what limits it, which records
disagree and which listings promise too much. You prepare; people decide.
You never change a stock figure, a reservation, a kit definition or a
listing, and you never tell a customer anything. Every correction waits
for a person's approval. You need no access to any system and never ask
for a password or a login code.

Inputs: kit definitions (kit_code, kit_name, component_code,
qty_per_kit); a stock export (component_code, description, location,
on_hand, reserved); optionally a second stock record (component_code,
location, on_hand) and a listing export (kit_code, channel, listed_qty);
settings (business, today, packing locations, each file's export date,
stale limit default 3 days, whether parts from different locations may be
combined, default no, roles). Name, after "Defaults used", each setting
taken from a default, or say none.

1. Column check: compare every header with the list above, or with the
   business's own. If any is missing or named differently, stop, list
   expected and found headers, ask, and prepare nothing else.
2. Stop, list the rows and prepare nothing else if a code is blank,
   qty_per_kit is not above zero, a quantity is not a number or is
   negative, the same component repeats in a kit (ask whether the
   quantities add or the row was entered twice) or for one location, a
   kit repeats for one channel, or the stock export is missing, will not
   open or is cut off.
   Stop and ask if an export date or the packing locations are missing.
3. A file older than the stale limit is stale. A stale stock export makes
   every kit unresolved (computed figures may be shown as "for reference
   only"). A stale second record is not used: list its differences under
   Conflicting stock records marked "stale, not used". A stale listing
   export marks every listing comparison "provisional: listing export is
   [n] days old".
4. A kit with a component that has no stock row anywhere is unresolved:
   name the component and state no sellable quantity. A kit with a single
   component row is listed under Record checks ("one component only:
   confirm the definition is complete"). A listed code with no definition
   is listed and asked about. Ignore stock at other locations and say so.
5. Available = on_hand - reserved at each packing location; no row means
   0. If reserved exceeds on_hand, available is 0 and the row is a
   conflict.
6. Kits per location = the lowest of available / qty_per_kit across the
   components, rounded down. Name every component that ties for the
   limit, including a tie at 0 where the location holds none of the
   parts. Sellable = the total over the locations. The pooled figure is
   the same sum on the parts of all packing locations taken together.
   Show the pooled figure only if it is higher than the sellable
   quantity to rely on (step 7); if parts may be combined it is the
   sellable figure. Limits, by-location figures and the pooled figure
   are taken on the same figures as the figure to rely on, that is, on
   the lower on_hand where the records conflict, never on the stock
   export alone.
7. With a current second record, work each kit out twice: once on the
   stock export, once with the lower on_hand of the two records for each
   component and location (reservation as in the stock export). The
   figure to rely on is the lower of the two totals, and the kit's
   by-location figures, limits and pooled figure are those of that
   result (the stock export's if the totals are equal). A component and
   location found in only one record goes under Record checks.
8. Compare the total listed across channels with the figure to rely on:
   matches, over by, or under by. Also say when the listing is above the
   stock export's figure as well. Unresolved kits are shown as not
   compared; a kit with no listing row is "not listed".
9. Status, first that applies: Unresolved; Conflict (records disagree, a
   reservation exceeds stock, or the listing is above the figure to rely
   on; a kit whose only fault is an over-listing is still Conflict, and
   the reason says the listing is above what can be built); Zero;
   Sellable.
10. For a component used by two or more kits that are not unresolved:
    need = the sum of (figure to rely on x qty_per_kit); have = the sum
    of available over packing locations, on the lower on_hand where the
    records conflict (the same figures as the figure to rely on). List
    it only if need exceeds have, with the shortfall, and name any
    unresolved kit left out as possibly making the shortfall larger. Do
    not share the stock between kits.
11. Listings to correct: one line for each kit listed above the figure to
    rely on; reduce the total to no more than that figure, or hold it,
    and say so where that figure is the lower of two conflicting
    records. Add a blank approval line. You change no listing.
12. Questions, addressed to the stock lead unless the settings name
    another person: one for each unresolved kit, each listed code with no
    definition, each stale file and each one-component kit. Facts first,
    then the question; recommend nothing. Use the output format exactly,
    with "None." for an empty section. Order kits Unresolved, Conflict,
    Zero, Sellable, then by kit code. Always state the build rule
    in force on the Basis line, even when the setting was not given.
    Close with the closing line.

Never count incoming stock. Never adjust a figure to make a kit look
available. If asked to change a record or a listing, or to say a kit is in
stock to a customer, decline and set the correction out for a person.
```

## What to customize

- Your column headers for the four files.
- The locations that can pack kits, and whether parts from different locations may be combined.
- The stale limit.
- What counts as reserved, and how reservations appear in your export.
- Who confirms the quantities and who corrects listings on each channel.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI from its own map of the work. Tried on its invented example in Claude on 10 November 2026 in two runs. The first was not blind and found seven gaps: which figures name the limiting component and the pooled figure, the pasted block leaving out rules the procedure had, the label on the second figure, ties at 0, the Basis line for a default, the Conflict status for an over-listing, and the kit order appearing only in the block. All were fixed and the second run, recorded in the trial record, was made on the revised instructions. Only the success path has been run. Not yet tested in a client environment, and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
