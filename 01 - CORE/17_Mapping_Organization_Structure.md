# Organization Structure - Source to Target Mapping

**Project:** GEODIS New HCM - AMARIS
**Phase:** 02 - Define
**Created:** 2025-12-06
**Purpose:** Document source-to-target mapping for Organization Structure repositories

---

## 1. Methodology

### 1.1 Approach

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 1: DISCOVERY                                                         │
│  ├── Identify target repositories (16 Organization Structure files)         │
│  ├── Identify source files (MDM MAB, MDM HR, MDM SITES)                     │
│  └── Document source file structures                                        │
├─────────────────────────────────────────────────────────────────────────────┤
│  PHASE 2: MAPPING DEFINITION                                                │
│  ├── Define source-to-target column mapping                                 │
│  ├── Document transformation rules                                          │
│  ├── Provide sample data for validation                                     │
│  └── USER VALIDATION CHECKPOINT                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│  PHASE 3: DATA POPULATION                                                   │
│  ├── Extract from source files                                              │
│  ├── Transform according to mapping rules                                   │
│  ├── Load into target Excel files                                           │
│  └── Quality check                                                          │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 1.2 Validation Rules

Before populating any repository:
1. Column mapping must be documented
2. Sample data (3-5 records) must be shown
3. User must confirm mapping is correct
4. Only then proceed with full data load

---

## 2. Progress Tracker

| # | Repository | Source Identified | Mapping Defined | User Validated | Populated | Records |
|---|------------|:-----------------:|:---------------:|:--------------:|:---------:|--------:|
| 1 | Country Code | ✅ Oracle Seeded | N/A | N/A | ⬜ | - |
| 2 | Geography | ✅ Oracle Seeded | N/A | N/A | ⬜ | - |
| 3 | Enterprise HCM | ✅ Manual | ⬜ | ⬜ | ⬜ | 1 |
| 4 | Legislative Data Group | ✅ Derived | ⬜ | ⬜ | ⬜ | TBD |
| 5 | Legal Address | ✅ Legal Sites.csv | ⬜ | ⬜ | ⬜ | TBD |
| 6 | Legal Entity | ✅ Legal Entities View.csv | ⬜ | ⬜ | ⬜ | ~300 |
| 7 | **Division** | ✅ Business Hierarchy.csv (L2) | ⬜ | ⬜ | ⬜ | 21 |
| 8 | **Business Unit** | ✅ SOUs View.csv | ⬜ | ⬜ | ⬜ | ~2,500 |
| 9 | Data Set | ✅ Manual | ⬜ | ⬜ | ⬜ | TBD |
| 10 | BU Set Assignment | ✅ Derived | ⬜ | ⬜ | ⬜ | TBD |
| 11 | **Department** | ✅ HubLibraries_Departments.json | ⬜ | ⬜ | ⬜ | 21,834 |
| 12 | Department Tree | ✅ HubLibraries_Departments.json | ⬜ | ⬜ | ⬜ | TBD |
| 13 | Organization Tree | ✅ Organisations.csv | ⬜ | ⬜ | ⬜ | TBD |
| 14 | Location | ✅ Site View.csv + Address View.csv | ⬜ | ⬜ | ⬜ | TBD |
| 15 | Reporting Establishment | ✅ Legal Sites.csv | ⬜ | ⬜ | ⬜ | TBD |
| 16 | Time Zone | ✅ Oracle Seeded | N/A | N/A | ⬜ | - |

**Legend:** ✅ Complete | ⬜ Pending | ❌ Blocked

---

## 3. Source Files Inventory

### 3.1 MDM MAB (01 - MDM MAB)

| File | Size | Records | Key Use |
|------|------|---------|---------|
| **Business Hierarchy.csv** | 2.9 KB | 44 | Division (L2) |
| **SOUs View.csv** | 389.5 KB | ~2,500 | Business Unit |
| **Legal Entities View.csv** | 121.3 KB | ~300 | Legal Entity |
| **Legal Sites.csv** | 294.9 KB | - | Legal Address, Reporting Establishment |
| Reporting Units View.csv | 106.5 KB | - | Reference |
| Managerial Hierarchy.csv | 34.9 KB | - | Reference |
| Local SOUs.csv | 472.5 KB | - | Cost Allocation |
| Systems.csv | 1.4 KB | - | Source System Owner |

### 3.2 MDM HR (02 - MDM HR)

| File | Size | Records | Key Use |
|------|------|---------|---------|
| **HubLibraries_Departments.json** | 15.1 MB | 21,834 | Department |
| **Organisations.csv** | 20.4 MB | - | Organization Tree |
| KeyPropertiesNewIE.csv | 5.8 MB | - | Reference values |
| JobRepositoryNewIE.csv | 9.3 MB | - | Job (Workforce) |

