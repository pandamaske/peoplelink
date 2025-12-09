# GEODIS HCM - Recruiting Module
## Context & Progress Tracker

---

**Last Updated:** 2025-12-07 (Session 1 - INITIAL SETUP + ATS ANALYSIS)
**Module:** Talent Acquisition / Recruiting
**Status:** 14 Repository Sheets | 191 Records | 2 ATS Analyzed (UKG + Talentsoft)

---

## Module Context & Expertise

### Domain Knowledge
- Oracle Fusion HCM Cloud Recruiting (IRC module)
- Requisition management and approval workflows
- Candidate lifecycle and pipeline management
- Job posting and sourcing strategies
- Offer management and approval
- Integration with Core HR (hire action)
- Career site configuration (Redwood UI)
- Recruiting analytics and reporting

### Current System (G-Talent+ / Talentsoft)
- Talentsoft Recruitment module
- Broadbean job posting integration
- Vacancy request → Vacancy → Closed workflow
- Internal posting 7-day rule
- Speculative applications module

---

## Oracle Recruiting Architecture

### Core Tables

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ORACLE RECRUITING (IRC)                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────┐     ┌─────────────────┐     ┌──────────────┐ │
│  │  REQUISITION    │────▶│   JOB POSTING   │────▶│  CANDIDATE   │ │
│  │  IRC_REQUISITIONS│     │  IRC_JOB_POSTINGS│     │ IRC_CANDIDATES│ │
│  └────────┬────────┘     └─────────────────┘     └──────┬───────┘ │
│           │                                              │         │
│           │              ┌─────────────────┐            │         │
│           └─────────────▶│  APPLICATION    │◀───────────┘         │
│                          │IRC_JOB_APPLICATIONS                    │
│                          └────────┬────────┘                      │
│                                   │                               │
│           ┌───────────────────────┼───────────────────────┐       │
│           ▼                       ▼                       ▼       │
│  ┌─────────────────┐     ┌─────────────────┐     ┌──────────────┐ │
│  │   INTERVIEW     │     │   ASSESSMENT    │     │    OFFER     │ │
│  │ IRC_INTERVIEWS  │     │  IRC_RATINGS    │     │  IRC_OFFERS  │ │
│  └─────────────────┘     └─────────────────┘     └──────┬───────┘ │
│                                                         │         │
│                                                         ▼         │
│                                                  ┌──────────────┐ │
│                                                  │    HIRE      │ │
│                                                  │ PER_ALL_*    │ │
│                                                  └──────────────┘ │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

### Integration with Core HR

When offer is accepted and hire action executed:

| Step | Oracle Table | Action |
|------|--------------|--------|
| 1 | IRC_OFFERS | Offer accepted |
| 2 | PER_ALL_PEOPLE_F | Person record created |
| 3 | PER_ALL_ASSIGNMENTS_F | Assignment created |
| 4 | PER_PERIODS_OF_SERVICE | Employment period started |
| 5 | ORA_HRT_JOURNEYS | Onboarding journey allocated |

---

## Repository Population Summary

### Completed Sheets (2025-12-07)

| # | Repository | Records | Description |
|---|------------|--------:|-------------|
| 1 | Requisition Template | 5 | GEODIS requisition templates |
| 2 | Requisition Phase | 8 | Draft → Open → Filled → Closed |
| 3 | Candidate Phase | 12 | New → Screen → Interview → Offer → Hire |
| 4 | Candidate State | 43 | Detailed states within each phase |
| 5 | Candidate Source | 17 | LinkedIn, Indeed, Referral, Career Site, etc. |
| 6 | Candidate Pool Type | 7 | Silver Medalists, Talent Community, etc. |
| 7 | Offer Letter Template | 18 | By country (FR, US, UK, DE, NL) + job family |
| 8 | Interview Guide | 10 | By job family (General, Technical, Leadership) |
| 9 | Interview Type | 9 | Phone, Video, On-Site, Panel, etc. |
| 10 | Posting Channel | 8 | Internal, LinkedIn, Indeed, Broadbean, etc. |
| 11 | Rejection Reason | 15 | Candidate rejection codes |
| 12 | Withdrawal Reason | 8 | Candidate withdrawal codes |
| 13 | Recruiting Action | 25 | Requisition, candidate, interview, offer actions |
| 14 | Recruiting Approval Workflow | 6 | Requisition and offer approval rules |

**Total Records:** 191

### Sheets to Add (Future)

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

### Candidate Pipeline (Phases)

```
NEW (1) → REVIEW (2) → SCREEN (3) → INTERVIEW (4) → ASSESSMENT (5)
    → REFERENCE (6) → OFFER (7) → HIRE (8)
                    ↘ REJECTED (9)
                    ↘ WITHDRAWN (10)
                    ↘ ON_HOLD (11)
                    ↘ POOL (12)
```

---

## Integration Requirements

### Job Board Integration

