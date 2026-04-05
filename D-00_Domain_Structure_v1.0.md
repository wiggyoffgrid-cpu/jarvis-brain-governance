# D-00 â€” Jarvis Brain Domain Structure

**Version:** 1.0
**Status:** Active
**Created:** April 3, 2026
**Authority:** Wiggy (Eric Legault)

---

## Purpose

The Domain Structure defines the architectural framework of the Jarvis Brain. It establishes every domain the system manages and ensures that every file, card, script, config, and document can be mapped, cross-referenced, and navigated with precision.

Nothing in the Jarvis Brain stands alone. Every file belongs to a domain. Every domain connects through the D-Series Compass. If a file has no domain, it has no home â€” and homeless files are how systems rot.

---

## Authority Tiers

Every domain operates under one of four authority levels:

**TIER 1 â€” WIGGY ONLY (Sacred/Bloodline)**
Only Wiggy writes, modifies, or approves content. AI does not touch these domains without explicit instruction.

**TIER 2 â€” WIGGY AUTHORITY, AI ASSISTS (Business Critical)**
AI can draft, organize, and prepare â€” but Wiggy reviews and approves before anything is committed. Sensitive business data lives here.

**TIER 3 â€” AI OPERATIONAL (AI builds, Wiggy approves)**
AI workers can build, maintain, and update these domains. Wiggy audits periodically. Standard operational data.

**TIER 4 â€” SYSTEM (AI managed, Wiggy audits)**
AI manages these domains autonomously. Wiggy reviews when significant changes occur. Technical infrastructure and system internals.

---

## Domain Registry

### TIER 1 â€” WIGGY ONLY

**D-10 People & Family**
Wiggy's family tree, relationships, personal contacts. 76 XML people cards across 11 subfolders. Only Wiggy dictates family data. No AI writes, infers, or modifies relationship information.
Location: D:\Jarvis\brain\knowledge\people\

**D-11 Provisioner's Codex**
Reference link to the Codex book project. Content lives in the separate Provisioner's Codex Claude project, not in the Jarvis brain. Cross-reference only.
Location: E:\THE PROVISIONERS CODEX\

---

### TIER 2 â€” WIGGY AUTHORITY, AI ASSISTS

**D-12 Clients & CRM**
APE Canada clients â€” companies and individuals with ongoing equipment relationships managed by Wiggy. Tailored quotes, negotiated pricing, project-based engagement. 309 client XML cards across 113 company folders. Card format: <CLIENT> standard 11-field template.
Location: D:\Jarvis\brain\knowledge\APE\clients\

**D-13 APE Employees**
APE staff, coworkers, internal contacts across APE Canada and APE Global operations.
Location: TBD â€” not yet built

**D-14 Navision**
APE global ERP server. SACRED. Read-only until explicitly governed by Wiggy. No AI writes to Navision without direct authorization. Integration planned but not active.
Location: TBD â€” requires Navision access governance

**D-15 Access & Security**
Building codes, gate codes, alarm codes, keys, access credentials. Highly sensitive operational data.
Location: TBD â€” not yet built

**D-16 Tenants & Leases**
Office renters and bay renters at APE Nisku facility. Lease terms, payment schedules, contact information.
Location: TBD â€” not yet built

**D-17 Assets & Capital**
Company-owned assets, depreciation schedules, asset tracking, capital equipment registry.
Location: TBD â€” not yet built

---

### TIER 3 â€” AI OPERATIONAL

**D-20 APE Equipment**
APE product line â€” vibro hammers, impact hammers, drill systems, wick drains. Product XMLs, specifications, manuals, WEAP data, technical documentation. Equipment that APE sells and rents to clients.
Location: D:\Jarvis\brain\knowledge\APE\ (20 chunked XMLs)

**D-21 Wiggy Equipment**
Personal equipment — cabin tools, vehicles, generators, off-grid systems, farm equipment. Not APE inventory. 10 category folders, 1,336 files.
Location: D:\Jarvis\brain\knowledge\wiggy_equipment\

