# GEODIS Workshop 1 - Job Requisitions: Ultra-Holistic Analysis

---

## Fit-to-Standard Update (2025-12-08)

The DFF configuration has been revised to maximize use of Oracle standard fields:

**Removed from DFF:**
- TOPEX Position -> Use `RECRUITING_TYPE = 'Executive'`
- Line of Business -> Use Division hierarchy via Department
- Salary fields -> Use standard IRC_REQUISITIONS_B columns

**Final DFF (7 segments):**
1. FTE Percentage
2. Budgeted Position
3. Budget Justification
4. Incumbent Name
5. Incumbent Last Day
6. Hiring Priority
7. Impact to Staffing

---



**Project:** GEODIS New HCM - AMARIS
**Module:** Oracle Recruiting Cloud (ORC)
**Workshop:** 1 - Job Requisitions
**Date:** December 10th, 2025
**Integrator:** HR Path
**Status:** Pre-Workshop - All Deliverables "Awaiting Workshop"

---

## Executive Summary

This document provides a comprehensive analysis cross-referencing:
1. **HR Path Workshop 1 Presentation** (36 slides)
2. **GEODIS Job Requisitions Requirement File** (13 tabs, V0)
3. **Existing GEODIS Recruiting Documentation** (from Define phase)

### Key Metrics

| Metric | Value |
|--------|-------|
| **Requirement File Tabs** | 13 |
| **Job Requisition Steps** | 17 (15 in creation wizard + formatting + posting) |
| **Standard Fields Available** | 100+ |
| **Languages Required** | 15 (EN + 14 translations) |
| **List of Values Categories** | 12 |
| **Deliverable Status** | All "Awaiting Workshop" |

---

## Part 1: Requirement File Structure & Deliverables

### 1.1 Summary Tab - Deliverables Checklist

| # | Area | Subject | Description | Status | Priority |
|---|------|---------|-------------|--------|----------|
| 1 | Job Requisitions | **Primary Locations** | Location repository for recruitment | Awaiting Workshop | HIGH |
| 2 | | **Job Requisitions Fields** | Field configuration per step | Awaiting Workshop | HIGH |
| 3 | | **Job Requisitions - Lists** | List of values for dropdowns | Awaiting Workshop | HIGH |
| 4 | | **Job Requisitions - DFF** | Custom flexfields | Awaiting Workshop | MEDIUM |
| 5 | | **Job Requisition Approvals** | Approval workflow rules | Awaiting Workshop | HIGH |
| 6 | | **Job Requisition Template** | Pre-configured templates | Awaiting Workshop | MEDIUM |
| 7 | | **Posting Description Templates** | Job description templates | Awaiting Workshop | MEDIUM |
| 8 | | **Formatting Job** | Employer/Org descriptions | Awaiting Workshop | LOW |
| 9 | | **Posting Jobs** | External posting (Agents/Jobboards) | Awaiting Workshop | HIGH |
| 10 | | **Prescreening Questions** | Screening & disqualification Q's | Awaiting Workshop | HIGH |
| 11 | | **Interview Feedback Questionnaires** | Interviewer feedback forms | Awaiting Workshop | MEDIUM |

### 1.2 Tab-by-Tab Analysis

#### Tab 1: Primary Locations (41 rows)
**Purpose:** Define geography structure for job search and candidate search

| Configuration | Options | GEODIS Decision Needed |
|---------------|---------|------------------------|
| **Level 1** | Country (mandatory) | All GEODIS countries |
| **Level 2** | State / County / Postal Code / City | TBD |
| **Level 3** | State / County / Postal Code / City | TBD |

**Cross-Reference with Existing GEODIS Data:**
- Core HR Location.xlsx: 919 locations
- Countries in scope: USA, Canada, Netherlands (Wave 1)

**Workshop Question:** What geography levels should be searchable for each country?

---

#### Tab 2: Job Requisition Fields (154 rows)
**Purpose:** Configure field visibility and requirements per step

