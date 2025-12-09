# G-Talent+ to Oracle HCM Cloud Mapping Document

## Document Purpose

**Project:** GEODIS New HCM - AMARIS
**Document Type:** System Mapping & Gap Analysis
**Status:** IN PROGRESS
**Last Updated:** 2025-12-06
**Version:** 1.0

---

## Executive Summary

This document provides a comprehensive mapping between the current G-Talent+ (Talentsoft) HRIS and the target Oracle HCM Cloud platform. It covers:
- Module-by-module feature mapping
- Process workflow transformations
- Data migration considerations
- Gap analysis and recommendations

---

## Reference Documentation

### Oracle HCM Cloud Documentation
- **Online Reference:** https://docs.oracle.com/en/cloud/saas/human-resources/index.html
- **Local Documentation:** `01 - Discovery/05 - Oracle Documentation/` (41 PDFs extracted)
- **Current Version:** 25B

### G-Talent+ Documentation
- **Source:** `01 - Discovery/08 - Talentsoft Guidelines/` (44 files extracted)
- **Extracted Content:** `talentsoft_guides_extracted.txt`

---

## Module Mapping Overview

| G-Talent+ Module | Oracle HCM Module | Mapping Complexity | Notes |
|------------------|-------------------|-------------------|-------|
| Core HR | Global Human Resources | Medium | Profile structure differs |
| Recruitment | Oracle Recruiting | High | Request vs Requisition model |
| Performance Appraisal | Performance Management | Medium | Campaign vs Document approach |
| Salary Review | Workforce Compensation | Medium | Budget workflow similar |
| People Review | Talent Review | Low | Good functional match |
| Exit Interview | Journeys (Exit) | Low | Journey-based approach |
| Campaign Management | Performance Templates | Medium | Configuration differs |
| HR KPIs | OTBI Analytics | High | Different reporting model |
| Assigned Employees | Global HR (Assignments) | Low | Standard Oracle model |

---

## 1. Recruitment Module Mapping

### 1.1 Concept Mapping

| G-Talent+ Concept | Oracle HCM Concept | Transformation Notes |
|-------------------|-------------------|---------------------|
| Vacancy Request | Job Requisition | Requisition is the Oracle equivalent; includes approval workflow |
| Vacancy | Job Posting | Created from requisition; posted to career sites |
| Candidate | Candidate | Direct mapping; prospect vs applicant distinction |
| Application | Job Application | Application linked to specific requisition |
| Speculative Application | Prospect / Candidate Pool | Use Candidate Pools for talent community |
| Broadbean Integration | Job Board Integration | Oracle Recruiting has native integrations + partners |
| Recruiter | Recruiter Role | Role-based security in Oracle |
| Hiring Manager | Hiring Manager Role | Participates in requisition and selection |

### 1.2 Process Flow Mapping

**G-Talent+ Vacancy Request Workflow:**
```
Manager Request → Approver Review → Recruiter Creates Vacancy → Internal Posting (1 week) → External Posting → Selection
```

**Oracle Requisition Workflow:**
```
Hiring Manager/Recruiter Creates Requisition → Approval Workflow → Job Posting → Candidate Sourcing → Selection → Offer
```

### 1.3 Key Differences

| Feature | G-Talent+ | Oracle HCM | Gap/Action |
|---------|-----------|------------|-----------|
| Request vs Requisition | Separate request object | Requisition includes request | Configure requisition template |
| Internal Posting Rule | System-enforced 1 week | Configurable via posting rules | Configure posting schedule |
| Broadbean | Native integration | Partner integration or native | Evaluate Oracle native options |
| Vacancy Expiration | 6 months auto-expire | Configurable | Set requisition status rules |
| Job Board Posting | Via Broadbean | Multiple options (LinkedIn, Indeed native) | Evaluate Recruiting Booster |

### 1.4 Oracle Configuration Requirements