### 3.3 MDM SITES (03 - MDM SITES)

| File | Size | Records | Key Use |
|------|------|---------|---------|
| **Site View.csv** | 77.3 KB | - | Location |
| **Address View.csv** | 75.5 KB | - | Location addresses |

---

## 4. Source File Structures

### 4.1 Business Hierarchy.csv (Division Source)

**Delimiter:** Semicolon (;)
**Encoding:** UTF-8

| Column | Description | Sample |
|--------|-------------|--------|
| LoB Code | Division code | FFAM, CLNE |
| Name | Full name | Freight Forwarding AMERICAS |
| Short name | Abbreviation | GFF |
| Hierarchy level | L0, L1, L2, L3, L4 | L2 |
| Parent Code | Parent LoB | FF |
| Activation Date | Start date | - |
| Deactivation Date | End date | - |
| Status Calculated | ACTIVATED / DEACTIVATED | ACTIVATED |

**Filter for Division:** `Hierarchy level = L2` AND `Status Calculated = ACTIVATED`

**L2 Records (21 ACTIVATED):**

| LoB Code | Name | Parent (L1) |
|----------|------|-------------|
| CLAM | Contract Logistics AMERICAS exc. NIND | CL |
| CLAP | Contract Logistics APAC Historical | CL |
| CLDHO | Contract Logistics - DHO | CL |
| CLFR | Contract Logistics FRANCE | CL |
| CLGL | Geodis Logistics | CL |
| CLNE | Contract Logistics EUROPE | CL |
| CLNIND | NIND | CL |
| DEFR | D&E - France & Holding hors UK | DE |
| DEUK | D&E UK | DE |
| FFAM | Freight Forwarding AMERICAS | FF |
| FFAP | Freight Forwarding APAC | FF |
| FFDHO | Freight Forwarding DHO | FF |
| FFFRE | Freight Forwarding FRANCE Region | FF |
| FFNE | Freight Forwarding EUROPE | FF |
| NOCORP | Corporate | NO |
| NORE | Corporate Real Estate | NO |
| NOTOP | Corporate Top Packages | NO |
| RTGRNB | SCOPE GRN | RT |
| RTNPH | NEW HISTORICAL PERIMETER | RT |

---

### 4.2 SOUs View.csv (Business Unit Source)

**Delimiter:** Semicolon (;)
**Encoding:** UTF-8

| Column | Description | Sample |
|--------|-------------|--------|
| SOU Code | Unique SOU identifier | 76COD01, 9SBOL01 |
| SOU Digits | Numeric part | - |
| Name | SOU description | - |
| Type | Operational / Support / Technical | Operational |
| Reporting Unit Code | Link to reporting unit | - |
| BOF site code | Site reference | - |
| Managerial Parent Code | Managerial hierarchy | - |
| Management Line Code | Management line | - |
| Business Parent Code | Business hierarchy (LoB) | FF, CL |
| Alpha-2 Country Code | Country | DE, FR, US |
| UN LOCODE | Location code | - |
| Legal Entity Code - DILITRUST | Legal entity reference | - |
| Country Subdivision Code | Region/State | - |
| Historical LoB Code | Legacy LoB | - |
| Site ID | Site reference | - |
| SOU Responsible | Owner | - |
| Activation Date | Start date | - |
| Deactivation Date | End date | - |
| Status Calculated | ACTIVATED / DEACTIVATED | ACTIVATED |

**Filter for Business Unit:** `Status Calculated = ACTIVATED`

---

### 4.3 HubLibraries_Departments.json (Department Source)

**Format:** JSON Array (pivoted structure)
**Encoding:** UTF-8
**Total Records:** 89,585 rows → 21,834 unique departments

**Raw Structure (each row = one field value):**

| Column | Description |
|--------|-------------|
| Library | Always "OrganisationalStructure" |
| ClientCode | Department ID |
| Field | Field name |
| Value | Field value |
| StartEffectDate | Effective date |
| Culture | Language (en-gb) |

**Pivoted Structure (one row per department):**

| Field | Description | Sample |
|-------|-------------|--------|
| ClientCode | Department ID | 10002085 |
| ShortName | Department name | APAC - SEA - Indonesia - Batam - SF |
| FullName | Full name (rare) | - |
| ParentClientCode | Parent department | 10003166 |
| IsActive | Y/N | Y |
| ManagerUniqueID | Manager reference | - |
| CostCenterClientCodes | Cost center link | - |

**Filter for Department:** `IsActive = Y`

---

### 4.4 Legal Entities View.csv (Legal Entity Source)

**Delimiter:** Semicolon (;)
**Encoding:** UTF-8

