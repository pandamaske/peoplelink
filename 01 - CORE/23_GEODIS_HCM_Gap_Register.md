# GEODIS HCM Implementation Gap Register

## Document Purpose

**Project:** GEODIS New HCM - AMARIS
**Document Type:** Gap Analysis Register
**Status:** DRAFT
**Last Updated:** 2025-12-06
**Version:** 1.0

---

## Executive Summary

This document provides a formal register of all identified gaps between current state (G-Talent+, Zendesk, HR Blueprint requirements) and the target Oracle HCM Cloud platform. Each gap is categorized, prioritized, and assigned a mitigation strategy.

---

## Gap Classification

### Gap Categories

| Category | Code | Description |
|----------|------|-------------|
| Functional | FUN | Feature/functionality differences |
| Process | PRC | Business process gaps |
| Data | DAT | Data structure/migration gaps |
| Integration | INT | System integration gaps |
| Reporting | RPT | Analytics/reporting gaps |
| Compliance | CMP | Regulatory/policy compliance |
| User Experience | UXP | UI/UX differences |

### Priority Levels

| Priority | Code | Description | Action Required |
|----------|------|-------------|-----------------|
| Critical | P1 | Blocks go-live | Must resolve before deployment |
| High | P2 | Significant impact | Resolve in Phase 1 |
| Medium | P3 | Workaround available | Resolve in Phase 2 |
| Low | P4 | Nice to have | Future enhancement |

### Resolution Types

| Type | Code | Description |
|------|------|-------------|
| Configuration | CFG | Standard Oracle configuration |
| Customization | CUS | Oracle extensibility (Page Composer, etc.) |
| Extension | EXT | Custom development (VBCS, etc.) |
| Integration | INT | External system integration |
| Process Change | PCH | Business process modification |
| Accept | ACC | Accept Oracle standard behavior |
| Defer | DEF | Defer to future phase |

---

## Gap Register

### Functional Gaps (FUN)

| Gap ID | Title | Current State | Oracle State | Priority | Resolution | Owner | Status |
|--------|-------|---------------|--------------|----------|------------|-------|--------|
| FUN-001 | Campaign-based Performance Management | G-Talent+ uses campaign model to group appraisals with specific populations and dates | Oracle uses document periods and performance templates | P2 | CFG | TBD | Open |
| FUN-002 | Internal Posting 1-Week Rule | System-enforced minimum 1 week internal posting before external | No automatic enforcement | P2 | CFG/EXT | TBD | Open |
| FUN-003 | Vacancy Auto-Expiration | Vacancies auto-expire after 6 months | Requisitions remain open until closed | P3 | CFG | TBD | Open |
| FUN-004 | Mid-Year Review from Performance Form | Create mid-year review directly from annual appraisal form | Separate Check-In or new document | P2 | CFG | TBD | Open |
| FUN-005 | Performance Rating Scale | 5-level scale with percentage ranges (<50% to >120%) | Configurable rating models | P2 | CFG | TBD | Open |
| FUN-006 | Speculative Applications Management | Dedicated module for unsolicited applications | Candidate Pools / Prospects | P2 | CFG | TBD | Open |
| FUN-007 | Exit Interview Mandatory for Managers | System-enforced exit interview for managers | Journey task with rules | P2 | CFG | TBD | Open |
| FUN-008 | Blue Collar Email Limitation | Some employees may not have email; alternative notification needed | Oracle assumes email for notifications | P2 | CFG/EXT | TBD | Open |
| FUN-009 | Mutation Form | Combined form for transfers, promotions, org changes | Separate Oracle actions | P3 | CFG | TBD | Open |
| FUN-010 | Assigned Employees Module | Specific module for secondments, expatriations, delegations | Global Transfer / Assignment | P2 | CFG | TBD | Open |

### Process Gaps (PRC)