| Configuration Item | Setup Location | GEODIS Requirement |
|-------------------|----------------|-------------------|
| Requisition Template | Setup > Recruiting | Include GEODIS fields |
| Approval Workflow | BPM Workflow | N+1 and HR approval chain |
| Posting Schedule | Recruiting Setup | Internal 1 week before external |
| Career Site | Oracle Career Site | GEODIS branded career site |
| Candidate Pool Process | Recruiting Setup | For speculative applications |

### 1.5 Oracle Documentation References

| Document | Content |
|----------|---------|
| implementing-recruiting.pdf | Requisition setup, templates, workflows |
| using-recruiting.pdf | End-user processes |
| using-and-administering-recruiting-booster.pdf | AI-powered recruiting features |

---

## 2. Performance Management Module Mapping

### 2.1 Concept Mapping

| G-Talent+ Concept | Oracle HCM Concept | Transformation Notes |
|-------------------|-------------------|---------------------|
| Performance Campaign | Performance Document Period | Defined period with population and form |
| Performance Form | Performance Template/Document | Template defines sections; Document is instance |
| Campaign Type (1/2/3) | Document Type Configuration | Configure participant flow |
| Rating Scale (<50% to >120%) | Rating Model | Create custom rating model |
| Skills Assessment | Competency Section | Use competencies in template |
| Values Assessment | Competency Section (Values) | Define GEODIS values as competencies |
| Development Plan | Development Goals Section | Link to Career Development |
| Career Aspirations | Career Planning Section | Use Talent Profile integration |
| Mid-Year Review | Check-In / Anytime Feedback | Use Check-In or create interim document |
| Objectives | Performance Goals | Integrate with Goal Management |

### 2.2 Rating Model Mapping

**G-Talent+ Rating Scale:**

| G-Talent+ Rating | % Range | Oracle Rating Model Level |
|-----------------|---------|--------------------------|
| Significantly Below | <50% | Level 1 - Does Not Meet |
| Below | 50-80% | Level 2 - Partially Meets |
| Meets | 80-100% | Level 3 - Meets Expectations |
| Exceeds | 100-120% | Level 4 - Exceeds |
| Far Exceeds | >120% | Level 5 - Significantly Exceeds |

**Oracle Configuration:**
- Create custom Rating Model: "GEODIS Performance Rating"
- Define 5 levels with numeric values (1-5)
- Associate with Performance Template sections

### 2.3 Campaign to Document Period Mapping

| G-Talent+ Campaign Type | Oracle Equivalent | Configuration |
|------------------------|-------------------|---------------|
| Type 1 (Employee only) | Self-Evaluation Document | Manager participation = None |
| Type 2 (Manager only) | Manager-Only Evaluation | Employee participation = None |
| Type 3 (Employee + Manager) | Standard Performance Document | Both participants required |

### 2.4 Performance Form Section Mapping

| G-Talent+ Section | Oracle Section Type | Notes |
|-------------------|--------------------| ------|
| Previous Year Objectives Review | Performance Goals (Previous) | Review previous period goals |
| Skills Assessment | Competencies | Use GEODIS competency model |
| Values Assessment | Competencies (Values) | Define values as competencies |
| Development Plan | Development Goals | Link to Career Development |
| Career Aspirations | Career Planning | Talent Profile integration |
| Next Year Objectives | Performance Goals (New) | Goal setting for next period |
| Overall Rating | Overall Summary | Calculated or manager-assigned |

### 2.5 Process Flow Mapping

**G-Talent+ Campaign Workflow:**
```
HR Admin Setup → Launch → Employee Self-Assessment → Manager Evaluation → Validation Meeting → Sign-off → Close
```

**Oracle Performance Document Workflow:**
```
Admin Creates Period → Template Assigned → Document Generated → Worker Self-Evaluation → Manager Evaluation → Approval → Complete
```

### 2.6 Mid-Year Review Transformation

| G-Talent+ | Oracle Options | Recommendation |
|-----------|---------------|----------------|
| Mid-Year Review (from form) | Option 1: Check-In feature | Informal, ongoing feedback |
| | Option 2: Interim Document Type | Formal mid-year evaluation |
| | Option 3: Anytime Feedback | Continuous feedback model |

