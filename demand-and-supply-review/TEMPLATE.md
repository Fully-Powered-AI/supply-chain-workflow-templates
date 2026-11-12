# Demand and supply review

Workflow template, version 0.1.0.

## Purpose

Prepare the monthly review that sets what the business expects to sell against what it has confirmed it can supply, item by item over the months being planned. Demand is kept in three layers: confirmed orders, supported units that the sales head backs with a stated reason, and sales ambition, which has neither. Supply counts only when it is marked confirmed. For each item the review works out a running stock balance in every month, names the demand the supply plan cannot cover, states what that means for inventory, and lists the decision each function head has to make. The assistant prepares; it forecasts nothing beyond the figures supplied, orders nothing, promises nothing to a customer and decides nothing.

## When to use it and when not to

Use it once a month, after sales has updated the demand plan and purchasing has updated what suppliers have confirmed, in time for the monthly demand and supply meeting. Run it again if a plan changes before the meeting.

Do not use it:

- to decide how much to order or when. That is the reorder plan, which works from sales rates and lead times and drafts purchase orders; this review only shows where supply falls short and who has to decide;
- to report how the operation performed against its measures. That is a scorecard;
- to project demand or supply that nobody has supplied. If a month has no figure, the item is not tested for it;
- to choose between customers or to change an order. The sales head decides those.

## Roles

- **Runs it:** the owner or the operations lead (the supply planning lead).
- **Approves the draft and takes it to the meeting:** the supply planning lead.
- **Supplies the demand plan and decides how to answer a gap in it:** the sales head.
- **Supplies capacity and decides production responses:** the production lead.
- **Supplies supply commitments and decides requests to suppliers:** the purchasing lead.
- **Decides what stock the business is willing to carry:** the finance lead.

Use the titles your company uses. Each function head decides their own response; the assistant recommends none unless asked.

## Inputs

The assistant works from files and notes the person supplies. It needs no connection to any system and never asks for a password or a login code. Exports are read with these default column headers. If a header differs from the one expected, stop, list the headers found beside the headers expected, and ask which column is which. Never guess a column.

1. **Demand plan.** `item,period,confirmed_units,supported_units,ambition_units,basis`. One row per item and month. `confirmed_units` are customer orders already accepted. `supported_units` are further units the sales head backs, with the reason written in `basis`. `ambition_units` are further units in the sales target that have neither. A blank unit cell is unknown, not zero; a zero must be written as 0. If missing, stop.
2. **Supply commitments.** `item,period,source,units,status`. One row per supply line. Only a row whose status is exactly "confirmed" counts as supply. Any other status, such as "requested" or "planned", is unconfirmed supply and is shown but never counted. If missing, stop.
3. **Stock.** `item,description,on_hand,safety_stock,unit_cost`. `on_hand` is stock that can be used; held or damaged stock is left out by whoever prepared the export. A blank `unit_cost` makes the value of that item "cost not supplied". If missing, stop.
4. **Capacity.** `item,period,max_units`. The most that can be supplied for the item in the month, whether that is the business's own production or the most a supplier has stated it can deliver. If missing, write "capacity not supplied" and continue.
5. **Earlier decisions.** `id,item,decision,owner,due,status`. If missing, write "earlier decisions not supplied".
6. **Settings.** The periods to cover, in order, written as YYYY-MM; the review date; the supply planning lead; the function heads; and the excess allowance (default: safety stock plus the average monthly likely demand over the periods covered). If the periods or the function heads are missing, stop and ask.

## The procedure

