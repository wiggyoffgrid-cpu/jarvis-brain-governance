# DRIVE CONSOLIDATION PLAN — THE BIG CLEANUP

**Version:** 1.0
**Status:** Active — Approved by Wiggy
**Created:** April 4, 2026
**Authority:** Wiggy (Eric Legault)
**Author:** Project Jarvis (Director)

---

## Purpose

The Beast has Jarvis files scattered across 6 drives. This plan consolidates everything onto D:\ as the single source of truth. One drive, one brain, one structure. No more hunting across letters.

After consolidation, every Jarvis-related file lives under `D:\Jarvis\`. The only exceptions are Windows itself (C:\) and the MCP config file that must stay at `%APPDATA%\Claude\claude_desktop_config.json`.

---

## Current State — What's Where

| Drive | Contents | Size (est.) | Action |
|-------|----------|-------------|--------|
| C:\ | Windows + Claude Desktop (~10GB in %APPDATA%\Claude\) | ~10GB Claude data | Cleanup/symlink — Phase 3 |
| D:\Jarvis\ | Brain, Flask, models, scripts, Mason, llama.cpp — the core | PRIMARY | Already structured — stays |
| E:\APE Work\ | APE quotes, Dropbox work files | UNKNOWN | Move to D:\ — Phase 2A |
| E:\THE PROVISIONERS CODEX\ | Wiggy's book project, PROJECT KNOWLEDGE BIN | UNKNOWN | Move to D:\ — Phase 2B |
| F:\ | Sources, reference material | UNKNOWN | Inventory first — Phase 1 |
| G:\ | Personal, cabin, family photos | UNKNOWN | Inventory only — Wiggy decides |
| H:\Koonie\ | Claude Code stable (task-file launcher) | Small | Move to D:\ — Phase 2C |
| H:\Gordons Stable\ | Gordon workspace | Small | Move to D:\ — Phase 2C |
| H:\Golden_Images\ | Backups (referenced in D-06) | UNKNOWN | Move to D:\ — Phase 2C |

---

## Target Structure — Post-Consolidation

Everything under `D:\Jarvis\`. No new root-level folders on D:\.

```
D:\Jarvis\
│
├── jarvis_flask.py
├── system_prompt_v13.txt
├── DockerBootSequence.ps1
│
├── brain\                             THE BRAIN — no changes
│   ├── governance\
│   │   ├── D-Series\
│   │   └── audit_logs\
│   ├── knowledge\
│   │   ├── people\                    D-10
│   │   ├── APE\                       D-12, D-20, D-09 (quoting)
│   │   ├── extracted\                 D-42
│   │   ├── wiggy_equipment\           D-21
│   │   └── wiggy_personal\
│   ├── archive\                       D-45
│   ├── mail_cart\
│   ├── Chat History\
│   ├── Ideas Vault\
│   ├── memory\
│   └── training_data\
│
├── codex\                             ← FROM E:\THE PROVISIONERS CODEX\
│   └── (entire Codex tree preserved)
│
├── ape_work\                          ← FROM E:\APE Work\
│   └── (contents sorted after inventory — some may
│         merge into brain\knowledge\APE\)
│
├── workers\                           ← NEW — all worker stables consolidated
│   ├── koonie\                        ← FROM H:\Koonie\
│   ├── gordon\                        ← FROM H:\Gordons Stable\
│   └── mason\                         ← FROM D:\Jarvis\Mason\ (SURGICAL — Docker repoint)
│
├── golden_images\                     ← FROM H:\Golden_Images\
│
├── llama.cpp\                         No change
├── llama.cpp.backup\                  No change
├── qlora\                             No change (models, output)
├── scripts\                           No change (brain server, cloudflared, fix scripts)
├── logs\                              No change
├── uploads\                           No change (upload condo)
├── voices\                            No change (pending Adrian files)
├── Dashboard\                         No change
├── searxng\                           No change
└── acks\                              No change
```

---

## Phase Breakdown

### Phase 1 — Inventory (Neurologist)

**Objective:** Full scan of all drives. Document what exists, how big it is, flag duplicates and homeless files. No files are moved.

**Deliverable:** `CONSOLIDATION_INVENTORY_YYYYMMDD.md` via mail cart

**Scope:**
- E:\APE Work\ — full tree, file counts, sizes
- E:\THE PROVISIONERS CODEX\ — full tree, file counts, sizes
- F:\ — full tree (UNKNOWN contents — this is discovery)
- G:\ — full tree (personal/photos — Wiggy eyes only on contents)
- H:\ — full tree including Koonie, Gordons Stable, Golden_Images, anything else
- C:\Users\ericl\AppData\Roaming\Claude\ — size breakdown (vm_bundles, configs, sessions)
- D:\Jarvis\ — current size baseline for comparison

**Duplicate scan:** Flag any files that exist in multiple locations (same name + same size = probable dupe).

**Priority order:** C:\ bloat → E:\APE Work → E:\Codex → H:\ → F:\ → G:\

See: `TO_NEUROLOGIST_CONSOLIDATION_INVENTORY_TASK.md` for the formal task sheet.

---

### Phase 2 — Execute Moves (Surgeon + Wiggy approval)

Each sub-phase gets its own Surgeon pre-op plan. No batch moves — one source at a time. Grossmann Rule applies.

**Phase 2A — E:\APE Work\ → D:\Jarvis\ape_work\**
1. Surgeon copies entire tree to D:\Jarvis\ape_work\
2. Verify file counts match source
3. Wiggy reviews contents — decides what merges into brain\knowledge\APE\ vs stays in ape_work\
4. After Wiggy confirms, wipe source
5. Update Three Authorities

**Phase 2B — E:\THE PROVISIONERS CODEX\ → D:\Jarvis\codex\**
1. Surgeon copies entire tree to D:\Jarvis\codex\
2. Verify file counts and sizes match
3. Update D-11 location in D-00, D-02, D-07, D-Master Build
4. Update any references in other docs (D-04 Navigation Spine, etc.)
5. After Wiggy confirms, wipe source
6. Update Three Authorities

**Phase 2C — H:\ Stables + Golden Images → D:\Jarvis\**
1. Copy H:\Koonie\ → D:\Jarvis\workers\koonie\
2. Copy H:\Gordons Stable\ → D:\Jarvis\workers\gordon\
3. Copy H:\Golden_Images\ → D:\Jarvis\golden_images\
4. Verify all three destinations
5. Update Claude Code task launcher paths (koonie)
6. After Wiggy confirms, wipe H:\ sources
7. Update Three Authorities

**Phase 2D — Mason Reorganization (SURGICAL)**
This is NOT a drive consolidation move — Mason is already on D:\. This is a reorganization into the workers\ folder.

1. Copy D:\Jarvis\Mason\ → D:\Jarvis\workers\mason\
2. Update Docker container volume mount (docker-compose or run command)
3. Grep all 20+ playbooks for hardcoded D:\Jarvis\Mason\ paths — update each
4. Update inbox/outbox task system references
5. Start container, verify it reads from new path
6. Test at least one playbook end-to-end
7. After Wiggy confirms, delete old D:\Jarvis\Mason\
8. Update Three Authorities

**Phase 2E — C:\ Cleanup**
Options (Wiggy decides after inventory):
- **Symlink:** Move %APPDATA%\Claude\ contents to D:\Jarvis\claude_desktop\ and symlink back. MCP config stays functional. Saves ~10GB on C:\.
- **Periodic cleanup:** Delete vm_bundles periodically. Accept C:\ usage.
- **Accept it:** Claude Desktop needs what it needs. MCP config must stay on C:\ regardless.

**Phase 2F — F:\ and G:\ (Wiggy decides after inventory)**
- F:\ — contents unknown until Phase 1 inventory. Could be reference material that maps to a domain, or could be static archive.
- G:\ — personal/cabin/family photos. Wiggy only. Inventory tells us the size. Wiggy decides if it moves, stays, or gets backed up to golden_images.

---

### Phase 3 — Verify and Close (Neurologist + Wiggy)

1. Neurologist runs post-consolidation audit
2. Verify D:\ contains everything — no orphans on other drives
3. Verify Three Authorities all reflect new paths
4. Verify all services still work (Flask, llama-server, brain server, tunnel, Docker containers)
5. Verify MCP config still points correctly
6. Verify brain.wiggyoffgrid.com still serves correctly
7. Wiggy approves final state
8. Update D-05 Drive Rules table (remove E:\, F:\, G:\, H:\ Jarvis references)
9. Close consolidation project

---

## Rules

1. **No moves without inventory.** Phase 1 completes before Phase 2 starts.
2. **No moves without Wiggy approval.** Every sub-phase gets a pre-op plan. Wiggy approves before any file touches disk.
3. **One source at a time.** Grossmann Rule. Don't move E:\ and H:\ simultaneously.
4. **Copy first, verify, THEN delete source.** Never move-delete in one step.
5. **Three Authorities updated after EVERY sub-phase.** D-07, D-02, D-Master Build must all agree before proceeding.
6. **Family data on G:\ — ONLY Wiggy touches.** Neurologist inventories folder names and sizes. Never reads file contents.
7. **C:\ MCP config stays on C:\.** No exceptions. That's where Claude Desktop reads it.
8. **Downloads folder is staging.** Clean after every confirmed deployment.

---

## Governance Impact

After consolidation, the following docs need version bumps:
- **D-00** — Domain locations updated (D-11 Codex, D-44 Workers)
- **D-02** — File counts and paths updated
- **D-05** — Drive Rules table simplified (D:\ is primary, C:\ is Windows only)
- **D-07** — Full folder map rewrite reflecting new structure
- **D-Master Build** — Strategic status updated for affected domains

---

## Success Criteria

- [ ] Every Jarvis file lives under D:\Jarvis\
- [ ] E:\, F:\, H:\ contain zero Jarvis files (or are empty)
- [ ] G:\ status decided by Wiggy
- [ ] C:\ contains only Windows + MCP config (Claude Desktop bloat addressed)
- [ ] All services operational post-consolidation
- [ ] Three Authorities aligned and current
- [ ] No ideas lost. Not one fart in the wind.

---

*"Care for what sustains you, and it will sustain you in return." — Wiggy*
