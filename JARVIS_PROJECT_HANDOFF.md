# PROJECT JARVIS — SESSION HANDOFF

**Updated:** April 4, 2026 (end of session — all governance docs, handoffs, and memory aligned)
**Previous session:** April 4, 2026 (evening — infrastructure buildout + quote engine start)
**Authority:** Wiggy (Eric Legault)

---

## WHAT THIS PROJECT IS

Jarvis is a fully private local AI assistant running on WIGGYS-BEAST. No cloud dependency. No API keys for inference. Everything runs local — even off-grid at the cabin in northern Ontario on Starlink.

The system uses three layers: system prompt (facts), LoRA v13 (personality), and Jigsaw XML injection (relationships/data). Flask on port 5001 assembles the context, llama-server on port 8080 runs inference, Chatterbox TTS on port 8004 provides voice output.

---

## GOVERNANCE — D-SERIES COMPASS

The Jarvis Brain is governed by the D-Series Compass. Nine governance doctrines are active:

| Doc | Name | Version | Purpose |
|-----|------|---------|---------|
| D-00 | Domain Structure | v1.0 | Master map of all 26 domains across 4 authority tiers |
| D-01 | Governance Charter | v1.0 | Authority model, standing orders, Three Authorities rule |
| D-02 | Operational Index | v1.3 | Registry of every active file, card, and component |
| D-03 | Numbering Constitution | v1.0 | Permanent numbering rules, reserved ranges |
| D-04 | Navigation Spine | v1.0 | How everything cross-references and connects |
| D-05 | File Architecture | v1.0 | Naming rules, folder structure, card templates |
| D-06 | Revision Control | v1.0 | Versioning, lock sequence, backup rules |
| D-07 | Folder Map | v1.0 | Physical truth of what exists on disk |
| D-08 | MCP Access Protocol | v1.0 | How AIs connect to the Jarvis Brain — MCP, tunnel, tiers — NEW April 4 |
| D-09 | Quote Engine Playbook | v1.0 | AI Quote Engine — voice-to-PDF quote generation — NEW April 4 |

**D-Master Build** (Strategic Command Ledger v1.0) — the third Authority — created April 4. Tracks all 26 domains with strategic status, worker deployment, access architecture, and roadmap.

**The Three Authorities Rule:** No structural change is valid unless reflected in all three: D-07 Folder Map (physical truth), D-02 Operational Index (registry), and D-Master Build (strategic ledger). If any one doesn't match, the change is invalid.

**Location on disk:** D:\Jarvis\brain\governance\D-Series\

---

## MULTI-PROJECT SYSTEM — NEW THIS SESSION

### Project Roster

| Project | Role | Model | Purpose |
|---------|------|-------|---------|
| **Project Jarvis** | Director | Opus 4.6 | Architecture, planning, strategy, D-series governance |
| **Jarvis Brain Neurologist** | Inspector | Sonnet 4.6 | Scans, audits, diagnoses. Read-only. Never touches files. |
| **Jarvis Brain Surgeon** | Operator | Sonnet 4.6 | Executes fixes with Wiggy approval. Pre-op/post-op reports. |
| **The Provisioners Codex** | Book Project | Opus/Sonnet | Codex rebuild — separate project |
| **Project Jarvis Assistant** | Assistant | Opus 4.6 | Phone-first personal assistant — quotes, lookups, lists. NEW April 4 |

### Communication System — MCP + Mail Cart + Cloudflare Tunnel

**MCP Filesystem Server (NEW April 4):**
- All Cowork projects connect directly to D:\Jarvis\brain\ via MCP filesystem server
- Config at: %APPDATA%\Claude\claude_desktop_config.json
- NO MORE PROJECT BINS for file sharing — the disk IS the bin
- Dispatch (iPhone) reads/writes through active Cowork session on Beast

**Cloudflare Tunnel (NEW April 4):**
- Domain: wiggyoffgrid.com (registered April 4, 2026, expires April 4, 2036)
- URL: https://brain.wiggyoffgrid.com (permanent named tunnel)
- Server: jarvis_brain_server.py on localhost:8009 (read-only)
- Any AI with web_fetch can read the Jarvis Brain via this URL
- Director Claude Web and Grossmann use this path
- Tier 1 protection: /knowledge/people/ returns 403