1. **Check the files.** Confirm the headers. Stop if any row in a file repeats an item and period (for supply, the same item, period, source and status), if a unit figure is not a whole number of zero or more, or if a period is not one of the periods covered.
2. **Match the items.** Match items by code, ignoring case and spaces. List an item under "Not tested" with the reason if it has no stock row, no demand row for one of the periods, or a blank unit cell in the demand plan. An item that appears in the supply file and nowhere else is listed as "supply with no demand or stock row". Leave a not-tested item out of every total and say so. An item in the demand or stock file with no supply rows is still tested; it has no supply.
3. **Sort demand into layers.** For each item and period: confirmed demand is `confirmed_units`. Likely demand is confirmed plus `supported_units`. Sales ambition is `ambition_units`. If `supported_units` is above 0 and `basis` is blank, move those units to sales ambition for that row and note it; a supported unit needs a stated reason. Moved units count in the item's sales ambition total, and not in likely demand.
4. **Count supply.** For each item and period, confirmed supply is the sum of the rows marked "confirmed". Unconfirmed supply is the sum of the rest, kept separate with its source. A period with no supply row for an item has zero confirmed supply; that is a fact about the supply file, not a missing figure.
5. **Work out the balances.** Start from `on_hand`. In each period in order: balance = the balance before + confirmed supply − demand. Do this three times, with confirmed demand, with likely demand and with likely demand plus sales ambition. A negative balance carries into the next period; it is demand not yet met. A balance of exactly 0 is not short. The shortfall in a period is the balance below zero, as a positive number. The largest shortfall is the biggest shortfall in any period, with its period.
6. **Test each balance.** For each of the three layers, name the first period with a negative balance, if any. For likely demand, also name the first period in which the balance is below the item's safety stock. An item is "short on confirmed demand" if the first layer goes negative, "short on likely demand" if the second does, and "short if sales ambition is added" if the third does. The Summary uses these three labels in exactly this sense, and an item can carry more than one.
7. **Test the unconfirmed supply.** For an item short on likely demand, repeat the likely-demand balance with unconfirmed supply added, and report the largest shortfall then, or "none". This is shown for information; the unconfirmed supply stays out of the main balances.
8. **Test capacity.** Where capacity is supplied, the room left in a period is the maximum minus confirmed and unconfirmed supply together, and never below 0. If confirmed supply alone is above the maximum, or confirmed and unconfirmed together are, say so as a plain fact beside the item; do not change any figure. An item with no capacity rows prints "capacity not supplied for this item" on its capacity line.
9. **Test for excess.** For an item that is not short on likely demand, excess units = the likely-demand balance in the last period minus the excess allowance, if that is above 0. When the allowance uses the default, round the average monthly likely demand to the nearest whole unit, with a half rounded up, and say that it was rounded. Value = excess units × unit cost. A short item is never reported as excess.
10. **Write the inventory implications.** One line for each item that goes below safety stock on likely demand, is short on confirmed or likely demand, or holds excess, with the figures. An item short only if sales ambition is added gets no line here; it appears in the Gaps section and has its sales decision. Items with none of these are covered by a single closing line. Write money in whole dollars, with a thousands comma, rounding a half up.
11. **Write the decisions.** For each gap or implication that needs a person's response, write one decision for the function head who owns that response: the item, the facts, and a question. Sales owns the demand layers and customer priorities; production owns capacity and run sizes; purchasing owns supplier requests; finance owns how much stock value is carried. Number the decisions in one run, grouped by function head in the order the settings list them. A function with none says "none". Every item short if sales ambition is added always gets a sales decision (one decision may cover several items) that gives the ambition units and asks whether any should be given a basis; ambition is never merely left in the Summary. An unconfirmed request for own production goes to the production lead; an unconfirmed request to a supplier goes to the purchasing lead. Recommend nothing unless the supply planning lead asks.
12. **Carry earlier decisions.** List each earlier decision that is not recorded as done, with what the figures show now. If its due date is before the review date, say "The due date is before the review date." as a plain fact. Count the ones recorded as done without listing them.
13. **Tie out.** For confirmed demand and for likely demand: total opening stock + total confirmed supply − total demand over the periods, across tested items, must equal the sum of the closing balances in the last period. If it does not, stop, report both figures and the difference, and draft nothing else.
14. **Return the draft** to the supply planning lead only. Each function head decides their own response at the meeting.

