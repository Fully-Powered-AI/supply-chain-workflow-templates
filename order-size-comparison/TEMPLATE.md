# Order size comparison

Capability template, version 0.1.0.

## Purpose

Prepare one comparison of the quantities a supplier has offered for a single item: what a year of the item would cost at each quantity (goods, ordering and holding), the cash tied up when the order arrives, how many months it lasts and how long it would last if demand fell, whether it fits the storage limit and any shelf life, how it stands against the company's standard order, and the conditions the figures do not price. Every figure traces to an input, and the arithmetic is written out. The assistant prepares the comparison; the inventory planner selects the quantity, and it never places an order, contacts a supplier or changes a record.

## When to use it and when not to

Use it when a supplier offers a larger order, a different minimum quantity or a new price break on an item the company buys regularly and expects to keep buying.

Do not use it:

- to decide when to reorder or how much the stock needs next. That is a reorder plan, which works from current stock, lead times and open orders;
- to choose between suppliers or compare their quotes. Here the supplier is fixed and the quantity is the question;
- for an item with fewer than six months of demand history and no figure from the planner, or one-off buys such as a launch or a promotion;
- to set safety stock, forecast demand or decide what to do with surplus stock;
- to judge price terms that are not in the offer, such as rebates paid later or a commitment to buy a minimum amount over a year. These are listed as not priced and left to the people who agree them.

One run covers one item from one supplier. Several items are several runs, each with its own output.

## Roles

- **Runs it:** the inventory planner, the buyer or the operations lead.
- **Selects the quantity:** [your quantity decider], usually the inventory planner. The comparison never selects one.
- **Approves the purchase:** [your approver], usually procurement or the owner.
- **Places the order and records it in the company's system:** the person the company names, after approval. Always a person.

## Inputs

The assistant works only from the exports, settings and notes the person supplies. It needs no connection to any system or supplier site, and never asks for a password or a login code.

1. **The offer.** One row per quantity. Default column headers: `option`, `quantity`, `unit_price`, `freight_per_order`. `unit_price` is the price per unit that applies to every unit in that option, before tax. `freight_per_order` is the delivery and handling charge the supplier adds to that order, 0 if none. If the supplier's price is tiered, so that different units in one order carry different prices, the planner enters the blended price per unit for that quantity and says so in the notes.
2. **The demand history.** One row per month for this item, the twelve most recent full months. Default column headers: `month` (as YYYY-MM), `units_sold`. Use units sold or used, whichever the company plans on.
3. **The settings,** typed: the item and supplier, today's date, who selects the quantity, the currency, and these numbers.
   - Holding rate: the yearly cost of holding stock as a percentage of its value. [your holding rate]. No default; if it is missing, stop and ask.
   - Cost of placing and receiving one order, apart from freight: [your cost per order]. No default; if it is missing, stop and ask.
   - Standard option: the name of the offered row that is the company's usual order.
   - Stock expected on hand when an order arrives: units, 0 if none is expected.
   - Storage limit in units: [your storage limit], or "not given".
   - Shelf life in months: [your shelf life], or "not given".
   - Demand-drop test: [your demand-drop test], default 25%.
   - Seasonal flag: [your seasonal flag], default a month above 1.5 times or below 0.5 times the average month.
4. **Notes** (optional): deadlines on the discount, conditions attached to it, a known seasonal pattern, a change in demand the planner expects, a month the item was out of stock, a one-off order to leave out. If none are supplied, write "no notes supplied" in the header.

**Column check.** Before any arithmetic, compare each export's headers with the defaults, or with the company's own headers if [your column headers] are set. If a header is missing or named differently, stop. List the headers expected and the headers found, ask which column is which, and produce nothing else. Never guess a column.

## The procedure

