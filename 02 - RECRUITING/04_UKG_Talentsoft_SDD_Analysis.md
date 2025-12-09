# Gap Analysis: UKG (UltiPro) vs Talentsoft Recruitment Module

**Document Version:** 1.0
**Date:** 2025-11-22
**Scope:** Talent Acquisition / Recruitment Data Model Comparison

---

## Executive Summary

This document analyzes the data model gaps between **UKG (UltiPro) Talent Acquisition** and **Cegid Talentsoft Recruiting** modules, with specific focus on SDD (Standard Data Delivery) report availability.

### Key Findings

| Category | UKG Fields | Gap Count | Impact |
|----------|------------|-----------|--------|
| Total Fields Analyzed | 594 | - | - |
| No Talentsoft Equivalent | - | 15 | Medium |
| Requires Custom Fields | - | 4 | Low |
| Calculated Fields (not stored) | - | 10 | High |
| Not in SDD Reports | - | 130 | Critical |
| Multi-SDD Joins Required | - | 80 | Medium |

---

## 1. Architecture Comparison

### 1.1 UKG Data Architecture

UKG uses a **Star Schema** optimized for Business Intelligence reporting:

```
[Presentation Layer]
    └── [Unified Reporting - Talent Acquisition]
            │
            ├── [Opportunities] ──────────────────┐
            │       ├── Opening Information       │
            │       ├── Company Information       │
            │       ├── Compensation              │  Denormalized
            │       ├── Screening                 │  (594 fields)
            │       ├── Recruiting Process        │
            │       └── Applications ─────────────┤
            │             ├── Hire Details        │
            │             ├── Education           │
            │             ├── Experience          │
            │             └── Disposition         │
            │                                     │
            └── [Candidates] ─────────────────────┘
                    ├── Candidate Details
                    └── Applications (same structure)
```

**Characteristics:**
- Pre-joined, denormalized structure
- Pre-calculated metrics (Days-to-Hire)
- Single query access to all related data
- 594 fields available in reporting layer

### 1.2 Talentsoft Data Architecture

Talentsoft uses a **Normalized Relational Model** with **SDD Reports** for aggregated views:

```
[Normalized Tables]                    [SDD Reports - Aggregated Views]

┌─────────────┐                        ┌──────────────────────────────┐
│   offer     │ ───────────────────►   │      SDD_VACANCIES.csv       │
│  (40 cols)  │                        │        (56 columns)          │
└─────────────┘                        │  Includes: Offer + Location  │
                                       │  + Criteria + JobDescription │
┌─────────────┐                        └──────────────────────────────┘
│  entity     │ ─────────┐
│             │          │             ┌──────────────────────────────┐
└─────────────┘          └──────────►  │    SDD_APPLICATION.csv       │
                                       │        (18 columns)          │
┌─────────────┐                        │  Includes: Application +     │
│ applicant   │ ─── NOT IN SDD ───X    │  Candidate ID + Offer link   │
│  (33 cols)  │                        └──────────────────────────────┘
└─────────────┘
                                       ┌──────────────────────────────┐
┌─────────────┐                        │  SDD_APPLICATION_EVENTS.csv  │
│ publication │ ───────────────────►   │        (7 columns)           │
└─────────────┘                        │  Child events with dates     │
                                       └──────────────────────────────┘
┌─────────────┐
│  events     │ ───────────────────►   ┌──────────────────────────────┐
└─────────────┘                        │ SDD_VACANCY_REQUESTS_*.csv   │
                                       │  Pre-approval workflow       │
                                       └──────────────────────────────┘
```

**Characteristics:**
- Normalized source tables
- SDD reports provide aggregated views
- Candidate data NOT included in SDD
- Requires joins for complete picture
- 56 + 18 + 7 columns in main SDD files

---

## 2. SDD Files Overview

### 2.1 Available SDD Files

