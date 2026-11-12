# Demand and supply review

The operations lead gets one monthly review from the demand plan, confirmed supply and stock: where confirmed and likely demand outrun supply, what that does to inventory, and the decision each function head has to make. Sales ambition stays separate and nothing is forecast beyond your figures.

*Workflow template · Supply chain and inventory · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflows/demand-and-supply-review/)*

## The outcome

Once a month, sales, production, purchasing and finance sit down with the same page. It shows, item by item, the demand your supply plan cannot cover, and it shows that demand in three clearly separated layers: orders that are confirmed, units the sales head backs with a stated reason, and sales ambition that has neither. Only supply that has been confirmed counts. A request still waiting on a supplier is shown beside the gap and never subtracted from it.

The page also says what the gaps mean for stock: which items run below their safety stock, which run short, and which end the period holding more than your own allowance, with the cost of that excess. It closes with the decisions each function head has to make, written as questions with their facts. The operations lead edits and approves the draft, and each function head decides their own response.

## Who starts the work, and when

The owner or the operations lead runs it at the start of the monthly demand and supply meeting cycle, once sales has updated the demand plan and purchasing has updated what suppliers have confirmed. The same person takes the approved page into the meeting.

## What they supply

- The demand plan by item and month: confirmed units, supported units with the reason, and sales ambition.
- The supply commitments by item and month, each marked confirmed or not.
- Stock on hand, safety stock and unit cost for each item.
- Capacity limits by item and month, where there are any.
- The decisions recorded at earlier reviews, and the settings: the months to cover and the function heads.

## What comes out

One review in a fixed order: a summary, then the items whose demand the supply plan cannot cover, the inventory implications, anything that could not be tested, the decisions for each function head, the decisions carried from earlier months, and check lines that tie the totals. If a file's column headers do not match, the review stops and asks before drawing anything.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Supply chain & inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/), where the planning cycle lives.
- [Operations & process improvement](https://fullypowered.ai/functions/operations-and-process-improvement/), for the operations lead who runs the monthly meeting.
- [Manufacturing](https://fullypowered.ai/industries/manufacturing/), where capacity limits and confirmed material decide what can be made.
- [E-commerce & retail](https://fullypowered.ai/industries/ecommerce-and-retail/), where sales plans and stock commitments meet every month.
- [Consumer brands](https://fullypowered.ai/industries/consumer-brands/), where promotions raise demand before supply is confirmed.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/), when sales ambition starts to outrun what suppliers and production can deliver.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/), where the monthly meeting already exists and needs a shared page.

## What has to change for your company

Name your function heads and the month the review covers. Decide which sales reasons count as a basis for supported demand, and who decides that. Set your excess allowance; the starting rule is safety stock plus an average month of likely demand. Agree what your suppliers' confirmation looks like, so that "confirmed" means the same thing to everyone. Keep one export layout for each file so the headers match every month.

## What has been checked

Fully Powered AI wrote this workflow template. It was editorially reviewed on 10 November 2026. It was tried on its invented example in Claude on 10 November 2026, and the run was repeated after corrections by the model that made them, so it is not independent of the example; the record is published with it. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on a past month your team already knows, with cases written in advance: a confirmed order the supply cannot meet, a supplier request that is not confirmed, supported units with no reason given, an item with no stock row. The operations lead checks every balance against a hand calculation before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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
- [Operations KPI scorecard](https://fullypowered.ai/workflows/operations-kpi-scorecard/)
- [Slow-moving stock and markdown plan](https://fullypowered.ai/workflows/slow-moving-stock-and-markdown-plan/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
