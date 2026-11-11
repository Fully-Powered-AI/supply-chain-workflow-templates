# Kit component availability check: an invented example

*Illustrative example with invented data.* The business, the kits, the components, the quantities and every date below are invented. The business is an invented online gift shop, called the Shop here, with two places that can pack kits, Main and Annex. It keeps its stock in a stock system and also has a second stock record on its web shop platform, and it sells kits on its own web shop and on one marketplace. People are referred to by role.

The inputs come first, in full, so the template can be run on them. The check follows. Labels are set in bold and sections as lists here for reading; the template prints them as plain text.

## The inputs

### 1. Settings (typed by the stock lead)

```
Business: the Shop
Today: Tuesday 10 November 2026
Locations that can pack kits: Main, Annex
Parts from different locations may be combined: not given
Export dates: kit definitions, stock export, second stock record and
  listing export were all taken on 10 November 2026
Stale limit: not given
Stock lead: the stock lead
Approver: the inventory planner
```

### 2. Kit definitions

```
kit_code,kit_name,component_code,qty_per_kit
GFT-SPA,Spa gift box,SOAP-1,2
GFT-SPA,Spa gift box,CAND-1,1
GFT-SPA,Spa gift box,BOX-L,1
GFT-HOME,Home set,CAND-1,2
GFT-HOME,Home set,MUG-1,2
GFT-HOME,Home set,BOX-L,1
GFT-TEA,Tea sampler,TEA-A,3
GFT-TEA,Tea sampler,TEA-B,3
GFT-TEA,Tea sampler,BOX-S,1
GFT-TEAP,Tea duo,TEA-A,2
GFT-TEAP,Tea duo,BOX-S,1
GFT-NEW,Winter tin set,TIN-9,1
GFT-NEW,Winter tin set,CAND-1,1
```

### 3. Stock export

```
component_code,description,location,on_hand,reserved
SOAP-1,Lavender soap bar,Main,40,6
SOAP-1,Lavender soap bar,Annex,10,0
CAND-1,Soy candle,Main,25,5
CAND-1,Soy candle,Annex,4,0
BOX-L,Large gift box,Main,30,10
BOX-L,Large gift box,Annex,12,2
MUG-1,Stoneware mug,Main,20,0
MUG-1,Stoneware mug,Annex,0,0
TEA-A,Tea blend A,Main,30,0
TEA-B,Tea blend B,Main,8,2
BOX-S,Small gift box,Main,50,0
```

### 4. Second stock record (web shop platform)

```
component_code,location,on_hand
SOAP-1,Main,36
SOAP-1,Annex,10
CAND-1,Main,25
CAND-1,Annex,4
BOX-L,Main,30
BOX-L,Annex,12
MUG-1,Main,17
MUG-1,Annex,0
TEA-A,Main,30
TEA-B,Main,8
BOX-S,Main,50
```

### 5. Listing export

```
kit_code,channel,listed_qty
GFT-SPA,Web shop,25
GFT-HOME,Web shop,8
GFT-TEA,Web shop,12
GFT-TEA,Marketplace,6
GFT-TEAP,Web shop,15
GFT-NEW,Web shop,5
GFT-OLD,Web shop,3
```

## The output

**KIT COMPONENT AVAILABILITY CHECK: the Shop, stock as of Tuesday 10 November 2026**

- **For:** the stock lead and the inventory planner. Prepared Tuesday 10 November 2026 from: kit definitions (13 rows, 5 kits), stock export (11 rows, exported 10 November 2026), second stock record (11 rows, web shop platform, exported 10 November 2026), listing export (7 rows, exported 10 November 2026), settings.
- **Column check:** all headers matched.
- **Basis:** packing locations Main and Annex; stock at other locations ignored. Available is on hand less reserved; a component with no row for a location counts as 0 there. Each kit is built at one location from the parts held there. Incoming stock is not counted. Freshness: all files within 3 days.
- **Settings:** stale limit 3 days; approver the inventory planner. Defaults used: stale limit, parts from different locations.
- **Summary:** 5 kits defined. Sellable 1. Conflict 3. Zero 0. Unresolved 1. Component clashes between kits 2. Stock records in conflict 2. Listings to correct 2.