| SDD File | Columns | Records | Purpose |
|----------|---------|---------|---------|
| `SDD_VACANCIES.csv` | 56 | Varies | Job offers with location, criteria, job description |
| `SDD_APPLICATION.csv` | 18 | Varies | Applications with candidate link and status |
| `SDD_APPLICATION_EVENTS.csv` | 7 | Varies | Application child events (interviews, etc.) |
| `SDD_VACANCY_REQUESTS_LIST.csv` | 55 | Varies | Vacancy requests (pre-approval) |
| `SDD_VACANCY_REQUESTS_EVENTS.csv` | 7 | Varies | Vacancy request workflow events |
| `SDD_VACANCY_REQUESTS_VALIDATION.csv` | 13 | Varies | Approval/validation workflow |

### 2.2 SDD_VACANCIES.csv - Key Columns

| Column | Description | UKG Equivalent |
|--------|-------------|----------------|
| `OfferID` | Unique offer identifier | (Internal ID) |
| `Offer_Reference_` | Requisition number | Requisition Number |
| `Offer_OfferStatus_` | Vacancy status | Opportunity Status |
| `Offer_CreationDate_` | Creation timestamp | Created Date |
| `Offer_CreationUser_` | Created by user | Created By |
| `JobDescriptionTranslation_JobTitle_` | Job title | Opportunity Title |
| `JobDescription_PrimaryProfile_` | Job family/profile | Job Family |
| `JobDescription_Contract_` | Contract type | Full-Time Or Part-Time |
| `JobDescription_ProfessionalCategory_` | Professional category | EEO Category |
| `Location_JobLocation_` | Job location | Location |
| `Location_Country_Country_` | Country | Country |
| `Location_Region_Region_` | Region/State | State/Province |
| `Location_Department_Department_` | Department | Org Level |
| `Origin_Entity_` | Organization entity | Company |
| `Origin_NumberOfVacancies_` | Number of positions | Headcount fields |
| `Origin_OperationalManagerEmail_` | Hiring manager email | Hiring Manager Email |
| `ApplicantCriteria_EducationLevel_` | Required education | N/A |
| `ApplicantCriteria_ExperienceLevel_` | Required experience | N/A |
| `FirstPublicationDate` | First publication date | First Published Date |
| `Offer_BackOfficeUser_User_` | Recruiter | Recruiter |

### 2.3 SDD_APPLICATION.csv - Key Columns

| Column | Description | UKG Equivalent |
|--------|-------------|----------------|
| `JobApplicationEventID` | Application ID | Application ID |
| `ApplicantID` | Candidate ID | Candidate reference |
| `JobApplicationEvent_Offer_` | Linked offer | Opportunity reference |
| `JobApplicationEvent_Entity_` | Application entity | Company |
| `JobApplicationEvent_EventDate_` | Application date | Date Applied |
| `JobApplicationEvent_CreationDate_` | Creation timestamp | Created Date |
| `JobApplicationEvent_CreationUser_` | Created by | Application Created By |
| `JobApplicationEvent_JobApplicationStatus_` | Application status | Disposition |
| `JobApplicationEvent_JobApplicationEventType_` | Application type | Internal/External |
| `JobApplicationEvent_PublicationSupport_` | Source channel | Source |
| `JobApplicationEvent_Comment_` | Comments | Disposition Notes |
| `JobApplicationEvent_Motivation_` | Motivation letter | N/A |
| `JobApplicationEvent_Supervisor_` | Supervisor | Supervisor |

### 2.4 SDD_APPLICATION_EVENTS.csv - Key Columns

| Column | Description | UKG Equivalent |
|--------|-------------|----------------|
| `JobApplicationEventID` | Parent application ID | Application reference |
| `ChildEventID` | Event ID | N/A |
| `JobApplicationChildEvent_EventDate_` | Event date | Various date fields |
| `JobApplicationChildEvent_JobApplicationChildEventType_` | Event type | Event type |
| `JobApplicationChildEvent_Comment_` | Event comment | Notes |
| `JobApplicationChildEvent_CreationUser_` | Created by | Created By |
| `JobApplicationChildEvent_Supervisor_` | Supervisor | Supervisor |

---

## 3. Gap Analysis Details

### 3.1 Fields with No Talentsoft Equivalent (15 fields)

**Severity: Medium**
**Impact: Data loss during migration**

