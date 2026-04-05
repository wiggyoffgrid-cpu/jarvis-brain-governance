# D-06 â€” Jarvis Brain Revision Control Protocol

**Version:** 1.0
**Status:** Active
**Created:** April 3, 2026
**Authority:** Wiggy (Eric Legault)

---

## Purpose

This doctrine governs how changes are versioned, tracked, and preserved across the Jarvis Brain. Every modification has a history. Every version is recoverable. No retroactive edits.

---

## Version Numbering

- **v1.0** â€” Initial creation
- **v1.1, v1.2** â€” Minor updates (content additions, corrections, formatting)
- **v2.0** â€” Major revision (structural changes, new sections, architectural shifts)
- Highest version number is always the canonical (current) version
- Prior versions are retained â€” never deleted

---

## Change Protocol

### For Governance Doctrines (D-00 through D-06)
1. Create new version file with incremented version number
2. Document what changed in the file header
3. Update D-02 Operational Index with new version
4. Update D-Master Build
5. Retain prior version in same folder

### For XML Cards (People, Clients, Equipment)
1. Edit card in place (cards are living documents)
2. Log the change in session documentation
3. If structural format changes, update ALL cards to match (batch operation with verification)

### For Session Documentation (Science Sheet, Ideas Vault, etc.)
1. Append at bottom â€” never overwrite existing content
2. Use session header: "Royal Project [Date] [Time Range]"
3. Mark completed items with [x], pending with [ ]

---

## Backup Rules

1. Always backup before overwriting any master document
2. Golden Images maintained at H:\Golden_Images\
3. Project Bin Files at D:\Project Bin Files\ for staging
4. Never delete without explicit confirmation after dry-run report

---

## Amendment Sequence (Lock Sequence)

Every time ANY structural change is made:
1. **MAKE** the change
2. **UPDATE** D-02 Operational Index
3. **CONFIRM** D-02 is correct
4. **UPDATE** D-Master Build
5. **CONFIRM** D-Master Build is correct
6. **UPDATE** D-07 Folder Map if physical structure changed
7. **CONFIRM** all Three Authorities agree
8. Only then proceed to next change

Skipping any step makes the change invalid.

---

## What NOT To Do

- Do not create files with lineage in the filename (no _FROM_Rev2.3)
- Do not retroactively edit prior versions â€” create new version instead
- Do not delete prior versions without archival confirmation
- Do not make multiple structural changes without updating the Three Authorities between each one
- Do not assume a change was applied â€” verify on disk

---

*"Every change has a version. Every version has a history. No retroactive edits."*