| Gap ID | Title | Current State | Oracle State | Priority | Resolution | Owner | Status |
|--------|-------|---------------|--------------|----------|------------|-------|--------|
| PRC-001 | Vacancy Request vs Requisition | Separate request object approved before vacancy created | Requisition is single object with approval | P2 | PCH | TBD | Open |
| PRC-002 | Broadbean Multi-Posting | Native Broadbean integration for job board posting | Partner integration or native Oracle options | P2 | INT | TBD | Open |
| PRC-003 | HR Service Center Ticketing | Zendesk for US HR service requests | No native ticketing; HR Help Desk available | P2 | INT/CFG | TBD | Open |
| PRC-004 | I-9 Reverification Process | Monthly auto-report with video verification | Configure compliance tracking | P2 | CFG/INT | TBD | Open |
| PRC-005 | VOYA FMLA Integration | VOYA handles FMLA/disability claims | Absence Management with integration | P2 | INT | TBD | Open |
| PRC-006 | Sterling Background Check | Sterling for pre-employment checks | Oracle supports Sterling integration | P2 | INT | TBD | Open |
| PRC-007 | Work Number Verification | Primary employment verification via Work Number | Configure verification process | P3 | CFG | TBD | Open |
| PRC-008 | E-Verify Integration | E-Verify for work eligibility | Oracle supports E-Verify integration | P2 | INT | TBD | Open |
| PRC-009 | Cascade Calibration Process | People Review: Country → Region → LoB → Group | Talent Review meeting structure | P2 | CFG | TBD | Open |
| PRC-010 | Non-Poaching Policy Enforcement | System prevents recruiting from certain entities | Business rule; not system enforced | P3 | PCH | TBD | Open |

### Data Gaps (DAT)

| Gap ID | Title | Current State | Oracle State | Priority | Resolution | Owner | Status |
|--------|-------|---------------|--------------|----------|------------|-------|--------|
| DAT-001 | Performance History Format | G-Talent+ campaign-based history | Oracle document-based history | P2 | DAT | TBD | Open |
| DAT-002 | Custom Employee Fields | G-Talent+ specific profile fields | Map to Oracle flexfields | P2 | CFG | TBD | Open |
| DAT-003 | Candidate Source Tracking | Broadbean source tracking | Oracle source configuration | P3 | CFG | TBD | Open |
| DAT-004 | Position History | G-Talent+ situation history | Oracle assignment history | P2 | DAT | TBD | Open |
| DAT-005 | Objective/Goal Format | G-Talent+ objective structure | Oracle Goal Management format | P2 | DAT | TBD | Open |
| DAT-006 | Competency Model | G-Talent+ skills/values structure | Oracle competency model | P2 | CFG/DAT | TBD | Open |
| DAT-007 | Training History | G-Campus/G-Learning completions | Oracle Learning records | P2 | DAT/INT | TBD | Open |
| DAT-008 | Exit Interview Data | G-Talent+ exit interview responses | Oracle questionnaire responses | P3 | DAT | TBD | Open |
| DAT-009 | Talent Segmentation Data | High Potential, Key Talent categories | Talent pool membership | P2 | DAT | TBD | Open |
| DAT-010 | Salary History | G-Talent+ compensation history | Oracle compensation history | P2 | DAT | TBD | Open |

### Integration Gaps (INT)

| Gap ID | Title | Current State | Oracle State | Priority | Resolution | Owner | Status |
|--------|-------|---------------|--------------|----------|------------|-------|--------|
| INT-001 | Broadbean Job Posting | Native G-Talent+ integration | Partner integration required | P2 | INT | TBD | Open |
| INT-002 | Minerve+ Financial System | G-Talent+ to Minerve+ sync | Oracle to Minerve+ integration | P1 | INT | TBD | Open |
| INT-003 | G-Campus Onboarding | Native training platform | Oracle Learning or integration | P2 | INT/CFG | TBD | Open |
| INT-004 | G-Learning E-Learning | Native e-learning platform | Oracle Learning Cloud | P2 | INT/CFG | TBD | Open |
| INT-005 | Local Payroll Systems | Country-specific payroll integrations | Oracle Payroll or integration | P1 | INT | TBD | Open |
| INT-006 | Zendesk HR Service | US HR ticketing platform | Oracle HR Help Desk or integration | P2 | INT | TBD | Open |
| INT-007 | Sterling Background Check | Pre-employment screening | Oracle Sterling integration | P2 | INT | TBD | Open |
| INT-008 | VOYA FMLA/Disability | Leave management provider | Absence Management integration | P2 | INT | TBD | Open |
| INT-009 | E-Verify | Work eligibility verification | Oracle E-Verify integration | P2 | INT | TBD | Open |
| INT-010 | Service Now IT Offboarding | IT access termination | Workflow integration | P2 | INT | TBD | Open |

