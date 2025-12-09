# GEODIS HR Workflows & Business Processes Catalog

## Document Purpose & Scope

**Project:** GEODIS New HCM - AMARIS
**Document Type:** Workflow Synthesis & Process Documentation
**Status:** IN PROGRESS
**Last Updated:** 2025-12-06

---

### Purpose

This document consolidates and synthesizes all HR workflow documentation from multiple GEODIS sources to:

1. **Catalog** all existing HR business processes across regions (US, Global)
2. **Map** current G-Talent+ workflows to Oracle HCM Cloud equivalents
3. **Identify** gaps, overlaps, and standardization opportunities
4. **Support** the Oracle HCM Cloud implementation with process requirements

### Scope

| Domain | Included | Source |
|--------|----------|--------|
| Recruitment & Onboarding | Yes | HR Blueprint, Zendesk, Talentsoft |
| Employee Lifecycle | Yes | HR Blueprint, Zendesk |
| Performance Management | Yes | HR Blueprint, Talentsoft |
| Compensation & Benefits | Yes | HR Blueprint, Zendesk, Talentsoft |
| Talent Management | Yes | HR Blueprint, Talentsoft |
| Leave Management | Yes | Zendesk |
| Termination | Yes | Zendesk |
| Payroll | Yes | HR Blueprint |

---

## Revision History & Progress Tracking

| Version | Date | Author | Changes | Status |
|---------|------|--------|---------|--------|
| 0.1 | 2025-12-06 | HCM Agent | Initial structure, source inventory | Draft |
| 0.2 | 2025-12-06 | HCM Agent | HR Blueprint review complete (8 PDFs, 8 Mermaid) | In Progress |
| 0.3 | 2025-12-06 | HCM Agent | Zendesk US Processes complete (12 processes, 24 docs) | In Progress |
| 0.4 | 2025-12-06 | HCM Agent | Talentsoft Guidelines complete (44 files extracted) | In Progress |
| 0.5 | 2025-12-06 | HCM Agent | Oracle HCM mapping document created (41 PDFs analyzed) | In Progress |
| 0.6 | 2025-12-06 | HCM Agent | Approval workflows specification (22_), Gap register (23_), Config specs (24_) | In Progress |
| 0.7 | 2025-12-06 | HCM Agent | Process & Security Excel sheets populated (Actions, Reasons, Approvals) | In Progress |
| 0.8 | 2025-12-06 | HCM Agent | Cross-check with CORE HR Template - redundancy analysis complete | In Progress |
| 0.9 | 2025-12-06 | HCM Agent | Security Matrix Oracle tab updated with GEODIS role logic (252 objects) | In Progress |
| 1.0 | 2025-12-06 | HCM Agent | Pending Worker & Contingent Worker access rules added (308 objects); Onboarding process documented | In Progress |

---

## Progress Checklist

### Source Document Review Status

#### HR Blueprint (01 - Discovery/03 - HR Blueprint)

| # | Document | Status | Notes |
|---|----------|--------|-------|
| 1 | [ENG] Processes Summary.pdf | [x] Complete | 7 domains, 52 sub-processes overview |
| 2 | [ENG] Book of functional processes.pdf | [x] Complete | Process matrix/index |
| 3 | [ENG] Talent Acquisition.pdf | [x] Complete | 4 sub-processes, recruitment rules |
| 4 | [ENG] HR Commitment.pdf | [x] Complete | D&I, engagement, communication |
| 5 | [ENG] Administration & Payroll.pdf | [x] Complete | 14 sub-processes, lifecycle + payroll |
| 6 | [ENG] Social & Legal Matters.pdf | [x] Complete | 6 sub-processes, compliance, GDPR |
| 7 | [ENG] Compensation & Benefits.pdf | [x] Complete | 4 sub-processes, grading, LTIP |
| 8 | [ENG] Talent Management & Development.pdf | [x] Complete | 11 sub-processes, learning, mobility |

#### HR Blueprint - Modelization (Mermaid Diagrams)

| # | Document | Status | Notes |
|---|----------|--------|-------|
| 1 | Step 1- Recruitment - Preboarding - Onboarding.mermaid | [x] Complete | Full hire-to-retire lifecycle flow |
| 2 | Step 2- Compensation Planning Cycle.mermaid | [x] Complete | Job grading, annual review, LTIP |
| 3 | Step 3- Performance Management Cycle.mermaid | [x] Complete | Jan-April cycle, SMART objectives |
| 4 | Step 4- Succession and Talent Review.mermaid | [x] Complete | May-Oct, cascade calibration |
| 5 | Step 5- Learning and Development.mermaid | [x] Complete | GEODIS University, G-Learning |
| 6 | Step 7- Payroll Processing Cycle.mermaid | [x] Complete | One cycle per country |
| 7 | Step 10- Benefits Enrollment.mermaid | [x] Complete | Locally managed benefits |
| 8 | Step 12- Employee Transfers and Mobility.mermaid | [x] Complete | IM Coordinator, repatriation |

#### Zendesk Business Processes (US-Specific)

| # | Document | Process Area | Status | Notes |
|---|----------|--------------|--------|-------|
| 1 | Final Onboarding Process.docx | Onboarding | [x] Complete | Background check, I-9/E-Verify within 3 days |
| 2 | Final Onboarding Workflow Process.pptx | Onboarding | [x] Complete | Visual workflow |
| 3 | Final Employee Action Form (EAF) Process.docx | Employee Changes | [x] Complete | All employment profile changes |
| 4 | Final Employee Action Form (EAF) Workflow.pptx | Employee Changes | [x] Complete | Visual workflow |
| 5 | Final Voluntary Termination Process Use.docx | Termination | [x] Complete | ESN required, rehire eligibility matrix |
| 6 | Final Voluntary Termination Workflow.pptx | Termination | [x] Complete | Visual workflow |
| 7 | Final Involuntary Termination Process.docx | Termination | [x] Complete | ESN + termination corrective required |
| 8 | Final Involuntary Termination Workflow.pptx | Termination | [x] Complete | Visual workflow |
| 9 | Final Job Abandonment Process.docx | Termination | [x] Complete | 2 consecutive NC/NS days trigger |
| 10 | Final Job Abandonment Workflow.pptx | Termination | [x] Complete | Visual workflow |
| 11 | Final Personal Leave of Absence Process.docx | Leave | [x] Complete | PLOA with HRD approval required |
| 12 | Final Personal Leave of Absence Workflow.pptx | Leave | [x] Complete | Visual workflow |
| 13 | Medical Leave of Absence Process.docx | Leave | [x] Complete | MLOA/FMLA with VOYA integration |
| 14 | Medical Leave of Absence Workflow.pptx | Leave | [x] Complete | Visual workflow |
| 15 | Final Corrective Action Process.docx | Discipline | [x] Complete | Warning levels, UKG disciplinary tracking |
| 16 | Final Corrective Action Workflow.pptx | Discipline | [x] Complete | Visual workflow |
| 17 | Final ADA Administrative Process.docx | Compliance | [x] Complete | Interactive process, 15-day document return |
| 18 | Final ADA Administation Wrokflow.pptx | Compliance | [x] Complete | Visual workflow |
| 19 | Final Employment Verification Process.docx | Verification | [x] Complete | Work Number primary, 48h SLA |
| 20 | Final Employment Verification Workflow.pptx | Verification | [x] Complete | Visual workflow |
| 21 | Final I-9 Reverification Process.docx | Compliance | [x] Complete | Monthly auto-report, video verification |
| 22 | Final I-9 Reverification Process Workflow.pptx | Compliance | [x] Complete | Visual workflow |
| 23 | Final Compassion Fund Payroll Deduction.docx | Benefits | [x] Complete | Voluntary deduction, bi-weekly processing |
| 24 | Final Compassion Fund Payroll Deduction.pptx | Benefits | [x] Complete | Visual workflow |
| 25 | CLUS - Administrative and Selfservices workflows.pdf | Overview | [ ] Pending | CL US overview (PDF format) |

#### Talentsoft Guidelines (G-Talent+ Current System)

