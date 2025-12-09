# GEODIS Oracle IRC - Field Mapping & Flexfield Analysis

**Document:** 15_Oracle_IRC_Field_Mapping_Flexfields.md
**Version:** 1.0
**Created:** 2025-12-07
**Module:** Oracle Recruiting Cloud (IRC)
**Purpose:** Map GEODIS source fields (UKG/Talentsoft) to Oracle IRC standard & custom fields

---

## UPDATE NOTICE (2025-12-08)

**Philosophy Change: Fit-to-Standard**

This document has been updated to align with Oracle standard field usage:

| Original DFF | New Approach | Rationale |
|--------------|--------------|-----------|
| TOPEX Position (ATTRIBUTE10) | **REMOVED** - Use `RECRUITING_TYPE_CODE = 'Executive'` | Oracle seeded recruiting type |
| Line of Business (ATTRIBUTE11) | **REMOVED** - Use `DEPARTMENT_ID` -> Division hierarchy | Oracle organization structure |
| Min/Max Salary (ATTRIBUTE5-7) | **REMOVED** - Use standard `MIN_SALARY`, `MAX_SALARY`, `SALARY_CURRENCY_CODE` | Oracle IRC_REQUISITIONS_B columns |

**Final Requisition DFF: 7 segments only**
1. FTE Percentage (ATTRIBUTE1)
2. Budgeted Position (ATTRIBUTE2)
3. Budget Justification (ATTRIBUTE3)
4. Incumbent Name (ATTRIBUTE4)
5. Incumbent Last Day (ATTRIBUTE_DATE1)
6. Hiring Priority (ATTRIBUTE5)
7. Impact to Staffing (ATTRIBUTE6)

---

## 1. Executive Summary

### 1.1 Field Analysis Summary

| Source System | Total Fields | Mapped to Standard | Requires Flexfield | Not Available | Must Calculate |
|---------------|--------------|-------------------|-------------------|---------------|----------------|
| UKG | 594 | 454 (76.4%) | 35 (5.9%) | 13 (2.2%) | 13 (2.2%) |
| Talentsoft | 320 | 280 (87.5%) | 25 (7.8%) | 8 (2.5%) | 7 (2.2%) |
| **Combined Unique** | **~650** | **~520** | **~45** | **~15** | **~15** |

### 1.2 Flexfield Requirements Summary

| Flexfield Type | Object | Count | Purpose |
|----------------|--------|-------|---------|
| Requisition DFF | IRC_REQUISITIONS | 12 | Custom requisition fields |
| Candidate DFF | IRC_CANDIDATES | 15 | Custom candidate fields |
| Application DFF | IRC_JOB_APPLICATIONS | 8 | Custom application fields |
| Offer DFF | IRC_OFFERS | 10 | Custom offer fields |
| Interview DFF | IRC_INTERVIEWS | 5 | Custom interview fields |

### 1.3 Key Decisions Required

| Decision | Options | Recommendation |
|----------|---------|----------------|
| FTE Tracking | Standard vs DFF | Use DFF for granular tracking |
| Incumbent Info | Lose vs DFF | Create DFF to preserve |
| Salary Details | Standard only vs DFF | Use standard + DFF for currency/range |
| Manager Titles | Lose vs Concatenate | Accept loss (not business critical) |
| Metrics Calculation | Pre-store vs BI | Calculate in OTBI |

---

## 2. Source System Field Inventory

### 2.1 UKG Field Categories (594 Total)

| Category | Field Count | Oracle Coverage |
|----------|-------------|-----------------|
| Application Core | 106 | 95% Standard |
| Candidate Personal | 152 | 90% Standard |
| Candidate Education | 30 | 85% Standard |
| Candidate Experience | 18 | 90% Standard |
| Candidate Address | 19 | 95% Standard |
| Candidate Referral | 3 | 100% Standard |
| Opportunity Core | 136 | 80% Standard |
| Opportunity Manager | 28 | 70% Standard |
| Opportunity Onboarding | 28 | 60% Standard |
| Opportunity Opening | 18 | 50% Standard + DFF |
| Opportunity Recruiter | 19 | 75% Standard |
| Opportunity Screening | 22 | 85% Standard |
| Opportunity Supervisor | 15 | 70% Standard |

### 2.2 Talentsoft Field Categories (320 Total)

| Category | Field Count | WordPlus Prefix | Oracle Coverage |
|----------|-------------|-----------------|-----------------|
| Vacancy Request (P-) | 85 | P- | 85% Standard |
| Vacancy/Offer (O-) | 120 | O- | 80% Standard |
| Applicant (A-) | 115 | A- | 90% Standard |

### 2.3 Critical GEODIS Custom Fields (Talentsoft)

