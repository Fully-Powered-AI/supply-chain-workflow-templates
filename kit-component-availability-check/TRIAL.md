# Kit component availability check: tried on its invented example

- **Product:** Claude, run in Claude Code
- **Model:** Claude Sonnet 5.5 (model ID claude-sonnet-5-5)
- **Date:** 2026-11-10

The inputs were the invented example in `public/example.md`: the settings, the kit definitions, the stock export, the second stock record and the listing export. No client data was used. This is the record of the second run of the day. The first run, on the earlier instructions, found seven gaps; they are listed below with what was done about each.

## How the run went, and one caveat

The model read the revised pasted instruction block and the output format, and followed them step by step on the example's inputs. The caveat: this run was not blind. The same model that revised the template made the run, and the example's published output was on screen. To make up for it, every figure was recomputed from the input files with a short script (available on hand less reserved, per location, on the stock export and on the lower of the two records, and the pooled figure on both sets), and the script agreed with the output below.

## What came out

KIT COMPONENT AVAILABILITY CHECK: the Shop, stock as of Tuesday 10 November 2026

- For: the stock lead and the inventory planner. Prepared Tuesday 10 November 2026 from: kit definitions (13 rows, 5 kits), stock export (11 rows, exported 10 November 2026), second stock record (11 rows, web shop platform, exported 10 November 2026), listing export (7 rows, exported 10 November 2026), settings.
- Column check: all headers matched.
- Basis: packing locations Main and Annex; stock at other locations ignored. Available is on hand less reserved; a component with no row for a location counts as 0 there. Each kit is built at one location from the parts held there. Incoming stock is not counted. Freshness: all files within 3 days.
- Settings: stale limit 3 days; approver the inventory planner. Defaults used: stale limit, parts from different locations.
- Summary: 5 kits defined. Sellable 1. Conflict 3. Zero 0. Unresolved 1. Component clashes between kits 2. Stock records in conflict 2. Listings to correct 2.

Record checks

- GFT-NEW: component TIN-9 has no row in the stock export. See question 1.
- GFT-OLD is in the listing export (Web shop, 3) and has no kit definition. See question 2.

Kit by kit

- GFT-NEW Winter tin set. Unresolved: TIN-9 has no row in the stock export. Sellable: cannot be stated. Listed: Web shop 5, total 5; not compared.
- GFT-HOME Home set. Conflict: the two stock records disagree on MUG-1 at Main. Sellable to rely on 8. By location: Main 8 (limit MUG-1), Annex 0 (limit MUG-1). On the stock export 10; on the lower of the two records 8. Listed: Web shop 8, total 8; matches.
- GFT-SPA Spa gift box. Conflict: the two stock records disagree on SOAP-1 at Main; the listing is above the figure to rely on and above the stock export's figure. Sellable to rely on 19. By location: Main 15 (limit SOAP-1), Annex 4 (limit CAND-1). On the stock export 21; on the lower of the two records 19. Pooled across locations 20; needs parts moved between locations. Listed: Web shop 25, total 25; over by 6.
- GFT-TEA Tea sampler. Conflict: the listing is above what can be built. Sellable to rely on 2. By location: Main 2 (limit TEA-B), Annex 0 (limit TEA-A, TEA-B and BOX-S, tied at 0). Listed: Web shop 12, Marketplace 6, total 18; over by 16.
- GFT-TEAP Tea duo. Sellable. Sellable to rely on 15. By location: Main 15 (limit TEA-A), Annex 0 (limit TEA-A and BOX-S, tied at 0). Listed: Web shop 15, total 15; matches.

Conflicting stock records

- SOAP-1 Lavender soap bar, Main: stock export 40 on hand, 6 reserved; second record 36. Lower figure used: 36, available 30. Affects GFT-SPA. Check: count the shelf at Main; the stock lead decides which record is right.
- MUG-1 Stoneware mug, Main: stock export 20 on hand, 0 reserved; second record 17. Lower figure used: 17, available 17. Affects GFT-HOME. Check: count the shelf at Main; the stock lead decides which record is right.

