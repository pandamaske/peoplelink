# Oracle HCM Cloud Approval Workflows Specification

## Document Purpose

**Project:** GEODIS New HCM - AMARIS
**Document Type:** Approval Workflow Requirements
**Status:** DRAFT
**Last Updated:** 2025-12-06
**Version:** 1.0

---

## Executive Summary

This document specifies the approval workflows required for the Oracle HCM Cloud implementation at GEODIS. It covers all HR processes requiring approval chains, mapped from current G-Talent+ and HR Blueprint requirements to Oracle BPM workflow configurations.

---

## Approval Framework Overview

### Oracle Approval Components

| Component | Description | Use Case |
|-----------|-------------|----------|
| **BPM Workflow** | Business Process Management engine | Complex multi-level approvals |
| **Approval Rules** | Configurable approval conditions | Define who approves what |
| **Approval Groups** | Collections of approvers | HR team, management chain |
| **Routing Rules** | Logic for approval path | Hierarchy, position-based |
| **Notifications** | Email/Bell alerts | Approval requests, reminders |

### Approval Pattern Types

| Pattern | Description | Oracle Configuration |
|---------|-------------|---------------------|
| **Supervisory** | Manager hierarchy chain | Management Chain routing |
| **Position-Based** | Specific positions approve | Position Hierarchy |
| **Job-Based** | Based on job level/grade | Job Level rules |
| **Amount-Based** | Threshold triggers approval | Amount-based conditions |
| **HR Validation** | HR must validate | Include HR in chain |

---

## 1. Recruitment Approval Workflows

### 1.1 Job Requisition Approval

**Current State (G-Talent+):** Vacancy Request → N+1 Approval → HR Review → Recruiter Action

**Oracle Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│ Hiring Manager  │────▶│   N+1 Manager   │────▶│   HR Business   │────▶│    Recruiter    │
│ Creates Req     │     │   Approves      │     │   Partner       │     │   Posts Job     │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
                                                        │
                                                        ▼ (if salary > €125k)
                                                ┌─────────────────┐
                                                │    EVP HR       │
                                                │   Approves      │
                                                └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver | Sequence |
|---------|-----------|----------|----------|
| REQ-001 | All requisitions | N+1 (Supervisor) | 1 |
| REQ-002 | All requisitions | HR Business Partner | 2 |
| REQ-003 | Salary >= €125,000 | EVP HR | 3 |
| REQ-004 | TOPEX Position | CHRO | 3 |

**Oracle Configuration:**

| Setting | Value |
|---------|-------|
| Transaction | Create Requisition |
| Approval Task | IRC_REQUISITION_APPROVAL |
| Routing Type | Parallel for same sequence, Serial across sequences |
| Auto-Approve | No |
| Expiration | 7 days, then escalate |

### 1.2 Job Offer Approval

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Recruiter    │────▶│ Hiring Manager  │────▶│   HR / Comp     │
│  Creates Offer  │     │   Approves      │     │   Validates     │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                                        │
                                                        ▼ (if above threshold)
                                                ┌─────────────────┐
                                                │   EVP HR        │
                                                └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver | Sequence |
|---------|-----------|----------|----------|
| OFR-001 | All offers | Hiring Manager | 1 |
| OFR-002 | All offers | HR/Compensation | 2 |
| OFR-003 | Total Package >= €155,000 | CnB Director notification | 2 |
| OFR-004 | Base Salary >= €125,000 | EVP HR | 3 |

---

## 2. Performance Management Approval Workflows

### 2.1 Performance Document Approval

**Current State (G-Talent+):** Employee Self-Assessment → Manager Evaluation → Validation Meeting → Sign-off

