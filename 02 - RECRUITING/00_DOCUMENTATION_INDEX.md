# GEODIS HCM - Recruiting Module Documentation Index

**Project:** GEODIS New HCM - AMARIS
**Module:** Talent Acquisition / Recruiting
**Phase:** 02 - Define
**Last Updated:** 2025-12-08
**Status:** In Progress - 14 Repository Sheets | 191 Records | 2 ATS Analyzed | 6 Interactive Decision Flowcharts | Immigration Compliance Guide | Business Requirements Complete | **Workshop 1 Analysis Complete**

---

## Design Philosophy: Fit-to-Standard (2025-12-08)

All Oracle IRC configuration follows these principles:

1. **Use Oracle standard fields** before creating DFFs
2. **Use seeded lookups** (RECRUITING_TYPE, MANAGER_LEVEL) before custom value sets
3. **Use organization hierarchy** (Department -> Division) for Line of Business
4. **Only create DFFs** for fields with NO Oracle equivalent

### Requisition DFF Summary (7 segments)

| # | Field | Justification |
|---|-------|---------------|
| 1 | FTE % | Oracle tracks headcount only |
| 2 | Budgeted? | No standard budget flag |
| 3 | Budget Justification | No standard field |
| 4 | Incumbent Name | No standard incumbent tracking |
| 5 | Incumbent Last Day | No standard field |
| 6 | Hiring Priority | HOT_JOB_FLAG is different |
| 7 | Impact to Staffing | Workforce planning custom |

### Removed from DFF (Use Oracle Standard)

- **TOPEX** -> `RECRUITING_TYPE_CODE = 'Executive'`
- **Line of Business** -> `DEPARTMENT_ID` -> Division hierarchy
- **Salary Min/Max/Currency** -> Standard `MIN_SALARY`, `MAX_SALARY`, `SALARY_CURRENCY_CODE`

---

## Quick Navigation

### Module Documentation (00 - DOCUMENTATION)