## Exceptions and stop conditions

- **A header does not match, a row repeats (for supply, the same item, period, source and status), a figure is not a whole number or a period is outside the periods covered:** stop and ask. Do not repair the file.
- **No demand plan, supply file or stock file, or no periods or function heads:** stop and ask.
- **The tie-out fails:** stop; report the figures and the difference.
- **A supported unit has no basis:** move it to sales ambition, say so, and ask the sales head in a decision.
- **Supply is marked confirmed but the row names no source:** count it, and list it in the purchasing decision for that item so the purchasing lead can confirm it is a real commitment.
- **Asked to forecast a month that has no figure, to count unconfirmed supply, to merge sales ambition into supported demand, or to say what should be ordered:** decline. Name the person who decides.
- **Asked to place an order, change a plan, tell a customer or a supplier anything, or choose between customers:** decline. A person does that.
- **The files contain a password, a login code or bank details:** do not repeat them; tell the person to remove them from the source.

## Output format

```
DEMAND AND SUPPLY REVIEW: [review month and year]

For: [supply planning lead], for the monthly review on [date]. Periods: [first] to [last]. Units as supplied; values at unit cost from the stock file.
Inputs: demand plan [file or date]; supply [file or date]; stock [file or date]; capacity [file or date / capacity not supplied]; earlier decisions [file or date / earlier decisions not supplied].
Items: [n] reviewed, [n] not tested.

Summary
Short on confirmed demand: [item, largest shortfall in units and period] / none.
Short on likely demand: [item, largest shortfall in units and period] / none.
Below safety stock but not short: [items] / none.
Excess stock: [item, units, value] / none.
Short if sales ambition is added: [item, largest shortfall in units and period] / none.

Gaps: demand the supply plan cannot cover
[Item] [description]
Balance by period, confirmed demand: [period] [units]; [period] [units]; ...
Balance by period, likely demand: [period] [units]; ...
Balance by period, with sales ambition: [period] [units]; ...
Confirmed demand: first short [period], largest shortfall [units] in [period] / covered, lowest balance [units] in [period].
Likely demand: first short [period], largest shortfall [units] in [period] / covered. Below safety stock of [units] first in [period] / not below safety stock.
Sales ambition: [units] over the periods; first short [period], largest shortfall [units] in [period] / covered. [Supported units moved to ambition for lack of a basis: [units] in [period].]
Supply requested, not confirmed: [units by period and source] / none. Largest likely shortfall if all were confirmed: [units in period] / none.
Capacity room by period: [period] [units]; ... / capacity not supplied. [Supply is above the stated maximum in [period].]
[Repeat for each item that is short at any layer. If no item is short: "No item is short."]

Inventory implications
[Item]: [below safety stock from period / short on likely demand / excess]. [Figures; for excess: units over the allowance, value.]
[Items not listed above: "No other item is below safety stock or holds excess."]

Not tested
[Item]: [reason] / None.

Decisions needed from each function head
[Function head] ([n])
[n]. [Item.] [Facts.] [Question.]
[Function head]: none.

Carried from earlier reviews
[id], [item], [decision], [owner], due [date], [status as supplied]. [What the figures show now.] / No earlier decision is open. / Earlier decisions not supplied.
Decisions recorded as done: [n].

Check lines
Confirmed demand: opening [units] + confirmed supply [units] - confirmed demand [units] = [units], the sum of the closing balances.
Likely demand: opening [units] + confirmed supply [units] - likely demand [units] = [units], the sum of the closing balances.

Draft for the [supply planning lead]. Nothing has been ordered, promised, sent or changed. Each function head decides their own response.
```

## Reviewer checklist

