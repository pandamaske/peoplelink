# Repository Population Methodology

**Project:** GEODIS New HCM - AMARIS
**Phase:** 02 - Define
**Created:** 2025-12-06
**Purpose:** Master methodology for populating all HCM repositories

---

## 1. Overview

This document defines the methodology for populating **69 repository files** across **6 iterations**:

| Iteration | Files | Priority |
|-----------|:-----:|:--------:|
| 1. Organization Structure | 16 | HIGH |
| 2. Workforce Structure | 8 | HIGH |
| 3. Personal Details | 24 | MEDIUM |
| 4. Employment Details | 10 | MEDIUM |
| 5. Compensation Details | 6 | MEDIUM |
| 6. Process and Security | 5 | LOW |

---

## 2. Four-Phase Methodology

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         FOR EACH REPOSITORY:                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  PHASE 1: SOURCE IDENTIFICATION                                     │   │
│  │  ├── Identify source file(s) from MDM MAB / MDM HR / MDM SITES     │   │
│  │  ├── Document source file structure (columns, delimiter, encoding) │   │
│  │  ├── Identify filter criteria (e.g., Status = ACTIVATED)           │   │
│  │  └── Count expected records                                         │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              ↓                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  PHASE 2: COLUMN MAPPING                                            │   │
│  │  ├── Map each target column to source column                        │   │
│  │  ├── Define transformation rules (lookups, defaults, formats)       │   │
│  │  ├── Mark required fields (*)                                       │   │
│  │  └── Document any business rules                                    │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              ↓                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  PHASE 3: SAMPLE VALIDATION                                         │   │
│  │  ├── Generate 3-5 sample records                                    │   │
│  │  ├── Show source → target transformation                           │   │
│  │  ├── ⚠️  USER CONFIRMS MAPPING IS CORRECT                          │   │
│  │  └── Document any adjustments                                       │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              ↓                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  PHASE 4: POPULATION                                                │   │
│  │  ├── Extract data from source                                       │   │
│  │  ├── Apply transformations                                          │   │
│  │  ├── Load into target Excel file                                    │   │
│  │  ├── Quality check (record count, required fields)                  │   │
│  │  └── Mark as COMPLETE in progress tracker                           │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 3. Source Files Master List

### 3.1 MDM MAB (01 - MDM MAB)

| File | Size | Delimiter | Key Use |
|------|------|:---------:|---------|
| Business Hierarchy.csv | 2.9 KB | ; | Division (L2) |
| SOUs View.csv | 389 KB | ; | Business Unit |
| Legal Entities View.csv | 121 KB | ; | Legal Entity |
| Legal Sites.csv | 295 KB | ; | Legal Address, Reporting Establishment |
| Reporting Units View.csv | 107 KB | ; | Reference |
| Managerial Hierarchy.csv | 35 KB | ; | Reference |
| Local SOUs.csv | 473 KB | ; | Cost Allocation |
| ActivitiesFunctions View.csv | 52 KB | ; | Job Function |
| Systems.csv | 1.4 KB | ; | Source System Owner |

### 3.2 MDM HR (02 - MDM HR)

| File | Size | Format | Key Use |
|------|------|:------:|---------|
| HubLibraries_Departments.json | 15.1 MB | JSON | Department |
| Organisations.csv | 20.4 MB | , | Organization Tree |
| JobRepositoryNewIE.csv | 9.3 MB | , | Job |
| KeyPropertiesNewIE.csv | 5.8 MB | , | Reference values |
| ValuesListLibrary.csv | 208 KB | , | Lookup values |
| GenericLibrary.csv | 1.5 MB | , | Generic lookups |
| Collective_Agreements_Template.csv | 17 KB | , | Collective Agreement |

### 3.3 MDM SITES (03 - MDM SITES)

| File | Size | Delimiter | Key Use |
|------|------|:---------:|---------|
| Site View.csv | 77 KB | ; | Location |
| Address View.csv | 75 KB | ; | Location addresses |

---

## 4. Global Progress Tracker

### 4.1 Organization Structure (16 files)

| # | Repository | Source | Records | Status |
|---|------------|--------|--------:|:------:|
| 1 | Country Code | Oracle Seeded | - | N/A |
| 2 | Geography | Oracle Seeded | - | N/A |
| 3 | **Enterprise HCM** | Manual | **1** | DONE 2025-12-06 |
| 4 | **Legislative Data Group** | Legal Entities View.csv | **62** | DONE 2025-12-06 |
| 5 | **Legal Address** | Legal Sites.csv | **2,046** | DONE 2025-12-06 |
| 6 | **Legal Entity** | Legal Entities View.csv | **364** | DONE 2025-12-06 |
| 7 | **Division** | Business Hierarchy.csv (L2) | **19** | DONE 2025-12-06 |
| 8 | **Business Unit** | SOUs View.csv | **2,175** | DONE 2025-12-06 |
| 9 | **Data Set** | Manual | **1** | DONE 2025-12-06 |
| 10 | **BU Set Assignment** | SOUs View.csv | **2,175** | DONE 2025-12-06 |
| 11 | **Department** | HubLibraries_Departments.json | **10,803** | DONE 2025-12-06 |
| 12 | **Department Tree** | HubLibraries_Departments.json | **10,802** | DONE 2025-12-06 |
| 13 | **Organization Tree** | Business Hierarchy.csv | **40** | DONE 2025-12-06 |
| 14 | **Location** | Site View.csv + Address View.csv | **919** | DONE 2025-12-06 |
| 15 | **Reporting Establishment** | Legal Sites.csv | **2,046** | DONE 2025-12-06 |
| 16 | Time Zone | Oracle Seeded | - | N/A |

