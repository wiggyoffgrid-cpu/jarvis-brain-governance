# D-04 â€” Jarvis Brain Navigation Spine

**Version:** 1.1
**Status:** Active
**Created:** April 3, 2026
**Updated:** April 5, 2026 (added D-07, D-08, D-09, D-Master Build to governance layer; added D-09 and D-08 connections)
**Authority:** Wiggy (Eric Legault)

---

## Purpose

The Navigation Spine is the structural backbone of the Jarvis Brain. It defines how every doctrine, domain, card, script, and config file interconnects without contradiction, duplication, or structural drift.

---

## Core Directives

1. Every file must map to a primary domain (D-10 through D-44)
2. Every active file must be indexed in D-02 Operational Index
3. Every cross-reference must be bidirectional â€” if A points to B, B points to A
4. No file may exist without a defined structural purpose
5. Expansion must follow D-03 Numbering Constitution
6. Redundancy without purpose is prohibited

---

## Cross-Reference Map

### Governance Layer (D-00 through D-09 + D-Master Build)
- D-00 Domain Structure defines WHAT domains exist
- D-01 Governance Charter defines WHO has authority and HOW changes are made
- D-02 Operational Index defines WHERE everything is and its current state (Registry — Authority 2)
- D-03 Numbering Constitution defines HOW things are numbered
- D-04 Navigation Spine (this document) defines HOW everything connects
- D-05 File Architecture defines HOW files are named and organized
- D-06 Revision Control defines HOW versions are managed
- D-07 Folder Map defines WHAT physically exists on disk (Physical Truth — Authority 1)
- D-08 MCP Access Protocol defines HOW AIs connect to the brain (three doors, tier security)
- D-09 Quote Engine Playbook defines HOW AI generates APE quotes (voice-to-PDF pipeline)
- D-Master Build defines the STRATEGIC LEDGER — what's planned, active, retired, who owns what, what depends on what (Strategic — Authority 3)

**Three Authorities Rule:** D-07 (physical truth) + D-02 (registry) + D-Master Build (strategic) must all agree. Any disagreement = invalid state.

### Domain Connections
- D-10 People & Family connects to D-12 Clients (some clients are personal contacts)
- D-12 Clients & CRM connects to D-20 APE Equipment (quotes reference equipment)
- D-12 Clients & CRM connects to D-09 Quote Engine (clients are the recipients of generated quotes)
- D-12 Clients & CRM connects to D-14 Navision (account data)
- D-13 APE Employees connects to D-27 Office & IT (workstations, access)
- D-20 APE Equipment connects to D-09 Quote Engine (equipment is the subject of quotes — vibro, impact, drill, wick drain)
- D-20 APE Equipment connects to D-24 Parts & Inventory (parts for equipment)
- D-25 Equipment Fleet connects to D-29 Shop Maintenance (fleet servicing)
- D-26 Fleet & Transport connects to D-30 Yard Operations (vehicle staging)
- D-40 Models & Inference connects to D-41 Infrastructure (server configs)
- D-43 Governance connects to ALL domains (governance applies everywhere)

### Infrastructure & Access Connections
- D-08 MCP Access Protocol connects to D-41 Infrastructure (MCP filesystem server, Cloudflare tunnel, Flask — the three doors)
- D-08 MCP Access Protocol connects to D-44 Automation & Workers (Cowork projects, Dispatch, Claude Code all reach the brain through MCP)
- D-09 Quote Engine connects to D-41 Infrastructure (generate_quote_v6.js, add_watermark.py, pricing JSON live in brain\knowledge\APE\quoting\)
- D-09 Quote Engine connects to D-40 Models & Inference (local models assist quote generation via Flask)

### Jigsaw Integration
- D-10 People cards are injected via people_index.py
- D-12 Client cards are injected via client lookup in Flask
- D-20 APE Equipment is injected via ape_index.py
- Future domains will get their own index files following the same pattern

---

## Structural Integrity Mandate

All additions to the Jarvis Brain must reinforce clarity, structural mapping, and navigational coherence. Redundancy without purpose is prohibited. Expansion must increase precision, not noise.

If you cannot explain why a file exists and which domain it belongs to, the file should not exist.

---

*"Every file maps to a domain. Every domain connects through the spine. Nothing floats homeless."*