**Oracle Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Employee     │────▶│    Manager      │────▶│   Share with    │────▶│    Complete     │
│ Self-Evaluation │     │   Evaluation    │     │   Employee      │     │   Document      │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
```

**Process Flow Configuration:**

| Step | Task | Actor | Required |
|------|------|-------|----------|
| 1 | Set Goals | Manager + Employee | Yes |
| 2 | Worker Self-Evaluation | Employee | Yes |
| 3 | Manager Evaluation | Manager | Yes |
| 4 | Share | Manager | Yes |
| 5 | Provide Feedback | Employee | Optional |
| 6 | Complete | Manager | Yes |

**Approval Rules:**

| Rule ID | Condition | Action | Notes |
|---------|-----------|--------|-------|
| PRF-001 | Self-evaluation complete | Route to Manager | Automatic |
| PRF-002 | Manager evaluation complete | Enable Share | Sequential |
| PRF-003 | All sections rated | Enable Complete | Validation |

### 2.2 Goal Approval

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Employee     │────▶│    Manager      │────▶│     Goal        │
│  Creates Goal   │     │   Approves      │     │    Active       │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver | Auto-Approve |
|---------|-----------|----------|--------------|
| GOL-001 | Employee creates goal | Direct Manager | No |
| GOL-002 | Manager creates for employee | No approval | Yes |
| GOL-003 | Goal weight change | Direct Manager | No |

---

## 3. Compensation Approval Workflows

### 3.1 Salary Review (Workforce Compensation)

**Current State (G-Talent+):** Manager Proposal → N+1 Review → HR Approval → Final

**Oracle Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Manager      │────▶│   N+1 Manager   │────▶│  HR / CnB       │────▶│    Approved     │
│   Proposes      │     │   Validates     │     │   Final         │     │   & Applied     │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
                                                        │
                                                        ▼ (if > guideline)
                                                ┌─────────────────┐
                                                │    EVP HR       │
                                                └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver | Sequence |
|---------|-----------|----------|----------|
| SAL-001 | All salary changes | N+1 Manager | 1 |
| SAL-002 | All salary changes | HR/CnB | 2 |
| SAL-003 | Increase > guideline max | EVP HR | 3 |
| SAL-004 | New salary >= €125,000 | EVP HR | 3 |
| SAL-005 | TOPEX employee | CHO | 3 |

**Budget Controls:**

| Control | Configuration |
|---------|---------------|
| Budget Pool | By organization unit |
| Spending Limit | Cannot exceed allocated budget |
| Guideline Enforcement | Warning if outside range |

### 3.2 Ad-Hoc Salary Change (Outside Cycle)

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Manager /     │────▶│   N+1 Manager   │────▶│      HR         │────▶│    Approved     │
│      HR         │     │                 │     │   Validates     │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver |
|---------|-----------|----------|
| ADH-001 | Promotion | N+1 + HR |
| ADH-002 | Retention | N+1 + HR + EVP HR |
| ADH-003 | Market adjustment | HR + EVP HR |

---

## 4. Employee Lifecycle Approval Workflows

### 4.1 Hire (from Recruiting)

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  Offer Accepted │────▶│  HR Processes   │────▶│  Employee       │
│                 │     │  Hire Action    │     │  Created        │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver | Notes |
|---------|-----------|----------|-------|
| HIR-001 | Standard hire | No additional approval | Offer already approved |
| HIR-002 | Contingent worker | HR approval | Different worker type |

### 4.2 Transfer

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│ Current Manager │────▶│ Receiving Mgr   │────▶│      HR         │────▶│   Transfer      │
│   Initiates     │     │   Approves      │     │   Validates     │     │   Effective     │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver | Sequence |
|---------|-----------|----------|----------|
| TRF-001 | All transfers | Receiving Manager | 1 |
| TRF-002 | All transfers | HR | 2 |
| TRF-003 | Cross-country transfer | IM Coordinator | 2 |
| TRF-004 | Cross-LoB transfer | Both LoB HR | 2 |

### 4.3 Promotion

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Manager      │────▶│   N+1 Manager   │────▶│      HR         │────▶│   Promotion     │
│   Proposes      │     │   Approves      │     │   Validates     │     │   Effective     │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver | Notes |
|---------|-----------|----------|-------|
| PRO-001 | All promotions | N+1 Manager | Required |
| PRO-002 | All promotions | HR | Manager cannot approve alone |
| PRO-003 | To TOPEX level | CHRO | Executive approval |
| PRO-004 | With salary increase | Follow SAL rules | Combined workflow |

### 4.4 Termination

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Manager      │────▶│      HR         │────▶│  Termination    │
│   Initiates     │     │   Validates     │     │   Processed     │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                │
                                ▼ (if involuntary)
                        ┌─────────────────┐
                        │  HR Director    │
                        │  (major cases)  │
                        └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver | Notes |
|---------|-----------|----------|-------|
| TRM-001 | Voluntary resignation | HR validation | No approval needed |
| TRM-002 | Involuntary - performance | HR + HRD | Documentation required |
| TRM-003 | Involuntary - misconduct | HR + HRD + Legal | Legal review |
| TRM-004 | Restructuring | HR + HRD + EVP HR | Mass action |

---

## 5. Talent Management Approval Workflows

### 5.1 Succession Plan Updates

**Approval Rules:**

| Rule ID | Condition | Approver |
|---------|-----------|----------|
| SUC-001 | Add successor | HR + Position Owner |
| SUC-002 | Remove successor | HR |
| SUC-003 | Change readiness | HR |

### 5.2 Talent Pool Membership

**Approval Rules:**

| Rule ID | Condition | Approver |
|---------|-----------|----------|
| TPL-001 | Add to High Potential pool | HR + Manager + Talent Committee |
| TPL-002 | Remove from pool | HR + Talent Committee |

---

## 6. Learning Approval Workflows

### 6.1 Training Request

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Employee     │────▶│    Manager      │────▶│    Enrolled     │
│   Requests      │     │   Approves      │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                │
                                ▼ (if cost > threshold)
                        ┌─────────────────┐
                        │      HR         │
                        └─────────────────┘
```

