# D-05 â€” Jarvis Brain File Architecture

**Version:** 1.0
**Status:** Active
**Created:** April 3, 2026
**Authority:** Wiggy (Eric Legault)

---

## Purpose

This doctrine standardizes file naming, folder structure, and organizational consistency across the entire Jarvis Brain. It eliminates naming drift, inconsistent formats, and structural confusion.

---

## Naming Rules

1. Folder names use lowercase_with_underscores (e.g., people, clients, aecon, wiggy_contacts)
2. XML card filenames use lowercase_with_underscores (e.g., eric_legault.xml, abdullah_gul.xml)
3. Governance docs use D-##_Doctrine_Name_v#.#.md format
4. No special characters beyond hyphen and underscore
5. No apostrophes in folder or file names
6. No spaces in filenames â€” use underscores
7. No LOCKED in filenames â€” use FINAL if governance label needed
8. No _FROM_Rev lineage in filenames
9. Version format: v1.0, v2.0, v1.1, etc. â€” always at end of filename before extension

---

## Folder Structure Standard

Each domain gets its own root folder. Subfolders organize by category within the domain.

```
D:\Jarvis\brain\knowledge\
    people\                          â† D-10 People & Family
        wiggy\
        wife\
        parents\
        siblings\
        nieces_nephews\
        great_nieces_nephews\
        inlaws\
    APE\                             â† Multiple APE domains
        clients\                     â† D-12 Clients & CRM
            [company_name]\
                wiggy_contacts\
                    person_name.xml
        equipment\                   â† D-20 APE Equipment (chunked XMLs)
        employees\                   â† D-13 APE Employees (future)
    wiggy_equipment\                 â† D-21 Wiggy Equipment (future)
    extracted\                       â† D-42 Knowledge & Extraction
        commands_that_worked\
        commands_that_failed\
        lessons_learned\
        architecture_decisions\
        ideas_from_chats\
        people_data\
        ape_technical\
        codex_and_book\
```

---

## Card Format Standards

### People Cards (D-10)
```xml
<PERSON>
  <FULL_NAME>NAME UPPERCASE</FULL_NAME>
  <SPECIES>Human</SPECIES>
  <RELATIONSHIP_TO_WIGGY>Relationship</RELATIONSHIP_TO_WIGGY>
  <BORN>Date</BORN>
  <MARITAL_STATUS>Status</MARITAL_STATUS>
  <!-- ... all fields present, [UNDEFINED] if unknown -->
</PERSON>
```

### Client Cards (D-12)
```xml
<CLIENT>
  <FULL_NAME>NAME UPPERCASE</FULL_NAME>
  <ADDRESSED_AS>How Wiggy calls them</ADDRESSED_AS>
  <MOBILE_PHONE>phone</MOBILE_PHONE>
  <CURRENT_COMPANY>company</CURRENT_COMPANY>
  <JOB_TITLE>[UNDEFINED]</JOB_TITLE>
  <EMAIL>[UNDEFINED]</EMAIL>
  <COMPANY_ADDRESS>[UNDEFINED]</COMPANY_ADDRESS>
  <COMPANY_PHONE>[UNDEFINED]</COMPANY_PHONE>
  <COMPANY_FAX>[UNDEFINED]</COMPANY_FAX>
  <PAST_COMPANIES>[UNDEFINED]</PAST_COMPANIES>
  <NOTES>[UNDEFINED]</NOTES>
</CLIENT>
```

### Future Domain Cards
Each new domain defines its own card template in its doctrine page. Templates must follow these rules:
- XML format with clear field names
- [UNDEFINED] for unknown values â€” never blank, never guessed
- FULL_NAME in uppercase
- All fields present even if undefined
- UTF-8 encoding, no BOM
- No special characters that break JSON serialization

---

## Transport Verification

Before any file is considered deployed:
1. Confirm file exists at destination path
2. Confirm file size > 0 bytes
3. Confirm file opens and parses correctly (no UTF-8 errors)
4. Confirm D-02 Operational Index is updated
5. Only then proceed to next file

---

## Drive Rules

| Drive | Purpose | AI Access |
|-------|---------|-----------|
| C:\ | Windows ONLY | NEVER â€” sacred |
| D:\ | Jarvis Brain, all AI infrastructure | Primary workspace |
| E:\ | APE Work, Dropbox, Codex | Read access, Codex separate project |
| F:\ | Sources, reference material | Read access |
| G:\ | Personal, cabin, family photos | Wiggy only |
| H:\ | Backup, staging, worker stables | Worker deployment |

---

*"Folder name = purpose. File name = identity. Version = history. No drift allowed."*
