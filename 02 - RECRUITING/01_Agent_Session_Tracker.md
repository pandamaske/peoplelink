# GEODIS HCM Recruiting Implementation Agent
## Context & Progress Tracker

---

**Last Updated:** 2025-12-07 (Session 2)
**Module:** Talent Acquisition / Recruiting
**Status:** 14 Repository Sheets | 191 Records | 2 ATS Analyzed | Business Requirements Complete

---

## Agent Context & Expertise

### Domain Knowledge

- Oracle Fusion HCM Cloud Recruiting (IRC module)
- Requisition management and approval workflows
- Candidate lifecycle and pipeline management
- Job posting and sourcing strategies
- Offer management and approval
- Integration with Core HR (hire action)
- Career site configuration (Redwood UI)
- Recruiting analytics and reporting
- HDL migration for recruiting objects

### Source Systems Knowledge

| System | Region | Architecture | Key Metrics |
|--------|--------|--------------|-------------|
| **UKG (UltiPro)** | US | Star schema, denormalized | 594 fields |
| **Talentsoft (G-Talent+)** | Global | Normalized + SDD reports | 234 API schemas |

### Current State Expertise

- Talentsoft Recruitment module workflows
- Broadbean job posting integration
- Vacancy Request → Vacancy → Closed lifecycle
- Internal posting 7-day rule
- Speculative applications module
- SDD report structure (6 files, ~170MB)
- WordPlus tag system for document generation

---

## Oracle Recruiting Architecture

### Core Tables (IRC Module)

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ORACLE RECRUITING (IRC)                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────┐     ┌─────────────────┐     ┌──────────────┐  │
│  │  REQUISITION    │────▶│   JOB POSTING   │────▶│  CANDIDATE   │  │
│  │  IRC_REQUISITIONS│    │  IRC_JOB_POSTINGS│    │ IRC_CANDIDATES│  │
│  └────────┬────────┘     └─────────────────┘     └──────┬───────┘  │
│           │                                              │          │
│           │              ┌─────────────────┐            │          │
│           └─────────────▶│  APPLICATION    │◀───────────┘          │
│                          │IRC_JOB_APPLICATIONS                     │
│                          └────────┬────────┘                       │
│                                   │                                │
│           ┌───────────────────────┼───────────────────────┐        │
│           ▼                       ▼                       ▼        │
│  ┌─────────────────┐     ┌─────────────────┐     ┌──────────────┐  │
│  │   INTERVIEW     │     │   ASSESSMENT    │     │    OFFER     │  │
│  │ IRC_INTERVIEWS  │     │  IRC_RATINGS    │     │  IRC_OFFERS  │  │
│  └─────────────────┘     └─────────────────┘     └──────┬───────┘  │
│                                                         │          │
│                                                         ▼          │
│                                                  ┌──────────────┐  │
│                                                  │    HIRE      │  │
│                                                  │ PER_ALL_*    │  │
│                                                  └──────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

### HDL Business Objects

| Object | Purpose |
|--------|---------|
| Requisition | Job requisition data |
| Candidate | Candidate profiles |
| JobApplication | Application records |
| RecruiterAssignment | Recruiter assignments |

---

## UKG to Talentsoft Migration Analysis

### Field Mapping Summary

| Metric | Value | Percentage |
|--------|-------|------------|
| **Total UKG Fields** | 594 | 100% |
| Mapped (Direct) | 454 | 76.4% |
| Mapped (Reference) | 84 | 14.1% |
| System Fields | 22 | 3.7% |
| Must Calculate | 13 | 2.2% |
| Not Available | 13 | 2.2% |
| Custom Fields | 8 | 1.3% |
| **Coverage Rate** | - | **97.8%** |

### Key Gaps Identified

| Gap Category | Fields | Risk | Status |
|--------------|--------|------|--------|
| Incumbent Tracking | 3 | HIGH | ADDRESSED via custom field |
| Manager Title/Suffix | 12 | LOW | Accept loss |
| FTE Granularity | 4 | HIGH | Calculate from applications |
| Days-to-Hire Metrics | 5 | HIGH | Build BI calculations |
| Licenses/Certifications | 3 | MEDIUM | ADDRESSED via custom fields |

### GEODIS Talentsoft Custom Fields (Already Configured)

| UKG Gap | Talentsoft Field | WordPlus Tag |
|---------|------------------|--------------|
| Incumbent Name | Name of person being replaced | [P-RequestMotive_ShortText1] |
| Is Budgeted | Budgeted vacancy request | [P-Planned] |
| FTE % | FTE % | [P-PreliminaryJobDescription_ShortText1] |
| Licenses | Certifications | [A-Diploma_LongText2] |
| Middle Name | Middle name | [A-MiddleName] |

