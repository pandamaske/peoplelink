# Repository Schema Reference

**Project:** GEODIS New HCM - AMARIS
**Phase:** 02 - Define
**Created:** 2025-12-06
**Purpose:** Document Oracle HCM column structures, sample values, and source mappings

---

## 1. Employment Details

### 1.1 Contract Type

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Unique contract type code |
| Start Date | DATE | ✅ | Effective start (01/01/2001) |
| End Date | DATE | ✅ | Effective end (12/31/4712) |
| Meaning | VARCHAR | ✅ | Display name |
| Tag | VARCHAR | | Country tag (+FR, +US, etc.) |
| HRP Status | VARCHAR | | HRP load status |
| Enable (Yes/No) | VARCHAR | ✅ | Yes/No |
| Status | VARCHAR | | Processing status |

**Sample Record:**
```
Lookup Code: FR_ADAPTATION
Start Date: 01/01/2001
End Date: 12/31/4712
Meaning: Adaptation contract
Tag: +FR
Enable (Yes/No): Yes
```

**Source:** KeyPropertiesNewIE.csv (WorkContractType)
**Records:** 62

---

### 1.2 Manager Type

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Code | VARCHAR | ✅ | Manager type code |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Display name |
| Description | VARCHAR | | Detailed description |
| HRP Status | VARCHAR | | HRP load status |
| Status | VARCHAR | | Processing status |

**Sample Record:**
```
Code: LM
Meaning: Line Manager
Description: Primary hierarchical manager - Hiérarchique
```

**Source:** Organisations.csv (organization column)
**Records:** 6

---

### 1.3 Worker Category

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup code | VARCHAR | ✅ | Worker category code |
| Enabled | CHAR(1) | ✅ | Y/N |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | English name |
| Meaning (FR) | VARCHAR | | French name |
| Description | VARCHAR | | Description |
| Tag | VARCHAR | | Country tag |
| HRP Status | VARCHAR | | HRP status |
| Status | VARCHAR | | Processing status |

**Sample Record:**
```
Lookup code: BC
Meaning: Blue Collar
Enabled: Y
```

**Source:** Standard Oracle values
**Records:** 4

---

### 1.4 Assignment Category

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Category code |
| Enabled | CHAR(1) | ✅ | Y/N |
| Start date | DATE | ✅ | Effective start |
| End date | DATE | ✅ | Effective end |
| Meaning (ENG) | VARCHAR | ✅ | English name |
| Meaning (FR) | VARCHAR | | French name |
| Description | VARCHAR | | Description |
| Tag | VARCHAR | | Country tag |
| HRP Status | VARCHAR | | HRP status |
| Status | VARCHAR | | Processing status |

**Sample Record:**
```
Lookup Code: FR
Meaning (ENG): Full-time regular
Enabled: Y
```

**Source:** Standard Oracle values
**Records:** 4

---

### 1.5 Assignment Status

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| User Status | VARCHAR | ✅ | User-friendly status name |
| Assignment Status Code | VARCHAR | ✅ | System code |
| HR Status | VARCHAR | | HR processing status |
| Meaning FR | VARCHAR | | French translation |
| Pay Status | VARCHAR | | Payroll status |
| Enable | CHAR(1) | ✅ | Y/N |
| Status | VARCHAR | | Processing status |

**Sample Record:**
```
User Status: Active Assignment
Assignment Status Code: ACTIVE_ASSIGN
Enable: Y
```

**Source:** Standard Oracle values
**Records:** 4

---

### 1.6 Hourly-Salaried

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Code (H/S) |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Display name |
| Meaning FR | VARCHAR | | French name |
| Description | VARCHAR | | Description |
| Enable | VARCHAR | ✅ | Yes/No |
| Client Status | VARCHAR | | Processing status |

**Sample Record:**
```
Lookup Code: H
Meaning: Hourly
Enable: Yes
```

**Source:** Standard Oracle values
**Records:** 2

---