1. **Check the inputs.** Run the column check. Confirm that the standard option is one of the offered rows, that every quantity is a whole number above zero, and that every unit price and freight figure is a number. A missing price or quantity, a repeated option name or a missing standard option: stop and ask.
2. **Read the demand.** Count the months supplied. With fewer than six, stop and ask for the planner's own monthly figure. With six to eleven, annual demand = units in the months supplied ÷ the number of months × 12, and the Demand line says the history is short. With twelve, annual demand = the twelve months added up. Average month = annual demand ÷ 12, shown to one decimal place. Take out any one-off order the notes name, and say so.
3. **Test the pattern.** Compare each month with the average month. If any month is above the seasonal flag's upper limit or below its lower limit, the item is SEASONAL: say which months. A flat average can mislead for a seasonal item, so show every figure as at average demand, label the Demand line SEASONAL, and ask the planner for the units expected in each month of the cover period. When the planner supplies them, replace the average month with the planner's figure in the cover lines and say so. Never apply the flat average silently. If a month is zero because the item was out of stock, and the notes say so, leave that month out of the average and count the months that remain. Annual demand is then the average of those months × 12, as in step 2's short-history rule; the twelve-month sum of step 2 is not used unchanged.
4. **Work out the yearly cost of each option.** For every offered option, with Q its quantity and D annual demand:
   - orders a year = D ÷ Q, shown to one decimal place;
   - goods = D × unit price;
   - ordering = orders a year × (cost of placing and receiving one order + freight per order);
   - holding = (Q ÷ 2) × unit price × holding rate. This assumes use at an even pace, so that on average half an order is on the shelf; safety stock is the same whatever the quantity and is left out;
   - yearly cost = goods + ordering + holding;
   - cost per unit = yearly cost ÷ D.
   Use the unrounded orders a year in the arithmetic. Where D ÷ Q is not exact at one decimal, write the Ordering line with D ÷ Q itself (for example (1,200 ÷ 700) × (...)) so that the line recomputes from the figures shown. Round each money line to the cent, half up, and add the rounded lines. Round cost per unit to the cent, half up.
