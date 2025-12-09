# GEODIS Oracle Recruiting - Workflow & Campaign Configuration Guide

**Document:** 17_Oracle_Recruiting_Workflow_Configuration_Guide.md
**Version:** 1.0
**Created:** 2025-12-07
**Module:** Oracle Recruiting Cloud (IRC)
**Purpose:** Complete guide for configuring workflows, stages, steps, actors, and campaigns

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Oracle Recruiting Workflow Architecture](#2-oracle-recruiting-workflow-architecture)
3. [Requisition Workflow Configuration](#3-requisition-workflow-configuration)
4. [Candidate Selection Process Configuration](#4-candidate-selection-process-configuration)
5. [Phases and States Configuration](#5-phases-and-states-configuration)
6. [Actors and Roles Configuration](#6-actors-and-roles-configuration)
7. [Approval Workflows (BPM)](#7-approval-workflows-bpm)
8. [Automated Actions and Notifications](#8-automated-actions-and-notifications)
9. [Campaign Management (Paradox Equivalent)](#9-campaign-management-paradox-equivalent)
10. [GEODIS-Specific Configuration](#10-geodis-specific-configuration)
11. [Implementation Checklist](#11-implementation-checklist)

---

## 1. Executive Summary

### 1.1 Purpose

This document provides detailed configuration guidance for:
- **Workflow stages and steps** for requisition and candidate management
- **Actor assignments** (who does what in the process)
- **Approval workflows** for requisitions and offers
- **Campaign functionality** to replace/complement Paradox campaigns

### 1.2 Current State (Paradox)

GEODIS currently uses Paradox for:
- Mass candidate communication (SMS/Email)
- Single campaigns (one-time messages)
- Drip campaigns (automated sequences)
- Audience targeting (by status, job, location, source)
- Interview scheduling campaigns
- Hiring event coordination

### 1.3 Oracle Recruiting Capabilities

Oracle Recruiting provides:
- **Candidate Selection Process** (phases/states workflow)
- **Approval Workflows** (BPM-based)
- **Correspondence Rules** (automated emails)
- **Candidate Pools** (talent communities)
- **Bulk Actions** (mass disposition, communication)
- **Oracle Recruiting Booster** (AI-powered outreach)
- **Integration with Paradox** (if retained)

---

## 2. Oracle Recruiting Workflow Architecture

### 2.1 Workflow Hierarchy

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    ORACLE RECRUITING WORKFLOW HIERARCHY                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  LEVEL 1: REQUISITION TEMPLATE                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ Defines: Form layout, required fields, default values, approvals    │   │
│  │ GEODIS Templates: STD, EXEC, FR, US, INTERN                         │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│           │                                                                 │
│           ▼                                                                 │
│  LEVEL 2: CANDIDATE SELECTION PROCESS                                       │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ Defines: Phases (stages), States (steps), Transitions, Actions      │   │
│  │ Each template can have different selection process                  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│           │                                                                 │
│           ▼                                                                 │
│  LEVEL 3: PHASES (STAGES)                                                   │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ Major milestones: NEW → SCREEN → INTERVIEW → OFFER → HIRE           │   │
│  │ Each phase can have multiple states                                 │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│           │                                                                 │
│           ▼                                                                 │
│  LEVEL 4: STATES (STEPS)                                                    │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ Detailed steps within phases: Scheduled, Completed, Passed, etc.    │   │
│  │ States have: Actions, Transitions, Notifications                    │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│           │                                                                 │
│           ▼                                                                 │
│  LEVEL 5: ACTIONS & NOTIFICATIONS                                           │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ System/user actions triggered by state changes                      │   │
│  │ Correspondence rules for automated communications                   │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 2.2 Key Configuration Areas

| Area | Setup Task | Location in Oracle |
|------|------------|-------------------|
| **Requisition Templates** | Define form structure | Setup and Maintenance → Recruiting → Requisition Templates |
| **Selection Process** | Configure phases/states | Setup and Maintenance → Recruiting → Candidate Selection Process |
| **Approval Workflows** | BPM workflow rules | Setup and Maintenance → Approval Management |
| **Correspondence** | Email templates & rules | Setup and Maintenance → Recruiting → Correspondence |
| **Notifications** | Alert configuration | Setup and Maintenance → Alerts Composer |
| **Security** | Roles and data access | Setup and Maintenance → Security Console |

---

## 3. Requisition Workflow Configuration

### 3.1 Requisition Lifecycle Phases

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       REQUISITION LIFECYCLE                                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌────────┐    ┌──────────────┐    ┌──────────┐    ┌────────┐    ┌───────┐ │
│  │ DRAFT  │───▶│   PENDING    │───▶│ APPROVED │───▶│  OPEN  │───▶│FILLED │ │
│  │        │    │   APPROVAL   │    │          │    │        │    │       │ │
│  └────────┘    └──────────────┘    └──────────┘    └────────┘    └───────┘ │
│       │              │                   │              │             │     │
│       ▼              ▼                   │              ▼             ▼     │
│  ┌────────┐    ┌──────────┐             │        ┌──────────┐   ┌───────┐ │
│  │CANCELLED│   │ REJECTED │             │        │ ON HOLD  │   │CLOSED │ │
│  └────────┘    └──────────┘             │        └──────────┘   └───────┘ │
│                                          │                                  │
│  ACTIONS BY PHASE:                       │                                  │
│  ─────────────────                       │                                  │
│  DRAFT: Create, Edit, Submit, Cancel     │                                  │
│  PENDING: Approve, Reject, Request Info  │                                  │
│  APPROVED: Activate (auto or manual)     │                                  │
│  OPEN: Post Jobs, Source, Hold, Fill     │                                  │
│  FILLED: Close, Archive                  │                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Requisition Phase Configuration

| Phase Code | Phase Name | Description | Auto-Advance | GEODIS Rule |
|------------|------------|-------------|--------------|-------------|
| DRAFT | Draft | Initial creation | No | - |
| PENDING_APPROVAL | Pending Approval | Awaiting approvals | No | - |
| APPROVED | Approved | All approvals complete | Yes | Auto to OPEN |
| OPEN | Open | Actively recruiting | No | - |
| ON_HOLD | On Hold | Temporarily paused | No | Max 90 days |
| FILLED | Filled | Position(s) filled | No | - |
| CLOSED | Closed | Process complete | No | Archive after 30 days |
| CANCELLED | Cancelled | Requisition abandoned | No | - |

### 3.3 Requisition Actions by Actor

| Actor | Allowed Actions |
|-------|-----------------|
| **Hiring Manager** | Create, Edit (Draft), Submit, View, Request Hold |
| **Recruiter** | Edit, Post Jobs, Source Candidates, Fill, Close |
| **HRBP** | Approve, Reject, Request Info, Override Hold |
| **N+1 Manager** | Approve, Reject, Request Info |
| **EVP HR / CHRO** | Approve (High Salary/TOPEX), Reject |
| **System** | Auto-advance, Send Notifications, Calculate SLAs |

---

## 4. Candidate Selection Process Configuration

### 4.1 GEODIS Candidate Selection Process

```
┌─────────────────────────────────────────────────────────────────────────────┐
│              GEODIS CANDIDATE SELECTION PROCESS (12 PHASES)                  │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  PHASE 1: NEW ──────────────────────────────────────────────────────────▶  │
│  ├── State: New - Pending Review (auto on apply)                           │
│  ├── State: New - Under Consideration                                      │
│  └── Actions: Review Resume, Move to Screen, Reject, Add to Pool           │
│                                                                             │
│  PHASE 2: SCREENING ────────────────────────────────────────────────────▶  │
│  ├── State: Phone Screen Scheduled                                         │
│  ├── State: Phone Screen Completed                                         │
│  ├── State: Screening Passed                                               │
│  └── Actions: Schedule Call, Complete Screen, Pass/Fail, Add Notes         │
│                                                                             │
│  PHASE 3: ASSESSMENT ───────────────────────────────────────────────────▶  │
│  ├── State: Assessment Invited                                             │
│  ├── State: Assessment In Progress                                         │
│  ├── State: Assessment Completed                                           │
│  ├── State: Assessment Passed                                              │
│  └── Actions: Send Assessment, View Results, Pass/Fail                     │
│                                                                             │
│  PHASE 4: INTERVIEW ────────────────────────────────────────────────────▶  │
│  ├── State: Interview Scheduled                                            │
│  ├── State: Interview Completed                                            │
│  ├── State: Interview Passed                                               │
│  └── Actions: Schedule, Reschedule, Cancel, Complete, Collect Feedback     │
│                                                                             │
│  PHASE 5: MANAGER REVIEW ───────────────────────────────────────────────▶  │
│  ├── State: Pending Manager Decision                                       │
│  ├── State: Manager Approved                                               │
│  └── Actions: Review Feedback, Approve, Request Additional Interview       │
│                                                                             │
│  PHASE 6: REFERENCE CHECK ──────────────────────────────────────────────▶  │
│  ├── State: References Requested                                           │
│  ├── State: References Received                                            │
│  ├── State: References Verified                                            │
│  └── Actions: Request References, Verify, Document Results                 │
│                                                                             │
│  PHASE 7: OFFER ────────────────────────────────────────────────────────▶  │
│  ├── State: Offer Pending Approval                                         │
│  ├── State: Offer Approved                                                 │
│  ├── State: Offer Extended                                                 │
│  ├── State: Offer Accepted                                                 │
│  ├── State: Offer Declined                                                 │
│  └── Actions: Create Offer, Approve, Extend, Negotiate, Accept/Decline     │
│                                                                             │
│  PHASE 8: BACKGROUND CHECK ─────────────────────────────────────────────▶  │
│  ├── State: Background Initiated                                           │
│  ├── State: Background In Progress                                         │
│  ├── State: Background Cleared                                             │
│  ├── State: Background Issue                                               │
│  └── Actions: Initiate Check, Update Status, Clear/Flag                    │
│                                                                             │
│  PHASE 9: HR PROCESSING ────────────────────────────────────────────────▶  │
│  ├── State: Documents Requested                                            │
│  ├── State: Documents Received                                             │
│  ├── State: HR Review Complete                                             │
│  └── Actions: Request Docs, Verify, Complete Review                        │
│                                                                             │
│  PHASE 10: PRE-HIRE ────────────────────────────────────────────────────▶  │
│  ├── State: Pre-Hire Tasks Assigned                                        │
│  ├── State: Pre-Hire Complete                                              │
│  └── Actions: Assign Tasks, Track Completion                               │
│                                                                             │
│  PHASE 11: HIRE ────────────────────────────────────────────────────────▶  │
│  ├── State: Hire Confirmed                                                 │
│  ├── State: Start Date Set                                                 │
│  └── Actions: Confirm Hire, Set Start Date, Create Employee                │
│                                                                             │
│  PHASE 12: COMPLETE ────────────────────────────────────────────────────▶  │
│  ├── State: Onboarding Initiated                                           │
│  ├── State: Process Complete                                               │
│  └── Actions: Launch Onboarding, Archive                                   │
│                                                                             │
│  TERMINAL PHASES:                                                          │
│  ├── REJECTED: Rejection reason required, notification sent                │
│  ├── WITHDRAWN: Candidate initiated, reason captured                       │
│  ├── ON_HOLD: Temporary pause, auto-reminder after 30 days                 │
│  └── POOLED: Added to talent pool for future consideration                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 4.2 Phase-State Configuration Table

| Phase | Phase Code | Seq | States | Terminal? |
|-------|------------|-----|--------|-----------|
| New | NEW | 1 | Pending Review, Under Consideration | No |
| Screening | SCREEN | 2 | Scheduled, Completed, Passed | No |
| Assessment | ASSESS | 3 | Invited, In Progress, Completed, Passed | No |
| Interview | INTERVIEW | 4 | Scheduled, Completed, Passed | No |
| Manager Review | MGR_REVIEW | 5 | Pending Decision, Approved | No |
| Reference Check | REFERENCE | 6 | Requested, Received, Verified | No |
| Offer | OFFER | 7 | Pending Approval, Approved, Extended, Accepted, Declined | No |
| Background | BACKGROUND | 8 | Initiated, In Progress, Cleared, Issue | No |
| HR Processing | HR_PROC | 9 | Docs Requested, Docs Received, Review Complete | No |
| Pre-Hire | PRE_HIRE | 10 | Tasks Assigned, Complete | No |
| Hire | HIRE | 11 | Confirmed, Start Date Set | No |
| Complete | COMPLETE | 12 | Onboarding, Complete | Yes |
| Rejected | REJECTED | 99 | (Single state) | Yes |
| Withdrawn | WITHDRAWN | 98 | (Single state) | Yes |
| On Hold | ON_HOLD | 97 | (Single state) | No |
| Pooled | POOLED | 96 | (Single state) | Yes |

---

## 5. Phases and States Configuration

### 5.1 State Configuration Details

#### Phase: NEW

| State Code | State Name | Entry Action | Exit Action | SLA | Auto-Advance |
|------------|------------|--------------|-------------|-----|--------------|
| NEW_PENDING | Pending Review | Send confirmation email | - | 48 hrs | No |
| NEW_CONSIDER | Under Consideration | - | - | - | No |

**Allowed Transitions from NEW:**
- → SCREEN (Move to Screening)
- → REJECTED (Reject)
- → POOLED (Add to Pool)
- → WITHDRAWN (Candidate Withdraws)

#### Phase: SCREENING

| State Code | State Name | Entry Action | Exit Action | SLA | Auto-Advance |
|------------|------------|--------------|-------------|-----|--------------|
| SCR_SCHEDULED | Phone Screen Scheduled | Send interview invite | Reminder 24h before | - | No |
| SCR_COMPLETED | Phone Screen Completed | Request feedback | - | 24 hrs | No |
| SCR_PASSED | Screening Passed | - | - | - | No |

**Allowed Transitions from SCREENING:**
- → ASSESS (Move to Assessment)
- → INTERVIEW (Skip to Interview)
- → REJECTED (Reject)
- → WITHDRAWN (Candidate Withdraws)

#### Phase: INTERVIEW

| State Code | State Name | Entry Action | Exit Action | SLA | Auto-Advance |
|------------|------------|--------------|-------------|-----|--------------|
| INT_SCHEDULED | Interview Scheduled | Send invite, Book room | Reminder 24h + 1h | - | No |
| INT_COMPLETED | Interview Completed | Request feedback | - | 48 hrs | No |
| INT_PASSED | Interview Passed | Notify candidate | - | - | No |

**Allowed Transitions from INTERVIEW:**
- → INTERVIEW (Additional Interview)
- → MGR_REVIEW (Move to Manager Review)
- → REJECTED (Reject)
- → WITHDRAWN (Candidate Withdraws)

#### Phase: OFFER

| State Code | State Name | Entry Action | Exit Action | SLA | Auto-Advance |
|------------|------------|--------------|-------------|-----|--------------|
| OFF_PENDING | Offer Pending Approval | Route to approvers | - | 3 days | No |
| OFF_APPROVED | Offer Approved | Notify recruiter | - | - | No |
| OFF_EXTENDED | Offer Extended | Send offer via DocuSign | Reminder Day 3 | 5 days | No |
| OFF_ACCEPTED | Offer Accepted | Notify team, Create tasks | - | - | Yes → BACKGROUND |
| OFF_DECLINED | Offer Declined | Capture reason | - | - | Terminal |

### 5.2 State Transition Rules

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         STATE TRANSITION RULES                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  RULE 1: Sequential Phase Movement                                          │
│  ─────────────────────────────────                                          │
│  Candidates must complete all states in a phase before moving to next      │
│  Exception: Can skip phases if configured (e.g., skip Assessment)          │
│                                                                             │
│  RULE 2: Backward Movement                                                  │
│  ─────────────────────────────                                              │
│  Generally prohibited except:                                               │
│  - Additional Interview (INTERVIEW → INTERVIEW)                            │
│  - Offer Renegotiation (OFF_EXTENDED → OFF_PENDING)                        │
│                                                                             │
│  RULE 3: Terminal States                                                    │
│  ──────────────────────────                                                 │
│  Once in terminal state, no further transitions allowed except:            │
│  - REJECTED → POOLED (Silver medalist)                                     │
│  - WITHDRAWN → POOLED (Future consideration)                               │
│                                                                             │
│  RULE 4: Parallel States                                                    │
│  ────────────────────────                                                   │
│  Some activities can run in parallel:                                       │
│  - Reference check during Interview phase                                  │
│  - Background check initiated before Offer acceptance                      │
│                                                                             │
│  RULE 5: Required Data                                                      │
│  ─────────────────────                                                      │
│  Certain transitions require data entry:                                   │
│  - → REJECTED: Rejection reason required                                   │
│  - → OFF_EXTENDED: Offer details required                                  │
│  - → HIRE: Start date required                                             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 6. Actors and Roles Configuration

### 6.1 Oracle Recruiting Roles (Security Roles)

| Role | Code | Description | Typical Users |
|------|------|-------------|---------------|
| **Hiring Manager** | ORA_IRC_HIRING_MANAGER | Creates requisitions, reviews candidates, makes decisions | Line managers |
| **Recruiter** | ORA_IRC_RECRUITER | Full recruiting lifecycle management | TA team |
| **Recruiting Coordinator** | ORA_IRC_COORDINATOR | Scheduling, administration | TA coordinators |
| **Recruiting Manager** | ORA_IRC_RECRUITING_MANAGER | Team oversight, reporting | TA managers |
| **HR Business Partner** | ORA_IRC_HRBP | Approvals, advisory | HRBPs |
| **Compensation Analyst** | ORA_IRC_COMP_ANALYST | Offer review, salary validation | Comp team |
| **Interviewer** | ORA_IRC_INTERVIEWER | Interview participation, feedback | Interview panel |
| **Executive Approver** | GEODIS_EXEC_APPROVER | High-value approvals | EVP HR, CHRO |
| **Candidate** | ORA_IRC_CANDIDATE | Self-service application | External/internal candidates |

### 6.2 Hiring Team Roles

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           HIRING TEAM STRUCTURE                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  REQUISITION OWNER                                                          │
│  ─────────────────                                                          │
│  └── Hiring Manager (Required)                                              │
│      • Creates requisition                                                  │
│      • Makes final hiring decision                                          │
│      • Primary contact for candidates                                       │
│                                                                             │
│  PRIMARY RECRUITER (Required)                                               │
│  ─────────────────────────────                                              │
│  └── Assigned Recruiter                                                     │
│      • Manages end-to-end process                                           │
│      • Sources and screens candidates                                       │
│      • Coordinates interviews                                               │
│      • Extends offers                                                       │
│                                                                             │
│  SECONDARY RECRUITER (Optional)                                             │
│  ──────────────────────────────                                             │
│  └── Backup/Support Recruiter                                               │
│      • Coverage during absence                                              │
│      • High-volume support                                                  │
│                                                                             │
│  COLLABORATORS (Optional)                                                   │
│  ─────────────────────────                                                  │
│  ├── Interview Panel Members                                                │
│  │   • Participate in interviews                                            │
│  │   • Provide feedback                                                     │
│  ├── HR Business Partner                                                    │
│  │   • Advisory role                                                        │
│  │   • Approval chain                                                       │
│  └── Compensation Partner                                                   │
│      • Offer validation                                                     │
│      • Salary band review                                                   │
│                                                                             │
│  APPROVERS (Workflow-based)                                                 │
│  ──────────────────────────                                                 │
│  ├── N+1 Manager (Hiring Manager's manager)                                │
│  ├── HRBP                                                                   │
│  ├── EVP HR (High salary)                                                  │
│  └── CHRO (TOPEX)                                                          │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 6.3 Role-Based Actions Matrix

| Action | Hiring Mgr | Recruiter | HRBP | Interviewer | Candidate |
|--------|-----------|-----------|------|-------------|-----------|
| Create Requisition | ✓ | ✓ | - | - | - |
| Edit Requisition | ✓ (Draft) | ✓ | ✓ | - | - |
| Approve Requisition | - | - | ✓ | - | - |
| Post Job | - | ✓ | - | - | - |
| View Candidates | ✓ | ✓ | ✓ | ✓ (assigned) | - |
| Move Candidate | ✓ | ✓ | - | - | - |
| Schedule Interview | - | ✓ | - | - | ✓ (self) |
| Provide Feedback | ✓ | ✓ | - | ✓ | - |
| Create Offer | - | ✓ | - | - | - |
| Approve Offer | - | - | ✓ | - | - |
| Accept/Decline Offer | - | - | - | - | ✓ |
| Initiate Hire | - | ✓ | ✓ | - | - |

---

## 7. Approval Workflows (BPM)

### 7.1 Requisition Approval Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    REQUISITION APPROVAL WORKFLOW (BPM)                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  WORKFLOW: GEODIS_REQ_APPROVAL                                              │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ START: Requisition Submitted                                        │   │
│  └────────────────────────────────┬────────────────────────────────────┘   │
│                                   │                                         │
│                                   ▼                                         │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ RULE 1: Check Salary Level                                          │   │
│  │                                                                     │   │
│  │ IF MAX_SALARY < 125000 EUR → Standard Path                         │   │
│  │ IF MAX_SALARY >= 125000 AND < 155000 EUR → Senior Path             │   │
│  │ IF MAX_SALARY >= 155000 EUR OR TOPEX = Y → Executive Path          │   │
│  └────────────────────────────────┬────────────────────────────────────┘   │
│                                   │                                         │
│         ┌─────────────────────────┼─────────────────────────┐              │
│         ▼                         ▼                         ▼              │
│  ┌─────────────┐          ┌─────────────┐          ┌─────────────┐        │
│  │  STANDARD   │          │   SENIOR    │          │  EXECUTIVE  │        │
│  │             │          │             │          │             │        │
│  │ N+1 Manager │          │ N+1 Manager │          │ N+1 Manager │        │
│  │     ↓       │          │     ↓       │          │     ↓       │        │
│  │   HRBP      │          │  Director   │          │  Director   │        │
│  │             │          │     ↓       │          │     ↓       │        │
│  │             │          │   HRBP      │          │    VP       │        │
│  │             │          │             │          │     ↓       │        │
│  │             │          │             │          │   CHRO      │        │
│  └─────────────┘          └─────────────┘          └─────────────┘        │
│         │                         │                         │              │
│         └─────────────────────────┴─────────────────────────┘              │
│                                   │                                         │
│                                   ▼                                         │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ RULE 2: All Approvals Complete?                                     │   │
│  │                                                                     │   │
│  │ YES → Set Status = APPROVED, Notify Requester                      │   │
│  │ NO (Rejected) → Set Status = REJECTED, Return to Requester         │   │
│  │ NO (Info Request) → Set Status = INFO_REQUESTED, Notify Requester  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│  ESCALATION RULES:                                                         │
│  ──────────────────                                                        │
│  • No response in 2 days → Email reminder                                  │
│  • No response in 3 days → Second reminder + Manager notification          │
│  • No response in 5 days → Auto-escalate to next level                    │
│                                                                             │
│  EMAIL APPROVAL:                                                           │
│  ───────────────                                                           │
│  • Approvers can approve/reject directly from email                       │
│  • Email contains: Requisition summary, Approve/Reject buttons            │
│  • Link to full details in Oracle                                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 7.2 Offer Approval Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       OFFER APPROVAL WORKFLOW (BPM)                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  WORKFLOW: GEODIS_OFFER_APPROVAL                                            │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ START: Offer Created and Submitted                                  │   │
│  └────────────────────────────────┬────────────────────────────────────┘   │
│                                   │                                         │
│                                   ▼                                         │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ RULE 1: Check Offer Value                                           │   │
│  │                                                                     │   │
│  │ BASE_SALARY = Offer.SalaryAmount                                   │   │
│  │ TOTAL_COMP = BASE + BONUS_TARGET + SIGN_ON + OTHER                 │   │
│  │                                                                     │   │
│  │ IF BASE < 125000 EUR AND TOTAL < 155000 EUR → Standard Path        │   │
│  │ IF BASE >= 125000 EUR OR TOTAL >= 155000 EUR → High Value Path     │   │
│  │ IF TOPEX = Y → Executive Path                                       │   │
│  └────────────────────────────────┬────────────────────────────────────┘   │
│                                   │                                         │
│         ┌─────────────────────────┼─────────────────────────┐              │
│         ▼                         ▼                         ▼              │
│  ┌─────────────┐          ┌─────────────┐          ┌─────────────┐        │
│  │  STANDARD   │          │ HIGH VALUE  │          │  EXECUTIVE  │        │
│  │             │          │             │          │             │        │
│  │Hiring Manager│         │Hiring Manager│         │Hiring Manager│       │
│  │     ↓       │          │     ↓       │          │     ↓       │        │
│  │  HR/Comp    │          │  HR/Comp    │          │  HR/Comp    │        │
│  │             │          │     ↓       │          │     ↓       │        │
│  │             │          │  EVP HR     │          │   CHRO      │        │
│  └─────────────┘          └─────────────┘          └─────────────┘        │
│         │                         │                         │              │
│         └─────────────────────────┴─────────────────────────┘              │
│                                   │                                         │
│                                   ▼                                         │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ APPROVED → State = OFF_APPROVED                                     │   │
│  │ REJECTED → State = OFF_PENDING (with comments)                     │   │
│  │ COUNTER → State = OFF_RENEGOTIATE (candidate counter offer)        │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 7.3 Approval Workflow Configuration Steps

1. **Navigate to:** Setup and Maintenance → Approval Management → Manage Task Configurations

2. **Create Approval Policy:**
   ```
   Policy Name: GEODIS_Requisition_Approval
   Task Type: Requisition Approval
   Rules:
     - Rule 1: Salary < 125K → Standard Chain
     - Rule 2: Salary >= 125K < 155K → Senior Chain
     - Rule 3: Salary >= 155K OR TOPEX → Executive Chain
   ```

3. **Configure Approval Chains:**
   ```
   Standard Chain:
     Stage 1: Reporting Manager (1 approver required)
     Stage 2: HRBP (1 approver required)

   Senior Chain:
     Stage 1: Reporting Manager
     Stage 2: Director (2 levels up)
     Stage 3: HRBP

   Executive Chain:
     Stage 1: Reporting Manager
     Stage 2: Director
     Stage 3: VP
     Stage 4: CHRO
   ```

4. **Set Escalation:**
   ```
   Escalation Timeout: 2 days
   First Reminder: 1 day
   Second Reminder: 2 days
   Auto-Escalate: 3 days
   ```

---

## 8. Automated Actions and Notifications

### 8.1 Correspondence Rules (Email Automation)

| Rule Code | Trigger Event | Recipients | Template |
|-----------|---------------|------------|----------|
| APPLY_CONFIRM | Candidate applies | Candidate | Application Confirmation |
| SCREEN_INVITE | Move to Screening | Candidate | Phone Screen Invitation |
| INT_INVITE | Interview scheduled | Candidate + Interviewers | Interview Invitation |
| INT_REMIND_24H | 24h before interview | Candidate + Interviewers | Interview Reminder |
| INT_REMIND_1H | 1h before interview | Candidate | Final Reminder |
| INT_FEEDBACK | Interview completed | Interviewer | Feedback Request |
| INT_FEEDBACK_OVERDUE | Feedback overdue 48h | Interviewer + Recruiter | Feedback Reminder |
| OFFER_EXTEND | Offer extended | Candidate | Offer Letter |
| OFFER_REMIND | Offer Day 3 | Candidate | Offer Reminder |
| OFFER_ACCEPT | Offer accepted | Hiring Team | Acceptance Notification |
| OFFER_DECLINE | Offer declined | Hiring Team | Decline Notification |
| REJECT | Candidate rejected | Candidate | Rejection Letter |
| POOL_ADD | Added to pool | Candidate | Talent Pool Welcome |
| BG_INITIATE | Background started | Candidate | Background Check Info |
| BG_COMPLETE | Background cleared | Recruiter | Background Results |
| HIRE_CONFIRM | Hire confirmed | Candidate | Welcome Letter |
| REQ_APPROVAL | Req needs approval | Approver | Approval Request |
| REQ_APPROVED | Req approved | Requester + Recruiter | Approval Confirmation |
| REQ_REJECTED | Req rejected | Requester | Rejection Notice |

### 8.2 Notification Configuration

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    NOTIFICATION CONFIGURATION                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ORACLE ALERTS COMPOSER:                                                    │
│  ───────────────────────                                                    │
│  Setup and Maintenance → Alerts Composer → Manage Alerts                   │
│                                                                             │
│  ALERT 1: Interview Feedback Overdue                                        │
│  ────────────────────────────────────                                       │
│  Trigger: Interview completed > 48 hours ago AND feedback not submitted    │
│  Recipients: Interviewer, CC: Recruiter                                     │
│  Frequency: Daily until submitted or 5 days                                │
│  Message: "Interview feedback overdue for [Candidate] - [Requisition]"     │
│                                                                             │
│  ALERT 2: Offer Expiring                                                    │
│  ────────────────────────                                                   │
│  Trigger: Offer expiration in 2 days AND status = EXTENDED                 │
│  Recipients: Candidate, CC: Recruiter                                       │
│  Frequency: Once                                                            │
│  Message: "Your offer from GEODIS expires in 2 days"                       │
│                                                                             │
│  ALERT 3: Requisition Aging                                                 │
│  ────────────────────────                                                   │
│  Trigger: Requisition open > 45 days AND status = OPEN                     │
│  Recipients: Recruiter, Hiring Manager                                      │
│  Frequency: Weekly                                                          │
│  Message: "Requisition [Number] has been open for [X] days"                │
│                                                                             │
│  ALERT 4: 6-Month Auto-Close Warning                                        │
│  ──────────────────────────────────                                         │
│  Trigger: Requisition open > 150 days (5 months)                           │
│  Recipients: Recruiter, Hiring Manager, HRBP                                │
│  Frequency: Weekly until 180 days                                          │
│  Message: "Requisition will auto-close at 6 months unless extended"        │
│                                                                             │
│  ALERT 5: Approval Pending                                                  │
│  ────────────────────────                                                   │
│  Trigger: Approval pending > 24 hours                                      │
│  Recipients: Approver                                                       │
│  Frequency: Daily until actioned                                           │
│  Message: "[Object] awaiting your approval - Day [X]"                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 9. Campaign Management (Paradox Equivalent)

### 9.1 Paradox Current Capabilities

Based on the GEODIS Paradox Campaigns Process document:

| Feature | Paradox Capability | Description |
|---------|-------------------|-------------|
| **Single Campaign** | One-time message | Mass communication to selected candidates |
| **Drip Campaign** | Automated sequence | Auto-scheduled messages based on triggers |
| **Audience Upload** | CSV import | Upload candidate list from Indeed/Insight |
| **Audience Build** | Filter existing | Filter candidates by status, job, location |
| **Channels** | SMS + Email | Multi-channel communication |
| **Campaign Types** | Message, Conversation, Scheduling | Different interaction types |
| **Virtual Assistant** | Sophie | AI chatbot for conversations |
| **Event Integration** | Hiring events | Link campaigns to hiring events |
| **Metrics** | Engagement tracking | Sent, Engaged, Opened, Scheduled, Qualified |

### 9.2 Oracle Recruiting Equivalents

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    CAMPAIGN FUNCTIONALITY IN ORACLE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  OPTION 1: ORACLE RECRUITING BOOSTER (Recommended)                          │
│  ─────────────────────────────────────────────────                          │
│                                                                             │
│  Oracle Recruiting Booster is an AI-powered add-on that provides:          │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ CAMPAIGNS                                                           │   │
│  │ ├── Create targeted campaigns                                       │   │
│  │ ├── Single or automated sequences                                   │   │
│  │ ├── Email and SMS channels                                          │   │
│  │ ├── Audience segmentation                                           │   │
│  │ └── Campaign analytics                                              │   │
│  ├─────────────────────────────────────────────────────────────────────┤   │
│  │ AI MATCHING                                                         │   │
│  │ ├── AI-powered candidate matching                                   │   │
│  │ ├── Skill-based recommendations                                     │   │
│  │ └── Similar candidate suggestions                                   │   │
│  ├─────────────────────────────────────────────────────────────────────┤   │
│  │ CHATBOT                                                             │   │
│  │ ├── Oracle Digital Assistant                                        │   │
│  │ ├── 24/7 candidate support                                          │   │
│  │ ├── FAQ responses                                                   │   │
│  │ └── Application assistance                                          │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│  OPTION 2: NATIVE ORACLE RECRUITING FEATURES                                │
│  ─────────────────────────────────────────────                              │
│                                                                             │
│  Without Recruiting Booster, use these native features:                    │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ BULK ACTIONS                                                        │   │
│  │ ├── Select multiple candidates                                      │   │
│  │ ├── Send bulk emails                                                │   │
│  │ ├── Move to phase/state                                             │   │
│  │ ├── Add to candidate pool                                           │   │
│  │ └── Export for external processing                                  │   │
│  ├─────────────────────────────────────────────────────────────────────┤   │
│  │ CANDIDATE POOLS                                                     │   │
│  │ ├── Silver Medalists                                                │   │
│  │ ├── Talent Community (speculative)                                  │   │
│  │ ├── Event Attendees                                                 │   │
│  │ ├── Referral Pool                                                   │   │
│  │ └── Custom pools                                                    │   │
│  ├─────────────────────────────────────────────────────────────────────┤   │
│  │ CORRESPONDENCE RULES                                                │   │
│  │ ├── Automated emails on state change                                │   │
│  │ ├── Scheduled reminders                                             │   │
│  │ └── Event-triggered notifications                                   │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
│  OPTION 3: RETAIN PARADOX INTEGRATION                                       │
│  ─────────────────────────────────────                                      │
│                                                                             │
│  Continue using Paradox for campaign management:                           │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ INTEGRATION ARCHITECTURE                                            │   │
│  │                                                                     │   │
│  │  Oracle Recruiting ←──────────────────────→ Paradox                │   │
│  │       │                                          │                  │   │
│  │       │ • Candidate sync (bi-directional)       │                  │   │
│  │       │ • Status updates                         │                  │   │
│  │       │ • Application import                     │                  │   │
│  │       │ • Event coordination                     │                  │   │
│  │                                                                     │   │
│  │  Benefits:                                                          │   │
│  │  ├── Keep proven campaign functionality                             │   │
│  │  ├── Sophie virtual assistant continues                             │   │
│  │  ├── SMS capabilities maintained                                    │   │
│  │  └── Minimal change management                                      │   │
│  │                                                                     │   │
│  │  Drawbacks:                                                         │   │
│  │  ├── Two systems to maintain                                        │   │
│  │  ├── Integration complexity                                         │   │
│  │  └── Additional licensing cost                                      │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 9.3 Campaign Use Cases - Oracle Implementation

#### Use Case 1: Single Campaign (Mass Communication)

**Paradox:** Single Campaign → Message type → Send to filtered audience

**Oracle Native:**
```
1. Navigate: Recruiting → Candidates
2. Filter: By requisition, status, source, location, date
3. Select: Check multiple candidates
4. Action: "Send Email"
5. Template: Select or compose message
6. Send: Immediate or scheduled
```

**Oracle Booster:**
```
1. Navigate: Recruiting Booster → Campaigns
2. Create: New Campaign
3. Type: Single Message
4. Audience: Build or upload
5. Content: Email/SMS with personalization
6. Schedule: Send now or later
7. Track: View engagement metrics
```

#### Use Case 2: Drip Campaign (Automated Sequence)

**Paradox:** Drip Campaign → Auto-schedule messages based on triggers

**Oracle Native (Correspondence Rules):**
```
Setup:
1. Navigate: Setup → Recruiting → Correspondence Rules
2. Create rules for each trigger:
   - Rule 1: On Apply → Send Welcome (Day 0)
   - Rule 2: On Apply + 3 days → Send Company Info (Day 3)
   - Rule 3: On Apply + 7 days if still NEW → Send Engagement (Day 7)
```

**Oracle Booster:**
```
1. Navigate: Recruiting Booster → Campaigns
2. Create: New Drip Campaign
3. Define sequence:
   - Message 1: Day 0 (Welcome)
   - Message 2: Day 3 (Company culture)
   - Message 3: Day 7 (Application tips)
   - Message 4: Day 14 (Interview prep if scheduled)
4. Triggers: Apply, status change, job match
5. Activate: Enable campaign
```

#### Use Case 3: Event/Hiring Campaign

**Paradox:** Scheduling campaign linked to hiring event

**Oracle Native:**
```
1. Create Candidate Pool: "Hiring Event - [Location] - [Date]"
2. Add candidates to pool (filter or import)
3. Bulk action: Send event invitation email
4. Track RSVPs via questionnaire response
5. Create requisition linked to event
6. Bulk schedule interviews for attendees
```

**Oracle Booster:**
```
1. Create Event Campaign
2. Link to specific requisition(s)
3. Define audience criteria
4. Send event invitation
5. Track registrations
6. Automated reminders before event
7. Post-event follow-up sequence
```

### 9.4 Campaign Feature Mapping

| Paradox Feature | Oracle Native | Oracle Booster | Paradox Integration |
|-----------------|---------------|----------------|---------------------|
| Single Campaign | ✓ Bulk email | ✓ Full campaign | ✓ As-is |
| Drip Campaign | △ Correspondence rules | ✓ Full sequences | ✓ As-is |
| SMS Channel | ✗ Not native | △ Limited | ✓ Full SMS |
| Sophie Chatbot | ✗ Not native | △ ODA chatbot | ✓ As-is |
| CSV Import | ✓ HDL import | ✓ Audience upload | ✓ As-is |
| Audience Filter | ✓ Advanced search | ✓ Smart segments | ✓ As-is |
| Event Link | △ Manual pool | ✓ Event campaigns | ✓ Event inbox |
| Auto-Scheduling | △ Self-schedule | ✓ AI scheduling | ✓ As-is |
| Metrics | △ OTBI reports | ✓ Campaign analytics | ✓ Built-in |

**Legend:** ✓ Full support | △ Partial support | ✗ Not available

### 9.5 Recommendation for GEODIS

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         RECOMMENDATION                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  SHORT-TERM (Go-Live): Retain Paradox Integration                           │
│  ─────────────────────────────────────────────────                          │
│                                                                             │
│  Rationale:                                                                 │
│  • High-volume recruiting (250K+ applications) needs proven campaign tool  │
│  • SMS capability critical for frontline/hourly recruiting                 │
│  • Sophie chatbot handling significant candidate volume                    │
│  • Change management complexity - minimize for go-live                     │
│  • UKG Americas team already trained on Paradox                            │
│                                                                             │
│  Integration Points:                                                        │
│  • Oracle → Paradox: New candidates, status updates                        │
│  • Paradox → Oracle: Application data, interview confirmations             │
│  • Sync frequency: Every 15 minutes (current UKG setup)                    │
│                                                                             │
│  ─────────────────────────────────────────────────────────────────────────  │
│                                                                             │
│  MEDIUM-TERM (6-12 months): Evaluate Oracle Recruiting Booster              │
│  ─────────────────────────────────────────────────────────────              │
│                                                                             │
│  Decision Criteria:                                                         │
│  • Booster campaign functionality maturity                                 │
│  • SMS capabilities (via Oracle Digital Assistant)                         │
│  • Cost comparison: Booster license vs Paradox license                     │
│  • Single system simplification benefits                                   │
│  • Global deployment requirements                                          │
│                                                                             │
│  ─────────────────────────────────────────────────────────────────────────  │
│                                                                             │
│  LONG-TERM (12+ months): Consolidate to Single Platform                     │
│  ───────────────────────────────────────────────────────                    │
│                                                                             │
│  If Oracle Recruiting Booster meets requirements:                          │
│  • Phase out Paradox                                                       │
│  • Migrate campaign templates                                              │
│  • Retrain recruiters                                                      │
│  • Simplify integration architecture                                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 10. GEODIS-Specific Configuration

### 10.1 7-Day Internal Posting Rule

```
WORKFLOW RULE: INTERNAL_POSTING_FIRST

Trigger: Requisition status = APPROVED

Action:
  1. Create internal job posting (visibility: Internal only)
  2. Set posting start date = Today
  3. Set posting end date = Today + 7 days
  4. Schedule external posting creation = Today + 7 days
  5. Notification to Hiring Manager: "Internal posting active for 7 days"

At Day 7:
  1. Create external job postings (Indeed, LinkedIn, Career Site)
  2. Maintain internal posting (concurrent)
  3. Notification: "External posting now active"

Override Process:
  IF urgent_hiring_flag = Y:
    1. Require HRBP approval for override
    2. If approved: Create external posting immediately
    3. Add audit note: "7-day rule overridden - [reason]"
```

### 10.2 High-Value Approval Thresholds

| Threshold | Amount (EUR) | Applies To | Additional Approver |
|-----------|--------------|------------|---------------------|
| Standard | < 125,000 | Base salary | None |
| High Salary | ≥ 125,000 | Base salary | EVP HR |
| High Total | ≥ 155,000 | Total compensation | EVP HR |
| TOPEX | Any | Executive positions | CHRO |

### 10.3 6-Month Auto-Close Rule

```
SCHEDULED JOB: REQUISITION_AGE_CHECK (Daily at 6 AM)

Logic:
  FOR each requisition WHERE status = 'OPEN':

    days_open = SYSDATE - APPROVED_DATE

    IF days_open = 150 (5 months):
      Send WARNING notification to Recruiter, HM, HRBP
      "Requisition will auto-close in 30 days unless extended"

    IF days_open = 165:
      Send SECOND WARNING
      Prompt for extension request

    IF days_open = 180 AND no_extension_approved:
      Set status = CLOSED
      Set close_reason = 'AUTO_CLOSED_6_MONTH_RULE'
      Move all active candidates to POOLED
      Send notification: "Requisition auto-closed per 6-month rule"

    IF extension_approved:
      Reset days_open tracking
      Set extension_flag = Y
      Set new_close_date = APPROVED_DATE + extension_days
```

### 10.4 Requisition Template by Region

| Template | Region | Special Fields | Approval Path |
|----------|--------|----------------|---------------|
| GEODIS_STD | Global | Standard fields | Standard |
| GEODIS_FR | France | French labor law fields, CDI/CDD | + Works Council |
| GEODIS_US | USA | EEO/OFCCP, Pay Transparency | Standard |
| GEODIS_DE | Germany | Betriebsrat fields | + Works Council |
| GEODIS_NL | Netherlands | CAO fields | Standard |
| GEODIS_EXEC | Global | Executive fields, confidential | TOPEX path |
| GEODIS_INTERN | Global | Internship fields, school info | Simplified |

---

## 11. Implementation Checklist

### 11.1 Pre-Configuration Tasks

- [ ] Define all phases and states (use existing 12-phase model)
- [ ] Document state transitions and rules
- [ ] Map actors to Oracle security roles
- [ ] Design approval workflows (BPM)
- [ ] Create email templates (25+ templates)
- [ ] Define correspondence rules

### 11.2 Setup and Maintenance Configuration

- [ ] Create requisition templates (5 templates)
- [ ] Configure candidate selection process
- [ ] Set up phases and states
- [ ] Configure allowed transitions
- [ ] Create value sets for lookups
- [ ] Configure flexfields (18 DFFs)

### 11.3 Approval Workflow Configuration

- [ ] Create requisition approval policy
- [ ] Create offer approval policy
- [ ] Define approval chains by threshold
- [ ] Configure escalation rules
- [ ] Enable email approval
- [ ] Test approval routing

### 11.4 Correspondence and Notifications

- [ ] Create email templates
- [ ] Configure correspondence rules
- [ ] Set up scheduled alerts
- [ ] Test email delivery
- [ ] Configure SMS (if using)

### 11.5 Campaign Configuration

- [ ] Decision: Paradox integration vs Oracle Booster
- [ ] If Paradox: Configure integration
- [ ] If Booster: License and configure
- [ ] Create campaign templates
- [ ] Test campaign workflows

### 11.6 Testing

- [ ] End-to-end requisition workflow test
- [ ] End-to-end candidate workflow test
- [ ] Approval workflow test (all paths)
- [ ] Notification delivery test
- [ ] Campaign functionality test
- [ ] Integration test (Paradox/job boards)

---

## Document Information

| Attribute | Value |
|-----------|-------|
| Document ID | 17_Oracle_Recruiting_Workflow_Configuration_Guide |
| Version | 1.0 |
| Created | 2025-12-07 |
| Total Phases | 12 (+ 4 terminal) |
| Total States | 43 |
| Approval Workflows | 2 (Requisition, Offer) |
| Email Templates | 25+ |

---

*End of Document*