### 1.7 Regular or Temporary

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Code (R/T) |
| Display Sequence | NUMBER | | Sort order |
| Enabled | CHAR(1) | ✅ | Y/N |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Display name |
| Description | VARCHAR | | Description |
| Tag | VARCHAR | | Country tag |
| Load Status | VARCHAR | | Load status |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
Lookup Code: R
Meaning: Regular
Display Sequence: 1
Enabled: Y
```

**Source:** Standard Oracle values
**Records:** 2

---

### 1.8 Seniority Rules

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Rule code |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Rule name |
| Tag | VARCHAR | | Country tag |
| Enable (Yes/No) | VARCHAR | ✅ | Yes/No |
| Status | VARCHAR | | Processing status |

**Sample Record:**
```
Lookup Code: COMPANY
Meaning: Company Seniority
Enable (Yes/No): Yes
```

**Source:** Standard values
**Records:** 3

---

### 1.9 Frequency Working Hours

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Frequency code |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Frequency name |
| Tag | VARCHAR | | Country tag |
| Enable (Yes/No) | VARCHAR | ✅ | Yes/No |
| Status | VARCHAR | | Processing status |

**Sample Record:**
```
Lookup Code: W
Meaning: Weekly
Enable (Yes/No): Yes
```

**Source:** GenericLibrary.csv (PERIODICITY)
**Records:** 8

---

### 1.10 Collective Agreement

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| * Effective Start Date | DATE | ✅ | Agreement start date |
| *Country | VARCHAR | ✅ | Country code |
| *Status | CHAR(1) | ✅ | A (Active) / I (Inactive) |
| * Identification Code | VARCHAR | ✅ | Unique identifier |
| *Name | VARCHAR | ✅ | Agreement name |
| Description | VARCHAR | | Description |
| Union | VARCHAR | | Union name |
| Bargaining Unit | VARCHAR | | Bargaining unit |
| Legal Employer | VARCHAR | | Legal employer code |
| Status | VARCHAR | | Processing status |
| Load Status | VARCHAR | | Load status |

**Sample Record:**
```
* Identification Code: FR_CCNTRANS
*Name: Convention Collective Nationale des Transports
*Country: FR
*Status: A
```

**Source:** Collective_Agreements_Template.csv
**Records:** 112

---

## 2. Personal Details

### 2.1 Gender

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Gender code (M/F/U) |
| Enabled | CHAR(1) | ✅ | Y/N |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Display name |
| Tag | VARCHAR | | Country tag |
| Load Status | VARCHAR | | Load status |
| Enable (Y/N) | CHAR(1) | | Enable flag |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
Lookup Code: M
Meaning: Male
Enabled: Y
```

**Source:** Standard Oracle values
**Records:** 3

---

### 2.2 Marital Statuses

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Status code |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Status name |
| Tag | VARCHAR | | Country tag |
| Enable (Yes/No) | VARCHAR | ✅ | Yes/No |
| Load Status | VARCHAR | | Load status |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
Lookup Code: M
Meaning: Married
Enable (Yes/No): Yes
```

**Source:** GenericLibrary.csv (SITFAM)
**Records:** 6

---

### 2.3 Titles

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Title code |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Title name |
| Tag | VARCHAR | | Country tag |
| (Yes/No) Enable | VARCHAR | ✅ | Yes/No |
| Load Status | VARCHAR | | Load status |

**Sample Record:**
```
Lookup Code: MR
Meaning: Mr
(Yes/No) Enable: Yes
```

**Source:** KeyPropertiesNewIE.csv (Title)
**Records:** 7

---

### 2.4 Highest Education Level

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Education level code |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Level name |
| Tag | VARCHAR | | Country tag |
| (Yes/No) Enable | VARCHAR | ✅ | Yes/No |
| Load Status | VARCHAR | | Load status |

**Sample Record:**
```
Lookup Code: BAC+5
Meaning: Master's Degree
(Yes/No) Enable: Yes
```

**Source:** GenericLibrary.csv (NIVEAUDIPLOME)
**Records:** 10

---

### 2.5 Document Category

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Category code |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Category name |
| Description | VARCHAR | | French name |
| Tag | VARCHAR | | Country tag |
| Enable | VARCHAR | | Enabled status |
| Status | VARCHAR | | SEEDED / CUSTOM |

**Sample Record (Seeded):**
```
Lookup Code: EMPMNT
Meaning: Employment
Enable: Cannot be disabled
Status: SEEDED
```

**Sample Record (Custom):**
```
Lookup Code: GEO_ONBOARD
Meaning: Onboarding
Enable: Yes
Status: CUSTOM
```

**Source:** Oracle Seeded (17) + GEODIS Custom (9)
**Records:** 26

---

### 2.6 Document Type

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Document type code |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Type name |
| Description | VARCHAR | | French name |
| Category Code | VARCHAR | ✅ | Parent category code |
| Parent Code | VARCHAR | | Parent type (for hierarchy) |
| Self Service | CHAR(1) | | Y/N for employee access |
| Enable | VARCHAR | ✅ | Yes/No |
| Source | VARCHAR | | G-Talent+ / Benchmark |

**Sample Record:**
```
Lookup Code: SYSTEM_TYPEOFDOCUMENTS_CONTRACT_32074
Meaning: Contracts
Category Code: EMPMNT
Self Service: N
Source: G-Talent+
```

**Source:** typeOfDocuments_referential.json + Benchmark recommendations
**Records:** 98

---

## 3. Workforce Structure

### 3.1 Job Family

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| * Job family name | VARCHAR | ✅ | Family display name |
| * Job Family Code | VARCHAR | ✅ | Unique code |
| Effective start date | DATE | ✅ | Start date |
| Effective end date | DATE | | End date |
| Active status (A / I) | CHAR(1) | ✅ | A or I |
| Load Status | VARCHAR | | Load status |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
* Job Family Code: 14PL0
* Job family name: 4PL Operations
Active status (A / I): A
```

