# GEODIS Recruitment Process Workflows
## Ultra-Comprehensive End-to-End Process Documentation

---

**Document:** 12_GEODIS_Recruitment_Process_Workflows.md
**Version:** 1.0
**Created:** 2025-12-07
**Status:** COMPLETE
**Module:** Oracle Recruiting Cloud (IRC)

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-07 | Claude Code | Initial comprehensive workflow documentation |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [End-to-End Process Overview](#2-end-to-end-process-overview)
3. [Workforce Planning & Requisition Workflows](#3-workforce-planning--requisition-workflows)
4. [Job Posting & Sourcing Workflows](#4-job-posting--sourcing-workflows)
5. [Candidate Management Workflows](#5-candidate-management-workflows)
6. [Interview & Assessment Workflows](#6-interview--assessment-workflows)
7. [Offer & Hire Workflows](#7-offer--hire-workflows)
8. [Integration & System Flows](#8-integration--system-flows)
9. [RACI Matrix & Governance](#9-raci-matrix--governance)
10. [KPIs & Metrics](#10-kpis--metrics)
11. [Appendices](#11-appendices)

---

## 1. Executive Summary

### 1.1 Purpose

This document provides ultra-comprehensive process workflows for GEODIS recruitment operations, consolidating requirements from:

- **HR Blueprint - Talent Acquisition** (GEODIS corporate policy)
- **Talentsoft G-Talent+** (Current global ATS)
- **UKG UltiPro** (Current Americas ATS)
- **Workshop RFP** (716 functional requirements)
- **Oracle Recruiting Cloud** (Target system configuration)

### 1.2 Scope

| Dimension | Coverage |
|-----------|----------|
| **Regions** | Global (Americas, EMEA, APAC) |
| **Volume** | 250,000+ applications/year |
| **Users** | 25+ recruiters, 1,000+ hiring managers |
| **Integrations** | Indeed, LinkedIn, Sterling, DocuSign, Oracle Core HR |

### 1.3 Key Business Rules

| Rule | Description | Exception |
|------|-------------|-----------|
| **7-Day Internal First** | Internal posting before external | Urgent with HRBP approval |
| **6-Month Limit** | Close unfilled requisitions | Extension with justification |
| **High-Value Threshold** | EUR 125K base / 155K total | EVP HR approval required |
| **TOPEX Approval** | Executive positions | CHRO approval required |
| **Reference Checks** | Mandatory for white collar | None |
| **Agency Approval** | Regional HRD approval | None |

### 1.4 Process Actors

| Actor | Role | System Access |
|-------|------|---------------|
| **Hiring Manager** | Initiates requisition, interviews, selects | Requisitions, Candidates |
| **Recruiter** | Manages end-to-end process | Full Recruiting module |
| **HRBP** | Approves requisitions, advises | Approval workflows |
| **HR/Compensation** | Validates offers, salary bands | Offer approval |
| **EVP HR** | High-value approvals | Escalation approvals |
| **CHRO** | TOPEX approvals | Executive approvals |
| **Candidate** | Applies, interviews, accepts | Career site, Self-service |

---

## 2. End-to-End Process Overview

### 2.1 Master Recruitment Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│                           GEODIS RECRUITMENT MASTER WORKFLOW                             │
├─────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                          │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌────────┐ │
│  │ PLANNING │──▶│REQUISITION│──▶│ POSTING  │──▶│SOURCING  │──▶│SCREENING │──▶│INTERVIEW│ │
│  │          │   │          │   │          │   │          │   │          │   │        │ │
│  │ Identify │   │ Create & │   │ Internal │   │ Receive  │   │ Review & │   │Schedule│ │
│  │ Need     │   │ Approve  │   │ External │   │ Apply    │   │ Qualify  │   │Evaluate│ │
│  └──────────┘   └──────────┘   └──────────┘   └──────────┘   └──────────┘   └────────┘ │
│       │              │              │              │              │              │      │
│       ▼              ▼              ▼              ▼              ▼              ▼      │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │                              CANDIDATE PIPELINE                                   │  │
│  │  NEW → REVIEW → SCREEN → INTERVIEW → ASSESSMENT → REFERENCE → OFFER → HIRE      │  │
│  │                    ↘ REJECTED  ↘ WITHDRAWN  ↘ ON_HOLD  ↘ POOL                    │  │
│  └──────────────────────────────────────────────────────────────────────────────────┘  │
│       │              │              │              │              │              │      │
│       ▼              ▼              ▼              ▼              ▼              ▼      │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌────────┐ │
│  │ASSESSMENT│──▶│REFERENCE │──▶│  OFFER   │──▶│ ACCEPT   │──▶│  HIRE    │──▶│ONBOARD │ │
│  │          │   │          │   │          │   │          │   │          │   │        │ │
│  │ Skills   │   │ Check    │   │ Create & │   │ E-Sign   │   │ Core HR  │   │Journey │ │
│  │ Test     │   │ Verify   │   │ Approve  │   │ DocuSign │   │ Record   │   │Launch  │ │
│  └──────────┘   └──────────┘   └──────────┘   └──────────┘   └──────────┘   └────────┘ │
│                                                                                          │
└─────────────────────────────────────────────────────────────────────────────────────────┘
```

### 2.2 Process Phases Summary

| Phase | Duration Target | Key Activities | System |
|-------|-----------------|----------------|--------|
| **1. Planning** | 1-3 days | Identify need, budget check | Oracle HCM |
| **2. Requisition** | 2-5 days | Create, route approval | Oracle Recruiting |
| **3. Posting** | 1-7 days | Internal first, then external | Career Site + Job Boards |
| **4. Sourcing** | Ongoing | Receive applications | Indeed, LinkedIn, Career Site |
| **5. Screening** | 3-5 days | Review, qualify, shortlist | Oracle Recruiting |
| **6. Interview** | 5-10 days | Schedule, conduct, feedback | Outlook + Oracle |
| **7. Assessment** | 2-5 days | Skills test, panel review | Assessment tools |
| **8. Reference** | 2-3 days | Background check, references | Sterling |
| **9. Offer** | 3-5 days | Create, approve, extend | Oracle + DocuSign |
| **10. Hire** | 1 day | Accept, create employee | Oracle Core HR |
| **11. Onboard** | Pre-start | Launch onboarding journey | Oracle Onboarding |

### 2.3 Volume Metrics

| Metric | Annual Volume | Notes |
|--------|---------------|-------|
| Applications received | 250,000+ | Americas alone |
| Indeed applications | 60-73% | Primary source |
| Hires | 9,000-14,000 | Varies by year |
| Conversion rate | 3.6-11.6% | Application to hire |
| Recruiters | 25 | Corporate + Frontline |

---

## 3. Workforce Planning & Requisition Workflows

### 3.1 Standard Requisition Creation Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    3.1 STANDARD REQUISITION CREATION WORKFLOW                        │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  HIRING MANAGER                    SYSTEM                         APPROVERS         │
│  ─────────────                     ──────                         ─────────         │
│       │                               │                               │             │
│       │  1. Identify hiring need      │                               │             │
│       │──────────────────────────────▶│                               │             │
│       │                               │                               │             │
│       │  2. Access Oracle Recruiting  │                               │             │
│       │──────────────────────────────▶│                               │             │
│       │                               │                               │             │
│       │  3. Select template           │                               │             │
│       │     ┌─────────────────────┐   │                               │             │
│       │     │ GEODIS_STD (default)│   │                               │             │
│       │     │ GEODIS_EXEC (TOPEX) │   │                               │             │
│       │     │ GEODIS_FR (France)  │   │                               │             │
│       │     │ GEODIS_US (US/EEO)  │   │                               │             │
│       │     │ GEODIS_INTERN       │   │                               │             │
│       │     └─────────────────────┘   │                               │             │
│       │──────────────────────────────▶│                               │             │
│       │                               │                               │             │
│       │  4. Auto-populate from Job    │                               │             │
│       │◀──────────────────────────────│  Job code → Job title,        │             │
│       │                               │  description, grade,          │             │
│       │                               │  salary range                 │             │
│       │                               │                               │             │
│       │  5. Complete requisition      │                               │             │
│       │     ┌─────────────────────────────────────────────┐           │             │
│       │     │ GENERAL INFORMATION                         │           │             │
│       │     │ • Requisition title                         │           │             │
│       │     │ • Reason for opening (Replacement/Growth)   │           │             │
│       │     │ • Incumbent name (if replacement)           │           │             │
│       │     │ • Is budgeted? (Yes/No)                     │           │             │
│       │     │ • If not budgeted, justification            │           │             │
│       │     ├─────────────────────────────────────────────┤           │             │
│       │     │ POSITION DETAILS                            │           │             │
│       │     │ • Job code (lookup from Job.xlsx - 688)     │           │             │
│       │     │ • Job family (from Job Family.xlsx - 27)    │           │             │
│       │     │ • Grade (from Grade.xlsx - 20)              │           │             │
│       │     │ • Number of positions (headcount)           │           │             │
│       │     │ • FTE % (part-time indicator)               │           │             │
│       │     │ • Contract type (Permanent/Fixed/Intern)    │           │             │
│       │     ├─────────────────────────────────────────────┤           │             │
│       │     │ ORGANIZATION                                │           │             │
│       │     │ • Legal entity (from Legal Entity - 364)    │           │             │
│       │     │ • Business unit (from BU.xlsx - 2,175)      │           │             │
│       │     │ • Department (from Dept.xlsx - 10,803)      │           │             │
│       │     │ • Location (from Location.xlsx - 919)       │           │             │
│       │     │ • Cost center                               │           │             │
│       │     ├─────────────────────────────────────────────┤           │             │
│       │     │ COMPENSATION                                │           │             │
│       │     │ • Salary range (min/max)                    │           │             │
│       │     │ • Currency                                  │           │             │
│       │     │ • Pay transparency flag                     │           │             │
│       │     │ • Hourly/Salaried indicator                 │           │             │
│       │     ├─────────────────────────────────────────────┤           │             │
│       │     │ REQUIREMENTS                                │           │             │
│       │     │ • Education level                           │           │             │
│       │     │ • Experience years                          │           │             │
│       │     │ • Required skills                           │           │             │
│       │     │ • Required certifications                   │           │             │
│       │     │ • Languages                                 │           │             │
│       │     │ • Driving license                           │           │             │
│       │     ├─────────────────────────────────────────────┤           │             │
│       │     │ SCREENING                                   │           │             │
│       │     │ • Pre-screening questions                   │           │             │
│       │     │ • Disqualifying answers                     │           │             │
│       │     │ • Points scoring                            │           │             │
│       │     └─────────────────────────────────────────────┘           │             │
│       │                               │                               │             │
│       │  6. Assign recruiter          │                               │             │
│       │──────────────────────────────▶│                               │             │
│       │                               │                               │             │
│       │  7. Submit for approval       │                               │             │
│       │──────────────────────────────▶│                               │             │
│       │                               │                               │             │
│       │                               │  8. Route to N+1              │             │
│       │                               │─────────────────────────────▶ │             │
│       │                               │                               │             │
│       │                               │                    9. N+1 Review            │
│       │                               │                    ┌──────────────────┐     │
│       │                               │                    │ □ Approve        │     │
│       │                               │                    │ □ Reject         │     │
│       │                               │                    │ □ Request Info   │     │
│       │                               │                    └──────────────────┘     │
│       │                               │◀─────────────────────────────│             │
│       │                               │                               │             │
│       │                               │  10. Route to HRBP            │             │
│       │                               │─────────────────────────────▶ │             │
│       │                               │                               │             │
│       │                               │                   11. HRBP Review           │
│       │                               │                    ┌──────────────────┐     │
│       │                               │                    │ □ Approve        │     │
│       │                               │                    │ □ Reject         │     │
│       │                               │                    │ □ Request Info   │     │
│       │                               │                    └──────────────────┘     │
│       │                               │◀─────────────────────────────│             │
│       │                               │                               │             │
│       │                               │  12. Requisition APPROVED     │             │
│       │◀──────────────────────────────│                               │             │
│       │   Email notification          │                               │             │
│       │                               │                               │             │
│       │                               │  13. Status = OPEN            │             │
│       │                               │  Ready for posting            │             │
│       │                               │                               │             │
└─────────────────────────────────────────────────────────────────────────────────────┘

REQUISITION LIFECYCLE:
┌────────┐   ┌─────────────────┐   ┌──────────┐   ┌────────┐   ┌────────┐   ┌────────┐
│ DRAFT  │──▶│PENDING APPROVAL │──▶│ APPROVED │──▶│  OPEN  │──▶│ FILLED │──▶│ CLOSED │
└────────┘   └─────────────────┘   └──────────┘   └────────┘   └────────┘   └────────┘
                    │                                  │
                    ▼                                  ▼
              ┌──────────┐                       ┌──────────┐
              │ REJECTED │                       │ ON HOLD  │
              └──────────┘                       └──────────┘
```

### 3.2 High-Salary Requisition Approval (≥ EUR 125K)

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│              3.2 HIGH-SALARY REQUISITION APPROVAL WORKFLOW (≥ EUR 125K)              │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  TRIGGER: Salary range maximum ≥ EUR 125,000                                        │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         APPROVAL CHAIN                                        │   │
│  │                                                                               │   │
│  │   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐  │   │
│  │   │   HIRING    │    │    N+1      │    │    HRBP     │    │   EVP HR    │  │   │
│  │   │   MANAGER   │───▶│  MANAGER    │───▶│             │───▶│             │  │   │
│  │   │             │    │             │    │             │    │             │  │   │
│  │   │  Initiator  │    │  1st Level  │    │  2nd Level  │    │  3rd Level  │  │   │
│  │   └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘  │   │
│  │                                                                               │   │
│  │   Timeline:          2 days max        2 days max        3 days max          │   │
│  │   Escalation:        Auto-remind       Auto-remind       CEO notification    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  APPROVAL DECISION POINTS:                                                          │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ N+1 Manager Review                                                          │    │
│  │ ├── Business justification                                                  │    │
│  │ ├── Budget availability                                                     │    │
│  │ ├── Team structure impact                                                   │    │
│  │ └── Headcount allocation                                                    │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ HRBP Review                                                                 │    │
│  │ ├── Job grade alignment                                                     │    │
│  │ ├── Internal equity analysis                                                │    │
│  │ ├── Market rate validation                                                  │    │
│  │ └── Succession planning impact                                              │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ EVP HR Review (HIGH SALARY ONLY)                                            │    │
│  │ ├── Strategic workforce planning                                            │    │
│  │ ├── Executive compensation alignment                                        │    │
│  │ ├── Cross-regional equity                                                   │    │
│  │ └── Board visibility (if required)                                          │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│  EMAIL APPROVAL OPTION:                                                             │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ Approvers can approve/reject via email without logging into Oracle          │    │
│  │ Email contains: Requisition summary, salary details, approve/reject links   │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 3.3 TOPEX (Executive) Requisition Approval

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    3.3 TOPEX REQUISITION APPROVAL WORKFLOW                           │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  TRIGGER: TOPEX flag = Yes (Executive/Leadership positions)                         │
│  TEMPLATE: GEODIS_EXEC                                                              │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         TOPEX APPROVAL CHAIN                                  │   │
│  │                                                                               │   │
│  │   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                      │   │
│  │   │   HIRING    │    │    N+1      │    │    CHRO     │                      │   │
│  │   │   MANAGER   │───▶│  MANAGER    │───▶│             │                      │   │
│  │   │             │    │             │    │             │                      │   │
│  │   │  Initiator  │    │  1st Level  │    │  FINAL      │                      │   │
│  │   └─────────────┘    └─────────────┘    └─────────────┘                      │   │
│  │                                                                               │   │
│  │   Note: HRBP bypassed for TOPEX - goes directly to CHRO                      │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  TOPEX-SPECIFIC REQUIREMENTS:                                                       │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ □ Executive search agency pre-approval (if external search)                 │    │
│  │ □ Succession plan documentation                                              │    │
│  │ □ Organization chart impact                                                  │    │
│  │ □ Board notification (CEO direct reports)                                    │    │
│  │ □ Confidential requisition handling                                          │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 3.4 Requisition Hold/Cancel Workflow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                      3.4 REQUISITION HOLD/CANCEL WORKFLOW                            │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  HOLD REQUISITION (Temporary Pause)                                                 │
│  ─────────────────────────────────────                                              │
│                                                                                      │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐          │
│  │    OPEN     │───▶│  ON HOLD    │───▶│  REACTIVATE │───▶│    OPEN     │          │
│  │ Requisition │    │             │    │  (Resume)   │    │ Requisition │          │
│  └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘          │
│        │                  │                                                         │
│        │                  │ Actions while ON HOLD:                                  │
│        │                  │ • Job postings removed                                  │
│        │                  │ • Applications paused                                   │
│        │                  │ • Candidates notified (optional)                        │
│        │                  │ • Requisition visible but inactive                      │
│        │                  │                                                         │
│        │                  │ Hold Duration: Max 90 days                              │
│        │                  │ After 90 days: Auto-prompt to close or reactivate       │
│        │                                                                            │
│  CANCEL REQUISITION (Permanent Close - No Hire)                                     │
│  ───────────────────────────────────────────────                                    │
│                                                                                      │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                              │
│  │    OPEN     │───▶│  CANCELLED  │───▶│   CLOSED    │                              │
│  │ Requisition │    │   (No Hire) │    │  (Archive)  │                              │
│  └─────────────┘    └─────────────┘    └─────────────┘                              │
│                            │                                                         │
│                            │ Cancel Actions:                                         │
│                            │ • Reason required (budget cut, reorg, etc.)            │
│                            │ • All candidates notified                               │
│                            │ • Job postings removed immediately                      │
│                            │ • Pipeline candidates moved to pool                     │
│                            │ • Audit trail maintained                                │
│                                                                                      │
│  6-MONTH AUTO-CLOSE RULE:                                                           │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ If requisition unfilled after 6 months:                                     │    │
│  │ • System sends warning at 5 months                                          │    │
│  │ • Hiring manager can request extension (justification required)             │    │
│  │ • HRBP approval for extension                                               │    │
│  │ • If no extension: Auto-close with notification                             │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 3.5 Multi-Location/Multi-Company Requisition

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                  3.5 MULTI-LOCATION/MULTI-COMPANY REQUISITION                        │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  USE CASE: Single requisition for multiple locations OR legal entities              │
│  Example: Warehouse Associate needed in 5 distribution centers                       │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         MULTI-LOCATION SETUP                                  │   │
│  │                                                                               │   │
│  │   Single Requisition                                                          │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ Req #12345: Warehouse Associate                                     │    │   │
│  │   │ Total Headcount: 15                                                 │    │   │
│  │   │                                                                     │    │   │
│  │   │ Locations:                                                          │    │   │
│  │   │ ├── Chicago DC      - 4 positions                                   │    │   │
│  │   │ ├── Dallas DC       - 3 positions                                   │    │   │
│  │   │ ├── Los Angeles DC  - 3 positions                                   │    │   │
│  │   │ ├── Atlanta DC      - 3 positions                                   │    │   │
│  │   │ └── New Jersey DC   - 2 positions                                   │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  │   Job Postings (Auto-Generated):                                              │   │
│  │   ├── Internal Career Site: 1 posting (all locations listed)                 │   │
│  │   └── Indeed/LinkedIn: 5 postings (location-specific)                        │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         MULTI-COMPANY SETUP                                   │   │
│  │                                                                               │   │
│  │   Single Requisition                                                          │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ Req #12346: Regional Sales Manager                                  │    │   │
│  │   │ Total Headcount: 3                                                  │    │   │
│  │   │                                                                     │    │   │
│  │   │ Legal Entities:                                                     │    │   │
│  │   │ ├── GEODIS USA Inc.         - 1 position (Texas)                    │    │   │
│  │   │ ├── GEODIS Logistics LLC    - 1 position (California)               │    │   │
│  │   │ └── GEODIS Wilson USA       - 1 position (Ohio)                     │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  │   Offer Letter: Auto-selects correct legal entity template                    │   │
│  │   Payroll Setup: Routes to correct legal entity payroll                       │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  TRACKING:                                                                          │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ Location/Entity │ Budgeted │ Applications │ Interviews │ Offers │ Hired    │    │
│  │─────────────────┼──────────┼──────────────┼────────────┼────────┼──────────│    │
│  │ Chicago DC      │    4     │      45      │     12     │   5    │    4     │    │
│  │ Dallas DC       │    3     │      32      │      8     │   4    │    3     │    │
│  │ Los Angeles DC  │    3     │      51      │     10     │   3    │    2     │    │
│  │ Atlanta DC      │    3     │      28      │      6     │   3    │    3     │    │
│  │ New Jersey DC   │    2     │      22      │      5     │   2    │    2     │    │
│  │─────────────────┼──────────┼──────────────┼────────────┼────────┼──────────│    │
│  │ TOTAL           │   15     │     178      │     41     │  17    │   14     │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 3.6 Requisition Data Integration with Core HR

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                   3.6 REQUISITION DATA INTEGRATION WITH CORE HR                      │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    CORE HR REPOSITORIES USED                                  │   │
│  │                                                                               │   │
│  │   Requisition Field          Core HR Repository          Records             │   │
│  │   ────────────────────       ─────────────────────       ───────             │   │
│  │   Job Code                   Job.xlsx                    688                 │   │
│  │   Job Family                 Job Family.xlsx             27                  │   │
│  │   Grade                      Grade.xlsx                  20                  │   │
│  │   Legal Entity               Legal Entity.xlsx           364                 │   │
│  │   Business Unit              Business Unit.xlsx          2,175               │   │
│  │   Department                 Department.xlsx             10,803              │   │
│  │   Location                   Location.xlsx               919                 │   │
│  │   Position                   Position.xlsx               (Dynamic)           │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  AUTO-POPULATION FLOW:                                                              │
│                                                                                      │
│   ┌─────────────────┐         ┌─────────────────┐         ┌─────────────────┐      │
│   │   User Selects  │         │   System Looks  │         │  Auto-Populates │      │
│   │   Job Code      │────────▶│   Up Job.xlsx   │────────▶│  Fields         │      │
│   │   "WHSE_ASSOC"  │         │                 │         │                 │      │
│   └─────────────────┘         └─────────────────┘         └─────────────────┘      │
│                                                                                      │
│   Auto-populated fields:                                                            │
│   • Job Title: "Warehouse Associate"                                                │
│   • Job Family: "Operations"                                                        │
│   • Grade: "G5"                                                                     │
│   • Salary Range: "$35,000 - $45,000"                                              │
│   • Job Description (standard)                                                      │
│   • Required skills                                                                 │
│   • Required certifications                                                         │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 4. Job Posting & Sourcing Workflows

### 4.1 Seven-Day Internal Posting Rule

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                      4.1 SEVEN-DAY INTERNAL POSTING RULE                             │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  BUSINESS RULE: Internal candidates must have 7-day priority before external        │
│  SOURCE: HR Blueprint - Talent Acquisition                                          │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         POSTING TIMELINE                                      │   │
│  │                                                                               │   │
│  │   DAY 0          DAY 1-7                    DAY 8+                           │   │
│  │   ─────          ───────                    ─────                            │   │
│  │                                                                               │   │
│  │   Requisition    INTERNAL ONLY              INTERNAL + EXTERNAL              │   │
│  │   Approved       ┌─────────────────┐        ┌─────────────────────────────┐  │   │
│  │       │          │ • InJob         │        │ • InJob (internal)          │  │   │
│  │       │          │ • Internal      │        │ • Career Site (external)    │  │   │
│  │       ▼          │   Career Site   │        │ • Indeed                    │  │   │
│  │   ┌───────┐      │ • Email to      │        │ • LinkedIn                  │  │   │
│  │   │ POST  │─────▶│   employees     │───────▶│ • Broadbean (multi-post)    │  │   │
│  │   └───────┘      │                 │        │ • Other job boards          │  │   │
│  │                  │ Visible to:     │        │                             │  │   │
│  │                  │ EMPLOYEES ONLY  │        │ Visible to: EVERYONE        │  │   │
│  │                  └─────────────────┘        └─────────────────────────────┘  │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  WORKFLOW STEPS:                                                                    │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ Step 1: Requisition Approved                                                │    │
│  │         └── System auto-creates internal posting                            │    │
│  │         └── Internal career site (InJob) activated                          │    │
│  │         └── Email notification to department employees                      │    │
│  │                                                                              │    │
│  │ Step 2: Day 1-7 - Internal Window                                           │    │
│  │         └── Only employees can view and apply                               │    │
│  │         └── Internal candidates tagged with yellow indicator                │    │
│  │         └── Hiring manager receives daily application summary               │    │
│  │                                                                              │    │
│  │ Step 3: Day 7 - Review Internal Applicants                                  │    │
│  │         └── Recruiter reviews internal applications                         │    │
│  │         └── Decision point: Sufficient internal candidates?                 │    │
│  │             ├── YES: Continue with internal candidates only                 │    │
│  │             └── NO: Proceed to external posting                             │    │
│  │                                                                              │    │
│  │ Step 4: Day 8+ - External Posting (if needed)                               │    │
│  │         └── System auto-activates external channels                         │    │
│  │         └── Indeed, LinkedIn, career site go live                           │    │
│  │         └── Broadbean multi-posts to additional boards                      │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│  INTERNAL CANDIDATE IDENTIFICATION:                                                 │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   ┌─────────────────────────────────────────────────────────────────────┐   │    │
│  │   │  🟡 INTERNAL CANDIDATE                                              │   │    │
│  │   │                                                                     │   │    │
│  │   │  Name: John Smith                                                   │   │    │
│  │   │  Current Position: Warehouse Associate                              │   │    │
│  │   │  Department: Operations - Chicago DC                                │   │    │
│  │   │  Tenure: 3 years 4 months                                          │   │    │
│  │   │  Employee ID: EMP-12345                                             │   │    │
│  │   │                                                                     │   │    │
│  │   │  Applied: Day 3 of internal window                                  │   │    │
│  │   │  Manager Notification: Sent to current manager                      │   │    │
│  │   └─────────────────────────────────────────────────────────────────────┘   │    │
│  │                                                                              │    │
│  │   Internal candidates receive:                                               │    │
│  │   • Yellow tag/badge in candidate list                                      │    │
│  │   • Employee profile link                                                   │    │
│  │   • Performance history access (for recruiter)                              │    │
│  │   • Current manager notification                                            │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 4.2 Urgent Posting Override (Skip Internal Window)

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    4.2 URGENT POSTING OVERRIDE WORKFLOW                              │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  USE CASE: Business-critical position requiring immediate external posting          │
│  APPROVAL: HRBP approval required to skip 7-day internal window                     │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         URGENT OVERRIDE FLOW                                  │   │
│  │                                                                               │   │
│  │   HIRING MANAGER              HRBP                    SYSTEM                  │   │
│  │   ──────────────              ────                    ──────                  │   │
│  │         │                       │                       │                     │   │
│  │         │  1. Request urgent    │                       │                     │   │
│  │         │     posting           │                       │                     │   │
│  │         │─────────────────────▶ │                       │                     │   │
│  │         │                       │                       │                     │   │
│  │         │     Justification:    │                       │                     │   │
│  │         │     □ Critical skill  │                       │                     │   │
│  │         │     □ Revenue impact  │                       │                     │   │
│  │         │     □ Safety concern  │                       │                     │   │
│  │         │     □ Compliance req  │                       │                     │   │
│  │         │                       │                       │                     │   │
│  │         │                       │  2. Review & approve  │                     │   │
│  │         │                       │─────────────────────▶ │                     │   │
│  │         │                       │                       │                     │   │
│  │         │                       │       ┌───────────────────────────────┐     │   │
│  │         │                       │       │ 3. URGENT FLAG ACTIVATED      │     │   │
│  │         │                       │       │                               │     │   │
│  │         │                       │       │ • Internal + External         │     │   │
│  │         │                       │       │   posted SIMULTANEOUSLY       │     │   │
│  │         │                       │       │ • All channels go live Day 0  │     │   │
│  │         │                       │       │ • Audit log records override  │     │   │
│  │         │                       │       └───────────────────────────────┘     │   │
│  │         │                       │                       │                     │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  TRACKING & COMPLIANCE:                                                             │
│  • All urgent overrides logged for audit                                            │
│  • Monthly report to HR leadership                                                  │
│  • Internal fill rate tracked separately for urgent vs standard                     │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 4.3 Multi-Channel Posting Workflow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                      4.3 MULTI-CHANNEL POSTING WORKFLOW                              │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         POSTING CHANNELS HIERARCHY                            │   │
│  │                                                                               │   │
│  │                        ┌─────────────────────┐                                │   │
│  │                        │  ORACLE RECRUITING  │                                │   │
│  │                        │   (Source System)   │                                │   │
│  │                        └──────────┬──────────┘                                │   │
│  │                                   │                                           │   │
│  │           ┌───────────────────────┼───────────────────────┐                  │   │
│  │           │                       │                       │                  │   │
│  │           ▼                       ▼                       ▼                  │   │
│  │   ┌───────────────┐      ┌───────────────┐      ┌───────────────┐           │   │
│  │   │   INTERNAL    │      │   EXTERNAL    │      │  JOB BOARD    │           │   │
│  │   │   CHANNELS    │      │  CAREER SITE  │      │ INTEGRATIONS  │           │   │
│  │   └───────┬───────┘      └───────┬───────┘      └───────┬───────┘           │   │
│  │           │                      │                      │                    │   │
│  │           ▼                      ▼                      ▼                    │   │
│  │   ┌─────────────┐        ┌─────────────┐        ┌─────────────┐             │   │
│  │   │   InJob     │        │ geodis.com/ │        │   Indeed    │             │   │
│  │   │ (Internal)  │        │  careers    │        │   (API)     │             │   │
│  │   └─────────────┘        └─────────────┘        └─────────────┘             │   │
│  │                                                                               │   │
│  │   ┌─────────────┐        ┌─────────────┐        ┌─────────────┐             │   │
│  │   │  Internal   │        │   Redwood   │        │  LinkedIn   │             │   │
│  │   │  Email      │        │     UI      │        │   (API)     │             │   │
│  │   └─────────────┘        └─────────────┘        └─────────────┘             │   │
│  │                                                                               │   │
│  │                                                 ┌─────────────┐             │   │
│  │                                                 │  Broadbean  │             │   │
│  │                                                 │ (Multi-Post)│             │   │
│  │                                                 └──────┬──────┘             │   │
│  │                                                        │                    │   │
│  │                                    ┌───────────────────┼───────────────────┐│   │
│  │                                    ▼                   ▼                   ▼│   │
│  │                              ┌──────────┐       ┌──────────┐       ┌──────────┐ │
│  │                              │CareerBld │       │ZipRecrtr │       │ Talent   │ │
│  │                              └──────────┘       └──────────┘       │  .com    │ │
│  │                                                                    └──────────┘ │
│  │                              ┌──────────┐       ┌──────────┐       ┌──────────┐ │
│  │                              │ Appcast  │       │FactoryFx │       │  WayUp   │ │
│  │                              └──────────┘       └──────────┘       └──────────┘ │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  CHANNEL CONFIGURATION PER REQUISITION:                                             │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ Channel               │ Auto-Post │ Manual │ Cost    │ Volume │ Quality   │    │
│  │───────────────────────┼───────────┼────────┼─────────┼────────┼───────────│    │
│  │ InJob (Internal)      │    ✓      │        │ Free    │ Low    │ High      │    │
│  │ Oracle Career Site    │    ✓      │        │ Free    │ Medium │ Medium    │    │
│  │ Indeed                │    ✓      │        │ CPC     │ High   │ Variable  │    │
│  │ LinkedIn              │    ✓      │        │ Premium │ Medium │ High      │    │
│  │ Broadbean (Multi)     │           │   ✓    │ Per-post│ High   │ Variable  │    │
│  │ Agency Portal         │           │   ✓    │ Fee     │ Low    │ High      │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│  POSTING DATA FLOW:                                                                 │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Oracle Requisition                    Job Board                            │    │
│  │   ─────────────────                    ─────────                             │    │
│  │                                                                              │    │
│  │   • Job Title          ───────────▶    • Title                              │    │
│  │   • Description1       ───────────▶    • Description                        │    │
│  │   • Description2       ───────────▶    • Requirements                       │    │
│  │   • Location           ───────────▶    • Location                           │    │
│  │   • Salary Range       ───────────▶    • Compensation (if enabled)          │    │
│  │   • Apply URL          ───────────▶    • Apply Link                         │    │
│  │   • Job ID             ───────────▶    • Reference ID                       │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 4.4 Indeed Integration Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                         4.4 INDEED INTEGRATION FLOW                                  │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  VOLUME: 60-73% of all applications come from Indeed                                │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                      OUTBOUND: JOB POSTING TO INDEED                          │   │
│  │                                                                               │   │
│  │   ┌─────────────┐        ┌─────────────┐        ┌─────────────┐              │   │
│  │   │   ORACLE    │        │    API      │        │   INDEED    │              │   │
│  │   │ RECRUITING  │───────▶│  GATEWAY    │───────▶│   PORTAL    │              │   │
│  │   └─────────────┘        └─────────────┘        └─────────────┘              │   │
│  │                                                                               │   │
│  │   Trigger: Requisition approved + External posting enabled                    │   │
│  │   Frequency: Real-time (webhook)                                              │   │
│  │                                                                               │   │
│  │   Data Sent:                                                                  │   │
│  │   • Job title                    • Salary range (if pay transparency)        │   │
│  │   • Job description              • Apply URL (back to Oracle)                │   │
│  │   • Location (city, state)       • Job type (full-time, part-time)           │   │
│  │   • Company name                 • Experience level                          │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    INBOUND: APPLICATIONS FROM INDEED                          │   │
│  │                                                                               │   │
│  │   ┌─────────────┐        ┌─────────────┐        ┌─────────────┐              │   │
│  │   │   INDEED    │        │    API      │        │   ORACLE    │              │   │
│  │   │ APPLICATION │───────▶│  CALLBACK   │───────▶│ RECRUITING  │              │   │
│  │   └─────────────┘        └─────────────┘        └─────────────┘              │   │
│  │                                                                               │   │
│  │   Trigger: Candidate clicks "Apply" on Indeed                                 │   │
│  │   Frequency: Real-time                                                        │   │
│  │                                                                               │   │
│  │   Data Received:                                                              │   │
│  │   • Candidate name               • Phone number                              │   │
│  │   • Email address                • Resume (parsed)                           │   │
│  │   • Indeed profile data          • Application answers (if configured)       │   │
│  │                                                                               │   │
│  │   Auto-Actions in Oracle:                                                     │   │
│  │   • Create candidate profile (if new)                                        │   │
│  │   • Create application linked to requisition                                 │   │
│  │   • Set phase = NEW                                                          │   │
│  │   • Set source = "Indeed"                                                    │   │
│  │   • Trigger screening questions (if configured)                              │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         INDEED APPLY FLOW                                     │   │
│  │                                                                               │   │
│  │   Candidate on Indeed          Oracle Career Site          Oracle ATS        │   │
│  │   ──────────────────          ─────────────────           ──────────         │   │
│  │          │                           │                         │             │   │
│  │          │  1. View job              │                         │             │   │
│  │          │                           │                         │             │   │
│  │          │  2. Click "Apply"         │                         │             │   │
│  │          │─────────────────────────▶ │                         │             │   │
│  │          │   (Redirect to Oracle)    │                         │             │   │
│  │          │                           │                         │             │   │
│  │          │                           │  3. Complete application│             │   │
│  │          │                           │  • Upload resume        │             │   │
│  │          │                           │  • Answer questions     │             │   │
│  │          │                           │  • Consent checkbox     │             │   │
│  │          │                           │─────────────────────────▶             │   │
│  │          │                           │                         │             │   │
│  │          │                           │                4. Application created │   │
│  │          │                           │                   Source = Indeed     │   │
│  │          │                           │                         │             │   │
│  │          │◀──────────────────────────────────────────────────── │             │   │
│  │          │  5. Confirmation email                              │             │   │
│  │          │                                                     │             │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 4.5 LinkedIn Integration Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        4.5 LINKEDIN INTEGRATION FLOW                                 │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    LINKEDIN RECRUITER INTEGRATION                             │   │
│  │                                                                               │   │
│  │   FEATURES:                                                                   │   │
│  │   ├── Job posting to LinkedIn                                                │   │
│  │   ├── LinkedIn profile import                                                │   │
│  │   ├── InMail integration                                                     │   │
│  │   └── Recruiter seat synchronization                                         │   │
│  │                                                                               │   │
│  │   JOB POSTING FLOW:                                                          │   │
│  │                                                                               │   │
│  │   ┌─────────────┐        ┌─────────────┐        ┌─────────────┐              │   │
│  │   │   ORACLE    │        │  LinkedIn   │        │  LinkedIn   │              │   │
│  │   │ Requisition │───────▶│    API      │───────▶│  Job Board  │              │   │
│  │   └─────────────┘        └─────────────┘        └─────────────┘              │   │
│  │                                                                               │   │
│  │   Data Mapping:                                                               │   │
│  │   • Oracle Job Title      →  LinkedIn Title                                  │   │
│  │   • Oracle Location       →  LinkedIn Location                               │   │
│  │   • Oracle Description1   →  LinkedIn Job Description                        │   │
│  │   • Oracle Job Family     →  LinkedIn Industry/Function                      │   │
│  │   • Oracle Experience     →  LinkedIn Seniority Level                        │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    LINKEDIN EASY APPLY FLOW                                   │   │
│  │                                                                               │   │
│  │   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐   │   │
│  │   │  Candidate  │    │  LinkedIn   │    │    API      │    │   Oracle    │   │   │
│  │   │   Profile   │───▶│ Easy Apply  │───▶│  Transfer   │───▶│ Application │   │   │
│  │   └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘   │   │
│  │                                                                               │   │
│  │   Data Transferred:                                                           │   │
│  │   • Name, email, phone                                                       │   │
│  │   • LinkedIn profile URL                                                     │   │
│  │   • Resume (if attached)                                                     │   │
│  │   • Work history (from LinkedIn)                                             │   │
│  │   • Education (from LinkedIn)                                                │   │
│  │   • Skills (from LinkedIn)                                                   │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 4.6 Posting Removal & Auto-Close

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                      4.6 POSTING REMOVAL & AUTO-CLOSE                                │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  AUTO-REMOVAL TRIGGERS:                                                             │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   Trigger Event                    Action                      Timeline      │   │
│  │   ─────────────                    ──────                      ────────      │   │
│  │                                                                               │   │
│  │   Requisition FILLED              Remove from ALL channels     Immediate     │   │
│  │   (All positions hired)           Archive job posting          Same day      │   │
│  │                                   Notify candidates in pipe    24 hours      │   │
│  │                                                                               │   │
│  │   Requisition ON HOLD             Remove from external         Immediate     │   │
│  │                                   Keep internal visible        Optional      │   │
│  │                                   Pause new applications       Immediate     │   │
│  │                                                                               │   │
│  │   Requisition CANCELLED           Remove from ALL channels     Immediate     │   │
│  │                                   Notify ALL candidates        24 hours      │   │
│  │                                   Move pipeline to pool        48 hours      │   │
│  │                                                                               │   │
│  │   Posting End Date Reached        Remove from external         Scheduled     │   │
│  │                                   Prompt recruiter             Same day      │   │
│  │                                   Option to extend             3-day window  │   │
│  │                                                                               │   │
│  │   6-Month Limit Reached           Warning at 5 months          Automated     │   │
│  │                                   Extension request            Required      │   │
│  │                                   Auto-close if no action      Day 180       │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  CANDIDATE NOTIFICATION ON CLOSURE:                                                 │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Template: GEODIS_REQ_CLOSED                                               │    │
│  │                                                                              │    │
│  │   Subject: Update on your application - [Job Title]                         │    │
│  │                                                                              │    │
│  │   Dear [Candidate Name],                                                    │    │
│  │                                                                              │    │
│  │   Thank you for your interest in the [Job Title] position at GEODIS.       │    │
│  │   We wanted to let you know that this position has been filled/closed.     │    │
│  │                                                                              │    │
│  │   We encourage you to:                                                      │    │
│  │   • Visit our careers page for other opportunities                         │    │
│  │   • Join our Talent Community for future openings                          │    │
│  │                                                                              │    │
│  │   Thank you for considering GEODIS.                                        │    │
│  │                                                                              │    │
│  │   Best regards,                                                             │    │
│  │   GEODIS Talent Acquisition Team                                           │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 5. Candidate Management Workflows

### 5.1 Application Intake Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        5.1 APPLICATION INTAKE FLOW                                   │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    APPLICATION ENTRY POINTS                                   │   │
│  │                                                                               │   │
│  │   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │   │
│  │   │   Career    │  │   Indeed    │  │  LinkedIn   │  │  Recruiter  │        │   │
│  │   │    Site     │  │   Apply     │  │ Easy Apply  │  │   Manual    │        │   │
│  │   └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘        │   │
│  │          │                │                │                │               │   │
│  │          └────────────────┴────────────────┴────────────────┘               │   │
│  │                                   │                                          │   │
│  │                                   ▼                                          │   │
│  │                        ┌─────────────────────┐                               │   │
│  │                        │   ORACLE RECRUITING │                               │   │
│  │                        │   Application Queue │                               │   │
│  │                        └──────────┬──────────┘                               │   │
│  │                                   │                                          │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  APPLICATION CREATION PROCESS:                                                      │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   Step 1: Candidate Submits Application                                       │   │
│  │   ─────────────────────────────────────                                       │   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ APPLICATION FORM                                                    │    │   │
│  │   │                                                                     │    │   │
│  │   │ PERSONAL INFORMATION                                                │    │   │
│  │   │ ├── First Name*              ├── Last Name*                        │    │   │
│  │   │ ├── Email*                   ├── Phone*                            │    │   │
│  │   │ ├── Address                  ├── City, State, Zip                  │    │   │
│  │   │ └── Country                                                        │    │   │
│  │   │                                                                     │    │   │
│  │   │ RESUME/CV                                                           │    │   │
│  │   │ ├── Upload file (PDF, DOC, DOCX)                                   │    │   │
│  │   │ └── Parse to extract: Education, Experience, Skills                │    │   │
│  │   │                                                                     │    │   │
│  │   │ SCREENING QUESTIONS                                                 │    │   │
│  │   │ ├── Are you authorized to work in [Country]?*                      │    │   │
│  │   │ ├── Do you have [X] years of experience?*                          │    │   │
│  │   │ ├── Do you have [Certification]?                                   │    │   │
│  │   │ └── Are you willing to relocate?                                   │    │   │
│  │   │                                                                     │    │   │
│  │   │ CONSENT                                                             │    │   │
│  │   │ ├── □ I consent to data processing (GDPR)*                         │    │   │
│  │   │ └── □ I certify information is accurate*                           │    │   │
│  │   │                                                                     │    │   │
│  │   │ [SUBMIT APPLICATION]                                                │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  │   Step 2: System Processing                                                   │   │
│  │   ─────────────────────────                                                   │   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ 1. Duplicate check (email, phone)                                   │    │   │
│  │   │    ├── New candidate: Create profile                                │    │   │
│  │   │    └── Existing: Link to existing profile                           │    │   │
│  │   │                                                                     │    │   │
│  │   │ 2. Resume parsing                                                   │    │   │
│  │   │    ├── Extract education details                                    │    │   │
│  │   │    ├── Extract work experience                                      │    │   │
│  │   │    └── Extract skills & certifications                              │    │   │
│  │   │                                                                     │    │   │
│  │   │ 3. Screening question evaluation                                    │    │   │
│  │   │    ├── Score answers (if points configured)                         │    │   │
│  │   │    ├── Check disqualifying answers                                  │    │   │
│  │   │    └── Auto-reject if knockout criteria met                         │    │   │
│  │   │                                                                     │    │   │
│  │   │ 4. Source tracking                                                  │    │   │
│  │   │    └── Record: Indeed/LinkedIn/Career Site/Referral/etc.            │    │   │
│  │   │                                                                     │    │   │
│  │   │ 5. Internal candidate check                                         │    │   │
│  │   │    ├── Match email to employee database                             │    │   │
│  │   │    └── If match: Flag as INTERNAL + notify current manager          │    │   │
│  │   │                                                                     │    │   │
│  │   │ 6. Application created                                              │    │   │
│  │   │    ├── Phase = NEW                                                  │    │   │
│  │   │    ├── State = Application Received                                 │    │   │
│  │   │    └── Timestamp recorded                                           │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  │   Step 3: Notifications                                                       │   │
│  │   ────────────────────                                                        │   │
│  │                                                                               │   │
│  │   To Candidate:                                                               │   │
│  │   • Confirmation email with application reference number                      │   │
│  │   • Link to candidate self-service portal                                     │   │
│  │                                                                               │   │
│  │   To Recruiter:                                                               │   │
│  │   • New application notification                                              │   │
│  │   • Daily digest summary (configurable)                                       │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 5.2 Candidate Pipeline - 12 Phases with 43 States

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                   5.2 CANDIDATE PIPELINE - 12 PHASES / 43 STATES                     │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         CANDIDATE PHASE FLOW                                  │   │
│  │                                                                               │   │
│  │  ┌─────┐ ┌──────┐ ┌──────┐ ┌─────────┐ ┌──────────┐ ┌─────────┐ ┌─────┐     │   │
│  │  │ NEW │▶│REVIEW│▶│SCREEN│▶│INTERVIEW│▶│ASSESSMENT│▶│REFERENCE│▶│OFFER│     │   │
│  │  │ (1) │ │ (2)  │ │ (3)  │ │   (4)   │ │   (5)    │ │   (6)   │ │ (7) │     │   │
│  │  └─────┘ └──────┘ └──────┘ └─────────┘ └──────────┘ └─────────┘ └──┬──┘     │   │
│  │                                                                     │        │   │
│  │                                                                     ▼        │   │
│  │                                                               ┌─────────┐    │   │
│  │                                                               │  HIRE   │    │   │
│  │                                                               │   (8)   │    │   │
│  │                                                               └─────────┘    │   │
│  │                                                                              │   │
│  │  EXIT PHASES (from any active phase):                                        │   │
│  │  ┌──────────┐  ┌───────────┐  ┌─────────┐  ┌────────┐                       │   │
│  │  │ REJECTED │  │ WITHDRAWN │  │ ON_HOLD │  │  POOL  │                       │   │
│  │  │   (9)    │  │   (10)    │  │  (11)   │  │  (12)  │                       │   │
│  │  └──────────┘  └───────────┘  └─────────┘  └────────┘                       │   │
│  │                                                                              │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  DETAILED STATES PER PHASE:                                                         │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ PHASE 1: NEW (3 states)                                                     │    │
│  │ ├── Application Received                                                    │    │
│  │ ├── Duplicate Check Pending                                                 │    │
│  │ └── Ready for Review                                                        │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 2: REVIEW (4 states)                                                  │    │
│  │ ├── Under Review                                                            │    │
│  │ ├── Hiring Manager Review                                                   │    │
│  │ ├── Shortlisted                                                             │    │
│  │ └── Additional Info Requested                                               │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 3: SCREEN (4 states)                                                  │    │
│  │ ├── Phone Screen Scheduled                                                  │    │
│  │ ├── Phone Screen Completed                                                  │    │
│  │ ├── Video Screen Scheduled                                                  │    │
│  │ └── Screen Passed                                                           │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 4: INTERVIEW (6 states)                                               │    │
│  │ ├── Interview Scheduling                                                    │    │
│  │ ├── Interview Scheduled                                                     │    │
│  │ ├── Interview In Progress                                                   │    │
│  │ ├── Interview Completed                                                     │    │
│  │ ├── Additional Interview Required                                           │    │
│  │ └── Interview Passed                                                        │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 5: ASSESSMENT (4 states)                                              │    │
│  │ ├── Assessment Pending                                                      │    │
│  │ ├── Assessment In Progress                                                  │    │
│  │ ├── Assessment Completed                                                    │    │
│  │ └── Assessment Passed                                                       │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 6: REFERENCE (4 states)                                               │    │
│  │ ├── Reference Check Initiated                                               │    │
│  │ ├── References Pending                                                      │    │
│  │ ├── Background Check In Progress                                            │    │
│  │ └── References Verified                                                     │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 7: OFFER (5 states)                                                   │    │
│  │ ├── Offer Pending Approval                                                  │    │
│  │ ├── Offer Approved                                                          │    │
│  │ ├── Offer Extended                                                          │    │
│  │ ├── Offer Negotiation                                                       │    │
│  │ └── Offer Accepted                                                          │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 8: HIRE (3 states)                                                    │    │
│  │ ├── Pre-Hire Processing                                                     │    │
│  │ ├── Hire Confirmed                                                          │    │
│  │ └── Onboarding Initiated                                                    │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 9: REJECTED (5 states)                                                │    │
│  │ ├── Auto-Rejected (Screening)                                               │    │
│  │ ├── Rejected - Not Qualified                                                │    │
│  │ ├── Rejected - Position Filled                                              │    │
│  │ ├── Rejected - No Response                                                  │    │
│  │ └── Rejected - Other                                                        │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 10: WITHDRAWN (3 states)                                              │    │
│  │ ├── Candidate Withdrew                                                      │    │
│  │ ├── Accepted Other Offer                                                    │    │
│  │ └── No Longer Available                                                     │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 11: ON_HOLD (2 states)                                                │    │
│  │ ├── On Hold - Candidate Request                                             │    │
│  │ └── On Hold - Requisition Hold                                              │    │
│  ├─────────────────────────────────────────────────────────────────────────────┤    │
│  │ PHASE 12: POOL (3 states)                                                   │    │
│  │ ├── Silver Medalist                                                         │    │
│  │ ├── Talent Community                                                        │    │
│  │ └── Future Consideration                                                    │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│  TOTAL: 12 Phases | 43 States                                                       │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 5.3 Candidate Screening & Auto-Disqualification

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                  5.3 CANDIDATE SCREENING & AUTO-DISQUALIFICATION                     │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    SCREENING QUESTION TYPES                                   │   │
│  │                                                                               │   │
│  │   ┌────────────────┬────────────────────────────────────────────────────┐    │   │
│  │   │ Type           │ Example                                            │    │   │
│  │   ├────────────────┼────────────────────────────────────────────────────┤    │   │
│  │   │ Yes/No         │ Are you authorized to work in the US?              │    │   │
│  │   │ (Knockout)     │ [Yes = Pass, No = Auto-Reject]                     │    │   │
│  │   ├────────────────┼────────────────────────────────────────────────────┤    │   │
│  │   │ Multiple Choice│ How many years of warehouse experience?            │    │   │
│  │   │ (Scored)       │ [0-1: 0pts, 2-3: 5pts, 4-5: 10pts, 5+: 15pts]      │    │   │
│  │   ├────────────────┼────────────────────────────────────────────────────┤    │   │
│  │   │ Numeric Range  │ What is your expected salary?                      │    │   │
│  │   │                │ [Min: $35,000 - Max: $55,000]                      │    │   │
│  │   ├────────────────┼────────────────────────────────────────────────────┤    │   │
│  │   │ Text           │ Describe your forklift certification               │    │   │
│  │   │                │ [Free text response]                               │    │   │
│  │   ├────────────────┼────────────────────────────────────────────────────┤    │   │
│  │   │ Date           │ What is your earliest available start date?        │    │   │
│  │   │                │ [Date picker]                                      │    │   │
│  │   └────────────────┴────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  AUTO-DISQUALIFICATION FLOW:                                                        │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   ┌─────────────┐    ┌─────────────┐    ┌─────────────────────────────┐      │   │
│  │   │  Candidate  │    │  Screening  │    │     Evaluation Engine       │      │   │
│  │   │  Submits    │───▶│  Questions  │───▶│                             │      │   │
│  │   │ Application │    │  Answered   │    │  ┌─────────────────────────┐│      │   │
│  │   └─────────────┘    └─────────────┘    │  │ Check Knockout Questions││      │   │
│  │                                          │  │                         ││      │   │
│  │                                          │  │ Q: Work authorization?  ││      │   │
│  │                                          │  │ A: No                   ││      │   │
│  │                                          │  │ Result: DISQUALIFY      ││      │   │
│  │                                          │  └────────────┬────────────┘│      │   │
│  │                                          └───────────────┼─────────────┘      │   │
│  │                                                          │                    │   │
│  │                                                          ▼                    │   │
│  │                                               ┌─────────────────────┐         │   │
│  │                                               │   AUTO-REJECTED     │         │   │
│  │                                               │                     │         │   │
│  │                                               │ Phase: REJECTED     │         │   │
│  │                                               │ State: Auto-Rejected│         │   │
│  │                                               │ Reason: Work Auth   │         │   │
│  │                                               └─────────────────────┘         │   │
│  │                                                          │                    │   │
│  │                                                          ▼                    │   │
│  │                                               ┌─────────────────────┐         │   │
│  │                                               │ Rejection Email     │         │   │
│  │                                               │ (Auto-sent)         │         │   │
│  │                                               └─────────────────────┘         │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  SCORING EXAMPLE:                                                                   │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ Candidate: John Smith                          Total Score: 75/100          │    │
│  │                                                                              │    │
│  │ Question                          Answer              Points                 │    │
│  │ ──────────────────────────────────────────────────────────────────────────  │    │
│  │ Years of experience?              4-5 years           15/15                  │    │
│  │ Forklift certification?           Yes                 20/20                  │    │
│  │ Shift flexibility?                Days only           10/20                  │    │
│  │ Education level?                  High School         10/15                  │    │
│  │ Leadership experience?            No                  0/15                   │    │
│  │ Available within 2 weeks?         Yes                 20/15                  │    │
│  │ ──────────────────────────────────────────────────────────────────────────  │    │
│  │ TOTAL                                                 75/100                 │    │
│  │                                                                              │    │
│  │ Threshold for auto-advance: 60    Status: QUALIFIED                         │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 5.4 Mass Disposition Workflow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        5.4 MASS DISPOSITION WORKFLOW                                 │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  USE CASE: Recruiter needs to move multiple candidates to new phase/state           │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         MASS DISPOSITION SCREEN                               │   │
│  │                                                                               │   │
│  │   Requisition: REQ-12345 - Warehouse Associate                               │   │
│  │   Current view: 45 candidates in REVIEW phase                                │   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ □ Select All | ■ 12 Selected                                        │    │   │
│  │   ├─────────────────────────────────────────────────────────────────────┤    │   │
│  │   │ ■ John Smith      | Score: 85 | Source: Indeed  | Days: 3          │    │   │
│  │   │ ■ Jane Doe        | Score: 78 | Source: Career  | Days: 5          │    │   │
│  │   │ ■ Bob Johnson     | Score: 92 | Source: Indeed  | Days: 2          │    │   │
│  │   │ □ Alice Brown     | Score: 45 | Source: Indeed  | Days: 7          │    │   │
│  │   │ ■ Mike Wilson     | Score: 88 | Source: Referral| Days: 1          │    │   │
│  │   │ ...                                                                 │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  │   BULK ACTIONS:                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ [Move to Phase ▼]  [Change State ▼]  [Send Email ▼]  [Add to Pool]  │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  │   Selected Action: Move to SCREEN phase                                       │   │
│  │   New State: Phone Screen Scheduled                                          │   │
│  │   Add Note: "Batch moved after initial review - high potential candidates"   │   │
│  │                                                                               │   │
│  │   [APPLY TO 12 CANDIDATES]                                                    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  MASS REJECTION FLOW:                                                               │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   1. Select candidates (filter by score < threshold)                          │   │
│  │   2. Choose "Reject" action                                                   │   │
│  │   3. Select rejection reason (required):                                      │   │
│  │      ├── Not Qualified - Skills                                              │   │
│  │      ├── Not Qualified - Experience                                          │   │
│  │      ├── Not Qualified - Education                                           │   │
│  │      ├── Position Filled                                                     │   │
│  │      ├── No Response                                                         │   │
│  │      └── Other (specify)                                                     │   │
│  │   4. Select email template:                                                   │   │
│  │      ├── GEODIS_REJECT_STANDARD                                              │   │
│  │      ├── GEODIS_REJECT_POSITION_FILLED                                       │   │
│  │      └── No email                                                            │   │
│  │   5. Confirm and execute                                                      │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 5.5 Talent Pool Management

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                       5.5 TALENT POOL MANAGEMENT                                     │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         POOL TYPES (7 Configured)                             │   │
│  │                                                                               │   │
│  │   Pool Type              Description                    Auto-Add Criteria    │   │
│  │   ─────────              ───────────                    ──────────────────   │   │
│  │                                                                               │   │
│  │   Silver Medalist        Strong candidates not selected Reached Offer phase, │   │
│  │                          for current role               not hired             │   │
│  │                                                                               │   │
│  │   Talent Community       Speculative applications       Applied without       │   │
│  │                          (no specific role)             specific requisition  │   │
│  │                                                                               │   │
│  │   Employee Referrals     Referred candidates            Source = Referral     │   │
│  │                          across all roles                                     │   │
│  │                                                                               │   │
│  │   Internal Mobility      Internal candidates            Internal flag = Y     │   │
│  │                          expressing interest            Not selected          │   │
│  │                                                                               │   │
│  │   Graduate Pipeline      Recent graduates               Education < 2 years   │   │
│  │                          for entry-level roles          ago                   │   │
│  │                                                                               │   │
│  │   Executive Pipeline     Senior candidates              Grade >= Director     │   │
│  │                          for leadership roles           Not selected          │   │
│  │                                                                               │   │
│  │   Alumni Rehire          Former employees               Previous employee ID  │   │
│  │                          eligible for rehire            exists                │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  POOL WORKFLOW:                                                                     │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   ADD TO POOL                                                                 │   │
│  │   ───────────                                                                 │   │
│  │                                                                               │   │
│  │   ┌─────────────┐         ┌─────────────┐         ┌─────────────┐            │   │
│  │   │  Candidate  │         │  Select     │         │  Candidate  │            │   │
│  │   │  Rejected/  │────────▶│  Pool Type  │────────▶│  Added to   │            │   │
│  │   │  Not Hired  │         │  + Notes    │         │  Pool       │            │   │
│  │   └─────────────┘         └─────────────┘         └─────────────┘            │   │
│  │                                                                               │   │
│  │   SEARCH POOL                                                                 │   │
│  │   ───────────                                                                 │   │
│  │                                                                               │   │
│  │   New requisition opened                                                      │   │
│  │   ┌─────────────┐         ┌─────────────┐         ┌─────────────┐            │   │
│  │   │  Search     │         │  View       │         │  Re-engage  │            │   │
│  │   │  Pools by   │────────▶│  Matching   │────────▶│  Candidate  │            │   │
│  │   │  Skills/Loc │         │  Candidates │         │  (New App)  │            │   │
│  │   └─────────────┘         └─────────────┘         └─────────────┘            │   │
│  │                                                                               │   │
│  │   POOL MAINTENANCE                                                            │   │
│  │   ────────────────                                                            │   │
│  │                                                                               │   │
│  │   • GDPR: Auto-remove after consent expiry (configurable: 12-24 months)      │   │
│  │   • Inactive: Flag candidates with no engagement > 6 months                   │   │
│  │   • Duplicate: Merge duplicate candidate profiles                             │   │
│  │   • Opted-out: Remove candidates who request deletion                         │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 5.6 Candidate Communication Workflow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    5.6 CANDIDATE COMMUNICATION WORKFLOW                              │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    AUTOMATED EMAIL TRIGGERS                                   │   │
│  │                                                                               │   │
│  │   Phase Transition          Email Template              Timing               │   │
│  │   ────────────────          ──────────────              ──────               │   │
│  │                                                                               │   │
│  │   Application Received      GEODIS_APP_CONFIRM          Immediate            │   │
│  │   Phone Screen Scheduled    GEODIS_SCREEN_INVITE        Immediate            │   │
│  │   Interview Scheduled       GEODIS_INTERVIEW_INVITE     Immediate            │   │
│  │   Interview Reminder        GEODIS_INTERVIEW_REMINDER   24 hrs before        │   │
│  │   Assessment Sent           GEODIS_ASSESSMENT_LINK      Immediate            │   │
│  │   Offer Extended            GEODIS_OFFER_LETTER         Immediate            │   │
│  │   Offer Accepted            GEODIS_WELCOME              Immediate            │   │
│  │   Rejected                  GEODIS_REJECT_STANDARD      Same day             │   │
│  │   Position Filled           GEODIS_POSITION_FILLED      Same day             │   │
│  │   No Response (14 days)     GEODIS_FOLLOWUP             Day 14               │   │
│  │   Pool Added                GEODIS_TALENT_COMMUNITY     Immediate            │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    CANDIDATE SELF-SERVICE PORTAL                              │   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ GEODIS Candidate Portal                                             │    │   │
│  │   │                                                                     │    │   │
│  │   │ Welcome, John Smith                                                 │    │   │
│  │   │                                                                     │    │   │
│  │   │ MY APPLICATIONS                                                     │    │   │
│  │   │ ┌─────────────────────────────────────────────────────────────┐    │    │   │
│  │   │ │ Warehouse Associate - Chicago DC                            │    │    │   │
│  │   │ │ Status: Interview Scheduled                                 │    │    │   │
│  │   │ │ Applied: Dec 1, 2025                                        │    │    │   │
│  │   │ │ Next Step: Video Interview - Dec 10, 2025 @ 2:00 PM        │    │    │   │
│  │   │ │ [View Details] [Withdraw Application]                       │    │    │   │
│  │   │ └─────────────────────────────────────────────────────────────┘    │    │   │
│  │   │                                                                     │    │   │
│  │   │ MY PROFILE                                                          │    │   │
│  │   │ ├── Update contact information                                     │    │   │
│  │   │ ├── Upload new resume                                              │    │   │
│  │   │ ├── Manage communication preferences                               │    │   │
│  │   │ └── Data privacy settings (GDPR)                                   │    │   │
│  │   │                                                                     │    │   │
│  │   │ RECOMMENDED JOBS                                                    │    │   │
│  │   │ Based on your profile...                                           │    │   │
│  │   │                                                                     │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 6. Interview & Assessment Workflows

### 6.1 Interview Scheduling Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        6.1 INTERVIEW SCHEDULING FLOW                                 │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    INTERVIEW TYPES SUPPORTED                                  │   │
│  │                                                                               │   │
│  │   Type                  Format              Duration    Typical Stage         │   │
│  │   ────                  ──────              ────────    ─────────────         │   │
│  │   Phone Screen          Audio call          15-30 min   Screen phase          │   │
│  │   Video Screen          Teams/Zoom          30-45 min   Screen phase          │   │
│  │   Hiring Manager        In-person/Video     45-60 min   Interview phase       │   │
│  │   Technical             In-person/Video     60-90 min   Interview phase       │   │
│  │   Panel Interview       In-person/Video     60-90 min   Interview phase       │   │
│  │   Executive/Final       In-person           60-90 min   Interview phase       │   │
│  │   On-site Visit         In-person           2-4 hours   Interview phase       │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  SCHEDULING WORKFLOW:                                                               │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   RECRUITER                    SYSTEM                    CANDIDATE            │   │
│  │   ─────────                    ──────                    ─────────            │   │
│  │       │                           │                           │               │   │
│  │       │  1. Select candidate      │                           │               │   │
│  │       │     for interview         │                           │               │   │
│  │       │──────────────────────────▶│                           │               │   │
│  │       │                           │                           │               │   │
│  │       │  2. Choose interview type │                           │               │   │
│  │       │     & interviewer(s)      │                           │               │   │
│  │       │──────────────────────────▶│                           │               │   │
│  │       │                           │                           │               │   │
│  │       │                           │  3. Check interviewer     │               │   │
│  │       │                           │     calendar availability │               │   │
│  │       │                           │     (Outlook integration) │               │   │
│  │       │                           │                           │               │   │
│  │       │  4. Select time slots     │                           │               │   │
│  │       │     (up to 5 options)     │                           │               │   │
│  │       │──────────────────────────▶│                           │               │   │
│  │       │                           │                           │               │   │
│  │       │                           │  5. Send scheduling       │               │   │
│  │       │                           │     invitation to         │               │   │
│  │       │                           │     candidate             │               │   │
│  │       │                           │──────────────────────────▶│               │   │
│  │       │                           │                           │               │   │
│  │       │                           │                           │  6. Candidate │   │
│  │       │                           │                           │     selects   │   │
│  │       │                           │                           │     slot      │   │
│  │       │                           │◀──────────────────────────│               │   │
│  │       │                           │                           │               │   │
│  │       │                           │  7. Auto-confirm:         │               │   │
│  │       │                           │  • Calendar invite sent   │               │   │
│  │       │                           │  • Teams link generated   │               │   │
│  │       │                           │  • Reminder scheduled     │               │   │
│  │       │                           │                           │               │   │
│  │       │◀──────────────────────────│──────────────────────────▶│               │   │
│  │       │  8. Notification:         │  8. Confirmation email    │               │   │
│  │       │     Interview scheduled   │     with details          │               │   │
│  │       │                           │                           │               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  CALENDAR INTEGRATION:                                                              │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   ┌─────────────┐        ┌─────────────┐        ┌─────────────┐             │    │
│  │   │   ORACLE    │◀──────▶│  MICROSOFT  │◀──────▶│  OUTLOOK    │             │    │
│  │   │ RECRUITING  │  API   │   GRAPH     │  Sync  │  CALENDAR   │             │    │
│  │   └─────────────┘        └─────────────┘        └─────────────┘             │    │
│  │                                                                              │    │
│  │   Features:                                                                  │    │
│  │   • Real-time availability check                                            │    │
│  │   • Auto-create calendar events                                             │    │
│  │   • Teams meeting link generation                                           │    │
│  │   • Conflict detection                                                      │    │
│  │   • Reschedule synchronization                                              │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 6.2 Panel Interview Coordination

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                      6.2 PANEL INTERVIEW COORDINATION                                │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  USE CASE: Multiple interviewers evaluate same candidate (common for mid-senior)    │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         PANEL SETUP                                           │   │
│  │                                                                               │   │
│  │   Panel Configuration for: Senior Operations Manager                          │   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ INTERVIEWER          │ ROLE           │ FOCUS AREA      │ REQUIRED │    │   │
│  │   ├──────────────────────┼────────────────┼─────────────────┼──────────│    │   │
│  │   │ John Smith (HM)      │ Hiring Manager │ Overall fit     │    ✓     │    │   │
│  │   │ Jane Doe             │ Director Ops   │ Leadership      │    ✓     │    │   │
│  │   │ Bob Wilson           │ Peer Manager   │ Collaboration   │          │    │   │
│  │   │ Alice Chen           │ HRBP           │ Culture fit     │    ✓     │    │   │
│  │   │ Mike Johnson         │ Technical Lead │ Technical skills│          │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  │   Panel Type: Sequential (one after another) / Concurrent (same time)        │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  SEQUENTIAL PANEL FLOW:                                                             │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   9:00 AM          10:00 AM         11:00 AM         12:00 PM                │   │
│  │   ────────         ────────         ────────         ────────                │   │
│  │                                                                               │   │
│  │   ┌─────────┐      ┌─────────┐      ┌─────────┐      ┌─────────┐            │   │
│  │   │  HM     │      │Director │      │  HRBP   │      │Technical│            │   │
│  │   │Interview│─────▶│Interview│─────▶│Interview│─────▶│Interview│            │   │
│  │   │ 45 min  │      │ 45 min  │      │ 30 min  │      │ 60 min  │            │   │
│  │   └─────────┘      └─────────┘      └─────────┘      └─────────┘            │   │
│  │       │                │                │                │                   │   │
│  │       ▼                ▼                ▼                ▼                   │   │
│  │   ┌─────────┐      ┌─────────┐      ┌─────────┐      ┌─────────┐            │   │
│  │   │Feedback │      │Feedback │      │Feedback │      │Feedback │            │   │
│  │   │  Form   │      │  Form   │      │  Form   │      │  Form   │            │   │
│  │   └─────────┘      └─────────┘      └─────────┘      └─────────┘            │   │
│  │       │                │                │                │                   │   │
│  │       └────────────────┴────────────────┴────────────────┘                   │   │
│  │                                │                                              │   │
│  │                                ▼                                              │   │
│  │                      ┌─────────────────────┐                                  │   │
│  │                      │  DEBRIEF MEETING    │                                  │   │
│  │                      │  All interviewers   │                                  │   │
│  │                      │  discuss candidate  │                                  │   │
│  │                      └─────────────────────┘                                  │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  CONCURRENT PANEL FLOW:                                                             │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │                    PANEL INTERVIEW ROOM                              │    │   │
│  │   │                         90 minutes                                   │    │   │
│  │   │                                                                     │    │   │
│  │   │   ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐       │    │   │
│  │   │   │    HM     │  │ Director  │  │   HRBP    │  │ Technical │       │    │   │
│  │   │   │           │  │           │  │           │  │           │       │    │   │
│  │   │   └───────────┘  └───────────┘  └───────────┘  └───────────┘       │    │   │
│  │   │                                                                     │    │   │
│  │   │                      ┌───────────┐                                  │    │   │
│  │   │                      │ CANDIDATE │                                  │    │   │
│  │   │                      │           │                                  │    │   │
│  │   │                      └───────────┘                                  │    │   │
│  │   │                                                                     │    │   │
│  │   │   Interview Format:                                                 │    │   │
│  │   │   • Round-robin questions (each interviewer asks assigned topics)  │    │   │
│  │   │   • Structured competency assessment                                │    │   │
│  │   │   • Unified scorecard completion                                    │    │   │
│  │   │                                                                     │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 6.3 Interview Feedback Collection

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                     6.3 INTERVIEW FEEDBACK COLLECTION                                │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    STRUCTURED FEEDBACK FORM                                   │   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ INTERVIEW FEEDBACK - Warehouse Associate                            │    │   │
│  │   │                                                                     │    │   │
│  │   │ Candidate: John Smith                                               │    │   │
│  │   │ Interview Date: Dec 7, 2025                                         │    │   │
│  │   │ Interviewer: Jane Doe (Hiring Manager)                              │    │   │
│  │   │                                                                     │    │   │
│  │   │ ─────────────────────────────────────────────────────────────────── │    │   │
│  │   │                                                                     │    │   │
│  │   │ COMPETENCY RATINGS (1-5 scale)                                      │    │   │
│  │   │                                                                     │    │   │
│  │   │ Technical Skills                                                    │    │   │
│  │   │ ├── Equipment operation    [1] [2] [3] [●4] [5]                    │    │   │
│  │   │ ├── Safety awareness       [1] [2] [3] [4] [●5]                    │    │   │
│  │   │ └── Process knowledge      [1] [2] [●3] [4] [5]                    │    │   │
│  │   │                                                                     │    │   │
│  │   │ Soft Skills                                                         │    │   │
│  │   │ ├── Communication          [1] [2] [3] [●4] [5]                    │    │   │
│  │   │ ├── Teamwork               [1] [2] [3] [4] [●5]                    │    │   │
│  │   │ └── Problem solving        [1] [2] [3] [●4] [5]                    │    │   │
│  │   │                                                                     │    │   │
│  │   │ Cultural Fit                                                        │    │   │
│  │   │ ├── GEODIS values align    [1] [2] [3] [●4] [5]                    │    │   │
│  │   │ └── Team dynamics          [1] [2] [3] [4] [●5]                    │    │   │
│  │   │                                                                     │    │   │
│  │   │ ─────────────────────────────────────────────────────────────────── │    │   │
│  │   │                                                                     │    │   │
│  │   │ OVERALL RECOMMENDATION                                              │    │   │
│  │   │ ○ Strong Hire (proceed immediately)                                 │    │   │
│  │   │ ● Hire (recommend moving forward)                                   │    │   │
│  │   │ ○ Maybe (additional interview needed)                               │    │   │
│  │   │ ○ No Hire (do not recommend)                                        │    │   │
│  │   │                                                                     │    │   │
│  │   │ ─────────────────────────────────────────────────────────────────── │    │   │
│  │   │                                                                     │    │   │
│  │   │ STRENGTHS (required):                                               │    │   │
│  │   │ ┌─────────────────────────────────────────────────────────────┐    │    │   │
│  │   │ │ Strong safety awareness, excellent teamwork skills,         │    │    │   │
│  │   │ │ previous experience aligns well with role requirements.     │    │    │   │
│  │   │ └─────────────────────────────────────────────────────────────┘    │    │   │
│  │   │                                                                     │    │   │
│  │   │ AREAS OF CONCERN (if any):                                          │    │   │
│  │   │ ┌─────────────────────────────────────────────────────────────┐    │    │   │
│  │   │ │ Limited experience with WMS systems - training required.    │    │    │   │
│  │   │ └─────────────────────────────────────────────────────────────┘    │    │   │
│  │   │                                                                     │    │   │
│  │   │ [SUBMIT FEEDBACK]                                                   │    │   │
│  │   │                                                                     │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  FEEDBACK WORKFLOW:                                                                 │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   ┌───────────────┐    ┌───────────────┐    ┌───────────────┐                │   │
│  │   │  Interview    │    │   Feedback    │    │   Recruiter   │                │   │
│  │   │  Completed    │───▶│   Reminder    │───▶│   Aggregates  │                │   │
│  │   │               │    │   (24 hours)  │    │   Feedback    │                │   │
│  │   └───────────────┘    └───────────────┘    └───────────────┘                │   │
│  │                                                                               │   │
│  │   Feedback SLA:                                                               │   │
│  │   • Target: Within 24 hours of interview                                     │   │
│  │   • Escalation: Email reminder at 24 hours                                   │   │
│  │   • Second reminder: 48 hours                                                │   │
│  │   • Report to manager: 72 hours (overdue)                                    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  CONSOLIDATED FEEDBACK VIEW (Recruiter):                                            │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ Candidate: John Smith              Average Score: 4.2/5.0                   │    │
│  │                                                                              │    │
│  │ Interviewer       │ Rating │ Recommendation │ Feedback Status               │    │
│  │───────────────────┼────────┼────────────────┼─────────────────────────────  │    │
│  │ Jane Doe (HM)     │  4.3   │ Hire           │ ✓ Completed                   │    │
│  │ Bob Smith (Ops)   │  4.0   │ Hire           │ ✓ Completed                   │    │
│  │ Alice Chen (HRBP) │  4.5   │ Strong Hire    │ ✓ Completed                   │    │
│  │ Mike Wilson (Tech)│  4.0   │ Hire           │ ⏳ Pending                    │    │
│  │                                                                              │    │
│  │ CONSENSUS: PROCEED TO OFFER                                                 │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 6.4 Assessment Integration

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        6.4 ASSESSMENT INTEGRATION                                    │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    ASSESSMENT TYPES BY JOB FAMILY                             │   │
│  │                                                                               │   │
│  │   Job Family          Assessment Type         Provider        Duration        │   │
│  │   ──────────          ───────────────         ────────        ────────        │   │
│  │   Warehouse/Ops       Skills Test             Internal        30 min          │   │
│  │   Drivers             Driving Assessment      Third-party     60 min          │   │
│  │   IT/Technical        Coding Challenge        HackerRank      90 min          │   │
│  │   Sales               Sales Simulation        SalesForce      45 min          │   │
│  │   Finance             Excel/Analytics         Internal        60 min          │   │
│  │   Leadership          Personality/360         SHL             45 min          │   │
│  │   Customer Service    Scenario-based          Internal        30 min          │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ASSESSMENT WORKFLOW:                                                               │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   RECRUITER                  SYSTEM                    CANDIDATE              │   │
│  │   ─────────                  ──────                    ─────────              │   │
│  │       │                         │                           │                 │   │
│  │       │  1. Trigger assessment  │                           │                 │   │
│  │       │     for candidate       │                           │                 │   │
│  │       │────────────────────────▶│                           │                 │   │
│  │       │                         │                           │                 │   │
│  │       │                         │  2. Send assessment       │                 │   │
│  │       │                         │     invitation email      │                 │   │
│  │       │                         │     with unique link      │                 │   │
│  │       │                         │──────────────────────────▶│                 │   │
│  │       │                         │                           │                 │   │
│  │       │                         │                           │  3. Complete    │   │
│  │       │                         │                           │     assessment  │   │
│  │       │                         │                           │     (timed)     │   │
│  │       │                         │◀──────────────────────────│                 │   │
│  │       │                         │                           │                 │   │
│  │       │                         │  4. Auto-score results    │                 │   │
│  │       │                         │     (if applicable)       │                 │   │
│  │       │                         │                           │                 │   │
│  │       │◀────────────────────────│                           │                 │   │
│  │       │  5. Results available   │                           │                 │   │
│  │       │     in Oracle           │                           │                 │   │
│  │       │                         │                           │                 │   │
│  │       │  6. Review & decide     │                           │                 │   │
│  │       │     on next step        │                           │                 │   │
│  │       │                         │                           │                 │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ASSESSMENT RESULTS IN ORACLE:                                                      │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │ ASSESSMENT RESULTS - John Smith                                             │    │
│  │                                                                              │    │
│  │ Assessment: Warehouse Operations Skills Test                                 │    │
│  │ Completed: Dec 7, 2025 14:32                                                │    │
│  │ Duration: 28 minutes (max 30)                                               │    │
│  │                                                                              │    │
│  │ ┌─────────────────────────────────────────────────────────────────────┐     │    │
│  │ │ OVERALL SCORE: 82/100 (PASS)                      Threshold: 70     │     │    │
│  │ └─────────────────────────────────────────────────────────────────────┘     │    │
│  │                                                                              │    │
│  │ Section Breakdown:                                                          │    │
│  │ ├── Safety Protocols         │████████████████████│ 95%                    │    │
│  │ ├── Equipment Operation      │████████████████░░░░│ 80%                    │    │
│  │ ├── Inventory Management     │██████████████░░░░░░│ 70%                    │    │
│  │ └── Quality Control          │████████████████░░░░│ 85%                    │    │
│  │                                                                              │    │
│  │ Recommendation: PROCEED - Strong safety awareness, meets requirements       │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 7. Offer & Hire Workflows

### 7.1 Offer Creation Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                          7.1 OFFER CREATION FLOW                                     │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         OFFER DATA COLLECTION                                 │   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │ CREATE OFFER - Warehouse Associate                                  │    │   │
│  │   │                                                                     │    │   │
│  │   │ CANDIDATE INFORMATION (auto-populated)                              │    │   │
│  │   │ ├── Name: John Smith                                               │    │   │
│  │   │ ├── Email: john.smith@email.com                                    │    │   │
│  │   │ └── Phone: (555) 123-4567                                          │    │   │
│  │   │                                                                     │    │   │
│  │   │ POSITION DETAILS (from requisition)                                 │    │   │
│  │   │ ├── Job Title: Warehouse Associate                                 │    │   │
│  │   │ ├── Job Code: WHSE_ASSOC_001                                       │    │   │
│  │   │ ├── Department: Operations - Chicago DC                            │    │   │
│  │   │ ├── Location: Chicago, IL                                          │    │   │
│  │   │ ├── Legal Entity: GEODIS USA Inc.                                  │    │   │
│  │   │ ├── Reports To: Jane Doe (Operations Supervisor)                   │    │   │
│  │   │ └── Grade: G5                                                      │    │   │
│  │   │                                                                     │    │   │
│  │   │ COMPENSATION (recruiter enters)                                     │    │   │
│  │   │ ├── Base Salary: $42,000 annually                                  │    │   │
│  │   │ │   └── Range: $35,000 - $48,000 (within band ✓)                  │    │   │
│  │   │ ├── Pay Frequency: Bi-weekly                                       │    │   │
│  │   │ ├── Overtime Eligible: Yes (non-exempt)                            │    │   │
│  │   │ ├── Sign-on Bonus: $1,000                                          │    │   │
│  │   │ └── Relocation: Not applicable                                     │    │   │
│  │   │                                                                     │    │   │
│  │   │ BENEFITS (standard package auto-selected)                           │    │   │
│  │   │ ├── Health Insurance: GEODIS Standard Plan                         │    │   │
│  │   │ ├── 401(k): Eligible after 90 days                                 │    │   │
│  │   │ ├── PTO: 15 days annually                                          │    │   │
│  │   │ └── Other: Life insurance, disability                              │    │   │
│  │   │                                                                     │    │   │
│  │   │ START DATE                                                          │    │   │
│  │   │ ├── Proposed: January 6, 2026                                      │    │   │
│  │   │ └── Candidate Available: January 2, 2026                           │    │   │
│  │   │                                                                     │    │   │
│  │   │ CONTINGENCIES                                                       │    │   │
│  │   │ ├── ☑ Background check clearance                                   │    │   │
│  │   │ ├── ☑ Drug screening                                               │    │   │
│  │   │ ├── ☑ I-9 verification                                             │    │   │
│  │   │ └── ☐ Reference check (completed)                                  │    │   │
│  │   │                                                                     │    │   │
│  │   │ OFFER LETTER TEMPLATE                                               │    │   │
│  │   │ └── [GEODIS_US_STANDARD_OFFER ▼]                                   │    │   │
│  │   │                                                                     │    │   │
│  │   │ [PREVIEW OFFER LETTER]  [SUBMIT FOR APPROVAL]                       │    │   │
│  │   │                                                                     │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  OFFER LETTER TEMPLATES (18 Configured):                                            │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Country    │ Template Name              │ Use Case                        │    │
│  │   ──────────┼────────────────────────────┼─────────────────────────────────│    │
│  │   US         │ GEODIS_US_STANDARD         │ Standard offers                 │    │
│  │   US         │ GEODIS_US_EXEMPT           │ Exempt (salaried) positions     │    │
│  │   US         │ GEODIS_US_NONEXEMPT        │ Non-exempt (hourly) positions   │    │
│  │   US         │ GEODIS_US_EXECUTIVE        │ Executive/TOPEX positions       │    │
│  │   US         │ GEODIS_US_INTERN           │ Internship offers               │    │
│  │   France     │ GEODIS_FR_CDI              │ Permanent contract (CDI)        │    │
│  │   France     │ GEODIS_FR_CDD              │ Fixed-term contract (CDD)       │    │
│  │   France     │ GEODIS_FR_CADRE            │ Management positions            │    │
│  │   UK         │ GEODIS_UK_STANDARD         │ Standard UK offers              │    │
│  │   UK         │ GEODIS_UK_EXECUTIVE        │ UK executive positions          │    │
│  │   Germany    │ GEODIS_DE_STANDARD         │ Standard German offers          │    │
│  │   Germany    │ GEODIS_DE_TARIF            │ Collective agreement positions  │    │
│  │   Netherlands│ GEODIS_NL_STANDARD         │ Standard Dutch offers           │    │
│  │   ...        │ ...                        │ ...                             │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 7.2 Offer Approval Workflow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        7.2 OFFER APPROVAL WORKFLOW                                   │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    STANDARD OFFER APPROVAL CHAIN                              │   │
│  │                                                                               │   │
│  │   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐  │   │
│  │   │  RECRUITER  │    │   HIRING    │    │    COMP/    │    │    OFFER    │  │   │
│  │   │  Creates    │───▶│   MANAGER   │───▶│    HR       │───▶│   APPROVED  │  │   │
│  │   │  Offer      │    │  Approves   │    │  Validates  │    │             │  │   │
│  │   └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘  │   │
│  │                                                                               │   │
│  │   Standard Flow (Base < EUR 125K):                                           │   │
│  │   • Hiring Manager: Confirm candidate selection                              │   │
│  │   • Compensation/HR: Validate salary within band                             │   │
│  │   • Auto-approve if all conditions met                                       │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │              HIGH-VALUE OFFER APPROVAL (≥ EUR 125K Base OR ≥ EUR 155K Total)  │   │
│  │                                                                               │   │
│  │   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │   │
│  │   │  RECRUITER  │  │   HIRING    │  │    COMP/    │  │   EVP HR    │        │   │
│  │   │  Creates    │─▶│   MANAGER   │─▶│    HR       │─▶│  Approves   │        │   │
│  │   │  Offer      │  │  Approves   │  │  Validates  │  │             │        │   │
│  │   └─────────────┘  └─────────────┘  └─────────────┘  └──────┬──────┘        │   │
│  │                                                              │               │   │
│  │                                                              ▼               │   │
│  │                                                     ┌─────────────┐          │   │
│  │                                                     │    OFFER    │          │   │
│  │                                                     │   APPROVED  │          │   │
│  │                                                     └─────────────┘          │   │
│  │                                                                               │   │
│  │   High-Value Validation:                                                     │   │
│  │   • Internal equity analysis required                                        │   │
│  │   • Market data comparison                                                   │   │
│  │   • Budget impact assessment                                                 │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    TOPEX OFFER APPROVAL                                       │   │
│  │                                                                               │   │
│  │   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │   │
│  │   │  RECRUITER  │  │   HIRING    │  │   EVP HR    │  │    CHRO     │        │   │
│  │   │  Creates    │─▶│   MANAGER   │─▶│  Reviews    │─▶│  FINAL      │        │   │
│  │   │  Offer      │  │  Approves   │  │             │  │  APPROVAL   │        │   │
│  │   └─────────────┘  └─────────────┘  └─────────────┘  └──────┬──────┘        │   │
│  │                                                              │               │   │
│  │                                                              ▼               │   │
│  │                                                     ┌─────────────┐          │   │
│  │                                                     │    OFFER    │          │   │
│  │                                                     │   APPROVED  │          │   │
│  │                                                     └─────────────┘          │   │
│  │                                                                               │   │
│  │   TOPEX Additional Requirements:                                             │   │
│  │   • Executive compensation analysis                                          │   │
│  │   • Board notification (if CEO direct report)                                │   │
│  │   • Retention/non-compete clause review                                      │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  EMAIL APPROVAL OPTION:                                                             │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   ┌─────────────────────────────────────────────────────────────────────┐   │    │
│  │   │ From: Oracle Recruiting <noreply@geodis.com>                        │   │    │
│  │   │ To: John.Manager@geodis.com                                         │   │    │
│  │   │ Subject: Offer Approval Required - Warehouse Associate              │   │    │
│  │   │                                                                     │   │    │
│  │   │ An offer requires your approval:                                    │   │    │
│  │   │                                                                     │   │    │
│  │   │ Candidate: John Smith                                               │   │    │
│  │   │ Position: Warehouse Associate                                       │   │    │
│  │   │ Base Salary: $42,000                                                │   │    │
│  │   │ Start Date: January 6, 2026                                         │   │    │
│  │   │                                                                     │   │    │
│  │   │ [APPROVE]  [REJECT]  [VIEW DETAILS]                                 │   │    │
│  │   │                                                                     │   │    │
│  │   │ Click APPROVE to approve without logging in.                        │   │    │
│  │   └─────────────────────────────────────────────────────────────────────┘   │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 7.3 DocuSign E-Signature Integration

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    7.3 DOCUSIGN E-SIGNATURE INTEGRATION                              │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         DOCUSIGN WORKFLOW                                     │   │
│  │                                                                               │   │
│  │   ORACLE RECRUITING              DOCUSIGN                  CANDIDATE          │   │
│  │   ────────────────               ────────                  ─────────          │   │
│  │         │                           │                           │             │   │
│  │         │  1. Offer approved        │                           │             │   │
│  │         │     Generate PDF          │                           │             │   │
│  │         │──────────────────────────▶│                           │             │   │
│  │         │                           │                           │             │   │
│  │         │  Data sent:               │                           │             │   │
│  │         │  • Offer letter PDF       │                           │             │   │
│  │         │  • Candidate email        │                           │             │   │
│  │         │  • Signing fields         │                           │             │   │
│  │         │  • Expiry date (7 days)   │                           │             │   │
│  │         │                           │                           │             │   │
│  │         │                           │  2. Send signing          │             │   │
│  │         │                           │     invitation            │             │   │
│  │         │                           │──────────────────────────▶│             │   │
│  │         │                           │                           │             │   │
│  │         │                           │                           │  3. Review  │   │
│  │         │                           │                           │     & Sign  │   │
│  │         │                           │                           │     offer   │   │
│  │         │                           │◀──────────────────────────│             │   │
│  │         │                           │                           │             │   │
│  │         │  4. Webhook notification  │                           │             │   │
│  │         │     Signed document       │                           │             │   │
│  │         │◀──────────────────────────│                           │             │   │
│  │         │                           │                           │             │   │
│  │         │  5. Auto-update Oracle:   │                           │             │   │
│  │         │  • Offer status = Accepted│                           │             │   │
│  │         │  • Store signed PDF       │                           │             │   │
│  │         │  • Trigger hire process   │                           │             │   │
│  │         │                           │                           │             │   │
│  │         │  6. Confirmation emails   │──────────────────────────▶│             │   │
│  │         │     to all parties        │                           │             │   │
│  │         │                           │                           │             │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  DOCUSIGN ENVELOPE STRUCTURE:                                                       │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Envelope: GEODIS Offer Letter - John Smith                                │    │
│  │                                                                              │    │
│  │   Documents:                                                                 │    │
│  │   ├── 1. Offer Letter (main document)                                       │    │
│  │   ├── 2. Benefits Summary (attachment)                                      │    │
│  │   └── 3. At-Will Employment Notice (US only)                                │    │
│  │                                                                              │    │
│  │   Signing Fields:                                                            │    │
│  │   ├── Signature (page 3)                                                    │    │
│  │   ├── Date (page 3)                                                         │    │
│  │   ├── Printed Name (page 3)                                                 │    │
│  │   └── Initial (page 1 - acknowledgment)                                     │    │
│  │                                                                              │    │
│  │   Expiration: 7 days from send date                                         │    │
│  │   Reminders: Day 3, Day 5, Day 7 (final)                                    │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│  SIGNATURE STATUS IN ORACLE:                                                        │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Candidate: John Smith                                                      │    │
│  │   Offer Status: PENDING SIGNATURE                                           │    │
│  │                                                                              │    │
│  │   DocuSign Status:                                                          │    │
│  │   ├── Envelope ID: abc123-def456-ghi789                                     │    │
│  │   ├── Sent: Dec 7, 2025 10:30 AM                                            │    │
│  │   ├── Viewed: Dec 7, 2025 2:15 PM  ✓                                        │    │
│  │   ├── Signed: Pending                                                       │    │
│  │   └── Expires: Dec 14, 2025                                                 │    │
│  │                                                                              │    │
│  │   [RESEND]  [VOID & CREATE NEW]  [EXTEND DEADLINE]                          │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 7.4 Sterling Background Check Integration

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                  7.4 STERLING BACKGROUND CHECK INTEGRATION                           │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    BACKGROUND CHECK PACKAGES                                  │   │
│  │                                                                               │   │
│  │   Package Name           │ Checks Included              │ Region    │ SLA    │   │
│  │   ─────────────────────  │ ────────────────────         │ ──────    │ ───    │   │
│  │   GEODIS EXEMPT          │ SSN, Criminal, Employment,   │ US        │ 3-5d   │   │
│  │                          │ Education, Credit            │           │        │   │
│  │                                                                               │   │
│  │   GEODIS NON-EXEMPT      │ SSN, Criminal, Employment    │ US        │ 2-3d   │   │
│  │                                                                               │   │
│  │   GEODIS DRIVER          │ SSN, Criminal, MVR, Drug,    │ US        │ 3-5d   │   │
│  │                          │ DOT Physical                 │           │        │   │
│  │                                                                               │   │
│  │   GEODIS EXECUTIVE       │ Full package + Media search, │ US        │ 5-7d   │   │
│  │                          │ Civil litigation             │           │        │   │
│  │                                                                               │   │
│  │   GEODIS EU STANDARD     │ Criminal (country-specific), │ EU        │ 5-10d  │   │
│  │                          │ Right to work                │           │        │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  INTEGRATION WORKFLOW:                                                              │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   ORACLE                     STERLING                    CANDIDATE            │   │
│  │   ──────                     ────────                    ─────────            │   │
│  │      │                          │                            │                │   │
│  │      │  1. Initiate BGC         │                            │                │   │
│  │      │     (Recruiter clicks    │                            │                │   │
│  │      │      "Request Check")    │                            │                │   │
│  │      │─────────────────────────▶│                            │                │   │
│  │      │                          │                            │                │   │
│  │      │  Data sent via API:      │                            │                │   │
│  │      │  • Candidate name        │                            │                │   │
│  │      │  • Email                 │                            │                │   │
│  │      │  • SSN (encrypted)       │                            │                │   │
│  │      │  • Package type          │                            │                │   │
│  │      │  • Position/location     │                            │                │   │
│  │      │                          │                            │                │   │
│  │      │                          │  2. Send candidate         │                │   │
│  │      │                          │     consent form           │                │   │
│  │      │                          │───────────────────────────▶│                │   │
│  │      │                          │                            │                │   │
│  │      │                          │                            │  3. Complete   │   │
│  │      │                          │                            │     consent    │   │
│  │      │                          │◀───────────────────────────│     & info     │   │
│  │      │                          │                            │                │   │
│  │      │                          │  4. Process checks         │                │   │
│  │      │                          │     (3-7 days)             │                │   │
│  │      │                          │                            │                │   │
│  │      │  5. Results webhook      │                            │                │   │
│  │      │◀─────────────────────────│                            │                │   │
│  │      │                          │                            │                │   │
│  │      │  6. Update candidate     │                            │                │   │
│  │      │     status in Oracle     │                            │                │   │
│  │      │                          │                            │                │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  RESULTS HANDLING:                                                                  │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Result          │ Oracle Action                  │ Next Step              │    │
│  │   ──────          │ ─────────────                  │ ─────────              │    │
│  │   CLEAR           │ Auto-update: BGC Passed        │ Proceed to hire        │    │
│  │   CONSIDER        │ Alert recruiter for review     │ Manual decision        │    │
│  │   FAIL            │ Auto-update: BGC Failed        │ Rescind offer process  │    │
│  │   PENDING         │ Status: In Progress            │ Wait for completion    │    │
│  │                                                                              │    │
│  │   Adjudication (CONSIDER results):                                          │    │
│  │   • Recruiter reviews Sterling report                                       │    │
│  │   • HRBP consultation (required)                                            │    │
│  │   • Legal review (if criminal record)                                       │    │
│  │   • Decision documented in Oracle                                           │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 7.5 Hire to Core HR Workflow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                       7.5 HIRE TO CORE HR WORKFLOW                                   │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  TRIGGER: Offer accepted + All contingencies cleared                                │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         HIRE PROCESS FLOW                                     │   │
│  │                                                                               │   │
│  │   ORACLE RECRUITING              ORACLE CORE HR            ONBOARDING        │   │
│  │   ────────────────               ──────────────            ──────────        │   │
│  │         │                              │                        │            │   │
│  │         │  1. "Hire" action            │                        │            │   │
│  │         │     triggered                │                        │            │   │
│  │         │─────────────────────────────▶│                        │            │   │
│  │         │                              │                        │            │   │
│  │         │  Data transferred:           │                        │            │   │
│  │         │  ┌───────────────────────────────────────────────┐   │            │   │
│  │         │  │ PERSONAL                                      │   │            │   │
│  │         │  │ • Name, DOB, Gender                           │   │            │   │
│  │         │  │ • Address, Phone, Email                       │   │            │   │
│  │         │  │ • SSN/National ID                             │   │            │   │
│  │         │  │ • Emergency contact                           │   │            │   │
│  │         │  │                                               │   │            │   │
│  │         │  │ EMPLOYMENT                                    │   │            │   │
│  │         │  │ • Job code, title, grade                      │   │            │   │
│  │         │  │ • Legal entity, BU, department                │   │            │   │
│  │         │  │ • Location, cost center                       │   │            │   │
│  │         │  │ • Manager (reports to)                        │   │            │   │
│  │         │  │ • Start date, worker type                     │   │            │   │
│  │         │  │                                               │   │            │   │
│  │         │  │ COMPENSATION                                  │   │            │   │
│  │         │  │ • Base salary, currency                       │   │            │   │
│  │         │  │ • Pay frequency                               │   │            │   │
│  │         │  │ • Bonus eligibility                           │   │            │   │
│  │         │  └───────────────────────────────────────────────┘   │            │   │
│  │         │                              │                        │            │   │
│  │         │                              │  2. Create pending     │            │   │
│  │         │                              │     worker record      │            │   │
│  │         │                              │     (future-dated)     │            │   │
│  │         │                              │                        │            │   │
│  │         │                              │  3. Trigger            │            │   │
│  │         │                              │     onboarding         │            │   │
│  │         │                              │────────────────────────▶            │   │
│  │         │                              │                        │            │   │
│  │         │                              │                        │ 4. Launch  │   │
│  │         │                              │                        │    journey │   │
│  │         │                              │                        │            │   │
│  │         │◀─────────────────────────────│◀───────────────────────│            │   │
│  │         │  5. Update: Hired            │  Employee ID assigned  │            │   │
│  │         │                              │                        │            │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  PRE-HIRE CHECKLIST (Auto-validated):                                               │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   ☑ Offer letter signed (DocuSign)                                          │    │
│  │   ☑ Background check cleared (Sterling)                                     │    │
│  │   ☑ References verified (if required)                                       │    │
│  │   ☑ Drug test passed (if required)                                          │    │
│  │   ☑ I-9 documents collected (US)                                            │    │
│  │   ☑ Work authorization verified                                             │    │
│  │   ☐ New hire paperwork completed (onboarding)                               │    │
│  │                                                                              │    │
│  │   [CREATE EMPLOYEE RECORD]                                                   │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
│  ONBOARDING JOURNEY TRIGGER:                                                        │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   New Hire: John Smith                                                       │    │
│  │   Start Date: January 6, 2026                                               │    │
│  │   Journey Assigned: GEODIS_US_WAREHOUSE_ONBOARD                             │    │
│  │                                                                              │    │
│  │   Pre-Day 1 Tasks:                                                          │    │
│  │   ├── Complete I-9 form                          Due: Dec 20               │    │
│  │   ├── Direct deposit setup                       Due: Dec 23               │    │
│  │   ├── Benefits enrollment                        Due: Dec 30               │    │
│  │   ├── Review employee handbook                   Due: Jan 3                │    │
│  │   └── Complete safety training (online)          Due: Jan 3                │    │
│  │                                                                              │    │
│  │   Day 1 Tasks:                                                              │    │
│  │   ├── Badge pickup                                                         │    │
│  │   ├── IT equipment collection                                              │    │
│  │   ├── Manager meet & greet                                                 │    │
│  │   └── Team introduction                                                    │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 7.6 Offer Decline & Renegotiation

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    7.6 OFFER DECLINE & RENEGOTIATION                                 │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    OFFER RESPONSE SCENARIOS                                   │   │
│  │                                                                               │   │
│  │   ┌─────────────────────────────────────────────────────────────────────┐    │   │
│  │   │                                                                     │    │   │
│  │   │   OFFER EXTENDED                                                    │    │   │
│  │   │        │                                                            │    │   │
│  │   │        ├──────────────┬──────────────┬──────────────┐              │    │   │
│  │   │        │              │              │              │              │    │   │
│  │   │        ▼              ▼              ▼              ▼              │    │   │
│  │   │   ┌────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐         │    │   │
│  │   │   │ACCEPTED│    │ DECLINED│    │NEGOTIATE│    │ EXPIRED │         │    │   │
│  │   │   └───┬────┘    └────┬────┘    └────┬────┘    └────┬────┘         │    │   │
│  │   │       │              │              │              │              │    │   │
│  │   │       ▼              ▼              ▼              ▼              │    │   │
│  │   │   Proceed to     Reason for     Counter-      Reopen or           │    │   │
│  │   │   Hire           decline?       offer?        withdraw?           │    │   │
│  │   │                                                                     │    │   │
│  │   └─────────────────────────────────────────────────────────────────────┘    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  DECLINE WORKFLOW:                                                                  │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   Candidate declines offer                                                    │   │
│  │        │                                                                      │   │
│  │        ▼                                                                      │   │
│  │   ┌────────────────────────────────────────────────────────────────┐         │   │
│  │   │ DECLINE REASON (required)                                      │         │   │
│  │   │ ○ Accepted another offer                                       │         │   │
│  │   │ ○ Compensation too low                                         │         │   │
│  │   │ ○ Location/commute                                             │         │   │
│  │   │ ○ Role not as expected                                         │         │   │
│  │   │ ○ Counter-offer from current employer                          │         │   │
│  │   │ ○ Personal reasons                                             │         │   │
│  │   │ ○ Other (specify)                                              │         │   │
│  │   └────────────────────────────────────────────────────────────────┘         │   │
│  │        │                                                                      │   │
│  │        ▼                                                                      │   │
│  │   Actions:                                                                    │   │
│  │   • Void DocuSign envelope (if pending)                                      │   │
│  │   • Update offer status = DECLINED                                           │   │
│  │   • Notify recruiter & hiring manager                                        │   │
│  │   • Option: Add to Silver Medalist pool                                      │   │
│  │   • Option: Reopen requisition                                               │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  NEGOTIATION WORKFLOW:                                                              │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   Candidate requests negotiation                                              │   │
│  │        │                                                                      │   │
│  │        ▼                                                                      │   │
│  │   ┌────────────────────────────────────────────────────────────────┐         │   │
│  │   │ COUNTER-OFFER DETAILS                                          │         │   │
│  │   │                                                                 │         │   │
│  │   │ Original Offer:         Counter-Request:                       │         │   │
│  │   │ Base: $42,000           Base: $48,000                          │         │   │
│  │   │ Sign-on: $1,000         Sign-on: $3,000                        │         │   │
│  │   │ Start: Jan 6            Start: Jan 13                          │         │   │
│  │   │                                                                 │         │   │
│  │   │ Candidate Notes: "Need higher base to match current salary"    │         │   │
│  │   └────────────────────────────────────────────────────────────────┘         │   │
│  │        │                                                                      │   │
│  │        ▼                                                                      │   │
│  │   Recruiter reviews with Hiring Manager                                       │   │
│  │        │                                                                      │   │
│  │        ├──────────────────┬──────────────────┐                               │   │
│  │        │                  │                  │                               │   │
│  │        ▼                  ▼                  ▼                               │   │
│  │   ┌─────────┐       ┌──────────┐      ┌──────────┐                           │   │
│  │   │ ACCEPT  │       │  MODIFY  │      │ DECLINE  │                           │   │
│  │   │ COUNTER │       │ & COUNTER│      │ COUNTER  │                           │   │
│  │   └────┬────┘       └────┬─────┘      └────┬─────┘                           │   │
│  │        │                 │                 │                                 │   │
│  │        ▼                 ▼                 ▼                                 │   │
│  │   New offer =       Send revised      Maintain original                      │   │
│  │   $48K + $3K        offer: $45K       or withdraw                            │   │
│  │   (re-approval      + $2,000                                                 │   │
│  │   if threshold)                                                              │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 8. Integration & System Flows

### 8.1 Integration Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                      8.1 INTEGRATION ARCHITECTURE OVERVIEW                           │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         SYSTEM LANDSCAPE                                      │   │
│  │                                                                               │   │
│  │                          ┌─────────────────────┐                              │   │
│  │                          │   ORACLE FUSION     │                              │   │
│  │                          │   HCM CLOUD         │                              │   │
│  │                          │                     │                              │   │
│  │                          │ ┌─────────────────┐ │                              │   │
│  │                          │ │   RECRUITING    │ │                              │   │
│  │                          │ │   (IRC)         │ │                              │   │
│  │                          │ └────────┬────────┘ │                              │   │
│  │                          │          │          │                              │   │
│  │                          │ ┌────────▼────────┐ │                              │   │
│  │                          │ │   CORE HR       │ │                              │   │
│  │                          │ │   (HCM)         │ │                              │   │
│  │                          │ └────────┬────────┘ │                              │   │
│  │                          │          │          │                              │   │
│  │                          │ ┌────────▼────────┐ │                              │   │
│  │                          │ │  ONBOARDING     │ │                              │   │
│  │                          │ └─────────────────┘ │                              │   │
│  │                          └──────────┬──────────┘                              │   │
│  │                                     │                                         │   │
│  │      ┌──────────────────────────────┼──────────────────────────────┐         │   │
│  │      │                              │                              │         │   │
│  │      ▼                              ▼                              ▼         │   │
│  │  ┌────────┐                   ┌──────────┐                   ┌──────────┐    │   │
│  │  │ JOB    │                   │ BACKGROUND│                  │ E-SIGN   │    │   │
│  │  │ BOARDS │                   │ CHECK     │                  │          │    │   │
│  │  ├────────┤                   ├──────────┤                   ├──────────┤    │   │
│  │  │Indeed  │                   │ Sterling │                   │ DocuSign │    │   │
│  │  │LinkedIn│                   │ (US)     │                   │          │    │   │
│  │  │Broadbn │                   │ Certn    │                   │          │    │   │
│  │  └────────┘                   │ (EU)     │                   └──────────┘    │   │
│  │                               └──────────┘                                    │   │
│  │                                                                               │   │
│  │      ▼                              ▼                              ▼         │   │
│  │  ┌────────┐                   ┌──────────┐                   ┌──────────┐    │   │
│  │  │ MDM    │                   │ CALENDAR │                   │ASSESSMENT│    │   │
│  │  │ (EBX)  │                   │          │                   │          │    │   │
│  │  ├────────┤                   ├──────────┤                   ├──────────┤    │   │
│  │  │Org     │                   │ Microsoft│                   │HackerRank│    │   │
│  │  │Structure│                  │ Outlook  │                   │ SHL      │    │   │
│  │  │Sync    │                   │ Teams    │                   │          │    │   │
│  │  └────────┘                   └──────────┘                   └──────────┘    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 8.2 Integration Summary Table

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        8.2 INTEGRATION SUMMARY TABLE                                 │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │ Integration     │ Direction  │ Method   │ Frequency │ Data Flow              │   │
│  │ ─────────────── │ ────────── │ ──────── │ ───────── │ ─────────────────────  │   │
│  │                 │            │          │           │                        │   │
│  │ Indeed          │ Bi-dir     │ REST API │ Real-time │ Jobs out, Apps in      │   │
│  │ LinkedIn        │ Bi-dir     │ REST API │ Real-time │ Jobs out, Apps in      │   │
│  │ Broadbean       │ Outbound   │ API      │ Real-time │ Multi-post to boards   │   │
│  │ Sterling        │ Bi-dir     │ REST API │ Real-time │ Check request/results  │   │
│  │ DocuSign        │ Bi-dir     │ REST API │ Real-time │ Offer send/signed      │   │
│  │ Oracle Core HR  │ Native     │ Internal │ Real-time │ Hire creates employee  │   │
│  │ MDM (EBX)       │ Inbound    │ File/API │ Daily     │ Org structure sync     │   │
│  │ MS Outlook      │ Bi-dir     │ Graph API│ Real-time │ Calendar/scheduling    │   │
│  │ MS Teams        │ Outbound   │ Graph API│ Real-time │ Meeting link creation  │   │
│  │ Assessment      │ Bi-dir     │ REST API │ On-demand │ Test request/results   │   │
│  │                 │            │          │           │                        │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  INTEGRATION PRIORITY:                                                              │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Priority 1 (Go-Live Required):                                            │    │
│  │   ├── Oracle Career Site (Internal + External)                              │    │
│  │   ├── Indeed API (60-73% of applications)                                   │    │
│  │   ├── LinkedIn API                                                          │    │
│  │   ├── Sterling Background Check                                             │    │
│  │   ├── DocuSign E-Signature                                                  │    │
│  │   └── Oracle Core HR (native)                                               │    │
│  │                                                                              │    │
│  │   Priority 2 (Phase 2):                                                     │    │
│  │   ├── Broadbean Multi-Posting                                               │    │
│  │   ├── MS Outlook Calendar Integration                                       │    │
│  │   └── MS Teams Meeting Links                                                │    │
│  │                                                                              │    │
│  │   Priority 3 (Future):                                                      │    │
│  │   ├── Assessment Tools (HackerRank, SHL)                                    │    │
│  │   ├── AI Chatbot (Paradox or Oracle Assistant)                              │    │
│  │   └── Video Interview Platform                                              │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 8.3 MDM/EBX Organization Sync

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                       8.3 MDM/EBX ORGANIZATION SYNC                                  │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  PURPOSE: Keep Oracle HCM organization structure synchronized with master data      │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         SYNC WORKFLOW                                         │   │
│  │                                                                               │   │
│  │   EBX (MDM)                   OIC                        ORACLE HCM          │   │
│  │   ────────                    ───                        ──────────          │   │
│  │       │                        │                              │              │   │
│  │       │  1. Daily extract      │                              │              │   │
│  │       │     (2:00 AM EST)      │                              │              │   │
│  │       │───────────────────────▶│                              │              │   │
│  │       │                        │                              │              │   │
│  │       │  Data:                 │                              │              │   │
│  │       │  • Legal entities      │                              │              │   │
│  │       │  • Business units      │                              │              │   │
│  │       │  • Departments         │                              │              │   │
│  │       │  • Locations           │                              │              │   │
│  │       │  • Cost centers        │                              │              │   │
│  │       │                        │                              │              │   │
│  │       │                        │  2. Transform & validate     │              │   │
│  │       │                        │     (HDL format)             │              │   │
│  │       │                        │                              │              │   │
│  │       │                        │  3. Load to Oracle           │              │   │
│  │       │                        │────────────────────────────▶ │              │   │
│  │       │                        │                              │              │   │
│  │       │                        │                              │  4. Update   │   │
│  │       │                        │                              │     org      │   │
│  │       │                        │                              │     tables   │   │
│  │       │                        │                              │              │   │
│  │       │                        │  5. Sync confirmation        │              │   │
│  │       │                        │◀──────────────────────────── │              │   │
│  │       │                        │                              │              │   │
│  │       │◀───────────────────────│  6. Status report            │              │   │
│  │       │                        │                              │              │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  DATA VOLUMES:                                                                      │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Object               │ Records  │ Update Frequency │ Impact on Recruiting │    │
│  │   ────────────────────────────────────────────────────────────────────────  │    │
│  │   Legal Entity         │ 364      │ Monthly          │ Offer letter entity  │    │
│  │   Business Unit        │ 2,175    │ Weekly           │ Requisition BU       │    │
│  │   Department           │ 10,803   │ Daily            │ Requisition dept     │    │
│  │   Location             │ 919      │ Weekly           │ Job posting location │    │
│  │   Cost Center          │ ~5,000   │ Monthly          │ Budget tracking      │    │
│  │   Job Code             │ 688      │ Monthly          │ Requisition job code │    │
│  │   Position             │ Dynamic  │ Real-time        │ Vacancy management   │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 8.4 Recruiting to Core HR Data Flow

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                    8.4 RECRUITING TO CORE HR DATA FLOW                               │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         DATA MAPPING                                          │   │
│  │                                                                               │   │
│  │   RECRUITING OBJECT          CORE HR OBJECT            NOTES                 │   │
│  │   ─────────────────          ──────────────            ─────                 │   │
│  │                                                                               │   │
│  │   REQUISITION                                                                 │   │
│  │   ├── Job Code           →   Assignment.JobId          Lookup                │   │
│  │   ├── Job Title          →   Assignment.JobName        Direct                │   │
│  │   ├── Grade              →   Assignment.GradeId        Lookup                │   │
│  │   ├── Legal Entity       →   Assignment.LegalEntity    Lookup                │   │
│  │   ├── Business Unit      →   Assignment.BusinessUnit   Lookup                │   │
│  │   ├── Department         →   Assignment.DepartmentId   Lookup                │   │
│  │   ├── Location           →   Assignment.LocationId     Lookup                │   │
│  │   ├── Manager            →   Assignment.ManagerId      Person lookup         │   │
│  │   └── Cost Center        →   Assignment.CostCenter     Lookup                │   │
│  │                                                                               │   │
│  │   CANDIDATE                                                                   │   │
│  │   ├── First Name         →   Person.FirstName          Direct                │   │
│  │   ├── Last Name          →   Person.LastName           Direct                │   │
│  │   ├── Email              →   Person.WorkEmail          Direct                │   │
│  │   ├── Phone              →   Person.PhoneNumber        Direct                │   │
│  │   ├── Address            →   Address.AddressLine1      Direct                │   │
│  │   ├── City               →   Address.City              Direct                │   │
│  │   ├── State              →   Address.Region            Lookup                │   │
│  │   ├── Country            →   Address.Country           Lookup                │   │
│  │   └── Postal Code        →   Address.PostalCode        Direct                │   │
│  │                                                                               │   │
│  │   OFFER                                                                       │   │
│  │   ├── Base Salary        →   Salary.Amount             Direct                │   │
│  │   ├── Currency           →   Salary.Currency           Direct                │   │
│  │   ├── Pay Frequency      →   Salary.PayFrequency       Lookup                │   │
│  │   ├── Start Date         →   Assignment.StartDate      Direct                │   │
│  │   └── Worker Type        →   Person.WorkerType         Lookup                │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  HIRE ACTION SEQUENCE:                                                              │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                                                                              │    │
│  │   Step │ Action                              │ Result                        │    │
│  │   ─────┼─────────────────────────────────────┼─────────────────────────────  │    │
│  │   1    │ Recruiter clicks "Hire"             │ Validate all contingencies   │    │
│  │   2    │ System creates Person record        │ Person ID generated          │    │
│  │   3    │ System creates Work Relationship    │ Employment record created    │    │
│  │   4    │ System creates Assignment           │ Job assignment created       │    │
│  │   5    │ System creates Salary record        │ Compensation set up          │    │
│  │   6    │ System triggers Onboarding          │ Journey assigned             │    │
│  │   7    │ Employee ID assigned                │ Returned to Recruiting       │    │
│  │   8    │ Candidate status = HIRED            │ Requisition count updated    │    │
│  │                                                                              │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 9. RACI Matrix & Governance

### 9.1 RACI Matrix by Process

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                         9.1 RACI MATRIX BY PROCESS                                   │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  R = Responsible | A = Accountable | C = Consulted | I = Informed                   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │ PROCESS               │ HM │ Recr │ HRBP │ Comp │ EVP │ CHRO │ Cand │        │   │
│  │ ─────────────────────────────────────────────────────────────────────────────│   │
│  │                       │    │      │      │      │     │      │      │        │   │
│  │ REQUISITION           │    │      │      │      │     │      │      │        │   │
│  │ Create requisition    │ R  │  C   │  C   │  -   │  -  │  -   │  -   │        │   │
│  │ Approve requisition   │ A  │  -   │  R   │  -   │  C  │  C   │  -   │        │   │
│  │ Approve high-salary   │ R  │  -   │  R   │  C   │  A  │  -   │  -   │        │   │
│  │ Approve TOPEX         │ R  │  -   │  -   │  -   │  -  │  A   │  -   │        │   │
│  │                       │    │      │      │      │     │      │      │        │   │
│  │ POSTING               │    │      │      │      │     │      │      │        │   │
│  │ Create job posting    │ C  │  R   │  I   │  -   │  -  │  -   │  -   │        │   │
│  │ Approve urgent post   │ R  │  C   │  A   │  -   │  -  │  -   │  -   │        │   │
│  │ Multi-channel posting │ I  │  R   │  -   │  -   │  -  │  -   │  -   │        │   │
│  │                       │    │      │      │      │     │      │      │        │   │
│  │ SOURCING              │    │      │      │      │     │      │      │        │   │
│  │ Review applications   │ C  │  R   │  -   │  -   │  -  │  -   │  -   │        │   │
│  │ Screen candidates     │ I  │  R   │  -   │  -   │  -  │  -   │  R   │        │   │
│  │ Manage talent pools   │ -  │  R   │  -   │  -   │  -  │  -   │  -   │        │   │
│  │                       │    │      │      │      │     │      │      │        │   │
│  │ INTERVIEW             │    │      │      │      │     │      │      │        │   │
│  │ Schedule interviews   │ C  │  R   │  -   │  -   │  -  │  -   │  R   │        │   │
│  │ Conduct interviews    │ R  │  C   │  C   │  -   │  -  │  -   │  R   │        │   │
│  │ Provide feedback      │ R  │  A   │  R   │  -   │  -  │  -   │  -   │        │   │
│  │ Make hire decision    │ A  │  R   │  C   │  -   │  -  │  -   │  -   │        │   │
│  │                       │    │      │      │      │     │      │      │        │   │
│  │ OFFER                 │    │      │      │      │     │      │      │        │   │
│  │ Create offer          │ C  │  R   │  -   │  C   │  -  │  -   │  -   │        │   │
│  │ Approve standard      │ A  │  R   │  -   │  R   │  -  │  -   │  -   │        │   │
│  │ Approve high-value    │ R  │  C   │  C   │  R   │  A  │  -   │  -   │        │   │
│  │ Approve TOPEX offer   │ R  │  C   │  -   │  R   │  R  │  A   │  -   │        │   │
│  │ Extend offer          │ I  │  R   │  -   │  -   │  -  │  -   │  R   │        │   │
│  │ Negotiate offer       │ C  │  R   │  -   │  C   │  -  │  -   │  R   │        │   │
│  │                       │    │      │      │      │     │      │      │        │   │
│  │ HIRE                  │    │      │      │      │     │      │      │        │   │
│  │ Background check      │ I  │  R   │  -   │  -   │  -  │  -   │  R   │        │   │
│  │ Complete hire         │ I  │  R   │  I   │  I   │  -  │  -   │  I   │        │   │
│  │ Trigger onboarding    │ -  │  R   │  -   │  -   │  -  │  -   │  R   │        │   │
│  │                       │    │      │      │      │     │      │      │        │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  LEGEND:                                                                            │
│  HM = Hiring Manager | Recr = Recruiter | HRBP = HR Business Partner               │
│  Comp = Compensation | EVP = EVP HR | CHRO = Chief HR Officer | Cand = Candidate   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 9.2 Approval Thresholds Summary

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                      9.2 APPROVAL THRESHOLDS SUMMARY                                 │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    REQUISITION APPROVAL THRESHOLDS                            │   │
│  │                                                                               │   │
│  │   Condition                      │ Approval Chain                            │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   Standard requisition           │ Hiring Manager → N+1 → HRBP              │   │
│  │   High salary (≥EUR 125K)        │ HM → N+1 → HRBP → EVP HR                 │   │
│  │   TOPEX position                 │ HM → N+1 → CHRO                          │   │
│  │   Not budgeted                   │ + Finance approval                        │   │
│  │   Agency requisition             │ + Regional HRD approval                   │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    OFFER APPROVAL THRESHOLDS                                  │   │
│  │                                                                               │   │
│  │   Condition                      │ Approval Chain                            │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   Standard offer                 │ Hiring Manager → Compensation/HR          │   │
│  │   Base ≥ EUR 125,000             │ HM → Comp → EVP HR                        │   │
│  │   Total comp ≥ EUR 155,000       │ HM → Comp → EVP HR                        │   │
│  │   TOPEX offer                    │ HM → EVP HR → CHRO                        │   │
│  │   Sign-on bonus > $10,000        │ + Finance approval                        │   │
│  │   Relocation > $25,000           │ + Finance approval                        │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    SLA TARGETS                                                │   │
│  │                                                                               │   │
│  │   Process Step                   │ SLA Target    │ Escalation                │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   Requisition approval           │ 3 days        │ N+1 at day 4              │   │
│  │   Application review             │ 5 days        │ Manager at day 6          │   │
│  │   Interview feedback             │ 24 hours      │ HR at 48 hours            │   │
│  │   Offer approval                 │ 2 days        │ EVP at day 3              │   │
│  │   Background check               │ 5 days        │ Recruiter at day 6        │   │
│  │   Candidate response to offer    │ 7 days        │ Recruiter at day 5        │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 10. KPIs & Metrics

### 10.1 Recruiting KPIs Dashboard

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        10.1 RECRUITING KPIs DASHBOARD                                │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    EFFICIENCY METRICS                                         │   │
│  │                                                                               │   │
│  │   KPI                        │ Calculation                    │ Target       │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   Time to Fill               │ Approval date → Hire date      │ Reduce       │   │
│  │   Time to Publish            │ Request date → First posting   │ < 3 days     │   │
│  │   Time to Review             │ Application → First review     │ < 5 days     │   │
│  │   Time to Interview          │ Review → First interview       │ < 10 days    │   │
│  │   Time to Offer              │ Final interview → Offer sent   │ < 5 days     │   │
│  │   Time to Accept             │ Offer sent → Offer accepted    │ < 7 days     │   │
│  │   Time to Start              │ Offer accepted → Start date    │ < 30 days    │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    QUALITY METRICS                                            │   │
│  │                                                                               │   │
│  │   KPI                        │ Calculation                    │ Target       │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   Offer Acceptance Rate      │ Accepted / Extended            │ > 85%        │   │
│  │   Interview-to-Offer Ratio   │ Offers / Interviews            │ > 25%        │   │
│  │   Application-to-Hire Ratio  │ Hires / Applications           │ 3-10%        │   │
│  │   Quality of Hire            │ Performance rating at 6 months │ > 3.5/5      │   │
│  │   Short-term Turnover        │ Left < 12 months / Hired       │ < 15%        │   │
│  │   Hiring Manager Satisfaction│ Survey score                   │ > 4.0/5      │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    SOURCE EFFECTIVENESS                                       │   │
│  │                                                                               │   │
│  │   KPI                        │ Calculation                    │ Target       │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   Source Mix                 │ Applications by source         │ Balanced     │   │
│  │   Source-to-Hire Rate        │ Hires by source / Apps         │ Track        │   │
│  │   Internal Fill Rate         │ Internal hires / Total hires   │ > 30%        │   │
│  │   Referral Rate              │ Referral hires / Total hires   │ > 20%        │   │
│  │   Cost per Source            │ Spend / Applications           │ Optimize     │   │
│  │   Cost per Hire              │ Total spend / Hires            │ Reduce       │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    DIVERSITY METRICS                                          │   │
│  │                                                                               │   │
│  │   KPI                        │ Calculation                    │ Target       │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   Gender Diversity           │ Female applicants/hires %      │ Track        │   │
│  │   Diversity at Each Stage    │ Diverse candidates by phase    │ No drop-off  │   │
│  │   Disability Representation  │ Self-identified %              │ Track        │   │
│  │   Veteran Hiring             │ Veteran hires %                │ Track        │   │
│  │   EEO Compliance (US)        │ OFCCP metrics                  │ 100%         │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 10.2 OTBI Reports Required

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        10.2 OTBI REPORTS REQUIRED                                    │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   Report Name               │ Metrics                        │ Audience      │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │                             │                                │               │   │
│  │   Recruiting Dashboard      │ Open reqs, pipeline,           │ TA Leadership │   │
│  │                             │ time-to-fill, YTD hires        │               │   │
│  │                             │                                │               │   │
│  │   Recruiter Workload        │ Assigned reqs, candidates      │ Recruiters    │   │
│  │                             │ per phase, activity metrics    │               │   │
│  │                             │                                │               │   │
│  │   Source Effectiveness      │ Applications by source,        │ TA Leadership │   │
│  │                             │ conversion rate, cost          │               │   │
│  │                             │                                │               │   │
│  │   Time-to-Hire Analysis     │ Days per phase, bottleneck     │ HR Leadership │   │
│  │                             │ analysis, trend                │               │   │
│  │                             │                                │               │   │
│  │   Diversity Report          │ Gender, disability by stage    │ HR/Compliance │   │
│  │                             │ EEOC data (US)                 │               │   │
│  │                             │                                │               │   │
│  │   Cost per Hire             │ Agency fees, job board spend   │ Finance/HR    │   │
│  │                             │ total cost breakdown           │               │   │
│  │                             │                                │               │   │
│  │   Hiring Manager Report     │ Requisitions by manager,       │ Managers      │   │
│  │                             │ time-to-fill, candidates       │               │   │
│  │                             │                                │               │   │
│  │   Offer Analysis            │ Offers extended/accepted,      │ Compensation  │   │
│  │                             │ decline reasons, salary data   │               │   │
│  │                             │                                │               │   │
│  │   Pipeline Report           │ Candidates by phase/state,     │ Recruiters    │   │
│  │                             │ aging, next actions            │               │   │
│  │                             │                                │               │   │
│  │   Compliance Report         │ Background check status,       │ Compliance    │   │
│  │                             │ I-9 completion, EEO filing     │               │   │
│  │                             │                                │               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 11. Appendices

### 11.1 Candidate Source Codes

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                        11.1 CANDIDATE SOURCE CODES                                   │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                    17 CONFIGURED SOURCES                                      │   │
│  │                                                                               │   │
│  │   Code         │ Source Name              │ Type           │ Cost Model      │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   INDEED       │ Indeed                   │ Job Board      │ CPC             │   │
│  │   LINKEDIN     │ LinkedIn                 │ Job Board      │ Premium         │   │
│  │   CAREER_INT   │ Career Site (Internal)   │ Direct         │ Free            │   │
│  │   CAREER_EXT   │ Career Site (External)   │ Direct         │ Free            │   │
│  │   REFERRAL     │ Employee Referral        │ Internal       │ Bonus           │   │
│  │   INTERNAL     │ Internal Application     │ Internal       │ Free            │   │
│  │   AGENCY       │ Staffing Agency          │ Agency         │ Fee %           │   │
│  │   EXEC_SEARCH  │ Executive Search         │ Agency         │ Retainer        │   │
│  │   GLASSDOOR    │ Glassdoor                │ Job Board      │ CPC             │   │
│  │   ZIPRECRUITER │ ZipRecruiter             │ Job Board      │ Subscription    │   │
│  │   CAREERBLDR   │ CareerBuilder            │ Job Board      │ Per-post        │   │
│  │   COLLEGE      │ College/University       │ Campus         │ Event           │   │
│  │   JOB_FAIR     │ Job Fair                 │ Event          │ Event           │   │
│  │   SOCIAL       │ Social Media             │ Organic        │ Free            │   │
│  │   REHIRE       │ Rehire/Alumni            │ Internal       │ Free            │   │
│  │   WALK_IN      │ Walk-in                  │ Direct         │ Free            │   │
│  │   OTHER        │ Other                    │ Misc           │ Varies          │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 11.2 Rejection Reason Codes

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                       11.2 REJECTION REASON CODES                                    │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   RECRUITER-INITIATED REJECTIONS:                                            │   │
│  │                                                                               │   │
│  │   Code              │ Reason                        │ Auto-Reject │ Email    │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │   NOT_QUALIFIED     │ Does not meet requirements    │ No          │ Standard │   │
│  │   UNDERQUALIFIED    │ Insufficient experience       │ No          │ Standard │   │
│  │   OVERQUALIFIED     │ Overqualified for role        │ No          │ Standard │   │
│  │   NO_WORK_AUTH      │ Not authorized to work        │ Yes         │ Standard │   │
│  │   FAILED_SCREEN     │ Failed screening questions    │ Yes         │ Standard │   │
│  │   FAILED_BGC        │ Background check failure      │ No          │ Special  │   │
│  │   NO_RESPONSE       │ Candidate unresponsive        │ No          │ Standard │   │
│  │   POS_FILLED        │ Position filled               │ No          │ Filled   │   │
│  │   POS_CANCELLED     │ Position cancelled            │ No          │ Cancelled│   │
│  │   NOT_FIT           │ Not a cultural fit            │ No          │ Standard │   │
│  │   SALARY_MISMATCH   │ Salary expectations too high  │ No          │ Standard │   │
│  │   LOCATION          │ Cannot relocate/commute       │ No          │ Standard │   │
│  │   DUPLICATE         │ Duplicate application         │ Yes         │ None     │   │
│  │                                                                               │   │
│  │   CANDIDATE-INITIATED WITHDRAWALS:                                           │   │
│  │                                                                               │   │
│  │   WITHDREW          │ Candidate withdrew            │ N/A         │ Confirm  │   │
│  │   OTHER_OFFER       │ Accepted another offer        │ N/A         │ Confirm  │   │
│  │   NOT_INTERESTED    │ No longer interested          │ N/A         │ Confirm  │   │
│  │   PERSONAL          │ Personal reasons              │ N/A         │ Confirm  │   │
│  │   COUNTER_OFFER     │ Accepted counter-offer        │ N/A         │ Confirm  │   │
│  │                                                                               │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 11.3 Email Template Reference

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                      11.3 EMAIL TEMPLATE REFERENCE                                   │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   Template Code              │ Trigger                  │ Recipient          │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │                              │                          │                    │   │
│  │   CANDIDATE COMMUNICATIONS:                                                  │   │
│  │   GEODIS_APP_CONFIRM         │ Application submitted    │ Candidate          │   │
│  │   GEODIS_APP_UPDATE          │ Status change            │ Candidate          │   │
│  │   GEODIS_SCREEN_INVITE       │ Phone screen scheduled   │ Candidate          │   │
│  │   GEODIS_INTERVIEW_INVITE    │ Interview scheduled      │ Candidate          │   │
│  │   GEODIS_INTERVIEW_REMINDER  │ 24 hrs before interview  │ Candidate          │   │
│  │   GEODIS_ASSESSMENT_LINK     │ Assessment assigned      │ Candidate          │   │
│  │   GEODIS_OFFER_PENDING       │ Offer being prepared     │ Candidate          │   │
│  │   GEODIS_OFFER_LETTER        │ Offer extended           │ Candidate          │   │
│  │   GEODIS_WELCOME             │ Offer accepted           │ Candidate          │   │
│  │   GEODIS_REJECT_STANDARD     │ Rejected                 │ Candidate          │   │
│  │   GEODIS_REJECT_FILLED       │ Position filled          │ Candidate          │   │
│  │   GEODIS_TALENT_COMMUNITY    │ Added to pool            │ Candidate          │   │
│  │                              │                          │                    │   │
│  │   INTERNAL NOTIFICATIONS:                                                    │   │
│  │   GEODIS_REQ_APPROVAL        │ Requisition pending      │ Approver           │   │
│  │   GEODIS_OFFER_APPROVAL      │ Offer pending            │ Approver           │   │
│  │   GEODIS_NEW_APPLICATION     │ New application          │ Recruiter          │   │
│  │   GEODIS_BGC_COMPLETE        │ Background check done    │ Recruiter          │   │
│  │   GEODIS_OFFER_SIGNED        │ Offer signed             │ Recruiter/HM       │   │
│  │   GEODIS_INTERNAL_APPLY      │ Internal candidate       │ Current Manager    │   │
│  │   GEODIS_FEEDBACK_REMINDER   │ Feedback overdue         │ Interviewer        │   │
│  │                              │                          │                    │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### 11.4 Security Roles Summary

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                       11.4 SECURITY ROLES SUMMARY                                    │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                                                                               │   │
│  │   Role                   │ Access Level             │ Data Security          │   │
│  │   ─────────────────────────────────────────────────────────────────────────  │   │
│  │                          │                          │                        │   │
│  │   Recruiting Manager     │ Full module access       │ All requisitions       │   │
│  │                          │ All configurations       │ All candidates         │   │
│  │                          │ All reports              │ All offers             │   │
│  │                          │                          │                        │   │
│  │   Recruiter              │ Assigned requisitions    │ Own requisitions       │   │
│  │                          │ All candidates           │ Assigned candidates    │   │
│  │                          │ Create/edit offers       │ Own offers             │   │
│  │                          │                          │                        │   │
│  │   Hiring Manager         │ Own requisitions only    │ Own requisitions       │   │
│  │                          │ Assigned candidates      │ Own candidates         │   │
│  │                          │ View/approve offers      │ Own team offers        │   │
│  │                          │                          │                        │   │
│  │   HRBP                   │ Regional requisitions    │ Region-based           │   │
│  │                          │ Approval workflows       │ Regional candidates    │   │
│  │                          │ Regional reports         │ Regional offers        │   │
│  │                          │                          │                        │   │
│  │   Interviewer            │ Assigned interviews      │ Interview feedback     │   │
│  │                          │ Feedback forms           │ Assigned candidates    │   │
│  │                          │ Limited candidate view   │                        │   │
│  │                          │                          │                        │   │
│  │   Compensation Analyst   │ Offer approval           │ Salary data            │   │
│  │                          │ Compensation reports     │ All offers             │   │
│  │                          │ Salary band validation   │                        │   │
│  │                          │                          │                        │   │
│  │   Candidate (External)   │ Self-service portal      │ Own profile            │   │
│  │                          │ Application status       │ Own applications       │   │
│  │                          │ Profile updates          │                        │   │
│  │                          │                          │                        │   │
│  │   Employee (Internal)    │ Internal job board       │ Own profile            │   │
│  │                          │ Internal applications    │ Own applications       │   │
│  │                          │ Profile + employee data  │                        │   │
│  │                          │                          │                        │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Document Summary

### Coverage Summary

| Section | Sub-sections | Workflows Documented |
|---------|--------------|---------------------|
| 1. Executive Summary | 4 | Overview, scope, rules, actors |
| 2. End-to-End Overview | 3 | Master flow, phases, volumes |
| 3. Requisition | 6 | Standard, high-salary, TOPEX, hold/cancel, multi-location, Core HR |
| 4. Job Posting | 6 | 7-day rule, urgent, multi-channel, Indeed, LinkedIn, auto-close |
| 5. Candidate Management | 6 | Intake, 12-phase pipeline, screening, mass disposition, pools, comms |
| 6. Interview | 4 | Scheduling, panel, feedback, assessment |
| 7. Offer & Hire | 6 | Creation, approval, DocuSign, Sterling, Core HR, decline/renegotiate |
| 8. Integration | 4 | Architecture, MDM sync, Recruiting-to-HR data flow |
| 9. RACI & Governance | 2 | RACI matrix, approval thresholds |
| 10. KPIs & Metrics | 2 | KPI dashboard, OTBI reports |
| 11. Appendices | 4 | Sources, rejection codes, email templates, security roles |

### Key Metrics

| Metric | Value |
|--------|-------|
| Total Sections | 11 |
| Total Sub-sections | 47 |
| Workflow Diagrams | 35+ |
| Process Phases | 12 |
| Candidate States | 43 |
| Offer Templates | 18 |
| Integration Points | 10 |
| Source Codes | 17 |
| Security Roles | 8 |

---

**Document Status:** COMPLETE
**Version:** 1.0
**Created:** 2025-12-07
**Total Lines:** ~2,400