| # | UKG Field | Context | Reason |
|---|-----------|---------|--------|
| 1 | Incumbent First Name | Opening Information | TS does not track incumbent |
| 2 | Incumbent Last Name | Opening Information | TS does not track incumbent |
| 3 | Incumbent Name (Last, First) | Opening Information | TS does not track incumbent |
| 4 | Title (Hiring Manager) | Recruiting Process | TS only stores First/Last name |
| 5 | Middle Name (Hiring Manager) | Recruiting Process | TS only stores First/Last name |
| 6 | Suffix (Hiring Manager) | Recruiting Process | TS only stores First/Last name |
| 7 | Title (Onboarding Owner) | Recruiting Process | TS only stores First/Last name |
| 8 | Middle Name (Onboarding Owner) | Recruiting Process | TS only stores First/Last name |
| 9 | Suffix (Onboarding Owner) | Recruiting Process | TS only stores First/Last name |
| 10 | Middle Name (Supervisor) | Recruiting Process | TS only stores First/Last name |
| 11 | Suffix (Supervisor) | Recruiting Process | TS only stores First/Last name |
| 12 | Title (Supervisor) | Recruiting Process | TS only stores First/Last name |
| 13 | Middle Name (Recruiter) | Recruiting Process | TS only stores First/Last name |
| 14 | Suffix (Recruiter) | Recruiting Process | TS only stores First/Last name |
| 15 | Title (Recruiter) | Recruiting Process | TS only stores First/Last name |

**Recommendation:**
- Accept data loss for Title/Middle Name/Suffix fields
- For incumbent tracking, consider custom fields or separate incumbent management process

---

### 3.2 Fields Requiring Custom Fields in Talentsoft (4 fields)

**Severity: Low**
**Impact: Requires configuration**

| # | UKG Field | Recommended TS Custom Field |
|---|-----------|----------------------------|
| 1 | License Number | `PersonalInformationCustomFields.ShortText1` |
| 2 | License/Certification Name | `PersonalInformationCustomFields.ShortText2` |
| 3 | License Number (duplicate) | Same as above |
| 4 | License/Certification Name (duplicate) | Same as above |

**Action Required:**
1. Configure custom field block in Talentsoft for Licenses/Certifications
2. Map import process to populate these fields
3. Update export/report configurations to include custom fields

---

### 3.3 Calculated Fields - Not Stored in Talentsoft (10 fields)

**Severity: High**
**Impact: Requires BI-layer calculations**

UKG pre-calculates these hiring metrics and stores them. Talentsoft requires calculation from event dates.

| # | UKG Metric | Calculation Formula |
|---|------------|---------------------|
| 1 | Days Between Accept and Offer Dates | `AcceptEventDate - OfferEventDate` |
| 2 | Days Between Accept and Start Dates | `AcceptEventDate - StartEventDate` |
| 3 | Days Between Hire and Publish Dates | `HireEventDate - FirstPublicationDate` |
| 4 | Days Between Offer and Start Dates | `OfferEventDate - StartEventDate` |
| 5 | Days Between Start and Publish Dates | `StartEventDate - FirstPublicationDate` |
| 6-10 | (Duplicates in Candidates context) | Same formulas |

**Data Sources for Calculation:**
```sql
-- Example: Days to Hire calculation
SELECT
    app.JobApplicationEventID,
    app.JobApplicationEvent_Offer_,
    DATEDIFF(day,
        pub.FirstPublicationDate,
        hire_event.JobApplicationChildEvent_EventDate_
    ) AS DaysToHire
FROM SDD_APPLICATION app
JOIN SDD_VACANCIES vac ON app.JobApplicationEvent_Offer_ = vac.OfferID
JOIN SDD_APPLICATION_EVENTS hire_event
    ON app.JobApplicationEventID = hire_event.JobApplicationEventID
    AND hire_event.JobApplicationChildEvent_JobApplicationChildEventType_ = 'Hired'
```

**Recommendation:**
1. Create calculated measures in BI tool (Power BI DAX / Tableau calculated fields)
2. Or build a data warehouse layer with pre-calculated metrics
3. Document event type codes for each milestone (Offer, Accept, Hire, Start)