### Reporting Gaps (RPT)

| Gap ID | Title | Current State | Oracle State | Priority | Resolution | Owner | Status |
|--------|-------|---------------|--------------|----------|------------|-------|--------|
| RPT-001 | HR KPIs - FTE Calculation | Specific FTE formula (period-end, average) | OTBI FTE calculations | P2 | CFG/RPT | TBD | Open |
| RPT-002 | Turnover Rate Formula | Specific turnover calculation | OTBI turnover reports | P2 | CFG/RPT | TBD | Open |
| RPT-003 | Frequency Rate (Accidents) | (Accidents × 1M) / Hours Worked | Custom OTBI report | P2 | RPT | TBD | Open |
| RPT-004 | Severity Rate (Accidents) | (Days Lost × 1K) / Hours Worked | Custom OTBI report | P2 | RPT | TBD | Open |
| RPT-005 | Absenteeism Rate | Specific absence calculation | OTBI absence reports | P2 | CFG/RPT | TBD | Open |
| RPT-006 | Data Quality Dashboard | G-Talent+ completeness tracking | Custom OTBI dashboard | P3 | RPT | TBD | Open |
| RPT-007 | Recruitment Metrics | Time to fill, cost per hire | OTBI recruiting reports | P2 | CFG/RPT | TBD | Open |
| RPT-008 | Performance Distribution | Rating distribution reports | OTBI performance reports | P2 | CFG/RPT | TBD | Open |
| RPT-009 | Training Completion | Training hours per employee | Oracle Learning reports | P2 | CFG/RPT | TBD | Open |
| RPT-010 | Quarterly Litigation Report | Litigation tracking report | Custom OTBI report | P2 | RPT | TBD | Open |

### Compliance Gaps (CMP)

| Gap ID | Title | Current State | Oracle State | Priority | Resolution | Owner | Status |
|--------|-------|---------------|--------------|----------|------------|-------|--------|
| CMP-001 | GDPR Compliance | G-Talent+ GDPR features | Oracle GDPR capabilities | P1 | CFG | TBD | Open |
| CMP-002 | US I-9 Compliance | UKG/E-Verify integration | Oracle I-9 management | P1 | CFG/INT | TBD | Open |
| CMP-003 | State Separation Notices | State-specific termination notices | Configure by legislation | P2 | CFG | TBD | Open |
| CMP-004 | Payroll Audit Requirements | Bi-annual payroll audit | Oracle audit capabilities | P2 | CFG | TBD | Open |
| CMP-005 | Document Retention | GDPR retention policies | Oracle purge policies | P2 | CFG | TBD | Open |

### User Experience Gaps (UXP)

| Gap ID | Title | Current State | Oracle State | Priority | Resolution | Owner | Status |
|--------|-------|---------------|--------------|----------|------------|-------|--------|
| UXP-001 | G-Talent+ UI Familiarity | Users trained on G-Talent+ UI | Oracle Redwood UI | P3 | PCH | TBD | Open |
| UXP-002 | Mobile App for Blue Collar | Limited mobile capability | Oracle ME mobile apps | P2 | CFG | TBD | Open |
| UXP-003 | Manager Self-Service | G-Talent+ manager actions | Oracle manager self-service | P2 | CFG | TBD | Open |
| UXP-004 | Employee Self-Service | G-Talent+ employee portal | Oracle employee self-service | P2 | CFG | TBD | Open |

---

## Gap Summary by Priority

| Priority | Count | Percentage |
|----------|-------|------------|
| Critical (P1) | 4 | 8% |
| High (P2) | 40 | 80% |
| Medium (P3) | 6 | 12% |
| Low (P4) | 0 | 0% |
| **Total** | **50** | **100%** |

## Gap Summary by Category

| Category | Count | Percentage |
|----------|-------|------------|
| Functional (FUN) | 10 | 20% |
| Process (PRC) | 10 | 20% |
| Data (DAT) | 10 | 20% |
| Integration (INT) | 10 | 20% |
| Reporting (RPT) | 10 | 20% |
| Compliance (CMP) | 5 | 10% |
| User Experience (UXP) | 4 | 8% |

## Gap Summary by Resolution Type