**Mail Cart (still active):**
- Location: D:\Jarvis\brain\mail_cart\
- Protocol: Files named TO_[DESTINATION]_description_YYYYMMDD.md
- Now shared via MCP — all Cowork projects can read/write directly
- Rule: Wiggy is the mail carrier. All relay goes through him.

### Assembly Line (proven this session)
1. Neurologist scans and produces audit report
2. Wiggy reviews findings and makes decisions
3. Neurologist produces surgical orders
4. Wiggy relays to Surgeon
5. Surgeon builds pre-op plan (dry run)
6. Wiggy approves
7. Surgeon executes and produces post-op report
8. Surgeon flags governance updates back to Project Jarvis
9. Project Jarvis updates D-02/D-07
10. Neurologist runs post-remediation audit

### Key Documents in Project Bins

**Neurologist:** D-02 v1.1, D-05 v1.0, D-07 v1.0, Inter-Project Task Template, Output Hygiene Rules
**Surgeon:** Science Sheet v2, New Discovery Form, Inter-Project Task Template, Output Hygiene Rules
**All projects:** SERVICE_BULLETIN_MAIL_CART.md

### Audit Log System
**Location:** D:\Jarvis\brain\governance\audit_logs\
**Contents:** OUTPUT_HYGIENE_RULES.md, SURGEON_POSTOP_20260403_01.md, SURGEON_POSTOP_20260403_02.md
**Rule:** All reports saved as downloadable files, deployed to audit_logs, Downloads cleaned after delivery.

---

## CURRENT STATE — WHAT'S BUILT

### Knowledge Base (Jigsaw XML Injection)
- **76 people cards** — D-10, across 15+ subfolders at D:\Jarvis\brain\knowledge\people\
- **309 client cards** — D-12, across 113 company folders at D:\Jarvis\brain\knowledge\APE\clients\
- **20 APE equipment XMLs** — D-20, chunked from manuals at D:\Jarvis\brain\knowledge\APE\
- **8 extraction categories** — D-42, at D:\Jarvis\brain\knowledge\extracted\
- **10 wiggy equipment categories** — D-21, at D:\Jarvis\brain\knowledge\wiggy_equipment\

### People Card Structure (Updated This Session)
Inlaws folder split into 4 subfolders:
- inlaws\parent_inlaws\ (2 cards — Bob Barnes, Janet Barnes)
- inlaws\sibling_inlaws\ (2 cards — Julie Legault, Serge Cote)
- inlaws\nephew_inlaws\ (3 cards — Mikey Poirier, Noah Thibert, Pat Goulard)
- inlaws\future_inlaws\ (2 cards — Brook St-Martin, Jeremy Lahti)

**Relationship field format:** "Primary first, qualifier after hyphen"
- Uncle-maternal, Aunt-paternal, Nephew-great, Niece-great
- Nephew-in-law, Nephew-in-law-future, Brother-in-law-ex
- 30 cards renamed this session

### Client Card Cleanup (This Session)
- All 316→309 phones standardized to dash format (260 already clean, 45 fixed, 7 dupes removed)
- 3 cards enriched: Peter Cabral (phone, title, address), Ryan Beers (phone, title, email, address), Jun Sohn (title, company phone, address)
- 7 duplicate company folders merged:
  - peter_kiewit_sons_ulc → kiewit (Yaodong Yu dupe deleted)
  - dybamic_global → dynamic_global (typo fixed, Ian Purvis past company added)
  - ppm → pacific_pile_and_marine
  - vancouver_piledrivingcarlson + carlson_construction_group → vancouver_piledriving
  - formula → formula_contractors (Chris Cleave)
  - west_shore_constructors → westshore_constructors
  - subsurface_corp deleted (all 3 cards were dupes of subsurface_construction)

