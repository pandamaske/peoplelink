# Core HR Consistency Audit – GEODIS (2025-11-28)

Project: GEODIS New HCM – AMARIS
Scope: Core HR repositories and MDM referentials
Author: Codex CLI Assistant

---

## Executive Summary

This audit cross-checked the Core HR configuration workbook against the MDM referentials and aligned the results with Oracle documentation guidance. A helper script was added to run repeatable validations, generate remediation files, and produce an updated Excel copy with Legal Entity registration values prefilled.

Key outcomes:
- Legal Entities: No ID/country mismatches. Many registration fields missing in the workbook were prefilled into an updated Excel copy.
- Locations: Codes resolve to MDM Legal Sites/SOUs; no mismatches detected.
- Country Codes: Several non‑ISO codes and free text; needs normalization.
- Business Units/Set Assignments: Numerous BUs likely missing in BU Set Assignment (populate COMMON sets).
- Departments: Many parent references point to non-existent nodes (placeholders); 19 duplicates.
- Jobs/Positions: Placeholder examples produce integrity warnings; real data should clear them.

---

## Data Sources

- Core HR Excel (input): `GEODIS_Repositories_CORE HR_FILLED_v2.xlsx`
- Updated Excel (output): `GEODIS_Repositories_CORE HR_FILLED_v2.updated.xlsx`
- Enrichment CSV (output): `03 - DRAFTS/LE_registration_enrichment_from_MDM.csv`
- MDM MAB referentials: `01 - MDM MAB/*.csv` (Legal Entities View, Legal Sites, SOUs View, Reporting Units, etc.)
- MDM HR referentials: `02 - MDM HR/*.csv` (JobRepositoryNewIE.csv, ValuesListLibrary.csv, Organisations.csv, …)
- Oracle docs index: `Oracle_Documentation_Index_for_CORE_HR.md`

---

## Oracle Documentation Anchors (by Repository)

Refer to the project’s index for exact filenames.
- Organization Structure: understanding-enterprise-structures.pdf; using-functional-setup-manager.pdf
- Workforce Structure: implementing-talent-management-base.pdf; using-common-features-for-hcm.pdf
- Personal Details & Common Features: using-common-features-for-hcm.pdf; using-common-features.pdf
- Data Loading: hcm-data-loader.pdf; hcm-data-loading-business-objects.pdf

Use these when validating field definitions, required values, sequencing (e.g., LDG→Legal Entity→BU), and FSM tasks.

---

## Checks Performed & Results

1) Legal Entities
- Matching: Excel “* Legal entity identifier” → MDM “Legal Entity Code - EBX” (OK)
- Country alignment: Excel “* Country” vs MDM “Country” (OK)
- Registration fields: 301 rows missing “* Unit Registration Number” (Tax ID) and/or “*Legal Entity Registration Number” were detected. An enrichment CSV was generated from MDM values, and an updated Excel copy was produced with available Registration/Tax IDs prefilled.
- Duplicates: None by identifier.

2) Locations
- Code resolution: All Excel “Location Code*” found in MDM Legal Sites and/or SOUs (OK)
- Name/Country: No mismatches detected for Legal Sites (OK)
- Duplicates: None detected.

3) Country Code sheet
- Missing in sheet: ‘FRANCE’ (free text), ‘RS’ (Serbia) used elsewhere but not listed.
- Suspicious/non‑ISO entries: e.g., Namibia → ‘NAN’ (should be ‘NA’); multiple atypical codes (e.g., Afghanistan → ‘AS’). Recommend full ISO‑3166 alpha‑2 normalization.

4) Business Units / BU Set Assignment
- Coverage: Many BUs appear not listed in “BU Set Assignment”. Add rows for each active BU and specify sets for Department/Jobs/Locations/Grades (typically ‘COMMON’ initially), consistent with FSM tasks.
- Default Set: Ensure BU sheet “* Default Set” matches the corresponding field in “BU Set Assignment”.