5. **Work out cash and cover.** Cash tied up in goods on arrival = Q × unit price. Cover in months = Q ÷ the average month. Cover if demand falls = Q ÷ (the average month × (1 − demand-drop test)). Both to one decimal place, half up.
6. **Check the limits.** Storage: stock expected on hand when an order arrives + Q, against the storage limit. If it is above, the option DOES NOT FIT STORAGE, with the units over the limit; its figures are still worked out. If the limit is not given, write "storage limit not given". Shelf life, if given: if cover in months is longer than the shelf life, the option EXPIRES BEFORE USED, with the units expected to be left when the shelf life ends (Q − the average month × shelf life, rounded up) and their cost at the unit price. This count ignores stock expected on hand at arrival. If not given, write "not given".
7. **Measure each option against the standard.** For every option other than the standard: the difference in yearly cost (standard minus option; "lower" when positive, "higher" when negative); extra cash tied up on arrival = the option's cash − the standard's cash; saving per 1,000 of extra cash (in the setting's currency) = the difference in yearly cost ÷ the extra cash × 1,000, shown only when the option costs less a year and ties up more cash; and the break-even holding rate = ((standard goods + standard ordering) − (option goods + option ordering)) ÷ ((option's average stock value) − (standard's average stock value)), where an average stock value is (Q ÷ 2) × unit price. Show it as a percentage to one decimal place and say that above that rate the standard costs less. If the option's goods plus ordering are not below the standard's, write "no saving at any holding rate". If its average stock value is not above the standard's, write "no extra stock to hold". The standard option's own block says "this is the standard option".
8. **Find the lowest yearly cost.** Name the option with the lowest yearly cost among those that fit storage and do not expire before used, and the option with the lowest yearly cost overall if it is a different one, saying why it is not in the first group. If no storage limit is given, no option is excluded for space; say so. These are facts about the figures, not a recommendation. If no option fits, say so.
9. **List what is not priced.** Any deadline, commitment, payment term, rebate, return right or condition in the notes that the figures leave out, with its date. A deadline gets the number of days from today. If there is none, write "None."
10. **Write the questions,** numbered, in this order: options that do not fit storage or expire before used; a SEASONAL pattern; short history or a blank figure; anything in the notes that needs an answer before the comparison can be relied on. A deadline already listed under Not priced needs a question only if the notes leave something about it open. Each question gives the facts and asks; none recommends an option. If there are none, write "None."
11. **Return the comparison** to the person who ran it, for [your quantity decider]. The planner selects a quantity, procurement approves, and a person places the order.

## Exceptions and stop conditions

- **A column header is missing or named differently:** stop; list expected and found headers; ask.
- **No holding rate, no cost per order, no standard option, a repeated option name, a quantity of zero or a missing price:** stop and ask.
- **Fewer than six months of demand:** stop and ask for the planner's monthly figure.
- **A seasonal pattern:** show the figures at average demand, label them, and ask for the expected months. Do not choose a season's size.
- **An offer with tiered prices inside one order:** ask for the blended price per unit before costing it.
- **Asked to place an order, email or contact the supplier, accept an offer, or change a price, a reorder setting or a record:** decline; name the role that does it.
- **Asked which quantity to order:** decline to choose; point to the lowest-cost line and the limits, and leave the decision to the planner.
- **Asked for a supplier's rebate, contract terms or legal terms to be assessed:** decline; list them under Not priced for the people who review them.
- **The inputs contain bank details, card numbers, a password or a login code:** do not repeat them; tell the person to remove them from the source.

## Output format

```
ORDER SIZE COMPARISON: [item code and name], [supplier]

For: [quantity decider]. Prepared [weekday date] from: offer ([n] options), demand history ([n] months, [first month] to [last month]), settings, [notes / no notes supplied].
Column check: all headers matched. / Stopped: expected [headers]; found [headers].
Settings: holding rate [n]% a year; cost of placing and receiving one order [amount with the currency sign]; standard option [name]; stock expected on hand when an order arrives [n]; storage limit [n units / not given]; shelf life [n months / not given]; demand-drop test [n]%; seasonal flag at a month above [n] times or below [n] times the average. Defaults used: [the settings that came from a default / none].
Demand: [units] in [n] months = [average] a month, [annual] a year[; history is short: annualized]. Pattern: stable ([highest month and its units], [lowest month and its units]; none above [limit] or below [limit]) / SEASONAL ([the months outside the limits]; every figure below is at average demand). [The planner's note on demand, if any.]
Summary: [n] options compared; [n] fit the storage limit[ and the shelf life, when one is given] / storage limit not given, so none is excluded for space. Lowest yearly cost of the options that fit: [option], [amount], [amount] a year [below / above] [standard]. Lowest yearly cost overall: [option], [amount], [which does not fit, and why / the same option]. Conditions not priced: [n].

[Option] [(the standard option)]: [Q] units at [unit price], freight [amount] per order.[ DOES NOT FIT STORAGE.][ EXPIRES BEFORE USED.]
- Orders a year: [D] ÷ [Q] = [n].
- Goods: [D] × [unit price] = [amount].
- Ordering: [orders a year, or D ÷ Q where that is not exact at one decimal] × ([cost per order] + [freight]) = [amount].
- Holding: ([Q] ÷ 2) × [unit price] × [rate]% = [amount].
- Yearly cost: [amount] ([amount] a unit).
- Against the standard option: [amount] a year [lower / higher]. Extra cash tied up on arrival: [option cash] − [standard cash] = [amount]. Saving per [1,000 in the currency] of extra cash: [amount]. Break-even holding rate: [n]% ([working]); above that rate [standard] costs less. / this is the standard option.
- Cash tied up in goods on arrival: [Q] × [unit price] = [amount].
- Cover: [n] months; [n] months if demand is [n]% lower ([rate] a month).
- Storage: [on hand] + [Q] = [n] of [limit] units; fits, [n] units to spare / does not fit, [n] units over / storage limit not given.
- Shelf life: not given / [n] months; [fine / n units, [amount], left when it ends].
(one block per option, in the order of the offer)

Not priced
- [Condition, with its date and the days from today.]
/ None.

Questions for [quantity decider]
[n]. [The facts. The question.]
/ None.

Draft for [quantity decider]'s decision. The planner selects the quantity. Nothing has been ordered, sent or changed in any system.
```

## Reviewer checklist

1. Every export header matched, or the work stopped. (Planner)
2. The annual demand equals the months supplied, less only the one-off orders the notes name. (Planner)
3. Each option's goods, ordering, holding and yearly cost recompute from the offer and the settings, and the money lines add to the total. (Planner)
4. The standard option is measured against nothing, and every other option against it. (Planner)
5. Every option has a storage line and a shelf-life line, and an option that does not fit is marked. (Planner)
6. A seasonal item is labeled and a question asks for the expected months. (Planner)
7. Every condition in the notes appears under Not priced or in a question. (Approver)
8. No line recommends a quantity. (Approver)
9. The quantity is selected by the planner and the purchase approved before anyone places an order. (Approver)

## Acceptance tests

Proposed tests, none yet run as separate tests. Tests 1 to 4 use cases that also appear in the invented example.

1. **Three options, one too big.** Annual demand 1,200, holding rate 24%, cost per order $45.00, storage limit 800, 40 on hand on arrival. Options 300 at $8.40 with $60.00 freight, 600 at $8.00 with $90.00, 1,200 at $7.60 with $150.00. Expected: yearly costs $10,802.40, $10,446.00 and $10,409.40; the third marked DOES NOT FIT STORAGE, 440 over; the lowest cost among those that fit is the 600 option, $356.40 below the standard.
2. **Break-even.** The same case. Expected: break-even holding rates of 55.3% for the 600 option and 35.9% for the 1,200 option, each stating that the standard costs less above it.
3. **Renamed column.** The offer has `qty` instead of `quantity`. Expected: stops, lists expected and found headers, produces nothing else.
4. **Demand drop.** The same case. Expected: cover of 4.0, 8.0 and 16.0 months at 25% lower demand, from 75.0 a month.
5. **Seasonal item.** A month of 160 against an average of 100. Expected: labeled SEASONAL, figures marked as at average demand, a question asking for the expected monthly units.
6. **Short history.** Nine months of history. Expected: annualized, said on the Demand line. With four months, expected: stops and asks for the planner's monthly figure.
7. **Shelf life.** A shelf life of 6 months and an option covering 12 months at 100 a month. Expected: EXPIRES BEFORE USED, 600 units left, with their cost.
8. **No saving.** An option whose goods plus ordering are not below the standard's. Expected: "no saving at any holding rate" in place of a break-even rate.
9. **Missing holding rate.** Expected: stops and asks; no default is used.
10. **Asked to order.** "Place the 600 order with the supplier." Expected: declines; names the person who places approved orders.
11. **Asked which to choose.** "Which one should I buy?" Expected: declines to choose; points to the lowest-cost line, the limits and the questions.
12. **Tiered price.** The notes say the price falls after the 500th unit. Expected: asks for the blended price before costing it.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare an order size comparison for one item from one supplier,
using the exports, settings and notes the user supplies. You prepare;
people decide. You never place an order, accept an offer, contact a
supplier, or change a price, a reorder setting or any record. The
inventory planner selects the quantity and a person approves the
purchase before anything is ordered. You need no access to any system
and never ask for a password or a login code.

Inputs: the offer (option, quantity, unit_price, freight_per_order);
twelve months of demand (month as YYYY-MM, units_sold); settings (item,
supplier, today, who selects the quantity, currency, holding rate as a
yearly percentage, cost of placing and receiving one order, standard
option, stock expected on hand when an order arrives, storage limit,
shelf life, demand-drop test default 25%, seasonal flag default a month
above 1.5 times or below 0.5 times the average month); optional notes.
The Settings line gives every number (amounts with the currency sign)
and names, after "Defaults used", each one taken from a default, or
says none.

1. Column check: compare every header with the list above, or with the
   company's own headers if given. If any is missing or named
   differently, stop, list expected and found headers, ask, and produce
   nothing else. No holding rate, no cost per order, no standard option,
   a repeated option name, a zero quantity or a missing price: stop and
   ask. A tiered price inside one order: ask for the blended price per
   unit first.
2. Demand: fewer than six months, stop and ask for the planner's monthly
   figure. Six to eleven months: annual demand = units / months x 12,
   and say the history is short. Twelve: annual demand = the sum. Take
   out one-off orders the notes name. Average month = annual demand / 12,
   one decimal.
3. Pattern: if any month is outside the seasonal flag, label the item
   SEASONAL, name the months, show every figure as at average demand,
   and ask for the expected units in each month of the cover period.
   Never apply the flat average silently. If a month is zero because of
   a stock-out the notes name, leave it out of the average and take
   annual demand as the average of the remaining months x 12. If the
   user supplies expected units for each month, use them in place of
   the average month in the cover lines and say so.
4. For each option, with Q its quantity and D annual demand: orders a
   year = D / Q (one decimal; use the unrounded figure in the working);
   goods = D x unit price; ordering = orders a year x (cost per order +
   freight); holding = (Q / 2) x unit price x holding rate; yearly cost
   = goods + ordering + holding; cost per unit = yearly cost / D. Round
   each money line and the cost per unit to the cent, half up, and add
   the rounded money lines. Where D / Q is not exact at one decimal,
   write the Ordering line with D / Q itself so it recomputes.
5. Cash tied up on arrival = Q x unit price. Cover in months = Q /
   average month. Cover if demand falls = Q / (average month x (1 -
   demand-drop test)). One decimal, half up.
6. Storage: stock expected on arrival + Q against the limit; if above,
   mark DOES NOT FIT STORAGE with the units over, and still work out its
   figures; no limit given, say so. Shelf life: if cover is longer than
   the shelf life, mark EXPIRES BEFORE USED with the units left (Q -
   average month x shelf life, rounded up, ignoring stock on hand at
   arrival) and their cost.
7. Against the standard option, for every other option: the difference
   in yearly cost; extra cash tied up on arrival; saving per 1,000 of
   extra cash in the currency (only if it costs less and ties up more
   cash); and the break-even holding rate = ((standard goods + ordering) - (option
   goods + ordering)) / (option's (Q / 2) x price - standard's (Q / 2) x
   price), as a percentage to one decimal, saying that above that rate
   the standard costs less. If the option's goods plus ordering are not
   lower, write "no saving at any holding rate"; if its average stock
   value is not higher, "no extra stock to hold".
8. Name the lowest yearly cost among options that fit storage and do not
   expire before used, and the lowest overall if different, with the
   reason it is excluded. If no storage limit is given, exclude none
   for space and say so in the Summary line. State these as facts.
   Never say which quantity to order.
9. List under Not priced every deadline, commitment, payment term,
   rebate or condition in the notes that the figures leave out, with
   its date and the days from today.
10. Questions, numbered, in this order: options that do not fit or
    expire; a seasonal pattern; short history or blank figures; notes
    needing an answer. A deadline already under Not priced needs a
    question only if the notes leave something about it open. Each
    gives the facts and asks; none recommends.
    Write "None." for an empty section.
11. Use the output format exactly, one block per option in the order of
    the offer. End with the draft line that says nothing has been
    ordered, sent or changed.

If asked to place an order, email or contact the supplier, accept an
offer, or change a price, setting or record, decline and name the role
that does it. If asked which quantity to buy, decline to choose and
point to the lowest-cost line, the limits and the questions. If asked
to assess rebates, contract terms or legal terms, decline and list
them under Not priced for the people who review them. If the inputs
contain bank details, card numbers, a password or a login code, do not
repeat them; tell the user to remove them. Recompute every figure
before you return the comparison.
```

## What to customize

- [your column headers]: your own export headers, so the check passes without a question.
- [your holding rate]: the yearly cost of holding stock, as your finance lead sees it, including money tied up, storage, insurance and going out of date.
- [your cost per order]: the staff time and fees of placing and receiving one order.
- [your storage limit] and [your shelf life], per item or product family.
- [your demand-drop test] and [your seasonal flag], if a different test suits your range.
- [your quantity decider] and [your approver], and whether a purchase above a set amount needs a second approver.
- How freight and duties are entered in the offer export, so every option is costed on the same basis.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI from its own published map of the work. Editorially reviewed; the figures in the invented example were recomputed by hand. Tried once on its invented example in Claude on 10 November 2026; the record of that run is published with the template. Edits made afterward have not been run again: the example's shelf-life setting now reads "not given", the example's closing lines match the output format, the example shows the lower-demand cover figure for every option, and clarifications were added to steps 3, 4, 6, 7, 8 and 10, the output format and the instruction block (the planner's expected months in the cover lines, the Summary line and a missing storage limit, the Ordering line when orders a year is not exact, the currency of the saving per 1,000 of extra cash, the currency sign on settings amounts, and the rounding of cost per unit). Not yet tested in a client environment and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
