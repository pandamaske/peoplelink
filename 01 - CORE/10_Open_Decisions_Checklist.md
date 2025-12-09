GEODIS – Open Decisions Checklist (Core HR Dimensions)

**Last Updated:** 2025-11-30
**Status:** Partially Resolved - Review with stakeholders for remaining items

---

## RESOLVED DECISIONS

### Organization Structure
- [x] **Division definition:** RESOLVED - 35 divisions from Managerial + Business Hierarchy
- [x] **Department source of truth:** RESOLVED - OrganisationalUnit from KeyPropertiesNewIE.csv (10,811 active units, 10-level hierarchy)
- [x] **Organization Tree:** RESOLVED - Department Tree with 10 levels published

### Workforce Structure
- [x] **Job Function taxonomy:** RESOLVED - Covered by Job Family (842 families from JobRepositoryNewIE.csv)
- [x] **Management Level:** RESOLVED - 11 levels derived from job names (Entry level, Confirmed, Mgmt level 1-3, Director, etc.)

### Compensation
- [x] **Mercer PositionClass policy:** RESOLVED - Grades G40-G68 + BAND 1-6 (22 total from GRADING_GEODIS)
- [x] **LDG codes:** RESOLVED - 80 LDGs created (one per country with Legal Entities)

---

## PENDING DECISIONS (Require Business Confirmation)

### Organization Structure
- [ ] **Business Unit derivation:** Confirm whether BU codes derive from Legal Entity Company Code, Business Hierarchy, or a separate BU list. (Current: 27 BUs from Business Hierarchy)
- [ ] **BU-Department association:** Confirm which BU each department belongs to

### Locations
- [ ] **Location source:** Confirm Legal Sites.csv (2,046 records) as authoritative for HR Locations
- [ ] **Country-specific address rules:** Provide any country-specific address format requirements
- [ ] **Time zone defaulting:** Confirm time zone assignment per location

### Compensation
- [ ] **Grade rates by country:** Define compensation ranges per LDG (Mercer data available for major countries)
- [ ] **Grade-Job mapping:** Confirm valid grades per job

### Lookups & Integrations
- [ ] **Cost centers:** Confirm integration approach (Finance as source) and whether HR holds a reference list
- [ ] **Source system owner:** Confirm which applications will contribute source keys for HDL

---

## NEXT STEPS

1. Review resolved decisions with business stakeholders
2. Get confirmation on pending items above
3. Create HDL templates for Oracle loading
4. Define security matrix and approval workflows

---

## Reference Documents

- See `DOCUMENTATION_INDEX.md` at root level for full documentation
- See `agent.md` for current implementation status (69/70 sheets populated)
- See `GEODIS_Repositories_CORE HR_FILLED_v2.xlsx` for populated data