### Converter Outputs

| File | Records | Description |
|------|---------|-------------|
| TS_Import_offer.csv | 33,952 | Vacancy records |
| TS_Import_offeruser.csv | 116,101 | Manager/Recruiter assignments |
| TS_Import_entity.csv | 278 | Company entities |

---

## Repository Population Summary

### Oracle Configuration (03 - ORACLE)

| # | Repository | Records | Description |
|---|------------|--------:|-------------|
| 1 | Requisition Template | 5 | GEODIS requisition templates |
| 2 | Requisition Phase | 8 | Draft → Open → Filled → Closed |
| 3 | Candidate Phase | 12 | New → Screen → Interview → Offer → Hire |
| 4 | Candidate State | 43 | Detailed states within each phase |
| 5 | Candidate Source | 17 | LinkedIn, Indeed, Referral, Career Site |
| 6 | Candidate Pool Type | 7 | Silver Medalists, Talent Community |
| 7 | Offer Letter Template | 18 | By country (FR, US, UK, DE, NL) + job family |
| 8 | Interview Guide | 10 | By job family (General, Technical, Leadership) |
| 9 | Interview Type | 9 | Phone, Video, On-Site, Panel |
| 10 | Posting Channel | 8 | Internal, LinkedIn, Indeed, Broadbean |
| 11 | Rejection Reason | 15 | Candidate rejection codes |
| 12 | Withdrawal Reason | 8 | Candidate withdrawal codes |
| 13 | Recruiting Action | 25 | Requisition, candidate, interview, offer actions |
| 14 | Recruiting Approval Workflow | 6 | Requisition and offer approval rules |

**Total Records:** 191

### Planned Sheets (Future)

| # | Repository | Purpose | Priority |
|---|------------|---------|----------|
| 15 | Questionnaire Template | Pre-screening questions | P2 |
| 16 | Background Check Type | Verification types | P2 |
| 17 | Recruiting Metric | KPI definitions | P3 |
| 18 | Career Site Configuration | Redwood UI settings | P2 |

---

## GEODIS-Specific Configuration

### Requisition Templates

| Template | Country | Job Family | Use Case |
|----------|---------|------------|----------|
| GEODIS_STD | Global | All | Default template |
| GEODIS_EXEC | Global | Executive | TOPEX positions |
| GEODIS_FR | France | All | France-specific fields |
| GEODIS_US | US | All | EEO/OFCCP fields |
| GEODIS_INTERN | Global | All | Internships/trainees |

### Approval Workflows

| Workflow | Object | Approvers | Condition |
|----------|--------|-----------|-----------|
| Standard Requisition | Requisition | N+1 → HRBP | Default |
| High Salary Requisition | Requisition | N+1 → HRBP → EVP HR | Salary >= EUR 125K |
| TOPEX Requisition | Requisition | N+1 → CHRO | TOPEX flag = Y |
| Standard Offer | Offer | Hiring Mgr → HR/Comp | Default |
| High Value Offer | Offer | Hiring Mgr → HR/Comp → EVP HR | Base >= 125K or Total >= 155K |
| TOPEX Offer | Offer | Hiring Mgr → CHRO | TOPEX flag = Y |

### Internal Posting Rule

```
Business Rule: Internal candidates must have 7-day priority
Implementation: Posting schedule configuration
  - Step 1: Internal posting only (Day 1-7)
  - Step 2: External posting enabled (Day 8+)
  - Exception: Urgent hiring (manager override with HRBP approval)
```

### Candidate Pipeline

```
NEW (1) → REVIEW (2) → SCREEN (3) → INTERVIEW (4) → ASSESSMENT (5)
    → REFERENCE (6) → OFFER (7) → HIRE (8)
                    ↘ REJECTED (9)
                    ↘ WITHDRAWN (10)
                    ↘ ON_HOLD (11)
                    ↘ POOL (12)
```

---

## Integration with Core HR

| Core HR Repository | Records | Recruiting Usage |
|-------------------|--------:|------------------|
| Job.xlsx | 688 | Requisition job code |
| Job Family.xlsx | 27 | Offer letter template selection |
| Grade.xlsx | 20 | Salary range validation |
| Location.xlsx | 919 | Requisition work location |
| Department.xlsx | 10,803 | Hiring department |
| Business Unit.xlsx | 2,175 | Requisition organization |
| Legal Entity.xlsx | 364 | Offer legal employer |

---

## Key Decisions

### Confirmed

| Decision | Value | Notes |
|----------|-------|-------|
| Internal Posting Rule | 7 days mandatory | Step 1 internal, Step 2 external |
| Offer Approval Threshold | EUR 125K base / 155K total | High-value offer escalation |
| TOPEX Escalation | CHRO approval | For executive positions |
| Speculative Applications | Talent Community pool | Configured in Candidate Pool Type |

