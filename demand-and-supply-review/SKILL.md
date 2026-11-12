---
name: "demand-and-supply-review"
description: "Prepare the monthly review that sets what the business expects to sell against what it has confirmed it can supply, item by item over the months being planned. Demand is kept in three layers: confirmed orders, supported units that the sales head backs with a stated reason, and sales ambition, which has neither. Supply counts only when it is marked confirmed. For each item the review works out a running stock balance in every month, names the demand the supply plan cannot cover, states what that means for inventory, and lists the decision each function head has to make. The assistant prepares; it forecasts nothing beyond the figures supplied, orders nothing, promises nothing to a customer and decides nothing."
license: "MIT"
metadata:
  version: "0.1.0"
  publisher: "Fully Powered AI"
  template: "Demand and supply review"
---

# Demand and supply review

This is the technical file for a Fully Powered workflow template. It carries the instructions an AI product follows. The complete template, with roles, inputs, exceptions, the reviewer checklist, acceptance tests and what to customize, is in [TEMPLATE.md](TEMPLATE.md). A worked example with invented data is in [EXAMPLE.md](EXAMPLE.md).

## Instructions

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

## Before relying on it

Decide every item under "What to customize" in TEMPLATE.md and set the limits the instructions in this file leave open, written in square brackets such as [N], to your own. Then run the acceptance tests in TEMPLATE.md on past work. A person starts this work, supplies the inputs and decides what happens with the result.
