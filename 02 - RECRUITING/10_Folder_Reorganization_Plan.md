# Recruiting Module - Folder Reorganization Plan

**Created:** 2025-12-07
**Status:** COMPLETED

---

## Current State Analysis

### Total Files Found: 318 (Excel + CSV)

### Issues Identified

| # | Issue | Location | Impact |
|---|-------|----------|--------|
| 1 | **Duplicate TS_Import_Output** | Root + `01 - TS/` | 2x storage, confusion |
| 2 | **4 UKG Mapping versions** | Root level | Unclear which to use |
| 3 | **2 UKG Package versions** | `UKG GAP ANALYSIS/` | v2 vs v3 |
| 4 | **165+ scattered CSVs** | `01 - TS/Data Model/` | No organization |
| 5 | **40+ timestamped UAT files** | UAT folders | Redundant iterations |
| 6 | **207MB UKG source at root** | `Opportunity Detail.csv` | Wrong location |
| 7 | **Empty 99 - OTHER folder** | Root level | No purpose |
| 8 | **Python cache files** | `__pycache__`, `output/` | Dev artifacts |

---

## Proposed Structure

```
02 - Recruiting/
│
├── 00 - DOCUMENTATION/           # All markdown docs (10 files)
│   ├── 00_DOCUMENTATION_INDEX.md
│   ├── 01_Module_Session_Tracker.md
│   ├── 02-09_*.md (analysis docs)
│   └── 10_Folder_Reorganization_Plan.md (this file)
│
├── 01 - SOURCE DATA/             # Renamed from "01 - TS"
│   ├── TALENTSOFT/               # Talentsoft exports
│   │   ├── SDD Reports/          # SDD_*.csv files (6 files, ~170MB)
│   │   ├── Data Model/           # Referential CSVs (160+ files)
│   │   └── Field Documentation/  # PDFs (applicant, vacancy fields)
│   │
│   └── UKG/                      # UKG exports (moved from 02 - UKG)
│       ├── Opportunity Detail.csv    # 207MB source file
│       └── Talent Acquisition Package.xls
│
├── 02 - MAPPING/                 # All mapping files consolidated
│   ├── UKG_Talentsoft_Holistic_Mapping.xlsx   # CORRECTED version only
│   ├── UKG_Talentsoft_Mapping_CORRECTIONS.xlsx  # Corrections log
│   └── US Talent Acquisition Package mapped v3.xlsx  # Latest analysis
│
├── 03 - ORACLE/                  # Target Oracle configuration (14 files)
│   ├── Requisition Template.xlsx
│   ├── Candidate Phase.xlsx
│   ├── ... (14 repository sheets)
│   └── create_recruiting_sheets.py
│
├── 04 - CONVERSION/              # Converter tools
│   ├── Scripts/                  # Python converters
│   │   ├── opportunity_converter.py
│   │   ├── ukg_to_talentsoft_converter.py
│   │   └── run_production.py
│   │
│   ├── Output/                   # Latest converted files only
│   │   ├── PRODUCTION/           # Latest production output
│   │   │   ├── TS_Import_offer.csv
│   │   │   ├── TS_Import_offeruser.csv
│   │   │   └── TS_Import_entity.csv
│   │   └── UAT/                  # Latest UAT output only
│   │
│   └── Batch Files/              # Execution scripts
│       ├── RUN_PRODUCTION.bat
│       ├── RUN_UAT.bat
│       └── RUN_CONVERTER_MENU.bat
│
└── 99 - ARCHIVE/                 # Old versions, backups
    ├── Mapping_Versions/         # Old mapping files
    │   ├── UKG_Talentsoft_Holistic_Mapping_BACKUP.xlsx
    │   ├── UKG_Talentsoft_Holistic_Mapping_ORIGINAL.xlsx
    │   └── US Talent Acquisition Package mapped v2.xlsx
    │
    └── Conversion_History/       # Old timestamped outputs
        └── 2024-11-23/           # By date
```

---

## Files to DELETE (Duplicates/Temp)

| File/Folder | Reason | Size |
|-------------|--------|------|
| `TS_Import_Output/` (root) | Duplicate of `01 - TS/TS_Import_Output/` | ~50MB |
| `__pycache__/` | Python cache | <1MB |
| `output/` in converter | Empty/temp output | <1MB |
| `_ul` file | Unknown temp | <1KB |
| 38 old timestamped CSVs | Keep only latest (2024-11-24_175949) | ~100MB |

---

## Files to RENAME/MOVE

| Current Location | New Location | Action |
|-----------------|--------------|--------|
| `UKG_Talentsoft_Holistic_Mapping_CORRECTED.xlsx` | `02 - MAPPING/UKG_Talentsoft_Holistic_Mapping.xlsx` | Rename (remove _CORRECTED) |
| `UKG_Talentsoft_Holistic_Mapping.xlsx` | `99 - ARCHIVE/Mapping_Versions/..._ORIGINAL.xlsx` | Archive |
| `UKG_Talentsoft_Holistic_Mapping_BACKUP.xlsx` | `99 - ARCHIVE/Mapping_Versions/` | Archive |
| `Opportunity Detail.csv` | `01 - SOURCE DATA/UKG/` | Move |
| `Doc_Export_Import_Rec_FR.xlsx` | `01 - SOURCE DATA/TALENTSOFT/Field Documentation/` | Move |
| `01 - TS/Data Model/*.csv` | `01 - SOURCE DATA/TALENTSOFT/Data Model/` | Keep in place |
| `02 - UKG/` contents | `01 - SOURCE DATA/UKG/` | Consolidate |

---

## Folders to DELETE (Empty After Cleanup)

- `02 - UKG/` (contents moved to `01 - SOURCE DATA/UKG/`)
- `99 - OTHER/` (empty, replaced by `99 - ARCHIVE/`)
- `UKG GAP ANALYSIS/` (after moving v3 file)
- `UKG_to_Talentsoft_Converter/output/` (empty)
- `UKG_to_Talentsoft_Converter/__pycache__/` (cache)

---

## Storage Impact

| State | Files | Size |
|-------|-------|------|
| Before cleanup | 318 | ~600MB |
| After cleanup | ~200 | ~500MB |
| Savings | ~118 files | ~100MB |

---

## Execution Order

1. Create new folder structure
2. Move files to new locations
3. Delete duplicates and old versions
4. Update documentation index
5. Verify file integrity

---

## Execution Summary

**Reorganization completed:** 2025-12-07

### Results

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Total files | 318 | 209 | -109 (34%) |
| Root folders | 12 | 6 | -6 |
| Mapping versions | 4 | 1 (+ 3 archived) | Consolidated |
| Duplicate TS_Import_Output | 2 | 1 | Removed |
| Timestamped CSVs | 40+ | Latest only | Cleaned |

### Actions Taken

- [x] Created new folder structure (6 main folders)
- [x] Consolidated mapping files to `02 - MAPPING/`
- [x] Moved source data to `01 - SOURCE DATA/`
- [x] Organized converter to `04 - CONVERSION/`
- [x] Archived old versions to `99 - ARCHIVE/`
- [x] Removed duplicate `TS_Import_Output/`
- [x] Removed temp files (`__pycache__`, `_ul`)
- [x] Updated documentation index

---

*Completed: 2025-12-07*