| # | Folder/Document | Process Area | Status | Notes |
|---|-----------------|--------------|--------|-------|
| 1 | Core HR/CORE.HR - EN - Guide - v2.pptx | Core HR | [x] Complete | Employee lifecycle, profile sections |
| 2 | Core HR/User Guide Data Quality.pptx | Data Quality | [x] Complete | Data quality dashboards |
| 3 | Core HR/G-Talent_Guide_Changing Employee Profile.pdf | Employee Data | [x] Complete | Profile change guide |
| 4 | Recruitment/Recruiter Guidelines EN.pptx | Recruitment | [x] Complete | Recruiter workflow |
| 5 | Recruitment/Vacancy Management.pptx | Recruitment | [x] Complete | Vacancy publication |
| 6 | Recruitment/Vacancy Request Management EN.pptx | Recruitment | [x] Complete | Request + approval flow |
| 7 | Recruitment/Selection of applications EN.pptx | Recruitment | [x] Complete | Candidate selection |
| 8 | Recruitment/Management of Speculative Applications.pdf | Recruitment | [x] Complete | Speculative apps workflow |
| 9 | Performance Appraisal/GTalent_Guide_EAP_V2_EN.pptx | Performance | [x] Complete | Full appraisal guide |
| 10 | Performance Appraisal/Performance Appraisal - KPI.xlsx | Performance | [x] Complete | KPI definitions |
| 11 | Salary Review/20242025_Salary_Review_User_Guide.pdf | Compensation | [x] Complete | Manager SR guide |
| 12 | Salary Review/20242025_Salary_Review_Administrator_Guide.pdf | Compensation | [x] Complete | Admin SR guide |
| 13 | People Review/Guide People Review - Campaign Management.pptx | Talent Review | [x] Complete | Campaign setup |
| 14 | Campaign Management/GTalent_Guide_EN_Campaign Administrator.pptx | Campaigns | [x] Complete | Admin workflow |
| 15 | Campaign Management/GTalent_Guide_EN_Piloting the campaign.pptx | Campaigns | [x] Complete | Campaign monitoring |
| 16 | Campaign Management/G-Talent_Mid year review_ENG.pptx | Mid-Year | [x] Complete | Mid-year creation |
| 17 | Exit Interview/GT_Exit Interview_En.pptx | Offboarding | [x] Complete | Mandatory for managers |
| 18 | Assigned employees/Assigned employees_EN.pptx | Assignment | [x] Complete | Assignment management |
| 19 | Guides Minerve+/GTalent_Guide_Minerve+.pptx | Minerve+ | [x] Complete | Minerve+ integration |
| 20 | Geodis_HR_KPIs_Manual.pdf | HR KPIs | [x] Complete | 75+ indicator definitions |

#### Oracle Documentation (01 - Discovery/05 - Oracle Documentation)

| # | Document | Module | Status | Notes |
|---|----------|--------|--------|-------|
| 1 | implementing-recruiting.pdf | Recruiting | [x] Complete | Requisition, templates, workflows |
| 2 | using-recruiting.pdf | Recruiting | [x] Complete | End-user processes |
| 3 | implementing-performance-management.pdf | Performance | [x] Complete | Templates, process flows |
| 4 | using-performance-management.pdf | Performance | [x] Complete | User guide |
| 5 | implementing-and-using-journeys.pdf | Journeys | [x] Complete | Onboarding, offboarding |
| 6 | implementing-talent-review-and-succession-management.pdf | Talent | [x] Complete | Succession planning |
| 7 | hcm-data-loader.pdf | Integration | [x] Complete | Data migration |
| 8 | + 33 additional Oracle HCM PDFs | Various | [x] Complete | See oracle_hcm_docs_extracted.txt |

#### Process & Security Sheets (02 - Define/01 - Repositories/04 - SHEETS)

| # | File | Content | Status | Records |
|---|------|---------|--------|---------|
| 1 | Approval Workflows.xlsx | BPM approval workflow definitions | [x] Complete | 31 workflows |
| 2 | Action.xlsx | GEODIS-specific HR action types | [x] Complete | 41 actions (added 4 onboarding actions) |
| 3 | Action & Reasons.xlsx | GEODIS-specific action reason codes | [x] Complete | 67 reasons (after removing 3 redundant) |
| 4 | Security Matrix.xlsx | Oracle HCM security matrix with GEODIS roles (7 roles + 2 worker types) | [x] Complete | 308 data objects |

**Approval Workflows by Module:**
- Recruiting: 3 (Requisition, TOPEX Requisition, Offer)
- Core HR: 8 (Hire, Transfer, Promotion, Terminations)
- Compensation: 4 (Salary Review, Ad-Hoc, TOPEX, Bonus)
- Performance: 2 (Goal, Performance Document)
- Absence: 4 (Standard, PLOA, MLOA, ADA)
- Learning: 4 (Internal, External, High-Cost, Leadership)
- Talent: 3 (Succession, HP Pool, Pool Removal)

**Actions by Type:**
- Add Assignment: 6 (Hire, Rehire, CWK, Pending, Convert Pending)
- Change Assignment: 13 (Promote, Transfer, Demote, etc.)
- Compensation Change: 5 (Salary, Bonus, LTIP)
- Global Transfer: 5 (International, Secondment, Expatriation)
- End Assignment: 4 (Terminate voluntary/involuntary)
- Suspend/Leave: 5 (Leave, Suspend, Reactivate)
- Trial Period: 4 (Extend, Complete, Fail, Renew/End Notices)
- Other: 2 (Data Correction, Retro Change)

**Key Reason Codes:**
- Voluntary Termination: 14 reasons (from Zendesk US)
- Involuntary Termination: 16 reasons (from Zendesk US)
- Leave: 7 reasons (MLOA, FMLA, PLOA, etc.)
- Promotion: 5 reasons (Merit, People Review, etc.)

#### Cross-Check Analysis: CORE HR Template vs Populated Sheets

**Reference Template:** `GEODIS_Repositories_CORE HR_Template.v26.11.25.xlsx`

The CORE HR Template is the master Oracle HCM configuration repository containing Oracle standard values. The Process & Security sheets contain GEODIS-specific additions discovered from HR Blueprint, Zendesk, and Talentsoft sources.

**Purpose of Each Tab:**

| Tab | Purpose | Oracle Standard | GEODIS Customization |
|-----|---------|-----------------|----------------------|
| Action | HR transaction types (Hire, Terminate, etc.) | 88 standard codes | 37 GEODIS-specific codes |
| Action & Reasons | Maps actions to reasons (WHY an action occurred) | 75 standard codes | 64 GEODIS-specific codes |
| Approval Workflows | Defines approver chains for each action | 25 workflows (all bypass) | 31 workflows with approver chains |

**Cross-Check Results:**

| Metric | Action | Action & Reasons | Approval Workflows |
|--------|--------|------------------|-------------------|
| Template records | 88 | 75 | 25 |
| Populated records | 42 | 65 | 31 |
| Overlapping | 5 | 1 | 0 |
| New GEODIS value | 37 | 64 | 31 |

**Action Codes - Overlap (5 codes to avoid duplication):**
- `ADD_CWK`, `GLB_TRANSFER`, `HIRE`, `REHIRE`, `TRANSFER`

**Action Codes - GEODIS-Specific (37 new codes):**
- Termination: `TERMINATE_VOL`, `TERMINATE_INVOL`, `TERMINATE_CWK`
- Compensation: `SALARY_CHANGE`, `SALARY_REVIEW`, `BONUS`, `LTIP_AWARD`, `WELCOME_BONUS`
- Leave: `LEAVE_START`, `LEAVE_RETURN`, `LEAVE_EXTEND`
- Global: `EXPATRIATION`, `REPATRIATION`, `SECONDMENT`
- Changes: `CHG_MANAGER`, `CHG_LOCATION`, `CHG_DEPARTMENT`, `CHG_COST_CENTER`, etc.

**Action Reasons - GEODIS-Specific (64 new codes from Zendesk US):**

*Voluntary Termination Reasons:*
- `OTHER_JOB`, `PERSONAL_FAMILY`, `MOVING`, `RETIREMENT`, `CAREER_DEV`
- `DISSATISFIED_PAY`, `DISSATISFIED_MGMT`, `DISSATISFIED_DUTIES`, `DISSATISFIED_HOURS`
- `EDUCATION`, `MILITARY`, `WALKOUT`

*Involuntary Termination Reasons:*
- `PERFORMANCE`, `ATTENDANCE`, `POLICY_MISC`, `GROSS_MISCONDUCT`
- `HARASSMENT`, `VIOLENCE`, `DRUG_POLICY`, `THEFT`, `SAFETY`
- `JOB_ABANDONMENT`, `I9_FAILURE`, `PROBATION_FAIL`, `RIF`

*Leave Reasons:*
- `FMLA`, `MLOA`, `PLOA`, `MATERNITY`, `PATERNITY`, `SABBATICAL`

**Approval Workflows - GEODIS Requirements (not in template):**

The template has 25 Oracle Quick Actions all set to "Bypass=Yes" (auto-approve). GEODIS requires actual approval chains:

| Workflow | GEODIS Requirement |
|----------|-------------------|
| Requisition | N+1 > HR BP > EVP HR (if >= 125k EUR) |
| TOPEX Requisition | N+1 > HR BP > CHRO |
| Job Offer | Hiring Mgr > HR/Comp > EVP HR (if >= 125k or 155k package) |
| Promotion | N+1 > HR (mandatory - manager cannot approve alone) |
| Involuntary Termination | HR > HR Director |
| Misconduct Termination | HR > HR Director > Legal |
| Salary Review | N+1 > HR/CnB > EVP HR (if above guideline or >= 125k) |