| Talentsoft Field | WordPlus Tag | Business Purpose | Oracle Target |
|------------------|--------------|------------------|---------------|
| FTE % | [P-PreliminaryJobDescription_ShortText1] | Track FTE allocation | Requisition DFF |
| Working time (%) | [O-JobDescription_ShortText2] | Published FTE | Requisition DFF |
| Budgeted vacancy request | [P-Planned] | Budget approval flag | Requisition DFF |
| Name of person being replaced | [P-RequestMotive_ShortText1] | Incumbent tracking | Requisition DFF |
| Certifications | [A-Diploma_LongText2] | Candidate certifications | Candidate DFF |
| License Number | [A-Diploma_ShortText2] | Certification ID | Candidate DFF |
| Driving license (category) | [A-Diploma_ShortText1] | License type | Candidate DFF |
| Min gross annual salary | [P-PreliminaryJobDescription_ShortText2] | Salary range | Requisition DFF |
| Max gross annual salary | [P-PreliminaryJobDescription_ShortText3] | Salary range | Requisition DFF |
| Currency | [P-PreliminaryJobDescription_CustomCodeTableValue1] | Salary currency | Requisition DFF |

---

## 3. Oracle IRC Standard Field Mapping

### 3.1 Requisition Object (IRC_REQUISITIONS)

| Source Field (UKG/TS) | Oracle Standard Field | API Name | Data Type | Notes |
|-----------------------|----------------------|----------|-----------|-------|
| Requisition Number | Requisition Number | REQUISITION_NUMBER | VARCHAR2(30) | Auto-generated or manual |
| Job Title | Title | TITLE | VARCHAR2(240) | Required |
| Job Description | Description | DESCRIPTION | CLOB | Rich text supported |
| Company/Entity | Business Unit | BUSINESS_UNIT_ID | NUMBER | FK to HR_ORGANIZATION_UNITS |
| Department | Department | DEPARTMENT_ID | NUMBER | FK to HR_ORGANIZATION_UNITS |
| Location | Primary Location | PRIMARY_LOCATION_ID | NUMBER | FK to HR_LOCATIONS_ALL |
| Job Family | Job Family | JOB_FAMILY_ID | NUMBER | FK to PER_JOB_FAMILIES |
| Job | Job | JOB_ID | NUMBER | FK to PER_JOBS |
| Grade | Grade | GRADE_ID | NUMBER | FK to PER_GRADES |
| Headcount | Number of Openings | NUMBER_OF_OPENINGS | NUMBER | Integer value |
| Target Start Date | Target Start Date | TARGET_START_DATE | DATE | |
| Contract Type | Worker Type | WORKER_TYPE | VARCHAR2(30) | Lookup: WORKER_TYPE |
| Full-time/Part-time | Regular/Temporary | REGULAR_TEMPORARY | VARCHAR2(30) | Lookup |
| Hiring Manager | Hiring Manager | HIRING_MANAGER_ID | NUMBER | FK to PER_ALL_PEOPLE_F |
| Recruiter | Recruiter | RECRUITER_ID | NUMBER | FK to PER_ALL_PEOPLE_F |
| Reason for Opening | Requisition Reason | REQUISITION_REASON | VARCHAR2(30) | Lookup |
| Status | Phase | PHASE_CODE | VARCHAR2(30) | Requisition phase |
| Created Date | Creation Date | CREATION_DATE | DATE | System field |
| Requisition Template | Template | TEMPLATE_ID | NUMBER | FK to templates |

### 3.2 Candidate Object (IRC_CANDIDATES)