**Structure by Step:**

| Step | Name | Field Count | Mandatory | Key Fields |
|------|------|-------------|-----------|------------|
| 1 | How | 12 | Yes | Requisition Type, Template, Location, Organization |
| 2 | Basic Info | 8 | Yes | Title, # Openings, Languages, Business Justification |
| 3 | Hiring Team | 3 | Yes | Hiring Manager, Recruiter, Collaborators |
| 4 | Requisition Structure | 6 | Yes | Recruiting Type, Organization, Job Family, Location |
| 5 | Details | 20 | No | Salary, Worker Type, Education Level, Job Type |
| 6 | Work Requirements | 10 | No | Travel, Workdays, Hours, Relocation |
| 7 | Posting Description | 17 | No | Short/Long Description, Internal/External |
| 8 | Skills | 7 | No | Skill, Importance, Level, Experience |
| 9 | Licenses & Certifications | 7 | No | License, Country, State, Required |
| 10 | Offer Info | 8 | No | Legal Employer, BU, Department, Grade, Location |
| 11 | Estimated Time to Hire | 1 | No | AI-based prediction |
| 12 | Attachments | 1 | No | Files/URLs |
| 13 | Configuration | 8 | Yes | CSP, Application Flow, Auto-post settings |
| 14 | Questionnaires | 3 | No | External/Internal Prescreening |
| 15 | Interview Questionnaires | 1 | No | Feedback questionnaires |
| 16 | Screening Services | 3 | Conditional | Assessments, Background Check, Tax Credits |
| 17 | Tax Credits | 3 | Conditional | CSP, Location Package, User Account |

**Two View Configurations:**
- **Hiring Manager View** - Limited fields
- **Recruiter View** - Full access

**Field Types:**
- Core HR Repository (Job, Location, Department, Grade, etc.)
- List of Values (Recruiting Type, Job Shift, etc.)
- System (auto-populated)
- Optional (user input)

---

#### Tab 3: Job Req. List of Values (136 rows)
**Purpose:** Define dropdown values for requisition fields

| Category | Field | Seeded Values | Custom Slots | Source |
|----------|-------|---------------|--------------|--------|
| **How** | Recruiting Type | 6 (Executive, Campus, Contingent, Professional, Hourly, Agency Contingent) | 3 | ORC Lookup |
| **Basic Info** | Business Justification | 4 (Extension, Modification, New Position, Replacement) | 1+ | ORC Lookup |
| **Hiring Team** | Collaborator Type | 1 (Collaborator) | 2+ | ORC Lookup |
| **Details** | Job Shift | 4 (Day, Evening, Night, On Call) | 1+ | ORC Lookup |
| **Details** | Job Type | 9 (Co-op, Internship, Standard, Summer, etc.) | 1+ | ORC Lookup |
| **Details** | Salary Period | 6 (Per Hour/Day/Week/Month/Year) | 1+ | ORC Lookup |
| **Details** | Worker Type | 2 (Employee, Contingent Worker) | - | Core HR |
| **Details** | Education Level | 25 levels | - | Core HR |
| **Details** | Pay Frequency | 6 (Daily to Yearly) | - | Core HR |
| **Details** | Management Level | 10 levels | - | Core HR |
| **Work Req** | Travel Frequency | 4 (0.25, 0.5, 0.75, 1) | - | ORC Lookup |
| **Work Req** | Work Hours | 3 templates | - | Core HR |
| **Work Req** | Work Days | 3 templates | - | Core HR |
| **Skills** | Importance | 6 levels (None to Very Important) | - | Core HR |

**Translation Requirements:** 15 languages
- EN (base) + FR, pt_BR, CZ, DK, NL, FI, DE, IT, NO, PL, ES, SE, TR

---

#### Tab 4: Job Req. DFF (5 rows)
**Purpose:** Custom Flexfields for additional GEODIS-specific data