**Recommendations:**

1. **Remove 5 overlapping action codes** from Process & Security `Action.xlsx`
2. **Keep 37 GEODIS-specific actions** - these ADD to the template
3. **Remove 1 overlapping reason** (REORG) from `Action & Reasons.xlsx`
4. **Keep 64 GEODIS-specific reasons** - these ADD to the template
5. **Merge approval workflows** - populate template with GEODIS approver chains

#### Security Matrix Oracle - GEODIS Role Logic

**File:** `Security Matrix.xlsx` → Tab: `Security Matrix Oracle`

The Security Matrix Oracle tab has been updated with GEODIS-specific role logic based on:
- Role Rationalization Analysis (43 → 18 target roles)
- HR Blueprint (7 domains, 52 sub-processes)
- Zendesk US Processes (12 process areas)
- Approval Workflows (31 workflows with approver chains)

**GEODIS Roles (Columns 3-9):**

| Column | Role | Description | Source |
|--------|------|-------------|--------|
| 3 | Employee (GEODIS) | Self-service access | Rationalization + HR Blueprint |
| 4 | Line Manager (GEODIS) | Direct/indirect reports management | Rationalization + Workflows |
| 5 | HR Business Partner (GEODIS) | Local/Regional HR operations | Rationalization + Zendesk |
| 6 | Recruiter (GEODIS) | Recruitment operations | HR Blueprint + Workflows |
| 7 | HR Administrator (GEODIS) | HR Admin operations (onboarding, terminations) | Zendesk + Workflows |
| 8 | Pending Worker (GEODIS) | Pre-hire status, preboarding access | Onboarding Workshops |
| 9 | Contingent Worker (GEODIS) | External worker, limited access | Onboarding Workshops |

**Access Levels Applied:**

| Level | Color | Description |
|-------|-------|-------------|
| Update | Green | Full create/read/update access |
| Read Only | Yellow | View access only |
| No Access | Red | Blocked access |
| Initiate | Blue | Can start transaction (requires approval) |
| Approve | Light Green | Can approve transactions |
| N/A | Gray | Not applicable to this role |

**Key Workflow Rules Applied:**

| Rule | Access Pattern |
|------|----------------|
| Salary ≥ €125k | Line Manager: Initiate → HR BP: Approve → EVP HR |
| TOPEX Positions | Line Manager: Initiate → HR BP: Approve → CHRO |
| Promotions | Line Manager: Initiate → HR BP: Approve (mandatory) |
| Involuntary Termination | Line Manager: Initiate → HR BP: Approve → HR Director |
| Salary Data | HR Admin: No Access (restricted to Compensation roles) |

**Data Objects Updated:** 252 objects across sections:
- Personal Info (29 objects)
- Document Records (4 objects)
- Employment (45 objects)
- Compensation (12 objects)
- Career and Performance (12 objects)
- Workforce Structures (19 objects)
- Payroll (5 objects)
- Mass Updates (2 objects)
- Tools (5 objects)

**Pending Worker Access Rules (Preboarding Phase):**

| Data Category | Access | Rationale |
|--------------|--------|-----------|
| Personal Info (photo, address, contacts) | Update | Self-service during preboarding |
| Documents (upload) | Update | Document collection phase |
| Bank Information | Update | Required for transport refund |
| Education/Certifications | Update | Background capture |
| Employment Info | Read Only | HR manages assignment |
| Salary/Compensation | No Access | Not visible until active |
| HR Actions | No Access | Restricted to HR roles |

**Contingent Worker Access Rules:**

| Data Category | Access | Rationale |
|--------------|--------|-----------|
| Personal Info | Update | Self-service like employee |
| Documents | Update | Can upload documents |
| Skills/Qualifications | Update | Maintain skill profile |
| Employment Info | Read Only | Limited visibility |
| Payroll/Bank Info | No Access | Paid via vendor |
| Salary/Compensation | No Access | No internal compensation |
| HR Actions | No Access | Restricted to HR roles |

**Reference:** `RolesEtDroits.csv` (G.A.R.V.I.S) - 50+ G-Talent+ roles with 700+ rights analyzed for rationalization.

---

## Source Files Inventory

### Source 1: HR Blueprint

**Path:** `01 - Discovery/03 - HR Blueprint`

| Subfolder | Content | File Count |
|-----------|---------|------------|
| 01 - Blueprint per process | PDF process documents (ENG) | 8 files |
| 02 - Blueprint modelization | Mermaid workflow diagrams | 8 files |

**Key Documents:**
- Processes Summary (overview)
- Functional process book
- Domain-specific guides (Talent Acquisition, Compensation, etc.)

### Source 2: Zendesk Business Processes

**Path:** `01 - Discovery/07 - Zendesk Business Processes`

| Content Type | Count | Format |
|--------------|-------|--------|
| Process Documents | 13 | .docx |
| Workflow Diagrams | 12 | .pptx |
| Overview | 1 | .pdf |

**Coverage:** US-specific administrative and self-service workflows

### Source 3: Talentsoft Guidelines

**Path:** `01 - Discovery/08 - Talentsoft Guidelines`

| Subfolder | Content | Files |
|-----------|---------|-------|
| Core HR | Core HR guides, data quality | 3 |
| Recruitment | Vacancy, selection, recruiter guides | 7 |
| Performance Appraisal | EAP guide, KPIs | 2 |
| Salary Review | User & Admin guides, videos | 5 |
| People Review | Campaign management | 1 |
| Campaign Management | Admin, piloting, mid-year | 5 |
| Exit Interview | Exit interview guide | 1 |
| Assigned employees | Assignment guide | 1 |
| Guides Minerve+ | Minerve+ integration | 1 |
| Job Referential | Job reference video | 1 |

---

## Process Domains

### 1. Recruitment & Talent Acquisition

**Oracle HCM Module:** Recruiting

| Process | Current System | Source Documents | Oracle Equivalent |
|---------|----------------|------------------|-------------------|
| Vacancy Request | G-Talent+ | Vacancy Request Management EN | Requisition |
| Vacancy Management | G-Talent+ | Vacancy Management.pptx | Job Posting |
| Application Selection | G-Talent+ | Selection of applications EN | Candidate Selection |
| Speculative Applications | G-Talent+ | Management of Speculative Applications.pdf | Talent Pool |
| Recruiter Workflow | G-Talent+ | Recruiter Guidelines EN | Recruiting Role |

**Workflow Summary (from HR Blueprint 2.1-2.6):**

| Sub-Process | Key Rules | Tools |
|-------------|-----------|-------|
| 2.1 Employer Branding | Career site, social media, employer awards | G-Talent+, Career Site |
| 2.2 Recruitment Need & Job Description | Internal posting 1 week min; Vacancy expires at 6 months | G-Talent+, Job Referential |
| 2.3 Candidate Selection/Search | Reference checks mandatory for white collar; CV screening criteria | G-Talent+ |
| 2.4 Offer Management | 90-day agency contract max; Salary benchmarking required | G-Talent+ |
| 2.5 TopEx Position Management | CHRO approval required; Succession planning integration | TopEx Policy |
| 2.6 TopEx Recruitment | CHRO validates external; Must interview 1 internal candidate | TopEx Policy |

**Key Business Rules:**
- Internal posting minimum 1 week before external
- Vacancy request expires after 6 months (must restart)
- €125k threshold requires EVP HR approval
- Reference checks mandatory for white collar positions
- TOPEX positions require CHRO approval and succession planning

---

### 2. Onboarding & Preboarding

**Oracle HCM Module:** Onboarding, Journeys

| Process | Region | Source Documents | Oracle Equivalent |
|---------|--------|------------------|-------------------|
| Onboarding Process | US | Final Onboarding Process.docx | Onboarding Journey |
| Preboarding | Global | Step 1 Mermaid | Preboarding Checklist |
| I-9 Verification | US | I-9 Reverification Process | Work Eligibility |
| Background Check | US | Onboarding Process | Pre-Hire Checklist |

**Workflow Summary (from HR Blueprint 3.1-3.2):**

| Sub-Process | Key Rules | Tools |
|-------------|-----------|-------|
| 3.1 Employee Onboarding & Induction | Create G-Talent+ file 2 weeks before arrival; Contract signed Day 1 (48h for fixed-term) | G-Talent+, G-Campus |
| 3.2 Probation Review | Mid-probationary interview mandatory; End-probation meeting required | Onboarding tool |

**Workflow Summary (from Zendesk - US Specific):**

