# Oracle HCM Cloud Configuration Specifications

## Document Purpose

**Project:** GEODIS New HCM - AMARIS
**Document Type:** Configuration Specifications
**Status:** DRAFT
**Last Updated:** 2025-12-06
**Version:** 1.0

---

## Executive Summary

This document provides detailed configuration specifications for Oracle HCM Cloud implementation at GEODIS. It covers all modules in scope with specific configuration decisions, values, and implementation notes.

---

## Configuration Overview

### Modules in Scope

| Module | Priority | Phase |
|--------|----------|-------|
| Global Human Resources (Core HR) | P1 | 1 |
| Oracle Recruiting | P1 | 1 |
| Performance Management | P1 | 1 |
| Goal Management | P1 | 1 |
| Workforce Compensation | P1 | 1 |
| Talent Review & Succession | P2 | 1 |
| Oracle Learning | P2 | 1 |
| Journeys | P2 | 1 |
| Absence Management | P2 | 1 |
| Analytics (OTBI) | P2 | 1 |

---

## 1. Enterprise Structure Configuration

### 1.1 Enterprise Definition

| Configuration | Value | Notes |
|---------------|-------|-------|
| Enterprise Name | GEODIS | Global enterprise |
| Base Language | English (US) | Primary language |
| Additional Languages | French, German, Spanish, Portuguese | Per country needs |
| Calendar | Gregorian | Standard |
| Currency | EUR (Base), USD, GBP, etc. | Per country |

### 1.2 Legal Employer Structure

| Legal Employer | Country | Legislation | Payroll |
|----------------|---------|-------------|---------|
| GEODIS SA | France | FR | Local Integration |
| GEODIS USA Inc | United States | US | Local Integration |
| GEODIS UK Ltd | United Kingdom | GB | Local Integration |
| GEODIS Germany GmbH | Germany | DE | Local Integration |
| (Additional per country) | ... | ... | ... |

### 1.3 Business Unit Structure

| Business Unit | Description | Manager Level |
|---------------|-------------|---------------|
| GEODIS Global | Corporate functions | EVP |
| GEODIS Freight Forwarding | Freight business line | SVP |
| GEODIS Supply Chain | Supply chain business line | SVP |
| GEODIS Distribution & Express | Distribution business line | SVP |
| GEODIS Road Transport | Road transport business line | SVP |

### 1.4 Department Hierarchy

| Configuration | Value |
|---------------|-------|
| Hierarchy Type | Department Tree |
| Top Level | Enterprise |
| Levels | Country → Region → Business Unit → Department |
| Manager Assignment | By position |

### 1.5 Location Configuration

| Configuration | Value |
|---------------|-------|
| Location Set | GEODIS Global Locations |
| Address Style | By country legislation |
| Time Zone | Per location |
| Work Schedule | Per location |

---

## 2. Core HR Configuration

### 2.1 Person Types

| Person Type | Category | Use Case |
|-------------|----------|----------|
| Employee | Employee | Regular employees |
| Contingent Worker | Contingent | Contractors, temps |
| Pending Worker | Pending Worker | Pre-boarding |
| Non-Worker | Non-Worker | Board members, external |

### 2.2 Assignment Categories

| Category | Description | FTE Calculation |
|----------|-------------|-----------------|
| Full-Time Regular | Permanent full-time | 1.0 |
| Part-Time Regular | Permanent part-time | Hours / Standard |
| Full-Time Temporary | Fixed-term full-time | 1.0 |
| Part-Time Temporary | Fixed-term part-time | Hours / Standard |
| Contingent | Non-employee workers | N/A |

### 2.3 Action Types

| Action | Action Type | Reason Codes Required |
|--------|------------|----------------------|
| Hire | Add Assignment | Yes |
| Rehire | Add Assignment | Yes |
| Promotion | Change Assignment | Yes |
| Transfer | Change Assignment | Yes |
| Demotion | Change Assignment | Yes |
| Salary Change | Change Assignment | Yes |
| Termination | End Assignment | Yes (see term reasons) |
| Global Transfer | Global Transfer | Yes |