| Column | Purpose |
|--------|---------|
| Name EN | Field label in English |
| Translated +FR...+TR | 14 language translations |
| Field Type | Text, Number, Date, LOV |
| List of Values Labels | If LOV, define options |
| Required | Y/N |

**Cross-Reference with Existing Analysis:**
- Current DFF count target: 4 (from v2.0 Fit-to-Standard)
- Previous v1.0 had 12 DFFs (67% reduction achieved)

**Recommended GEODIS DFFs:**
1. **Incumbent Name** (from UKG gap analysis)
2. **Is Budgeted** (Y/N)
3. **FTE %** (percentage)
4. **PERM Required** (Y/N for US immigration compliance)

---

#### Tab 5: Job Requisition Approvals (131 rows)
**Purpose:** Configure approval workflow rules

| Config | Options | GEODIS Decision |
|--------|---------|-----------------|
| **Activate Approval** | Y/N | TBD |
| **Criteria** | Fields used to route approvals | TBD |
| **Approver 1-4** | Role or specific person | TBD |

**Cross-Reference with Existing GEODIS Rules:**
- Offer approval thresholds: <EUR 125K (1 level), EUR 125-155K (2 levels), >EUR 155K (3 levels)
- Should similar thresholds apply to requisition approval?

**Workshop Questions:**
1. Should requisition approval be active?
2. What criteria determine routing (Location? Salary? Grade? BU?)?
3. How many approval levels?

---

#### Tab 6: Job Req. Template (103 rows)
**Purpose:** Pre-configured requisition templates

**Template Structure (3 templates available):**

| Section | Fields |
|---------|--------|
| **Base** | Job / Position / Standalone |
| **Basic Info** | Recruiting Type, BU, Code, Name, Title, Languages |
| **Hiring Team** | Manager, Recruiter, Collaborators |
| **Posting Structure** | Organization, Locations, Job Family/Function |
| **Offer Info** | Department, Work Location, Workplace (On-site/Hybrid/Remote), Grade, Legal Employer |
| **Budget** | Currency, Referral Bonus, Sourcing/Travel/Relocation Budget |
| **Compensation** | Currency, Min/Max Salary, Pay Frequency |
| **Job Requisition DFF** | Custom fields |
| **Job Profile** | Travel, Duration, Work Days |
| **Additional Details** | Worker Type, Regular/Temp, Management Level, FT/PT, Shift, Job Type, Education |

**Cross-Reference with Existing GEODIS Templates:**
- Requisition Template.xlsx: 5 templates configured
- Template types: Professional, Executive, Hourly, Campus, Contingent

---

#### Tab 7: Posting Description Templates (76 rows)
**Purpose:** Reusable job description templates

| Component | Languages | Notes |
|-----------|-----------|-------|
| **Template Name** | 15 | Identifier |
| **Short Description** | 15 | Career site search results |
| **Description** | 15 | Full job details |
| **Responsibilities** | 15 | Job duties |
| **Qualifications** | 15 | Requirements |

**LinkedIn Integration Note:** Use only "Description" box for LinkedIn automatic posting

**AI Assist Feature:** Available in ORC to generate descriptions (requires 100+ character input)

---

#### Tab 8: Formatting (15 rows)
**Purpose:** Employer and organization branding

| Element | Translations | Use |
|---------|--------------|-----|
| **Employer Description** | 15 | Company overview on career site |
| **Recruiting Organization Description** | 15 | Department/team description |

**Supports:** 3 different organization descriptions per Legal Entity or BU

---

#### Tab 9: Posting (21 rows)
**Purpose:** External posting channels

**Staffing Agents Configuration:**

| Field | Description |
|-------|-------------|
| Agency Name | Staffing agency name |
| Referral Type | Type of referral |
| Main Contact | Primary contact person |
| Contract Type | Agreement type |
| Agency Email | Contact email |
| Exclusivity Length | Exclusive period |
| Create Job Application | Can agent create applications? |
| Note or Address | Additional info |

**Jobboards Integration:**

