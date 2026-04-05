# D-02 — Jarvis Brain Operational Index

**Version:** 1.1
**Status:** Active — Living Document
**Created:** April 3, 2026
**Updated:** April 4, 2026 (D-09 activated — Quote Engine Playbook v1.0)
**Authority:** Wiggy (Eric Legault)

---

## Purpose

The Operational Index is the single registry of every active doctrine, domain, file, and structural component in the Jarvis Brain. If it is not in this index, it does not officially exist. This is the navigational spine that maps everything to its domain.

---

## D-Series Governance Doctrines

| ID | Name | Version | Status |
|----|------|---------|--------|
| D-00 | Domain Structure | v1.0 | Active |
| D-01 | Governance Charter | v1.0 | Active |
| D-02 | Operational Index | v1.1 | Active |
| D-03 | Numbering Constitution | v1.0 | Active |
| D-04 | Navigation Spine | v1.0 | Active |
| D-05 | File Architecture | v1.0 | Active |
| D-06 | Revision Control | v1.0 | Active |
| D-07 | Folder Map | v1.0 | Active |
| D-08 | MCP Access Protocol | v1.0 | Active |
| D-09 | Quote Engine Playbook | v1.0 | Active |
| D-MB | D-Master Build — Strategic Command Ledger | v1.0 | Active |

---

## Tier 1 — Wiggy Only

| ID | Domain | Files | Status |
|----|--------|-------|--------|
| D-10 | People & Family | 76 XML cards, 15+ subfolders (includes split inlaws: parent_inlaws, sibling_inlaws, nephew_inlaws, future_inlaws) | Active |
| D-11 | Provisioner's Codex | Reference link only | Active — separate project |

---

## Tier 2 — Wiggy Authority, AI Assists

| ID | Domain | Files | Status |
|----|--------|-------|--------|
| D-12 | Clients & CRM | 309 XML cards, 113 company folders | Active |
| D-13 | APE Employees | 0 | Not yet built |
| D-14 | Navision | 0 | Not yet built — SACRED |
| D-15 | Access & Security | 0 | Not yet built |
| D-16 | Tenants & Leases | 0 | Not yet built |
| D-17 | Assets & Capital | 0 | Not yet built |

---

## Tier 3 — AI Operational

| ID | Domain | Files | Status |
|----|--------|-------|--------|
| D-20 | APE Equipment | 20 chunked XMLs | Active |
| D-21 | Wiggy Equipment | Active — 10 category folders, 1,336 files | Active |
| D-22 | Vendors & Suppliers | 0 | Not yet built |
| D-23 | Marketing | 0 | Not yet built |
| D-24 | Parts & Inventory | 0 | Not yet built |
| D-25 | Equipment Fleet | 0 | Not yet built |
| D-26 | Fleet & Transport | 0 | Not yet built |
| D-27 | Office & IT | 0 | Not yet built |
| D-28 | Facility Maintenance | 0 | Not yet built |
| D-29 | Shop Maintenance | 0 | Not yet built |
| D-30 | Yard Operations | 0 | Not yet built |
| D-31 | Subscriptions & Licenses | 0 | Not yet built |
| D-32 | Calendar & Schedules | 0 | Not yet built |

---

## Tier 4 — System

| ID | Domain | Files | Status |
|----|--------|-------|--------|
| D-40 | Models & Inference | 6 model files, LoRA v13, training data | Active |
| D-41 | Infrastructure & Config | Flask, llama-server b8639, Docker, Dashboard, acks, voices, searxng, scripts | Active |
| D-42 | Knowledge & Extraction | 8 category folders + Claude sessions report, chat history | Active |
| D-43 | Governance & Planning | D-Series Compass, Ideas Vault, Handoff docs | Active |
| D-44 | Automation & Workers | Mason (Docker Claude), Koonie stable (Claude Code), Gordon stable, scripts | Active |
| D-45 | Archives & Retired | 8 archive subfolders with manifest — legacy, modelfiles, extraction tests, old knowledge, reference, legacy UI, root scripts | Active |

---

## Changes Log — v1.3 (April 4, 2026)

- D-09 activated: Quote Engine Playbook v1.0 (AI quote generation pipeline — vibro, impact, drill, wick drain)
- Files at: knowledge/APE/quoting/ (4 rules XMLs, pricing JSON, generator JS, watermark PY, README)
- Cross-reference updated to include D-09

## Changes Log — v1.2 (April 4, 2026)

- D-08 activated: MCP Access Protocol v1.0 (three-door access model, tier-based security, tunnel/MCP/Flask)
- D-Master Build added: Strategic Command Ledger v1.0 (Third Authority — tracks all 26 domains with strategic status)
- D-41 note: Brain server (jarvis_brain_server.py), Cloudflare tunnel (config.yml), startup script (JARVIS_BRAIN_STARTUP.ps1) now live
- Cross-reference updated to include D-Master Build

## Changes Log — v1.1

- Added D-07 Folder Map (v1.0)
- Added D-45 Archives & Retired domain
- D-12 updated: 309 cards (was 316), 113 folders (was 121)
- Merged: peter_kiewit_sons_ulc into kiewit, dybamic_global into dynamic_global, ppm into pacific_pile_and_marine, vancouver_piledrivingcarlson + carlson_construction_group into vancouver_piledriving, formula into formula_contractors, west_shore_constructors into westshore_constructors
- Deleted: subsurface_corp (all duplicates of subsurface_construction)
- D-10 updated: inlaws folder split into parent_inlaws, sibling_inlaws, nephew_inlaws, future_inlaws
- D-10 updated: all relationship fields renamed to "primary first, qualifier after hyphen" format (30 cards)
- D-12 updated: all phone numbers standardized to dash format, 3 cards enriched (Peter Cabral, Ryan Beers, Jun Sohn)
- D-44 updated: Mason documented as Docker Claude worker with scripts, playbooks, and task system
- D-21 updated: 10 equipment categories confirmed on disk
- Archived: Legacy, modelfiles, extracted_claude_test, knowledge archives, reference, jarvis-ui, root scripts
- Nuked: Members Of The Royal Court, __pycache__

---

## Index Rules

1. Every active file must appear in this index under its domain
2. This index is updated every time a new file is created or retired
3. File counts are verified periodically against actual disk contents
4. If a file exists on disk but not in this index, it is unregistered — flag and classify it
5. If a file appears in this index but not on disk, it is missing — investigate and resolve

---

## Cross-Reference

This index maps to:
- D-00 Domain Structure (domain definitions and tiers)
- D-07 Folder Map (physical disk locations)
- D-09 Quote Engine Playbook (AI quote generation pipeline)
- D-Master Build (strategic command ledger)

All three must agree. Discrepancy = invalid state.

---

*"If it is not in the index, it does not exist."*
