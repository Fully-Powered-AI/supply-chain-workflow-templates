# Supplier delivery date check

The purchasing or operations person gets one comparison from the open purchase orders and the supplier replies: promised and revised dates side by side, the orders each change puts at risk, and the follow-ups still unanswered. No supplier is contacted.

*Capability template · Supply chain and inventory · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/supplier-delivery-date-check/)*

## The outcome

A supplier says "a week later" on a call, a confirmation lands in someone's inbox, and three weeks on nobody can say which orders were promised for when. This capability puts every open purchase order line on one page: the date the supplier first promised, the latest date a supplier has actually confirmed, how many days it moved, and whether the line is already past due.

Each reply is graded by what it can support. A written confirmation or a recorded call fixes a date. An informal estimate is shown beside the line and never replaces the confirmed date. A reply with no date in it is shown as exactly that.

The comparison then follows each change to the orders that wait on the goods, whether customer orders or production orders. It adds your receiving days to the arrival date and sets the result against each order's ship-by date, so you see which orders are late, which are not late yet but rest on a date nobody has confirmed, and how many days are spare.

Last, it lists the questions suppliers have not answered and the lines that need a follow-up but have none. You decide whom to chase and what to tell customers; the page gives you the facts to do it with.

## Who starts the work, and when

A buyer, a purchasing coordinator or an operations lead runs it when a supplier confirmation arrives, after a status call, or on a set day each week for the open orders that matter most. It is most useful when the stock or the work is tight and a slipped date would cost a delivery.

The same person, or the supply planner they report to, reads the result and decides which shortages to escalate. Anything that changes the commercial terms of an order, such as a part-delivery, faster freight or a price change, belongs to the buyer with authority to agree it.

## What they supply

- **The open purchase order lines:** PO number, line, supplier, item code, description, quantity still open, order date and the supplier's original promise date.
- **The supplier replies:** the date each was logged, the supplier, the PO line, how it was given (written confirmation, call record or informal estimate), the date named in it if any, and a note.
- **The follow-ups already asked:** when, of whom, about which line, the question, and the date it was answered, blank if it has not been.
- **The dependent orders:** for each PO line, the customer or production order that waits on it and the date that order must ship by.
- **Settings:** today's date, who decides, and the receiving days between arrival and ready-to-ship.

Each export's column headers are checked first. If one does not match, the work stops and asks which column is which. The capability works from files you supply and needs no connection to your purchasing system.

## What comes out

One comparison in a fixed order: a summary and data checks, then every open line grouped by supplier with its original date, confirmed date, days moved and status, then the orders affected, then the unanswered follow-ups and the lines that need one, and a numbered question for each line that needs a decision. A section with nothing in it says "None."

The page shows its working. Each order's late or spare days can be checked with a calendar, and each line says which reply its date came from.

Nothing is sent. The capability does not write to a supplier, tell a customer or change an order date in your system.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): inbound dates compared with what the warehouse and the order book depend on.
- [Procurement and suppliers](https://fullypowered.ai/functions/procurement-and-suppliers/): a record of what each supplier said, when and how firmly, to take into the next call.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): components and materials whose late arrival stops a build.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): stock whose delay leaves customer orders waiting.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/): inbound goods where each dependent shipment has a cut-off.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when supplier dates live in inboxes and memory and the order book has outgrown them.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when more suppliers and more open orders make tracking by hand unreliable.

It is not a view of how reliable a supplier is over time, which is [supplier performance scorecard](https://fullypowered.ai/capabilities/supplier-performance-scorecard/). It is not a brief on an event that threatens a supplier, which is [supplier risk alert brief](https://fullypowered.ai/capabilities/supplier-risk-alert-brief/). Deciding what to reorder is [inventory reorder plan](https://fullypowered.ai/capabilities/inventory-reorder-plan/).

## What has to change for your company

- **Your export headers,** set once so the check passes without a question.
- **Your receiving days,** and whether they differ by site or product.
- **How replies are logged:** which of your records count as a written confirmation or a call record, and who may log one.
- **Who decides** which shortages to escalate, and who may agree a commercial change.
- **Where the dependent orders come from,** and what ship-by date means in your business.
- **Your AI product.** It runs in ChatGPT, Claude, Copilot or Gemini from the files you supply. It sends nothing, contacts no supplier and never asks for a password.

## What has been checked

Fully Powered AI wrote this capability template in its own words from its own map of the work, with no third-party text. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026, by a model that did not write it, and the record is published with it. It has not yet been tested in a client environment.

Testing in your environment means running it on a past week of open orders that your buyer remembers well, plus hard cases written in advance with their expected results: a renamed column, an estimate that is later than a confirmed date, a reply with no date, a line already past due, an order that waits on two lines. The buyer checks every date against the exports before anyone acts.

- Written by Fully Powered AI.
- Sources and rights reviewed.
- Editorially reviewed on 10 November 2026.
- Package format checked by script on every release.
- Tried once on its invented example in Claude on 10 November 2026. The record is in [TRIAL.md](TRIAL.md).
- Not yet tested in a client environment.

## What is in this folder

- [TEMPLATE.md](TEMPLATE.md): the complete capability template. Roles, inputs, the procedure, exceptions and stop conditions, the output format, a reviewer checklist, acceptance tests, the instructions for an AI assistant and what to customize.
- [EXAMPLE.md](EXAMPLE.md): a worked example with invented data.
- [TRIAL.md](TRIAL.md): what came out when the template was tried on its example.
- [SKILL.md](SKILL.md): the technical file, for AI products that load packaged instructions from a folder.
- [SOURCES.md](SOURCES.md): what the capability drew on, with licences.
- [LICENSE](LICENSE): MIT. Use it, change it, make it yours.

## Start using it

1. Read [EXAMPLE.md](EXAMPLE.md) to see what a good result looks like.
2. Open [TEMPLATE.md](TEMPLATE.md) and set every item under "What to customize" to your own rules, roles and limits.
3. Give your AI assistant the instruction block and the output format from the template, with your own limits in place of the ones the instructions leave open in square brackets. Paste them in as custom instructions in ChatGPT, Claude, Copilot or Gemini, or copy this whole folder into a product that loads `SKILL.md` packages. This folder stands alone; you do not need the rest of the repository.
4. Run it on past work first, using the reviewer checklist and acceptance tests in the template, before anyone relies on it.

## Related capabilities

- [Supplier risk alert brief](https://fullypowered.ai/capabilities/supplier-risk-alert-brief/)
- [Supplier performance scorecard](https://fullypowered.ai/capabilities/supplier-performance-scorecard/)
- [Inventory reorder plan](https://fullypowered.ai/capabilities/inventory-reorder-plan/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