Components shared by kits

- CAND-1 Soy candle: available 24 (Main 20, Annex 4). GFT-SPA 19 × 1 = 19 and GFT-HOME 8 × 2 = 16 need 35; short by 11. Left out: GFT-NEW, unresolved, also uses it; the shortfall may be larger. The planner decides how the stock is shared.
- TEA-A Tea blend A: available 30 (Main 30, Annex 0). GFT-TEA 2 × 3 = 6 and GFT-TEAP 15 × 2 = 30 need 36; short by 6. The planner decides how the stock is shared.

Listings to correct

- GFT-SPA, Web shop: listed 25; sellable 19, the lower of two stock records. Reduce the total to no more than 19, or hold the listing. Approved: ______________ Date: ________
- GFT-TEA, Web shop 12 and Marketplace 6: listed 18; sellable 2. Reduce the total to no more than 2, or hold the listing. Approved: ______________ Date: ________

Questions for the stock lead

1. GFT-NEW Winter tin set: component TIN-9 has no row in the stock export, and the kit is listed on the Web shop at 5. Is the code wrong in the definition, or has the tin not yet been set up in the stock system?
2. GFT-OLD is listed on the Web shop at 3 and has no kit definition. Is it a retired kit whose listing was left up, or a live kit whose definition is missing?

Draft for the inventory planner's decision. Nothing has been changed in the stock system, the store or any listing, and no customer has been told anything. Quantities are worked out from the files supplied, as of 10 November 2026.

## What was observed

- **Every required part was produced:** the header, summary, record checks, kit by kit, conflicting records, shared components, listings to correct, questions and closing line. Nothing in the run made the template stop: all headers matched, no row failed the row checks, all files were dated 10 November, and the packing locations were given.
- **Difference from the example output:** none in any figure, status, ordering or question. The wording of the Tea sampler's Conflict reason differs from the earlier first run, as the revised step 9 asks. Given the caveat above, this agreement is weaker evidence than a blind run would give.
- **The three rules that decide printed figures were followed without a guess:** the Home set's limit at Main was named on the lower figures (MUG-1 alone, not a tie with CAND-1); the Spa gift box's pooled figure was taken on the lower figures (20, not 22) and compared with the 19 to rely on; the Home set's and Spa gift box's shared-component lines used the figure to rely on.
- **Facts not in the inputs:** none. Every number traces to a row in the inputs. The weekday (Tuesday) comes from the typed date in the settings.
- **Settings left out:** the stale limit and the parts-combining rule were not given, so the defaults applied and were named after "Defaults used", and the Basis line states the build rule.

## Gaps found by the first run, and what was changed

1. Which figures name the limiting component: the template now says the limit, the by-location figures and the pooled figure are taken on the figure to rely on, in the procedure and in the block.
2. Which total the pooled figure is compared with: now the sellable quantity to rely on.
3. Ties at 0: the template now says to name them where the location holds none of the parts, as the example prints.
4. Basis line when the setting is not given: now stated in the output format notes, the procedure and the block.
5. The pasted block left out rules the procedure had: the stale-second-record wording, one-record-only pairs, the stock export comparison, naming the lower of two records on a listing to correct, the questions to ask, "for reference only", and the shared-component `have` rule. The block's steps 3, 4, 6, 7, 8, 9, 10, 11 and 12 were brought into line.
6. A kit whose only fault is an over-listing is Conflict: step 9 now says so and why.
7. The kit order now appears in the procedure and the output format notes as well as the block. The label for the second figure now reads "on the lower of the two records".

## What was not tested

Only the success path with one conflict pattern was run. The stop conditions (renamed column, stale export, missing date, reservation larger than stock, request to change a listing) were not exercised. The acceptance tests in the template remain proposed and unrun.