| Source Field (UKG/TS) | Oracle Standard Field | API Name | Data Type | Notes |
|-----------------------|----------------------|----------|-----------|-------|
| First Name | First Name | FIRST_NAME | VARCHAR2(150) | Required |
| Last Name | Last Name | LAST_NAME | VARCHAR2(150) | Required |
| Middle Name | Middle Name | MIDDLE_NAME | VARCHAR2(80) | Optional |
| Title | Title | TITLE | VARCHAR2(30) | Salutation |
| Email | Email Address | EMAIL_ADDRESS | VARCHAR2(240) | Primary email |
| Primary Phone | Phone Number | PHONE_NUMBER | VARCHAR2(60) | |
| Secondary Phone | Alternate Phone | ALTERNATE_PHONE | VARCHAR2(60) | |
| Address | Address Line 1 | ADDRESS_LINE_1 | VARCHAR2(240) | |
| City | City | CITY | VARCHAR2(60) | |
| State/Province | Region | REGION | VARCHAR2(120) | |
| Postal Code | Postal Code | POSTAL_CODE | VARCHAR2(30) | |
| Country | Country | COUNTRY_CODE | VARCHAR2(2) | ISO code |
| Nationality | Citizenship | CITIZENSHIP_ID | NUMBER | FK |
| Gender | Gender | SEX | VARCHAR2(30) | Lookup |
| Date of Birth | Date of Birth | DATE_OF_BIRTH | DATE | |
| Internal/External | Candidate Type | CANDIDATE_TYPE | VARCHAR2(30) | INTERNAL/EXTERNAL |
| Current Employer | Current Employer | CURRENT_EMPLOYER | VARCHAR2(240) | |
| Current Job Title | Current Job Title | CURRENT_JOB_TITLE | VARCHAR2(240) | |
| Education Level | Highest Education | HIGHEST_EDUCATION_LEVEL | VARCHAR2(30) | Lookup |
| Years of Experience | Years of Experience | YEARS_OF_EXPERIENCE | NUMBER | |
| Availability Date | Available Date | AVAILABLE_DATE | DATE | |
| Salary Expectations | Expected Salary | EXPECTED_SALARY | NUMBER | |
| Source | Source | SOURCE_ID | NUMBER | FK to sources |
| Referrer Name | Referred By | REFERRED_BY | VARCHAR2(240) | |
| Consent Status | Consent Status | CONSENT_STATUS | VARCHAR2(30) | GDPR |
| Veteran Status | Veteran Status | VETERAN_STATUS | VARCHAR2(30) | Lookup |
| Disability Status | Disability Status | DISABILITY_STATUS | VARCHAR2(30) | Lookup |

### 3.3 Job Application Object (IRC_JOB_APPLICATIONS)

| Source Field (UKG/TS) | Oracle Standard Field | API Name | Data Type | Notes |
|-----------------------|----------------------|----------|-----------|-------|
| Application ID | Application ID | APPLICATION_ID | NUMBER | PK |
| Requisition | Requisition | REQUISITION_ID | NUMBER | FK |
| Candidate | Candidate | CANDIDATE_ID | NUMBER | FK |
| Date Applied | Submission Date | SUBMISSION_DATE | DATE | |
| Status | Current Phase | CURRENT_PHASE_ID | NUMBER | FK to phases |
| State | Current State | CURRENT_STATE_ID | NUMBER | FK to states |
| Source | Source | SOURCE_ID | NUMBER | FK |
| Internal/External | Application Type | APPLICATION_TYPE | VARCHAR2(30) | |
| Screening Score | Prescreening Score | PRESCREENING_SCORE | NUMBER | |
| Overall Rating | Overall Rating | OVERALL_RATING | NUMBER | |

### 3.4 Offer Object (IRC_OFFERS)

| Source Field (UKG/TS) | Oracle Standard Field | API Name | Data Type | Notes |
|-----------------------|----------------------|----------|-----------|-------|
| Offer ID | Offer ID | OFFER_ID | NUMBER | PK |
| Application | Application | APPLICATION_ID | NUMBER | FK |
| Offer Date | Offer Date | OFFER_DATE | DATE | |
| Expiry Date | Expiration Date | EXPIRATION_DATE | DATE | |
| Base Salary | Proposed Salary | PROPOSED_SALARY | NUMBER | |
| Currency | Currency Code | CURRENCY_CODE | VARCHAR2(3) | ISO code |
| Start Date | Proposed Start Date | PROPOSED_START_DATE | DATE | |
| Status | Offer Status | OFFER_STATUS | VARCHAR2(30) | Lookup |
| Accept Date | Acceptance Date | ACCEPTANCE_DATE | DATE | |
| Offer Letter Template | Template | TEMPLATE_ID | NUMBER | FK |

### 3.5 Interview Object (IRC_INTERVIEWS)

| Source Field (UKG/TS) | Oracle Standard Field | API Name | Data Type | Notes |
|-----------------------|----------------------|----------|-----------|-------|
| Interview ID | Interview ID | INTERVIEW_ID | NUMBER | PK |
| Application | Application | APPLICATION_ID | NUMBER | FK |
| Interview Type | Interview Type | INTERVIEW_TYPE | VARCHAR2(30) | Lookup |
| Scheduled Date | Interview Date | INTERVIEW_DATE | DATE | |
| Start Time | Start Time | START_TIME | VARCHAR2(8) | HH:MI format |
| Duration | Duration (Minutes) | DURATION_MINUTES | NUMBER | |
| Location | Location | LOCATION | VARCHAR2(240) | |
| Interviewer | Interviewer | INTERVIEWER_ID | NUMBER | FK to person |
| Status | Status | STATUS | VARCHAR2(30) | Lookup |
| Feedback | Comments | COMMENTS | CLOB | |
| Rating | Overall Rating | OVERALL_RATING | NUMBER | 1-5 scale |
| Recommendation | Recommendation | RECOMMENDATION | VARCHAR2(30) | HIRE/NO_HIRE/MAYBE |