| Option | Provider | Status | Notes |
|--------|----------|--------|-------|
| A | Oracle Native (LinkedIn, Indeed) | Evaluate | Built-in connectors |
| B | Oracle Recruiting Booster | Evaluate | AI-powered features |
| C | Broadbean | Current | REST API integration needed |

**Decision Required:** Continue with Broadbean or migrate to Oracle native?

### Background Check Integration

| Provider | Region | Integration |
|----------|--------|-------------|
| TBD | Global | REST API |
| Sterling | US | Partner connector |
| Certn | EU | REST API |

### E-Signature Integration

| Provider | Use Case | Integration |
|----------|----------|-------------|
| DocuSign | Offer letters | Oracle delivered integration |
| Adobe Sign | Alternative | Partner connector |

---

## Data Migration Strategy

### From G-Talent+ to Oracle

| Data Type | Volume | Approach | Priority |
|-----------|--------|----------|----------|
| Open Requisitions | TBD | Manual re-entry or HDL | P1 |
| Active Candidates | TBD | HDL migration | P1 |
| Application History | 12 months | HDL migration | P2 |
| Speculative Apps | TBD | Talent Community pool | P2 |
| Interview Records | TBD | Selective migration | P3 |
| Offer Documents | Recent only | Document migration | P3 |

### HDL Business Objects

| Object | Purpose |
|--------|---------|
| Requisition | Job requisition data |
| Candidate | Candidate profiles |
| JobApplication | Application records |
| RecruiterAssignment | Recruiter assignments |

---

## Session History

### Session 1 (2025-12-07) - Initial Setup + ATS Analysis Discovery

**Actions Completed:**
1. Analyzed Oracle Recruiting module requirements
2. Identified 14 configuration tables needed
3. Created Python script to generate Excel sheets
4. Populated all 14 repository sheets (191 records)
5. Created 00 - DOCUMENTATION folder
6. Created Documentation Index and Session Tracker
7. Discovered existing ATS analysis documentation (UKG + Talentsoft)
8. Updated documentation index with Source System Analysis section

**Repository Sheets Created:**
- Requisition Template (5)
- Requisition Phase (8)
- Candidate Phase (12)
- Candidate State (43)
- Candidate Source (17)
- Candidate Pool Type (7)
- Offer Letter Template (18)
- Interview Guide (10)
- Interview Type (9)
- Posting Channel (8)
- Rejection Reason (15)
- Withdrawal Reason (8)
- Recruiting Action (25)
- Recruiting Approval Workflow (6)

**Existing ATS Analysis Discovered:**

| Document | Content | Status |
|----------|---------|--------|
| UKG_Talentsoft_Gap_Analysis_UPDATED.md | Master gap analysis v2.2, 594 fields | Complete |
| UKG_Talentsoft_Field_Definitions.md | Field definitions, WordPlus tags | Complete |
| UKG GAP ANALYSIS/UKG_Talentsoft_Gap_Analysis.md | SDD coverage, 130 fields not in SDD | Complete |
| UKG GAP ANALYSIS/UKG_vs_Talentsoft_DataModel_Comparison.md | Architecture comparison | Complete |
| UKG GAP ANALYSIS/UKG_Fields_Missing_in_Talentsoft.md | 26 fields data loss checklist | Complete |
| UKG_to_Talentsoft_Converter/README.md | Converter (33,952 offers processed) | Complete |

**UKG to Talentsoft Mapping Summary:**
- Total UKG fields: 594
- Mapped: 454 (76.4%) + 84 reference (14.1%) + 22 system (3.7%)
- Must calculate: 13 (2.2%) - Days-to-hire metrics
- Not available: 13 (2.2%) - Title/Suffix, Incumbent, FTE granularity
- **Coverage rate: 97.8%**

**Key Findings:**
- GEODIS Talentsoft already has custom fields for Incumbent, Budget, FTE%, Licenses
- UKG converter processed 33,952 offers, 116,101 user assignments, 278 entities
- 34 WordPlus tag corrections identified and applied
- SDD reports cover transactional data but not candidate profiles (API required)

**Final Status:** 14 files | 191 records | 2 ATS analyzed | Documentation updated

---

## Next Steps Recommended

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

Current status:
- 14 repository sheets created (191 records)
- Located in: 03 - ORACLE/ folder

Focus areas:
- Requisition template validation
- Approval workflow configuration
- Job board integration decision
- Data migration planning

Core HR reference (for cross-module alignment):
02 - Define/01 - Repositories/00 - Documentation/00_DOCUMENTATION_INDEX.md
```

---

*Last Updated: 2025-12-07 | Status: INITIAL SETUP + ATS ANALYSIS COMPLETE*
*Location: 00 - DOCUMENTATION/01_Module_Session_Tracker.md*
*Records: 14 Oracle files | 191 records | 2 ATS analyzed | 97.8% coverage*
