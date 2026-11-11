# Carrier performance review: an invented example

*Illustrative example with invented data.* The company, the carriers, the lanes and every shipment and charge below are made up. Carrier A and Carrier B are invented names, not real carriers. The settings are an invented company's: review period October 2026, ship dates 2026-10-01 to 2026-10-31, today 2026-11-04, the review run by the logistics planner, grace days 0, fewest shipments to compare 4, and the default gaps worth a decision (10.0 points for on time, 5.0 points for damage, 10.0 points for tracking gaps, 10.0 percent for cost per kilogram). Currency is dollars. The company is Larkfield Candle Works, an invented company; the shipping lead is the invented Dana Ortiz.

## What the shipping lead supplies

Shipment export (service is "ground" on every row):

```
shipment_id,ship_date,carrier,lane,service,promised_date,delivered_date,weight_kg,damage,tracking_gap
S101,2026-10-02,Carrier A,Warehouse to Phoenix,ground,2026-10-06,2026-10-06,40,no,no
S102,2026-10-05,Carrier A,Warehouse to Phoenix,ground,2026-10-09,2026-10-10,55,no,yes
S103,2026-10-12,Carrier A,Warehouse to Phoenix,ground,2026-10-16,2026-10-16,30,no,no
S104,2026-10-20,Carrier A,Warehouse to Phoenix,ground,2026-10-24,2026-10-27,25,yes,yes
S105,2026-10-03,Carrier B,Warehouse to Phoenix,ground,2026-10-07,2026-10-07,38,no,no
S106,2026-10-08,Carrier B,Warehouse to Phoenix,ground,2026-10-12,2026-10-12,52,no,no
S107,2026-10-15,Carrier B,Warehouse to Phoenix,ground,2026-10-19,2026-10-18,45,no,no
S108,2026-10-22,Carrier B,Warehouse to Phoenix,ground,2026-10-26,2026-10-28,20,no,no
S109,2026-10-27,Carrier B,Warehouse to Phoenix,ground,2026-10-31,,35,no,yes
S110,2026-10-04,Carrier A,Warehouse to Seattle,ground,2026-10-09,2026-10-09,60,no,no
S111,2026-10-11,Carrier A,Warehouse to Seattle,ground,2026-10-16,2026-10-16,48,no,no
S112,2026-10-18,Carrier A,Warehouse to Seattle,ground,2026-10-23,2026-10-24,33,no,no
S113,2026-10-25,Carrier A,Warehouse to Seattle,ground,2026-10-30,2026-10-30,70,yes,no
S114,2026-10-26,Carrier A,Warehouse to Seattle,ground,,2026-10-31,22,no,no
```

Freight charges export:

```
invoice,shipment_id,carrier,charge_type,amount
INV-A-4410,S101,Carrier A,freight,62.00
INV-A-4410,S101,Carrier A,fuel,9.30
INV-A-4410,S102,Carrier A,freight,78.00
INV-A-4410,S102,Carrier A,fuel,11.70
INV-A-4410,S103,Carrier A,freight,51.00
INV-A-4410,S103,Carrier A,fuel,7.65
INV-A-4410,S104,Carrier A,freight,44.00
INV-A-4410,S104,Carrier A,fuel,6.60
INV-A-4410,S104,Carrier A,accessorial,15.00
INV-A-4410,S110,Carrier A,freight,88.00
INV-A-4410,S110,Carrier A,fuel,13.20
INV-A-4410,S111,Carrier A,freight,72.00
INV-A-4410,S111,Carrier A,fuel,10.80
INV-A-4410,S112,Carrier A,freight,56.00
INV-A-4410,S112,Carrier A,fuel,8.40
INV-A-4410,S113,Carrier A,freight,101.00
INV-A-4410,S113,Carrier A,fuel,15.15
INV-B-2207,S105,Carrier B,freight,58.00
INV-B-2207,S105,Carrier B,fuel,5.80
INV-B-2207,S106,Carrier B,freight,75.00
INV-B-2207,S106,Carrier B,fuel,7.50
INV-B-2207,S107,Carrier B,freight,66.00
INV-B-2207,S107,Carrier B,fuel,6.60
INV-B-2207,S108,Carrier B,freight,33.00
INV-B-2207,S108,Carrier B,fuel,3.30
INV-B-2207,S109,Carrier B,freight,52.00
INV-B-2207,S109,Carrier B,fuel,5.20
INV-B-2207,S199,Carrier B,freight,40.00
```

## What comes out

