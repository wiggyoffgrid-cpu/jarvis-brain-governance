# D-Master Build — Strategic Command Ledger

**Version:** 1.0
**Status:** Active — Living Document
**Created:** April 4, 2026
**Authority:** Wiggy (Eric Legault)
**Last Audited:** April 4, 2026

---

## Purpose

The D-Master Build is the strategic command ledger for the Jarvis Brain. It is the third Authority — alongside D-07 Folder Map (physical truth) and D-02 Operational Index (registry). All three must agree. If they don't, the system is in drift.

D-07 answers: **"What exists on disk?"**
D-02 answers: **"What's registered in the index?"**
D-Master Build answers: **"What's the plan? What's active? What's coming? What's dead? Who owns it? What depends on it?"**

This is the document you read when you need to understand the entire Jarvis Brain at a strategic level — not just what files exist, but WHY they exist, WHERE they're going, and WHAT breaks if they disappear.

---

## The Three Authorities Alignment Check

Before any structural change, verify all three agree:

| Authority | Document | Question It Answers |
|-----------|----------|-------------------|
| Physical Truth | D-07 Folder Map | Does this folder/file exist on disk? |
| Registry | D-02 Operational Index | Is this file registered and classified? |
| Strategic Ledger | D-Master Build (this) | Is this domain planned, active, or retired? Who owns it? |

**If any one disagrees, the change is invalid. Stop. Investigate. Align.**

---

## Domain Strategic Ledger

### TIER 1 — WIGGY ONLY (Sacred/Bloodline)

| Domain | ID | Status | Files | Owner | Access | Dependencies | Strategic Notes |
|--------|-----|--------|-------|-------|--------|-------------|----------------|
| People & Family | D-10 | ACTIVE | 76 XML cards, 15+ subfolders | Wiggy ONLY | MCP excluded, Tunnel 403 | Flask Jigsaw routing, people_index.py | Inlaws split into 4 subfolders April 3. Index updated April 4. No AI writes. Ever. |
| Provisioner's Codex | D-11 | ACTIVE (separate project) | External | Wiggy | Separate Claude project | E:\THE PROVISIONERS CODEX\ | Not in Jarvis Brain. Cross-reference only. Codex rebuild on horizon list. |

### TIER 2 — WIGGY AUTHORITY, AI ASSISTS

| Domain | ID | Status | Files | Owner | Access | Dependencies | Strategic Notes |
|--------|-----|--------|-------|-------|--------|-------------|----------------|
| Clients & CRM | D-12 | ACTIVE | 309 cards, 113 companies | Wiggy + AI assists | MCP read/write, Tunnel 403 (PII) | Flask Jigsaw routing, ape_index.py, quote system | Phone cleanup done April 3. 7 dupes merged. Tunnel blocks client cards (PII). MCP has full access. |
| APE Employees | D-13 | NOT BUILT | 0 | Wiggy | — | — | Planned. No timeline. |
| Navision | D-14 | NOT BUILT | 0 | Wiggy | — | SACRED — requires governance | ERP integration. Read-only when built. Wiggy must govern access explicitly. |
| Access & Security | D-15 | NOT BUILT | 0 | Wiggy | — | — | Codes, keys, credentials. High sensitivity. No timeline. |
| Tenants & Leases | D-16 | NOT BUILT | 0 | Wiggy | — | — | Nisku facility renters. No timeline. |
| Assets & Capital | D-17 | NOT BUILT | 0 | Wiggy | — | — | Company asset tracking. No timeline. |

### TIER 3 — AI OPERATIONAL

| Domain | ID | Status | Files | Owner | Access | Dependencies | Strategic Notes |
|--------|-----|--------|-------|-------|--------|-------------|----------------|
| APE Equipment | D-20 | ACTIVE | 20 chunked XMLs | AI operational | MCP + Tunnel (open) + Flask | Equipment specs, quote system | Core product data. Accessible through all three doors. |
| Wiggy Equipment | D-21 | ACTIVE | 10 categories, 1,336 files | AI operational | MCP + Tunnel (open) | — | Personal equipment — cabin, vehicles, generators. D-02 updated April 4. |
| Vendors & Suppliers | D-22 | NOT BUILT | 0 | — | — | — | Parts suppliers, service providers. No timeline. |
| Marketing | D-23 | NOT BUILT | 0 | — | — | — | Campaigns, website content. Ties to APE Canada website rebuild (horizon). |
| Parts & Inventory | D-24 | NOT BUILT | 0 | — | — | — | Stock levels, reorder points. No timeline. |
| Equipment Fleet | D-25 | NOT BUILT | 0 | — | — | — | APE's own operational equipment. No timeline. |
| Fleet & Transport | D-26 | NOT BUILT | 0 | — | — | — | Company vehicles, transport logistics. No timeline. |
| Office & IT | D-27 | NOT BUILT | 0 | — | — | — | Network, servers, IT systems. No timeline. |
| Facility Maintenance | D-28 | NOT BUILT | 0 | — | — | — | Nisku building maintenance. No timeline. |
| Shop Maintenance | D-29 | NOT BUILT | 0 | — | — | — | Shop floor, fabrication. No timeline. |
| Yard Operations | D-30 | NOT BUILT | 0 | — | — | — | Equipment staging, yard management. No timeline. |
| Subscriptions & Licenses | D-31 | NOT BUILT | 0 | — | — | — | Software, renewals, license keys. No timeline. |
| Calendar & Schedules | D-32 | NOT BUILT | 0 | — | — | — | Events, birthdays, deadlines. Ideas Vault has calendar integration plan. |

