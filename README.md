# AI workflow templates for supply chain and inventory teams

FullyPowered Workflow Templates for supply chain and inventory teams turn the AI your company already pays for into a team that knows how the work is done: a shipping lead with the carrier comparison by lane prepared, an inventory planner with each discounted order size costed the same way, a fulfilment lead with the aged list of unshipped orders prepared. 6 workflow templates, made to be customized and deployed. All plain Markdown, all free, MIT license.

We are FullyPowered AI. We build AI workflows for companies, and these are the templates we start from. We publish them because a good starting point should be open to everyone. Copy one. Change it. Make it yours.

> [!TIP]
> **Missing a template that is not listed here, or want these customized for your organization? Reach out to us.** These are templates, made to be customized and deployed. FullyPowered AI customizes and builds AI workflows, connects them to your business systems, installs them in your agents and puts them in the hands of the people who own the work. [See more examples for supply chain and inventory teams](https://fullypowered.ai/functions/supply-chain-and-inventory/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=supply-chain-readme&from=gh-supply-chain-readme) · [Have one built for your team](https://fullypowered.ai/pricing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=supply-chain-readme&from=gh-supply-chain-readme). Not sure where to start? Email hello@fullypowered.ai and a person will answer.

**Who this is for**

- Owners and CEOs who want stock, suppliers and shipments run with the same care every week.
- Supply chain and fulfilment leads who want a review their team can run this week.
- The planner or buyer who does the work, gets a precise way to prepare it and still decides.

**What these are for**

- **Your best way of doing it, for the whole team.** One piece of work, written down precisely enough that an assistant prepares it the same way every time.
- **Work you can check.** Every template says what it needs, what it produces, what it checked and what it could not.
- **A person decides.** Anything that sends, posts, pays or changes a record waits for someone to approve it.
- **Tied into your business systems.** A workflow can be designed to pull from the systems your company already runs, and even push data back into them, with guardrails and a person approving. [Browse the Connectors Directory](https://fullypowered.ai/connectors/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=supply-chain-readme&from=gh-supply-chain-readme).
- **Free, open and portable.** MIT-licensed plain instructions that run in the assistant or agent your team already uses: ChatGPT, Claude, Claude Code, Claude Cowork, Codex, Copilot, Gemini, Grok, Perplexity.

**Quick start**

1. **Check which orders a late supplier date puts at risk.** Copy the text below into ChatGPT, Claude, Copilot or Gemini. Paste in your open purchase order lines, the supplier replies you have logged and the customer orders that wait on them, then read what comes back. No sign-in here and nothing to download.

   ```text
   You are helping a buyer compare supplier delivery dates. Use only the
   information I paste below. Do not guess a date and do not forecast.

   For each open purchase order line, show the date the supplier first
   promised, the latest date confirmed in writing or on a recorded call,
   and how many days it moved. Treat an informal estimate as a note beside
   the line, never as the confirmed date. If a reply has no date, say so.
   Mark lines already past due.

   Then, for each customer order that waits on a line, add [my receiving
   days] days to the arrival date and compare it with the ship-by date. Say
   whether it is late or has spare days, and show the arithmetic.

   Finish with unanswered supplier questions and one numbered question for
   me per line that needs a decision.

   Today is [date]. The person who decides is [role]. Nothing is sent, no
   supplier is contacted and no order is changed. I decide what to do.

   [Paste open order lines, supplier replies, follow-ups and customer
   orders here]
   ```

2. Read what comes back. It marks what it checked and what is left for you. What comes back:

   ```text
   **SUPPLIER DELIVERY DATE CHECK: the Company, Tuesday 10 November 2026**

   For: the supply planner. Prepared Tuesday 10 November 2026 from: open orders (8 lines), supplier replies (9 rows), follow-ups (5 rows), dependent orders (11 rows), settings.
   Column check: all headers matched.
   Settings: receiving days 2, counted in calendar days. Defaults used: receiving days.
   Summary: 8 open lines. Moved later 2, moved earlier 1, as promised 2, estimate only 1, no confirmed date 2. Past due: 2. Orders on the list: 10; late on the date relied on 4; not late yet but resting on an unconfirmed date 3; spare days on a confirmed date, not listed 3. Unanswered follow-ups: 3. Lines needing a follow-up with none open: 1.

   **Data checks**

   - A reply for PO-2099 line 1 (Supplier A, logged Monday 2 November) has no line on the open orders. Left out; read as closed or mistyped.
   ```

3. Stop there. You will know if this is for you. When you want it fitted to your company, or built into your agents, [that is what we do](https://fullypowered.ai/pricing/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=supply-chain-readme&from=gh-supply-chain-readme).

A person starts each workflow, supplies the files and decides what to order, move, chase or promise; the template only prepares and checks.

These are examples and a starting point, made to be changed to fit how your company works. Your own work may not appear in them, and a workflow can be a single step or many, so a workflow that is not here can still be built.

## The workflow templates here today

- **[Carrier performance review](carrier-performance-review/)**: The shipping lead gets a lane-by-lane comparison of carriers from the delivery export and the freight charges: on-time delivery, damage, tracking gaps and cost, each with the shipments behind it. A person decides whether to raise issues or change carrier.
- **[Demand and supply review](demand-and-supply-review/)**: The operations lead gets one monthly review from the demand plan, confirmed supply and stock: where confirmed and likely demand outrun supply, what that does to inventory, and the decision each function head has to make. Sales ambition stays separate and nothing is forecast beyond your figures.
- **[Kit component availability check](kit-component-availability-check/)**: The stock or online-store lead gets every kit beside the quantity actually sellable, the component that limits it, the stock records that disagree and the listings that promise more than can be built. Nothing is changed until a person decides.
- **[Order size comparison](order-size-comparison/)**: When a supplier offers a bigger discounted order, the inventory planner gets each quantity costed the same way: yearly cost, cash tied up, months of cover and storage fit. The planner chooses the quantity; nothing is ordered.
- **[Supplier delivery date check](supplier-delivery-date-check/)**: The purchasing or operations person gets one comparison from the open purchase orders and the supplier replies: promised and revised dates side by side, the orders each change puts at risk, and the follow-ups still unanswered. No supplier is contacted.
- **[Unshipped order review](unshipped-order-review/)**: The fulfilment or customer-service lead gets one aged list of the orders not yet sent, whole or in part: how old each is, what is holding it, who owns the next step, and which orders have none. Nothing is released, moved or sent.

## How to use one

Open a folder and start with its README. Every folder stands alone, so copy the one you want and leave the rest. The templates are written for ChatGPT, Claude, Copilot and Gemini: paste the instruction block and the output format in as custom instructions, or load the folder in a product that reads `SKILL.md` packages.

To take the whole collection, press **Use this template** at the top of this page: it copies every folder into a repository in your own account, yours to change.

In every template a person starts the work, supplies the inputs and decides. The template prepares and checks. Anything that sends, posts, pays or changes a record waits for a person to approve it.

## What SKILL.md is

Each folder holds a file named `SKILL.md`. It is the technical file: the same instructions and output format as the template, in the packaged form that AI products which load instructions from a folder read. It is generated from `TEMPLATE.md`, so the two always agree. The workflow template is the whole folder; `SKILL.md` is one way of loading it. If your AI product does not read that format, use `TEMPLATE.md`.

## What "checked" means here

Each folder says exactly what was checked and when: who wrote it, that its sources and rights were reviewed, the date of its editorial review, and whether it has been tried on its example in a named AI product. Nothing is described as tested for a client unless it was. Test a template on your own past work before your team relies on it; each one comes with acceptance tests for that.

## More workflow templates

The [FullyPowered Workflows Directory](https://fullypowered.ai/workflows/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=supply-chain-readme&from=gh-supply-chain-readme) lists every workflow template across functions and industries, with search. A machine-readable list of this repository is in [index.json](index.json).

For the work these templates come from, by team and by task, see [AI workflow examples for supply chain and inventory teams](https://fullypowered.ai/functions/supply-chain-and-inventory/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=supply-chain-readme&from=gh-supply-chain-readme).

## Licence and credits

MIT, in [LICENSE](LICENSE) and in every folder. Each folder's SOURCES.md names what the workflow template drew on. Published by [FullyPowered AI](https://fullypowered.ai/?utm_source=github&utm_medium=referral&utm_campaign=workflow-collections&utm_content=supply-chain-readme&from=gh-supply-chain-readme).