### 2.4 Termination Reasons (from Zendesk US)

**Voluntary Reasons:**

| Reason Code | Description | Rehire Eligible |
|-------------|-------------|-----------------|
| VOL_LOA_NO_RETURN | Did not return from LOA | Yes |
| VOL_HOURS | Dissatisfied - Hours | Yes |
| VOL_MGMT | Dissatisfied - Management | Yes |
| VOL_DUTIES | Dissatisfied - Job Duties | Yes |
| VOL_PAY | Dissatisfied - Pay | Yes |
| VOL_EDUCATION | Education | Yes |
| VOL_JOB_ABANDON | Job Abandonment NC/NS | No |
| VOL_MOVING | Moving | Yes |
| VOL_MUTUAL | Mutual Agreement | Yes |
| VOL_NO_REASON | No Reason Given | Yes |
| VOL_OTHER_JOB | Other Job | Yes |
| VOL_PERSONAL | Personal/Family | Yes |
| VOL_RETIREMENT | Retirement | Yes |
| VOL_WALKOUT | Quit No Notice - Walk Out | No |

**Involuntary Reasons:**

| Reason Code | Description | Rehire Eligible |
|-------------|-------------|-----------------|
| INV_PERFORMANCE | Cannot Perform Duties | Yes |
| INV_ATTENDANCE | Excessive Absences/Tardiness | No |
| INV_DEATH | Death | N/A |
| INV_I9_FAILURE | Failed to Meet I-9 Requirements | Yes |
| INV_MISCONDUCT | Gross Misconduct | No |
| INV_LEAVE_INELIG | Ineligible for Leave | Yes |
| INV_PERFORMANCE | Performance | No |
| INV_DRUG | Policy - Drug Free Workplace | No |
| INV_HARASSMENT | Policy - Harassment | No |
| INV_POLICY_MISC | Policy - Misc. | No |
| INV_SAFETY | Policy - Safety | No |
| INV_VIOLENCE | Policy - Workplace Violence | No |
| INV_RIF | Reduction in Work Force | Yes |
| INV_TEMP_END | Temporary Job Ended | Yes |
| INV_THEFT | Theft | No |

### 2.5 Flexfield Configuration

**Person Descriptive Flexfield (DFF):**

| Context | Segment | Data Type | Required |
|---------|---------|-----------|----------|
| Global | Employee Population | List (Blue Collar, White Collar, TOPEX) | Yes |
| Global | GDPR Consent Date | Date | No |
| Global | Previous System ID | Text | No |
| US | Veteran Status | List | No |
| US | Disability Status | List | No |

**Assignment Descriptive Flexfield:**

| Context | Segment | Data Type | Required |
|---------|---------|-----------|----------|
| Global | Cost Center | Text | Yes |
| Global | Project Code | Text | No |
| Global | Work Authorization Expiry | Date | No |

### 2.6 Document Types

| Document Category | Document Type | Required |
|-------------------|---------------|----------|
| Personal | Passport | No |
| Personal | National ID | Per country |
| Personal | Driver License | Job dependent |
| Work Authorization | Work Permit | Non-citizens |
| Work Authorization | Visa | Non-citizens |
| Employment | Employment Contract | Yes |
| Employment | Offer Letter | Yes |
| Compliance | Background Check | Pre-hire |
| Compliance | I-9 Form | US only |

---

## 3. Recruiting Configuration

### 3.1 Requisition Configuration

| Configuration | Value |
|---------------|-------|
| Requisition Numbering | Auto-generated (REQ-YYYY-NNNNN) |
| Default Template | GEODIS Standard Requisition |
| Approval Required | Yes (see workflow spec) |
| Clone Enabled | Yes |
| Phase Configuration | Draft → Open → Filled → Closed |

### 3.2 Requisition Template

