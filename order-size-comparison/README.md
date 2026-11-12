# Order size comparison

When a supplier offers a bigger discounted order, the inventory planner gets each quantity costed the same way: yearly cost, cash tied up, months of cover and storage fit. The planner chooses the quantity; nothing is ordered.

*Workflow template · Supply chain and inventory · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/order-size-comparison/)*

## The outcome

A discount on a larger order is easy to like and hard to judge. The unit price falls, but the stock sits on the shelf longer, the money is gone from the bank sooner, and the warehouse may not have room. This workflow template puts every quantity the supplier offered side by side, costed the same way, so the choice rests on figures rather than on the size of the discount.

For each quantity the comparison shows what a year of that item would cost: the goods, the cost of placing and receiving each order including freight, and the cost of holding the stock. It shows the cash tied up the day the order arrives, how many months the order lasts, how long it would last if demand dropped, and whether it fits the storage you have. Against your standard order it shows the yearly saving, the extra cash that saving needs, and how high your holding cost would have to climb before the bigger order stopped paying.

Nothing is hidden in an average. Every line has its arithmetic written out, an item with a seasonal pattern is flagged, its flat-average figures are labelled as such, and the planner is asked for the expected months. Anything the figures do not price, such as a deadline on the discount, is listed beside them.

## Who starts the work, and when

The inventory planner or buyer starts it whenever a supplier puts forward a larger order, a new minimum quantity or a price break on an item the company expects to keep buying. It is run for one item from one supplier at a time; a supplier's offer on several items is several runs.

The planner reads the comparison and selects a quantity. Procurement approves the purchase, and whoever places orders places it. The workflow template prepares the comparison and does none of those steps.

## What they supply

- **The supplier's offer:** one row per quantity, with the unit price that applies to the whole order and the freight or delivery charge for it.
- **The demand history:** units sold or used for this item in each of the last twelve months.
- **Your cost figures:** your holding rate for a year as a percentage of the stock's value, and what it costs you to place and receive one order.
- **Your limits:** which option is your standard order, how many units you can store, the stock you expect to have when the order arrives, and a shelf life if the item has one.
- **Notes:** deadlines, conditions on the discount, a seasonal pattern, a change in demand you already expect.

The headers of the two exports are checked first. If one does not match, the work stops and asks which column is which.

## What comes out

One comparison in a fixed order: a header with your settings, the demand pattern, a summary, then a block for each quantity with its arithmetic written out, a list of conditions the figures do not price, and numbered questions for the planner. A section with nothing in it says "None."

The comparison states which options fit your storage and which has the lowest yearly cost. It does not say which to order. The planner chooses.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): the cost of holding stock set against the discount for buying more of it.
- [Procurement and suppliers](https://fullypowered.ai/functions/procurement-and-suppliers/): a supplier's volume offer judged on your own costs before you accept it.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): fast lines where a bulk price is tempting and shelf space is limited.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): components and materials bought in pallets, with storage and cash both constrained.
- [Consumer brands](https://fullypowered.ai/industries/consumer-brands/): brands weighing a larger production or purchase run against the cash it ties up.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when volumes have grown into the supplier's next price break and cash still matters.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when a standard order size set years ago has never been tested against the offers now available.

It answers a different question from [inventory reorder plan](https://fullypowered.ai/workflows/inventory-reorder-plan/), which decides when to reorder and how much against current stock and lead times. It also differs from [vendor quote comparison](https://fullypowered.ai/workflows/vendor-quote-comparison/), which chooses between suppliers; here the supplier is fixed and the quantity is the question. Stock that a large order leaves sitting is dealt with in [slow-moving stock and markdown plan](https://fullypowered.ai/workflows/slow-moving-stock-and-markdown-plan/).

## What has to change for your company

- **Your export headers,** set once so the check passes without a question.
- **Your holding rate,** which should include the cost of the money tied up, storage, insurance and the risk of the stock going out of date, as your finance lead sees it.
- **Your cost of placing and receiving one order,** in staff time and fees.
- **Your standard order,** your storage limit and any shelf life, per item or per product family.
- **Your demand-drop test and seasonal flags,** if a different test suits your range better.
- **Who selects the quantity and who approves the purchase,** and when a second approver is needed.
- **Your AI product.** It runs in ChatGPT, Claude, Copilot or Gemini from the exports and notes you supply. It needs no connection to your systems, places no orders and never asks for a password.

## What has been checked

Fully Powered AI wrote this workflow template in its own words. It was editorially reviewed on 10 November 2026, and every figure in its invented example was recomputed by hand. It was tried once on its invented example in Claude on 10 November 2026, and the record of that run is published with the template. It lists the edits made afterward, which have not been run again: the example's shelf-life setting now reads "not given", the example's closing lines were brought into line with the output format, the example now shows the lower-demand cover figure for every option and not only the standard one, and clarifications were added to the procedure and the output format (re-annualizing demand after a stock-out month, stock on hand at shelf-life end, when a listed deadline also needs a question, using the planner's expected months in the cover lines, what the Summary line counts and says when no storage limit is given, how the Ordering line is written when orders a year is not exact, the currency of the saving per 1,000 of extra cash, and the rounding of cost per unit). It has not yet been tested in a client environment, and it has not been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on two or three past supplier offers whose outcome you already know, plus cases written in advance with the expected behavior: a renamed column, an offer that does not fit the warehouse, a seasonal item, a short demand history, an item with a shelf life. The planner checks every figure against the offer and the exports before a quantity is selected. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/) builds that test set, and [What we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) shows the record.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete workflow template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the workflow template drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related workflow templates

- [Inventory reorder plan](https://fullypowered.ai/workflows/inventory-reorder-plan/)
- [Vendor quote comparison](https://fullypowered.ai/workflows/vendor-quote-comparison/)
- [Slow-moving stock and markdown plan](https://fullypowered.ai/workflows/slow-moving-stock-and-markdown-plan/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