---

### 3.4 Fields Not Available in SDD Reports (130 fields)

**Severity: Critical**
**Impact: Requires additional data sources**

#### Distribution by Category:

| Category | Fields | Percentage |
|----------|--------|------------|
| Candidates (profile data) | 111 | 85% |
| Opportunities (education/experience in applications) | 19 | 15% |

#### Candidate Fields NOT in SDD:

| Sub-Category | Fields | Examples |
|--------------|--------|----------|
| Personal Information | 20+ | Address, City, Country, Phone, Email |
| Education Details | 20+ | Degree, School, Graduation Year, Major |
| Work Experience | 18+ | Company, Title, Start/End Date |
| Skills/Languages | 10+ | Skill name, Level |
| Consent/GDPR | 5+ | Consent Status, Version |

**Root Cause:**
SDD reports focus on **transactional recruitment data** (vacancies, applications, events). Candidate profile data is maintained separately and not included in SDD exports.

**Solution Architecture:**
```
┌─────────────────────────────────────────────────────────────┐
│                    Complete Data View                        │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌─────────────────┐    ┌─────────────────┐                 │
│  │  SDD Reports    │    │  CSV Exports    │                 │
│  │                 │    │                 │                 │
│  │ - SDD_VACANCIES │    │ - applicant.csv │                 │
│  │ - SDD_APPLICA.. │    │ - applicant     │                 │
│  │ - SDD_APP_EVE.. │    │   experience.csv│                 │
│  │                 │    │ - education     │                 │
│  └────────┬────────┘    │   (via API)     │                 │
│           │             └────────┬────────┘                 │
│           │                      │                          │
│           └──────────┬───────────┘                          │
│                      │                                      │
│              ┌───────▼───────┐                              │
│              │   JOIN on     │                              │
│              │  ApplicantID  │                              │
│              └───────────────┘                              │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

**Recommendation:**
1. Create combined data extract process
2. Join SDD_APPLICATION with applicant.csv on `ApplicantID`
3. Schedule regular exports of candidate data
4. Consider API integration for real-time candidate data

---

### 3.5 Fields Requiring Multiple SDD Joins (80 fields)

**Severity: Medium**
**Impact: Complex report queries**

All **Hire Details** and **Disposition** fields require joining:
- `SDD_APPLICATION.csv` (parent application record)
- `SDD_APPLICATION_EVENTS.csv` (child events with dates/types)

**Join Specification:**
```sql
SELECT
    app.*,
    evt.JobApplicationChildEvent_EventDate_,
    evt.JobApplicationChildEvent_JobApplicationChildEventType_,
    evt.JobApplicationChildEvent_Comment_
FROM SDD_APPLICATION.csv app
LEFT JOIN SDD_APPLICATION_EVENTS.csv evt
    ON app.JobApplicationEventID = evt.JobApplicationEventID
```

**Affected Fields:**
- All date-based hire details (Offer Date, Accept Date, Start Date, Hire Date)
- All disposition/status change events
- Interview events and feedback
- Workflow step completions

---

### 3.6 FTE/Headcount Tracking Gap

**Severity: High**
**Impact: Loss of granular headcount tracking**

#### Comparison:

| UKG Field | Description | Talentsoft Equivalent |
|-----------|-------------|----------------------|
| Budgeted FTE | Planned FTE count | `NumberOfVacancies` |
| Filled FTE | FTEs already hired | **Not tracked** |
| Remaining FTE | FTEs still to hire | **Not tracked** |
| Hired Headcount | People hired | **Calculated from events** |
| Maximum Headcount | Max people to hire | `NumberOfVacancies` |
| Remaining Headcount | People still to hire | **Not tracked** |

**Gap Impact:**
- Cannot track FTE fulfillment progress natively
- No distinction between FTE and headcount
- Cannot report on partial fills

**Workaround Solution:**
```sql
-- Calculate filled positions from applications
SELECT
    vac.OfferID,
    vac.Offer_Reference_,
    vac.Origin_NumberOfVacancies_ AS Budgeted,
    COUNT(CASE WHEN app.JobApplicationEvent_JobApplicationStatus_ = 'Hired'
               THEN 1 END) AS Filled,
    vac.Origin_NumberOfVacancies_ -
        COUNT(CASE WHEN app.JobApplicationEvent_JobApplicationStatus_ = 'Hired'
                   THEN 1 END) AS Remaining
