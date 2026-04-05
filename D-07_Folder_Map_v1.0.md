# D-07 — Jarvis Brain Folder Map

**Version:** 1.0
**Status:** Active — Living Document
**Created:** April 3, 2026
**Authority:** Wiggy (Eric Legault)
**Last Audited:** April 4, 2026

---

## Purpose

The Folder Map is the physical truth of what exists on disk. It is one of the Three Authorities — no structural change is valid unless this map, D-02 Operational Index, and D-Master Build all agree.

If a folder exists on disk but not in this map, it is unregistered. If a folder appears in this map but not on disk, it is missing. Both conditions are invalid.

---

## D:\ Drive — Jarvis Brain (Primary Workspace)

### D:\Jarvis\ (Root)

| Folder/File | Domain | Purpose | Status |
|---|---|---|---|
| jarvis_flask.py | D-41 | Flask app, port 5001, Jigsaw XML injection | Active |
| system_prompt_v13.txt | D-41 | System prompt (facts layer) | Active |
| DockerBootSequence.ps1 | D-41 | 19-second auto-start sequence | Active |
| acks\ | D-41 | TTS acknowledgment WAV files (ack_0 through ack_5) | Active |
| Dashboard\ | D-41 | Mission Control HTML dashboards (v3, v4, Operators Manual) | Active |
| llama.cpp\ | D-41 | llama-server b8639 (current build) | Active |
| llama.cpp.backup\ | D-41 | llama-server backup (pre-b8639) | Active |
| logs\ | D-41 | Boot sequence and system logs | Active |
| Mason\ | D-44 | Docker Claude (Anthropic) worker — scripts, playbooks, task system | Active |
| scripts\ | D-44 | Operational scripts (fix_docker.ps1, time_check.ps1, jarvis_brain_server.py, JARVIS_BRAIN_STARTUP.ps1, config.yml, cloudflared.exe) | Active |
| searxng\ | D-41 | SearXNG search engine config | Active |
| uploads\ | D-41 | Jarvis upload condo — documents, extractions, images | Active |
| voices\ | D-41 | TTS voice files — empty, Adrian voice not yet deployed | Pending |
| qlora\ | D-40 | QLoRA training — datasets, models, output, scripts, venv | Active |

### D:\Jarvis\brain\

| Folder | Domain | Purpose | Status |
|---|---|---|---|
| governance\ | D-43 | D-Series Compass (D-00 through D-09, D-Master Build), worker project instructions | Active |
| governance\audit_logs\ | D-43 | Neurologist audits, Surgeon post-ops, discovery forms, hygiene rules | Active |
| knowledge\ | Multiple | All knowledge domains | Active |
| Chat History\ | D-42 | Claude session transcripts, ChatGPT exports | Active |
| Ideas Vault\ | D-43 | Ideas Vault markdown | Active |
| memory\ | D-41 | Cache, knowledge, uploads, vector_db | Active |
| training_data\ | D-40 | Training datasets — email, codex, quote JSONL files | Active |
| archive\ | D-45 | Archived/retired files with manifest | Active |

### D:\Jarvis\brain\knowledge\

| Folder | Domain | Purpose | Status |
|---|---|---|---|
| people\ | D-10 | 76 XML people cards across 15 subfolders | Active |
| APE\ | D-12/D-20 | Client cards (309) and equipment XMLs (20) | Active |
| extracted\ | D-42 | 8 extraction categories + Claude sessions report | Active |
| wiggy_equipment\ | D-21 | Personal equipment — Argo, Cat 330CL, sawmill, etc. (10 categories) | Active |
| wiggy_personal\ | D-10 | Cabin build, world vision, family brain docs | Active |

### D:\Jarvis\brain\knowledge\people\

| Folder | Card Count | Notes |
|---|---|---|
| wiggy\ | 1 | eric_legault.xml |
| wife\ | 1 | cherryl_legault.xml |
| parents\ | 3 | claude_legault, gail_legault, claudette |
| siblings\ | 4 | randy, shawn, tammy_cote, tammy_lee_desjardin |
| nieces_nephews\ | 13 | Direct nieces and nephews |
| great_nieces_nephews\ | 8 | Children of nieces/nephews |
| inlaws\parent_inlaws\ | 2 | bob_barnes, janet_barnes |
| inlaws\sibling_inlaws\ | 2 | julie_legault, serge_cote |
| inlaws\nephew_inlaws\ | 3 | mikey_poirier, noah_thibert, pat_goulard |
| inlaws\future_inlaws\ | 2 | brook_stmartin, jeremy_lahti |
| grandparents_maternal\ | 2 | eric_puhakka, muriel_puhakka |
| grandparents_paternal\ | 2 | lomer_legault, yvette_legault |
| aunts_uncles_maternal\ | 8 | Puhakka aunts and uncles |
| aunts_uncles_paternal\ | 5 | Legault aunts and uncles |
| extended_family\ | 7 | Andy Leveille, ex in-laws, others |
| friends\ | 11 | Personal friends |
| colleagues\ | 1 | jarvis.xml |
| pets\ | 1 | kaiya.xml |

### D:\Jarvis\brain\knowledge\APE\