**Recommendation:** Use Oracle Check-In for informal mid-year discussions, with optional interim performance document for formal review.

### 2.7 Oracle Configuration Requirements

| Configuration Item | Setup Location | GEODIS Requirement |
|-------------------|----------------|-------------------|
| Rating Model | Profile Management Setup | 5-level GEODIS scale |
| Performance Template | Performance Setup | Annual appraisal template |
| Document Type | Performance Setup | Annual, Mid-Year types |
| Review Period | Performance Setup | January-April (extendable) |
| Process Flow | Performance Setup | Self-eval → Manager → Complete |
| Competency Model | Profile Management | GEODIS skills and values |

### 2.8 Oracle Documentation References

| Document | Content |
|----------|---------|
| implementing-performance-management.pdf | Template setup, process flows |
| using-performance-management.pdf | End-user processes |
| implementing-goal-management.pdf | Goal integration |
| using-goal-management.pdf | Goal management user guide |

---

## 3. Core HR Module Mapping

### 3.1 Employee Profile Mapping

| G-Talent+ Profile Section | Oracle HCM Object | Oracle Component |
|--------------------------|-------------------|------------------|
| Civil Registration | Person | Personal Details |
| Contracts | Assignment | Work Relationship > Assignment |
| Situations | Assignment | Position, Organization, Manager |
| FTE | Assignment | Working Hours / FTE |
| Identity Documents | Person Documents | Document Records |
| Bank Details | Payment Methods | Personal Payment Method |
| Address | Person Address | Address (Home, Mailing) |
| Emergency Contacts | Person Contacts | Emergency Contact |

### 3.2 Employee Lifecycle Actions

| G-Talent+ Action | Oracle Action | Transaction Type |
|------------------|---------------|------------------|
| Employee Creation (from recruitment) | Hire | New Hire from Recruiting |
| Employee Creation (blank form) | Hire | Direct Hire (Global HR) |
| Mutation (Transfer) | Transfer | Change Assignment |
| Mutation (Promotion) | Promotion | Change Assignment + Salary |
| Mutation (Organizational Change) | Transfer | Change Organization |
| Secondment | Global Transfer | Temporary Assignment |
| Expatriation | Global Transfer | International Assignment |
| Termination | Termination | End Employment |

### 3.3 Journeys for Lifecycle Events

Oracle Journeys can replace/enhance G-Talent+ workflows:

| G-Talent+ Process | Oracle Journey Category | Pre-built Journey |
|-------------------|------------------------|-------------------|
| Onboarding | Enterprise Onboarding | Oracle - Onboarding Journey |
| Transfer | Contextual | Oracle - Intra-Company Transfer Journey |
| Promotion | Guided | Oracle - Promotion Journey |
| Offboarding | Offboarding | Configure Exit Journey |

### 3.4 Data Quality Dashboard Mapping

| G-Talent+ Feature | Oracle Equivalent | Setup |
|-------------------|-------------------|-------|
| Data Completeness Tracking | OTBI Reports | Create data quality report |
| Missing Fields Alerts | Notifications/Rules | Configure validation rules |
| Data Quality KPIs | HR Analytics Dashboard | Build OTBI dashboard |

### 3.5 Oracle Configuration Requirements

| Configuration Item | Setup Location | GEODIS Requirement |
|-------------------|----------------|-------------------|
| Person Flexfields | Setup > HCM | Custom GEODIS attributes |
| Assignment Flexfields | Setup > HCM | Additional assignment data |
| Action Types | Setup > Employment | Mutation types |
| Action Reasons | Setup > Employment | Termination reasons |
| Document Types | Document Records Setup | ID documents, contracts |
| Journey Templates | Journey Setup | Onboarding, transfer, exit |

### 3.6 Oracle Documentation References

| Document | Content |
|----------|---------|
| understanding-enterprise-structures.pdf | Enterprise, legal entity, organization setup |
| implementing-and-using-journeys.pdf | Journey configuration |
| using-common-features-for-hcm.pdf | Common HCM features |
| hcm-data-loader.pdf | Data migration |