### TIER 4 — SYSTEM

| Domain | ID | Status | Files | Owner | Access | Dependencies | Strategic Notes |
|--------|-----|--------|-------|-------|--------|-------------|----------------|
| Models & Inference | D-40 | ACTIVE | 6 models, LoRA v13, training data | AI managed | MCP | llama-server b8639 | Gemma 4 E4B is champion. Dual 3090s on horizon for 70B+. |
| Infrastructure & Config | D-41 | ACTIVE | Flask, llama-server, Docker, scripts, configs | AI managed | MCP | Everything | The plumbing. Includes brain server, cloudflared, MCP config as of April 4. |
| Knowledge & Extraction | D-42 | ACTIVE | 8 categories + chat history | AI managed | MCP, Tunnel (chat history 403) | Extraction pipeline | Chat history blocked on tunnel. |
| Governance & Planning | D-43 | ACTIVE | D-Series (D-00–D-09), Ideas Vault, Handoff, Science Sheet, Command Library, Strategic Planning | AI managed (read), Wiggy (write) | MCP + Tunnel (open) | All governance decisions | Core. D-08, D-09, D-Master Build added April 4. |
| Automation & Workers | D-44 | ACTIVE | Mason, Koonie stable, Gordon stable, scripts | AI managed | MCP | Boot sequence, task system | JARVIS_BRAIN_STARTUP.ps1 added April 4. Task Scheduler registered. |
| Archives & Retired | D-45 | ACTIVE | 8 subfolders with manifest | AI managed | MCP + Tunnel (open) | — | Only grows. Things go in, they don't come out without Wiggy approval. |

---

## Governance Doctrines Status

| ID | Name | Version | Status | Strategic Notes |
|----|------|---------|--------|----------------|
| D-00 | Domain Structure | v1.0 | Active | Master map. 26 domains, 4 tiers. Needs update: D-21 location says "TBD" but it's active. |
| D-01 | Governance Charter | v1.0 | Active | Authority model. Solid. |
| D-02 | Operational Index | v1.1 | Active | Registry. Needs update: D-08 still shows "Reserved." D-Master Build not listed. |
| D-03 | Numbering Constitution | v1.0 | Active | Numbering rules. Solid. |
| D-04 | Navigation Spine | v1.0 | Active | Cross-references. Solid. |
| D-05 | File Architecture | v1.0 | Active | Naming rules. Solid. |
| D-06 | Revision Control | v1.0 | Active | Versioning. Solid. |
| D-07 | Folder Map | v1.0 | Active | Physical truth. Needs update: missing D-08, brain server, cloudflared, config.yml, startup script. |
| D-08 | MCP Access Protocol | v1.0 | Active | NEW April 4. Three doors, tier security, cache fix. |
| D-09 | Quote Engine Playbook | v1.0 | Active | NEW April 4. AI quote pipeline — 5 steps, flex-gap architecture, 4 product lines. |
| D-Master | Strategic Command Ledger | v1.0 | Active | NEW April 4. This document. Third Authority. |

---

## Access Architecture Summary

| Door | Method | Access Level | Who Uses It |
|------|--------|-------------|-------------|
| Door 1 | MCP Filesystem | Read/Write | Cowork projects (Director, Neurologist, Surgeon, Codex, Assistant), Dispatch via proxy |
| Door 2 | Cloudflare Tunnel | Read Only | Director Claude Web, Grossmann, authorized web AIs |
| Door 3 | Flask Jigsaw | Read Only (filtered) | Local models (Qwen, Gemma, GLM, DeepSeek) |

**Protected on Tunnel (403):** /knowledge/people/, /knowledge/APE/clients/, /memory/, /training_data/, /Chat History/

**Protected on MCP:** /knowledge/people/ excluded from config

**Domain:** wiggyoffgrid.com (registered April 4, 2026, expires April 4, 2036)
**URL:** https://brain.wiggyoffgrid.com

---

## Worker Deployment