FROM SDD_VACANCIES vac
LEFT JOIN SDD_APPLICATION app
    ON vac.OfferID = app.JobApplicationEvent_Offer_
GROUP BY vac.OfferID, vac.Offer_Reference_, vac.Origin_NumberOfVacancies_
```

---

### 3.7 Screening Questions Gap

**Severity: Medium**
**Impact: Questions/answers not in SDD**

#### UKG Screening Fields (23 total):

| Field | Description |
|-------|-------------|
| Answer Choice | Selected answer |
| Correct Answer | Flag for correct answer |
| Disqualifying Answer | Flag for knockout answer |
| Answer Type | Multiple choice, text, etc. |
| Application Question | Question text |
| Disqualify | Auto-disqualify flag |
| Library Question | From question library flag |
| Maximum/Minimum | Range for numeric questions |
| Points | Score value |
| Question Position | Display order |

#### Talentsoft Status:
- Questions are configured per offer
- **NOT included in SDD exports**
- Available only via API: `/api/recruiting/v1/vacancies/{id}/questions`

**Recommendation:**
1. Use API integration for screening question reporting
2. Build separate data pipeline for question/answer data
3. Consider storing aggregated scores only (pass/fail, total points)

---

## 4. Field Mapping Summary

### 4.1 Mapping Statistics

| Mapping Type | Count | Percentage |
|--------------|-------|------------|
| Direct Field Mapping | 459 | 77.3% |
| Referential (Lookup) | 84 | 14.1% |
| System Fields | 22 | 3.7% |
| No Mapping | 15 | 2.5% |
| Calculated | 10 | 1.7% |
| Custom Field | 4 | 0.7% |
| **Total** | **594** | **100%** |

### 4.2 SDD Coverage

| SDD Target | Fields | Percentage |
|------------|--------|------------|
| SDD_VACANCIES.csv | 223 | 37.5% |
| SDD_APPLICATION.csv | 137 | 23.1% |
| SDD_APPLICATION + EVENTS (joined) | 80 | 13.5% |
| Not in SDD (Candidates) | 92 | 15.5% |
| Not in SDD (Experience/Education) | 38 | 6.4% |
| SDD_VACANCY_REQUESTS_LIST | 13 | 2.2% |
| SDD_VACANCY_REQUESTS_VALIDATION | 11 | 1.9% |
| **Total** | **594** | **100%** |

---

## 5. Migration Recommendations

### 5.1 Priority Matrix

| Priority | Gap | Action | Effort | Timeline |
|----------|-----|--------|--------|----------|
| **P1** | Candidate data not in SDD | Build combined export: SDD + applicant.csv | High | Week 1-2 |
| **P1** | Hiring metrics calculation | Create BI calculated measures | Medium | Week 1 |
| **P1** | Multi-table joins | Pre-build joined datasets | Medium | Week 1 |
| **P2** | FTE tracking | Custom fields + calculated metrics | Medium | Week 2-3 |
| **P2** | Screening questions | API integration | High | Week 3-4 |
| **P3** | Name fields (Title/Suffix) | Accept loss or store in comments | Low | N/A |
| **P3** | Custom fields setup | Configure TS custom fields | Low | Week 1 |

### 5.2 Data Integration Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                     Recommended Data Flow                            │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌──────────────┐     ┌──────────────┐     ┌──────────────┐        │
│  │  Talentsoft  │     │   Staging    │     │   Data       │        │
│  │   Exports    │────►│    Area      │────►│  Warehouse   │        │
│  └──────────────┘     └──────────────┘     └──────────────┘        │
│         │                    │                    │                 │
│         │                    │                    │                 │
│  ┌──────┴──────┐      ┌─────┴─────┐       ┌─────┴─────┐           │
│  │ SDD Reports │      │   Join    │       │Calculated │           │
│  │ applicant   │      │  Tables   │       │  Metrics  │           │
│  │   .csv      │      │           │       │           │           │
│  │   API       │      │           │       │           │           │
│  └─────────────┘      └───────────┘       └───────────┘           │
│                                                  │                  │
│                                           ┌──────┴──────┐          │
│                                           │   BI Tool   │          │
│                                           │ (Power BI/  │          │
│                                           │  Tableau)   │          │
│                                           └─────────────┘          │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### 5.3 Required Joins for Complete View

```sql
-- Master recruitment view combining all sources
CREATE VIEW vw_RecruitmentComplete AS
SELECT
    -- Vacancy data
    v.OfferID,
    v.Offer_Reference_ AS RequisitionNumber,
    v.JobDescriptionTranslation_JobTitle_ AS JobTitle,
    v.Offer_OfferStatus_ AS Status,
    v.Origin_NumberOfVacancies_ AS Headcount,
    v.Origin_Entity_ AS Entity,
    v.Location_JobLocation_ AS Location,

    -- Application data
    a.JobApplicationEventID AS ApplicationID,
    a.JobApplicationEvent_EventDate_ AS ApplicationDate,
    a.JobApplicationEvent_JobApplicationStatus_ AS ApplicationStatus,
    a.JobApplicationEvent_PublicationSupport_ AS Source,

    -- Candidate data (from applicant.csv)
    c.ApplicantCode,
    c.Name AS CandidateLastName,
    c.FirstName AS CandidateFirstName,
    c.Email AS CandidateEmail,

    -- Calculated metrics
    DATEDIFF(day, v.FirstPublicationDate,
             hire_evt.JobApplicationChildEvent_EventDate_) AS DaysToHire

