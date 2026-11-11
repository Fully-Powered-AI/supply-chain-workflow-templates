# Carrier performance review

The shipping lead gets a lane-by-lane comparison of carriers from the delivery export and the freight charges: on-time delivery, damage, tracking gaps and cost, each with the shipments behind it. A person decides whether to raise issues or change carrier.

*Capability template · Supply chain and inventory · version 0.1.0 · [Capabilities Directory](https://fullypowered.ai/capabilities/carrier-performance-review/)*

## The outcome

When the carrier review comes round, the shipping lead has one page that sets the carriers side by side on each lane, using only what the exports show. For every lane and service, each carrier's on-time deliveries, damaged shipments, shipments with a tracking gap and freight cost per shipment and per kilogram sit next to one another, with the counts behind them.

Every figure lists its evidence. A late-delivery figure names the late shipments, with the promised date, the delivery date and the days late. A damage figure names the shipments. A cost figure shows the charges by type, so a fuel or accessorial charge is visible rather than buried in a total.

The review compares like with like only. Carriers are set against each other on the same lane and the same service. A lane served by one carrier is reported but not compared, and a shipment with no delivery date is counted and listed, never treated as on time or late. It does not give a carrier an overall grade, and it does not pick one. It shows the gaps, and the shipping lead decides what to do with them.

## Who starts the work, and when

The shipping lead, logistics planner or an operations analyst starts it when the agreed carrier review is due, usually monthly or quarterly, once the period's deliveries are in and the carriers' freight invoices have been entered. The shipping lead reads the comparison and decides whether to raise points with a carrier or change carrier on a lane. Procurement approves any commitment to a carrier.

## What they supply

- **A shipment export** for the period: shipment, ship date, carrier, lane, service, promised date, delivery date, weight, whether it arrived damaged and whether it had a tracking gap.
- **A freight charges export:** invoice, shipment, carrier, type of charge and amount.
- **The settings:** the period, today's date, how many days late still counts as on time, the fewest shipments worth comparing, and the size of difference that is worth a decision.

The export's column headers are checked first. If one does not match, the work stops and asks which column is which.

## What comes out

One review in a fixed order: data checks, the comparison for each lane, the charges by type, the points to raise with each carrier, and the decisions for the shipping lead. A section with nothing in it says "None." The last lines say what was not supplied or not checked, and that nothing was changed or sent.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): delivery and freight cost read together, on one fixed method, whoever runs the review.
- [Procurement and suppliers](https://fullypowered.ai/functions/procurement-and-suppliers/): the facts to take into a carrier conversation before any commitment is made.
- [Logistics and trade](https://fullypowered.ai/industries/logistics-and-trade/): businesses that move goods on several lanes with more than one carrier.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): parcel and freight carriers whose lateness and damage reach customers directly.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/): outbound freight to customers and distributors, where a late truck can hold up a line.
- [Growth and scaling](https://fullypowered.ai/situations/growth-and-scaling/): when volume has grown past what the shipping lead can check by hand.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when carrier arrangements set years ago have not been compared since.

Rating suppliers of goods is [supplier performance scorecard](https://fullypowered.ai/capabilities/supplier-performance-scorecard/); this capability looks at the carriers that move them. The full cost of a product, with freight as one part, is [product landed cost worksheet](https://fullypowered.ai/capabilities/product-landed-cost-worksheet/). Writing to a carrier about a problem is outside this capability: the person who owns that relationship does it.

## What has to change for your company

- **Your export's column headers,** set once so the check passes without a question.
- **How you name lanes and services,** consistently, because the review takes the names exactly as written.
- **Your settings:** days late that still count as on time, the fewest shipments worth comparing, and the differences worth a decision.
- **What counts as a tracking gap** in your carriers' data, and where that flag comes from.
- **Who decides** what to raise and who approves a change of carrier.
- **Your AI product.** It runs in ChatGPT, Claude, Copilot or Gemini from the exports you supply. It needs no connection to your shipping or accounting systems, contacts no carrier and never asks for a password.

## What has been checked

Fully Powered AI wrote this capability template in its own words. It was editorially reviewed on 10 November 2026. It was tried on its invented example in Claude on 10 November 2026; the record of that run is published with it, and lists the edits made after the first run, with the run made again on the revised version. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a past period your shipping lead knows well, plus hard cases written in advance, each with its expected behavior: a renamed column, a shipment with no delivery date, a charge for a shipment not in the export, a lane with one carrier, two services on the same lane. The shipping lead checks every figure against the exports before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/capabilities/pilot-acceptance-test-preparation/) builds that test set, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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

- [Supplier performance scorecard](https://fullypowered.ai/capabilities/supplier-performance-scorecard/)
- [Product landed cost worksheet](https://fullypowered.ai/capabilities/product-landed-cost-worksheet/)

## Make it yours

This is the starting version. Fully Powered AI adapts capabilities to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