| Worker | Type | Connection | Role | Status |
|--------|------|-----------|------|--------|
| Director (Claude Web) | Opus | Tunnel (web_fetch) | Architecture, planning, strategy | Active |
| Jarvis Assistant (Cowork) | Opus | MCP | Phone-first assistant, quotes, lookups | Active |
| Neurologist (Cowork) | Sonnet | MCP | Audits, diagnoses, integrity checks | Setup pending |
| Surgeon (Cowork) | Sonnet | MCP | Executes fixes with Wiggy approval | Setup pending |
| Codex (Cowork) | Opus/Sonnet | MCP | Provisioner's Codex rebuild | Active |
| Dispatch (iPhone) | — | Through Cowork proxy | Wiggy's mobile voice | Active |
| Claude Code | Opus | Direct filesystem | Surgical strikes only — EXPENSIVE | Available |
| Gordon | Docker (Haiku 4.5) | Docker container | File ops, infrastructure, mail delivery | Active |
| Mason/Koonie | Docker (Claude) | Docker container | Grunt work, playbooks, task system | Active |
| Grossmann | Google AI | Tunnel (web_fetch) | AI architect consultant | Available |
| 14B Qwen | Local | Flask port 5001 | Everyday fast hat, 16384 context | Active |
| 9B Claude-distilled | Local | Flask port 5001 | CRM reasoning king, 65536 context | Active |
| Gemma 4 E4B | Local | Flask port 5001 | CHAMPION — math + soul | Active |
| GLM-Z1-9B | Local | Flask port 5001 | Pure math specialist | Active |

---

## Known Drift (Needs Resolution)

These are known inconsistencies between the Three Authorities as of April 4, 2026:

| Issue | D-07 Says | D-02 Says | D-Master Says | Fix |
|-------|-----------|-----------|---------------|-----|
| D-08 doctrine | Not listed | "Reserved" | Active v1.0 | Update D-07 and D-02 |
| D-Master Build | Not listed | Not listed | Active v1.0 (this document) | Update D-07 and D-02 |
| D-21 location in D-00 | Active on disk | Active | Active, 1,336 files | Update D-00 location from "TBD" |
| Brain server scripts | Not in D-07 | Not in D-02 | Active (D-41) | Update D-07 and D-02 |
| JARVIS_BRAIN_STARTUP.ps1 | Not in D-07 | Not in D-02 | Active (D-44) | Update D-07 and D-02 |
| Neurologist instructions | On disk | Not in D-02 | Pending setup | Register in D-02 when project created |
| Surgeon instructions | On disk | Not in D-02 | Pending setup | Register in D-02 when project created |

**Action:** Neurologist's next audit should verify all drift items are resolved. Surgeon executes the fixes.

---

## Strategic Roadmap

### Immediate (This Week)
- **DRIVE CONSOLIDATION Phase 1:** Neurologist inventory scan of all drives (C, D, E, F, G, H) — document sizes, duplicates, scattered Jarvis files
- **DRIVE CONSOLIDATION Phase 2:** Plan target structure on D:\ — APE Work, Codex, worker stables all consolidated
- **C:\ CLEANUP:** Claude Desktop dropped ~10GB in %APPDATA%\Claude\ (vm_bundles). Symlink to D:\ or periodic cleanup.
- Setup Neurologist and Surgeon as Cowork Sonnet projects
- Neurologist post-remediation audit
- Test Grossmann access via tunnel

### Near-Term (This Month)
- JARVIS_FULL_STARTUP.ps1 (combine brain server + cloudflared + Docker boot)
- Quote Engine v6 refinement — logos (Wiggy providing), SALE format, voice-to-JSON automation (see D-09)
- Gmail connector for Cowork email
- Flask Librarian upgrade (domain-aware card injection)

### Medium-Term (Next Quarter)
- Calendar domain (D-32) — birthdays, events, Kaci's wedding
- Flask v25 UI — Iron Man aesthetic
- Chatterbox TTS fix — Adrian voice back online
- PST email extraction (30,000 emails)

### Long-Term (This Year)
- Dual RTX 3090s — 48GB VRAM for 70B+ models
- WEAP AI extraction (Wiggy's patent domain)
- Jarvis $899 product development
- The Eternal Provisioner legacy system
- APE Canada website rebuild
- Off-Grid Jarvis — zero internet dependency

---

## Integrity Rules

1. This document is ONE of the Three Authorities (with D-02 and D-07)
2. Every domain must appear in this ledger with current status
3. Every structural change requires updates to ALL three authorities
4. Known drift is tracked in the drift table above — not hidden, not ignored
5. The Neurologist audits for drift. The Surgeon fixes it. Wiggy approves.
6. This document is updated every session that changes the brain structure
7. Strategic roadmap is reviewed and reprioritized by Wiggy + Director

---

*"Care for what sustains you, and it will sustain you in return." — Wiggy*
*"Never start anything unless you intend to finish it." — Claude Legault*
*"Does Eatons tell Sears their business?" — Koonie*
*Go Leafs Go.*