---

## 4. Required Flexfields (DFF) Configuration

### 4.1 Requisition Descriptive Flexfield (IRC_REQUISITIONS_DFF)

**Context:** GEODIS_REQUISITION

| Segment | Name | Column | Data Type | Value Set | Required | Source Field |
|---------|------|--------|-----------|-----------|----------|--------------|
| 1 | FTE Percentage | ATTRIBUTE1 | VARCHAR2(150) | GEODIS_FTE_PCT | N | [P-PreliminaryJobDescription_ShortText1] |
| 2 | Budgeted Position | ATTRIBUTE2 | VARCHAR2(150) | YES_NO | N | [P-Planned] |
| 3 | Budget Justification | ATTRIBUTE3 | VARCHAR2(2000) | None | N | [P-PreliminaryJobRequest_LongText1] |
| 4 | Incumbent Name | ATTRIBUTE4 | VARCHAR2(240) | None | N | [P-RequestMotive_ShortText1] |
| 5 | Incumbent Last Day | ATTRIBUTE_DATE1 | DATE | None | N | Custom field |
| 6 | Min Salary | ATTRIBUTE5 | VARCHAR2(150) | None | N | [P-PreliminaryJobDescription_ShortText2] |
| 7 | Max Salary | ATTRIBUTE6 | VARCHAR2(150) | None | N | [P-PreliminaryJobDescription_ShortText3] |
| 8 | Salary Currency | ATTRIBUTE7 | VARCHAR2(150) | GEODIS_CURRENCY | N | [P-PreliminaryJobDescription_CustomCodeTableValue1] |
| 9 | Priority | ATTRIBUTE8 | VARCHAR2(150) | GEODIS_PRIORITY | N | Custom |
| 10 | Impact to Staffing | ATTRIBUTE9 | VARCHAR2(150) | GEODIS_STAFFING_IMPACT | N | Custom |
| 11 | TOPEX Position | ATTRIBUTE10 | VARCHAR2(150) | YES_NO | N | TOPEX flag |
| 12 | Pole/Line of Business | ATTRIBUTE11 | VARCHAR2(150) | GEODIS_LOB | N | [P-CompanyInformation_CustomCodeTableValue1] |

### 4.2 Candidate Descriptive Flexfield (IRC_CANDIDATES_DFF)

**Context:** GEODIS_CANDIDATE

| Segment | Name | Column | Data Type | Value Set | Required | Source Field |
|---------|------|--------|-----------|-----------|----------|--------------|
| 1 | Driving License Category | ATTRIBUTE1 | VARCHAR2(150) | GEODIS_LICENSE_CAT | N | [A-Diploma_ShortText1] |
| 2 | License Number | ATTRIBUTE2 | VARCHAR2(150) | None | N | [A-Diploma_ShortText2] |
| 3 | Certifications | ATTRIBUTE3 | VARCHAR2(2000) | None | N | [A-Diploma_LongText2] |
| 4 | Computer Skills | ATTRIBUTE4 | VARCHAR2(2000) | None | N | [A-Diploma_LongText1] |
| 5 | Notice Period | ATTRIBUTE5 | VARCHAR2(150) | GEODIS_NOTICE_PERIOD | N | [A-NoticeDuration] |
| 6 | Salary Expectations | ATTRIBUTE6 | VARCHAR2(150) | None | N | [A-SalaryPretensions] |
| 7 | Mobility | ATTRIBUTE7 | VARCHAR2(150) | GEODIS_MOBILITY | N | [A-Mobility] |
| 8 | French RQTH Status | ATTRIBUTE8 | VARCHAR2(150) | YES_NO | N | [A-FrenchDisabledWorkerStatus] |
| 9 | Work Email | ATTRIBUTE9 | VARCHAR2(240) | None | N | [A-ProfessionalEmail] |
| 10 | Referrer Email | ATTRIBUTE10 | VARCHAR2(240) | None | N | [A-RecommendedBy2] |
| 11 | Referrer Phone | ATTRIBUTE11 | VARCHAR2(60) | None | N | [A-RecommendedBy3] |
| 12 | Source Medium | ATTRIBUTE12 | VARCHAR2(150) | GEODIS_SOURCE_MEDIUM | N | Custom |
| 13 | Preferred Language | ATTRIBUTE13 | VARCHAR2(150) | GEODIS_LANGUAGE | N | [A-StudiedLanguageCollection] |
| 14 | Race (US) | ATTRIBUTE14 | VARCHAR2(150) | US_RACE | N | [A-Race] |
| 15 | Ethnicity (US) | ATTRIBUTE15 | VARCHAR2(150) | US_ETHNICITY | N | [A-Ethnicity] |