---

## 4. Talent Management Module Mapping

### 4.1 People Review / Talent Review

| G-Talent+ Concept | Oracle HCM Concept | Notes |
|-------------------|-------------------|-------|
| People Review Campaign | Talent Review Meeting | Similar concept |
| Talent Segmentation | Talent Ratings | High Potential, Key Talent |
| 9-Box Grid | Talent Matrix | Configurable matrix |
| Succession Planning | Succession Plans | Successor identification |
| Readiness Assessment | Succession Readiness | Ready Now/1-2 Years/3+ Years |

### 4.2 Process Flow Mapping

**G-Talent+ People Review:**
```
May-October → Country Review → Region Review → LoB Review → Group Calibration → Action Plans
```

**Oracle Talent Review:**
```
Create Review Meeting → Select Population → Review Talent Data → Calibrate → Identify Successors → Actions
```

### 4.3 Oracle Configuration Requirements

| Configuration Item | Setup Location | GEODIS Requirement |
|-------------------|----------------|-------------------|
| Talent Review Template | Talent Review Setup | Cascade calibration template |
| Talent Ratings | Profile Management | GEODIS talent categories |
| Succession Plan | Succession Setup | Key position plans |
| Matrix Configuration | Talent Review Setup | 9-box or custom |

### 4.4 Oracle Documentation References

| Document | Content |
|----------|---------|
| implementing-talent-review-and-succession-management.pdf | Talent review configuration |
| using-talent-review-and-succession-management.pdf | End-user guide |
| implementing-talent-management-base.pdf | Base talent setup |

---

## 5. Compensation Module Mapping

### 5.1 Salary Review Process

| G-Talent+ Step | Oracle Workforce Compensation Step |
|----------------|-----------------------------------|
| Configure parameters | Create Compensation Plan |
| Define population | Define Eligibility |
| Set budget envelope | Configure Budget |
| Manager proposes | Manager Worksheet |
| N+1 validates | Approval Workflow |
| HR approves | Final Approval |
| Generate letters | Compensation Statements |
| Update contracts | Update Assignment Salary |

### 5.2 Key Differences

| Feature | G-Talent+ | Oracle | Notes |
|---------|-----------|--------|-------|
| Budget Management | By organization | By plan/hierarchy | Similar capability |
| Guidelines | Min/Max % | Guidelines configurable | Configure ranges |
| Eligibility | Tenure, performance | Eligibility profiles | More flexible in Oracle |
| Statements | Generate letters | Compensation Statements | Enhanced in Oracle |

---

## 6. Exit Interview / Offboarding Mapping

### 6.1 Exit Interview Transformation

| G-Talent+ Feature | Oracle Equivalent |
|-------------------|-------------------|
| Exit Interview Form | Exit Journey with Survey |
| Mandatory for Managers | Journey Allocation Rules |
| Exit Topics Capture | Questionnaire Task |
| Exit Data Analysis | OTBI Reporting |

### 6.2 Oracle Journey Configuration

| Journey Element | Configuration |
|-----------------|---------------|
| Journey Category | Offboarding |
| Trigger | Termination Action |
| Survey Task | Questionnaire type |
| Access Control | Restrict from manager view |

---

## 7. Integration Mapping

### 7.1 Current Integrations to Transform

| Current Integration | G-Talent+ | Oracle Option | Recommendation |
|--------------------|-----------|---------------|----------------|
| Broadbean | Job board posting | Oracle native + partners | Evaluate Recruiting Booster |
| Minerve+ | Financial system | HCM-ERP Integration | Configure Oracle Integration |
| G-Campus | Onboarding training | Oracle Learning | Migrate or integrate |
| G-Learning | E-Learning | Oracle Learning Cloud | Consolidate to Oracle Learning |
| Local Payroll | Country payroll | Oracle Payroll or integration | Per-country decision |

### 7.2 Oracle Integration Tools