| Column | Description |
|--------|-------------|
| Legal Entity Code - EBX | EBX code |
| Legal Entity Code - DILITRUST | Dilitrust code |
| Legal Entity Name | Name |
| Country | Country code |
| Currency | Currency code |
| Registration ID | Registration number |
| Code APE/NAF | French activity code |
| Legal form | Legal form |
| Registration Date | Registration date |
| City of registration | City |
| Tax ID | Tax identifier |
| Address | Address |
| Activation Date | Start date |
| Deactivation Date | End date |
| Status Calculated | ACTIVATED / DEACTIVATED |

---

## 5. Column Mappings

### 5.1 Division Mapping

**Source:** Business Hierarchy.csv (L2, ACTIVATED)
**Target:** Division.xlsx

| # | Target Column | Source Column | Transformation | Required |
|---|---------------|---------------|----------------|:--------:|
| 1 | * Name (Eng) | Name | Direct | ✅ |
| 2 | Name (FR) | Name | Same (no FR available) | |
| 3 | * Effective Start Date | Activation Date | Default: 2000-01-01 | ✅ |
| 4 | Internal Address Line | - | Empty | |
| 5 | * Status | Status Calculated | ACTIVATED → A | ✅ |
| 6 | Action Reason | - | Empty | |
| 7 | Location | - | Empty | |
| 8 | Address | - | Empty | |
| 9 | Reporting Name | Short name | If available | |
| 10 | Manager | - | Empty | |
| 11 | Load Status | - | Empty | |
| 12 | Client Status | - | Empty | |

**Sample Output (3 records):**

| * Name (Eng) | Name (FR) | * Effective Start Date | * Status |
|--------------|-----------|------------------------|----------|
| Contract Logistics AMERICAS exc. NIND | Contract Logistics AMERICAS exc. NIND | 2000-01-01 | A |
| Freight Forwarding AMERICAS | Freight Forwarding AMERICAS | 2000-01-01 | A |
| Freight Forwarding EUROPE | Freight Forwarding EUROPE | 2000-01-01 | A |

**⏳ AWAITING USER VALIDATION**

---

### 5.2 Business Unit Mapping

**Source:** SOUs View.csv (ACTIVATED)
**Target:** Business Unit.xlsx

| # | Target Column | Source Column | Transformation | Required |
|---|---------------|---------------|----------------|:--------:|
| 1 | * Name | Name or SOU Code | Direct | ✅ |
| 2 | Location | UN LOCODE | If available | |
| 3 | Manager | SOU Responsible | If available | |
| 4 | * Default Set | - | "Common Set" | ✅ |
| 5 | Load Status | - | Empty | |
| 6 | Status | Status Calculated | ACTIVATED → Active | |

**Sample Output (TBD after source data review):**

**⏳ AWAITING USER VALIDATION**

---

### 5.3 Department Mapping

**Source:** HubLibraries_Departments.json (IsActive = Y)
**Target:** Department.xlsx

| # | Target Column | Source Column | Transformation | Required |
|---|---------------|---------------|----------------|:--------:|
| 1 | * Department name | ShortName | Direct | ✅ |
| 2 | Department Set Code* | - | "Common Set" | ✅ |
| 3 | Status (A or I)* | IsActive | Y → A, N → I | ✅ |
| 4 | * Effective Start Date | StartEffectDate | Direct | ✅ |
| 5 | Effective End Date | - | Empty | |
| 6 | Parent Name | ParentClientCode | Lookup ShortName | |
| 7 | Location | - | Empty | |
| 8 | Reporting Name | - | Empty | |
| 9 | Manager | ManagerUniqueID | If available | |
| 10 | Record Identifier | ClientCode | Department ID | |
| 11-14 | Cost Center fields | CostCenterClientCodes | If available | |
| 15-18 | Working Hours | - | Empty | |

**Sample Output (TBD after source data review):**

**⏳ AWAITING USER VALIDATION**

---

## 6. Validation Checkpoints

### Checkpoint 1: Division
- [ ] Column mapping confirmed
- [ ] Sample data approved
- [ ] Proceed with population

### Checkpoint 2: Business Unit
- [ ] Column mapping confirmed
- [ ] Sample data approved
- [ ] Proceed with population

### Checkpoint 3: Department
- [ ] Column mapping confirmed
- [ ] Sample data approved
- [ ] Proceed with population

### Checkpoint 4: Legal Entity
- [ ] Column mapping confirmed
- [ ] Sample data approved
- [ ] Proceed with population

### Checkpoint 5: Location
- [ ] Column mapping confirmed
- [ ] Sample data approved
- [ ] Proceed with population

---

## 7. Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-06 | Claude Code | Initial mapping documentation |

---

*This document tracks the source-to-target mapping for Organization Structure repositories.*