**D-22 Vendors & Suppliers**
Parts suppliers, service providers, manufacturer contacts, vendor relationships.
Location: TBD â€” not yet built

**D-23 Marketing**
Campaigns, materials, branding, website content, promotional assets.
Location: TBD â€” not yet built

**D-24 Parts & Inventory**
Parts stock, warehouse inventory, reorder points, stock levels.
Location: TBD â€” not yet built

**D-25 Equipment Fleet**
APE's own operational equipment â€” cranes, forklifts, yard equipment. Not products for sale â€” equipment APE uses internally.
Location: TBD â€” not yet built

**D-26 Fleet & Transport**
Company trucks, trailers, fuel tracking, licensing, inspections, transport logistics.
Location: TBD â€” not yet built

**D-27 Office & IT**
Server room, network infrastructure, computers, printers, IT systems.
Location: TBD â€” not yet built

**D-28 Facility Maintenance**
Building repairs, HVAC, electrical, plumbing â€” the physical APE Nisku facility.
Location: TBD â€” not yet built

**D-29 Shop Maintenance**
Shop floor, tools, welding equipment, fabrication systems, shop equipment maintenance.
Location: TBD â€” not yet built

**D-30 Yard Operations**
Yard layout, equipment storage staging, snow removal, yard management.
Location: TBD â€” not yet built

**D-31 Subscriptions & Licenses**
Software subscriptions, service accounts, renewal dates, license keys.
Location: TBD â€” not yet built

**D-32 Calendar & Schedules**
Events, birthdays, weddings (Kaci & Jeremy August 2026), deadlines, reminders, appointments. Both personal and business events in one domain with clear tagging.
Location: TBD â€” not yet built

---

### TIER 4 â€” SYSTEM

**D-40 Models & Inference**
Local model files, VRAM science, quantization records, LoRA adapters, model comparison data, inference parameters.
Location: D:\Jarvis\qlora\models\ and D:\Jarvis\qlora\output\

**D-41 Infrastructure & Config**
Flask app, llama-server, Docker, boot sequence, scripts, network config, system paths. The plumbing that makes Jarvis run.
Location: D:\Jarvis\ (various subdirectories)

**D-42 Knowledge & Extraction**
Extraction reports, chat history, session logs, Claude session archives, extracted knowledge across 8 categories.
Location: D:\Jarvis\brain\knowledge\extracted\ and D:\Jarvis\brain\Chat History\

**D-43 Governance & Planning**
Master Science Sheet, Strategic Planning, Task Lists, Command Library, Handoff documents, Ideas Vault. The documents that govern the project itself.
Location: D:\SCIENCE SHEET\, D:\Strategic Planning\, D:\Project Bin Files\

**D-44 Automation & Workers**
Koonie stable (Claude Code), Gordon stable, task templates, execution scripts, scheduled tasks, DockerBootSequence.
Location: H:\Koonie\, H:\Gordons Stable\, D:\Jarvis\scripts\

---

## Expansion Rules

- D-08: MCP Access Protocol (Active v1.0) — three-door access model, tier-based security
- D-09: Quote Engine Playbook (Active v1.0)
- D-MB: D-Master Build — Strategic Command Ledger (Active v1.0)
- D-18 through D-19: Reserved for future Tier 2 domains
- D-33 through D-39: Reserved for future Tier 3 domains
- D-45 through D-49: Reserved for future Tier 4 domains
- D-50 and above: Open for any future expansion
- Numbers are PERMANENT once assigned â€” never reuse, never insert between existing numbers
- New domains require: (1) domain classification, (2) authority tier assignment, (3) update to D-00, (4) update to D-02 Operational Index, (5) update to D-Master Build

---

## Purpose (Refined)

Nothing in the Jarvis Brain stands alone. Every file belongs to a domain, and every domain connects through the D-Series Compass â€” so any AI worker can move from "what do I have" to "where does it go" and from "what's broken" to "what fixes it", without guesswork.

---

*Written and governed by Wiggy. Maintained by the D-Series Compass.*
*"Care for what sustains you, and it will sustain you in return."*