| Step | Description | SLA | System |
|------|-------------|-----|--------|
| Offer Accepted | Local HR/Recruiter emails HRSC with candidate details | 48h before start | Zendesk |
| Background Check | Sterling background check launched; monitored daily | Must clear before start | Sterling |
| Onboarding Docs | Launch via Onboarding Gateway; candidate completes | 24h to complete | UKG Onboarding Gateway |
| Orientation Confirmation | HRSC calls/texts candidate to confirm date/time/location | Same day as ticket | Zendesk |
| I-9/E-Verify | Local HR completes I-9 and E-Verify | Within 3 days of start | UKG/E-Verify |
| Failure to Provide I-9 | ESN submitted if IDs not provided by Day 3 | Day 3 | UKG |

**Key Business Rules (Global + US):**
- Employee file created in G-Talent+ at least 2 weeks before arrival
- Employment contract/offer signed on Day 1 (within 48 hours for fixed-term)
- Buddy system encouraged for cultural integration
- Mandatory trainings include Welcome @ GEODIS, compliance, prevention & safety
- Welcoming compliance package includes Code of Ethics, Anti-corruption policy

#### GEODIS Onboarding Process (UES France ServiceNow Pilot)

**Source:** Onboarding - Workshops.pdf (35 pages)
**Scope:** UES France - ServiceNow pilot implementation

**Onboarding Timeline:**

```
Recruitment → Preboarding (45 days) → Day 1 → Week 1 → Month 1 → Month 3 → Trial Period End
```

| Phase | Timeline | Key Activities |
|-------|----------|----------------|
| Preboarding | -45 days to Day 1 | Document collection, HRACCESS profile creation |
| Day 1 | Arrival | Welcome, equipment, administrative tasks |
| Week 1 | Days 1-5 | Team integration, initial trainings |
| Month 1 | Days 1-30 | Role onboarding, manager check-in |
| Month 3 | Days 60-90 | Probation review, development plan |
| Trial Period | Varies | Renewal/End notices (-8 days, -3 weeks) |

**Preboarding Tasks by Role:**

| Task | HR | Newcomer | Manager | IT | Facilities |
|------|:--:|:--------:|:-------:|:--:|:----------:|
| Create ServiceNow ticket | X | | | | |
| Provide badge photo | | X | | | |
| Send bank information | | X | | | |
| Health insurance affiliation | | X | | | |
| Complete personal documents | | X | | | |
| Prepare workspace | | | | | X |
| Configure equipment | | | | X | |
| Set up HRACCESS profile | X | | | | |
| Assign buddy | | | X | | |

**System Interfaces Flow:**

```
TS Recruitment → ServiceNow (GEOBUS) → TS Core RH → LDAP → HR ACCESS
```

| System | Function | Timing |
|--------|----------|--------|
| TS Recruitment | Candidate selection, offer | Before hire |
| ServiceNow | Onboarding workflow orchestration | From offer acceptance |
| TS Core RH | Employee master data | Created during preboarding |
| LDAP | Directory services | -7 days |
| HR ACCESS | IT systems access | -7 days |

**Preboarding Checklist (Newcomer Tasks):**

1. **Photo for Badge** - Required for building access
2. **Bank Information** - For transport refund (RPC) processing
3. **Health Insurance** - Affiliation documents
4. **Beneficiary Designation** - Emergency contacts, insurance beneficiaries
5. **Personal Documents** - ID, diplomas, certifications

**HRACCESS Profile Creation:**
- Created 7 days before Day 1
- Synced from TS Core RH to LDAP
- Enables IT systems access on Day 1

**Trial Period Management:**

| Notice Type | Timing | Action |
|-------------|--------|--------|
| Renewal Notice | -8 days before end | Manager decision required |
| End Notice | -3 weeks before end | Final probation review |
| Extension | If applicable | HR approval required |
| Confirmation | End of trial | Automatic if no action |

**Onboarding Portal Requirements:**

- Bilingual: English + French
- GEODIS + HelpNow branding
- Self-service document upload
- Task tracking dashboard
- Integration with ServiceNow

**Key Roles & Responsibilities:**

| Role | Abbreviation | Responsibilities |
|------|--------------|------------------|
| HR | HR | Process owner, compliance, documentation |
| Newcomer | N | Self-service tasks, document submission |
| Manager | M | Team integration, buddy assignment, probation review |
| IT | IT | Equipment, system access, HRACCESS |
| Facilities | Fac | Workspace, badge, building access |
| Car Management | C | Vehicle assignment (if applicable) |
| Recruitment | R | Candidate handoff, offer finalization |
| ServiceNow | SN | Workflow automation, ticket management |

**US-Specific Rules (Zendesk):**
- Background check MUST clear before start (no exceptions for exempt/salaried roles except SVP HR approval)
- Non-exempt roles may start pending local checks if national criminal clears (with SVP HR approval)
- I-9 and E-Verify must be completed within 3 days of hire date
- If I-9 not completed by Day 3, termination required (Failure to satisfy I-9 requirements)
- Email subject line format: "Offer Accepted – [Candidate Name] – [Anticipated Start Date]"
- Peak accounts require account number in subject line
- Zendesk ticket marked Urgent priority

---

### 3. Employee Lifecycle & Administration

**Oracle HCM Module:** Core HR, Employment

| Process | Region | Source Documents | Oracle Equivalent |
|---------|--------|------------------|-------------------|
| Employee Action Form | US | EAF Process/Workflow | Employment Change |
| Employee Profile Change | Global | G-Talent Guide Changing Profile | Person/Assignment Update |
| Employment Verification | US | Employment Verification Process | Employment Verification |
| Employee Transfer | Global | Step 12 Mermaid | Transfer Action |
| Corrective Action | US | Corrective Action Process | Disciplinary Action |
| I-9 Reverification | US | I-9 Reverification Process | Work Eligibility |

**Workflow Summary (from HR Blueprint 4.1-4.11):**

| Sub-Process | Key Rules | Tools |
|-------------|-----------|-------|
| 4.1-4.3 Recruitment to Induction | Pre-boarding 2 weeks; Trial period management | G-Talent+ |
| 4.4 Employee Data Administration | Update G-Talent+ within 5 days of departure | G-Talent+ |
| 4.5 Business Travel | Follow company travel policy | Travel System |
| 4.6 Expenses | Expense management per policy | Expense System |
| 4.7 Disciplinary Procedures | HR validation required; No manager-only decisions | G-Talent+ |
| 4.8 Health & Security | Local compliance required | Local Systems |
| 4.9 Professional Evolution | Career progression framework | G-Talent+ |
| 4.10 Learning | Track completions in G-Talent+ | G-Campus, G-Learning |
| 4.11 Offboarding | Exit interview mandatory for white collar | G-Talent+ |

**Workflow Summary (from Zendesk - US Specific):**

**Employee Action Form (EAF) Process:**

| Change Type | Documentation Required |
|-------------|----------------------|
| Change Supervisor | No documentation (unless coupled with other changes) |
| Change Job Title | Signed Offer Letter with Manager and HR Approval |
| Change Profit Center | Signed Offer Letter with Manager and HR Approval |
| Change Employee Type | Signed Offer Letter with Manager and HR Approval |
| Change P/T or F/T | Signed Offer Letter with Manager and HR Approval |
| Change Pay Rate | Signed Offer Letter with Manager and HR Approval |
| Change Allocations | Email from Accounting Approving the Request |

**Corrective Action Process:**

| Step | Description | SLA |
|------|-------------|-----|
| Submit Corrective | Supervisor emails signed Employee Warning Notice | Within 24h of delivery |
| HR Signature | Required on all correctives except attendance warnings | Before processing |
| UKG Update | HRSC updates Disciplinary Action section in Insight | Same day |
| Upload to File | Document uploaded to Employee Relations category | Before ticket close |

**I-9 Reverification Process:**

| Step | Description | Timeline |
|------|-------------|----------|
| Auto-Report | HRIS generates monthly report of upcoming expirations | 30 days advance |
| Contact Employee | HRSC calls/texts employee to schedule verification | 2 weeks before expiration |
| Video Verification | Video call to verify document authenticity | Before expiration |
| Non-Response | If no response 2 weeks before, escalate to Local HR | 2 weeks before |
| Termination | If documents expire without renewal, terminate same day | On expiration date |

**Employment Verification Process:**

| Method | Primary | Backup |
|--------|---------|--------|
| Standard Verification | Work Number | HRSC manual completion |
| Government Agencies | HRSC manual completion | Fax or email submission |
| SLA | 48 hours from receipt | - |

**Key Business Rules (Global):**
- Update G-Talent+ within 5 days of employee departure
- Exit interviews mandatory for white collar only
- Disciplinary actions require HR validation (no manager-only decisions)
- All data changes must comply with GDPR