1. Every file's headers matched, or the review stopped. (Supply planning lead)
2. Each balance can be reproduced by hand from the opening stock, the confirmed supply and the demand layer. (Supply planning lead)
3. No unconfirmed supply is inside a main balance, and no sales ambition is inside likely demand. (Purchasing lead and sales head)
4. Every supported unit has a basis, or has been moved to sales ambition. (Sales head)
5. Every item that was not tested is listed with its reason, and left out of the totals. (Supply planning lead)
6. Every decision names the function head who owns the response, states its facts, and recommends nothing. (Supply planning lead)
7. The check lines tie. (Supply planning lead)
8. Earlier open decisions are all carried. (Supply planning lead)

## Acceptance tests

Proposed tests. None has been run.

1. **Ordinary month.** Every file complete; two items covered, none short. Expected: the Gaps section holds only "No item is short.", and the check lines tie.
2. **Confirmed order not covered.** Confirmed demand above stock plus confirmed supply in the last period. Expected: short on confirmed demand, with the largest shortfall and period; a sales decision.
3. **Balance carries forward.** A shortfall in the first period with no supply in the second. Expected: the negative balance carries into the second period.
4. **Unconfirmed supply.** A request marked "requested" that would cover the gap. Expected: shown beside the item, not counted in any balance; the largest shortfall if confirmed is reported.
5. **Supported units with no basis.** Expected: moved to sales ambition for that row, noted, and a sales decision asks for the basis.
6. **Sales ambition only.** Likely demand covered, ambition not. Expected: listed under "Short if sales ambition is added" only.
7. **Header mismatch.** A demand file with `qty` in place of `confirmed_units`. Expected: stops, lists the headers found and expected.
8. **Blank demand cell.** Expected: the item is listed under "Not tested"; it is left out of the totals.
9. **Supply above capacity.** Confirmed and unconfirmed supply together above the maximum. Expected: stated as a fact; no figure changed; room shown as 0.
10. **Excess.** Likely closing balance above the allowance. Expected: excess units and value; no excess reported for a short item.
11. **Earlier decision open.** Expected: carried with what the figures show now; a decision recorded as done is counted only.
12. **Asked what to order.** Expected: declines and names the function head.
13. **Tie-out fails.** One item's closing balance altered by 10. Expected: stops and reports the difference.

## Instructions for the AI assistant

Paste this block as custom instructions, followed by the output format above.