**Source:** ActivitiesFunctions View.csv (L4 with active jobs)
**Records:** 27

---

### 3.2 Job Sub Family

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Sub family code |
| Display Sequence | NUMBER | | Sort order |
| Enabled | CHAR(1) | ✅ | Y/N |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Sub family name |
| Tag | VARCHAR | | Parent Job Family Code |
| Description | VARCHAR | | Description |
| Load Status | VARCHAR | | Load status |
| Status | VARCHAR | | Processing status |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
Lookup Code: 14PLO
Meaning: 4PL Operations (L2)
Tag: 14PL0 (parent Job Family)
Enabled: Y
```

**Source:** ActivitiesFunctions View.csv (L5 with active jobs)
**Records:** 79

---

### 3.3 Job Function

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Function code |
| Display Sequence | NUMBER | | Sort order |
| Enabled | CHAR(1) | ✅ | Y/N |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Function name |
| Tag | VARCHAR | | Parent Job Sub Family Code |
| Description | VARCHAR | | Description |
| Load Status | VARCHAR | | Load status |
| Status | VARCHAR | | Processing status |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
Lookup Code: Accountant Payable
Meaning: Accountant Payable
Tag: 2FIAC (parent Sub Family)
Enabled: Y
```

**Source:** JobRepositoryNewIE.csv (nodes with parent in AF L5)
**Records:** 236

---

### 3.4 Job

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Job Code | VARCHAR | ✅ | Unique job code |
| Active Status | CHAR(1) | ✅ | A/I |
| * Effective Start Date | DATE | ✅ | Start date |
| * Effective End Date | DATE | | End date |
| Job Name | VARCHAR | ✅ | Job display name |
| Job Set Code | VARCHAR | ✅ | Set code (COMMON) |
| Job family name | VARCHAR | | Job family reference |
| Job Function Code | VARCHAR | | Parent function code |
| Job Level | VARCHAR | | Job level |
| Management Level | VARCHAR | | Management level code |
| HRP Status | VARCHAR | | HRP status |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
Job Code: 2FIAC_ACPAOFCF
Job Name: Accounts Payable Officer Confirmed
Job Function Code: Accountant Payable
Management Level: CF
Active Status: A
```

**Source:** JobRepositoryNewIE.csv (active jobs with underscore)
**Records:** 688

---

### 3.5 Management Level

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Lookup Code | VARCHAR | ✅ | Level code |
| Display Sequence | NUMBER | | Sort order |
| Start Date | DATE | ✅ | Effective start |
| End Date | DATE | ✅ | Effective end |
| Meaning | VARCHAR | ✅ | Level name |
| Description | VARCHAR | | Description |
| Tag | VARCHAR | | Tag |
| Enabled | CHAR(1) | ✅ | Y/N |
| Status | VARCHAR | | Processing status |
| Load status | VARCHAR | | Load status |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
Lookup Code: M1
Meaning: Management level 1
Display Sequence: 3
Enabled: Y
```

**Source:** Derived from Job names (pattern matching)
**Records:** 5