| Section | Fields | Visible |
|---------|--------|---------|
| Basic Information | Title, Department, Location, Manager | Yes |
| Job Details | Job Code, Grade, FTE | Yes |
| Compensation | Salary Range, Currency | Restricted |
| Requirements | Skills, Experience, Education | Yes |
| Posting | Internal/External, Duration | Yes |
| GEODIS Custom | Cost Center, Budget Code, Population Type | Yes |

### 3.3 Job Posting Configuration

| Configuration | Value |
|---------------|-------|
| Career Site | GEODIS Careers (branded) |
| Internal Posting Duration | Minimum 7 days before external |
| External Channels | LinkedIn, Indeed (evaluate native vs Broadbean) |
| Application Questions | Configurable questionnaires |
| Referral Program | Enable employee referrals |

### 3.4 Candidate Phases & States

| Phase | States | Auto-Progress |
|-------|--------|---------------|
| New | New, Review | No |
| Screen | Phone Screen, Shortlisted, Rejected | No |
| Interview | Scheduled, Completed, Passed, Failed | No |
| Offer | Draft, Pending Approval, Extended, Accepted, Declined | Partial |
| Hire | Ready to Hire, Hired | Yes (to HR) |

### 3.5 Offer Configuration

| Configuration | Value |
|---------------|-------|
| Offer Letter Templates | By country/job family |
| Approval Required | Yes (see workflow spec) |
| Electronic Signature | Enable DocuSign/equivalent |
| Offer Expiration | 7 days default |
| Counter Offer | Allow |

### 3.6 Candidate Pool Configuration

| Pool Type | Purpose | Retention |
|-----------|---------|-----------|
| Silver Medalists | Runner-up candidates | 12 months |
| Talent Community | General interest | 24 months (GDPR) |
| Speculative Applications | Unsolicited applications | 12 months |
| Internal Mobility | Internal candidates | Ongoing |

---

## 4. Performance Management Configuration

### 4.1 Rating Model - GEODIS Performance Rating

| Level | Short Name | Description | Numeric Value |
|-------|------------|-------------|---------------|
| 1 | Significantly Below | Does not meet expectations (<50%) | 1 |
| 2 | Below | Partially meets expectations (50-80%) | 2 |
| 3 | Meets | Meets expectations (80-100%) | 3 |
| 4 | Exceeds | Exceeds expectations (100-120%) | 4 |
| 5 | Far Exceeds | Significantly exceeds expectations (>120%) | 5 |

### 4.2 Performance Template - Annual Review

| Section | Section Type | Weight | Rating Model |
|---------|--------------|--------|--------------|
| Previous Year Objectives | Performance Goals | 40% | GEODIS Performance Rating |
| Competencies | Competencies | 30% | GEODIS Performance Rating |
| Values | Competencies (Values) | 15% | GEODIS Performance Rating |
| Development Goals | Development Goals | 15% | N/A |
| Career Discussion | Questionnaire | N/A | N/A |
| Overall Summary | Overall | 100% | GEODIS Performance Rating |

### 4.3 Document Types

| Document Type | Purpose | Period |
|---------------|---------|--------|
| Annual Performance Review | Full annual appraisal | January - December |
| Mid-Year Check-In | Interim review | July |
| Probation Review | End of probation | Variable |

### 4.4 Process Flow Configuration

| Step | Task | Participant | Due Date |
|------|------|-------------|----------|
| 1 | Set Goals | Manager + Worker | January 31 |
| 2 | Mid-Year Review | Manager + Worker | July 31 |
| 3 | Worker Self-Evaluation | Worker | March 15 |
| 4 | Manager Evaluation | Manager | March 31 |
| 5 | Share with Worker | Manager | April 15 |
| 6 | Acknowledge | Worker | April 30 |
| 7 | Complete | Manager | April 30 |

### 4.5 Eligibility Rules

| Rule | Criteria |
|------|----------|
| Annual Review | Active employees with 3+ months tenure |
| Mid-Year | Active employees with annual review |
| Probation | Employees in probation period |
| Exclude | Employees on long-term leave, terminating |