### 4.3 Job Application Descriptive Flexfield (IRC_JOB_APPLICATIONS_DFF)

**Context:** GEODIS_APPLICATION

| Segment | Name | Column | Data Type | Value Set | Required | Source Field |
|---------|------|--------|-----------|-----------|----------|--------------|
| 1 | Referral Source | ATTRIBUTE1 | VARCHAR2(150) | GEODIS_REFERRAL_SRC | N | Referral details |
| 2 | Referral Employee ID | ATTRIBUTE2 | VARCHAR2(150) | None | N | Employee number |
| 3 | Assessment Score | ATTRIBUTE3 | VARCHAR2(150) | None | N | External assessment |
| 4 | Assessment Date | ATTRIBUTE_DATE1 | DATE | None | N | Assessment completion |
| 5 | Background Check Status | ATTRIBUTE4 | VARCHAR2(150) | GEODIS_BG_STATUS | N | Sterling status |
| 6 | Background Check Date | ATTRIBUTE_DATE2 | DATE | None | N | Check completion |
| 7 | E-Signature Status | ATTRIBUTE5 | VARCHAR2(150) | GEODIS_ESIGN_STATUS | N | DocuSign status |
| 8 | Previous Application ID | ATTRIBUTE6 | VARCHAR2(150) | None | N | Link to prior app |

### 4.4 Offer Descriptive Flexfield (IRC_OFFERS_DFF)

**Context:** GEODIS_OFFER

| Segment | Name | Column | Data Type | Value Set | Required | Source Field |
|---------|------|--------|-----------|-----------|----------|--------------|
| 1 | Salary Type | ATTRIBUTE1 | VARCHAR2(150) | GEODIS_SALARY_TYPE | N | Hourly/Annual |
| 2 | Variable Compensation | ATTRIBUTE2 | VARCHAR2(150) | None | N | Bonus amount |
| 3 | Sign-On Bonus | ATTRIBUTE3 | VARCHAR2(150) | None | N | One-time bonus |
| 4 | Relocation Package | ATTRIBUTE4 | VARCHAR2(150) | YES_NO | N | Relocation flag |
| 5 | Relocation Amount | ATTRIBUTE5 | VARCHAR2(150) | None | N | Relocation value |
| 6 | Work Schedule | ATTRIBUTE6 | VARCHAR2(150) | GEODIS_SCHEDULE | N | Shift type |
| 7 | Remote Work | ATTRIBUTE7 | VARCHAR2(150) | GEODIS_REMOTE | N | Remote/Hybrid/Onsite |
| 8 | Contract Duration | ATTRIBUTE8 | VARCHAR2(150) | None | N | For fixed-term |
| 9 | Probation Period | ATTRIBUTE9 | VARCHAR2(150) | GEODIS_PROBATION | N | Months |
| 10 | Counter Offer Flag | ATTRIBUTE10 | VARCHAR2(150) | YES_NO | N | Was counter offered |

### 4.5 Interview Descriptive Flexfield (IRC_INTERVIEWS_DFF)

**Context:** GEODIS_INTERVIEW

| Segment | Name | Column | Data Type | Value Set | Required | Source Field |
|---------|------|--------|-----------|-----------|----------|--------------|
| 1 | Interview Guide Used | ATTRIBUTE1 | VARCHAR2(150) | GEODIS_INT_GUIDE | N | Guide reference |
| 2 | Technical Score | ATTRIBUTE2 | VARCHAR2(150) | None | N | Technical rating |
| 3 | Cultural Fit Score | ATTRIBUTE3 | VARCHAR2(150) | None | N | Cultural rating |
| 4 | Leadership Score | ATTRIBUTE4 | VARCHAR2(150) | None | N | Leadership rating |
| 5 | Video Platform | ATTRIBUTE5 | VARCHAR2(150) | GEODIS_VIDEO_PLATFORM | N | Teams/Zoom/etc |

---

## 5. Extensible Flexfields (EFF) Requirements

### 5.1 Requisition EFF - Additional Job Details

**Category:** GEODIS_JOB_DETAILS

| Attribute | Name | Data Type | Description |
|-----------|------|-----------|-------------|
| EFF_ATTR1 | Required Certifications | Text(2000) | List of required certs |
| EFF_ATTR2 | Preferred Certifications | Text(2000) | Nice-to-have certs |
| EFF_ATTR3 | Required Languages | Multiselect | Language requirements |
| EFF_ATTR4 | Travel Requirement | Percentage | Travel % required |
| EFF_ATTR5 | Physical Requirements | Text(2000) | Physical demands |
| EFF_ATTR6 | Equipment Provided | Text(1000) | Company equipment |

