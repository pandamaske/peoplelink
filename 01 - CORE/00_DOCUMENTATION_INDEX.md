# GEODIS HCM Implementation - Documentation Index

**Project:** GEODIS New HCM - AMARIS
**Phase:** 02 - Define
**Last Updated:** 2025-12-07
**Status:** Complete - 70 Files | 58,460 Records | Documentation Aligned

---

## Quick Navigation

| # | Document | Purpose | Status |
|---|----------|---------|--------|
| 00 | [DOCUMENTATION_INDEX](#00-documentation-index) | This file - start here | Current |
| 01 | [Agent_Session_Tracker](#01-agent-session-tracker) | Session context & progress | Active |
| 02 | [Oracle_HCM_Dimensions_Reference](#02-oracle-hcm-dimensions-reference) | Master HCM dimensions | Complete |
| 03 | [MDM_to_HCM_Mapping](#03-mdm-to-hcm-mapping) | Source to target mapping | Complete |
| 04 | [Mercer_Grade_Mapping](#04-mercer-grade-mapping) | Grade structure & comp | Complete |
| 05 | [Implementation_Methodology](#05-implementation-methodology) | 7-phase methodology | Complete |
| 06 | [Repository_Configuration_Guide](#06-repository-configuration-guide) | Detailed repository specs | Complete |
| 07 | [MDM_HR_Mapping_Refinement](#07-mdm-hr-mapping-refinement) | HR MDM analysis | Complete |
| 08 | [Oracle_Documentation_Index](#08-oracle-documentation-index) | Oracle docs reference | Complete |
| 09 | [MDM_HR_Analysis_Report](#09-mdm-hr-analysis-report) | MDM HR folder analysis | Complete |
| 10 | [Open_Decisions_Checklist](#10-open-decisions-checklist) | Pending decisions | Active |
| 11 | [Core_HR_Consistency_Audit](#11-core-hr-consistency-audit) | Data quality audit | Complete |
| 12 | [Global_Analytical_Allocation_Model](#12-global-analytical-allocation-model) | ~~Archived~~ (see 14) | Archived |
| 13 | [MDM_MAB_Analysis_Report](#13-mdm-mab-analysis-report) | MDM MAB files analysis | Complete |
| 14 | [Multialocation_MAB](#14-multialocation-mab) | **MASTER**: Allocation + Governance | Complete |
| 15 | [Documentation_Architecture](#15-documentation-architecture) | How all docs fit together | Complete |
| 16 | [Repository_Population_Methodology](#16-repository-population-methodology) | 4-phase repo methodology | Complete |
| 17 | [Mapping_Organization_Structure](#17-mapping-organization-structure) | Org structure mapping | Complete |
| 18 | [Role_Rationalization_Analysis](#18-role-rationalization-analysis) | Role analysis (43→18 roles) | Complete |
| 19 | [Repository_Schema_Reference](#19-repository-schema-reference) | Oracle HCM column structures | Complete |
| 20 | [GEODIS_HR_Workflows_Catalog](#20-geodis-hr-workflows-catalog) | HR business process workflows | **v1.0** |
| 21 | [GTalent_to_Oracle_HCM_Mapping](#21-gtalent-to-oracle-hcm-mapping) | G-Talent+ to Oracle mapping | Complete |
| 22 | [Oracle_HCM_Approval_Workflows](#22-oracle-hcm-approval-workflows) | Approval workflow specs | Complete |
| 23 | [GEODIS_HCM_Gap_Register](#23-geodis-hcm-gap-register) | Gap register (50 gaps) | Active |
| 24 | [Oracle_HCM_Configuration_Specifications](#24-oracle-hcm-configuration-specifications) | Configuration specs | Complete |
| 25 | [UKG_Talentsoft_to_Oracle_HCM_Mapping](#25-ukg-talentsoft-to-oracle-hcm-mapping) | Source system field mapping | Complete |
| 26 | [Documentation_Consistency_Audit](#26-documentation-consistency-audit) | Cross-reference audit report | **NEW** |

**Supporting Files:**
- `flowchart.md` - Mermaid diagram
- `Oracle_HCM_Structure_Diagram.md` - HCM architecture diagrams

---

## Document Details

### 00 DOCUMENTATION INDEX
**File:** `00_DOCUMENTATION_INDEX.md`
**Purpose:** Master navigation and table of contents
**Use when:** Starting any session, finding documentation

---

### 01 Agent Session Tracker
**File:** `01_Agent_Session_Tracker.md`
**Purpose:** Session progress tracker and implementation context
**Content:**
- Domain knowledge & expertise areas
- MDM MAB Architecture & Governance
- Final repository population summary
- Session history
- Resume prompt for continuity

**Use when:** Starting a new session, tracking progress

---

### 02 Oracle HCM Dimensions Reference
**File:** `02_Oracle_HCM_Dimensions_Reference.md`
**Purpose:** Master reference for Oracle HCM structural dimensions
**Content:**
- All 10+ HCM dimensions (Enterprise, Legal Entity, LDG, Division, BU, Department, Location, Job, Position, Grade)
- Authoritative sources per dimension
- Configuration instructions
- Governance rules & design principles

**Use when:** Understanding Oracle HCM structure, validating design decisions

---

### 03 MDM to HCM Mapping
**File:** `03_MDM_to_HCM_Mapping.md`
**Purpose:** Maps MDM MAB & HR sources to Oracle HCM targets
**Content:**
- Target IT Architecture (EBX, BAW, Datalayer)
- SOU cornerstone concept and code structure
- MDM Tables overview from EBX
- Governance roles (GDDO, GDDS, LRDS)
- Field-level mappings for all dimensions

**Use when:** Planning data migration, understanding source-target relationships

---

### 04 Mercer Grade Mapping
**File:** `04_Mercer_Grade_Mapping.md`
**Purpose:** Complete Mercer IPE grade structure for Oracle HCM
**Content:**
- Grade bands (G40-G74)
- Position Class to Grade mapping
- Compensation data by grade
- Job-to-Grade mapping logic
- HDL sample files

**Use when:** Configuring grades, grade rates, salary basis

---

### 05 Implementation Methodology
**File:** `05_Implementation_Methodology.md`
**Purpose:** Oracle Fusion HCM implementation approach
**Content:**
- 7-phase implementation sequence
- 64 repositories across 6 categories
- RACI matrix
- Configuration workstreams

**Use when:** Understanding implementation approach, sequencing tasks

---

### 06 Repository Configuration Guide
**File:** `06_Repository_Configuration_Guide.md`
**Purpose:** Detailed specifications for each repository
**Content:**
- All 6 repository categories with detailed specs
- Oracle attributes and configuration options
- GEODIS-specific design decisions

**Use when:** Configuring specific repositories

---

### 07 MDM HR Mapping Refinement
**File:** `07_MDM_HR_Mapping_Refinement.md`
**Purpose:** Critical findings from MDM HR folder analysis
**Content:**
- JobRepositoryNewIE.csv analysis
- ValuesListLibrary.csv mappings
- KeyPropertiesNewIE.csv structure
- Data transformation updates

**Use when:** Understanding HR data sources

---

### 08 Oracle Documentation Index
**File:** `08_Oracle_Documentation_Index.md`
**Purpose:** Quick reference to Oracle PDF documentation
**Content:**
- Mapping from repositories to Oracle PDFs
- Cross-cutting documentation references
- Full catalog of Oracle docs (41 PDFs)

**Use when:** Finding Oracle documentation for specific topics

---

### 09 MDM HR Analysis Report
**File:** `09_MDM_HR_Analysis_Report.md`
**Purpose:** Analysis of MDM HR folder files
**Content:**
- 12 files analyzed (~114 MB, 1.2M records)
- Detailed file structure and statistics
- Key findings for HCM implementation

**Use when:** Understanding MDM HR data structure

---

### 10 Open Decisions Checklist
**File:** `10_Open_Decisions_Checklist.md`
**Purpose:** Track resolved and pending business decisions
**Content:**
- Resolved decisions (Organization, Workforce, Compensation)
- Pending decisions requiring confirmation
- Next steps

**Use when:** Reviewing what needs business confirmation

---

### 11 Core HR Consistency Audit
**File:** `11_Core_HR_Consistency_Audit.md`
**Purpose:** Data quality audit report
**Content:**
- Cross-reference integrity checks
- Legal Entity validations
- Location and Department checks
- Remediation recommendations

**Use when:** Validating data quality

---

### 12 Global Analytical Allocation Model (ARCHIVED)
**File:** `12_Global_Analytical_Allocation_Model.md`
**Status:** ARCHIVED - Content merged into document 14
**Purpose:** Multi-ERP employee cost allocation model

**Use when:** See document 14 (Multialocation_MAB) instead

---

### 13 MDM MAB Analysis Report
**File:** `13_MDM_MAB_Analysis_Report.md`
**Purpose:** Analysis of MDM Management Accounting Blueprint files
**Content:**
- 15 CSV files analyzed (~3.9 MB)
- SOUs, Local SOUs, Analytical Mapping structure
- Systems/ERP list
- Activities, Products, Legal Entities
- Integration with Global Analytical Allocation Model

**Use when:** Understanding MAB data sources, cost allocation setup

---

### 14 Multialocation MAB (MASTER)
**File:** `14_Multialocation_MAB.md`
**Purpose:** **CONSOLIDATED MASTER** - Complete allocation model + governance
**Content:**
- **Sections 0-8:** Global Analytical Allocation Model
  - Key concepts (SOU, Local SOU, Analytical IDs, CoA)
  - Two-level allocation (Level A: SOU split, Level B: Analytical split)
  - Final allocation formula: `Final_% = Local_Sou_% × Analytical_% ÷ 100`
  - Canonical Global Analytical Allocation table structure
  - Mapping to Oracle GL & HCM Payroll Costing
  - FTE KPIs integration
  - Worked example (multi-ERP, 5 analytical lines)
- **Section 12:** Governance of Analytical IDs

**Use when:** Configuring payroll costing, multi-ERP allocations, governance model

---

### 15 Documentation Architecture
**File:** `15_Documentation_Architecture.md`
**Purpose:** Meta-documentation explaining how all docs fit together
**Content:**
- Four-layer documentation model (Meta, Design, Sources, Advanced)
- Recommended reading paths by audience
- Document dependency matrix
- Strengths summary & gap analysis

**Use when:** Onboarding new team members, understanding doc relationships

---

### 16 Repository Population Methodology
**File:** `16_Repository_Population_Methodology.md`
**Purpose:** Master methodology for populating all 69 HCM repositories
**Content:**
- 4-phase approach: Source Identification → Column Mapping → Sample Validation → Full Population
- 6 iterations covering all repository categories
- Validation checkpoints and quality rules

**Use when:** Planning data population, understanding methodology

---

### 17 Mapping Organization Structure
**File:** `17_Mapping_Organization_Structure.md`
**Purpose:** Source-to-target mapping for Organization Structure repositories
**Content:**
- 16 Organization Structure repositories
- Source file identification (MDM MAB, HR, SITES)
- Column-by-column mapping

**Use when:** Populating Organization Structure repositories

---

### 18 Role Rationalization Analysis
**File:** `18_Role_Rationalization_Analysis.md`
**Purpose:** Analysis of G-Talent+ roles for Oracle HCM security design
**Content:**
- 138,303 user-role assignments analyzed
- 43 current roles → ~18 target roles (58% reduction)
- Usage tier analysis (High/Medium/Low)
- Role-to-Oracle mapping recommendations

**Use when:** Designing security roles, planning role migration

---

### 19 Repository Schema Reference
**File:** `19_Repository_Schema_Reference.md`
**Purpose:** Oracle HCM column structures and sample values
**Content:**
- Column definitions for each repository type
- Required fields marked
- Sample records
- Source mapping references

**Use when:** Understanding Oracle HCM field structures

---

### 20 GEODIS HR Workflows Catalog
**File:** `20_GEODIS_HR_Workflows_Catalog.md`
**Version:** 1.0
**Purpose:** Consolidated HR business process workflows and synthesis
**Content:**
- **Source Documents Reviewed:**
  - HR Blueprint: 8 PDFs + 8 Mermaid diagrams
  - Zendesk US Processes: 25 workflow documents (12 processes)
  - Talentsoft Guidelines: 44 files (20+ guides)
  - Onboarding Workshops PDF: 35 pages
- **9 Process Domains:**
  - Recruitment & Talent Acquisition
  - Onboarding & Preboarding (incl. UES France ServiceNow pilot)
  - Employee Lifecycle & Administration
  - Performance Management
  - Compensation & Benefits
  - Leave Management
  - Talent Management & Development
  - Termination & Offboarding
  - Payroll & Administration
- **Security Matrix:** 9 GEODIS roles, 308 data objects
- **Actions:** 41 GEODIS-specific action codes
- **Approval Workflows:** 31 workflows with approver chains
- **Gap Analysis:** Cross-checked with CORE HR Template

**Use when:** Understanding current HR processes, mapping to Oracle HCM

---

### 21 GTalent to Oracle HCM Mapping
**File:** `21_GTalent_to_Oracle_HCM_Mapping.md`
**Purpose:** Detailed mapping from G-Talent+ modules to Oracle HCM Cloud
**Content:**
- Module-by-module mapping (Core HR, Recruitment, Performance, etc.)
- Object-level correspondence
- Functional gap identification
- Migration considerations

**Use when:** Planning G-Talent+ to Oracle migration, understanding equivalences

---

### 22 Oracle HCM Approval Workflows
**File:** `22_Oracle_HCM_Approval_Workflows.md`
**Purpose:** Detailed approval workflow specifications for Oracle BPM
**Content:**
- 31 approval workflows by module
- Approver chain definitions
- Threshold rules (€125k, TOPEX, etc.)
- Conditional routing logic
- Escalation rules

**Use when:** Configuring Oracle BPM approval workflows

---

### 23 GEODIS HCM Gap Register
**File:** `23_GEODIS_HCM_Gap_Register.md`
**Purpose:** Comprehensive gap register tracking current vs. target state
**Content:**
- 50 gaps identified across all modules
- Gap severity classification (Critical, High, Medium, Low)
- Remediation recommendations
- Owner assignments
- Status tracking

**Use when:** Tracking implementation gaps, prioritizing remediation

---

### 24 Oracle HCM Configuration Specifications
**File:** `24_Oracle_HCM_Configuration_Specifications.md`
**Purpose:** Detailed configuration specifications for Oracle HCM Cloud
**Content:**
- Module-specific configuration parameters
- Flex field definitions
- Value set configurations
- Lookup type specifications
- Profile option settings

**Use when:** Configuring Oracle HCM Cloud setup tasks

---

### 25 UKG Talentsoft to Oracle HCM Mapping
**File:** `25_UKG_Talentsoft_to_Oracle_HCM_Mapping.md`
**Version:** 1.0
**Purpose:** Field-level mapping from UKG and Talentsoft to Oracle HCM Cloud
**Content:**
- **UKG (US Operations):**
  - 1,617 fields analyzed
  - 180 Core HR fields mapped
  - 420 LDG/Country-specific fields (US)
  - 850 Payroll/T&A fields
  - 47 gaps identified
- **Talentsoft (Global):**
  - 427 fields analyzed
  - 285 Core HR fields mapped
  - 45 LDG-specific fields
  - 35 Payroll fields
  - 28 gaps identified
- **Gap Analysis:**
  - Multi-manager types (HR Manager, Travel Approver, etc.)
  - Cost allocation (multi-ERP)
  - Country-specific fields (France L0/L1/L2, Chile AFP)
  - Medical/Occupational health fields
- **Recommendations:**
  - Person DFF configuration
  - Assignment DFF configuration
  - LDG configuration by country
  - Data migration priority

**Use when:** Planning data migration, configuring Oracle HCM fields, understanding source-to-target mapping

---

### 26 Documentation Consistency Audit
**File:** `26_Documentation_Consistency_Audit.md`
**Version:** 1.0
**Purpose:** Cross-reference audit of all documentation vs actual Excel counts
**Content:**
- **Actual Record Counts:**
  - 70 Excel files analyzed in 04 - SHEETS
  - 58,460 total records (verified)
- **Discrepancy Analysis by Document:**
  - 01_Agent_Session_Tracker.md: 13 fields updated
  - 16_Repository_Population_Methodology.md: 4 fields updated
  - 17_Mapping_Organization_Structure.md: 2 fields updated
  - 19_Repository_Schema_Reference.md: 1 field updated
- **Key Changes:**
  - Business Unit: 27 → 2,175 (SOUs View source)
  - Job Family: 842 → 27 (4-level hierarchy restructure)
  - Job: 334 → 688 (active leaves only)
- **Grand Total Summary:**
  - Organization Structure: 16 files, 31,453 records
  - Workforce Structure: 9 files, 25,453 records
  - Personal Details: 24 files, 150 records
  - Employment Details: 10 files, 296 records
  - Compensation Details: 6 files, 53 records
  - Process and Security: 5 files, 1,055 records

**Use when:** Validating documentation accuracy, verifying record counts

---

## Process & Security Sheets (04 - SHEETS)

### Overview (Verified 2025-12-07)
| Category | Files | Records | Status |
|----------|------:|--------:|--------|
| Organization Structure | 16 | 31,453 | Complete |
| Workforce Structure | 9 | 25,453 | Complete |
| Personal Details | 24 | 150 | Complete |
| Employment Details | 10 | 296 | Complete |
| Compensation Details | 6 | 53 | Complete |
| Process and Security | 5 | 1,055 | Complete |
| **TOTAL** | **70** | **58,460** | **Verified** |

### Process and Security Files

| File | Content | Records | Last Updated |
|------|---------|---------|--------------|
| `Security Matrix.xlsx` | Role-based access matrix (9 GEODIS roles) | 308 objects | 2025-12-06 |
| `Action.xlsx` | GEODIS-specific HR action codes | 41 actions | 2025-12-06 |
| `Action & Reasons.xlsx` | Action reason codes | 67 reasons | 2025-12-06 |
| `Approval Workflows.xlsx` | BPM approval workflow definitions | 31 workflows | 2025-12-06 |
| `Core Data Model.xlsx` | Core HR data model reference | - | - |

**Security Matrix Roles (Columns 3-9):**

| Column | Role | Description |
|--------|------|-------------|
| 3 | Employee (GEODIS) | Self-service access |
| 4 | Line Manager (GEODIS) | Direct/indirect reports management |
| 5 | HR Business Partner (GEODIS) | Local/Regional HR operations |
| 6 | Recruiter (GEODIS) | Recruitment operations |
| 7 | HR Administrator (GEODIS) | HR Admin operations |
| 8 | Pending Worker (GEODIS) | Pre-hire preboarding access |
| 9 | Contingent Worker (GEODIS) | External worker limited access |

### Organization Structure Files (16)

| File | Content |
|------|---------|
| `Enterprise HCM.xlsx` | Enterprise definition |
| `Legislative Data Group.xlsx` | LDG definitions |
| `Legal Entity.xlsx` | Legal entities |
| `Legal Address.xlsx` | Legal entity addresses |
| `Division.xlsx` | Division hierarchy |
| `Business Unit.xlsx` | Business units |
| `Department.xlsx` | Departments |
| `Department Tree.xlsx` | Department hierarchy |
| `Organization Tree.xlsx` | Organization hierarchies |
| `Location.xlsx` | Physical locations |
| `Reporting Establishment.xlsx` | Reporting establishments |
| `Data Set.xlsx` | Data sets |
| `BU Set Assignment.xlsx` | BU set assignments |
| `Country Code.xlsx` | Country codes |
| `Geography.xlsx` | Geographic hierarchy |
| `Time Zone.xlsx` | Time zones |

### Personal Details Files (22)

| File | Content |
|------|---------|
| `Address Format.xlsx` | Address formats by country |
| `Address Type.xlsx` | Address types |
| `Citizenship Status.xlsx` | Citizenship statuses |
| `Contact.xlsx` | Contact types |
| `Correspondence Language.xlsx` | Languages |
| `Document Category.xlsx` | Document categories |
| `Document Type.xlsx` | Document types |
| `Driver Licence.xlsx` | Driver license types |
| `E-Mail Type.xlsx` | Email types |
| `Gender.xlsx` | Gender values |
| `Highest Education Level.xlsx` | Education levels |
| `Mandat type.xlsx` | Mandate types |
| `Marital Statuses.xlsx` | Marital statuses |
| `Name Formats.xlsx` | Name formats |
| `Name Styles.xlsx` | Name styles |
| `National ID.xlsx` | National ID types |
| `Passport.xlsx` | Passport types |
| `Person Identifier Type for Ext.xlsx` | External ID types |
| `Person Type.xlsx` | Person types |
| `Phone Type.xlsx` | Phone types |
| `Source System Owner.xlsx` | Source systems |
| `Statutory Dependent.xlsx` | Dependent types |
| `Titles.xlsx` | Titles |
| `Visa & Permits.xlsx` | Visa/permit types |

### Employment Details Files (12)

| File | Content |
|------|---------|
| `Assignment Category.xlsx` | Assignment categories |
| `Assignment Status.xlsx` | Assignment statuses |
| `Collective Agreement.xlsx` | Collective agreements |
| `Contract Type.xlsx` | Contract types |
| `Frequency Working Hours.xlsx` | Working hour frequencies |
| `Hourly-Salaried.xlsx` | Hourly/salaried indicators |
| `Manager Type.xlsx` | Manager types |
| `Regular or Temporary.xlsx` | Regular/temporary indicators |
| `Seniority Rules.xlsx` | Seniority calculation rules |
| `Worker Category.xlsx` | Worker categories |

### Workforce Structure Files (9)

| File | Content |
|------|---------|
| `Job.xlsx` | Job catalog |
| `Job Family.xlsx` | Job families |
| `Job Sub Family.xlsx` | Job sub-families |
| `Job Function.xlsx` | Job functions |
| `Grade.xlsx` | Grades (Mercer IPE) |
| `Grade Step.xlsx` | Grade steps |
| `Position.xlsx` | Positions |
| `Management Level.xlsx` | Management levels |
| `Currencies.xlsx` | Currency codes |

### Compensation Details Files (6)

| File | Content |
|------|---------|
| `Salary Basis.xlsx` | Salary basis definitions |
| `Frequence Salary.xlsx` | Salary frequencies |
| `Comp. Elements.xlsx` | Compensation elements |
| `Compensation History.xlsx` | Compensation history |
| `Individual Compensation Plan.xlsx` | Individual comp plans |
| `Payroll Relationship.xlsx` | Payroll relationships |

---

## Data Sources

### MDM MAB Files (01 - MDM MAB) - 15 files

| Source | Size | Key Content |
|--------|------|-------------|
| `SOUs View.csv` | 390 KB | Global SOUs |
| `Local SOUs.csv` | 473 KB | Local SOUs per ERP |
| `Legal Entities View.csv` | 121 KB | Legal entities |
| `Legal Sites.csv` | 295 KB | Physical locations |
| `Local Analytical Mapping IDs.csv` | 7 KB | Cost allocation keys |
| `Local CoA Mapping IDs.csv` | - | Chart of Accounts mapping |
| `Systems.csv` | 1 KB | ERP systems list |
| `Business Hierarchy.csv` | - | Business hierarchy |
| `Managerial Hierarchy.csv` | - | Managerial hierarchy |
| `ActivitiesFunctions View.csv` | - | Activities/Functions |
| `Local ActivitiesFunctions View.csv` | - | Local activities |
| `MAB Products Hierarchy.csv` | - | Products hierarchy |
| `Local Products Hierarchy.csv` | - | Local products |
| `Local Legal Entities.csv` | - | Local legal entities |
| `Reporting Units View.csv` | - | Reporting units |

### MDM HR Files (02 - MDM HR) - 14 files

| Source | Records | Key Content |
|--------|---------|-------------|
| `KeyPropertiesNewIE.csv` | 79,801 | Org units, grades |
| `JobRepositoryNewIE.csv` | 7,865 | Job catalog |
| `Organisations.csv` | 395,174 | Manager relationships |
| `GenericLibrary.csv` | 18,606 | Compensation elements |
| `ValuesListLibrary.csv` | - | Value lists |
| `HubLibraries*.csv` | - | Hub libraries |
| `HubLibraries_*.json` | - | JSON structures |
| `Competencies Dictionnary.xlsx` | - | Competencies |
| `Collective_Agreements_Template.csv` | - | Collective agreements |
| `typeOfDocuments_referential.json` | - | Document types |

### MDM SITES Files (03 - MDM SITES) - 11 files

| Source | Key Content |
|--------|-------------|
| `Site View.csv` | Sites master data |
| `Address View.csv` | Site addresses |
| `Building View.csv` | Buildings |
| `Campus View.csv` | Campuses |
| `Cell View.csv` | Cells |
| `Contract View.csv` | Site contracts |
| `Nearest Generic City View.csv` | Cities |
| `Site To Certification.csv` | Certifications |
| `Certification Life Cycle.csv` | Certification lifecycle |
| `Supplier for Certification.csv` | Cert suppliers |
| `MDM_SITES_DataModel.md` | Data model doc |

---

## Scripts

| Script | Location | Purpose |
|--------|----------|---------|
| `hcm_consistency_check.py` | `scripts/` | Data consistency validation |
| `analyze_mdm_hr.py` | `02 - MDM HR/` | MDM HR analysis |
| `populate_sheets.py` | Root | Populate Excel sheets |
| `analyze_template_tabs.py` | Root | Template analysis |
| `cross_check_analysis.py` | Root | Cross-check redundancies |
| `remove_redundancies.py` | Root | Remove redundant records |
| `analyze_security_matrix.py` | `04 - SHEETS/Process and Security/` | Security matrix analysis |
| `update_security_matrix_geodis.py` | `04 - SHEETS/Process and Security/` | Apply GEODIS roles |
| `update_security_matrix_replace.py` | `04 - SHEETS/Process and Security/` | Replace standard roles |
| `apply_preboarding_access.py` | `04 - SHEETS/Process and Security/` | Pending/CWK access rules |
| `check_matrix_columns.py` | `04 - SHEETS/Process and Security/` | Verify matrix columns |

---

## Folder Structure

```
02 - Define/01 - Repositories/
│
├── 00 - Documentation/           <-- 27 files (25 numbered + 2 supporting)
│   ├── 00_DOCUMENTATION_INDEX.md  <-- START HERE
│   ├── 01-24_*.md                 <-- Numbered docs
│   ├── flowchart.md               <-- Supporting
│   └── Oracle_HCM_Structure_Diagram.md
│
├── 00 - POSITION PAPER/          <-- Reference PDFs
│   ├── MDM MAB.pdf
│   └── Module 2.1_MAB Fundamentals_Participants.pdf
│
├── 01 - MDM MAB/                 <-- 15 CSV files + data model
├── 02 - MDM HR/                  <-- 14 files + scripts
├── 03 - MDM SITES/               <-- 11 CSV files + data model
│
├── 04 - SHEETS/                  <-- 69 Excel config sheets
│   ├── Organization Structure/   <-- 16 files
│   ├── Personal Details/         <-- 22 files
│   ├── Employment Details/       <-- 12 files
│   ├── Workforce Structure/      <-- 9 files
│   ├── Compensation Details/     <-- 6 files
│   └── Process and Security/     <-- 5 files + scripts
│
├── 99 - DRAFTS/                  <-- Archived drafts
├── scripts/                      <-- Utility scripts
│
├── GEODIS_Repositories_CORE HR_FILLED_v2.xlsx  <-- MASTER OUTPUT
└── Reporting_Establishments_from_RU.xlsx
```

---

## Output Files

| File | Status | Content |
|------|--------|---------|
| `GEODIS_Repositories_CORE HR_FILLED_v2.xlsx` | FINAL | ~27,000 records across 69 sheets |
| `04 - SHEETS/` | FINAL | Individual Excel files by category |

---

## Resume Prompt

```
Continue the GEODIS HCM implementation work.

Start with documentation index:
00 - Documentation/00_DOCUMENTATION_INDEX.md

Read session tracker for context:
00 - Documentation/01_Agent_Session_Tracker.md

Current status:
- 69 sheets populated (~27,000 records)
- Security Matrix: 9 GEODIS roles, 308 objects
- Actions: 41 GEODIS-specific codes
- Workflows: 31 approval workflows
- Gaps: 50 identified (see doc 23)

Key documents for workflows:
- 20_GEODIS_HR_Workflows_Catalog.md (v1.0)
- 21_GTalent_to_Oracle_HCM_Mapping.md
- 22_Oracle_HCM_Approval_Workflows.md
- 23_GEODIS_HCM_Gap_Register.md
- 24_Oracle_HCM_Configuration_Specifications.md
```

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-11-30 | Initial index creation |
| 1.1 | 2025-11-30 | Moved to dedicated folder with numbered files |
| 1.2 | 2025-11-30 | Added docs 12-13: Analytical Allocation Model & MAB Analysis |
| 1.3 | 2025-11-30 | Added doc 14: MASTER Multialocation MAB |
| 1.4 | 2025-11-30 | Added doc 15: Documentation Architecture |
| 1.5 | 2025-12-06 | Added docs 16-20, fixed numbering |
| 1.6 | 2025-12-06 | **Full scan update**: Added docs 21-24, Process & Security sheets inventory, scripts catalog, MDM SITES folder, updated folder structure. Total: 27 docs, 69 sheets, 11 scripts |
| 1.7 | 2025-12-07 | **Consistency audit**: Added doc 26 (Consistency Audit), updated all record counts to verified actuals (58,460 total records across 70 files) |

---

*Start here for all GEODIS HCM implementation documentation.*