| Provider | Integration Method |
|----------|-------------------|
| **eQuest** | ZIP File + Reference Key |
| **Broadbean** | ZIP File + Reference Key |

**Cross-Reference with GEODIS Decision:**
- Pending: Broadbean vs Oracle native integration
- Indeed, LinkedIn RSC already planned

---

#### Tab 10: Prescreening Questions (2 rows - template)
**Purpose:** Candidate screening questions

| Column | Purpose |
|--------|---------|
| Disqualification or Prescreening? | Question type |
| Contextualization | BU, Location, Job Family, Function, Internal/External |
| Question Name | 15 language translations |
| Response Type | Free text / Single Choice / Multiple Choice |
| Score Question | Y/N |
| Response Names | Answer options |
| Rejects Application | Y/N (for disqualification) |
| Score Points | Point value |

**Question Types:**
1. **Prescreening** - Informational scoring
2. **Disqualification** - Auto-reject based on answer

---

#### Tab 11: Interview Feedback Questionnaire (2 rows - template)
**Purpose:** Post-interview feedback collection

| Column | Purpose |
|--------|---------|
| Questionnaire Name | Identifier |
| Question Name | 15 translations |
| Response Type | Free text / Single Choice / Multiple Choice |
| Score Question | Y/N |
| Response Names | Answer options |
| Score Points | Point value |

---

#### Tab 12: Interview Templates (Empty)
**Purpose:** Interview schedule templates (not yet configured)

---

## Part 2: Workshop Presentation Analysis

### 2.1 Workshop Series Context

| Workshop | Topic | Dependency |
|----------|-------|------------|
| **1** | **Job Requisitions** | Foundation |
| 2 | Candidate Experience | Depends on 1 |
| 3 | Candidate Selection Process | Depends on 1 |
| 4 | Candidate Management | Depends on 1, 2, 3 |
| 5 | Onboarding | Depends on 4 |
| 6 | Alerts & Notifications | Cross-cutting |
| 7 | Security & Data Management | Cross-cutting |

### 2.2 Key Presentation Topics Mapped to Deliverables

| Presentation Topic | Requirement File Tab | Status |
|--------------------|---------------------|--------|
| Primary Location Structure (Slide 13) | Primary Locations | Awaiting |
| Job Requisition Fields (Slides 12-29) | Job Requisition Fields | Awaiting |
| List of Values (Slides 12-18) | JOB REQ. LIST OF VALUES | Awaiting |
| Custom Flexfields (Slide 17) | JOB REQ. DFF | Awaiting |
| Approval Process (Slide 30) | Job Requisition Approvals | Awaiting |
| Job Requisition Templates (Slide 12) | JOB REQ. TEMPLATE | Awaiting |
| Posting Description (Slides 19-20) | Posting Desc Templates | Awaiting |
| Job Formatting (Slide 31) | FORMATTING | Awaiting |
| Job Posting (Slide 32) | POSTING | Awaiting |
| Prescreening Questions (Slide 28) | Prescreening Questions | Awaiting |
| Interview Questionnaires (Slide 29) | Itw Feedback Questionnaire | Awaiting |

### 2.3 Three Requisition Creation Scenarios

| Scenario | Process Owner | Use Case |
|----------|---------------|----------|
| **Recruiter Process** | Recruiter | Centralized recruitment |
| **Hiring Manager Process** | Manager | Direct hire by manager |
| **Shared Process** | Manager + Recruiter | Collaborative (HM initiates, Recruiter completes) |

**GEODIS Decision Needed:** Which scenario(s) to enable?

---

## Part 3: Cross-Reference with Existing GEODIS Configuration

### 3.1 Existing Repository Sheets (03 - ORACLE/)