**Key Business Rules (US Zendesk):**
- All EAFs must be received by 12:30 PM CST on Friday before pay date
- EAF changes require approval in Recruiting Gateway
- Allocation changes require email approval from Finance
- Corrective actions for attendance do not require HR signature
- Bargaining unit correctives include approval email instead of HR signature
- I-9 reverification terminated if documents not provided by expiration date
- Employment verification completed within 48 hours

---

### 4. Performance Management

**Oracle HCM Module:** Performance Management

| Process | Current System | Source Documents | Oracle Equivalent |
|---------|----------------|------------------|-------------------|
| Annual Performance Appraisal | G-Talent+ | GTalent_Guide_EAP_V2_EN | Performance Document |
| Mid-Year Review | G-Talent+ | G-Talent_Mid year review_ENG | Check-In |
| Campaign Management | G-Talent+ | Campaign Administrator.pptx | Performance Template |
| People Review | G-Talent+ | Guide People Review | Talent Review |

**Workflow Summary (from HR Blueprint 3.3-3.4):**

| Sub-Process | Key Rules | Tools |
|-------------|-----------|-------|
| 3.3 Performance Appraisal | January-April (extension to June); 2 weeks notice; SMART objectives required | G-Talent+, Training Catalogs |
| 3.4 People Review & Succession | May-October; Cascade: Country→Region→LoB→Group | TopEx Policy |

**Key Business Rules:**
- Performance appraisals: January to April (possible extension to June)
- Employee must be notified 2 weeks in advance of appraisal meeting
- SMART objectives: Specific, Measurable, Audience-specific, Realistic, Time-bound
- Objectives must be recorded in G-Talent+ by end of 1st semester
- Mid-year interview mandatory if employee requests
- People Review: May to October, cascade calibration process
- Talent segmentation: High Potential, Key Talent, Core Contributors
- Succession readiness: Ready Now, Ready 1-2 Years, Ready 3+ Years

---

### 5. Compensation & Benefits

**Oracle HCM Module:** Compensation, Benefits

| Process | Region | Source Documents | Oracle Equivalent |
|---------|--------|------------------|-------------------|
| Salary Review | Global | Salary Review User/Admin Guides | Compensation Plan |
| Compensation Planning | Global | Step 2 Mermaid | Workforce Compensation |
| Benefits Enrollment | Global | Step 10 Mermaid | Benefits Enrollment |
| Compassion Fund | US | Compassion Fund Process | Voluntary Deduction |

**Workflow Summary (from HR Blueprint 5.1-5.4):**

| Sub-Process | Key Rules | Tools |
|-------------|-----------|-------|
| 5.1 Grading & Package Design | Mercer/WTW/Korn Ferry methodologies; Position Q1-Q3 market | Job Referential |
| 5.2 Compensation Administration | Annual review April; €125k threshold EVP HR approval; Variable non-discretionary | G-Talent+ |
| 5.3 Benefits Programs | Locally managed; Follow country regulations | Local Systems |
| 5.4 Retention/LTIP | CHO managed; TOPEX/Fast Trackers/Key People only | TopEx Policy |

**Key Business Rules:**
- Job grading: Mercer IPE, Willis Towers Watson, or Korn Ferry Hay
- Market positioning: Between Q1 (25th percentile) and Q3 (75th percentile)
- Salary review: Once a year in April
- €125k threshold (2025) requires EVP HR approval for entire Group
- Variable compensation: Must be non-discretionary, at least one financial KPI
- New joiners after October 1: Welcome Bonus instead of annual bonus (after probation)
- TOPEX compensation changes require CHO approval
- Benefits managed locally per country regulations

---

### 6. Leave Management

**Oracle HCM Module:** Absence Management

| Process | Region | Source Documents | Oracle Equivalent |
|---------|--------|------------------|-------------------|
| Personal Leave of Absence | US | Personal LOA Process | Absence Request |
| Medical Leave of Absence | US | Medical LOA Process | Medical Leave |
| ADA Accommodation | US | ADA Administrative Process | Accommodation Request |
| FMLA Leave | US | Medical LOA Process | FMLA Leave |

**Workflow Summary (from Zendesk - US Specific):**

**Personal Leave of Absence (PLOA) Process:**

| Step | Description | SLA/Timeline |
|------|-------------|--------------|
| Request Initiation | Employee or Local HR emails HRSC | Priority ticket |
| Approval Chain | Local HR → HRD approval required | Before HRSC processes |
| Approval Letter | HRSC creates and sends approval letter | Within 24 hours |
| Status Change | EAF submitted to change status to PLOA | On leave start date |
| RTW Confirmation | HRSC contacts employee 2 weeks before return | 2 weeks before RTW |
| Return to Active | EAF submitted to return to active status | On return date |
| No Return | ESN submitted with "Did not return from LOA" | On expected return date |

**Medical Leave of Absence (MLOA/FMLA) Process:**

| Step | Description | SLA/Timeline |
|------|-------------|--------------|
| Request Initiation | Local HR emails HRSC with completed LOA request | High priority ticket |
| VOYA Integration | If FMLA, employee contacts VOYA for claim number | Before approval |
| Approval Letter | HRSC creates and sends MLOA approval letter | Within 24 hours |
| Status Change | EAF submitted; Leave Reason = "Leave Pending" if awaiting VOYA | On leave start date |
| VOYA Determination | Update EAF when VOYA confirms FMLA status | When received |
| RTW Confirmation | HRSC contacts employee 2 weeks before return | 2 weeks before RTW |
| Return/Termination | EAF to active or ESN if no return | On return date |

**ADA Accommodation Process:**

| Step | Description | Timeline |
|------|-------------|----------|
| Request Received | Local HR emails HRSC with accommodation request | Same day ticket |
| Temporary Accommodation | HRSC creates temporary accommodation letter | Same day |
| Medical Certification | ADA Medical Certification Form sent to employee | With temporary letter |
| Document Return | Employee returns completed certification | 15 days (3 extensions max) |
| Interactive Process | Local HR reviews and determines accommodation | After docs received |
| Final Decision | Approval or Denial letter created and sent | After decision |
| Ticket Close | Upload all documents to UKG Medical category | Before close |

**Leave Status Codes in UKG:**

| Status | Description |
|--------|-------------|
| Leave Pending | Awaiting VOYA determination for FMLA |
| FMLA | Approved Family/Medical Leave Act leave |
| Leave-Medical | Non-FMLA medical leave |
| PLOA | Personal Leave of Absence |

**Key Business Rules (from HR Blueprint):**
- Absence records collected for payroll processing
- Local regulations govern leave types and entitlements
- Time and attendance integration with payroll required

**Key Business Rules (US Zendesk):**
- All PLOA requests require HRD approval before processing
- MLOA requests require completed Request for LOA form + physician documentation
- VOYA handles FMLA/disability claims and provides claim numbers
- ADA Medical Certification must be returned within 15 days (max 3 extensions)
- After 3rd extension without documents, ADA request is denied
- Leave status must be updated via EAF on leave start date
- Employee must confirm return 2 weeks before expected RTW date
- If employee does not return as planned, ESN submitted same day

---

### 7. Talent Management & Development

**Oracle HCM Module:** Talent Management, Learning

| Process | Current System | Source Documents | Oracle Equivalent |
|---------|----------------|------------------|-------------------|
| Succession Planning | G-Talent+ | Step 4 Mermaid | Succession Management |
| Learning & Development | G-Talent+ | Step 5 Mermaid | Learning |
| Talent Review | G-Talent+ | People Review Guide | Talent Review |

**Workflow Summary (from HR Blueprint 3.5-3.10):**

| Sub-Process | Key Rules | Tools |
|-------------|-----------|-------|
| 3.5 Learning Identification | No global learning without University/HR approval | Performance Appraisals, People Reviews |
| 3.6 Learning Design | In-house preferred; External needs internal supervisor | G-Learning |
| 3.7 Learning Delivery | 15 days advance invitation; Attendance mandatory once confirmed | G-Campus, G-Learning |
| 3.8 Learning Follow-up | Administrative file required; Annual learning review | G-Talent+, End-of-learning forms |
| 3.9 Promotion/Repositioning | Must be based on People Review or internal mobility; HR validation required | TopEx Policy |
| 3.10 Employee Mobility | IM Coordinator for international; Non-poaching policy | International Mobility Policy |

**Key Business Rules:**
- Training target: 1 training per employee every 2 years
- Training invitation: 15 days minimum advance notice
- No global learning initiative without University/HR approval
- Promotions must be based on People Review or internal mobility process
- Manager cannot validate promotion alone - HR required
- International mobility supervised by IM Coordinator
- Non-poaching policy applies to all mobility types
- GEODIS University platforms: GEODIS University, G-Campus, G-Learning

---

### 8. Termination & Offboarding

**Oracle HCM Module:** Core HR, Journeys