```
CARRIER PERFORMANCE REVIEW: October 2026

For: Dana Ortiz, shipping lead; run by the logistics planner. Ship dates 2026-10-01 to 2026-10-31; deliveries and charges as supplied on 2026-11-04.

Data checks: 14 shipments in the period; 0 outside it, with 0 charge lines totalling 0.00 left out. Charge lines: 27 matched to a shipment, 1 unmatched (INV-B-2207, S199, 40.00). Shipments with no charge line: S114. No delivery date: S109. No promised date: S114. Delivered before shipped: none. No damage entry: none. No tracking entry: none. No weight: none.

Lane comparison

Warehouse to Phoenix (ground)
- Carrier A: 4 shipments. On time 2 of 4 (50.0%). Damaged 1 of 4 (25.0%). Tracking gaps 2 of 4 (50.0%). Charges 285.25 on 4 invoiced shipments: 71.31 per shipment, 1.90 per kg.
- Carrier B: 5 shipments. On time 3 of 4 (75.0%). Damaged 0 of 5 (0.0%). Tracking gaps 1 of 5 (20.0%). Charges 312.40 on 5 invoiced shipments: 62.48 per shipment, 1.64 per kg.
- Compared with the best on each measure: on time, Carrier B highest; Carrier A lower by 25.0 points. Damage, Carrier B lowest; Carrier A higher by 25.0 points. Tracking gaps, Carrier B lowest; Carrier A higher by 30.0 points. Cost per kg, Carrier B lowest; Carrier A higher by 0.26 (15.9% of the lower printed figure).

Warehouse to Seattle (ground)
- Carrier A: 5 shipments. On time 3 of 4 (75.0%). Damaged 1 of 5 (20.0%). Tracking gaps 0 of 5 (0.0%). Charges 364.55 on 4 invoiced shipments: 91.14 per shipment, 1.73 per kg.
- Compared: no comparison, one carrier on this lane and service.

Charges by type
- Warehouse to Phoenix (ground), Carrier A: freight 235.00, fuel 35.25, accessorial 15.00, other 0.00; total 285.25.
- Warehouse to Phoenix (ground), Carrier B: freight 284.00, fuel 28.40, accessorial 0.00, other 0.00; total 312.40.
- Warehouse to Seattle (ground), Carrier A: freight 317.00, fuel 47.55, accessorial 0.00, other 0.00; total 364.55.

Points to raise
- Warehouse to Phoenix (ground), Carrier A: Late: S102, promised 2026-10-09, delivered 2026-10-10, 1 day; S104, promised 2026-10-24, delivered 2026-10-27, 3 days. Damaged: S104. Tracking gaps: S102, S104. Accessorial charges: S104, 15.00.
- Warehouse to Phoenix (ground), Carrier B: Late: S108, promised 2026-10-26, delivered 2026-10-28, 2 days. Damaged: none. Tracking gaps: S109. Accessorial charges: none.
- Warehouse to Seattle (ground), Carrier A: Late: S112, promised 2026-10-23, delivered 2026-10-24, 1 day. Damaged: S113. Tracking gaps: none. Accessorial charges: none.

Decisions for Dana Ortiz (1)
1. Warehouse to Phoenix (ground): Carrier A is behind Carrier B on on-time delivery by 25.0 points, on damage by 25.0 points, on tracking gaps by 30.0 points and on cost per kg by 0.26 (15.9%); each difference is at or above its gap. Whether to raise these with Carrier A, or to change the carrier on this lane.

Not supplied or not checked: no agreed rates, so the charges are not checked against them. No earlier period, so there is no trend. Damage and tracking gaps are as flagged in the export; no claim records were supplied.

Every figure traces to the shipment export for ship dates 2026-10-01 to 2026-10-31 and the charge export supplied on 2026-11-04. The review changes no records, contacts no carrier and sends nothing.
```

## How the figures were reached

Carrier A on Phoenix has four shipments, all with both dates: S102 (1 day late) and S104 (3 days late) are late, so 2 of 4 are on time, 50.0%. Carrier B has five shipments but S109 has no delivery date, leaving four to judge: S108 is 2 days late, S107 came a day early and counts as on time, so 3 of 4, 75.0%. Charges for Carrier A on Phoenix: 235.00 + 35.25 + 15.00 = 285.25 over 150 kg (40 + 55 + 30 + 25), which is 71.31 per shipment and 1.90 per kg. Carrier B: 284.00 + 28.40 = 312.40 over 190 kg, which is 62.48 and 1.64. The gap in cost per kg is worked from the printed figures: 1.90 less 1.64 is 0.26, and 0.26 over the lower printed figure, 1.64, is 15.9%. On Seattle, S114 has no promised date and no charge line, so on time is judged on four shipments and cost on four: 364.55 over 211 kg (60 + 48 + 33 + 70), 91.14 per shipment and 1.73 per kg. The unmatched charge for S199 is left out of every figure.