### 4.6 Competency Model

**Core Competencies:**

| Competency | Description | Applicable To |
|------------|-------------|---------------|
| Customer Focus | Delivers excellent customer service | All |
| Teamwork | Collaborates effectively | All |
| Communication | Communicates clearly | All |
| Problem Solving | Analyzes and resolves issues | All |
| Adaptability | Adapts to change | All |

**Leadership Competencies (Managers):**

| Competency | Description | Applicable To |
|------------|-------------|---------------|
| People Development | Develops team members | Managers |
| Strategic Thinking | Plans for future | Managers |
| Decision Making | Makes timely decisions | Managers |
| Change Leadership | Leads through change | Managers |

**GEODIS Values:**

| Value | Description |
|-------|-------------|
| Commitment | Dedicated to success |
| Innovation | Drives continuous improvement |
| Trust | Acts with integrity |
| Excellence | Strives for quality |
| Solidarity | Supports colleagues |

---

## 5. Goal Management Configuration

### 5.1 Goal Plan Configuration

| Configuration | Value |
|---------------|-------|
| Goal Plan Name | GEODIS Annual Goals |
| Review Period | January 1 - December 31 |
| Goal Types | Performance, Development |
| Weighting | Enable (total = 100%) |
| Alignment | Enable cascading |

### 5.2 Goal Library

| Category | Example Goals |
|----------|---------------|
| Financial | Revenue targets, cost reduction |
| Customer | NPS improvement, retention |
| Process | Efficiency, quality metrics |
| People | Training, engagement |

### 5.3 Goal Approval

| Configuration | Value |
|---------------|-------|
| Employee Creates | Manager approval required |
| Manager Creates | No approval |
| Weight Changes | Manager approval |

---

## 6. Workforce Compensation Configuration

### 6.1 Compensation Plan

| Configuration | Value |
|---------------|-------|
| Plan Name | GEODIS Annual Salary Review |
| Cycle | Annual (April effective) |
| Budget Type | By organization |
| Currency | Local currency |
| Guidelines | Enable min/max % |

### 6.2 Salary Basis

| Salary Basis | Annualization | Countries |
|--------------|---------------|-----------|
| Annual Salary | 1 | Most countries |
| Monthly Salary | 12 | France, Germany |
| Hourly Rate | 2080 | US hourly |

### 6.3 Compensation Components

| Component | Type | Eligibility |
|-----------|------|-------------|
| Base Salary | Salary | All |
| Annual Bonus | Bonus | White Collar, TOPEX |
| LTIP | Long-Term Incentive | TOPEX only |
| Sign-on Bonus | One-time | Per approval |

### 6.4 Approval Thresholds

| Threshold | Approver |
|-----------|----------|
| Standard increase | N+1 + HR |
| Above guideline | + EVP HR |
| >= €125,000 base | + EVP HR |
| TOPEX | + CHO |

---

## 7. Talent Review & Succession Configuration

### 7.1 Talent Review Meeting

| Configuration | Value |
|---------------|-------|
| Meeting Template | GEODIS People Review |
| Review Period | May - October |
| Population | Managers + High Potentials |
| Matrix Type | 9-Box (Performance x Potential) |

### 7.2 Talent Categories

| Category | Criteria |
|----------|----------|
| High Potential | Top performance + high potential |
| Key Talent | Critical skills/knowledge |
| Core Contributor | Solid performer |
| Emerging Talent | Early career high potential |

### 7.3 Succession Plan

| Configuration | Value |
|---------------|-------|
| Plan Types | Key Position, Talent Pool |
| Readiness Levels | Ready Now, 1-2 Years, 3+ Years |
| Visibility | HR + Position Owner |

---

## 8. Learning Configuration

### 8.1 Learning Catalog

| Category | Content Source |
|----------|----------------|
| Compliance | Oracle Learning (migrate from G-Campus) |
| Onboarding | Oracle Learning |
| Leadership | GEODIS University |
| Technical | External providers |
| E-Learning | Oracle Learning Cloud (migrate from G-Learning) |