**Approval Rules:**

| Rule ID | Condition | Approver |
|---------|-----------|----------|
| LRN-001 | Internal training | Manager auto-approve or approve |
| LRN-002 | External training | Manager + HR |
| LRN-003 | Cost > threshold | Manager + HR + Finance |
| LRN-004 | Leadership program | HR + University approval |

---

## 7. Leave / Absence Approval Workflows

### 7.1 Leave Request

**Workflow Design:**

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Employee     │────▶│    Manager      │────▶│     Leave       │
│   Requests      │     │   Approves      │     │    Approved     │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

**Approval Rules (US Specific from Zendesk):**

| Rule ID | Condition | Approver |
|---------|-----------|----------|
| LVE-001 | PTO / Vacation | Direct Manager |
| LVE-002 | PLOA (Personal Leave) | Manager + HRD |
| LVE-003 | MLOA (Medical Leave) | HR + VOYA integration |
| LVE-004 | FMLA | HR (VOYA determines eligibility) |

---

## 8. Document & Data Approval Workflows

### 8.1 Employee Data Change

**Approval Rules:**

| Rule ID | Data Type | Approver |
|---------|-----------|----------|
| DAT-001 | Personal data (self-service) | No approval |
| DAT-002 | Bank details | HR verification |
| DAT-003 | Emergency contacts | No approval |
| DAT-004 | Assignment data | HR |

### 8.2 Document Records

**Approval Rules:**

| Rule ID | Document Type | Approver |
|---------|--------------|----------|
| DOC-001 | ID documents | HR verification |
| DOC-002 | Contracts | HR |
| DOC-003 | Certifications | Manager or HR |

---

## 9. Approval Configuration Summary

### 9.1 Approval Groups to Create

| Group Name | Members | Used For |
|------------|---------|----------|
| HR Business Partners | Regional HRBPs | General HR approvals |
| Compensation Team | CnB specialists | Salary approvals |
| Talent Acquisition | Recruiters, TA leads | Recruiting approvals |
| Executive HR | EVP HR, CHRO, CHO | High-value approvals |
| IM Coordinators | International Mobility team | Global transfers |
| Talent Committee | HR + Business leaders | Talent pool decisions |

### 9.2 Notification Templates Required

| Template | Trigger | Recipients |
|----------|---------|------------|
| Approval Request | New approval needed | Approver |
| Approval Reminder | 3 days pending | Approver |
| Escalation Notice | 7 days pending | Approver + Manager |
| Approval Complete | Approved/Rejected | Initiator |
| FYI Notification | Threshold crossed | Stakeholders |

### 9.3 Delegation Rules

| Rule | Configuration |
|------|---------------|
| Vacation delegation | Allow approvers to delegate |
| Escalation | Auto-escalate after 7 days |
| Proxy approval | HR can act on behalf if needed |

---

## 10. Implementation Checklist

| # | Task | Module | Priority |
|---|------|--------|----------|
| 1 | Configure Requisition approval rules | Recruiting | High |
| 2 | Configure Offer approval rules | Recruiting | High |
| 3 | Configure Performance process flow | Performance | High |
| 4 | Configure Salary Review approvals | Compensation | High |
| 5 | Configure Transfer/Promotion approvals | Core HR | High |
| 6 | Configure Termination approvals | Core HR | High |
| 7 | Create Approval Groups | Foundation | High |
| 8 | Configure Notification templates | Foundation | Medium |
| 9 | Configure Delegation rules | Foundation | Medium |
| 10 | Test approval scenarios | All | High |

---

## Document Control

| Attribute | Value |
|-----------|-------|
| File Path | `02 - Define/01 - Repositories/00 - Documentation/22_Oracle_HCM_Approval_Workflows.md` |
| Created | 2025-12-06 |
| Author | HCM Implementation Agent |
| Review Status | Draft - Requires stakeholder validation |

---

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-06 | Initial approval workflows specification |

---

*This document requires validation with GEODIS HR stakeholders and Oracle implementation team.*