| Tool | Purpose | Use Case |
|------|---------|----------|
| HCM Data Loader (HDL) | Bulk data import | Initial migration, ongoing mass updates |
| HCM Extracts | Data export | Outbound integrations, reporting |
| REST APIs | Real-time integration | System-to-system |
| Oracle Integration Cloud | iPaaS | Complex integrations |

---

## 8. Data Migration Strategy

### 8.1 Data Categories and Approach

| Data Category | Migration Approach | Complexity | Tool |
|--------------|-------------------|------------|------|
| Employee Master | Full migration | High | HDL |
| Position History | Selected history | High | HDL |
| Performance Data | 2-3 years | Medium | HDL |
| Open Requisitions | Active only | Low | HDL |
| Candidate Data | Active + recent | Medium | HDL |
| Training Records | Completion history | Medium | HDL |

### 8.2 Key Migration Objects

| Oracle Object | HDL Business Object | Source |
|---------------|---------------------|--------|
| Person | Worker | G-Talent+ Employee |
| Assignment | Assignment | G-Talent+ Situations |
| Position | Position | G-Talent+ Positions |
| Requisition | Requisition | G-Talent+ Vacancies |
| Performance Document | PerformanceDocument | G-Talent+ Appraisals |
| Goal | Goal | G-Talent+ Objectives |

### 8.3 Oracle Documentation References

| Document | Content |
|----------|---------|
| hcm-data-loader.pdf | HDL usage guide |
| hcm-data-loading-business-objects.pdf | Business object reference |
| hcm-extracts.pdf | Data extraction |
| hcm-integrations.pdf | Integration patterns |

---

## 9. Gap Analysis Summary

### 9.1 Functional Gaps

| Gap | G-Talent+ Feature | Oracle Status | Mitigation |
|-----|-------------------|---------------|------------|
| G-001 | Campaign-based appraisal | Document-based | Configure document periods |
| G-002 | Internal posting 1-week rule | Manual tracking | Configure posting rules |
| G-003 | Vacancy auto-expiration | Configurable | Set status automation |
| G-004 | Mid-year review from form | Not native | Use Check-In or interim doc |
| G-005 | HR KPIs exact formulas | OTBI required | Build custom analytics |

### 9.2 Process Gaps

| Gap | Current Process | Oracle Gap | Recommendation |
|-----|-----------------|------------|----------------|
| P-001 | Broadbean integration | Partner needed | Evaluate native options |
| P-002 | Minerve+ financial sync | Custom integration | Oracle Integration Cloud |
| P-003 | Blue collar no-email | Alternative notification | Mobile app / kiosk |

### 9.3 Data Gaps

| Gap | Data Element | Issue | Resolution |
|-----|--------------|-------|------------|
| D-001 | Performance history | Format differs | Transform during migration |
| D-002 | Custom fields | Flexfield mapping | Map to Oracle flexfields |
| D-003 | Candidate source tracking | Different model | Configure source tracking |

---

## 10. Recommendations

### 10.1 Quick Wins (Low Effort, High Value)
1. Use Oracle pre-built Journeys for onboarding/offboarding
2. Leverage native LinkedIn/Indeed recruiting integrations
3. Implement Oracle Check-In for continuous feedback

### 10.2 Configuration Priorities
1. Create GEODIS Rating Model (5-level scale)
2. Configure Performance Template matching current appraisal form
3. Set up Requisition workflow with GEODIS approval chain
4. Build HR KPI dashboard in OTBI

### 10.3 Custom Development Needs
1. Mid-year review workflow (if formal document required)
2. HR KPIs matching exact G-Talent+ formulas
3. Custom integration with Minerve+ financial system

---

## Document Control

| Attribute | Value |
|-----------|-------|
| File Path | `02 - Define/01 - Repositories/00 - Documentation/21_GTalent_to_Oracle_HCM_Mapping.md` |
| Created | 2025-12-06 |
| Author | HCM Implementation Agent |
| Sources | Oracle HCM Documentation (41 PDFs), Talentsoft Guidelines (44 files) |
| Review Status | Draft |

---

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-06 | Initial mapping document created |

---

*This document should be reviewed and validated with GEODIS HR stakeholders and AMARIS implementation team.*