**Organization Structure Progress: 13/13 actionable repositories COMPLETE (31,453 records)**

### 4.2 Workforce Structure (8 files)

| # | Repository | Source | Records | Status |
|---|------------|--------|--------:|:------:|
| 1 | **Job** | JobRepositoryNewIE.csv (active, with underscore) | **688** | DONE 2025-12-06 |
| 2 | **Job Family** | ActivitiesFunctions View.csv (L4, with active jobs) | **27** | DONE 2025-12-06 |
| 3 | **Job Sub Family** | ActivitiesFunctions View.csv (L5, with active jobs) | **79** | DONE 2025-12-06 |
| 4 | **Job Function** | JobRepositoryNewIE.csv (parent in AF L5) | **236** | DONE 2025-12-06 |
| 5 | **Management Level** | JobRepositoryNewIE.csv (job name patterns) | **5** | DONE 2025-12-06 |
| 6 | **Grade** | MERCER Job Library (Career Level Title) | **20** | DONE 2025-12-06 |
| 7 | Grade Step | TBD | - | ⬜ |
| 8 | **Position** | MERCER Job Library (Job Code + Job Title) | **24,398** | DONE 2025-12-06 |
| 9 | Currencies | Oracle Seeded | - | N/A |

**Workforce Structure Progress: 7/8 actionable repositories COMPLETE (25,453 records)**

#### Workforce Structure Hierarchy (completed)

```
Job Family (AF L4: 27)
    └── Job Sub Family (AF L5: 79)
            └── Job Function (JobRepo nodes with parent in AF L5: 236)
                    └── Job (JobRepo nodes with underscore, active: 688)
```

**Hierarchy Rules:**
- Only Job Families (AF L4) with at least 1 active job linked are included
- Only Job Sub Families (AF L5) with at least 1 active job linked are included
- Job Functions link to their parent Job Sub Family (AF L5 code)
- Jobs link to their parent Job Function

#### Sample Records

**Job Family (from ActivitiesFunctions L4):**
| * Code | * Name | * Effective Start Date | * Status |
|--------|--------|------------------------|----------|
| 14PL0 | 4PL Operations | 2000-01-01 | A |
| 2HR00 | Human Resources | 2000-01-01 | A |
| 2FIN0 | Finance | 2000-01-01 | A |

**Job Sub Family (from ActivitiesFunctions L5):**
| * Code | * Name | * Job Family Code | * Effective Start Date | * Status |
|--------|--------|-------------------|------------------------|----------|
| 14PLO | 4PL Operations (L2) | 14PL0 | 2000-01-01 | A |
| 2HRPA | Payroll | 2HR00 | 2000-01-01 | A |
| 2FIAC | Accounting & Consolidation | 2FIN0 | 2000-01-01 | A |

**Job Function (from JobRepository, parent in AF L5):**
| * Code | * Name | * Job Sub Family Code | * Status |
|--------|--------|----------------------|----------|
| Accountant Payable | Accountant Payable | 2FIAC | A |
| Payroll Officer | Payroll Officer | 2HRPA | A |
| HR Manager | HR Manager | 2HRMG | A |

**Job (from JobRepository, active with underscore):**
| * Code | * Name | * Job Function Code | Management Level Code | * Status |
|--------|--------|---------------------|----------------------|----------|
| 2FIAC_ACPAOFCF | Accounts Payable Officer Confirmed | Accountant Payable | CF | A |
| 2HRPA_PAOFEL | Payroll Officer Entry level | Payroll Officer | EL | A |
| 2HRMG_HRMAM2 | HR Manager Management level 2 | HR Manager | M2 | A |

**Management Level (derived from job name patterns):**
| * Code | * Name | Jobs |
|--------|--------|-----:|
| EL | Entry level | 137 |
| CF | Confirmed | 177 |
| M1 | Management level 1 | 80 |
| M2 | Management level 2 | 111 |
| M3 | Management level 3 | 81 |

**Grade (from MERCER Career Level - 20 grades):**
| * Code | * Name | Career Stream |
|--------|--------|---------------|
| S1 | Entry Para-Professional | PARA-PROFESSIONAL |
| P1 | Entry Professional | PROFESSIONAL |
| M3 | Manager | MANAGEMENT |
| E1 | Executive Level 1 | EXECUTIVE |

**Position (from MERCER Job Library - 24,398 positions):**
| * Code | * Name | Grade Code |
|--------|--------|------------|
| GMA.01.001.E5A | Chair of the Board (Non CEO) - Global Parent/Corporate (E5) | E5 |
| FIN.02.003.P3 | Senior Accountant (P3) | P3 |
| HRM.01.002.M3 | HR Manager (M3) | M3 |

