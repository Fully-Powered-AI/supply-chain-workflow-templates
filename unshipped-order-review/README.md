# Unshipped order review

The fulfilment or customer-service lead gets one aged list of the orders not yet sent, whole or in part: how old each is, what is holding it, who owns the next step, and which orders have none. Nothing is released, moved or sent.

*Workflow template · Supply chain and inventory · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/unshipped-order-review/)*

## The outcome

Every morning there are orders that have not gone out, and most are fine: they came in an hour ago. The few that matter are the ones that have sat for days with nobody clearly responsible. This workflow template puts the whole set on one page, oldest first, so those few cannot hide among the rest.

Each order shows its age, the date it was promised, whether it is wholly unshipped or part-shipped and what is still to go, the hold on it and how long that hold has stood, and the next step with the name of whoever owns it. An order with a hold but no next step, or with no hold and no explanation, is pulled out into its own list.

The page works out what has shipped from the order lines, not from a status word. An order marked shipped whose lines say otherwise is shown for someone to confirm. An order with no shipping record at all is shown as unknown, never as shipped. A hold stays in force until a person releases it, however old it is.

You then decide the priorities, who takes over, and what each customer is told. The page gives you the facts to decide with and drafts no message.

## Who starts the work, and when

A fulfilment lead, a warehouse or operations manager, or a customer-service lead runs it at the start of each working day, or whenever the daily order review is due. A coordinator can prepare it from the exports.

The fulfilment lead sets the priorities and authorises any release or reassignment. The customer-service lead decides what customers hear. The workflow template changes no order, lifts no hold and contacts nobody.

## What they supply

- **The orders:** order number, order date, customer, promised date and the order's status from your system.
- **The order lines:** order number, line, item code, quantity ordered, quantity shipped and the date of the last shipment.
- **The active holds:** order number, the reason, the date it was placed, who owns it, the next step and who owns that.
- **Settings:** today's date, the age bands, which status words mean shipped and cancelled, and the limits for a hold and for a part-shipped order.

Each export's column headers are checked first. If one does not match, the work stops and asks which column is which. It works from files you supply and needs no connection to your order system.

## What comes out

One page in a fixed order: a summary and data checks, the aged list with every open order, the orders with no usable next step, the holds past your limit, the part-shipped orders with no recent shipment, the statuses to confirm, and a numbered question for the lead on each order that needs a decision. A section with nothing in it says "None."

Every age and count can be checked with a calendar and the exports. Each order says which hold and which items it comes from.

Nothing is sent. The workflow template releases no order, reassigns nothing and writes to no customer.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): the daily view of what is waiting to leave the warehouse.
- [Customer support and service](https://fullypowered.ai/functions/customer-support-and-service/): the answer to "where is my order" before the customer asks.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): web and marketplace orders held for stock, payment or address checks.
- [Consumer brands](https://fullypowered.ai/industries/consumer-brands/): direct orders alongside wholesale ones, each with its own holds.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): made-to-order and part-built orders waiting on parts or finishing.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when holds live in notes and memory rather than in a list.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when there are more open orders than anyone can check by eye each morning.

It looks at orders, not support tickets; the review of old tickets is [stale ticket sweep](https://fullypowered.ai/workflows/stale-ticket-sweep/). It does not judge a supplier's date, which is [supplier delivery date check](https://fullypowered.ai/workflows/supplier-delivery-date-check/). Deciding what to reorder is [inventory reorder plan](https://fullypowered.ai/workflows/inventory-reorder-plan/).

## What has to change for your company

- **Your export headers,** set once so the check passes without a question.
- **Your age bands,** and which band is young enough to need no explanation.
- **Your status words** for shipped and cancelled.
- **Your limits:** how many days a hold may stand, and how many days a part-shipped order may go without a shipment.
- **Who decides** priorities and releases, and who decides what customers are told.
- **Your AI product.** It runs in ChatGPT, Claude, Copilot or Gemini from the files you supply. It sends nothing and never asks for a password.

## What has been checked

Fully Powered AI wrote this workflow template in its own words from its own map of the work, with no third-party text. It was editorially reviewed on 10 November 2026. It was tried on its invented example on 10 November 2026 in Claude; the record is published with it. It has not yet been tested in a client environment.

Testing in your environment means running it on a past morning's orders that your fulfilment lead remembers well, plus hard cases written in advance with their expected results: a renamed column, an order marked shipped with an open line, an order with no lines, a hold with no next step, a hold older than the limit. The lead checks every age and every hold against the exports before anyone acts.

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

- [Stale ticket sweep](https://fullypowered.ai/workflows/stale-ticket-sweep/)
- [Supplier delivery date check](../supplier-delivery-date-check/)
- [Inventory reorder plan](https://fullypowered.ai/workflows/inventory-reorder-plan/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