### 5.2 Candidate EFF - Skills & Qualifications

**Category:** GEODIS_SKILLS

| Attribute | Name | Data Type | Description |
|-----------|------|-----------|-------------|
| EFF_ATTR1 | Technical Skills | Multiselect | From skills library |
| EFF_ATTR2 | Soft Skills | Multiselect | From skills library |
| EFF_ATTR3 | Industry Experience | Multiselect | Industries worked in |
| EFF_ATTR4 | Tools/Software | Text(2000) | Tools proficiency |
| EFF_ATTR5 | Language Proficiency | Table | Language + level matrix |

---

## 6. Value Sets Configuration

### 6.1 Independent Value Sets

#### GEODIS_FTE_PCT (FTE Percentage)

| Code | Meaning | Description |
|------|---------|-------------|
| 100 | 100% | Full-time |
| 90 | 90% | 4.5 days |
| 80 | 80% | 4 days |
| 75 | 75% | 3.75 days |
| 60 | 60% | 3 days |
| 50 | 50% | Half-time |
| 40 | 40% | 2 days |
| 25 | 25% | 1.25 days |
| 20 | 20% | 1 day |

#### GEODIS_PRIORITY (Hiring Priority)

| Code | Meaning | Description |
|------|---------|-------------|
| CRITICAL | Critical | Immediate fill required |
| HIGH | High | Fill within 30 days |
| MEDIUM | Medium | Standard timeline |
| LOW | Low | When suitable candidate found |
| PIPELINE | Pipeline | Future need |

#### GEODIS_CURRENCY (Salary Currency)

| Code | Meaning | Description |
|------|---------|-------------|
| EUR | Euro | European Union |
| USD | US Dollar | United States |
| GBP | British Pound | United Kingdom |
| CAD | Canadian Dollar | Canada |
| SGD | Singapore Dollar | Singapore |
| AUD | Australian Dollar | Australia |
| CHF | Swiss Franc | Switzerland |

#### GEODIS_LICENSE_CAT (Driving License)

| Code | Meaning | Description |
|------|---------|-------------|
| AM | AM | Moped |
| A1 | A1 | Light motorcycle |
| A2 | A2 | Medium motorcycle |
| A | A | Motorcycle |
| B | B | Car |
| B1 | B1 | Light quadricycle |
| BE | BE | Car + trailer |
| C | C | Truck |
| C1 | C1 | Medium truck |
| CE | CE | Truck + trailer |
| D | D | Bus |
| D1 | D1 | Minibus |
| DE | DE | Bus + trailer |

#### GEODIS_NOTICE_PERIOD (Notice Period)

| Code | Meaning | Description |
|------|---------|-------------|
| IMMEDIATE | Immediate | Available now |
| 1_WEEK | 1 Week | 1 week notice |
| 2_WEEKS | 2 Weeks | 2 weeks notice |
| 1_MONTH | 1 Month | 1 month notice |
| 2_MONTHS | 2 Months | 2 months notice |
| 3_MONTHS | 3 Months | 3 months notice |
| 6_MONTHS | 6 Months | 6 months notice |
| NEGOTIABLE | Negotiable | Flexible |

#### GEODIS_MOBILITY (Geographic Mobility)

| Code | Meaning | Description |
|------|---------|-------------|
| LOCAL | Local Only | Same city/area |
| REGIONAL | Regional | Same region/state |
| NATIONAL | National | Same country |
| INTERNATIONAL | International | Willing to relocate abroad |
| GLOBAL | Global | Any location |

#### GEODIS_LOB (Line of Business)

| Code | Meaning | Description |
|------|---------|-------------|
| D_AND_E | Distribution & Express | D&E division |
| FREIGHT | Freight Forwarding | FF division |
| CONTRACT | Contract Logistics | CL division |
| ROAD | Road Transport | RT division |
| SUPPLY | Supply Chain Optimization | SCO division |
| CORPORATE | Corporate Functions | HQ/Support |

#### GEODIS_BG_STATUS (Background Check Status)

| Code | Meaning | Description |
|------|---------|-------------|
| NOT_INITIATED | Not Initiated | Not yet started |
| CONSENT_PENDING | Consent Pending | Awaiting candidate consent |
| IN_PROGRESS | In Progress | Checks running |
| COMPLETE_CLEAR | Complete - Clear | All checks passed |
| COMPLETE_REVIEW | Complete - Review | Issues found, HR review |
| COMPLETE_FAIL | Complete - Failed | Check failed |
| EXPIRED | Expired | Consent expired |

#### GEODIS_ESIGN_STATUS (E-Signature Status)