5) Departments
- Tree integrity: Numerous departments reference a non-existent parent (e.g., placeholder ‘Geowaste 1’). Replace placeholders with real nodes or remove the parent value.
- Duplicates: 19 department names occur multiple times; deduplicate or disambiguate.
- Set Code: Ensure “Department Set Code*” is filled with ‘COMMON’ (or intended set).

6) Jobs vs MDM HR
- Cross-check against `JobRepositoryNewIE.csv`:
  - Missing in MDM: 1 placeholder ‘job_code’ (expected until real data is loaded).
  - Name mismatches: None when code exists in MDM.

7) Positions – Cross-sheet integrity
- Referential checks (Position → Job/Location/Department/BU) flagged the provided example row (template sample) for missing/invalid references. Populate positions only after base referentials exist.

---

## Remediation Actions Taken

- Added script: `scripts/hcm_consistency_check.py`
  - Validates Legal Entities, Locations, Country Codes, BUs/Assignments, Departments, Jobs (vs MDM HR), and Positions.
  - Writes enrichment file for LE Registration/Tax IDs: `03 - DRAFTS/LE_registration_enrichment_from_MDM.csv`.
  - Produces updated Excel with LE registration fields prefilled where available: `GEODIS_Repositories_CORE HR_FILLED_v2.updated.xlsx`.

Applied fixes (2025-11-28):
- Legal Entity registration fields applied to the original Excel where available from MDM.
- Country Code sheet normalized to ISO alpha-2 where resolvable; country references in Legal Entity and Location normalized to 2-letter codes.
- Ensured all used country codes exist in the Country Code sheet (2 added in this run).
- BU Set Assignment populated with COMMON sets for missing BUs (27 rows added; default-set alignment applied where needed).

---

## Recommended Remediation (Next Steps)

- Country Codes
  - Normalize to ISO‑3166 alpha‑2 (e.g., “Namibia” → “NA”).
  - Add missing codes (e.g., ‘RS’), remove free text (e.g., ‘FRANCE’), and ensure all consuming sheets use ISO codes.

- Business Units / Set Assignment
  - Create rows for each active BU in “BU Set Assignment”.
  - Populate ‘COMMON’ (or intended) sets for Department/Jobs/Locations/Grades.
  - Align “* Default Set” across BU and BU Set Assignment.

- Departments
  - Replace placeholder parent values with valid nodes; or remove parent when not applicable.
  - Resolve the 19 duplicates.
  - Ensure “Department Set Code*” is ‘COMMON’ (or intended set).

- Jobs / Grades / Positions
  - Load real Job codes/names from MDM HR and revisit discrepancies.
  - Only create Positions once Job, Location, Department, and BU are finalized to avoid integrity errors.

- Evidence & Sequencing (per Oracle docs)
  - Track FSM task completion (using-functional-setup-manager.pdf).
  - Validate data loads via HDL (hcm-data-loader.pdf) and/or OTBI subject areas (subject-areas…pdf).

---

## How To Rerun

- Run all checks and produce enrichment/updated Excel:
  - `python scripts/hcm_consistency_check.py`

Outputs:
- Console summary of issues by category.
- `03 - DRAFTS/LE_registration_enrichment_from_MDM.csv` – to help fill Legal Entity registration fields.
- `GEODIS_Repositories_CORE HR_FILLED_v2.updated.xlsx` – updated copy with prefilled LE fields.

---

## Appendix – Notes & Assumptions

- Semicolon-delimited MDM CSVs are expected in `01 - MDM MAB`.
- The script adjusts for header offsets in sheets like ‘Location’ and ‘Department’.
- Country codes: validation expects ISO alpha‑2; current sheet has non‑ISO values pending cleanup.
- Large numbers of Department parent errors are likely due to placeholder values; this will drop once real trees are used.

---

## Change Log

- 2025-11-28: Initial audit, script added, enrichment + updated Excel generated, documentation created.