| Resolution | Count | Effort Level |
|------------|-------|--------------|
| Configuration (CFG) | 25 | Low-Medium |
| Integration (INT) | 15 | Medium-High |
| Data Migration (DAT) | 8 | Medium |
| Custom Development (EXT) | 3 | High |
| Process Change (PCH) | 4 | Medium |
| Reporting (RPT) | 10 | Medium |

---

## Critical Gaps (P1) - Detailed Analysis

### INT-002: Minerve+ Financial System Integration

**Current State:** G-Talent+ syncs employee and compensation data with Minerve+ financial system.

**Gap:** Oracle HCM needs integration with Minerve+ for:
- Employee master data sync
- Compensation data for accounting
- Cost center allocation

**Impact:** Blocks financial reporting and payroll processing.

**Mitigation:**
1. Define integration requirements
2. Evaluate Oracle Integration Cloud (OIC)
3. Build bi-directional interface
4. Test end-to-end data flow

**Timeline:** Must complete before go-live

---

### INT-005: Local Payroll Systems Integration

**Current State:** Country-specific payroll systems receive data from G-Talent+.

**Gap:** Oracle HCM needs integration with local payroll systems OR implementation of Oracle Payroll.

**Impact:** Blocks payroll processing in all countries.

**Mitigation:**
1. Assess Oracle Payroll country availability
2. Define integration for non-Oracle payroll countries
3. Build HCM Extracts for payroll data
4. Configure inbound interfaces for payroll results

**Timeline:** Must complete before go-live

---

### CMP-001: GDPR Compliance

**Current State:** G-Talent+ has GDPR features for EU data protection.

**Gap:** Ensure Oracle HCM GDPR capabilities meet requirements:
- Data subject access requests
- Right to be forgotten
- Data retention policies
- Consent management

**Impact:** Legal/compliance risk if not properly configured.

**Mitigation:**
1. Review Oracle GDPR documentation
2. Configure purge policies
3. Set up data access controls
4. Test DSAR process

**Timeline:** Must complete before go-live

---

### CMP-002: US I-9 Compliance

**Current State:** UKG/E-Verify integration for US work eligibility.

**Gap:** Oracle HCM needs:
- I-9 form management
- E-Verify integration
- Reverification tracking
- Compliance reporting

**Impact:** Legal risk for US workforce.

**Mitigation:**
1. Configure Oracle I-9 management
2. Set up E-Verify integration
3. Configure reverification alerts
4. Test compliance workflow

**Timeline:** Must complete before US go-live

---

## Mitigation Roadmap

### Phase 1: Critical Gaps (Pre Go-Live)

| Gap ID | Action | Owner | Target Date |
|--------|--------|-------|-------------|
| INT-002 | Minerve+ integration design | TBD | TBD |
| INT-005 | Payroll integration strategy | TBD | TBD |
| CMP-001 | GDPR configuration | TBD | TBD |
| CMP-002 | I-9/E-Verify setup | TBD | TBD |

### Phase 2: High Priority Gaps (Phase 1 Deployment)

| Gap ID | Action | Owner | Target Date |
|--------|--------|-------|-------------|
| FUN-001 | Performance template configuration | TBD | TBD |
| FUN-005 | Rating model configuration | TBD | TBD |
| PRC-002 | Recruiting integration decision | TBD | TBD |
| INT-003/004 | Learning strategy | TBD | TBD |
| RPT-001-005 | OTBI report development | TBD | TBD |

### Phase 3: Medium Priority Gaps (Post Go-Live)

| Gap ID | Action | Owner | Target Date |
|--------|--------|-------|-------------|
| FUN-002 | Internal posting automation | TBD | TBD |
| FUN-003 | Requisition expiration rules | TBD | TBD |
| RPT-006-010 | Additional dashboards | TBD | TBD |
| UXP-001-004 | User experience optimization | TBD | TBD |

---

## Document Control

| Attribute | Value |
|-----------|-------|
| File Path | `02 - Define/01 - Repositories/00 - Documentation/23_GEODIS_HCM_Gap_Register.md` |
| Created | 2025-12-06 |
| Author | HCM Implementation Agent |
| Review Status | Draft - Requires stakeholder validation |

---

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-06 | Initial gap register with 50 identified gaps |

---

*This document requires validation with GEODIS HR stakeholders, AMARIS implementation team, and Oracle consultants.*
