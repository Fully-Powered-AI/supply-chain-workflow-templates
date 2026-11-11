# Order size comparison: an invented example

*Illustrative example with invented data.* The company, the supplier, the product, the prices, the demand and every date below are invented. The company, called the Company here, sells stainless water bottles online and buys them from Supplier A. Its inventory planner runs the comparison and the planner selects the quantity. People are referred to by role.

The inputs come first, in full, so the template can be run on them. The comparison follows.

## The inputs

### 1. Settings (typed by the planner)

```
Item: BOT-500, Stainless water bottle 500 ml
Supplier: Supplier A
Today: Tuesday 10 November 2026
Selects the quantity: the inventory planner
Currency: US dollars
Holding rate: 24% a year
Cost of placing and receiving one order: 45.00
Standard option: Standard
Stock expected on hand when an order arrives: 40
Storage limit: 800 units
Shelf life: not given
```

### 2. The supplier's offer

```
option,quantity,unit_price,freight_per_order
Standard,300,8.40,60.00
Mid,600,8.00,90.00
Pallet,1200,7.60,150.00
```

### 3. Demand history (units sold, last twelve months)

```
month,units_sold
2025-11,105
2025-12,100
2026-01,98
2026-02,92
2026-03,105
2026-04,100
2026-05,104
2026-06,97
2026-07,101
2026-08,99
2026-09,103
2026-10,96
```

### 4. Notes (typed by the planner)

```
- Supplier A holds the Pallet price only if the order is confirmed by
  Friday 20 November 2026.
- No change in demand expected over the next twelve months.
```

## The output

**ORDER SIZE COMPARISON: BOT-500 Stainless water bottle 500 ml, Supplier A**

- **For:** the inventory planner. Prepared Tuesday 10 November 2026 from: offer (3 options), demand history (12 months, November 2025 to October 2026), settings, notes.
- **Column check:** all headers matched.
- **Settings:** holding rate 24% a year; cost of placing and receiving one order \$45.00; standard option Standard; stock expected on hand when an order arrives 40; storage limit 800 units; shelf life not given; demand-drop test 25%; seasonal flag at a month above 1.5 times or below 0.5 times the average. Defaults used: the demand-drop test and the seasonal flag.
- **Demand:** 1,200 units in 12 months = 100.0 a month, 1,200 a year. Pattern: stable (highest month 105 in November 2025 and March 2026, lowest 92 in February 2026; none above 150.0 or below 50.0). The planner's note expects no change.
- **Summary:** 3 options compared; 2 fit the storage limit. Lowest yearly cost of the options that fit: Mid, \$10,446.00, \$356.40 a year below Standard. Lowest yearly cost overall: Pallet, \$10,409.40, which does not fit (440 units over the storage limit). Conditions not priced: 1.

**Standard** (the standard option): 300 units at \$8.40, freight \$60.00 per order.

- Orders a year: 1,200 ÷ 300 = 4.0.
- Goods: 1,200 × \$8.40 = \$10,080.00.
- Ordering: 4.0 × (\$45.00 + \$60.00) = \$420.00.
- Holding: (300 ÷ 2) × \$8.40 × 24% = \$302.40.
- Yearly cost: \$10,802.40 (\$9.00 a unit).
- Against the standard option: this is the standard option.
- Cash tied up in goods on arrival: 300 × \$8.40 = \$2,520.00.
- Cover: 3.0 months; 4.0 months if demand is 25% lower (75.0 a month).
- Storage: 40 + 300 = 340 of 800 units; fits, 460 units to spare.
- Shelf life: not given.

**Mid**: 600 units at \$8.00, freight \$90.00 per order.

- Orders a year: 1,200 ÷ 600 = 2.0.
- Goods: 1,200 × \$8.00 = \$9,600.00.
- Ordering: 2.0 × (\$45.00 + \$90.00) = \$270.00.
- Holding: (600 ÷ 2) × \$8.00 × 24% = \$576.00.
- Yearly cost: \$10,446.00 (\$8.71 a unit).
- Against the standard option: \$356.40 a year lower. Extra cash tied up on arrival: \$4,800.00 − \$2,520.00 = \$2,280.00. Saving per \$1,000 of extra cash: \$156.32. Break-even holding rate: 55.3% ((\$10,500.00 − \$9,870.00) ÷ (\$2,400.00 − \$1,260.00)); above that rate Standard costs less.
- Cash tied up in goods on arrival: 600 × \$8.00 = \$4,800.00.
- Cover: 6.0 months; 8.0 months if demand is 25% lower (75.0 a month).
- Storage: 40 + 600 = 640 of 800 units; fits, 160 units to spare.
- Shelf life: not given.

**Pallet**: 1,200 units at \$7.60, freight \$150.00 per order. DOES NOT FIT STORAGE.

- Orders a year: 1,200 ÷ 1,200 = 1.0.
- Goods: 1,200 × \$7.60 = \$9,120.00.
- Ordering: 1.0 × (\$45.00 + \$150.00) = \$195.00.
- Holding: (1,200 ÷ 2) × \$7.60 × 24% = \$1,094.40.
- Yearly cost: \$10,409.40 (\$8.67 a unit).
- Against the standard option: \$393.00 a year lower. Extra cash tied up on arrival: \$9,120.00 − \$2,520.00 = \$6,600.00. Saving per \$1,000 of extra cash: \$59.55. Break-even holding rate: 35.9% ((\$10,500.00 − \$9,315.00) ÷ (\$4,560.00 − \$1,260.00)); above that rate Standard costs less.
- Cash tied up in goods on arrival: 1,200 × \$7.60 = \$9,120.00.
- Cover: 12.0 months; 16.0 months if demand is 25% lower (75.0 a month).
- Storage: 40 + 1,200 = 1,240 of 800 units; does not fit, 440 units over.
- Shelf life: not given.

**Not priced**

- The Pallet price holds only if the order is confirmed by Friday 20 November 2026 (notes), ten days from today.

**Questions for the inventory planner**

1. Pallet needs room for 1,240 units against a limit of 800, 440 over. Is there space for the 440 units?

Draft for the inventory planner's decision. The planner selects the quantity. Nothing has been ordered, sent or changed in any system.