### 8.2 Learning Assignments

| Type | Trigger |
|------|---------|
| Required | New hire, compliance renewal |
| Recommended | Development plan |
| Self-Enrolled | Employee choice |

### 8.3 Completion Tracking

| Configuration | Value |
|---------------|-------|
| Completion Certificate | Enable |
| Manager Notification | On completion |
| Compliance Tracking | Enable with expiration |

---

## 9. Journeys Configuration

### 9.1 Journey Categories

| Category | Use Case |
|----------|----------|
| Enterprise Onboarding | New hire onboarding |
| Offboarding | Employee exit |
| Contextual - Transfer | Transfer process |
| Contextual - Promotion | Promotion process |
| Lifecycle | Career milestones |

### 9.2 Onboarding Journey Template

| Task Group | Tasks |
|------------|-------|
| Pre-Day 1 | Complete personal info, emergency contacts, bank details |
| Day 1 | Review policies, sign documents, IT setup |
| Week 1 | Meet team, complete compliance training |
| First 30 Days | Complete onboarding training, meet buddy |
| First 90 Days | Complete probation review |

### 9.3 Exit Journey Template

| Task Group | Tasks |
|------------|-------|
| Notice Period | Knowledge transfer, handover documentation |
| Manager Tasks | Conduct exit interview (mandatory for managers) |
| HR Tasks | Final pay, benefits termination |
| IT Tasks | Access revocation (via Service Now) |
| Last Day | Return equipment, final clearance |

### 9.4 Journey Allocation Rules

| Rule | Trigger | Population |
|------|---------|------------|
| Onboarding | New hire action | All new employees |
| Exit | Termination action | All terminating employees |
| Transfer | Transfer action | All transfers |
| Promotion | Promotion action | All promotions |

---

## 10. Absence Management Configuration

### 10.1 Absence Types

| Absence Type | Legislation | Accrual |
|--------------|-------------|---------|
| Annual Leave | All | Yes |
| Sick Leave | All | Per country |
| FMLA | US | No |
| PLOA | US | No |
| Maternity | All | Per country |
| Paternity | All | Per country |
| Bereavement | All | No |
| Jury Duty | All | No |

### 10.2 Absence Approval

| Configuration | Value |
|---------------|-------|
| Standard Leave | Manager approval |
| Extended Leave (PLOA) | Manager + HRD |
| Medical Leave | Manager + HR |
| FMLA | HR (VOYA determination) |

---

## 11. Analytics & Reporting Configuration

### 11.1 OTBI Dashboards Required

| Dashboard | Purpose | Audience |
|-----------|---------|----------|
| HR Executive | Key HR metrics | HR Leadership |
| Workforce Analytics | Headcount, FTE, demographics | HR, Managers |
| Recruiting Analytics | Req status, time to fill | TA Team |
| Performance Analytics | Completion rates, distribution | HR, Managers |
| Compensation Analytics | Budget tracking, increase analysis | Comp Team |
| Learning Analytics | Completion rates, hours | Learning Team |

### 11.2 Custom Reports Required

| Report | Formula/Logic | Frequency |
|--------|---------------|-----------|
| FTE Report | Period-end and average FTE | Monthly |
| Turnover Report | Leavers / Avg Headcount × 100 | Monthly |
| Frequency Rate | Accidents × 1M / Hours Worked | Quarterly |
| Severity Rate | Days Lost × 1K / Hours Worked | Quarterly |
| Absenteeism | Days Absent / Work Days × 100 | Monthly |
| Data Quality | Missing mandatory fields % | Weekly |

---

## 12. Security Configuration

### 12.1 Role Mapping

| G-Talent+ Role | Oracle Role | Data Access |
|----------------|-------------|-------------|
| Employee | Employee | Own data |
| Manager | Line Manager | Direct reports |
| HR Local | HR Specialist | Country/Region |
| HR Global | Human Resource Analyst | Enterprise |
| Recruiter | Recruiter | Assigned requisitions |
| Compensation | Compensation Analyst | Compensation plans |
| HRIS Admin | Human Resource Specialist | All HR data |