---

### 3.6 Grade

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Effective Start date | DATE | ✅ | Start date |
| Grade Set Code | VARCHAR | ✅ | Set code (COMMON) |
| Grade Name | VARCHAR | ✅ | Grade display name |
| Grade code | VARCHAR | ✅ | Unique grade code |
| Active status | CHAR(1) | ✅ | A/I |
| Legislative Data Group associated | VARCHAR | | LDG reference |
| Grade Rate Name | VARCHAR | | Rate name |
| Grade Rate Type | VARCHAR | | Rate type |
| Grade Rate Frequency | VARCHAR | | Frequency |
| Grade Rate Annualization Factor | NUMBER | | Factor |
| Grade Rate Currency | VARCHAR | | Currency code |
| Grade Rate Minimum | NUMBER | | Min rate |
| Grade Rate Maximum | NUMBER | | Max rate |
| Grade Rate Midpoint | NUMBER | | Mid rate |
| Grade Rate Value | NUMBER | | Rate value |
| Load Status | VARCHAR | | Load status |
| Client Status | VARCHAR | | Client status |

**Sample Record:**
```
Grade code: P3
Grade Name: Professional Level 3
Grade Set Code: COMMON
Active status: A
```

**Source:** MERCER Job Library (Career Level Title)
**Records:** 20

---

### 3.7 Position

**Oracle HCM Column Structure:**
| Column | Type | Required | Description |
|--------|------|:--------:|-------------|
| Position Code | VARCHAR | ✅ | Unique position code |
| Position Name | VARCHAR | ✅ | Position display name |
| Effective Start Date | DATE | ✅ | Start date |
| Effective End Date | DATE | | End date |
| Active Status | CHAR(1) | ✅ | A/I |
| Job Code | VARCHAR | | Associated job code |
| Grade Code | VARCHAR | | Associated grade code |
| Position Family | VARCHAR | | Position family |
| Load Status | VARCHAR | | Load status |
| Comments | VARCHAR | | Notes |

**Sample Record:**
```
Position Code: FIN.02.003.P3
Position Name: Senior Accountant (P3)
Grade Code: P3
Active Status: A
```

**Source:** MERCER Job Library (Job Code + Job Title)
**Records:** 24,398

---

## 4. Mapping Compliance Summary

| Repository | Source File | Columns Match | Records | Status |
|------------|-------------|:-------------:|--------:|:------:|
| Contract Type | KeyPropertiesNewIE.csv | ✅ | 62 | OK |
| Manager Type | Organisations.csv | ✅ | 6 | OK |
| Worker Category | Standard values | ✅ | 4 | OK |
| Assignment Category | Standard values | ✅ | 4 | OK |
| Assignment Status | Standard values | ✅ | 4 | OK |
| Hourly-Salaried | Standard values | ✅ | 2 | OK |
| Regular or Temporary | Standard values | ✅ | 2 | OK |
| Seniority Rules | Standard values | ✅ | 3 | OK |
| Frequency Working Hours | GenericLibrary.csv | ✅ | 8 | OK |
| Collective Agreement | Collective_Agreements_Template.csv | ✅ | 112 | OK |
| Gender | Standard values | ✅ | 3 | OK |
| Marital Statuses | GenericLibrary.csv | ✅ | 6 | OK |
| Titles | KeyPropertiesNewIE.csv | ✅ | 7 | OK |
| Highest Education Level | GenericLibrary.csv | ✅ | 10 | OK |
| Document Category | Oracle Seeded + Custom | ✅ | 26 | OK |
| Document Type | typeOfDocuments_referential.json | ✅ | 98 | OK |
| Job Family | ActivitiesFunctions View.csv | ✅ | 27 | OK |
| Job Sub Family | ActivitiesFunctions View.csv | ✅ | 79 | OK |
| Job Function | JobRepositoryNewIE.csv | ✅ | 236 | OK |
| Job | JobRepositoryNewIE.csv | ✅ | 688 | OK |
| Management Level | Derived from Job names | ✅ | 5 | OK |
| Grade | MERCER Job Library | ✅ | 20 | OK |
| Position | MERCER Job Library | ✅ | 24,398 | OK |

---

## 5. Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-06 | Claude Code | Initial schema documentation |

---

*This document serves as the master reference for Oracle HCM repository column structures.*