| # | Document | Purpose | Status |
|---|----------|---------|--------|
| 00 | [DOCUMENTATION_INDEX](#00-documentation-index) | This file - start here | Current |
| 01 | [Agent_Session_Tracker](#01-agent-session-tracker) | **Agent context & resume prompt** | Active |
| 02 | [Module_Progress_Log](#02-module-progress-log) | Session history & detailed progress | Active |
| 03 | [Oracle_Recruiting_Reference](#03-oracle-recruiting-reference) | Oracle Recruiting objects | Planned |
| 04 | [GEODIS_Recruiting_Configuration](#04-geodis-recruiting-configuration) | GEODIS-specific setup | Planned |
| 05 | [Source_System_Mapping](#05-source-system-mapping) | G-Talent+ to Oracle mapping | Planned |
| 06 | [Integration_Specifications](#06-integration-specifications) | Broadbean, LinkedIn, etc. | Planned |
| **11** | [**Oracle_Recruiting_Business_Requirements**](#11-business-requirements) | **Business requirements synthesis** | **Complete** |
| 12 | [GEODIS_Recruitment_Process_Workflows](#12-workflows) | End-to-end process workflows | Complete |
| 13 | [GEODIS_Recruitment_Mermaid_Diagrams](#13-diagrams) | Visual flowcharts (Mermaid) | Complete |
| 14 | [IRC_Configuration_Tables_Analysis](#14-tables-analysis) | IRC tables gap analysis | Complete |
| 15 | [Oracle_IRC_Field_Mapping_Flexfields](#15-field-mapping-v1) | Field mapping v1.0 (50 DFFs) | Superseded |
| **16** | [**Oracle_IRC_REVISED_Field_Mapping_FitToStandard**](#16-field-mapping-v2) | **Field mapping v2.0 (18 DFFs) - FIT TO STANDARD** | **Current** |
| **17** | [**Oracle_Recruiting_Workflow_Configuration_Guide**](#17-workflow-config) | **Workflows, stages, actors, campaigns** | **Complete** |
| **18** | [**IRC_Configuration_Tables_Oracle_EDM_Mapping**](#18-edm-mapping) | **Corrected Oracle EDM table mapping (63 items)** | **Complete** |
| **19** | [**GEODIS_Recruitment_Swimlane_Diagrams**](#19-swimlane-diagrams) | **End-to-end swimlane diagrams by role (9 diagrams)** | **Complete** |
| **20** | [**GEODIS_Recruitment_End_to_End_Sequence_Diagram**](#20-sequence-diagrams) | **Complete sequence diagrams - all actors & systems (10 diagrams)** | **Complete** |
| **21** | [**Decision_Flowcharts**](#21-decision-flowcharts) | **Interactive swimlane flowcharts with modal details (6 phases)** | **Complete** |
| **22** | [**Dynamic_Connector_Methodology**](#22-methodology) | **Technical documentation (integrated below)** | **Complete** |
| **23** | [**Immigration_Compliance_Checklist**](#23-immigration-compliance) | **PERM & visa compliance for foreign national hiring** | **Complete** |
| **24** | [**Paradox_Availability_Decision_Tree**](#24-paradox-availability) | **Country-based Paradox (Olivia) availability decision flow** | **Complete** |
| **25** | [**End_to_End_Overview**](#25-end-to-end-overview) | **Simplified E2E process with all phases and rules (no modals)** | **Complete** |
| **26** | [**Workshop1_Job_Requisitions_Holistic_Analysis**](#26-workshop1-analysis) | **Ultra-holistic analysis: HR Path workshop + Requirement File + GEODIS config** | **Complete** |

### HR Path Workshop Documentation (01 - HR PATH)

| # | Document | Purpose | Status |
|---|----------|---------|--------|
| W1 | GEODIS_WORKSHOP_1_JOB_REQUISITIONS.pdf | HR Path Workshop 1 presentation (36 slides) | Reference |
| RF1 | GEODIS_JOB_REQUISITIONS_REQUIREMENT_FILE_2025_V0.xlsx | Requirement file (13 tabs, 11 deliverables) | Awaiting Workshop |

### Source System Analysis (UKG + Talentsoft)

| # | Document | Purpose | Status |
|---|----------|---------|--------|
| 02 | [02_UKG_Talentsoft_Field_Definitions.md](#02-field-definitions) | Field definitions & WordPlus tags | Complete |
| 03 | [03_UKG_Talentsoft_Gap_Analysis.md](#03-gap-analysis) | Master gap analysis (v2.2, 594 fields) | Complete |
| 04 | [04_UKG_Talentsoft_SDD_Analysis.md](#04-sdd-analysis) | Detailed SDD coverage analysis | Complete |
| 05 | [05_UKG_vs_Talentsoft_DataModel.md](#05-data-model) | Architecture comparison | Complete |
| 06 | [06_UKG_Fields_Missing_in_Talentsoft.md](#06-missing-fields) | Data loss checklist (26 fields) | Complete |

### Data Conversion Tools

| # | Document | Purpose | Status |
|---|----------|---------|--------|
| 07 | [07_UKG_to_Talentsoft_Converter.md](#07-converter) | Converter documentation | Complete |
| 08 | [08_UKG_Converter_Updates.md](#08-converter-updates) | Update notes | Complete |
| 09 | [09_UKG_Converter_Production_Guide.md](#09-production-guide) | Production usage guide | Complete |

---

## Document Details

### 00 DOCUMENTATION INDEX
**File:** `00_DOCUMENTATION_INDEX.md`
**Purpose:** Master navigation and table of contents for Recruiting module
**Use when:** Starting any session, finding documentation

---

### 01 Agent Session Tracker
**File:** `01_Agent_Session_Tracker.md`
**Purpose:** Agent context, expertise, and session continuity
**Content:**
- Domain knowledge & source systems expertise
- Oracle Recruiting architecture (IRC module)
- UKG to Talentsoft migration analysis (97.8% coverage)
- Repository population summary (14 sheets, 191 records)
- GEODIS-specific configuration (templates, workflows)
- Resume prompt for continuity

**Use when:** Starting a new agent session, understanding module context

---

### 02 Module Progress Log
**File:** `02_Module_Progress_Log.md`
**Purpose:** Detailed session history and progress tracking
**Content:**
- Chronological session history
- Detailed actions completed per session
- File changes and migrations
- Technical implementation notes

**Use when:** Reviewing past work, understanding change history

---

### 03 Oracle Recruiting Reference (Planned)
**File:** `03_Oracle_Recruiting_Reference.md`
**Purpose:** Oracle HCM Cloud Recruiting objects and configuration
**Content:**
- Core Recruiting tables (IRC_*)
- Business objects for HDL
- Delivered workflows and notifications
- Career site configuration

**Use when:** Understanding Oracle Recruiting capabilities

---

### 04 GEODIS Recruiting Configuration (Planned)
**File:** `04_GEODIS_Recruiting_Configuration.md`
**Purpose:** GEODIS-specific recruiting configuration decisions
**Content:**
- Requisition template design
- Candidate phase workflow
- Approval workflow rules
- Country-specific offer letters

**Use when:** Configuring GEODIS-specific recruiting setup

---

### 05 Source System Mapping (Planned)
**File:** `05_Source_System_Mapping.md`
**Purpose:** G-Talent+ to Oracle Recruiting field mapping
**Content:**
- Vacancy to Requisition mapping
- Candidate data mapping
- Application history migration
- Source tracking conversion

**Use when:** Planning data migration from G-Talent+

---

### 06 Integration Specifications (Planned)
**File:** `06_Integration_Specifications.md`
**Purpose:** External integration requirements
**Content:**
- Broadbean job posting integration
- LinkedIn Recruiter integration
- Background check integration
- E-signature (DocuSign) integration

**Use when:** Planning recruiting integrations

---

### 21 Decision Flowcharts (Interactive HTML)
**Files:** `Decision_Flowchart_01_Requisition.html` through `Decision_Flowchart_06_Hire.html`
**Purpose:** Interactive swimlane flowcharts with click-to-display process details
**Content:**
- **Phase 1 - Requisition**: Position creation, approval workflow, budget validation
- **Phase 2 - Posting**: Internal posting (7-day rule), external publishing, Broadbean integration
- **Phase 3 - Screening**: Auto-screening KO criteria, qualification assessment, shortlisting
- **Phase 4 - Interview**: Panel interviews, feedback loops (48h SLA), assessment
- **Phase 5 - Offer**: Salary thresholds (<125K/125-155K/>155K), DocuSign, negotiation
- **Phase 6 - Hire**: Parallel preboarding (BGC via Sterling, Equipment via Coupa, IT provisioning)

**Features:**
- Dynamic JavaScript-based SVG connectors (Bezier curves for cross-lane)
- Click any step to view modal with: Description, Owner, Duration, Systems, Key Rules, GEODIS Good Practice
- GEODIS branding (Blue #3200eb, Orange #eb692b)
- Decision diamonds with Yes/No branches
- Animated return loops for iterative processes

**Use when:** Training users, process documentation, stakeholder presentations

---

### 22 Dynamic Connector Methodology
**Location:** Integrated into this index file (see "Dynamic Connector Methodology - Technical Reference" section below)
**Purpose:** Technical documentation for creating and maintaining flowchart diagrams
**Content:**
- Data structure specification (steps array, connections array, lanes array)
- Layout constants and dynamic width calculation
- Connector drawing algorithm (same-lane, cross-lane, return paths)
- CSS styling for connectors, decision diamonds, step blocks, animations
- Modal implementation guide with complete showStepModal() function
- Step-by-step implementation instructions with HTML boilerplate
- GEODIS brand colors reference and lane color mapping
- **Prerequisites and external dependencies (CDN)**
- **Build process (5 phases)**
- **Expected outcomes and business value**
- **File size reference**
- **Maintenance guide (add/modify steps, lanes, create new flowcharts)**

**Use when:** Maintaining existing flowcharts, creating new diagrams, understanding technical implementation

---

### 23 Immigration Compliance Checklist
**File:** `Immigration_Compliance_Checklist.md`
**Purpose:** Comprehensive guide for foreign national hiring and PERM labor certification compliance
**Content:**
- Pre-recruitment position eligibility assessment
- PERM pre-planning requirements (Prevailing Wage Determination)
- DOL-compliant advertising requirements (mandatory and professional position options)
- Recruitment documentation and retention requirements (5-year retention)
- Candidate evaluation compliance (U.S. worker testing, prohibited practices)
- Offer phase immigration considerations (prevailing wage compliance)
- Post-hire compliance (Public Access File, LCA posting)
- PERM process timeline visualization
- Visa category quick reference (H-1B, L-1, TN, OPT, Green Card)
- Complete compliance checklist summary

**Use when:** Hiring foreign national candidates, PERM cases, visa sponsorship questions, DOL audit preparation

---

### 24 Paradox Availability Decision Tree
**File:** `Decision_Flowchart_Paradox_Availability.html`
**Purpose:** Country-based decision tree for Paradox (Olivia) AI availability and alternate manual processes
**Content:**
- Visual decision flow for determining Paradox availability
- Side-by-side process comparison (Automated vs Manual)
- Affected recruitment phases (Posting, Screening, Interview)
- Configuration notes for Oracle Recruiting Cloud

**Use when:** Determining whether to use Paradox (Olivia) for a requisition, understanding manual fallback processes, training recruiters on country-specific workflows

---

### 25 End-to-End Overview
**File:** `GEODIS_Recruitment_End_to_End_Overview.html`
**Purpose:** Simplified single-page view of the complete recruitment process with all 6 phases and key rules
**Content:**
- All 6 recruitment phases displayed vertically
- Step flow visualization for each phase (5-6 steps per phase)
- Key rules and policies displayed inline (no modals)
- Links to detailed Decision Flowcharts for each phase
- Process statistics (6 phases, 21 steps, 10-12 weeks avg, 7 actors)
- Print-friendly layout

**Use when:** Quick process overview, stakeholder presentations, training materials, process audits, printing full process summary

---

### 11 Oracle Recruiting Business Requirements
**File:** `11_Oracle_Recruiting_Business_Requirements.md`
**Purpose:** Comprehensive business requirements synthesis for Oracle Recruiting
**Content:**
- Requirements from 4 source documents (HR Blueprint, Talentsoft, UKG TCE, Workshop RFP)
- Recruiting volume and scale analysis (250K+ applications/year)
- Requisition management requirements and approval workflows
- Job posting and sourcing requirements (7-day internal rule)
- Candidate management and pipeline configuration
- Interview and offer management requirements
- Background checks and compliance (PERM, I-9, visa tracking)
- Integration requirements (Indeed, LinkedIn, Sterling, DocuSign)
- GEODIS-specific business rules
- Gap analysis and recommendations

**Use when:** Configuring Oracle Recruiting, validating requirements, planning integrations

---

## Repository Sheets (03 - ORACLE)

### Overview (Created 2025-12-07)

| Category | Files | Records | Status |
|----------|------:|--------:|--------|
| Configuration | 14 | 191 | Complete |

### Repository Files

| # | File | Records | Description |
|---|------|--------:|-------------|
| 1 | Requisition Template.xlsx | 5 | Requisition form templates |
| 2 | Requisition Phase.xlsx | 8 | Requisition lifecycle phases |
| 3 | Candidate Phase.xlsx | 12 | Candidate pipeline phases |
| 4 | Candidate State.xlsx | 43 | Detailed candidate states |
| 5 | Candidate Source.xlsx | 17 | Application source tracking |
| 6 | Candidate Pool Type.xlsx | 7 | Talent pool categories |
| 7 | Offer Letter Template.xlsx | 18 | Country/job family templates |
| 8 | Interview Guide.xlsx | 10 | Interview question templates |
| 9 | Interview Type.xlsx | 9 | Interview format types |
| 10 | Posting Channel.xlsx | 8 | Job board channels |
| 11 | Rejection Reason.xlsx | 15 | Candidate rejection codes |
| 12 | Withdrawal Reason.xlsx | 8 | Candidate withdrawal codes |
| 13 | Recruiting Action.xlsx | 25 | Recruiting action codes |
| 14 | Recruiting Approval Workflow.xlsx | 6 | Approval workflow rules |

---

## Source Systems Analysis Summary

### Two ATS Systems Under Analysis

| System | Region | Status | Key Metrics |
|--------|--------|--------|-------------|
| **UKG (UltiPro)** | US | Analyzed | 594 fields, star schema, pre-calculated metrics |
| **Talentsoft (G-Talent+)** | Global | Analyzed | 234 API schemas, normalized model, SDD reports |

### UKG to Talentsoft Migration Status

| Metric | Value | Notes |
|--------|-------|-------|
| **Total UKG Fields** | 594 | From Talent Acquisition reporting layer |
| **Mapped Fields** | 454 (76.4%) | Direct field mapping |
| **Reference Fields** | 84 (14.1%) | Lookup/referential mapping |
| **System Fields** | 22 (3.7%) | Internal system fields |
| **Must Calculate** | 13 (2.2%) | Days-to-hire metrics |
| **Not Available** | 13 (2.2%) | Data loss (Title/Suffix, Incumbent) |
| **Custom Fields** | 8 (1.3%) | Requires custom configuration |
| **Coverage Rate** | **97.8%** | Only 13 fields with no equivalent |

### Key Gaps Identified

| Gap Category | Fields | Risk | Workaround |
|--------------|--------|------|------------|
| Incumbent Tracking | 3 | HIGH | Custom field in Vacancy Request |
| Manager Title/Suffix | 12 | LOW | Accept loss or concatenate |
| FTE Granularity | 4 | HIGH | Calculate from applications |
| Days-to-Hire Metrics | 5 | HIGH | Build BI calculations |
| Licenses/Certifications | 3 | MEDIUM | Custom fields configured |

### GEODIS Talentsoft Custom Fields (Already Addressed)

| UKG Gap | GEODIS Talentsoft Field | Status |
|---------|------------------------|--------|
| Incumbent Name | `Name of person being replaced` [P-RequestMotive_ShortText1] | ADDRESSED |
| Is Budgeted | `Budgeted vacancy request` [P-Planned] | ADDRESSED |
| FTE % | `FTE %` [P-PreliminaryJobDescription_ShortText1] | ADDRESSED |
| Licenses | `Certifications` [A-Diploma_LongText2] | ADDRESSED |
| Middle Name | `Middle name` [A-MiddleName] | AVAILABLE |

### Source System Files

| Source | Location | Content |
|--------|----------|---------|
| `01 - TS/` | Talentsoft exports | Vacancy, candidate data, conversion outputs |
| `02 - UKG/` | UKG exports | US recruiting data (Opportunity Detail.csv) |
| `UKG GAP ANALYSIS/` | Analysis folder | Gap analysis, data model comparison |
| `UKG_to_Talentsoft_Converter/` | Converter scripts | Python converter (33,952 offers processed) |
| `TS_Import_Output/` | Import files | Generated Talentsoft import CSVs |

### Mapping Files

| File | Purpose | Records |
|------|---------|---------|
| `UKG_Talentsoft_Holistic_Mapping_CORRECTED.xlsx` | Master field mapping | 594 fields |
| `UKG_Talentsoft_Mapping_CORRECTIONS.xlsx` | Tag corrections | 34 corrections |
| `UKG_Talentsoft_Field_Definitions.md` | Field definitions | Complete |
| `UKG_Talentsoft_Gap_Analysis_UPDATED.md` | Gap analysis v2.2 | Complete |
| `US Talent Acquisition Package mapped v3.xlsx` | UKG source analysis | 594 fields |

---

## Folder Structure (Reorganized 2025-12-07)

```
02 - Recruiting/
│
├── 00 - DOCUMENTATION/               <-- Documentation (20+ files)
│   ├── 00_DOCUMENTATION_INDEX.md       <-- START HERE
│   ├── 01_Agent_Session_Tracker.md     <-- Agent context & resume prompt
│   ├── 02_Module_Progress_Log.md       <-- Session history & progress
│   ├── 02_UKG_Talentsoft_Field_Definitions.md    <-- Field definitions
│   ├── 03_UKG_Talentsoft_Gap_Analysis.md         <-- Gap analysis v2.2
│   ├── 04_UKG_Talentsoft_SDD_Analysis.md         <-- SDD coverage analysis
│   ├── 05_UKG_vs_Talentsoft_DataModel.md         <-- Architecture comparison
│   ├── 06_UKG_Fields_Missing_in_Talentsoft.md    <-- Data loss checklist
│   ├── 07_UKG_to_Talentsoft_Converter.md         <-- Converter documentation
│   ├── 08_UKG_Converter_Updates.md               <-- Converter updates
│   ├── 09_UKG_Converter_Production_Guide.md      <-- Production guide
│   ├── 10_Folder_Reorganization_Plan.md          <-- Cleanup plan
│   │
│   ├── Decision_Flowchart_01_Requisition.html    <-- Phase 1 interactive flowchart
│   ├── Decision_Flowchart_02_Posting.html        <-- Phase 2 interactive flowchart
│   ├── Decision_Flowchart_03_Screening.html      <-- Phase 3 interactive flowchart
│   ├── Decision_Flowchart_04_Interview.html      <-- Phase 4 interactive flowchart
│   ├── Decision_Flowchart_05_Offer.html          <-- Phase 5 interactive flowchart
│   ├── Decision_Flowchart_06_Hire.html           <-- Phase 6 interactive flowchart
│   └── GEODIS_Recruitment_Swimlane_Connected.html  <-- Master reference diagram
│   (Dynamic Connector Methodology integrated into this index file)
│
├── 01 - SOURCE DATA/                 <-- Source system data
│   ├── TALENTSOFT/                     <-- Talentsoft exports
│   │   ├── Data Model/                   <-- 167 referential CSV files
│   │   ├── Field Documentation/          <-- PDFs + Excel specs
│   │   └── SDD Reports/                  <-- 6 SDD export files
│   │
│   └── UKG/                            <-- UKG exports (US)
│       └── Talent Acquisition Package.xls
│
├── 02 - MAPPING/                     <-- Mapping files (consolidated)
│   ├── UKG_Talentsoft_Holistic_Mapping.xlsx      <-- Master (corrected)
│   ├── UKG_Talentsoft_Mapping_CORRECTIONS.xlsx   <-- 34 corrections log
│   └── US Talent Acquisition Package mapped v3.xlsx  <-- UKG analysis
│
├── 03 - ORACLE/                      <-- Target Oracle configuration
│   ├── 00 - STANDARD TABLES/           <-- Oracle standard table documentation
│   │   ├── 00_INDEX.md                   <-- Standard tables index
│   │   ├── 01_IRC_REQUISITIONS_B_Standard.md
│   │   ├── 02_IRC_CANDIDATES_Standard.md
│   │   ├── 03_IRC_SUBMISSIONS_Standard.md
│   │   ├── 04_IRC_OFFERS_Standard.md
│   │   └── 05_Job_Offer_Sections_Standard.md
│   ├── Requisition Template.xlsx
│   ├── Candidate Phase.xlsx
│   ├── Candidate State.xlsx
│   ├── ... (14+ config files, 191+ records)
│   └── create_recruiting_sheets.py
│
├── 04 - CONVERSION/                  <-- UKG to Talentsoft converter
│   ├── Scripts/                        <-- Python converters
│   │   ├── opportunity_converter.py
│   │   ├── ukg_to_talentsoft_converter.py
│   │   ├── run_production.py
│   │   └── run_and_copy_to_uat.py
│   ├── Batch Files/                    <-- Windows batch scripts
│   ├── Output/                         <-- Latest converted files
│   │   ├── PRODUCTION/                   <-- Production output
│   │   └── UAT/                          <-- UAT output
│   └── QUICK_START.txt
│
└── 99 - ARCHIVE/                     <-- Old versions and backups
    └── Mapping_Versions/               <-- Superseded mapping files
        ├── UKG_Talentsoft_Holistic_Mapping_BACKUP.xlsx
        ├── UKG_Talentsoft_Holistic_Mapping_ORIGINAL.xlsx
        └── US Talent Acquisition Package mapped v2.xlsx
```

---

## Integration with Core HR

The Recruiting module integrates with Core HR repositories:

| Core HR Repository | Recruiting Usage |
|-------------------|------------------|
| Job.xlsx (688) | Requisition job code |
| Job Family.xlsx (27) | Offer letter template selection |
| Grade.xlsx (20) | Salary range validation |
| Location.xlsx (919) | Requisition work location |
| Department.xlsx (10,803) | Hiring department |
| Business Unit.xlsx (2,175) | Requisition organization |
| Legal Entity.xlsx (364) | Offer legal employer |

---

## Key Decisions & Gaps

### Decisions Required

| # | Decision | Options | Status |
|---|----------|---------|--------|
| 1 | Job Board Integration | Broadbean vs Oracle native | Pending |
| 2 | Internal Posting Rule | 7 days mandatory | Confirmed |
| 3 | Offer Approval Threshold | EUR 125K base / 155K total | Confirmed |
| 4 | Speculative Applications | Talent Community pool | Configured |

### Identified Gaps

| Gap ID | Description | Priority | Mitigation |
|--------|-------------|----------|------------|
| REC-001 | Broadbean integration | P2 | Evaluate Oracle native |
| REC-002 | Offer letter templates per country | P1 | 18 templates created |
| REC-003 | Candidate source tracking | P3 | 17 sources configured |
| REC-004 | OTBI recruiting dashboards | P2 | To be designed |

---

## Resume Prompt

```
Continue the GEODIS HCM Recruiting module implementation.

Start with documentation index:
02 - Define/02 - Core Model/02 - Recruiting/00 - DOCUMENTATION/00_DOCUMENTATION_INDEX.md

Read agent tracker for context:
02 - Define/02 - Core Model/02 - Recruiting/00 - DOCUMENTATION/01_Agent_Session_Tracker.md

Current status:
- 14 repository sheets created (191 records)
- 2 ATS analyzed (UKG + Talentsoft, 97.8% coverage)
- Folder reorganized (6 clean folders)
- Located in: 03 - ORACLE/ folder

Focus areas:
- Requisition template validation
- Approval workflow configuration
- Job board integration decision
- Data migration planning

Core HR reference:
02 - Define/01 - Repositories/00 - Documentation/00_DOCUMENTATION_INDEX.md
```

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-07 | Initial index creation with 14 repository sheets |
| 1.1 | 2025-12-07 | Added Source System Analysis (UKG + Talentsoft), updated folder structure |
| 1.2 | 2025-12-07 | Consolidated all markdown docs into 00 - DOCUMENTATION (10 files) |
| 1.3 | 2025-12-07 | Full folder reorganization: 318→209 files, removed duplicates, archived old versions |
| 1.4 | 2025-12-07 | Added dedicated Agent Session Tracker, renamed Module_Session_Tracker → Module_Progress_Log |
| 1.5 | 2025-12-07 | Added workflow docs (12, 13), IRC tables analysis (14), field mapping v1 (15) |
| **1.6** | **2025-12-07** | **Added Oracle standard tables folder (00 - STANDARD TABLES), REVISED field mapping v2.0 (16) - FIT TO STANDARD** |
| **1.7** | **2025-12-07** | **Added swimlane diagrams (19) - 9 role-based process diagrams** |
| 1.8 | 2025-12-08 | Added sequence diagrams (20) - 10 end-to-end sequence diagrams with all actors & integrations |
| 1.9 | 2025-12-08 | Added Decision Flowcharts (21) - 6 interactive HTML flowcharts with modal details; Dynamic Connector Methodology (22) |
| **2.0** | **2025-12-08** | **Integrated full Dynamic Connector Methodology into index: architecture, algorithms, CSS, modal implementation, build process, prerequisites, expected outcomes, maintenance guide** |

---

## Oracle Standard Tables Reference (NEW)

Located in: `03 - ORACLE/00 - STANDARD TABLES/`

| Table | Document | Key Standard Fields |
|-------|----------|---------------------|
| IRC_REQUISITIONS_B | 01_IRC_REQUISITIONS_B_Standard.md | MIN_SALARY, MAX_SALARY, NUMBER_TO_HIRE, HOT_JOB_FLAG |
| IRC_CANDIDATES | 02_IRC_CANDIDATES_Standard.md | AVAILABILITY_DATE, CAND_PREF_LANGUAGE_CODE |
| IRC_SUBMISSIONS | 03_IRC_SUBMISSIONS_Standard.md | QSTNR_SCORE, CURRENT_PHASE_ID, CURRENT_STATE_ID |
| IRC_OFFERS | 04_IRC_OFFERS_Standard.md | EXPIRATION_DATE, ACCEPTED_DATE (90 DFF char columns) |
| Job Offer Sections | 05_Job_Offer_Sections_Standard.md | Salary Section, Other Compensation, Assignment Info |

### DFF Reduction Summary (v1.0 → v2.0)

| Object | v1.0 DFFs | v2.0 DFFs | Reduction |
|--------|-----------|-----------|-----------|
| Requisition | 12 | 4 | -67% |
| Candidate | 15 | 8 | -47% |
| Application | 8 | 3 | -63% |
| Offer | 10 | 2 | -80% |
| Interview | 5 | 1 | -80% |
| **TOTAL** | **50** | **18** | **-64%** |

---

## Dynamic Connector Methodology - Technical Reference

This section provides the complete technical methodology for creating and maintaining interactive swimlane flowcharts with dynamic JavaScript-based connectors, as implemented in the GEODIS HCM Recruitment Decision Flowcharts.

### Key Benefits

| Feature | Description |
|---------|-------------|
| **Dynamic connectors** | Connection paths calculated at runtime based on actual element positions |
| **Adaptive width** | Diagram width automatically adjusts to content |
| **Data-driven** | Steps and connections defined as JavaScript arrays for easy maintenance |
| **Interactive modals** | Click on any step to view detailed process information |
| **GEODIS branding** | Consistent use of brand colors (Blue #3200eb, Orange #eb692b) |

---

### Architecture Overview

#### 1. Steps Array Structure

Each step is defined as an object with the following properties:

```javascript
const steps = [
    {
        id: 'unique_id',           // Unique identifier for the step
        lane: 0,                   // Lane index (0-based, top to bottom)
        x: 200,                    // X position in pixels from left
        label: 'Step Name',        // Display label
        num: '1',                  // Step number (displayed in badge)
        icon: 'fa-icon-name',      // FontAwesome icon class
        type: 'decision',          // Optional: 'decision' for diamond shapes, 'start', 'end', 'reject'
        meta: 'Short info',        // Optional: displayed under label
        highlighted: true,         // Optional: adds pulse animation

        // Detailed info for modal (recommended)
        desc: 'Full description of the step...',
        owner: 'Role/Department',
        duration: 'SLA: 24h',
        systems: ['Oracle HCM', 'DocuSign'],
        rules: ['Rule 1', 'Rule 2'],
        goodPractice: 'Best practice guidance...'
    },
    // ... more steps
];
```

#### 2. Connections Array Structure

Connections define the flow between steps:

```javascript
const connections = [
    { from: 'step1_id', to: 'step2_id' },                              // Standard connection
    { from: 'decision_id', to: 'yes_step', type: 'yes', label: 'Yes' }, // Decision Yes branch
    { from: 'decision_id', to: 'no_step', type: 'no', label: 'No' },    // Decision No branch
    { from: 'parallel1', to: 'join', type: 'parallel' },               // Parallel animated line
    { from: 'loop_end', to: 'loop_start', type: 'return' },            // Return/loop connection
];
```

#### 3. Lanes Array Structure

```javascript
const lanes = [
    { id: 0, name: 'Recruiter', class: 'lane-recruiter' },
    { id: 1, name: 'Hiring Manager', class: 'lane-manager' },
    { id: 2, name: 'HR/HRBP', class: 'lane-hr' },
    { id: 3, name: 'Candidate', class: 'lane-candidate' },
    { id: 4, name: 'System', class: 'lane-system' },
    { id: 5, name: 'External', class: 'lane-external' },
];
```

#### 4. Layout Constants

```javascript
const LANE_HEIGHT = 100;     // Height of each swimlane in pixels
const STEP_WIDTH = 140;      // Width of step blocks
const STEP_HEIGHT = 60;      // Height of step blocks
const V_CENTER = 50;         // Vertical center offset within lane
```

#### 5. Dynamic Width Calculation

```javascript
const maxX = Math.max(...steps.map(s => s.x)) + STEP_WIDTH + 100;
document.getElementById('diagram').style.width = maxX + 'px';
svgConnectors.setAttribute('width', maxX);
```

---

### Flowchart File Structure

```
00 - DOCUMENTATION/
├── Decision_Flowchart_01_Requisition.html    <-- Phase 1: Position creation & approval
├── Decision_Flowchart_02_Posting.html        <-- Phase 2: Internal/external posting
├── Decision_Flowchart_03_Screening.html      <-- Phase 3: Application screening
├── Decision_Flowchart_04_Interview.html      <-- Phase 4: Interview & assessment
├── Decision_Flowchart_05_Offer.html          <-- Phase 5: Offer management
├── Decision_Flowchart_06_Hire.html           <-- Phase 6: Hire & preboarding
└── GEODIS_Recruitment_Swimlane_Connected.html  <-- Master reference diagram
```

---

### Connector Drawing Algorithm

#### Same-Lane Connections (Straight Lines)

```javascript
if (fromLane === toLane) {
    d = `M ${fromX} ${fromY} L ${toX} ${toY}`;
}
```

#### Cross-Lane Connections (Bezier Curves)

```javascript
if (fromLane !== toLane) {
    const midX = fromX + (toX - fromX) / 2;
    d = `M ${fromX} ${fromY} C ${midX} ${fromY}, ${midX} ${toY}, ${toX} ${toY}`;
}
```

#### Return/Loop Connections

```javascript
if (type === 'return') {
    const dropY = Math.max(fromY, toY) + 30;
    d = `M ${fromX} ${fromY} Q ${fromX+50} ${dropY}, ${toX} ${toY}`;
}
```

#### Arrow Heads (SVG Polygon)

```javascript
const arrowSize = 6;
const points = [
    [toX, toY],                              // Tip
    [toX - arrowSize*1.5, toY - arrowSize],  // Upper wing
    [toX - arrowSize*1.5, toY + arrowSize]   // Lower wing
].map(p => p.join(',')).join(' ');

arrow.setAttribute('points', points);
```

---

### CSS Styling Reference

#### Connector Paths

```css
.connector-path {
    fill: none;
    stroke: #94A3B8;
    stroke-width: 2;
    stroke-linecap: round;
}

.connector-path.animated {
    stroke-dasharray: 8 4;
    animation: flowAnimation 1s linear infinite;
}

@keyframes flowAnimation {
    from { stroke-dashoffset: 12; }
    to { stroke-dashoffset: 0; }
}
```

#### Decision Diamonds

```css
.decision-diamond {
    width: 50px;
    height: 50px;
    background: #fff;
    border: 2px solid #eb692b;
    transform: rotate(45deg);
}
```

#### Step Blocks

```css
.step-block {
    position: absolute;
    width: 140px;
    height: 60px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    cursor: pointer;
    transition: all 0.2s ease;
}

.step-block:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}
```

---

### Modal Implementation

#### HTML Structure

```html
<div class="modal-overlay" id="modal">
    <div class="modal">
        <div class="modal-header">
            <h3>
                <span class="modal-icon" id="modalIcon"></span>
                <span id="modalTitleText">Step Title</span>
            </h3>
            <button class="modal-close" onclick="closeModal()">
                <i class="fas fa-times"></i>
            </button>
        </div>
        <div class="modal-body" id="modalBody">
            <!-- Dynamic content -->
        </div>
    </div>
</div>
```

#### Modal Content Sections

| Section | Purpose | Required |
|---------|---------|----------|
| **Description** | Full explanation of the step | Yes |
| **Owner/Duration** | Quick reference info boxes | Yes |
| **Systems & Tools** | Tags showing involved systems | Yes |
| **Key Rules** | Bullet list of requirements | Yes |
| **Good Practice** | Highlighted best practice guidance | Optional |

#### Show Modal Function

```javascript
function showStepModal(step, laneClass) {
    const modal = document.getElementById('modal');
    const icon = document.getElementById('modalIcon');
    const title = document.getElementById('modalTitleText');
    const body = document.getElementById('modalBody');

    // Set icon background color based on lane/type
    const colorMap = {
        'lane-recruiter': 'var(--lane-recruiter)',
        'lane-manager': 'var(--lane-manager)',
        'lane-hr': 'var(--lane-hr)',
        'lane-candidate': 'var(--lane-candidate)',
        'lane-system': 'var(--lane-system)',
        'lane-external': 'var(--lane-external)'
    };

    let iconColor = colorMap[laneClass] || 'var(--geodis-blue)';
    if (step.type === 'start') iconColor = 'var(--geodis-green)';
    if (step.type === 'end') iconColor = 'var(--geodis-purple)';
    if (step.type === 'reject') iconColor = 'var(--geodis-red)';
    if (step.type === 'decision') iconColor = 'var(--geodis-orange)';

    icon.style.background = iconColor;
    icon.innerHTML = `<i class="fas ${step.icon || 'fa-question'}"></i>`;
    title.textContent = step.label;

    // Build content
    const systemsTags = (step.systems || ['Oracle Recruiting Cloud'])
        .map(s => `<span class="tag">${s}</span>`).join('');
    const rulesList = (step.rules || ['Follow GEODIS standard process'])
        .map(r => `<li><i class="fas fa-check-circle"></i> ${r}</li>`).join('');
    const goodPracticeHtml = step.goodPractice
        ? `<div class="modal-section good-practice">
             <h4><i class="fas fa-lightbulb"></i> GEODIS Good Practice</h4>
             <p>"${step.goodPractice}"</p>
           </div>`
        : '';

    body.innerHTML = `
        <div class="modal-section">
            <h4><i class="fas fa-info-circle"></i> Description</h4>
            <p>${step.desc || 'No description available.'}</p>
        </div>
        <div class="info-row">
            <div class="info-box"><label>Owner</label><span>${step.owner || 'TBD'}</span></div>
            <div class="info-box"><label>Duration</label><span>${step.duration || 'Variable'}</span></div>
        </div>
        <div class="modal-section">
            <h4><i class="fas fa-cog"></i> Systems & Tools</h4>
            <div class="tag-list">${systemsTags}</div>
        </div>
        <div class="modal-section">
            <h4><i class="fas fa-gavel"></i> Key Rules</h4>
            <ul class="rule-list">${rulesList}</ul>
        </div>
        ${goodPracticeHtml}
    `;

    modal.classList.add('active');
}

function closeModal() {
    document.getElementById('modal').classList.remove('active');
}
```

#### Event Listeners

```javascript
// Click step to open modal
stepElement.onclick = () => showStepModal(step, laneClass);

// Click overlay to close
document.getElementById('modal').addEventListener('click', (e) => {
    if (e.target.id === 'modal') closeModal();
});

// Escape key to close
document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') closeModal();
});
```

---

### GEODIS Brand Colors

#### CSS Variables

```css
:root {
    --geodis-blue: #3200eb;
    --geodis-blue-dark: #2800c0;
    --geodis-blue-light: #ebe6ff;
    --geodis-orange: #eb692b;
    --geodis-orange-light: #fff5f0;
    --geodis-green: #10B981;
    --geodis-purple: #8B5CF6;
    --geodis-red: #EF4444;
}
```

#### Lane Colors Reference

| Lane | CSS Variable | Hex Color | Use Case |
|------|--------------|-----------|----------|
| Recruiter | `--lane-recruiter` | #F59E0B (Amber) | Recruitment team actions |
| Hiring Manager | `--lane-manager` | #3B82F6 (Blue) | Manager decisions |
| HR/HRBP | `--lane-hr` | #EC4899 (Pink) | HR operations |
| Candidate | `--lane-candidate` | #10B981 (Green) | Applicant actions |
| System | `--lane-system` | #6B7280 (Gray) | Automated processes |
| External | `--lane-external` | #06B6D4 (Cyan) | Third parties (Sterling, DocuSign) |

---

### Step-by-Step Implementation Guide

#### Step 1: Create HTML Boilerplate

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>GEODIS - [Phase Name] Decision Flowchart</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>/* CSS here */</style>
</head>
<body>
    <div class="header"><!-- Header content --></div>
    <div class="diagram-wrapper">
        <div class="diagram-container" id="diagramContainer">
            <div class="swimlane-labels" id="laneLabels"></div>
            <div class="diagram" id="diagram">
                <svg class="connectors" id="svgConnectors"></svg>
            </div>
        </div>
    </div>
    <div class="modal-overlay" id="modal"><!-- Modal content --></div>
    <script>/* JavaScript here */</script>
</body>
</html>
```

#### Step 2: Define Lanes

```javascript
const lanes = [
    { id: 0, name: 'Recruiter', class: 'lane-recruiter' },
    { id: 1, name: 'Hiring Manager', class: 'lane-manager' },
    // Add lanes as needed
];
```

#### Step 3: Define Steps with Full Details

Include all properties for rich modal content:
- `id`: Unique identifier (e.g., 's1', 'decision1')
- `lane`: Lane index (0-based)
- `x`: Horizontal position in pixels (~170px spacing between steps)
- `label`: Display name
- `num`: Step number
- `icon`: FontAwesome icon (e.g., 'fa-file-alt')
- `desc`: Detailed description (2-4 sentences)
- `owner`: Role responsible
- `duration`: SLA or time estimate
- `systems`: Array of system/tool names
- `rules`: Array of key rules/requirements
- `goodPractice`: Optional GEODIS best practice text

#### Step 4: Define Connections

Map the flow between steps:
- Standard: `{ from: 'a', to: 'b' }`
- Decision Yes: `{ from: 'd', to: 'yes', type: 'yes', label: 'Yes' }`
- Decision No: `{ from: 'd', to: 'no', type: 'no', label: 'No' }`
- Parallel: `{ from: 'a', to: 'b', type: 'parallel' }`
- Return loop: `{ from: 'end', to: 'start', type: 'return', label: 'Retry' }`

#### Step 5: Implement init() Function

```javascript
function init() {
    const maxX = Math.max(...steps.map(s => s.x)) + STEP_WIDTH + 100;
    document.getElementById('diagram').style.width = maxX + 'px';
    document.getElementById('svgConnectors').setAttribute('width', maxX);

    // Create lane backgrounds
    createLanes();

    // Create step elements
    steps.forEach(step => createStepElement(step));

    // Draw connections
    drawConnections();
}
```

#### Step 6: Test and Validate

- Open in browser
- Click each step to verify modal content
- Check connector paths are correct
- Verify decision branches labeled correctly
- Test Escape key closes modal
- Test click-outside closes modal

---

### Best Practices

| # | Practice | Description |
|---|----------|-------------|
| 1 | **Consistent spacing** | Maintain ~170px between steps horizontally |
| 2 | **Lane assignment** | Keep related steps in same lane when possible |
| 3 | **Decision placement** | Position decisions centrally in flow |
| 4 | **Connection clarity** | Avoid crossing connectors when possible |
| 5 | **Modal content** | Always include desc, owner, systems, rules |
| 6 | **Good practices** | Add GEODIS policy references where applicable |
| 7 | **Step numbering** | Use sequential numbers for main flow, letters for branches |
| 8 | **Icon consistency** | Use same icons for similar step types across diagrams |

---

### Flowchart Files Reference

| File | Phase | Steps | Key Features |
|------|-------|-------|--------------|
| `Decision_Flowchart_01_Requisition.html` | 1 - Requisition | ~12 | Approval workflow, budget validation |
| `Decision_Flowchart_02_Posting.html` | 2 - Posting | ~12 | 7-day internal rule, Broadbean |
| `Decision_Flowchart_03_Screening.html` | 3 - Screening | 13 | Auto-screening KO, qualification |
| `Decision_Flowchart_04_Interview.html` | 4 - Interview | 13 | 48h SLA, panel interviews |
| `Decision_Flowchart_05_Offer.html` | 5 - Offer | 12 | Salary thresholds, DocuSign |
| `Decision_Flowchart_06_Hire.html` | 6 - Hire | 17 | Parallel preboarding tracks |
| `GEODIS_Recruitment_Swimlane_Connected.html` | Master | All | Complete reference diagram |

---

## How the HTML Flowcharts Were Built

### Prerequisites

#### Technical Requirements

| Requirement | Description | Source |
|-------------|-------------|--------|
| **Process Knowledge** | Complete understanding of GEODIS recruitment workflow | HR Blueprint, Workshop RFPs |
| **Step Details** | Description, owner, duration, systems, rules for each step | `GEODIS_Recruitment_Swimlane_Connected.html` |
| **GEODIS Branding** | Official brand colors and fonts | Corporate guidelines |
| **Web Technologies** | HTML5, CSS3, JavaScript (ES6+), SVG | Standard web stack |

#### External Dependencies (CDN)

| Library | Version | Purpose | CDN URL |
|---------|---------|---------|---------|
| **Poppins Font** | - | Primary font family | Google Fonts |
| **Inter Font** | - | Secondary font | Google Fonts |
| **FontAwesome** | 6.4.0 | Icons for steps and modals | cdnjs.cloudflare.com |

```html
<!-- Required CDN links -->
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
```

#### Source Data Requirements

| Data Source | Content | Used For |
|-------------|---------|----------|
| `GEODIS_Recruitment_Swimlane_Connected.html` | Master process diagram with all step details | Step definitions, descriptions, rules |
| `11_Oracle_Recruiting_Business_Requirements.md` | Business requirements synthesis | GEODIS-specific rules, SLAs |
| `17_Oracle_Recruiting_Workflow_Configuration_Guide.md` | Workflow stages and actors | Lane assignments, phase boundaries |
| HR Blueprint Documents | Process flows from discovery phase | Original process definitions |

---

### Build Process

#### Phase 1: Data Extraction

1. **Identify process phase** (Requisition, Posting, Screening, Interview, Offer, Hire)
2. **Extract steps from master diagram** (`GEODIS_Recruitment_Swimlane_Connected.html`)
3. **Document for each step:**
   - Step ID and number
   - Lane assignment (actor)
   - Step label and icon
   - Full description
   - Process owner
   - Duration/SLA
   - Systems involved
   - Key business rules
   - GEODIS good practices (where applicable)

#### Phase 2: Structure Definition

```javascript
// Example: Phase 3 - Screening steps structure
const steps = [
    {
        id: 's1',
        lane: 0,  // Recruiter
        x: 200,
        label: 'Review Applications',
        num: '1',
        icon: 'fa-folder-open',
        meta: 'Initial Review',
        desc: 'Recruiter reviews incoming applications against minimum qualifications...',
        owner: 'Recruiter',
        duration: '24-48 hours',
        systems: ['Oracle Recruiting Cloud', 'Resume Parser'],
        rules: [
            'Review within 48 hours of submission',
            'Check minimum qualifications first',
            'Document rejection reasons'
        ],
        goodPractice: 'Use auto-screening KO criteria to filter unqualified candidates automatically.'
    },
    // ... more steps
];
```

#### Phase 3: Connection Mapping

1. **Map sequential flow** between steps
2. **Identify decision points** (Yes/No branches)
3. **Mark parallel processes** (e.g., BGC + Equipment + IT in Hire phase)
4. **Define return loops** (e.g., More Interview Rounds)

```javascript
const connections = [
    { from: 's1', to: 's2' },
    { from: 's2', to: 'decision1' },
    { from: 'decision1', to: 's3', type: 'yes', label: 'Qualified' },
    { from: 'decision1', to: 'reject', type: 'no', label: 'Not Qualified' },
    // ...
];
```

#### Phase 4: HTML Assembly

1. **Create HTML boilerplate** with DOCTYPE, head, body
2. **Add CDN dependencies** (fonts, icons)
3. **Define CSS styles** (~400 lines):
   - Root variables (colors)
   - Header styling
   - Swimlane layout
   - Step blocks and decision diamonds
   - Connector paths
   - Modal overlay and content
   - Animations
4. **Add HTML structure**:
   - Header with title and legend
   - Diagram container with SVG layer
   - Modal overlay
5. **Add JavaScript** (~300 lines):
   - Data arrays (lanes, steps, connections)
   - Layout constants
   - init() function
   - createStepElement() function
   - drawConnections() function
   - showStepModal() function
   - Event listeners

#### Phase 5: Testing & Validation

| Test | Expected Result |
|------|-----------------|
| Open in browser | Diagram renders with all steps visible |
| Click any step | Modal opens with correct content |
| Click outside modal | Modal closes |
| Press Escape | Modal closes |
| Check all connectors | Lines connect correct steps |
| Check decision branches | Yes/No labels visible |
| Verify GEODIS colors | Blue header, orange accents |
| Test horizontal scroll | Diagram scrolls smoothly |

---

### Expected Outcomes

#### Per Flowchart File

| Outcome | Description |
|---------|-------------|
| **Self-contained HTML** | Single file, no external dependencies except CDN |
| **Interactive diagram** | Clickable steps with modal popups |
| **GEODIS branded** | Corporate colors, fonts, logo reference |
| **Process documentation** | Complete step details in modals |
| **Print-friendly** | Can be exported/printed for workshops |

#### Complete Set (6 Files)

| Outcome | Metric |
|---------|--------|
| **Total steps documented** | ~80 steps across 6 phases |
| **Actors covered** | Recruiter, Hiring Manager, HR/HRBP, Candidate, System, External |
| **Systems referenced** | Oracle Recruiting Cloud, DocuSign, Sterling, Coupa, Broadbean, AD/Exchange |
| **GEODIS rules captured** | 7-day internal posting, salary thresholds, 48h feedback SLA, etc. |

#### Business Value

| Value | Description |
|-------|-------------|
| **Training material** | New recruiters can learn process visually |
| **Process documentation** | Compliant with Oracle implementation methodology |
| **Stakeholder alignment** | Visual aid for workshops and sign-offs |
| **Gap identification** | Clear view of system touchpoints and handoffs |
| **Future maintenance** | Data-driven structure allows easy updates |

---

### File Size Reference

| File | Approx. Size | Lines of Code |
|------|--------------|---------------|
| Decision_Flowchart_01_Requisition.html | ~45 KB | ~900 |
| Decision_Flowchart_02_Posting.html | ~45 KB | ~900 |
| Decision_Flowchart_03_Screening.html | ~50 KB | ~1000 |
| Decision_Flowchart_04_Interview.html | ~50 KB | ~1000 |
| Decision_Flowchart_05_Offer.html | ~48 KB | ~950 |
| Decision_Flowchart_06_Hire.html | ~55 KB | ~1100 |

---

### Maintenance Guide

#### Adding a New Step

1. Add step object to `steps` array with all properties
2. Add connection(s) to `connections` array
3. Adjust `x` positions of subsequent steps if needed
4. Test modal content displays correctly

#### Modifying Step Content

1. Locate step by `id` in `steps` array
2. Update relevant properties (desc, rules, systems, etc.)
3. Refresh browser to verify changes

#### Adding a New Lane

1. Add lane object to `lanes` array
2. Update `LANE_HEIGHT` calculations if needed
3. Update step `lane` indexes as needed
4. Add lane color CSS variable

#### Creating a New Phase Flowchart

1. Copy existing flowchart as template
2. Update title and header
3. Replace `steps` array with new phase data
4. Replace `connections` array with new flow
5. Adjust lane definitions if actors differ
6. Test all interactions

---

*Start here for all GEODIS HCM Recruiting module documentation.*
*2 ATS systems analyzed | 594 UKG fields mapped | 97.8% coverage | 14 Oracle repository sheets (191 records)*
*Folder reorganized: 6 clean folders | 22 documentation items | Old versions archived*
*Oracle standard tables documented | DFFs reduced from 50 to 18 (-64%) | FIT TO STANDARD approach*
***NEW: 6 Interactive Decision Flowcharts with click-to-display modal details | Dynamic Connector Methodology documented***