### 4.3 Personal Details (24 files)

| # | Repository | Source | Records | Status |
|---|------------|--------|--------:|:------:|
| 1 | Person Type | Oracle Seeded | - | N/A |
| 2 | Name Styles | Oracle Seeded | - | N/A |
| 3 | Name Formats | Oracle Seeded | - | N/A |
| 4 | **Titles** | KeyPropertiesNewIE.csv | **7** | DONE |
| 5 | **Gender** | Standard values | **3** | DONE |
| 6 | **Marital Statuses** | GenericLibrary.csv (SITFAM) | **6** | DONE |
| 7 | **Highest Education Level** | GenericLibrary.csv (NIVEAUDIPLOME) | **10** | DONE |
| 8 | **Document Category** | Oracle Seeded (17) + GEODIS Custom (9) | **26** | DONE |
| 9 | **Document Type** | typeOfDocuments_referential.json + Benchmark | **98** | DONE |
| 10-24 | Address/Phone types | Oracle Seeded / TBD | - | N/A |

**Personal Details Progress: 6 actionable repositories COMPLETE (150 records)**

### 4.4 Employment Details (10 files)

| # | Repository | Source | Records | Status |
|---|------------|--------|--------:|:------:|
| 1 | **Collective Agreement** | Collective_Agreements_Template.csv | **112** | DONE |
| 2 | **Contract Type** | Oracle Seeded (78) + GEODIS KeyProperties (73) | **151** | DONE |
| 3 | **Assignment Category** | Standard values | **4** | DONE |
| 4 | **Assignment Status** | Standard values | **4** | DONE |
| 5 | **Worker Category** | Standard values | **4** | DONE |
| 6 | **Hourly-Salaried** | Standard values | **2** | DONE |
| 7 | **Regular or Temporary** | Standard values | **2** | DONE |
| 8 | **Manager Type** | Organisations.csv (organization types) | **6** | DONE |
| 9 | **Seniority Rules** | Standard values | **3** | DONE |
| 10 | **Frequency Working Hours** | GenericLibrary.csv (PERIODICITY) | **8** | DONE |

**Employment Details Progress: 10/10 repositories COMPLETE (296 records)**

### 4.5 Compensation Details (6 files)

| # | Repository | Source | Records | Status |
|---|------------|--------|--------:|:------:|
| 1 | **Frequence Salary** | GenericLibrary.csv (PERIODICITY) | **8** | DONE |
| 2 | **Salary Basis** | Standard values | **4** | DONE |
| 3 | **Comp Elements** | GenericLibrary.csv (Bonus/Incentive/Advantage) | **35** | DONE |
| 4 | **Payroll Relationship** | Standard values | **2** | DONE |
| 5 | **Individual Compensation Plan** | Standard values | **3** | DONE |
| 6 | **Compensation History** | Template | **1** | DONE |

**Compensation Details Progress: 6/6 repositories COMPLETE (53 records)**

### 4.6 Process and Security (5 files)

| # | Repository | Source | Records | Status |
|---|------------|--------|--------:|:------:|
| 1 | **Action** | Standard HR actions | **9** | DONE |
| 2 | **Action & Reasons** | Standard HR reasons | **14** | DONE |
| 3 | **Core Data Model** | Template | **1** | DONE |
| 4 | **Approval Workflows** | Standard workflows | **4** | DONE |
| 5 | **Security Matrix** | RolesEtDroits.csv (GEODIS G-Talent+) | **53** | DONE |

**Process and Security Progress: 5/5 repositories COMPLETE (81 records)**

**Legend:**
- ⬜ Not started
- 🔄 In progress (current phase indicated)
- ✅ Complete
- N/A Oracle seeded / no action needed

---

## 5. Mapping Documentation Structure

For each repository, create a mapping section with:

```markdown
### [Repository Name] Mapping

**Source:** [File name and path]
**Filter:** [Filter criteria if any]
**Expected Records:** [Count]

#### Column Mapping

| # | Target Column | Source Column | Transformation | Required |
|---|---------------|---------------|----------------|:--------:|
| 1 | ... | ... | ... | ✅ / ⬜ |

#### Sample Data (Source → Target)

**Source Record:**
| Field | Value |
|-------|-------|
| ... | ... |

**Target Record:**
| Field | Value |
|-------|-------|
| ... | ... |

#### Validation Status
- [ ] Mapping confirmed by user
- [ ] Sample approved
- [ ] Ready for population
```

---

## 6. Quality Checklist

Before marking a repository as complete:

- [ ] All required fields (*) are populated
- [ ] Record count matches expected
- [ ] No duplicate keys
- [ ] Date formats are correct (YYYY-MM-DD)
- [ ] Status values are valid (A/I or Active/Inactive)
- [ ] Parent references exist (for hierarchies)
- [ ] Character encoding is correct (no garbled text)

---

## 7. Detailed Mappings by Iteration

See separate sections below for each iteration's detailed mappings.

---

## 8. Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-06 | Claude Code | Initial methodology |

---

*This methodology applies to all 69 repositories across 6 iterations.*