FROM SDD_VACANCIES v
LEFT JOIN SDD_APPLICATION a ON v.OfferID = a.JobApplicationEvent_Offer_
LEFT JOIN applicant c ON a.ApplicantID = c.ApplicantCode
LEFT JOIN SDD_APPLICATION_EVENTS hire_evt
    ON a.JobApplicationEventID = hire_evt.JobApplicationEventID
    AND hire_evt.JobApplicationChildEvent_JobApplicationChildEventType_ = 'Hired'
```

---

## 6. Appendix

### 6.1 Reference Documents

| Document | Location |
|----------|----------|
| UKG Data Model | `US Talent Acquisition Package mapped v3.xlsx` |
| Comparison Analysis | `UKG_vs_Talentsoft_DataModel_Comparison.md` |
| Talentsoft API Spec | `cegid-talentsoft-recruiting-customer.json` |
| Talentsoft Import/Export Doc | `Doc_Export_Import_Rec_FR.xlsx` |

### 6.2 SDD File Locations

| File | Path |
|------|------|
| SDD_VACANCIES | `G.A.R.V.I.S\00 - G.Talent\RECRUITMENT\SDD_VACANCIES.csv` |
| SDD_APPLICATION | `G.A.R.V.I.S\00 - G.Talent\RECRUITMENT\SDD_APPLICATION.csv` |
| SDD_APPLICATION_EVENTS | `G.A.R.V.I.S\00 - G.Talent\RECRUITMENT\SDD_APPLICATION_EVENTS.csv` |
| applicant.csv | `G.A.R.V.I.S\00 - G.Talent\RECRUITMENT\applicant.csv` |

### 6.3 Event Type Reference

Event types used in `SDD_APPLICATION_EVENTS.csv` for metric calculations:

| Event Type | Description | Used For |
|------------|-------------|----------|
| Applied | Initial application | Application Date |
| Screened | Screening completed | - |
| Interviewed | Interview conducted | - |
| Offered | Offer extended | Offer Date |
| Accepted | Offer accepted | Accept Date |
| Hired | Hire confirmed | Hire Date |
| Started | Employee started | Start Date |
| Rejected | Application rejected | - |
| Withdrawn | Candidate withdrew | - |

*Note: Actual event type codes may vary based on Talentsoft configuration.*

---

## 7. Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-11-22 | Claude Code | Initial version |

---

*Generated with Claude Code*