| Existing Repository | Records | Relevant to Workshop 1 |
|--------------------|---------|------------------------|
| Requisition Template.xlsx | 5 | Yes - Validate |
| Requisition Phase.xlsx | 8 | Yes - Reference |
| Candidate Phase.xlsx | 12 | Workshop 3 |
| Candidate State.xlsx | 43 | Workshop 3 |
| Candidate Source.xlsx | 17 | Workshop 2 |
| Candidate Pool Type.xlsx | 7 | Workshop 2 |
| Offer Letter Template.xlsx | 18 | Workshop 4 |
| Interview Guide.xlsx | 10 | Workshop 3 |
| Interview Type.xlsx | 9 | Workshop 3 |
| Posting Channel.xlsx | 8 | Yes - Reference |
| Rejection Reason.xlsx | 15 | Workshop 3 |
| Withdrawal Reason.xlsx | 8 | Workshop 3 |
| Recruiting Action.xlsx | 25 | Cross-workshop |
| Recruiting Approval Workflow.xlsx | 6 | Yes - Validate |

### 3.2 Alignment Check: Existing vs. Requirement File

| Area | Existing Config | Requirement File | Gap |
|------|-----------------|------------------|-----|
| **Requisition Templates** | 5 templates | 3 template slots | Need to confirm which 3 to use |
| **Approval Workflow** | 6 rules configured | 4 approver slots × 3 scenarios | Need to map existing rules |
| **Posting Channels** | 8 channels | Agents + Jobboards | Need to reconcile |
| **Primary Locations** | Uses Core HR (919) | New recruiting-specific structure | Need to define levels |

### 3.3 Alignment with Business Requirements (Doc #11)

| Requirement | Source | Requirement File Coverage |
|-------------|--------|---------------------------|
| 250K+ applications/year | HR Blueprint | Configuration capacity |
| 7-day internal posting rule | Workshop RFP | Configuration step 13 |
| Salary thresholds for approval | Workshop RFP | Approval tab |
| PERM compliance | Immigration Guide | DFF for PERM flag |
| Multi-language support | Global scope | 15 languages in all tabs |

---

## Part 4: Workshop Preparation Checklist

### 4.1 Pre-Workshop Data Collection

| Data Needed | Source | Status |
|-------------|--------|--------|
| Geography structure by country | Core HR / Business | TBD |
| Recruiting types in use | Current ATS (G-Talent+, UKG) | Available |
| Business justification reasons | GEODIS HR Policy | TBD |
| Custom fields needed | Gap analysis | 4 identified |
| Approval matrix | GEODIS HR Policy | Partially known |
| Job description templates | Current templates | TBD |
| Employer branding content | Marketing/HR | TBD |
| Staffing agencies list | Procurement/HR | TBD |
| Screening questions | Current ATS | TBD |

### 4.2 Key Decisions Required During Workshop

| # | Decision | Options | Impact |
|---|----------|---------|--------|
| 1 | **Requisition Creation Scenario** | Recruiter / Manager / Shared | Security roles, process flow |
| 2 | **Primary Location Levels** | Country + 1 or 2 levels | Candidate search, job filtering |
| 3 | **Approval Workflow Activation** | Yes / No | Requisition processing time |
| 4 | **Approval Criteria** | Salary / Grade / Location / BU | Workflow routing |
| 5 | **Custom DFFs** | 0-4 fields | Data capture, reporting |
| 6 | **Templates to Use** | Select from 5 existing | User efficiency |
| 7 | **Jobboard Integration** | Broadbean / eQuest / Both | Posting automation |
| 8 | **AI Assist Activation** | Yes / No | Description generation |
| 9 | **Hot Job Feature** | Yes / No | Career site visibility |
| 10 | **Auto-Open/Post/Fill/Unpost** | Configure each | Automation level |

### 4.3 Workshop Output Expected

| Deliverable | Status After Workshop |
|-------------|----------------------|
| Primary Locations structure | Defined |
| Job Requisition Fields config | HM vs Recruiter views defined |
| List of Values | Enabled/disabled, translations |
| DFF specifications | Fields defined |
| Approval workflow rules | Criteria and approvers defined |
| Templates | 3 templates configured |
| Posting Description Templates | At least 1 template |
| Formatting content | Employer description |
| Posting channels | Agents and jobboards |
| Prescreening questions | Initial set |
| Interview questionnaires | Initial set |