### 12.2 Data Security

| Configuration | Value |
|---------------|-------|
| Security Profile | Position-based |
| Organization Access | By hierarchy |
| Manager Hierarchy | Include matrix managers |
| HR Access | By country/region assignment |

---

## 13. Integration Configuration

### 13.1 Inbound Integrations

| Source | Data | Frequency | Method |
|--------|------|-----------|--------|
| Recruiting | New hires | Real-time | Internal |
| Payroll | Pay results | Per pay period | HCM Data Loader |
| Time & Attendance | Hours worked | Daily | REST API |

### 13.2 Outbound Integrations

| Target | Data | Frequency | Method |
|--------|------|-----------|--------|
| Minerve+ | Employee, Comp | Real-time | HCM Extracts |
| Local Payroll | Employee changes | Per pay period | HCM Extracts |
| Badge System | Active employees | Daily | HCM Extracts |
| Service Now | New hires, terms | Real-time | REST API |

---

## 14. Implementation Checklist

### Phase 1: Foundation

| # | Configuration Item | Module | Owner | Status |
|---|-------------------|--------|-------|--------|
| 1 | Enterprise structure | Core HR | TBD | Open |
| 2 | Legal employers | Core HR | TBD | Open |
| 3 | Business units | Core HR | TBD | Open |
| 4 | Departments | Core HR | TBD | Open |
| 5 | Locations | Core HR | TBD | Open |
| 6 | Jobs | Core HR | TBD | Open |
| 7 | Positions | Core HR | TBD | Open |
| 8 | Grades | Core HR | TBD | Open |

### Phase 2: Core HR

| # | Configuration Item | Module | Owner | Status |
|---|-------------------|--------|-------|--------|
| 9 | Person types | Core HR | TBD | Open |
| 10 | Action types/reasons | Core HR | TBD | Open |
| 11 | Flexfields | Core HR | TBD | Open |
| 12 | Document types | Core HR | TBD | Open |
| 13 | Security roles | Security | TBD | Open |
| 14 | Approval workflows | BPM | TBD | Open |

### Phase 3: Talent Modules

| # | Configuration Item | Module | Owner | Status |
|---|-------------------|--------|-------|--------|
| 15 | Requisition template | Recruiting | TBD | Open |
| 16 | Career site | Recruiting | TBD | Open |
| 17 | Candidate phases | Recruiting | TBD | Open |
| 18 | Rating models | Performance | TBD | Open |
| 19 | Performance template | Performance | TBD | Open |
| 20 | Goal plan | Goals | TBD | Open |
| 21 | Competency model | Profile | TBD | Open |
| 22 | Compensation plan | Compensation | TBD | Open |
| 23 | Talent review template | Talent | TBD | Open |
| 24 | Journey templates | Journeys | TBD | Open |
| 25 | Learning catalog | Learning | TBD | Open |
| 26 | Absence types | Absence | TBD | Open |

### Phase 4: Reporting & Integration

| # | Configuration Item | Module | Owner | Status |
|---|-------------------|--------|-------|--------|
| 27 | OTBI dashboards | Analytics | TBD | Open |
| 28 | Custom reports | Analytics | TBD | Open |
| 29 | HCM Extracts | Integration | TBD | Open |
| 30 | Inbound interfaces | Integration | TBD | Open |

---

## Document Control

| Attribute | Value |
|-----------|-------|
| File Path | `02 - Define/01 - Repositories/00 - Documentation/24_Oracle_HCM_Configuration_Specifications.md` |
| Created | 2025-12-06 |
| Author | HCM Implementation Agent |
| Review Status | Draft - Requires stakeholder validation |

---

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-06 | Initial configuration specifications |

---

*This document requires validation with GEODIS HR stakeholders, AMARIS implementation team, and Oracle consultants.*