| Folder | Contents | Domain |
|---|---|---|
| clients\ | 113 company folders, 309 XML client cards | D-12 |
| (equipment XMLs) | 20 chunked APE product XMLs | D-20 |
| quoting\ | Quote engine: 4 rules XMLs, sheet4_pricing.json, generate_quote_v6.js, add_watermark.py, QUOTE_ENGINE_README.md, logos/ | D-09 |

### D:\Jarvis\brain\knowledge\extracted\

| Folder | Domain | Purpose |
|---|---|---|
| commands_that_worked\ | D-42 | Verified working commands |
| commands_that_failed\ | D-42 | Failed commands with error context |
| lessons_learned\ | D-42 | Operational lessons |
| architecture_decisions\ | D-42 | Structural decisions |
| ideas_from_chats\ | D-42 | Ideas extracted from sessions |
| people_data\ | D-42 | People information extracted |
| ape_technical\ | D-42 | APE technical knowledge |
| codex_and_book\ | D-42 | Codex-related extractions |
| Claude sessions extraction report\ | D-42 | Extraction reports |

### D:\Jarvis\brain\archive\ (D-45)

| Folder | Contents | Source |
|---|---|---|
| legacy\ | Old docmatrix, ollama configs, master manual | D:\Jarvis\Legacy\ |
| modelfiles\ | Retired modelfiles (v12) | D:\Jarvis\modelfiles\ |
| extraction_tests\ | Test extraction folders (8 categories) | brain\knowledge\extracted_claude_test\ |
| knowledge_old\ | Pre-XML relationship files, emergency protocols | brain\knowledge\archive\ |
| knowledge_old_2\ | Old APE knowledge, construction docs | brain\knowledge\_archive\ |
| reference\ | Onboarding questionnaires, knowledge registry (FLAGGED for product) | brain\knowledge\_reference\ |
| legacy_ui\ | Old Flask UI (app.py, app_rag.py, templates) | D:\Jarvis\jarvis-ui\ |
| root_scripts\ | Batch extraction scripts, reports, training logs | D:\Jarvis\ root files |
| _MANIFEST.md | Archive contents manifest | Created April 3, 2026 |

---

## H:\ Drive — Backup, Staging, Worker Stables

| Folder | Domain | Purpose | Status |
|---|---|---|---|
| H:\Koonie\ | D-44 | Claude Code deployment — task launcher, logs, output | Active |
| H:\Gordons Stable\ | D-44 | Gordon worker stable — scripts, PST files, enrichment tools | Active |

---

## D:\Jarvis\qlora\ (D-40 Models & Inference)

| Folder | Purpose |
|---|---|
| models\ | Model GGUF files (14B, 9B, Gemma E4B, GLM-Z1-9B, DeepSeek R1, Qwen3-8B F16) |
| datasets\ | Training datasets |
| output\ | LoRA adapter output |
| scripts\ | Training scripts |
| venv\ | Python virtual environment |
| _archive\ | Archived training artifacts |

---

## D:\Jarvis\brain\governance\D-Series\

| File | Version | Status |
|---|---|---|
| CLAUDE_READ_THIS_FIRST.md | — | Active |
| D-00_Domain_Structure_v1.0.md | v1.0 | Active |
| D-01_Governance_Charter_v1.0.md | v1.0 | Active |
| D-02_Operational_Index_v1.2.md | v1.2 | Active |
| D-03_Numbering_Constitution_v1.0.md | v1.0 | Active |
| D-04_Navigation_Spine_v1.0.md | v1.0 | Active |
| D-05_File_Architecture_v1.0.md | v1.0 | Active |
| D-06_Revision_Control_v1.0.md | v1.0 | Active |
| D-07_Folder_Map_v1.0.md | v1.0 | Active |
| D-08_MCP_Access_Protocol_v1.0.md | v1.0 | Active |
| D-09_Quote_Engine_v1.0.md | v1.0 | Active |
| D-Master_Build_v1.0.md | v1.0 | Active |
| JARVIS_PROJECT_HANDOFF.md | — | Active |
| NEUROLOGIST_PROJECT_INSTRUCTIONS.md | — | Active |
| SURGEON_PROJECT_INSTRUCTIONS.md | — | Active |

---

## Other Drives

| Path | Domain | Purpose | AI Access |
|---|---|---|---|
| C:\ | — | Windows ONLY — SACRED | NEVER |
| E:\APE Work\ | D-12/D-20 | APE quotes, Dropbox, work files | Read |
| E:\THE PROVISIONERS CODEX\ | D-11 | Codex book project (separate) | Separate project |
| F:\ | — | Sources, reference material | Read |
| G:\ | — | Personal, cabin, family photos | Wiggy only |
| H:\ | D-44 | Backup, staging, worker stables | Worker deployment |

---

## Integrity Rules

1. This map is ONE of the Three Authorities (with D-02 and D-Master Build)
2. Every folder on disk must appear in this map
3. Every folder in this map must exist on disk
4. Discrepancy between map and disk = invalid state — fix before proceeding
5. New folders require: update this map, update D-02, update D-Master Build
6. Deleted folders require: update this map, update D-02, update D-Master Build
7. Archive moves require: manifest entry in D-45

---

*"Does Eatons tell Sears their business?" — Koonie*
*"Care for what sustains you, and it will sustain you in return." — Wiggy*