### Pending

| Decision | Options | Impact |
|----------|---------|--------|
| Job Board Integration | Broadbean vs Oracle native | Integration architecture |
| Background Check Provider | Sterling (US), Certn (EU), TBD (Global) | Vendor selection |
| E-Signature Solution | DocuSign vs Adobe Sign | Offer letter workflow |

---

## Folder Structure

```
02 - Recruiting/
├── 00 - DOCUMENTATION/     # 12 markdown docs
├── 01 - SOURCE DATA/       # TALENTSOFT + UKG exports
├── 02 - MAPPING/           # 3 mapping files
├── 03 - ORACLE/            # 14 repository sheets (191 records)
├── 04 - CONVERSION/        # Scripts + Output
└── 99 - ARCHIVE/           # Old versions
```

---

## Session History

### Session 1 (2025-12-07) - Initial Setup

**Actions Completed:**
1. Analyzed Oracle Recruiting module requirements
2. Identified 14 configuration tables needed
3. Created Python script to generate Excel sheets
4. Populated all 14 repository sheets (191 records)
5. Created 00 - DOCUMENTATION folder
6. Discovered existing ATS analysis (UKG + Talentsoft)
7. Reorganized folder structure (318 → 209 files)
8. Consolidated mapping files, archived old versions
9. Created dedicated Agent Session Tracker

**Final Status:** 14 files | 191 records | 2 ATS analyzed | Folder reorganized

---

### Session 2 (2025-12-07) - Business Requirements Synthesis

**Actions Completed:**
1. Read HR Blueprint - Talent Acquisition PDF (GEODIS policy document)
   - Identified 4 sub-processes: Employer Branding, Recruitment Need, Candidate Selection, Offer Management
   - Extracted key rules: 7-day internal posting, reference checks, agency approval
   - Documented KPIs: Time to fill, Internal fill rate, Diversity metrics

2. Read Talentsoft Recruitment Guidelines (3 documents)
   - Vacancy Request Management: Serial approval workflow, form sections
   - Vacancy Management: Publishing to InJob, geodis.com, Multiposting
   - Selection of Applications: 18 application actions, candidate groups, speculative applications

3. Read UKG TCE Presentation (Americas current state)
   - Volume: 252K applications, 9K hires (2023)
   - Team: 7 Corporate + 18 Frontline recruiters
   - Integrations: Paradox, Sterling, Indeed
   - Desired functionality: Scalability, UX, AI features, Reporting

4. Read Workshop RFP (716 requirements via Python)
   - 9 Recruitment sub-areas identified
   - All Recruitment items marked "Must Have"
   - Key requirements: Auto-populate, Email approval, Multi-posting, Auto-removal

5. Created comprehensive Business Requirements Synthesis document
   - File: `11_Oracle_Recruiting_Business_Requirements.md`
   - 15 sections covering all recruiting areas
   - Gap analysis and recommendations
   - Integration requirements matrix

**Final Status:** Business requirements document complete | 4 sources analyzed | Ready for validation

---

## Next Steps

### Phase 1: Configuration Validation
1. Review requisition templates with HR/TA team
2. Validate candidate phase workflow
3. Confirm offer letter templates by country
4. Finalize approval workflow thresholds

### Phase 2: Integration Decisions
1. Decide on Broadbean vs Oracle native job posting
2. Select background check provider
3. Confirm e-signature solution

### Phase 3: Data Migration Planning
1. Inventory active G-Talent+ data
2. Define migration scope (12 months history)
3. Create HDL templates for recruiting objects

### Phase 4: Career Site Design
1. Configure Oracle Career Site (Redwood UI)
2. Apply GEODIS branding
3. Set up job search and application flow

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
- Business requirements synthesized from 4 sources
- Folder reorganized (6 clean folders)
- Located in: 03 - ORACLE/ folder

Key document:
- 11_Oracle_Recruiting_Business_Requirements.md (comprehensive synthesis)

Focus areas:
- Validate requirements with HR/TA team
- Finalize integration decisions (Indeed, LinkedIn, Sterling)
- Configure approval workflows (7-day internal, EUR 125K thresholds)
- Plan data migration from G-Talent+

Core HR reference (for cross-module alignment):
02 - Define/01 - Repositories/00 - Documentation/00_DOCUMENTATION_INDEX.md
```

---

*Last Updated: 2025-12-07 | Status: SESSION 2 COMPLETE*
*Location: 00 - DOCUMENTATION/01_Agent_Session_Tracker.md*
*Records: 14 Oracle files | 191 records | Business Requirements Complete*
