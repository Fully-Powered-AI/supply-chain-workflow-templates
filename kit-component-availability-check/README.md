# Kit component availability check

The stock or online-store lead gets every kit beside the quantity actually sellable, the component that limits it, the stock records that disagree and the listings that promise more than can be built. Nothing is changed until a person decides.

*Workflow template · Supply chain and inventory · version 0.1.0 · [Workflows Directory](https://fullypowered.ai/workflow templates/kit-component-availability-check/)*

## The outcome

A kit is only as available as its scarcest part. A gift box can show forty in stock on the store while one of its three components is down to six, or sit in the other warehouse, or already be promised to open orders. The total on the screen hides it until a customer has paid for a kit nobody can pack.

This workflow template puts each kit beside what can actually be built. For every kit it works out the number sellable at each location from what is on hand less what is reserved, names the component that limits it, and shows the figure to rely on. Where two stock records disagree about a component, it works the kit out both ways and relies on the lower number until someone settles the difference. It then sets that number against what each sales channel is currently offering and shows where a listing promises more than can be built.

It also catches a trap that no single kit shows: two kits drawing on the same component. Each looks fine alone; sold together they need more than the shelf holds. Those are listed, with the shortfall, for the planner to decide.

The stock lead corrects the records and the listings. This workflow template changes no stock figure and no listing.

## Who starts the work, and when

The stock lead, or the online-store lead who sells kits and bundles built from separate items, starts it. Typical moments are before a promotion or a gift season, after a delivery or a count, when a customer is told a kit is out although the shelves look full, or on a regular day each week. The inventory planner reviews the draft and confirms the quantities before any promise to customers or any listing changes.

## What they supply

- **Kit definitions:** for each kit, its components and how many of each go into one kit.
- **A stock export:** each component by location, with the quantity on hand and the quantity reserved.
- **A second stock record,** if the business keeps one, such as the sales platform's own figures. This is how conflicting records are found.
- **A listing export,** if the kits are sold on one or more channels: the quantity each channel currently shows for each kit.
- **The settings:** which locations can pack kits, when each export was taken, and how old a record may be before it is not trusted.

Each file's column headers are checked first. If one does not match, the work stops and asks which column is which.

## What comes out

One page in a fixed order: the basis of the check, a summary, any problems found in the files, then each kit on its own line with the sellable quantity by location, the limiting component, the figure to rely on and how it compares with each listing. After that come the stock records that disagree, the components that more than one kit depends on, the listings a person should correct, and numbered questions. An empty section says "None." Every figure traces to a row in a supplied file, and the arithmetic is simple enough to recheck by hand.

See the worked example with invented data in [EXAMPLE.md](EXAMPLE.md).

## Where it fits

- [Supply chain and inventory](https://fullypowered.ai/functions/supply-chain-and-inventory/): the check that looks inside a stock total before a delivery promise is made.
- [E-commerce and retail](https://fullypowered.ai/industries/ecommerce-and-retail/): stores selling bundles, gift sets and multipacks built from items that also sell alone.
- [Consumer brands](https://fullypowered.ai/industries/consumer-brands/): brands that assemble sets and seasonal boxes from their own products.
- [Hardware and physical technology](https://fullypowered.ai/industries/hardware-and-physical-technology/): device kits and starter packs where one missing part holds back the whole box.
- [Growth & scaling](https://fullypowered.ai/situations/growth-and-scaling/): when more kits, channels and locations make the shelves harder to check by eye.
- [Established businesses](https://fullypowered.ai/situations/established-businesses/): when the same few best-selling kits keep going out of stock without warning.

It is not a count reconciliation; for that, use [stock count reconciliation](https://fullypowered.ai/workflows/stock-count-reconciliation/), which settles the books against the shelf. It does not decide what to order; the [inventory reorder plan](https://fullypowered.ai/workflows/inventory-reorder-plan/) does. [Slow-moving stock and markdown plan](https://fullypowered.ai/workflows/slow-moving-stock-and-markdown-plan/) covers the opposite problem, components that sit unsold.

## What has to change for your company

- **Your export headers,** set once so the column check passes without a question.
- **Which locations can pack kits,** and whether a kit may be built from parts held in two places.
- **How old a record may be,** before the kits that depend on it are left unresolved.
- **What counts as reserved:** open orders, held stock, display units or anything else you set aside.
- **Who confirms the quantities** and who corrects listings on each channel.
- **Your AI product.** It runs in ChatGPT, Claude, Copilot or Gemini from the files you supply. It needs no connection to your store or stock system, changes nothing in them and never asks for a password.

## What has been checked

Fully Powered AI wrote this workflow template in its own words, from its own published map of the work, with no third-party text. It was editorially reviewed on 10 November 2026. It was tried once on its invented example in Claude on 10 November 2026. That run was not blind, because the example's published output was on screen when it was made, and it found gaps in the instructions. They were fixed afterward and the template was run on the example again; the record of that second run is published with it. Only the success path has been run: the stop conditions and the acceptance tests have not. It has not yet been tested in a client environment. It has not yet been tested as a packaged version in ChatGPT, Claude, Copilot or Gemini.

Testing in your environment means running it on one or two kits your stock lead knows well, with hard cases written in advance: a component with no stock row, two records that disagree, a reservation larger than the stock, a listing above what can be built, and two kits that share a part. The stock lead checks every line against the exports before anyone relies on it. [Pilot acceptance-test preparation](https://fullypowered.ai/workflows/pilot-acceptance-test-preparation/) sets those cases up, and [what we test before we call an AI workflow ready](https://fullypowered.ai/insights/what-we-test-before-a-workflow-is-ready/) describes the record we keep.

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

- [Stock count reconciliation](https://fullypowered.ai/workflow templates/stock-count-reconciliation/)
- [Inventory reorder plan](https://fullypowered.ai/workflow templates/inventory-reorder-plan/)
- [Slow-moving stock and markdown plan](https://fullypowered.ai/workflow templates/slow-moving-stock-and-markdown-plan/)

## Make it yours

This is the starting version. Fully Powered AI adapts workflow templates to how your company works, proves them on real work and rolls them out to the roles that use them. [Talk with us](https://fullypowered.ai/contact/).