**Record checks**

- GFT-NEW: component TIN-9 has no row in the stock export. See question 1.
- GFT-OLD is in the listing export (Web shop, 3) and has no kit definition. See question 2.

**Kit by kit**

- **GFT-NEW** Winter tin set. Unresolved: TIN-9 has no row in the stock export. Sellable: cannot be stated. Listed: Web shop 5, total 5; not compared.
- **GFT-HOME** Home set. Conflict: the two stock records disagree on MUG-1 at Main. Sellable to rely on 8. By location: Main 8 (limit MUG-1), Annex 0 (limit MUG-1). On the stock export 10; on the lower of the two records 8. Listed: Web shop 8, total 8; matches.
- **GFT-SPA** Spa gift box. Conflict: the two stock records disagree on SOAP-1 at Main; the listing is above the figure to rely on and above the stock export's figure. Sellable to rely on 19. By location: Main 15 (limit SOAP-1), Annex 4 (limit CAND-1). On the stock export 21; on the lower of the two records 19. Pooled across locations 20; needs parts moved between locations. Listed: Web shop 25, total 25; over by 6.
- **GFT-TEA** Tea sampler. Conflict: the listing is above what can be built. Sellable to rely on 2. By location: Main 2 (limit TEA-B), Annex 0 (limit TEA-A, TEA-B and BOX-S, tied at 0). Listed: Web shop 12, Marketplace 6, total 18; over by 16.
- **GFT-TEAP** Tea duo. Sellable. Sellable to rely on 15. By location: Main 15 (limit TEA-A), Annex 0 (limit TEA-A and BOX-S, tied at 0). Listed: Web shop 15, total 15; matches.

**Conflicting stock records**

- **SOAP-1** Lavender soap bar, Main: stock export 40 on hand, 6 reserved; second record 36. Lower figure used: 36, available 30. Affects GFT-SPA. Check: count the shelf at Main; the stock lead decides which record is right.
- **MUG-1** Stoneware mug, Main: stock export 20 on hand, 0 reserved; second record 17. Lower figure used: 17, available 17. Affects GFT-HOME. Check: count the shelf at Main; the stock lead decides which record is right.

**Components shared by kits**

- **CAND-1** Soy candle: available 24 (Main 20, Annex 4). GFT-SPA 19 × 1 = 19 and GFT-HOME 8 × 2 = 16 need 35; short by 11. Left out: GFT-NEW, unresolved, also uses it; the shortfall may be larger. The planner decides how the stock is shared.
- **TEA-A** Tea blend A: available 30 (Main 30, Annex 0). GFT-TEA 2 × 3 = 6 and GFT-TEAP 15 × 2 = 30 need 36; short by 6. The planner decides how the stock is shared.

**Listings to correct**

- **GFT-SPA**, Web shop: listed 25; sellable 19, the lower of two stock records. Reduce the total to no more than 19, or hold the listing. Approved: ______________ Date: ________
- **GFT-TEA**, Web shop 12 and Marketplace 6: listed 18; sellable 2. Reduce the total to no more than 2, or hold the listing. Approved: ______________ Date: ________

**Questions for the stock lead**

1. GFT-NEW Winter tin set: component TIN-9 has no row in the stock export, and the kit is listed on the Web shop at 5. Is the code wrong in the definition, or has the tin not yet been set up in the stock system?
2. GFT-OLD is listed on the Web shop at 3 and has no kit definition. Is it a retired kit whose listing was left up, or a live kit whose definition is missing?

Draft for the inventory planner's decision. Nothing has been changed in the stock system, the store or any listing, and no customer has been told anything. Quantities are worked out from the files supplied, as of 10 November 2026.
