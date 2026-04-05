# D-09 — APE Quote Engine Playbook

**Version:** 1.0
**Status:** Active — IN DEVELOPMENT
**Created:** April 4, 2026
**Authority:** Wiggy (Eric Legault)

---

## Purpose

This doctrine governs the AI Quote Engine — the system that lets Wiggy dictate a quote by voice and have AI generate a professional, branded PDF document matching the Mason Excel workbook output format exactly.

---

## Architecture Overview

The Quote Engine is a 5-step pipeline:

1. **Identify product line** — vibro, impact, drill, or wick drain
2. **Look up client** — read the client card from `knowledge/APE/clients/[company]/wiggy_contacts/`
3. **Apply equipment rules** — read the product line rules XML to determine all required accessories
4. **Look up pricing** — read `sheet4_pricing.json` for monthly rent USD, MSRP, and weights
5. **Generate document** — run `generate_quote_v6.js` to produce docx, convert to PDF, apply watermark

---

## File Locations

| File | Path | Purpose |
|------|------|---------|
| Vibro rules | `knowledge/APE/quoting/vibro_quote_rules.xml` | 10 rules: stands, hose bundles, PU matching, clamps, beams, currency |
| Impact rules | `knowledge/APE/quoting/impact_quote_rules.xml` | 14 rules: diesel/hydraulic, drive cap system, leads, cushioning |
| Drill rules | `knowledge/APE/quoting/drill_quote_rules.xml` | 10 rules: standard drill, HD, DTH, CFA, polar penetrator |
| Wick drain rules | `knowledge/APE/quoting/wick_quote_rules.xml` | 10 rules: Nisha turnkey, crane-hung, consumables |
| Pricing database | `knowledge/APE/quoting/sheet4_pricing.json` | 46 categories, 1,127 items, all pricing/weights |
| Quote README | `knowledge/APE/quoting/QUOTE_ENGINE_README.md` | AI instructions for the 5-step workflow |
| Generator (v6) | `scripts/generate_quote_v6.js` | Node.js docx generator — flex-gap architecture |
| Watermark script | `scripts/add_watermark.py` | Python — adds faded ape behind PDF content |
| Logo (APE) | `scripts/logos/ape_bold.png` | APE screaming ape — bold, white background |
| Logo (J&M) | `scripts/logos/jm_final.png` | J&M Foundation Equipment |
| Logo (watermark) | `scripts/logos/logo-002.png` | Full-detail ape for PDF watermark overlay |

---

## Quote Format Rules — CRITICAL

These rules are NON-NEGOTIABLE. They come directly from Wiggy:

1. **NEVER show individual line item prices.** The quote is a PACKAGE. Show only the total monthly package rate. Showing per-item costs lets clients negotiate individual items — that's dangerous.
2. **ONE page maximum.** Every quote fits on a single page. The generator uses a flex-gap architecture to handle varying equipment list lengths.
3. **Hanging weight and shipping weight are REQUIRED.** Hanging weight = what hangs from the crane. Shipping weight = total package weight.
4. **Exchange rate is 1.37 (USD to CDN).** Always round up. This is hardcoded in the rules files.
5. **Currency conversion chain:** USD monthly x 1.37 = CDN monthly. CDN monthly / 3 = weekly. CDN monthly / 3 / 3 = daily (but daily is NOT shown on quotes — just weekly and monthly).
6. **Declared value = total MSRP of all equipment x exchange rate.**
7. **Hose bundle QTY = footage** (e.g., QTY 150 means 150 feet of hose bundle).

---

## Page Layout — Flex-Gap Architecture

The quote page is divided into two anchored blocks with a flex gap between them:

```
+------------------------------------------+
|  [LOGO LEFT]   TITLE/ADDRESS   [LOGO RT] |  <-- HEADER (top of page)
|  ----------------------------------------|
|  Client Name            Date              |
|  Company                                  |
|  Phone                                    |
|                                           |
|  Greeting + "I am Pleased to Offer..."    |
|                                           |
|  QTY  Description    Hanging Wt: [xxxxx]  |
|  QTY  Description    Shipping Wt: [xxxxx] |
|  QTY  Description                         |
|  QTY  Description                         |  <-- TOP BLOCK (equipment)
|  ...                                      |
|                                           |
|  ~~~~~~~~~ FLEX GAP ~~~~~~~~~~~~~~~~~~    |  <-- Shrinks as items are added
|  ~~~~~~~~~ (watermark lives here) ~~~~    |     Watermark fills this visually
|                                           |
|       [MONTHLY RENTAL RATE] [$xx,xxx]     |  <-- BOTTOM BLOCK (anchored)
|       [DECLARED VALUE]      [$x,xxx,xxx]  |
|                                           |
|  ***Daily rates only apply after 1 week** |
|  [WEEKLY CDN]  [MONTHLY CDN]              |
|  NOTES: $x,xxx   $xx,xxx                 |
|                                           |
|  TERMS & CONDITIONS                       |
|  (full T&C paragraph)                     |
|  ***Daily rates only apply...***          |
|                                           |
|  Eric Legault                             |
|  Canadian Regional Manager                |
|  587-988-3856   THIS QUOTE IS IN: CDN $   |  <-- SIGNATURE (page bottom)
+------------------------------------------+
```