| Code | Meaning | Description |
|------|---------|-------------|
| NOT_SENT | Not Sent | Document not sent |
| SENT | Sent | Awaiting signature |
| VIEWED | Viewed | Document opened |
| SIGNED | Signed | Fully signed |
| DECLINED | Declined | Candidate declined |
| EXPIRED | Expired | Signing period expired |
| VOIDED | Voided | Document voided |

#### GEODIS_SALARY_TYPE (Salary Type)

| Code | Meaning | Description |
|------|---------|-------------|
| ANNUAL | Annual Salary | Yearly base |
| MONTHLY | Monthly Salary | Monthly base |
| HOURLY | Hourly Rate | Per hour |
| DAILY | Daily Rate | Per day |

#### GEODIS_REMOTE (Remote Work)

| Code | Meaning | Description |
|------|---------|-------------|
| ONSITE | On-site | 100% office |
| HYBRID_1 | Hybrid (1 day remote) | 4 office, 1 remote |
| HYBRID_2 | Hybrid (2 days remote) | 3 office, 2 remote |
| HYBRID_3 | Hybrid (3 days remote) | 2 office, 3 remote |
| REMOTE | Fully Remote | 100% remote |
| FLEXIBLE | Flexible | As needed |

#### GEODIS_PROBATION (Probation Period)

| Code | Meaning | Description |
|------|---------|-------------|
| NONE | None | No probation |
| 1_MONTH | 1 Month | 1 month probation |
| 2_MONTHS | 2 Months | 2 months probation |
| 3_MONTHS | 3 Months | 3 months probation |
| 4_MONTHS | 4 Months | 4 months probation |
| 6_MONTHS | 6 Months | 6 months probation |

---

## 7. Field Transformation Rules

### 7.1 Name Transformations

| Source Pattern | Transformation | Target |
|----------------|----------------|--------|
| First Name + Middle Name + Last Name | Concatenate with space | Full Name |
| Title (Mr., Mrs., Dr.) | Direct map | IRC_CANDIDATES.TITLE |
| Suffix (Jr., Sr., III) | Append to Last Name | Not available - accept loss |
| Incumbent First + Last | Concatenate | Requisition DFF ATTRIBUTE4 |

### 7.2 Date Transformations

| Source Format | Transformation | Target Format |
|---------------|----------------|---------------|
| YYYY-MM-DD | Direct | Oracle DATE |
| DD/MM/YYYY | Convert | Oracle DATE |
| MM/DD/YYYY | Convert | Oracle DATE |
| Unix Timestamp | Convert | Oracle DATE |

### 7.3 Currency/Salary Transformations

| Source | Transformation | Target |
|--------|----------------|--------|
| Salary + Currency Code | Split | PROPOSED_SALARY + CURRENCY_CODE |
| Salary Range (50K-70K) | Parse Min/Max | DFF ATTRIBUTE5 + ATTRIBUTE6 |
| Hourly Rate | Store type + value | DFF ATTRIBUTE1 (type) + PROPOSED_SALARY |

### 7.4 Status/Phase Transformations

| UKG Status | Talentsoft Status | Oracle Phase | Oracle State |
|------------|-------------------|--------------|--------------|
| New | New Application | NEW | NEW_RECEIVED |
| Screened | Reviewed | REVIEW | REV_SHORTLIST |
| Interview Scheduled | Interview | INTERVIEW | INT_SCHEDULED |
| Interview Complete | Post-Interview | INTERVIEW | INT_COMPLETED |
| Offer Pending | Offer Created | OFFER | OFR_DRAFT |
| Offer Sent | Offer Extended | OFFER | OFR_EXTENDED |
| Offer Accepted | Hired | OFFER | OFR_ACCEPTED |
| Hired | Onboarding | HIRE | HIRE_COMPLETE |
| Rejected | Rejected | REJECTED | REJ_NOT_SELECTED |
| Withdrawn | Withdrawn | WITHDRAWN | WD_CANDIDATE |

### 7.5 Calculated Fields

| Field | Calculation | Storage |
|-------|-------------|---------|
| Days to Offer | Offer Date - Application Date | OTBI Calculated |
| Days to Accept | Accept Date - Offer Date | OTBI Calculated |
| Days to Start | Start Date - Accept Date | OTBI Calculated |
| Time to Fill | Hire Date - Requisition Open Date | OTBI Calculated |
| Time to Hire | Hire Date - Application Date | OTBI Calculated |
| Filled FTE | SUM(FTE) WHERE Status = 'Hired' | OTBI Calculated |
| Remaining FTE | Budgeted FTE - Filled FTE | OTBI Calculated |

---

## 8. Data Migration Mapping

