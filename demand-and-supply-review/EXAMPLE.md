# Demand and supply review: an invented example

*Illustrative example with invented data.* The company, the items, the suppliers, the roles and every figure below are invented. "Company A" is an invented 35-person business that makes and sells garden planters. The operations lead runs the review; the sales head, the production lead, the purchasing lead and the finance lead each own a part of the response. First come the inputs the operations lead supplied, in full, then the review the workflow template returned.

## The inputs

### 1. Settings

```
Review month: December 2026. Review date: Tuesday 1 December 2026.
Periods covered: 2026-12, 2027-01, 2027-02
Supply planning lead: Operations lead
Function heads: Sales head, Production lead, Purchasing lead, Finance lead
Excess allowance: the default (safety stock plus average monthly likely demand)
```

### 2. Stock (stock.csv)

```
item,description,on_hand,safety_stock,unit_cost
A1,Large planter,400,150,18.00
A2,Medium planter,900,200,11.50
B1,Saucer set,300,100,6.00
C1,Self-watering insert,120,60,4.50
```

### 3. Demand plan (demand.csv)

```
item,period,confirmed_units,supported_units,ambition_units,basis
A1,2026-12,300,150,100,Repeat pattern Retailers 1 and 2 last four months
A1,2027-01,250,150,100,Repeat pattern Retailers 1 and 2 last four months
A1,2027-02,200,200,150,Repeat pattern Retailers 1 and 2 last four months
A2,2026-12,250,100,0,Repeat pattern last four months
A2,2027-01,200,100,50,Repeat pattern last four months
A2,2027-02,150,100,50,Repeat pattern last four months
B1,2026-12,180,40,0,Sold with A1 orders
B1,2027-01,150,50,0,Sold with A1 orders
B1,2027-02,120,60,0,Sold with A1 orders
C1,2026-12,100,0,200,
C1,2027-01,80,0,150,
C1,2027-02,60,40,100,
```

### 4. Supply commitments (supply.csv)

```
item,period,source,units,status
A1,2026-12,Own production,250,confirmed
A1,2027-01,Own production,200,confirmed
A1,2027-01,Own production,100,requested
A1,2027-02,Own production,200,confirmed
A2,2026-12,Own production,300,confirmed
A2,2027-01,Own production,300,confirmed
A2,2027-02,Own production,200,confirmed
B1,2026-12,Supplier B,200,confirmed
B1,2027-01,Supplier B,100,confirmed
B1,2027-02,Supplier B,150,confirmed
C1,2026-12,Supplier A,100,confirmed
C1,2027-01,Supplier A,100,requested
```

### 5. Capacity (capacity.csv)

```
item,period,max_units
A1,2026-12,300
A1,2027-01,300
A1,2027-02,300
C1,2026-12,100
C1,2027-01,150
C1,2027-02,150
```

### 6. Earlier decisions (decisions.csv)

```
id,item,decision,owner,due,status
D07,C1,Ask Supplier A for a firm January delivery,Purchasing lead,2026-11-27,open
D08,A2,Hold the A2 run at 300 units a month until January,Production lead,2026-11-20,done
```

## The review

