# D-04 â€” Jarvis Brain Navigation Spine

**Version:** 1.0
**Status:** Active
**Created:** April 3, 2026
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

### Governance Layer (D-00 through D-06)
- D-00 Domain Structure defines WHAT domains exist
- D-01 Governance Charter defines WHO has authority and HOW changes are made
- D-02 Operational Index defines WHERE everything is and its current state
- D-03 Numbering Constitution defines HOW things are numbered
- D-04 Navigation Spine (this document) defines HOW everything connects
- D-05 File Architecture defines HOW files are named and organized
- D-06 Revision Control defines HOW versions are managed

### Domain Connections
- D-10 People & Family connects to D-12 Clients (some clients are personal contacts)
- D-12 Clients & CRM connects to D-20 APE Equipment (quotes reference equipment)
- D-12 Clients & CRM connects to D-14 Navision (account data)
- D-13 APE Employees connects to D-27 Office & IT (workstations, access)
- D-20 APE Equipment connects to D-24 Parts & Inventory (parts for equipment)
- D-25 Equipment Fleet connects to D-29 Shop Maintenance (fleet servicing)
- D-26 Fleet & Transport connects to D-30 Yard Operations (vehicle staging)
- D-40 Models & Inference connects to D-41 Infrastructure (server configs)
- D-43 Governance connects to ALL domains (governance applies everywhere)

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