### 8.1 HDL Business Objects

| Source Entity | HDL Object | HDL File Name |
|---------------|------------|---------------|
| Requisition | Requisition | Requisition.dat |
| Candidate | Candidate | Candidate.dat |
| Application | JobApplication | JobApplication.dat |
| Offer | Offer | Offer.dat |
| Interview | Interview | Interview.dat |
| Education | CandidateEducation | CandidateEducation.dat |
| Experience | CandidateWorkHistory | CandidateWorkHistory.dat |

### 8.2 Sample HDL Mapping (Requisition)

```
METADATA|Requisition|SourceSystemOwner|SourceSystemId|RequisitionNumber|Title|Description|BusinessUnitId|DepartmentId|JobId|GradeId|PrimaryLocationId|NumberOfOpenings|TargetStartDate|HiringManagerId|RecruiterId|PhaseCode|Attribute1|Attribute2|Attribute3|Attribute4
MERGE|Requisition|GEODIS_UKG|REQ-001|REQ-2024-0001|Senior Developer|Development role...|300000001234|300000005678|300000009012|300000003456|300000007890|2|2024-06-01|100000012345|100000067890|OPEN|100|Y||John Smith
```

### 8.3 Key Migration Considerations

| Consideration | UKG | Talentsoft | Oracle IRC |
|---------------|-----|------------|------------|
| Requisition ID | Opportunity ID | Offer Reference | REQUISITION_ID (auto) |
| Candidate ID | Candidate Key | ApplicantCode | CANDIDATE_ID (auto) |
| Application ID | Application Key | JobApplication ID | APPLICATION_ID (auto) |
| Cross-reference | Store in SOURCE_SYSTEM_ID | Store in SOURCE_SYSTEM_ID | Query by source reference |

---

## 9. Implementation Checklist

### 9.1 Pre-Configuration Tasks

- [ ] Confirm business unit hierarchy in Core HR
- [ ] Confirm department hierarchy in Core HR
- [ ] Confirm job catalog in Core HR
- [ ] Confirm grade structure in Core HR
- [ ] Confirm location setup in Core HR
- [ ] Map organization codes (UKG/TS → Oracle)
- [ ] Map job codes (UKG/TS → Oracle)
- [ ] Map location codes (UKG/TS → Oracle)

### 9.2 Value Set Creation

- [ ] Create GEODIS_FTE_PCT value set
- [ ] Create GEODIS_PRIORITY value set
- [ ] Create GEODIS_CURRENCY value set
- [ ] Create GEODIS_LICENSE_CAT value set
- [ ] Create GEODIS_NOTICE_PERIOD value set
- [ ] Create GEODIS_MOBILITY value set
- [ ] Create GEODIS_LOB value set
- [ ] Create GEODIS_BG_STATUS value set
- [ ] Create GEODIS_ESIGN_STATUS value set
- [ ] Create GEODIS_SALARY_TYPE value set
- [ ] Create GEODIS_REMOTE value set
- [ ] Create GEODIS_PROBATION value set

### 9.3 Flexfield Configuration

- [ ] Register IRC_REQUISITIONS_DFF context
- [ ] Configure 12 requisition DFF segments
- [ ] Register IRC_CANDIDATES_DFF context
- [ ] Configure 15 candidate DFF segments
- [ ] Register IRC_JOB_APPLICATIONS_DFF context
- [ ] Configure 8 application DFF segments
- [ ] Register IRC_OFFERS_DFF context
- [ ] Configure 10 offer DFF segments
- [ ] Register IRC_INTERVIEWS_DFF context
- [ ] Configure 5 interview DFF segments
- [ ] Deploy all flexfield configurations
- [ ] Test flexfield display in UI

### 9.4 Integration Testing

- [ ] Validate HDL import for requisitions
- [ ] Validate HDL import for candidates
- [ ] Validate HDL import for applications
- [ ] Validate HDL import for offers
- [ ] Validate HDL import for interviews
- [ ] Validate flexfield data population
- [ ] Validate value set lookups
- [ ] Validate cross-references

### 9.5 Reporting Validation

- [ ] Configure OTBI calculated fields
- [ ] Test Time to Fill calculation
- [ ] Test Time to Hire calculation
- [ ] Test FTE tracking calculations
- [ ] Test Days-to-X metrics
- [ ] Validate historical data accuracy

---

## Document Information

| Attribute | Value |
|-----------|-------|
| Document ID | 15_Oracle_IRC_Field_Mapping_Flexfields |
| Version | 1.0 |
| Created | 2025-12-07 |
| Total Fields Mapped | ~650 |
| DFF Segments | 50 |
| Value Sets | 12 |
| EFF Categories | 2 |

---

*End of Document*