**How the flex gap works:** The generator calculates the height of the top block (header + client + equipment) and the bottom block (rates + T&C + signature). The flex gap = page height - top - bottom. As equipment items are added, the flex gap shrinks. The watermark fills the gap visually.

---

## How to Generate a Quote

### Step 1: Build the JSON data file

```json
{
  "quoteType": "VIBRATORY HAMMER RENTAL QUOTE",
  "client": {
    "name": "Joel Day",
    "addressedAs": "Joel",
    "company": "Ledcor",
    "phone": "780-742-6696"
  },
  "lineItems": [
    {"qty": 1, "description": "200-6 Vibro"},
    {"qty": 150, "description": "200-6 Vibro HOSE BUNDLE"},
    {"qty": 1, "description": "800 Power Unit-Tier 4"},
    {"qty": 1, "description": "200-6 Vibro Stand"},
    {"qty": 1, "description": "8' Beam"},
    {"qty": 2, "description": "200 Caisson Clamp"}
  ],
  "hangingWeight": 25395,
  "shippingWeight": 48695,
  "monthlyTotal": 26715,
  "declaredValue": 1335750
}
```

To build this JSON:
- Read the client card for contact info
- Read the product line rules XML to determine all accessories
- Read `sheet4_pricing.json` to calculate: monthly total (sum all USD rates x 1.37), declared value (sum all MSRP x 1.37), weights (sum lbs)

### Step 2: Generate the docx

```bash
node generate_quote_v6.js output.docx quote_data.json
```

### Step 3: Convert to PDF

```bash
libreoffice --headless --convert-to pdf output.docx --outdir /output/dir/
```

### Step 4: Apply watermark

```bash
python3 add_watermark.py output.pdf output_final.pdf logos/logo-002.png 0.10
```

### Step 5: Save to mail cart

Copy the final PDF to `D:\Jarvis\brain\mail_cart\` for Wiggy to review.

---

## Equipment Rules — Quick Reference

### Vibratory Hammers
- Every vibro gets a stand (matched by model)
- Hose bundle: 150' standard, 200' for 400+ series
- PU matching: 150/200-6 → 800PU, 200-4 → 50PU, 400 → 1200PU-T4, etc.
- Clamps: 200 Caisson Clamp for standard, 400 Caisson Clamp for 400+ series
- Beam: sized by pile type/diameter

### Impact Hammers (Diesel + Hydraulic)
- Diesel trip size: D30-D180 = 4" trip, D250+ = 6" trip
- Diesel PU: D30→50PU, D50→51PU, D80→127PU, D180→127PU, D250→124PU-T4, D320→124PU-T4
- HIH PU: matched by energy rating
- Drive cap system: helmet (box/pipe) + insert + drive base + cushioning (micarta + aluminum) + striker plate
- Lead system: U-leads sized by pile diameter, headblock for fixed leads

### Drill Systems
- Standard drill PU: Model 12/20→260PU, 50/50BB→375PU, 75/80/100BB→475PU-T4
- HD drills: NO power unit (uses excavator hydraulics). Needs clamp, socket, hose kit, safety gate
- DTH: drill steel + DTH hammer + bit + sockets + swivel + ST75 leads
- CFA: flights + cutter head sized by pile diameter

### Wick Drains
- Nisha turnkey: DHJ-85 rig + 200 Wick Vibro + Type II leads + mandrel + consumables
- Crane-hung: 28/200 Wick Driver + ST75 leads
- Consumables (SALE, not rental): shoes, gaskets, PVD wick material

---

## Development Status

| Component | Status | Notes |
|-----------|--------|-------|
| vibro_quote_rules.xml | COMPLETE | Wiggy reviewed |
| impact_quote_rules.xml | COMPLETE | PU pairings need Wiggy verification |
| drill_quote_rules.xml | COMPLETE | PU pairings need Wiggy verification |
| wick_quote_rules.xml | COMPLETE | Wiggy's patent territory |
| sheet4_pricing.json | COMPLETE | 46 categories, 1,127 items |
| generate_quote_v6.js | IN PROGRESS | Flex-gap architecture working, logos TBD |
| add_watermark.py | COMPLETE | 10% opacity, behind content |
| APE logo | PENDING | Wiggy providing proper logo files |
| J&M logo | PENDING | Wiggy providing proper logo files |
| Voice-to-JSON pipeline | NOT STARTED | Wiggy dictates → AI builds JSON automatically |
| SALE quote format | NOT STARTED | Different layout for purchase quotes |

---

## Known Issues / Pending Fixes

1. **Logos** — Wiggy will provide proper logo files. Current extractions from PDF had quality issues.
2. **PU pairings** — Impact and drill power unit pairings are estimated from historical quotes. Wiggy needs to verify.
3. **SALE quotes** — Only RENTAL format is built. SALE format (from Mason's IMPACT PRINT, DRILL PRINT, WICK PRINT sheets) still needs to be built.
4. **Voice-to-JSON** — Currently the AI reads a dictated command and manually builds JSON. Needs automation.
5. **Wiggy's original dictated rules file** — He says it's somewhere on the Beast. Finding it would fill gaps.

---

*"Care for what sustains you, and it will sustain you in return." — Wiggy*