```
DEMAND AND SUPPLY REVIEW: December 2026

For: Operations lead, for the monthly review on Tuesday 1 December 2026. Periods: 2026-12 to 2027-02. Units as supplied; values at unit cost from the stock file.
Inputs: demand plan demand.csv; supply supply.csv; stock stock.csv; capacity capacity.csv; earlier decisions decisions.csv.
Items: 4 reviewed, 0 not tested.

Summary
Short on confirmed demand: C1, largest shortfall 20 units in 2027-02.
Short on likely demand: A1, largest shortfall 200 units in 2027-02; C1, largest shortfall 20 units in 2027-02.
Below safety stock but not short: none.
Excess stock: A2, 300 units, $3,450.
Short if sales ambition is added: A1, largest shortfall 550 units in 2027-02; C1, largest shortfall 510 units in 2027-02.

Gaps: demand the supply plan cannot cover
A1 Large planter
Balance by period, confirmed demand: 2026-12 350; 2027-01 300; 2027-02 300.
Balance by period, likely demand: 2026-12 200; 2027-01 0; 2027-02 -200.
Balance by period, with sales ambition: 2026-12 100; 2027-01 -200; 2027-02 -550.
Confirmed demand: covered, lowest balance 300 in 2027-01.
Likely demand: first short 2027-02, largest shortfall 200 in 2027-02. Below safety stock of 150 first in 2027-01.
Sales ambition: 350 units over the periods; first short 2027-01, largest shortfall 550 in 2027-02.
Supply requested, not confirmed: 100 in 2027-01 from Own production. Largest likely shortfall if all were confirmed: 100 in 2027-02.
Capacity room by period: 2026-12 50; 2027-01 0; 2027-02 100.

C1 Self-watering insert
Balance by period, confirmed demand: 2026-12 120; 2027-01 40; 2027-02 -20.
Balance by period, likely demand: 2026-12 120; 2027-01 40; 2027-02 -20.
Balance by period, with sales ambition: 2026-12 -80; 2027-01 -310; 2027-02 -510.
Confirmed demand: first short 2027-02, largest shortfall 20 in 2027-02.
Likely demand: first short 2027-02, largest shortfall 20 in 2027-02. Below safety stock of 60 first in 2027-01.
Sales ambition: 490 units over the periods; first short 2026-12, largest shortfall 510 in 2027-02. Supported units moved to ambition for lack of a basis: 40 in 2027-02.
Supply requested, not confirmed: 100 in 2027-01 from Supplier A. Largest likely shortfall if all were confirmed: none.
Capacity room by period: 2026-12 0; 2027-01 50; 2027-02 150.

Inventory implications
A1: below safety stock from 2027-01 (balance 0 against 150), then short by 200 in 2027-02.
C1: below safety stock from 2027-01 (balance 40 against 60), then short by 20 in 2027-02.
A2: excess. Likely balance in 2027-02 is 800 against an allowance of 500 (safety stock 200 plus average monthly likely demand 300): 300 units over, $3,450 at $11.50 a unit.
No other item is below safety stock or holds excess.

Not tested
None.

Decisions needed from each function head
Sales head (4)
1. A1. Likely demand exceeds confirmed supply by 200 units in 2027-02; confirmed demand is covered. Supported units for A1 are 150, 150 and 200 across the three periods. Do those supported units still stand, and if supply stays as it is, whose supported volume is met first?
2. C1. Confirmed orders exceed supply by 20 units in 2027-02 (60 units confirmed, none supplied; the 40 units left over from 2027-01 cover part of them). Could any of the confirmed C1 orders for 2027-02 be met in a later period?
3. C1. The 40 supported units in 2027-02 have no basis in the demand plan, so they are counted as sales ambition. What is the basis for them, or should they stay as ambition?
4. A1 and C1. Sales ambition is 350 units for A1 and 490 for C1 and is untested against any order or stated basis. If it were added, A1 would be short by 550 units and C1 by 510, both in 2027-02. Should any of it be given a basis and counted as supported demand? (A2 also carries 100 ambition units and stays covered.)
Production lead (2)
5. A1. Confirmed production is 250, 200 and 200 units; 100 more is requested for 2027-01. Capacity is 300 a month, so the room left is 50, 0 and 100 units. If the request were confirmed, the largest likely shortfall would be 100 units in 2027-02. Can the 100 requested units for 2027-01 be confirmed, and can production in 2027-02 go above the 200 now confirmed, up to the stated 300?
6. A2. Confirmed production is 300, 300 and 200 units. With 900 on hand, the likely balance in 2027-02 is 800. Do the confirmed A2 runs stay as they are?
Purchasing lead (1)
7. C1. Confirmed supply is 100 units in 2026-12 and none after; 100 units from Supplier A are requested for 2027-01. Capacity leaves room of 0, 50 and 150 units. If the request were confirmed the likely balances would be 120, 140 and 80. Can the January request be confirmed, and is any supply to be requested for 2027-02? Earlier decision D07 covers the January request.
Finance lead (1)
8. A2. The likely balance in 2027-02 is 300 units over the allowance, worth $3,450 at unit cost. Is that stock acceptable to carry through the periods covered?

Carried from earlier reviews
D07, C1, Ask Supplier A for a firm January delivery, Purchasing lead, due 2026-11-27, open. The January supply for C1 is still marked requested (100 units), not confirmed. The due date is before the review date.
Decisions recorded as done: 1.

Check lines
Confirmed demand: opening 1,720 + confirmed supply 2,000 - confirmed demand 2,040 = 1,680, the sum of the closing balances.
Likely demand: opening 1,720 + confirmed supply 2,000 - likely demand 2,990 = 730, the sum of the closing balances.

Draft for the Operations lead. Nothing has been ordered, promised, sent or changed. Each function head decides their own response.
```