| Process | Region | Source Documents | Oracle Equivalent |
|---------|--------|------------------|-------------------|
| Voluntary Termination | US | Voluntary Termination Process | Termination - Resignation |
| Involuntary Termination | US | Involuntary Termination Process | Termination - Involuntary |
| Job Abandonment | US | Job Abandonment Process | Termination - Abandonment |
| Exit Interview | Global | GT_Exit Interview_En | Exit Survey |
| Corrective Action | US | Corrective Action Process | Disciplinary Action |

**Workflow Summary (from HR Blueprint 3.11, 6.2):**

| Sub-Process | Key Rules | Tools |
|-------------|-----------|-------|
| 3.11 Offboarding | Exit interviews mandatory white collar only; All dismissals coordinated by HR | G-Talent+, Offboarding checklist |
| 6.2 Disciplinary Action | No action without HR validation; Major infractions escalate to higher HR | Disciplinary records |

**Workflow Summary (from Zendesk - US Specific):**

**Voluntary Termination Process:**

| Step | Description | SLA |
|------|-------------|-----|
| ESN Submission | Supervisor emails ESN to HRSC on last day | On last day |
| Documentation | Notice of Resignation required (email/text/form) | With ESN |
| Processing | HRSC submits ESN to HRDM for processing | Within 24 hours |
| Upload | ESN + resignation notice uploaded to UKG | Before ticket close |
| Separation Notice | State-required separation notice sent (if applicable) | After processing |
| Exit Survey | Survey Monkey link sent to exempt employees | With separation notice |

**Involuntary Termination Process:**

| Step | Description | SLA |
|------|-------------|-----|
| ESN Submission | Supervisor emails ESN + Termination Corrective to HRSC | On last day |
| Documentation | Employee Warning Notice with signatures required | With ESN |
| Off-boarding | Service Now ticket required if employee had network access | Before ESN |
| Processing | HRSC submits ESN to HRDM | Within 24 hours |
| Upload | ESN + Corrective uploaded to UKG (ESN Form + Employee Relations) | Before ticket close |
| Separation Notice | State-required notice + Benefit FAQs sent | After processing |

**Job Abandonment Process:**

| Step | Description | Timeline |
|------|-------------|----------|
| Trigger | 2 consecutive No Call/No Show days | 4 hours into 2nd day |
| Notification | Supervisor emails HRSC to initiate | Same day as 2nd NC/NS |
| Contact Attempt | HRSC calls, texts, and emails employee | Same day |
| Response Deadline | Employee given 24 hours to respond | Next day |
| LOA Review | If circumstances may qualify for LOA, redirect to Local HR | If applicable |
| ESN Request | If no response/no LOA, HRSC requests ESN from supervisor | After 24 hours |
| Termination | ESN submitted with "Job Abandonment" reason | 2nd NC/NS date |

**Voluntary Termination Reason Codes:**

| Term Reason | Description | Rehire Eligibility | Exceptions |
|-------------|-------------|-------------------|------------|
| Did not Return from LOA | Failed to return/contact after leave | Rehire | - |
| Dissatisfied - Hours | Unhappy with schedule/hours | Rehire | - |
| Dissatisfied - Management | Unhappy with management | Rehire | - |
| Dissatisfied - Job Duties | Unhappy with work nature | Rehire | - |
| Dissatisfied - Pay | Unhappy with compensation | Rehire | - |
| Education | Leaving for school | Rehire | - |
| Job Abandonment NC/NS | 2 consecutive NC/NS days | Do Not Rehire | 1 year with Account Mgr + HR review |
| Moving | Relocating out of area | Rehire | - |
| Mutual Agreement | With severance typically | Rehire | - |
| No Reason Given | Reason not specified | Rehire | - |
| Other Job | Left for other employment | Rehire | - |
| Personal/Family | Personal/family reasons | Rehire | - |
| Retirement | Retirement | Rehire | - |
| Quit No Notice - Walk Out | Walked off job | Do Not Rehire | 1 year with Account Mgr + HR review |

**Involuntary Termination Reason Codes:**

| Term Reason | Description | Rehire Eligibility | Exceptions |
|-------------|-------------|-------------------|------------|
| Cannot Perform Duties | Unable to perform after ADA process | Rehire | - |
| Excessive Absences/Tardiness | Reached 15 pts in 12 months or 6 pts in 90 days | Do Not Rehire | 6 months with Account Mgr + HR review |
| Death | Death | N/A | - |
| Failed to Meet I-9 Requirements | No work authorization within 72h or reverification failed | Rehire | - |
| Gross Misconduct | Code of conduct violation | Do Not Rehire | No Exceptions |
| Ineligible for Leave | Absence >3 days without FMLA/PLOA/PTO approval | Rehire | - |
| Performance | Poor performance with corrective action | Do Not Rehire | 6 months with Account Mgr + HR review |
| Policy - Drug Free Workplace | Failed/refused drug test | Do Not Rehire | 1 year with Campus VP + HR Manager review |
| Policy - Harassment | Anti-discrimination policy violation | Do Not Rehire | No Exceptions |
| Policy - Misc. | Other policy violations | Do Not Rehire | 1 year with Campus VP + HR Director review |
| Policy - Safety | Safety policy violation | Do Not Rehire | 1 year with Campus VP + HR Manager review |
| Policy - Workplace Violence | Workplace violence policy violation | Do Not Rehire | No Exceptions |
| Reduction in Work Force | Account close, loss of business | Rehire | - |
| Temporary Job Ended | End of peak/seasonal assignment | Rehire | - |
| Theft | Theft | Do Not Rehire | No Exceptions |

**Key Business Rules (Global):**
- Exit interviews mandatory for resigning white collars only
- All dismissals (performance, policy violation, restructure) must be discussed and coordinated by HR
- HR notification required as soon as resignation/retirement notification received
- Transition plan required: responsibilities and knowledge transfer
- Update G-Talent+ within 5 days of departure
- Prepare all documents required by local employment law
- Major disciplinary infractions escalate to higher HR level

**Key Business Rules (US Zendesk):**
- ESN must be submitted on employee's last day
- All ESNs submitted to HRDM for processing within 24 hours
- Involuntary terminations require signed Employee Warning Notice (Termination Corrective)
- Network access offboarding ticket number required on ESN
- California and Washington ESNs come from Local HR (not Supervisor)
- NAT GTS Operations employees: signed NSA must be sent with separation docs
- Zendesk ticket for terminations marked Urgent priority
- Job Abandonment: defined as 2 consecutive NC/NS days
- State separation notices required for specific states
- Benefit FAQs sent to all terminating employees
- Exit survey (Survey Monkey) sent to exempt employees only

---

### 9. Payroll & Administration

**Oracle HCM Module:** Payroll (if applicable), Global HR

| Process | Region | Source Documents | Oracle Equivalent |
|---------|--------|------------------|-------------------|
| Payroll Processing | Global | Step 7 Mermaid | Payroll Processing |
| Administration | Global | Administration & Payroll.pdf | HR Administration |

**Workflow Summary (from HR Blueprint 4.12-4.14):**

| Sub-Process | Key Rules | Tools |
|-------------|-----------|-------|
| 4.12 Pay Cycle Processing | One payroll cycle per country; Local HR approval required | Payroll System |
| 4.13 Manage Payroll Cycle | Statutory deductions, tax, social contributions | Payroll System |
| 4.14 Off-Cycle Pay Processing | Bonus, retroactive corrections | Payroll System |

**Key Business Rules:**
- One payroll cycle per country
- Local payroll team follows local regulations
- Payroll audit every 2 years
- NO CASH payments allowed
- Data collection: Employee master data, time & attendance, absences, compensation changes
- Local HR approval required before payment processing
- Statutory reporting: Tax authority, social insurance
- Post to General Ledger after payment

---

## Workflow Synthesis Template

### Template for Each Process

```markdown
#### [Process Name]

**Source:** [Document name and path]
**Region:** [Global / US / EU / etc.]
**Current System:** [G-Talent+ / Manual / Other]

**Process Overview:**
[Brief description]

**Key Steps:**
1. [Step 1]
2. [Step 2]
3. [Step 3]
...

**Actors/Roles:**
- [Role 1]: [Responsibilities]
- [Role 2]: [Responsibilities]

**Triggers:**
- [What initiates this process]

**Outputs:**
- [What the process produces]

**Oracle HCM Mapping:**
- **Module:** [Oracle module]
- **Objects:** [Oracle objects used]
- **Actions:** [Oracle actions]
- **Approval:** [Approval workflow needed]

**Gap Analysis:**
- [Any gaps between current and Oracle]

**Notes:**
- [Additional observations]
```

---

## Next Steps