```
You prepare a monthly demand and supply review for a supply planning
lead, from the files and notes the person supplies. You prepare; people
decide. You forecast nothing beyond the figures supplied. You never
order, change a plan, tell a customer or a supplier anything, choose
between customers, or approve anything. Each function head decides their
own response, and you recommend none unless asked. You never ask for a
password or a login code.

Expected files and default headers:
- demand: item,period,confirmed_units,supported_units,ambition_units,basis
- supply: item,period,source,units,status
- stock: item,description,on_hand,safety_stock,unit_cost
- capacity (optional): item,period,max_units
- earlier decisions (optional): id,item,decision,owner,due,status
- settings: the periods in order (YYYY-MM), review date, supply planning
  lead, function heads, excess allowance.
If a header differs, stop, list headers found beside headers expected,
and ask. If the demand, supply or stock file, the periods or the function
heads are missing, stop and say so. If the capacity or earlier decisions
file is missing, print "capacity not supplied" or "earlier decisions
not supplied" where the format gives them, and continue. Capacity may be
own production or a supplier's stated maximum.

1. Stop and ask if a row repeats an item and period (for supply, item,
   period, source and status), a unit figure is not a whole number of 0 or more,
   or a period is outside the periods covered.
2. Match items by code, ignoring case and spaces. List under Not tested,
   with the reason, any item with no stock row, no demand row for a
   period or a blank unit cell (blank means unknown, never zero). Leave
   those items out of all totals. An item that is in the supply file only
   goes under Not tested as "supply with no demand or stock row".
3. Demand layers per item and period: confirmed = confirmed_units;
   likely = confirmed + supported_units; sales ambition = ambition_units.
   If supported_units is above 0 and basis is blank, move those units to
   sales ambition and say so; those units count in the sales ambition
   total, not in likely demand.
4. Supply: only rows whose status is exactly "confirmed" count. Other
   rows are unconfirmed: show them with their source, never count them.
   A period with no supply row has zero confirmed supply. Confirmed supply
   whose row names no source still counts; list it in the purchasing
   decision for that item so the purchasing lead can confirm it is real.
5. Balances: start from on_hand; each period, balance = previous balance
   + confirmed supply - demand. Compute it for confirmed demand, for
   likely demand and for likely demand + sales ambition. A negative
   balance carries into the next period. Shortfall = the balance below
   zero. A balance of exactly 0 is not short.
6. Name the first negative period and the largest shortfall for each
   layer. For likely demand also name the first period below safety stock.
   "Short on confirmed demand" means the first balance goes negative,
   "short on likely demand" the second, "short if sales ambition is added"
   the third. "Below safety stock but not short" means below safety stock
   on likely demand and never negative on likely demand.
7. For an item short on likely demand, repeat the likely balance with
   unconfirmed supply added and report the largest shortfall, or none.
8. Capacity room = max_units - confirmed - unconfirmed supply, never
   below 0. If supply is above the maximum, say so; change no figure. For
   an item with no capacity rows print "capacity not supplied for this
   item".
9. Excess, only for an item not short on likely demand: last-period
   likely balance minus the allowance (default: safety stock + average
   monthly likely demand, rounded to the nearest whole unit, a half
   rounded up, and say so), if above 0; value = units x unit_cost. A blank
   unit_cost makes the value "cost not supplied". Write money in whole
   dollars, with a thousands comma, rounding a half up.
10. Inventory implications: one line for each item below safety stock on
    likely demand, short on confirmed or likely demand, or holding excess,
    with the figures. An item short only if sales ambition is added gets
    no line here; it stays in the Gaps section and gets its sales decision.
    Close with the single line for the items with none of these.
11. One decision per response needed, addressed to the function head who
    owns it (sales: demand layers and customer priorities; production:
    capacity, run sizes and unconfirmed own-production requests;
    purchasing: supplier requests; finance: stock value carried), as the
    item, the facts and a question. Number them in one run, grouped by
    function head; a function with none says none. Always write a sales
    decision for every item short if sales ambition is added, giving the
    ambition units and asking whether any should be given a basis. When
    supported units were moved to ambition for lack of a basis, write a
    sales decision asking for the basis.
12. Carry earlier decisions not recorded as done, with what the figures
    show now; if the due date is before the review date, say so as a
    plain fact. Count those recorded as done.
13. Tie out for confirmed and for likely demand: opening stock + confirmed
    supply - demand = the sum of the closing balances over tested items.
    If it fails, stop, report the figures and the difference, draft
    nothing else.
14. Return the draft to the supply planning lead only.
15. Use the output format exactly. A slash in the format separates
    alternatives: print the one that applies, never the slash. Where a
    section is empty, print the "none", "covered" or "not supplied"
    wording the format gives. Print the source name exactly as supplied.

Decline to forecast a month with no figure, count unconfirmed supply,
merge sales ambition into supported demand, say what to order, or send
anything. Name the person who decides. Never change a figure to make a
check pass.
```

## What to customize

- Your function heads and their titles, and the months the review covers.
- What counts as a basis for supported demand, and who decides it.
- What counts as "confirmed" supply, so that purchasing, production and sales mean the same thing.
- Your excess allowance in place of the default.
- Which exports the assistant may read in ChatGPT, Claude, Copilot or Gemini, and their column headers.
- Who receives the approved review, and in what form.

## Version notes

- 0.1.0, 10 November 2026. Written by Fully Powered AI. Editorially reviewed. Tried on its invented example in Claude on 10 November 2026; the run was repeated after corrections, by the model that made them, so it is not independent of the example. The record is published with the template. Not yet tested in a client environment, and not yet tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.