### Models on Disk
- **14B Qwen2.5-Instruct Q6_K** (11.29GB) — everyday hat, 16384 context CONFIRMED
- **9B Qwen3.5-Claude-Distilled Q6_K** (6.85GB) — CRM hat, 65536 context
- **Gemma 4 E4B Q6_K** (6.59GB) — CHAMPION: math + soul, 8206 MiB VRAM, 131072 context max
- **GLM-Z1-9B Q6_K** (8.27GB) — pure math champion, 10100 MiB VRAM
- **DeepSeek-R1-14B Q6_K** (12.1GB) — think-loop model

### Infrastructure
- Flask: D:\Jarvis\jarvis_flask.py (port 5001) — v24.3
- llama-server: D:\Jarvis\llama.cpp\llama-server.exe (port 8080) — build b8639
- Chatterbox TTS: Docker container (port 8004) — Adrian voice — CURRENTLY BROKEN
- Jarvis Brain Server: D:\Jarvis\scripts\jarvis_brain_server.py (port 8009) — read-only HTTP, Tier 1 protected — NEW April 4
- Cloudflare Tunnel: D:\Jarvis\scripts\cloudflared.exe — named tunnel "jarvis-brain" — NEW April 4
- Tunnel config: D:\Jarvis\scripts\config.yml — permanent tunnel config
- MCP Server: @modelcontextprotocol/server-filesystem via Node.js — config at %APPDATA%\Claude\claude_desktop_config.json — NEW April 4
- Boot: DockerBootSequence.ps1 — 19 second auto-start
- Docker fix script: D:\Jarvis\scripts\fix_docker.ps1
- Koonie stable: H:\Koonie\ (Claude Code task-file launcher)
- Gordon stable: H:\Gordons Stable\
- Mason: D:\Jarvis\Mason\ (Docker Claude, 20+ playbooks, inbox/outbox task system)

---

## BEAST DISK STATUS — POST CLEANUP

### D:\Jarvis\ Root (CLEAN)
12 folders, 3 files. No debris. No orphans.
- Folders: acks, brain, Dashboard, llama.cpp, llama.cpp.backup, logs, Mason, qlora, scripts, searxng, uploads, voices
- Files: jarvis_flask.py, system_prompt_v13.txt, DockerBootSequence.ps1

### D:\Jarvis\brain\ (CLEAN)
Zero loose files in root. Subfolders only:
- governance\ (D-Series\, audit_logs\, + 3 operational docs)
- knowledge\ (people\, APE\, extracted\, wiggy_equipment\, wiggy_personal\)
- Chat History\
- Ideas Vault\
- memory\
- training_data\
- archive\ (D-45 — 9 subfolders with manifest)
- mail_cart\ (inter-project relay — NEW)

### Governance Folder
- D-Series\: D-00 through D-09, D-Master Build, CLAUDE_READ_THIS_FIRST.md, JARVIS_PROJECT_HANDOFF.md, NEUROLOGIST_PROJECT_INSTRUCTIONS.md, SURGEON_PROJECT_INSTRUCTIONS.md
- audit_logs\: Output Hygiene Rules + 2 Surgeon post-op reports
- COMMAND_LIBRARY.md, MASTER_SCIENCE_SHEET_v2.md, STRATEGIC_PLANNING_v1.0.md

### Archive (D-45)
9 subfolders with _MANIFEST.md:
legacy\, modelfiles\, extraction_tests\, knowledge_old\, knowledge_old_2\, reference\, legacy_ui\, root_scripts\, project_setup_docs\, extraction_analysis\

### Other Locations
- Downloads: EMPTY
- D:\Project Bin Files\: DELETED (contents moved to governance)
- D:\Strategic Planning\: DELETED (contents moved to governance)
- Members Of The Royal Court\: NUKED

---

## WORKER ROSTER