1. [x] Review HR Blueprint PDF documents and extract process flows - **COMPLETE**
2. [x] Analyze Mermaid diagrams from Blueprint Modelization - **COMPLETE**
3. [x] Review US Zendesk processes for regional requirements - **COMPLETE** (24 documents, 12 processes)
4. [x] Review Talentsoft guides for G-Talent+ current state - **COMPLETE** (44 files extracted, 20+ guides)
5. [x] Map each process to Oracle HCM Cloud equivalents - **COMPLETE** (See 21_GTalent_to_Oracle_HCM_Mapping.md)
6. [x] Identify approval workflows needed - **COMPLETE** (See 22_Oracle_HCM_Approval_Workflows.md)
7. [x] Document gaps and transformation requirements - **COMPLETE** (See 23_GEODIS_HCM_Gap_Register.md - 50 gaps identified)
8. [x] Create configuration specifications - **COMPLETE** (See 24_Oracle_HCM_Configuration_Specifications.md)
9. [ ] Review remaining Discovery folders (01-Business Req, 02-Integration, 04-Business Processes, 06-Financial)
10. [ ] Validate all documents with GEODIS HR stakeholders
11. [ ] Assign gap owners and target dates
12. [ ] Finalize configuration decisions per module

---

## Talentsoft (G-Talent+) Key Findings Summary

### G-Talent+ System Overview

G-Talent+ is the current global HRIS system (powered by Talentsoft) used by GEODIS. It provides integrated modules for Core HR, Recruitment, Performance Management, and Campaign Management.

### Core HR Module

**Employee Profile Sections:**

| Section | Content | Oracle Mapping |
|---------|---------|----------------|
| Civil Registration | Name, DOB, nationality, gender | Person |
| Contracts | Contract type, dates, terms | Assignment |
| Situations | Position, organization, manager | Assignment |
| FTE | Full-time equivalent calculation | Assignment |
| Identity Documents | Passport, ID cards, work permits | Person Documents |
| Bank Details | Payment information | Payment Methods |
| Address | Home address, contact details | Person Address |
| Emergency Contacts | Emergency contact information | Person Contacts |

**Employee Lifecycle Actions:**

| Action | Description | G-Talent+ Process |
|--------|-------------|-------------------|
| Creation | New employee record | From recruitment or blank form |
| Mutation | Transfer, promotion, organizational change | Mutation form with approval |
| Termination | End of employment | Termination workflow |
| Secondment | Temporary assignment | Secondment module |
| Expatriation | International assignment | IM Coordinator process |

**Data Quality Dashboards:**
- Employee data completeness tracking
- Missing mandatory fields alerts
- Data quality KPI monitoring

### Recruitment Module

**Vacancy Request Workflow:**

| Step | Actor | Action | SLA |
|------|-------|--------|-----|
| 1 | Manager | Create vacancy request | - |
| 2 | Approver (N+1/HR) | Approve or reject request | - |
| 3 | Recruiter | Review approved request | - |
| 4 | Recruiter | Create vacancy from request | - |
| 5 | System | Auto-populate vacancy fields | - |

**Vacancy Publication Rules:**

| Publication Type | Platform | Rule |
|-----------------|----------|------|
| Internal | G-Talent+ Career Site | Minimum 1 week before external |
| External | Broadbean Integration | LinkedIn, Indeed, Monster, etc. |
| Speculative | Talent Pool | Managed via speculative module |

**Broadbean Integration:**
- Multi-posting to external job boards
- Supported platforms: LinkedIn, Indeed, Monster, Glassdoor, regional boards
- Application tracking from external sources
- Automated candidate import

**Candidate Selection Workflow:**

| Stage | Status | Action |
|-------|--------|--------|
| New | Application received | Initial screening |
| Shortlisted | Meets criteria | Interview scheduling |
| Interview | In process | Conduct interviews |
| Offer | Selected candidate | Generate offer |
| Hired | Accepted offer | Convert to employee |
| Rejected | Not selected | Send rejection notification |

**Speculative Applications:**
- Dedicated module for unsolicited applications
- Talent pool management
- Automatic matching to future vacancies
- GDPR-compliant retention policies

### Performance Management Module

**Performance Rating Scale:**

| Rating | Label | Description |
|--------|-------|-------------|
| <50% | Significantly Below | Does not meet expectations |
| 50-80% | Below | Partially meets expectations |
| 80-100% | Meets | Meets expectations |
| 100-120% | Exceeds | Exceeds expectations |
| >120% | Far Exceeds | Significantly exceeds expectations |

**Performance Appraisal Form Sections:**

| Section | Content | Completed By |
|---------|---------|--------------|
| Objectives Review | Previous year objectives assessment | Manager |
| Skills Assessment | Competency evaluation | Manager + Employee |
| Values Assessment | GEODIS values alignment | Manager |
| Development Plan | Training and development needs | Manager + Employee |
| Career Aspirations | Geographical mobility, career goals | Employee |
| Next Year Objectives | SMART objectives for next period | Manager |

**Campaign Management:**

| Campaign Type | Description | Process |
|--------------|-------------|---------|
| Type 3 | Employee + Manager completion | Most common |
| Type 2 | Manager only | Simplified |
| Type 1 | Employee only | Self-assessment |

**Campaign Workflow:**

| Phase | Actor | Action |
|-------|-------|--------|
| Setup | HR Admin | Define population, dates, form |
| Launch | System | Notify participants |
| Employee | Employee | Complete self-assessment |
| Manager | Manager | Complete evaluation |
| Validation | Manager | Sign-off meeting with employee |
| Close | HR Admin | Close campaign, generate reports |

**Mid-Year Review:**
- Created from performance form at any time
- Optional but recommended
- Tracks objective progress
- Can update development plan

### Salary Review Module

**Salary Review Process:**

| Step | Actor | Action |
|------|-------|--------|
| 1 | HR Admin | Configure review parameters |
| 2 | HR Admin | Define eligible population |
| 3 | Manager | Propose salary adjustments |
| 4 | N+1 | Review and validate proposals |
| 5 | HR | Final approval |
| 6 | System | Generate letters and update contracts |

**Review Parameters:**
- Budget envelope by organization
- Increase guidelines (min/max percentages)
- Retroactive date
- Eligibility criteria (tenure, performance)

### Exit Interview Module

**Exit Interview Requirements:**

| Employee Type | Exit Interview | Mandatory |
|--------------|----------------|-----------|
| Managers | Required | Yes |
| White Collar | Recommended | Per HR Blueprint |
| Blue Collar | Optional | No |

**Exit Interview Topics:**
- Reason for leaving
- Job satisfaction factors
- Management feedback
- Recommendations for improvement
- Would recommend GEODIS as employer

### Assigned Employees Module

**Assignment Types:**

| Type | Description | Duration |
|------|-------------|----------|
| Secondment | Temporary assignment to another entity | Fixed term |
| Expatriation | International long-term assignment | Multi-year |
| Delegation | Temporary management responsibility | Project-based |

### HR KPIs Manual

**Key Indicator Categories:**

| Category | Indicators | Count |
|----------|-----------|-------|
| Workforce | FTE, Headcount, Gender split | 15+ |
| Turnover | Voluntary, Involuntary, Total | 10+ |
| Absenteeism | Rate, Days lost, Causes | 12+ |
| Accidents | Frequency rate, Severity rate | 8+ |
| Training | Hours per employee, Completion rate | 10+ |
| Recruitment | Time to fill, Cost per hire | 8+ |
| Performance | Appraisal completion, Rating distribution | 6+ |

**FTE Calculation:**
- Period-end FTE: Active employees at end of period
- Average FTE: (Opening + Closing) / 2
- Full-time = 1.0 FTE
- Part-time = Actual hours / Standard hours

**Turnover Rate Formula:**
```
Turnover Rate = (Leavers in Period / Average Headcount) × 100
```

**Frequency Rate (Accidents):**
```
Frequency Rate = (Number of Accidents × 1,000,000) / Hours Worked
```

**Severity Rate (Accidents):**
```
Severity Rate = (Days Lost × 1,000) / Hours Worked
```

### G-Talent+ to Oracle HCM Mapping Summary

| G-Talent+ Module | Oracle HCM Module | Key Differences |
|------------------|-------------------|-----------------|
| Core HR | Core HR | Similar functionality |
| Recruitment | Recruiting | Requisition-based vs Request-based |
| Performance | Performance Management | Campaign vs Document approach |
| Salary Review | Workforce Compensation | Similar budget-based approach |
| People Review | Talent Review | Comparable succession features |
| Exit Interview | Journeys (Exit) | Journey-based offboarding |
| Campaigns | Performance Templates | Configuration approach differs |
| KPIs | OTBI/Analytics | Reporting methodology change |

### Key Integration Points for Oracle HCM Migration