---

## Part 5: Recommendations

### 5.1 Fit-to-Standard Approach

Following the v2.0 field mapping approach (-64% DFFs), recommend:

1. **Minimize Custom Fields**
   - Use standard fields wherever possible
   - Only add DFFs for true GEODIS-specific requirements

2. **Leverage Core HR Repositories**
   - Job, Location, Department, Grade already configured
   - Avoid duplicating data in ORC

3. **Standardize Templates**
   - Create templates by Recruiting Type (Professional, Hourly, Executive)
   - Not by region or BU

### 5.2 Integration Considerations

| Integration | Recommendation | Rationale |
|-------------|----------------|-----------|
| **LinkedIn** | Use native integration | Each location = separate ad |
| **Indeed** | Via Broadbean | Broader reach |
| **Broadbean** | Enable | Multi-board posting |
| **Sterling** | Connect for BGC | Background checks |

### 5.3 Process Automation

| Feature | Recommendation | Rationale |
|---------|----------------|-----------|
| **Auto-Open for Sourcing** | Yes, posted internally | 7-day internal rule |
| **Auto-Fill Requisition** | Yes | Reduce manual work |
| **Auto-Unpost** | Configure with Fast Formula | When filled |
| **AI Assist** | Enable after 6 months | Needs history data |

---

## Part 6: Gap Analysis - Requirement File vs. Current State

### 6.1 Items Ready (From Previous Work)

| Item | Source | Ready Status |
|------|--------|--------------|
| 5 Requisition Templates | Requisition Template.xlsx | Validate content |
| 6 Approval Rules | Recruiting Approval Workflow.xlsx | Map to criteria |
| 8 Posting Channels | Posting Channel.xlsx | Reconcile with Agents |
| Business Requirements | Doc #11 | Reference |
| Process Workflows | Doc #12, #19, #20 | Reference |

### 6.2 Items Requiring Workshop Input

| Item | Gap | Priority |
|------|-----|----------|
| Primary Location Structure | Not defined | HIGH |
| Field Visibility by Role | Not configured | HIGH |
| LOV Translations | Not provided | MEDIUM |
| DFF Specifications | Only identified, not detailed | MEDIUM |
| Approval Criteria | Not mapped | HIGH |
| Posting Description Content | Not created | MEDIUM |
| Employer Branding Text | Not provided | LOW |
| Prescreening Questions | Not defined | HIGH |
| Interview Questionnaires | Not defined | MEDIUM |

---

## Appendix A: Language Codes Reference

| Code | Language | Countries |
|------|----------|-----------|
| EN | English | US, Canada, Netherlands, Global |
| FR | French | France, Canada, Belgium |
| pt_BR | Portuguese (Brazil) | Brazil |
| CZ | Czech | Czech Republic |
| DK | Danish | Denmark |
| NL | Dutch | Netherlands, Belgium |
| FI | Finnish | Finland |
| DE | German | Germany, Austria, Switzerland |
| IT | Italian | Italy |
| NO | Norwegian | Norway |
| PL | Polish | Poland |
| ES | Spanish | Spain, Latin America |
| SE | Swedish | Sweden |
| TR | Turkish | Turkey |

---

## Appendix B: Core HR Repository Dependencies

| ORC Field | Core HR Source | Records |
|-----------|---------------|---------|
| Job | Job.xlsx | 688 |
| Job Family | Job Family.xlsx | 27 |
| Location | Location.xlsx | 919 |
| Department | Department.xlsx | 10,803 |
| Business Unit | Business Unit.xlsx | 2,175 |
| Legal Entity | Legal Entity.xlsx | 364 |
| Grade | Grade.xlsx | 20 |

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-08 | AI Agent | Initial holistic analysis |

---

*This document should be used alongside the Workshop 1 presentation and Requirement File during the December 10th, 2025 session.*