| Worker | Identity | Role | Connection | Status |
|--------|----------|------|------------|--------|
| **Claude Web** (Opus) | claude.ai | Director — architecture, planning, auditing | web_fetch via brain.wiggyoffgrid.com | Active |
| **Cowork Opus** | Claude Desktop | Jarvis Assistant, Neurologist, Surgeon, Codex | MCP filesystem to D:\Jarvis\brain\ | Active — NEW April 4 |
| **Dispatch** | Claude iOS | Phone-first assistant — Wiggy's mobile voice | Through active Cowork session | Active — NEW April 4 |
| **Claude Code** (Opus) | Terminal agent | Direct Beast execution — EXPENSIVE, surgical only | Direct filesystem | Available |
| **Gordon** | Docker Desktop AI (Haiku 4.5) | File ops, Docker, infrastructure. Business account wiggonator. | Docker container | Active |
| **Mason/Koonie** | Claude in Docker | Grunt worker, 20+ playbooks, task system. Named after Dad. | Docker container | Active |
| **Grossmann** | Google AI consultant | AI architect. Relay protocol only. | web_fetch via brain.wiggyoffgrid.com | Available |
| **14B Qwen** | Local llama-server | Everyday fast hat. 16384 context. | Flask port 5001 | Active |
| **9B Claude-distilled** | Local llama-server | CRM reasoning king. 65536 context. | Flask port 5001 | Active |
| **Gemma 4 E4B** | Local llama-server | CHAMPION — math + soul. Lowest VRAM. | Flask port 5001 | Active |
| **GLM-Z1-9B** | Local llama-server | Pure math specialist. | Flask port 5001 | Active |

**Key distinction:** Mason (Claude in Docker) is NOT Gordon. Mason is Anthropic Claude, free with Docker Business. Gordon is Docker's own AI. They're roommates, not the same worker.

---

## DOCKER STATUS