| Current Integration | Description | Oracle Consideration |
|--------------------|-------------|---------------------|
| Broadbean | Job board multi-posting | Oracle Recruiting integration |
| Minerve+ | Financial system | HCM-Finance integration |
| G-Campus | Onboarding training | Oracle Learning integration |
| G-Learning | E-Learning platform | Oracle Learning Cloud |
| Local Payroll | Country-specific payroll | Payroll integration strategy |

### Data Migration Considerations

| Data Category | Volume Estimate | Complexity |
|--------------|-----------------|------------|
| Employee Records | All active + termed | High |
| Position History | Assignment history | High |
| Performance Data | 2-3 years history | Medium |
| Recruitment Data | Open requisitions only | Low |
| Training Records | Completion history | Medium |

---

## Zendesk US Processes Key Findings Summary

### US HR Service Center (HRSC) Model

The US operates a centralized HR Service Center model using Zendesk for ticket management. All HR administrative requests are routed through HRServiceCenter@geodis.com.

### Critical SLAs

| Process | SLA | Priority |
|---------|-----|----------|
| Terminations (Vol/Invol) | 24 hours | Urgent |
| Onboarding/Background Check | Same day action | Urgent |
| Job Abandonment | Same day action | Priority |
| Medical LOA/ADA | 24 hours | High |
| EAF Processing | By Friday 12:30 PM CST for next pay | Normal |
| Employment Verification | 48 hours | Normal |
| I-9 Reverification | Before document expiration | Monthly monitoring |

### Key US-Specific Forms

| Form | Purpose | System |
|------|---------|--------|
| ESN (Employee Separation Notice) | All terminations | UKG |
| EAF (Employee Action Form) | Employment changes (job, pay, status) | UKG |
| Notice of Resignation | Voluntary termination documentation | Paper/Email |
| Employee Warning Notice | Corrective/Disciplinary action | UKG |
| Request for Leave of Absence | PLOA/MLOA initiation | Paper |
| ADA Medical Certification | Accommodation request | Paper |
| GCF Payroll Deduction Authorization | Compassion Fund donations | UKG |

### Ticket Lifecycle

1. Email received at HRServiceCenter@geodis.com
2. Zendesk auto-assigns ticket with priority
3. HRSC Coordinator processes request
4. Documents uploaded to UKG personnel file
5. Ticket set to "Solved" (4-day reopen window)
6. Auto-transitions to "Closed" after 4 days

### Key Integration Points for Oracle HCM

| Current System | Integration Type | Oracle Consideration |
|----------------|-----------------|---------------------|
| Sterling | Background Check | Pre-hire checklist/integration |
| E-Verify | Work Eligibility | I-9 integration |
| VOYA | FMLA/Disability | Absence Management integration |
| Work Number | Employment Verification | Verification configuration |
| Zendesk | Ticketing | HR Help Desk replacement |
| Service Now | IT Offboarding | Workflow integration |

### Attendance Point System (US)

| Threshold | Consequence |
|-----------|-------------|
| 6 points in 90 days | Termination eligible |
| 15 points in 12 rolling months | Termination eligible |

---

## HR Blueprint Key Findings Summary

### Annual HR Calendar

| Period | Process | Module |
|--------|---------|--------|
| January-April | Performance Appraisal | Performance Management |
| April | Annual Salary Review | Compensation |
| May-October | People Review & Succession | Talent Management |
| Year-round | Recruitment, Learning, Administration | Various |

### Critical Approval Thresholds

| Threshold | Approval Required | Process |
|-----------|-------------------|---------|
| €125,000 base salary | EVP HR | Recruitment, Compensation |
| €155,000 total package | CnB Director notification | Recruitment |
| TOPEX positions | CHRO/CHO | Recruitment, Compensation, Succession |
| All promotions | HR + Manager | Talent Management |
| All dismissals | HR coordination | Offboarding |
| All disciplinary actions | HR validation | Social & Legal |

### Key Systems (Current State)

**Global Systems:**

| System | Function | Oracle HCM Equivalent |
|--------|----------|----------------------|
| G-Talent+ | Core HR, Performance, Recruitment | Core HR, Recruiting, Performance |
| G-Campus | Onboarding Training | Onboarding, Journeys |
| G-Learning | E-Learning Platform | Learning |
| GEODIS University | Leadership Programs | Learning |
| Coupa | Equipment Ordering | Procurement Integration |

**US-Specific Systems (from Zendesk):**

| System | Function | Oracle HCM Equivalent |
|--------|----------|----------------------|
| UKG (Insight) | HRIS - Employee records, Disciplinary tracking | Core HR |
| Zendesk | HR Service Center ticketing platform | HR Help Desk |
| Sterling | Background check provider | Pre-hire checklist integration |
| VOYA | FMLA/Disability claims management | Absence Management |
| Recruiting Gateway | Candidate disposition and hiring | Recruiting |
| Onboarding Gateway | New hire document completion, I-9 | Onboarding |
| Work Number | Employment verification (primary) | Employment Verification |
| E-Verify | Employment eligibility verification | Work Eligibility |
| Service Now | IT offboarding tickets | IT Integration |
| Survey Monkey | Exit surveys (exempt employees) | Exit Survey |

**Zendesk Ticket Priority Levels:**

| Priority | Process Types | SLA |
|----------|--------------|-----|
| Urgent | Onboarding, Terminations | Same day / 24 hours |
| High | Medical LOA, ADA requests | 24 hours |
| Priority | Job Abandonment, PLOA | Same day action |
| Normal | EAF, Employment Verification, Corrective Action | 48 hours |

**Zendesk Email Routing:**

| Email Address | Purpose |
|--------------|---------|
| HRServiceCenter@geodis.com | All US HR Service Center requests |
| GEODISInsight.cl.us@geodis.com | Payroll deduction submissions |

### Employee Population Rules

| Population | Special Rules |
|------------|---------------|
| Blue Collar | May not have email; In-person trainings from TMS |
| White Collar | Exit interviews mandatory; Reference checks required |
| TOPEX | CHRO/CHO approvals; LTIP eligible; Special recruitment process |
| High Potential | People Review tracking; Development plans |

### Compliance Requirements

- GDPR mandatory even outside EU
- Local laws always prevail
- Payroll audit every 2 years
- No cash payments
- Quarterly litigation reporting

---

## Related Documentation

### Implementation Documents Created

| Document | Purpose | Status |
|----------|---------|--------|
| 05_Implementation_Methodology.md | Oracle HCM implementation phases | Draft |
| 06_Repository_Configuration_Guide.md | Repository configuration details | Draft |
| 08_Oracle_Documentation_Index.md | Oracle documentation references | Draft |
| **21_GTalent_to_Oracle_HCM_Mapping.md** | G-Talent+ to Oracle HCM mapping | Draft |
| **22_Oracle_HCM_Approval_Workflows.md** | Approval workflow specifications | Draft |
| **23_GEODIS_HCM_Gap_Register.md** | Gap register (50 gaps identified) | Draft |
| **24_Oracle_HCM_Configuration_Specifications.md** | Oracle HCM configuration specs | Draft |

### Oracle Documentation Source

| Location | Content |
|----------|---------|
| `01 - Discovery/05 - Oracle Documentation/` | 41 Oracle HCM PDF guides |
| `oracle_hcm_docs_extracted.txt` | Extracted text (1.3M lines) |
| https://docs.oracle.com/en/cloud/saas/human-resources/index.html | Oracle HCM Cloud online docs (v25B) |

### Process & Security Configuration Sheets

| File | Path | Records | Content |
|------|------|---------|---------|
| **Approval Workflows.xlsx** | `04 - SHEETS/Process and Security/` | 31 | BPM workflow definitions with approver chains |
| **Action.xlsx** | `04 - SHEETS/Process and Security/` | 42 | HR action types with journey triggers |
| **Action & Reasons.xlsx** | `04 - SHEETS/Process and Security/` | 70 | Action reason codes (incl. US termination reasons) |

### Source Document Extraction Scripts

| Script | Location | Output |
|--------|----------|--------|
| extract_office_content.py | `07 - Zendesk Business Processes/` | zendesk_processes_extracted.txt |
| extract_talentsoft_content.py | `08 - Talentsoft Guidelines/` | talentsoft_guides_extracted.txt |
| extract_oracle_docs.py | `05 - Oracle Documentation/` | oracle_hcm_docs_extracted.txt |
| populate_sheets.py | `04 - SHEETS/Process and Security/` | Populates Action, Reason, Workflow sheets |

---

## Document Control

**File Path:** `02 - Define/01 - Repositories/00 - Documentation/20_GEODIS_HR_Workflows_Catalog.md`

| Attribute | Value |
|-----------|-------|
| Created | 2025-12-06 |
| Author | HCM Implementation Agent |
| Classification | Internal |
| Review Cycle | As needed during synthesis |

---

*This is a living document. Update the progress checklists and revision history as each source document is reviewed and synthesized.*
