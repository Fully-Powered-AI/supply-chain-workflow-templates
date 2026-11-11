# Fully Powered Capability Templates: Supply Chain and Inventory

Know what is short before the customer does. These capability templates take the checking and comparing that keeps goods moving and give an AI assistant a precise way to prepare it from your own exports, with the planner making every call on what to order, move or promise.

This repository holds 6 capability templates for supply chain, inventory and fulfilment leads. Each one is a single piece of work with its own folder: what it is for and who starts it, the complete template an AI assistant follows, a worked example with invented data, what to change for your company, what has been checked, and its sources.

## The capabilities

- **[Carrier performance review](carrier-performance-review/)**: The shipping lead gets a lane-by-lane comparison of carriers from the delivery export and the freight charges: on-time delivery, damage, tracking gaps and cost, each with the shipments behind it. A person decides whether to raise issues or change carrier.
- **[Demand and supply review](demand-and-supply-review/)**: The operations lead gets one monthly review from the demand plan, confirmed supply and stock: where confirmed and likely demand outrun supply, what that does to inventory, and the decision each function head has to make. Sales ambition stays separate and nothing is forecast beyond your figures.
- **[Kit component availability check](kit-component-availability-check/)**: The stock or online-store lead gets every kit beside the quantity actually sellable, the component that limits it, the stock records that disagree and the listings that promise more than can be built. Nothing is changed until a person decides.
- **[Order size comparison](order-size-comparison/)**: When a supplier offers a bigger discounted order, the inventory planner gets each quantity costed the same way: yearly cost, cash tied up, months of cover and storage fit. The planner chooses the quantity; nothing is ordered.
- **[Supplier delivery date check](supplier-delivery-date-check/)**: The purchasing or operations person gets one comparison from the open purchase orders and the supplier replies: promised and revised dates side by side, the orders each change puts at risk, and the follow-ups still unanswered. No supplier is contacted.
- **[Unshipped order review](unshipped-order-review/)**: The fulfilment or customer-service lead gets one aged list of the orders not yet sent, whole or in part: how old each is, what is holding it, who owns the next step, and which orders have none. Nothing is released, moved or sent.

## How to use one

Open a folder and start with its README. Every folder stands alone, so copy the one you want and leave the rest. The templates are written for ChatGPT, Claude, Copilot and Gemini: paste the instruction block and the output format in as custom instructions, or load the folder in a product that reads `SKILL.md` packages.

In every template a person starts the work, supplies the inputs and decides. The template prepares and checks. Anything that sends, posts, pays or changes a record waits for a person to approve it.

## What "checked" means here

Each folder says exactly what was checked and when: who wrote it, that its sources and rights were reviewed, the date of its editorial review, and whether it has been tried on its invented example in a named AI product. Nothing is described as tested for a client unless it was. Test a template on your own past work before your team relies on it; each one comes with acceptance tests for that.

## More capabilities

The [Fully Powered Capabilities Directory](https://fullypowered.ai/capabilities/) lists every capability across functions and industries, with search. A machine-readable list of this repository is in [index.json](index.json).

## Licence and credits

MIT, in [LICENSE](LICENSE) and in every folder. Each folder's SOURCES.md names what the capability drew on. Published by [Fully Powered AI](https://fullypowered.ai/).