- Docker Desktop v4.67.0 on Business account (wiggonator)
- Gordon backend flag flipped by Docker Support April 3, 2026 (Case #00202864 — RESOLVED)
- EnableDockerAI in settings-store.json may need manual flip to true after re-login
- Docker fix script at D:\Jarvis\scripts\fix_docker.ps1 — kills all processes, shuts down WSL, clean restart
- WSL config at %USERPROFILE%\.wslconfig — limits memory to 4GB

---

## IDEAS VAULT — UPDATED THIS SESSION

**Location:** D:\Jarvis\brain\Ideas Vault\JARVIS_IDEAS_VAULT.md (43KB+)

New ideas logged this session:
1. **Jarvis Personal AI — $899 Product** — packaged local AI installer with onboarding questionnaire
2. **Off-Grid Homestead AI Demo** — Katrina the excavator scenario, 5-domain hit in one conversation
3. **The Eternal Provisioner** — Jarvis legacy system: eulogy, YouTube, website, knowledge lives forever
4. **Multi-Project Claude Communication Protocol** — specialized projects with mail cart relay
5. **Claude Project Installer / Local Sync Server** — localhost:8009 syncing project files, saves Anthropic storage

---

## LIBRARIAN ARCHITECTURE — PROVEN

Gemma tested with filtered card loading — PERFECT results:
- 13/13 direct nieces/nephews
- 8/8 great-nieces/nephews  
- 5/5 nephew-in-laws (no Bob Barnes, Janet, Julie contamination)

**Architecture:** D-series domains → Flask reads question → routes to correct domain → loads only relevant cards → model gets focused context → accuracy peaks

Folder structure IS the filter. The inlaws split eliminated over-inclusion. The relationship rename enables keyword-based routing.

---

## NEUROLOGIST FIRST AUDIT — COMPLETED

First full audit ran this session. Results:
- 3 Critical findings (all resolved by Surgeon)
- 7 Warnings (all resolved)
- 5 Info items (noted)
- Three Authorities: DRIFT → ALIGNED (all three pairs confirmed post-remediation)
- Post-remediation audit still pending (Neurologist waiting for next session)

### Open HOLDs from Neurologist
- HOLD-A: voices\ empty — status changed to Pending in D-07. Adrian voice files location unknown.
- HOLD-B: STRATEGIC_PLANNING_v1.md renamed to v1.0 — RESOLVED
- HOLD-C: wiggy_equipment\ (D-21) has 1,336 files but D-02 listed as "Not yet built" — RESOLVED April 4 (D-02, D-00, D-07 all updated)

---

## WHAT NEEDS TO HAPPEN NEXT

### Immediate (Next Session) — PRIORITY ORDER
- [ ] **DRIVE CONSOLIDATION — Phase 1: Inventory** (see plan below)
- [ ] Neurologist post-remediation audit (verify Three Authorities aligned — carried from April 3)
- [ ] Re-setup Neurologist and Surgeon as Sonnet projects in Cowork (instructions ready in governance/)
- [ ] Test Grossmann access via brain.wiggyoffgrid.com
- [ ] Find Adrian voice files for voices\ folder (likely in Docker container)

### Completed (April 4)
- [x] Create startup script: JARVIS_BRAIN_STARTUP.ps1 + Task Scheduler
- [x] Basic auth tested — removed (web_fetch can't send headers). Path-based 403 protection kept
- [x] D-Master Build v1.0 — third Authority document
- [x] Update D-02: D-21 wiggy_equipment Active, D-08 Active, D-09 Active, D-Master Build registered (now v1.3)
- [x] Update D-07: added D-08, D-09, D-Master Build, brain server scripts, quoting folder, worker instructions
- [x] Update D-00: D-21 location from TBD to Active, D-08/D-MB in expansion rules
- [x] Update people_index.py paths for split inlaws folders
- [x] Neurologist + Surgeon project instructions written (in governance/)
- [x] All handoff docs, briefing docs, memory files aligned for every worker

### Quote Engine — IN PROGRESS (April 4 continuation)
- [x] D-09 Quote Engine Playbook created — full doctrine in D-Series — DONE April 4
- [x] 4 product line rules XMLs (vibro, impact, drill, wick drain) — DONE April 4
- [x] Sheet4 master pricing database extracted (46 categories, 1,127 items) — DONE April 4
- [x] generate_quote_v6.js — flex-gap architecture (equipment top, rates/T&C/sig bottom) — DONE April 4
- [x] add_watermark.py — 10% opacity ape behind content via PDF overlay — DONE April 4
- [x] APE logo cleaned (ape_bold.png — flood-fill black→white, preserves outlines) — DONE April 4
- [x] End-to-end test: Joel Day 200-6 Vibro quote — numbers match Mason ($26,715/mo, $8,905/wk) — DONE April 4
- [ ] Wiggy providing proper logo files (current extractions have quality issues)
- [ ] Wiggy review of PU pairings in impact and drill rules (some estimated)
- [ ] SALE quote format (different layout for purchase quotes)
- [ ] Voice-to-JSON automation (currently AI builds JSON manually from dictation)
- [ ] Find Wiggy's original dictated equipment rules file (somewhere on the Beast)

### DRIVE CONSOLIDATION — THE BIG CLEANUP

**Problem:** Jarvis files scattered across C:\, D:\, E:\, F:\, G:\, H:\. Duplicates everywhere. C:\ gained ~10GB from Claude Desktop install (vm_bundles in %APPDATA%\Claude\). Wiggy wants D:\ as THE drive — one source of truth for everything.

**What's where right now:**
| Drive | What's on it | Status |
|-------|-------------|--------|
| C:\ | Windows + Claude Desktop (~10GB in AppData) | SACRED — needs cleanup, not Jarvis files |
| D:\Jarvis\ | Brain, Flask, models, scripts, Mason — the core | PRIMARY — already structured |
| E:\APE Work\ | APE quotes, Dropbox work files | SCATTERED — needs to move to D:\ |
| E:\THE PROVISIONERS CODEX\ | Wiggy's book project | SCATTERED — needs to move to D:\ |
| F:\ | Sources, reference material | UNKNOWN — needs inventory |
| G:\ | Personal, cabin, family photos | WIGGY ONLY — inventory only |
| H:\Koonie\, H:\Gordons Stable\ | Worker stables | FUNCTIONAL — low priority move |

**Phase 1 — Inventory (Neurologist):** Full scan all drives, document sizes, flag duplicates, produce CONSOLIDATION_INVENTORY.md
**Phase 2 — Plan (Director + Wiggy):** Decide target structure on D:\, plan each move
**Phase 3 — Execute (Surgeon + Wiggy approval):** Move files, update Three Authorities after each move
**Phase 4 — Verify and Wipe (Neurologist + Wiggy):** Post-move audit, Wiggy approves final wipe

**C:\ specifics:** Claude Desktop data at %APPDATA%\Claude\ (~10GB). Options: symlink to D:\, periodic cleanup of vm_bundles, or accept it. MCP config must stay at %APPDATA%\Claude\claude_desktop_config.json.

**Priority:** C:\ bloat first → E:\APE Work → E:\Codex → H:\ stables → F:\ and G:\

### Soon
- [ ] Add tunnel + server to DockerBootSequence.ps1 or create JARVIS_FULL_STARTUP.ps1
- [ ] Gmail connector for Cowork email sending
- [ ] Formal feedback to Anthropic re: Dispatch limitations (voice, project browser)
- [ ] Flask Librarian upgrade — domain-aware card injection
- [ ] Knowledge files (wiggy_history.md, wiggy_identity.md etc.) → convert to XML cards
- [ ] JSON card conversion alongside XML (keep both formats)
- [ ] Investigate Qwen3-8B F16 (30.53GB) — still needed for LoRA or delete?
- [ ] Fix Chatterbox TTS (currently broken)
- [ ] Cold boot verification — all services auto-start (including brain server + tunnel)
- [ ] Science Sheet v2 NEEDS_VERIFICATION items (14 items flagged)

### On the Horizon
- [ ] Flask v25 UI with hat-swap buttons
- [ ] WEAP AI extraction — Gemma or GLM as math engine (Wiggy is the PATENT HOLDER on wick drain shoes)
- [ ] Dual RTX 3090s (birthday gift) — 48GB VRAM unlocks 70B+ models
- [ ] LoRA training for Gemma 4 architecture
- [ ] Reverse index across all Jarvis domains
- [ ] PST email extraction (30,000 emails — Gordon + Mason job)
- [ ] Codex rebuild from E:\Dropbox\0 Wiggys Book\ fragments
- [ ] Jarvis $899 product development
- [ ] The Eternal Provisioner legacy system

---

## KEY LEARNINGS — APRIL 4, 2026

- **MCP is simpler than expected:** One npm package, one config file edit, instant filesystem access to the entire brain
- **BOM encoding breaks JSON:** Always use UTF8Encoding($false) for config files — no BOM
- **Cowork projects are desktop-only:** No mobile Cowork yet, Dispatch is the workaround
- **Dispatch memory can be hacked:** Write directly to agent\memory\ files on disk — turns generic Claude into Jarvis
- **Cloudflare quick tunnels change URL on restart:** Named tunnels with a domain are permanent
- **The human finds the loopholes:** Every breakthrough came from Wiggy thinking outside the box
- **Discussions ARE the work:** The brainstorm about mail cart problems led directly to eliminating bins entirely
- **One brain, every door:** MCP for Cowork, tunnel for web AIs, Flask for local models — same data, three paths
- **Flex-gap architecture is the answer for quotes:** Fixed blocks at top and bottom, gap shrinks as equipment grows. v3-v5 failed because they tried to distribute spacing — v6 calculates it mathematically
- **NEVER show per-item pricing:** Wiggy's #1 rule. Package rate only. One monthly total, divide by 3 for weekly. Multiply by 1.37 for CDN
- **LibreOffice headless for PDF conversion:** `soffice --headless --convert-to pdf` — works but watch for file lock errors (kill stale soffice processes)
- **Watermarks must be PDF overlay, not docx:** docx-js floating images with behindDocument:true get dropped by LibreOffice conversion. Use pypdf+reportlab as a separate step after PDF conversion
- **Logo processing: flood-fill from corners, not global replace:** PIL ImageDraw.floodfill with tolerance=50 from 8 points (corners + edge midpoints) preserves interior outlines while blanking background
- **Wiggy reviews by screenshot comparison:** He opens his Mason workbook output side-by-side with the AI output and gives a numbered correction list. Match his format pixel by pixel or you'll iterate forever

---

## KEY LEARNINGS — APRIL 3, 2026

- **Multi-project architecture works:** Neurologist diagnoses, Surgeon operates, mail cart delivers. Proven in one session.
- **Mail Cart is simple but powerful:** TO_[DESTINATION] naming, one flat folder, Wiggy delivers. 30 seconds vs 10 minutes of copy-paste.
- **The Surgeon follows protocol:** Asked for Wiggy approval before every cut. Flagged governance updates back to Jarvis. Produced post-op reports as files. Caught his own stale files.
- **The Neurologist is sharp:** Caught D-02 version conflict, 18 homeless files, unregistered archive folders, client count drift, and even flagged that HE might be auditing against a stale document.
- **New Discovery Form prevents freelancing:** Surgeon stops when he finds something unexpected. No unauthorized cuts.
- **Output Hygiene Rules:** Every report is a file. Downloads is staging. Clean after delivery.
- **Gordon is the mail boy:** Perfect future role — file delivery, no thinking required.
- **PowerShell traps are now in memory:** Join-Path two arguments only. Variable:colon breaks strings.
- **Wiggy has patents:** CA-3122984-C Wick Drain Shoe — granted in Canada, US, Mexico, China. 3 million units sold. 3 more patents pending.

---

## FILE PATHS QUICK REFERENCE

| Item | Path |
|------|------|
| D-Series governance | D:\Jarvis\brain\governance\D-Series\ |
| Audit logs | D:\Jarvis\brain\governance\audit_logs\ |
| Mail cart | D:\Jarvis\brain\mail_cart\ |
| Flask app | D:\Jarvis\jarvis_flask.py |
| llama-server (b8639) | D:\Jarvis\llama.cpp\llama-server.exe |
| People cards | D:\Jarvis\brain\knowledge\people\ |
| Client cards | D:\Jarvis\brain\knowledge\APE\clients\ |
| APE equipment | D:\Jarvis\brain\knowledge\APE\ |
| Wiggy equipment | D:\Jarvis\brain\knowledge\wiggy_equipment\ |
| Extraction | D:\Jarvis\brain\knowledge\extracted\ |
| Ideas Vault | D:\Jarvis\brain\Ideas Vault\ |
| Archive (D-45) | D:\Jarvis\brain\archive\ |
| Models | D:\Jarvis\qlora\models\ |
| Mason | D:\Jarvis\Mason\ |
| Koonie stable | H:\Koonie\ |
| Gordon stable | H:\Gordons Stable\ |
| Docker fix script | D:\Jarvis\scripts\fix_docker.ps1 |
| Science Sheet v2 | D:\Jarvis\brain\governance\MASTER_SCIENCE_SHEET_v2.md |
| Command Library | D:\Jarvis\brain\governance\COMMAND_LIBRARY.md |
| Strategic Planning | D:\Jarvis\brain\governance\STRATEGIC_PLANNING_v1.0.md |
| Codex project | E:\THE PROVISIONERS CODEX\ |
| Quote Engine (D-09) | D:\Jarvis\brain\knowledge\APE\quoting\ |
| Quote Generator v6 | D:\Jarvis\brain\knowledge\APE\quoting\generate_quote_v6.js |
| Watermark Script | D:\Jarvis\brain\knowledge\APE\quoting\add_watermark.py |
| Pricing Database | D:\Jarvis\brain\knowledge\APE\quoting\sheet4_pricing.json |
| Quote Logos | D:\Jarvis\brain\knowledge\APE\quoting\logos\ |
| Boot log | D:\Jarvis\logs\boot_sequence.log |
| Jarvis Brain Server | D:\Jarvis\scripts\jarvis_brain_server.py |
| Cloudflare Tunnel | D:\Jarvis\scripts\cloudflared.exe |
| Tunnel Config | D:\Jarvis\scripts\config.yml |
| MCP Config | %APPDATA%\Claude\claude_desktop_config.json |
| Dispatch Memory | %APPDATA%\Claude\local-agent-mode-sessions\ |
| Domain | wiggyoffgrid.com (expires April 4, 2036) |
| Brain URL | https://brain.wiggyoffgrid.com |

---

*"Care for what sustains you, and it will sustain you in return." — Wiggy*
*"Never start anything unless you intend to finish it." — Claude Legault*
*"Does Eatons tell Sears their business?" — Koonie*
*Go Leafs Go.*
