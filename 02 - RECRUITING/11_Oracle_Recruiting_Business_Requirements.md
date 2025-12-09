# GEODIS Oracle Recruiting - Business Requirements Synthesis

**Document:** 11_Oracle_Recruiting_Business_Requirements.md
**Created:** 2025-12-07
**Status:** COMPLETE
**Version:** 1.0

---

## Executive Summary

This document synthesizes business requirements for the Oracle Recruiting (IRC) module implementation at GEODIS, consolidating inputs from four primary sources:

1. **HR Blueprint - Talent Acquisition** (GEODIS corporate policy)
2. **Talentsoft Guidelines** (Current G-Talent+ system documentation)
3. **UKG TCE Presentation** (Americas current state & desired functionality)
4. **Workshop RFP** (716 functional requirements from business stakeholders)

The analysis covers recruiting volumes, process workflows, integration requirements, compliance needs, and desired future capabilities to ensure Oracle Recruiting is configured to meet GEODIS global standards.

---

## Table of Contents

1. [Source Documents](#1-source-documents)
2. [Recruiting Volume & Scale](#2-recruiting-volume--scale)
3. [Requisition Management](#3-requisition-management)
4. [Job Posting & Sourcing](#4-job-posting--sourcing)
5. [Candidate Management](#5-candidate-management)
6. [Interview Management](#6-interview-management)
7. [Offer Management](#7-offer-management)
8. [Background Checks & Compliance](#8-background-checks--compliance)
9. [Onboarding Integration](#9-onboarding-integration)
10. [Analytics & Reporting](#10-analytics--reporting)
11. [Integration Requirements](#11-integration-requirements)
12. [GEODIS-Specific Business Rules](#12-geodis-specific-business-rules)
13. [Desired Future Functionality](#13-desired-future-functionality)
14. [Oracle Configuration Alignment](#14-oracle-configuration-alignment)
15. [Gap Analysis & Recommendations](#15-gap-analysis--recommendations)

---

## 1. Source Documents

### 1.1 HR Blueprint - Talent Acquisition

**Location:** `01 - Discovery/03 - HR Blueprint/01 - Blueprint per process/[ENG] Talent Acquisition.pdf`

**Content Summary:**
- Official GEODIS recruiting policy document
- Defines 4 sub-processes: Employer Branding, Recruitment Need & JD, Candidate Selection, Offer Management
- Establishes key rules: 7-day internal posting, reference checks, agency approval
- Defines KPIs: Time to fill, Internal fill rate, Diversity metrics

### 1.2 Talentsoft Guidelines (G-Talent+)

**Location:** `01 - Discovery/08 - Talentsoft Guidelines/Recruitment/`

**Documents Analyzed:**
- Vacancy Request Management EN.pdf (16 pages)
- Vacancy Management.pdf (8 pages)
- Selection of Applications EN.pdf (11 pages)

**Content Summary:**
- Current G-Talent+ system workflows
- Vacancy Request → Vacancy → Application lifecycle
- Serial approval workflows
- Publishing to InJob, geodis.com, SNCFLogistics.com
- Multiposting integration (Broadbean equivalent)
- Application action statuses (18 states)

### 1.3 UKG TCE Presentation (Americas)

**Location:** `01 - Discovery/01 - CLUS Requirements/Recruitment/Nov 24 TCE presentation.pdf`

**Content Summary:**
- GEODIS Americas (US) current recruiting operations
- UKG Recruiting Gateway overview
- Volume metrics: 252K applications, 9K hires (2023)
- Technology integrations: Paradox, Sterling, Indeed
- Desired functionality for future ATS

### 1.4 Workshop RFP

**Location:** `01 - Discovery/01 - Business Requirements/WORKSHOP RFP MARION TOUFIK.xlsx`

**Content Summary:**
- 716 functional requirements across all HR areas
- 10 Personas defined
- Recruitment sub-areas: Requisition Management, Job Posting, Candidate Sourcing, Interview Scheduling, Offer Management, Advanced Tools, Employer Branding, Third-Party Integration
- All Recruitment items marked as "Must Have" priority

---

## 2. Recruiting Volume & Scale

### 2.1 Current Volume Metrics (Americas - UKG)

| Year | Applications | Hires | Conversion Rate |
|------|-------------|-------|-----------------|
| 2022 | 124,804 | 14,421 | 11.6% |
| 2023 | 252,901 | 9,089 | 3.6% |
| 2024 (YTD) | 164,136 | 7,298 | 4.4% |

### 2.2 Indeed Applications (Major Source)

| Year | Indeed Applications | % of Total |
|------|-------------------|------------|
| 2022 | 65,055 | 52% |
| 2023 | 185,672 | 73% |
| 2024 (YTD) | 97,492 | 59% |

### 2.3 Talent Team Structure

| Team | Headcount | Scope | Focus |
|------|-----------|-------|-------|
| Corporate Talent Team | 7 | All LoB | Americas HQ, Frontline Management, Regional Office Support |
| Frontline Recruiting | 18 | CL, FF, TM | Hourly, Exempt Non-Leader, Exempt Leader |

### 2.4 Oracle Requirement

**System must scale to handle:**
- 250,000+ applications per year (Americas alone)
- Global rollout will multiply volume significantly
- Peak hiring periods (seasonal warehouse operations)

---

## 3. Requisition Management

### 3.1 Core Requirements

| Requirement | Description | Source | Priority |
|-------------|-------------|--------|----------|
| Job Template Auto-Population | Auto-populate requisition from job code/template | Workshop RFP | Must Have |
| Multi-Company Posting | Single requisition for multiple legal entities | UKG TCE | Must Have |
| Multi-Location Posting | Single requisition for multiple locations | UKG TCE | Must Have |
| Screening Questions | Pre-screening with disqualify logic and points | UKG TCE | Must Have |
| FTE Count Tracking | Number of positions to fill per requisition | UKG TCE | Must Have |
| Employee Type | Hourly/Exempt/Leader classification | UKG TCE | Must Have |
| Reason for Opening | Replacement/Growth/New Position | UKG TCE, Talentsoft | Must Have |
| Requisition Hold | Pause requisition without closing | Workshop RFP | Must Have |
| Incumbent Name | Name of person being replaced | Talentsoft | Must Have |
| Budgeted Flag | Planned vs unplanned vacancy | Talentsoft | Must Have |
| Organization Coding | Department, Business Unit, Cost Center | UKG TCE | Must Have |
| Compensation & Pay Transparency | Salary range with compliance flags | UKG TCE | Must Have |

### 3.2 Requisition Data Fields (from UKG TCE)

**Data Stream:**
- Job codes
- Job descriptions
- Recruiter, Hiring Manager, HR assignments
- Multi Company & Location posting
- Organization coding
- Compensation & Pay Transparency

**Detail Tracking:**
- Intake meeting notes
- Screening Questions
- Required Experience, Education, Certifications
- Number of FTE & Employee Type
- Reason for opening

**Visibility:**
- Manage posting permissions
- Multi-process ability driving interview flow
- Define approval workflow
- Publish to internal/external boards and third-party sites

### 3.3 Approval Workflows

| Workflow | Object | Approvers | Condition | Source |
|----------|--------|-----------|-----------|--------|
| Standard Requisition | Requisition | N+1 → HRBP | Default | Talentsoft, HR Blueprint |
| High Salary Requisition | Requisition | N+1 → HRBP → EVP HR | Salary ≥ EUR 125K | HR Blueprint |
| TOPEX Requisition | Requisition | N+1 → CHRO | TOPEX flag = Y | HR Blueprint |
| Email Approval | Requisition | Via email without ATS login | All | Workshop RFP |

### 3.4 Requisition Lifecycle

**From Talentsoft:**
```
CREATE → AUTHORIZATION REQUEST → SEND → APPROVE → HISTORY
         (Serial approval)      (Sequential approvers)
```

**Oracle Equivalent:**
```
DRAFT → PENDING APPROVAL → APPROVED → OPEN → FILLED/CLOSED
```

---

## 4. Job Posting & Sourcing

### 4.1 Posting Requirements

| Requirement | Description | Source | Priority |
|-------------|-------------|--------|----------|
| **Internal Posting Rule** | 7-day internal posting before external | HR Blueprint | Mandatory |
| Internal Career Site | InJob equivalent for employees | Talentsoft | Must Have |
| External Career Site | geodis.com/careers | Talentsoft | Must Have |
| Multi-Posting | Distribute to multiple job boards simultaneously | Workshop RFP | Must Have |
| Indeed Integration | Direct API integration | UKG TCE | Must Have |
| LinkedIn Integration | Job posting and sourcing | Workshop RFP | Must Have |
| Broadbean Integration | Multi-posting aggregator | Talentsoft | Must Have |
| Auto-Removal | Remove posting when requisition filled | Workshop RFP | Must Have |
| Pay Transparency | Display salary range per state/country laws | UKG TCE | Must Have |

### 4.2 Internal Posting Rule Implementation

**Business Rule (HR Blueprint):**
> Internal candidates must have 7-day priority before external posting

**Implementation in Oracle:**
- Step 1: Internal posting only (Day 1-7)
- Step 2: External posting enabled (Day 8+)
- Exception: Urgent hiring (manager override with HRBP approval)

### 4.3 Publishing Channels (from Talentsoft)

| Channel | Type | Visibility |
|---------|------|------------|
| InJob | Internal | All employees |
| geodis.com | External | Public |
| SNCFLogistics.com | External | Public (legacy) |
| Multiposting | External | Multiple job boards |

### 4.4 Job Boards Integration (from UKG TCE)

**Current 3rd Party Job Sites:**
- Appcast Job Sites
- CareerBuilder Job Sites
- eQuest Job Sites
- FactoryFix Job Sites
- Indeed Job Sites
- Phenom People Job Sites
- Radancy Job Sites
- RiseKit Job Sites
- SmashFly Job Sites
- Symphony Talent: SmashFlyX Job Sites
- Talent.com Job Sites
- TeamWork Online Job Sites
- WayUp Job Sites
- ZipRecruiter Job Sites

### 4.5 Career Site Features (from UKG/Paradox)

- Job Postings & Branding
- Chat/Text to Apply
- Referral Technology
- Virtual Hiring Events

---

## 5. Candidate Management

### 5.1 Candidate Profile Requirements

| Requirement | Description | Source | Priority |
|-------------|-------------|--------|----------|
| Candidate Presence | Work Experience, Education, Certifications, Skills | UKG TCE | Must Have |
| Resume/CV Storage | Parse and store resumes | UKG TCE | Must Have |
| Application Questions | Answers to screening questions | UKG TCE | Must Have |
| References | Reference contact information | UKG TCE | Must Have |
| Internal Candidate Tag | Yellow tag for internal applicants | Talentsoft | Must Have |
| Candidate Ranking | Ability to rank/score applicants | UKG TCE | Nice to Have |
| AI Matching | AI-driven candidate matching | UKG TCE | Desired |

### 5.2 Candidate Search & Filtering

**Filter Capabilities (UKG TCE):**
- Filter by step (phase)
- Filter by type (internal/external)
- Filter by apply date
- Filter by source
- Application date / # of days in step
- Screening status
- Employee referral status

### 5.3 Candidate Actions

**Mass Actions:**
- Mass disposition candidate list
- Add to candidate pool
- Request background check
- Create offer
- Send email
- Schedule meeting

**Individual Actions:**
- Forward applicant details
- Review resume
- Add candidate notes
- Change disposition

### 5.4 Candidate Pipeline

**From All Sources Combined:**

```
┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐
│   NEW   │──▶│  REVIEW │──▶│  SCREEN │──▶│INTERVIEW│──▶│ASSESSMENT│
└─────────┘   └─────────┘   └─────────┘   └─────────┘   └─────────┘
                                                              │
    ┌─────────────────────────────────────────────────────────┘
    │
    ▼
┌─────────┐   ┌─────────┐   ┌─────────┐
│REFERENCE│──▶│  OFFER  │──▶│  HIRE   │
└─────────┘   └─────────┘   └─────────┘
                  │
    ┌─────────────┼─────────────┬─────────────┐
    ▼             ▼             ▼             ▼
┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐
│REJECTED │ │WITHDRAWN│ │ ON_HOLD │ │  POOL   │
└─────────┘ └─────────┘ └─────────┘ └─────────┘
```

### 5.5 Application Actions (from Talentsoft)

| Action | Description |
|--------|-------------|
| CV kept | Initial review - keep for consideration |
| Phone contact | Initial phone screening |
| Interview | In-person or virtual interview |
| Selected | Shortlisted candidate |
| Manager opinion | Hiring manager review |
| Final selection | Final candidate selection |
| Hiring proposal | Offer preparation |
| Recruitment | Hired |

### 5.6 Candidate Pools / Talent Communities

| Pool Type | Description | Source |
|-----------|-------------|--------|
| Silver Medalists | Strong candidates not selected | UKG TCE |
| Talent Community | Speculative applications | Talentsoft |
| Referrals | Employee referral candidates | UKG TCE |
| Private Pools | Recruiter-specific pools | Talentsoft |
| Shared Pools | Team-accessible pools | UKG TCE |

---

## 6. Interview Management

### 6.1 Interview Requirements

| Requirement | Description | Source | Priority |
|-------------|-------------|--------|----------|
| Interview Scheduling | Schedule with interviewers | UKG TCE | Must Have |
| Virtual Interviews | Video interview support | UKG TCE | Must Have |
| On-Site Interviews | In-person scheduling | UKG TCE | Must Have |
| Panel Interviews | Multiple interviewers | UKG TCE | Must Have |
| Calendar Integration | Sync with Outlook/Google | UKG TCE | Must Have |
| Interview Feedback | Capture interviewer ratings | Talentsoft | Must Have |
| Manager Opinion | Hiring manager feedback | Talentsoft | Must Have |
| Auto-Scheduling | AI-scheduled screenings | UKG TCE (Paradox) | Nice to Have |

### 6.2 Interview Types (Oracle Configuration)

| Type | Description |
|------|-------------|
| Phone Screen | Initial recruiter call |
| Video Interview | Virtual meeting |
| On-Site Interview | In-person meeting |
| Panel Interview | Multiple interviewers |
| Technical Interview | Skills assessment |
| Behavioral Interview | Competency-based |
| Executive Interview | Senior leadership |
| Final Interview | Last round |
| Assessment Center | Multi-activity evaluation |

### 6.3 Interview Workflow

**From UKG TCE:**
```
Using Paradox - Schedule interview(s) with Interviewers,
including virtual or in-person as well as 1+ interviewers
or panel interviews. Then disposition accordingly in UKG.
```

---

## 7. Offer Management

### 7.1 Offer Requirements

| Requirement | Description | Source | Priority |
|-------------|-------------|--------|----------|
| Offer Templates | By country and job family | UKG TCE, HR Blueprint | Must Have |
| Multi-Currency | Support all GEODIS currencies | UKG TCE | Must Have |
| Offer Approval | Workflow-based approvals | UKG TCE | Must Have |
| High-Value Escalation | ≥EUR 125K base or 155K total | HR Blueprint | Must Have |
| Electronic Signature | DocuSign/Adobe Sign integration | UKG TCE, Workshop RFP | Must Have |
| Offer Storage | Store signed offer letters | UKG TCE | Must Have |
| Auto-Populate | Candidate and company details | UKG TCE | Must Have |
| Benefits by Country | Country-specific benefits info | UKG TCE | Must Have |
| Document Attachment | Attach additional documents | UKG TCE | Must Have |

### 7.2 Offer Letter Templates (Oracle Configuration)

| Template | Country | Job Family |
|----------|---------|------------|
| GEODIS_FR_STD | France | Standard |
| GEODIS_FR_EXEC | France | Executive |
| GEODIS_US_STD | USA | Standard |
| GEODIS_US_EXEC | USA | Executive |
| GEODIS_UK_STD | UK | Standard |
| GEODIS_DE_STD | Germany | Standard |
| GEODIS_NL_STD | Netherlands | Standard |
| ... | ... | ... |

**Total: 18 templates configured**

### 7.3 Offer Approval Workflows

| Workflow | Approvers | Condition |
|----------|-----------|-----------|
| Standard Offer | Hiring Mgr → HR/Comp | Default |
| High Value Offer | Hiring Mgr → HR/Comp → EVP HR | Base ≥ 125K or Total ≥ 155K |
| TOPEX Offer | Hiring Mgr → CHRO | TOPEX flag = Y |

### 7.4 Offer Process (from UKG TCE)

```
CREATE OFFER ──▶ APPROVAL ──▶ EXTEND TO CANDIDATE ──▶ CANDIDATE ACCEPTS
     │              │                 │                      │
     ▼              ▼                 ▼                      ▼
From Candidate  Sequential      Electronic           Signed Offer
Profile         Approvers       Signature            Stored
```

---

## 8. Background Checks & Compliance

### 8.1 Background Check Requirements

| Requirement | Description | Source | Priority |
|-------------|-------------|--------|----------|
| Integration | Bi-directional with provider | UKG TCE (Sterling) | Must Have |
| Initiate from ATS | Launch check from candidate profile | UKG TCE | Must Have |
| Results in ATS | View results without leaving system | UKG TCE | Must Have |
| Reference Checks | Mandatory for white collar | HR Blueprint | Must Have |

### 8.2 Sterling Integration (Current UKG)

**Features:**
- Simplified workflow - initiate and access results within ATS
- Bi-directional integration
- 68% of background searches close within 1 day

**Check Types (GEODIS NON EXEMPT):**
- SSN Trace
- County Criminal Record
- Enhanced Nationwide Criminal Search
- DOJ Sex Offender Search
- Client Matrix Application

### 8.3 US Immigration & Compliance (from UKG TCE)

| Requirement | Description |
|-------------|-------------|
| Visa Status Tracking | Track visa status and expiration dates |
| I-9 Compliance | Employment eligibility verification |
| PERM Recruitment | Labor certification job posting compliance |
| Pay Scale Compliance | Prevailing wage for visa cases |
| DOL Reporting | Department of Labor documentation |

### 8.4 PERM Recruitment Process

**Required Capabilities:**
- Post jobs on internal website for H-1B visa cases
- Post jobs on external website for PERM cases
- Track completed applications and response options
- Access prior PERM recruitment history
- Provide supporting documentation for DOL challenges

---

## 9. Onboarding Integration

### 9.1 Requirements

| Requirement | Description | Source | Priority |
|-------------|-------------|--------|----------|
| Candidate to Employee | Seamless transition | UKG TCE | Must Have |
| Data Flow to Core HR | Auto-create employee record | UKG TCE | Must Have |
| Pre-Hire Documents | Collect before start date | UKG TCE | Must Have |
| Onboarding Launch | Trigger onboarding workflow | UKG TCE | Must Have |

### 9.2 Onboarding Workflow (from UKG TCE)

```
HIRE DISPOSITION ──▶ HR SERVICE CENTER TICKET ──▶ ONBOARDING GATEWAY
        │                    │                           │
        ▼                    ▼                           ▼
  Candidate info        "Offer Accepted"          Launch onboarding
  verified               ticket created           documents for
                                                  completion prior
                                                  to New Hire Orientation
```

### 9.3 Data Transfer to Core HR

**Required Data Elements:**
- Personal information (name, contact, address)
- Job information (title, department, location)
- Compensation (salary, pay frequency)
- Start date
- Manager assignment
- Legal entity

---

## 10. Analytics & Reporting

### 10.1 Required KPIs (from HR Blueprint)

| KPI | Definition | Frequency |
|-----|------------|-----------|
| New Joiners | Headcount by period | Monthly |
| Time to Fill | Days from requisition approval to hire | Per requisition |
| Time to Publish | Days from request to posting | Per requisition |
| Short-Term Turnover | Leavers within 12 months of hire | Quarterly |
| Internal Fill Rate | % positions filled internally | Quarterly |
| Gender Equality | M/F ratio in hiring | Quarterly |
| Disability Recruitment | Disability hiring metrics | Quarterly |
| Recruiting Costs | Cost per hire | Quarterly |

### 10.2 Dashboard Requirements (from UKG TCE)

| Feature | Description |
|---------|-------------|
| Real-Time Data | Live metrics and counts |
| Filter by Recruiter | View personal workload |
| Filter by Company | Multi-entity visibility |
| Filter by Location | Regional views |
| Click-Through | Drill into categories |
| Customizable Views | Save personal dashboards |

### 10.3 UKG Dashboard Metrics

**Candidates Hired by Source:**
- Paradox (56.3%)
- Indeed
- Walk-In
- Employment Guides
- Company Website
- Other sources

**Opportunities by Status:**
- Draft
- Pending Approval
- Approved
- Rejected
- Published (Internal/External/3rd Party)
- Closed

**Applicants by Phase:**
- Apply
- Initial Review
- Assessment
- Interview
- Application Verification
- Offer
- Hire
- Decline
- Number of days open

---

## 11. Integration Requirements

### 11.1 Required Integrations

| System | Purpose | Direction | Priority |
|--------|---------|-----------|----------|
| **Oracle Core HR** | Employee creation from hire | Outbound | Critical |
| **Oracle Onboarding** | Trigger onboarding workflow | Outbound | Critical |
| **MDM (EBX)** | Organization data sync | Inbound | High |
| **Paradox/Olivia** | AI chatbot, scheduling | Bi-directional | High |
| **Sterling** | Background checks | Bi-directional | High |
| **Indeed** | Job posting, applications | Bi-directional | High |
| **LinkedIn** | Job posting, sourcing | Bi-directional | High |
| **Broadbean** | Multi-posting aggregator | Outbound | Medium |
| **DocuSign** | E-signature for offers | Bi-directional | High |
| **Outlook/Google** | Calendar integration | Bi-directional | Medium |

### 11.2 Current UKG Integrations

**Paradox:**
- Current: Applications flow one-way into UKG
- Future (2025): Bi-directional integration
- Features: Career site, Chat/Text to Apply, Referrals, Virtual Events

**Indeed:**
- Auto-upload new opportunities to Indeed
- Applications sync back to ATS
- Time-saving features for job postings
- Robust tracking analysis

**Sterling:**
- Initiate background check from candidate profile
- Results accessible within ATS
- Bi-directional integration

### 11.3 Integration Frequency

| Integration | Sync Frequency |
|-------------|----------------|
| Paradox - Opportunity Updates | Every 15 minutes |
| Paradox - Employee Access | Once per day |
| Indeed - Job Postings | Real-time |
| Indeed - Applications | Real-time |
| Sterling - Background Checks | Real-time |

---

## 12. GEODIS-Specific Business Rules

### 12.1 Mandatory Rules (from HR Blueprint)

| Rule | Description | Exception |
|------|-------------|-----------|
| **Internal First** | 7-day internal posting before external | Urgent hiring with HRBP approval |
| **6-Month Limit** | Close unfilled requisitions after 6 months | Can be extended with justification |
| **Agency Approval** | Regional HRD approval for recruitment agencies | None |
| **TOPEX Approval** | CHRO approval for executive positions | None |
| **Reference Checks** | Mandatory for white collar positions | None |

### 12.2 Approval Thresholds

| Object | Condition | Escalation |
|--------|-----------|------------|
| Requisition | Salary ≥ EUR 125,000 base | Add EVP HR approval |
| Requisition | TOPEX position | CHRO approval required |
| Offer | Base ≥ EUR 125,000 | Add EVP HR approval |
| Offer | Total ≥ EUR 155,000 | Add EVP HR approval |
| Offer | TOPEX position | CHRO approval required |

### 12.3 Internal Mobility Rule

**From HR Blueprint:**
> "Priority to internal candidates through the appropriate professional development program"

**Implementation:**
- Internal postings visible on InJob (internal career site)
- Internal candidates flagged with yellow tag
- 7-day exclusive internal window
- Internal fill rate tracked as KPI

### 12.4 Recruiter Assignment Rules (from Talentsoft)

| Field | Description |
|-------|-------------|
| Primary Recruiter | Main recruiter responsible for requisition |
| Secondary Recruiter | Backup recruiter |
| Hiring Manager | Decision maker for hiring |
| HRBP | HR Business Partner for approvals |

---

## 13. Desired Future Functionality

### 13.1 From UKG TCE Presentation

| Feature | Description | Oracle Capability |
|---------|-------------|-------------------|
| **Scalability** | Handle growth and increasing volumes | Native cloud scalability |
| **User Experience** | Easy for candidates and recruiters | Redwood UI |
| **Onboarding Integration** | Smooth candidate to employee transition | Oracle Onboarding Cloud |
| **AI Features** | AI-driven candidate matching | Oracle AI/ML features |
| **Integration Capabilities** | Seamless HR tool integration | Oracle Integration Cloud |
| **Reporting & Analytics** | Comprehensive ATS reporting | OTBI, Analytics Cloud |

### 13.2 From Workshop RFP

| Requirement | Description |
|-------------|-------------|
| Internal Mobility Platform | Employees can view and apply for internal positions |
| Email Approval | Approve requisitions/offers without logging in |
| Contractor Association | Link contractors to requisitions for billing |
| Auto-Removal | Automatic job posting removal when filled |
| Direct Job Board Integration | Native API integrations |

### 13.3 Advanced Features for Consideration

| Feature | Benefit | Priority |
|---------|---------|----------|
| AI Resume Parsing | Automatic skill extraction | Medium |
| Chatbot Integration | 24/7 candidate support | High |
| Video Interview Platform | Built-in video interviews | Medium |
| Predictive Analytics | Forecast hiring success | Low |
| Talent Marketplace | Internal gig economy | Future |

---

## 14. Oracle Configuration Alignment

### 14.1 Repository Sheets Status

| Configuration | Records | Status | Alignment |
|---------------|---------|--------|-----------|
| Requisition Template | 5 | Complete | Covers STD, EXEC, FR, US, INTERN |
| Requisition Phase | 8 | Complete | Draft → Open → Filled → Closed |
| Candidate Phase | 12 | Complete | Full pipeline coverage |
| Candidate State | 43 | Complete | Detailed states within phases |
| Candidate Source | 17 | Complete | LinkedIn, Indeed, Referral, Career Site |
| Candidate Pool Type | 7 | Complete | Silver Medalists, Talent Community |
| Offer Letter Template | 18 | Complete | By country (FR, US, UK, DE, NL) |
| Interview Guide | 10 | Complete | By job family |
| Interview Type | 9 | Complete | Phone, Video, On-Site, Panel |
| Posting Channel | 8 | Complete | Internal, LinkedIn, Indeed, Broadbean |
| Rejection Reason | 15 | Complete | Candidate rejection codes |
| Withdrawal Reason | 8 | Complete | Candidate withdrawal codes |
| Recruiting Action | 25 | Complete | All recruiting actions |
| Approval Workflow | 6 | Complete | Requisition and offer approvals |

**Total: 14 files | 191 records**

### 14.2 Alignment with Business Requirements

| Requirement Area | Oracle Config | Gap |
|------------------|---------------|-----|
| Requisition Management | Requisition Template, Phase | None |
| Candidate Pipeline | Candidate Phase, State | None |
| Sourcing | Candidate Source, Posting Channel | None |
| Interviews | Interview Type, Guide | None |
| Offers | Offer Letter Template | None |
| Approvals | Approval Workflow | None |
| Rejections | Rejection/Withdrawal Reason | None |
| Talent Pools | Candidate Pool Type | None |

---

## 15. Gap Analysis & Recommendations

### 15.1 Identified Gaps

| Gap | Description | Impact | Recommendation |
|-----|-------------|--------|----------------|
| **Paradox/AI Chatbot** | Current UKG uses Paradox for candidate communication | HIGH | Evaluate Oracle Recruiting Assistant or Paradox integration |
| **Immigration Tracking** | US-specific PERM, I-9, visa status | HIGH | Configure custom fields or use Oracle Global HR |
| **Global Mobility** | Cross-border transfer tracking | MEDIUM | Leverage Oracle Workforce Management |
| **Pay Transparency** | State/country-specific compliance | HIGH | Configure by location/jurisdiction |
| **Contractor Billing** | Associate contractors with requisitions | LOW | Custom configuration |

### 15.2 Recommendations

#### Short-Term (Phase 1)

1. **Validate Requisition Templates** - Review with HR/TA team for completeness
2. **Confirm Approval Thresholds** - Verify EUR 125K/155K thresholds with Finance
3. **Test Internal Posting Rule** - Implement 7-day delay workflow
4. **Configure Offer Templates** - Finalize 18 country/job family templates

#### Medium-Term (Phase 2)

1. **Job Board Integrations** - Establish Indeed, LinkedIn, Broadbean connections
2. **Background Check Integration** - Connect Sterling or equivalent
3. **E-Signature Integration** - Implement DocuSign for offer letters
4. **Career Site Configuration** - Deploy Oracle Career Site (Redwood)

#### Long-Term (Phase 3)

1. **AI Features** - Evaluate Oracle Recruiting AI capabilities
2. **Predictive Analytics** - Implement hiring success models
3. **Global Mobility** - Extend to cross-border scenarios
4. **Immigration Compliance** - Full US compliance tracking

### 15.3 Open Decisions

| Decision | Options | Owner | Due Date |
|----------|---------|-------|----------|
| Job Board Aggregator | Broadbean vs Oracle native | TA Leadership | TBD |
| Background Check Provider | Sterling vs other | HR Operations | TBD |
| E-Signature Solution | DocuSign vs Adobe Sign | IT/Procurement | TBD |
| AI Chatbot | Paradox vs Oracle Assistant | TA Leadership | TBD |

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-07 | Agent | Initial synthesis from 4 source documents |

---

## Appendix A: Source Document Details

### A.1 HR Blueprint - Talent Acquisition

**Sub-Processes:**
- 2.1 Employer branding
- 2.2 Recruitment need & Job Description
- 2.3 Candidates selection/search
- 2.4 Candidates' recruitment & offer management

### A.2 Talentsoft Vacancy Request Form Sections

1. General information
2. Reason for request
3. Job details
4. Location
5. Criteria
6. Languages
7. Additional info
8. Back Office

### A.3 UKG TCE Workflow Summary

```
ATTRACT (Posting) ──▶ REVIEW (Candidates) ──▶ HIRE (Offer)
```

### A.4 Workshop RFP Recruitment Sub-Areas

1. Requisition Management
2. Job Posting
3. Candidate Sourcing and Screening
4. Interview Scheduling and Collaboration
5. Offer Management
6. Advanced Recruitment Tools
7. Recruitment Marketing and Employer Branding
8. Third-Party Tools Integration
9. User Interface

---

*Document Location: 02 - Recruiting/00 - DOCUMENTATION/11_Oracle_Recruiting_Business_Requirements.md*
*Created: 2025-12-07 | Status: COMPLETE*
*Sources: HR Blueprint, Talentsoft Guidelines, UKG TCE, Workshop RFP*
