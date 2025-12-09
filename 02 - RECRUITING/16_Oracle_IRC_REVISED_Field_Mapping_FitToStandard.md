# GEODIS Oracle IRC - REVISED Field Mapping (Fit to Standard)

**Document:** 16_Oracle_IRC_REVISED_Field_Mapping_FitToStandard.md
**Version:** 2.0
**Created:** 2025-12-07
**Module:** Oracle Recruiting Cloud (IRC)
**Purpose:** MAXIMIZED standard field usage - MINIMIZED custom flexfields

---

## Executive Summary - REVISED

### Key Changes from Version 1.0

| Metric | Version 1.0 | Version 2.0 (REVISED) | Change |
|--------|-------------|----------------------|--------|
| DFF Segments Total | 50 | 18 | -64% |
| Requisition DFFs | 12 | 4 | -67% |
| Candidate DFFs | 15 | 8 | -47% |
| Application DFFs | 8 | 3 | -63% |
| Offer DFFs | 10 | 2 | -80% |
| Interview DFFs | 5 | 1 | -80% |
| Value Sets | 12 | 8 | -33% |

### Rationale

Per Oracle best practices and user requirements:
- **FTE** maps to standard `NUMBER_TO_HIRE` field
- **Salary Range** maps to standard `MIN_SALARY` / `MAX_SALARY` fields
- **Currency** maps to standard `SALARY_CURRENCY_CODE` field
- **Priority** maps to standard `HOT_JOB_FLAG` field
- **Incumbent** handled via `JUSTIFICATION_CODE` = REPLACEMENT + `COMMENTS` field
- **Workplace Type** maps to standard `WORKPLACE_TYPE_CODE` field

---

## 1. Requisition Mapping - FIT TO STANDARD

### 1.1 Standard Fields (USE THESE)

| GEODIS Source Field | Oracle Standard Field | Table.Column | Data Type | Notes |
|--------------------|----------------------|--------------|-----------|-------|
| FTE / Headcount | Number to Hire | IRC_REQUISITIONS_B.NUMBER_TO_HIRE | NUMBER(9) | **STANDARD - Use this instead of DFF** |
| Min Salary | Minimum Salary | IRC_REQUISITIONS_B.MIN_SALARY | NUMBER | **STANDARD - Use this instead of DFF** |
| Max Salary | Maximum Salary | IRC_REQUISITIONS_B.MAX_SALARY | NUMBER | **STANDARD - Use this instead of DFF** |
| Salary Currency | Salary Currency | IRC_REQUISITIONS_B.SALARY_CURRENCY_CODE | VARCHAR2(30) | **STANDARD - FK to FND_CURRENCIES** |
| Salary Frequency | Salary Frequency | IRC_REQUISITIONS_B.SALARY_FREQUENCY_CODE | VARCHAR2(30) | **STANDARD - Lookup: CMP_SALARY_BASIS** |
| Priority/Hot Job | Hot Job Flag | IRC_REQUISITIONS_B.HOT_JOB_FLAG | VARCHAR2(1) | **STANDARD - Y/N flag** |
| Workplace Type | Workplace Type | IRC_REQUISITIONS_B.WORKPLACE_TYPE_CODE | VARCHAR2(30) | **STANDARD - ONSITE/REMOTE/HYBRID** |
| Full/Part Time | Full/Part Time | IRC_REQUISITIONS_B.FULL_PART_TIME | VARCHAR2(30) | **STANDARD - Lookup** |
| Regular/Temporary | Regular/Temporary | IRC_REQUISITIONS_B.REGULAR_TEMPORARY | VARCHAR2(30) | **STANDARD - Lookup** |
| Justification (Replacement) | Justification Code | IRC_REQUISITIONS_B.JUSTIFICATION_CODE | VARCHAR2(30) | **STANDARD - Lookup: ORA_IRC_REQ_JUSTIFICATION** |
| Target Start Date | Target Start Date | IRC_REQUISITIONS_B.TARGET_START_DATE | DATE | **STANDARD** |
| Comments/Incumbent Info | Comments | IRC_REQUISITIONS_B.COMMENTS | CLOB | **STANDARD - Include incumbent name here** |
| Hiring Manager | Hiring Manager | IRC_REQUISITIONS_B.HIRING_MANAGER_ID | NUMBER(18) | **STANDARD - FK to PER_PERSONS** |
| Recruiter | Recruiter | IRC_REQUISITIONS_B.RECRUITER_ID | NUMBER(18) | **STANDARD - FK to PER_PERSONS** |
| Position | Position | IRC_REQUISITIONS_B.POSITION_ID | NUMBER(18) | **STANDARD - FK to HR_ALL_POSITIONS_F** |
| Job | Job | IRC_REQUISITIONS_B.JOB_ID | NUMBER(18) | **STANDARD - FK to PER_JOBS_F** |
| Department | Organization | IRC_REQUISITIONS_B.ORGANIZATION_ID | NUMBER(18) | **STANDARD - FK to HR_ALL_ORGANIZATION_UNITS** |
| Business Unit | Business Unit | IRC_REQUISITIONS_B.BUSINESS_UNIT_ID | NUMBER(18) | **STANDARD** |
| Location | Location | IRC_REQUISITIONS_B.LOCATION_ID | NUMBER(18) | **STANDARD - FK to PER_LOCATIONS** |
| Grade | Grade | IRC_REQUISITIONS_B.GRADE_ID | NUMBER(18) | **STANDARD - FK to PER_GRADES_F** |
| Evergreen | Evergreen Flag | IRC_REQUISITIONS_B.EVERGREEN_FLAG | VARCHAR2(1) | **STANDARD - Y/N** |

### 1.2 Requisition DFF - MINIMIZED (Only 4 Segments)

**Context:** GEODIS_REQUISITION

| Segment | Name | Column | Data Type | Value Set | Source Field | Justification |
|---------|------|--------|-----------|-----------|--------------|---------------|
| 1 | Budgeted Position | ATTRIBUTE_CHAR1 | VARCHAR2(150) | YES_NO | [P-Planned] | No standard field for budget flag |
| 2 | Budget Justification | ATTRIBUTE_CHAR2 | VARCHAR2(2000) | None | [P-PreliminaryJobRequest_LongText1] | No standard long text for budget |
| 3 | TOPEX Position | ATTRIBUTE_CHAR3 | VARCHAR2(150) | YES_NO | Custom | GEODIS-specific classification |
| 4 | Pole/Line of Business | ATTRIBUTE_CHAR4 | VARCHAR2(150) | GEODIS_LOB | [P-CompanyInformation_CustomCodeTableValue1] | GEODIS-specific segmentation |

**REMOVED from DFF (Now Standard):**
- ~~FTE Percentage~~ → Use NUMBER_TO_HIRE
- ~~Min Salary~~ → Use MIN_SALARY
- ~~Max Salary~~ → Use MAX_SALARY
- ~~Salary Currency~~ → Use SALARY_CURRENCY_CODE
- ~~Priority~~ → Use HOT_JOB_FLAG
- ~~Incumbent Name~~ → Use COMMENTS field with format "Replacing: [Name]"
- ~~Incumbent Last Day~~ → Use COMMENTS field
- ~~Impact to Staffing~~ → Not critical, use COMMENTS if needed

### 1.3 Incumbent/Replacement Handling - STANDARD APPROACH

Instead of custom DFF for incumbent information, use:

1. **JUSTIFICATION_CODE** = 'REPLACEMENT' (Standard Lookup Value)
2. **COMMENTS** field with structured format:
   ```
   Replacement Hire
   Incumbent: [First Name] [Last Name]
   Last Day: [Date]
   Reason: [Departure Reason]
   ```
3. **POSITION_ID** - Links to position history showing previous incumbent

---

## 2. Candidate Mapping - FIT TO STANDARD

### 2.1 Standard Fields (USE THESE)

| GEODIS Source Field | Oracle Standard Field | Table.Column | Data Type | Notes |
|--------------------|----------------------|--------------|-----------|-------|
| First Name | First Name | PER_PERSONS.FIRST_NAME | VARCHAR2(150) | **STANDARD** |
| Last Name | Last Name | PER_PERSONS.LAST_NAME | VARCHAR2(150) | **STANDARD** |
| Email | Email Address | PER_EMAIL_ADDRESSES.EMAIL_ADDRESS | VARCHAR2(240) | **STANDARD** |
| Phone | Phone Number | PER_PHONES.PHONE_NUMBER | VARCHAR2(60) | **STANDARD** |
| Address | Address | PER_ADDRESSES.* | Multiple | **STANDARD** |
| Availability Date | Availability Date | IRC_CANDIDATES.AVAILABILITY_DATE | DATE | **STANDARD** |
| Preferred Language | Preferred Language | IRC_CANDIDATES.CAND_PREF_LANGUAGE_CODE | VARCHAR2(4) | **STANDARD** |
| Nationality | Citizenship | PER_CITIZENSHIPS.CITIZENSHIP_ID | NUMBER | **STANDARD** |
| Gender | Gender | PER_PERSONS.SEX | VARCHAR2(30) | **STANDARD** |
| Date of Birth | Date of Birth | PER_PERSONS.DATE_OF_BIRTH | DATE | **STANDARD** |
| Disability Status | Disability | PER_DISABILITIES.* | Multiple | **STANDARD** |
| Veteran Status | Veteran | PER_VETERANS.* | Multiple | **STANDARD - US specific** |
| Skills | Skills | HRT_PROFILES_B (Skills section) | Multiple | **STANDARD - Talent Profile** |
| Education | Education | HRT_PROFILES_B (Education section) | Multiple | **STANDARD - Talent Profile** |
| Experience | Work History | HRT_PROFILES_B (Experience section) | Multiple | **STANDARD - Talent Profile** |
| Resume | Attachments | IRC_DOCUMENTS | BLOB | **STANDARD** |

### 2.2 Candidate DFF - MINIMIZED (Only 8 Segments)

**Context:** GEODIS_CANDIDATE

| Segment | Name | Column | Data Type | Value Set | Source Field | Justification |
|---------|------|--------|-----------|-----------|--------------|---------------|
| 1 | Driving License Category | ATTRIBUTE_CHAR1 | VARCHAR2(150) | GEODIS_LICENSE_CAT | [A-Diploma_ShortText1] | Not in standard Oracle |
| 2 | License Number | ATTRIBUTE_CHAR2 | VARCHAR2(150) | None | [A-Diploma_ShortText2] | Not in standard Oracle |
| 3 | Certifications | ATTRIBUTE_CHAR3 | VARCHAR2(2000) | None | [A-Diploma_LongText2] | Beyond standard profile |
| 4 | Notice Period | ATTRIBUTE_CHAR4 | VARCHAR2(150) | GEODIS_NOTICE_PERIOD | [A-NoticeDuration] | Not in standard Oracle |
| 5 | Mobility | ATTRIBUTE_CHAR5 | VARCHAR2(150) | GEODIS_MOBILITY | [A-Mobility] | Not in standard Oracle |
| 6 | French RQTH Status | ATTRIBUTE_CHAR6 | VARCHAR2(150) | YES_NO | [A-FrenchDisabledWorkerStatus] | France-specific regulation |
| 7 | Source Medium | ATTRIBUTE_CHAR7 | VARCHAR2(150) | GEODIS_SOURCE_MEDIUM | Custom | Beyond standard source |
| 8 | Referrer Details | ATTRIBUTE_CHAR8 | VARCHAR2(500) | None | Combined email/phone | Reference contact info |

**REMOVED from DFF (Now Standard or Not Needed):**
- ~~Computer Skills~~ → Use Talent Profile Skills section
- ~~Salary Expectations~~ → Capture during application or offer
- ~~Work Email~~ → Use standard PER_EMAIL_ADDRESSES with type
- ~~Race (US)~~ → Use standard PER_PERSONS.ETHNICITY
- ~~Ethnicity (US)~~ → Use standard PER_PERSONS.ETHNICITY
- ~~Preferred Language~~ → Use CAND_PREF_LANGUAGE_CODE

---

## 3. Job Application (Submission) Mapping - FIT TO STANDARD

### 3.1 Standard Fields (USE THESE)

| GEODIS Source Field | Oracle Standard Field | Table.Column | Data Type | Notes |
|--------------------|----------------------|--------------|-----------|-------|
| Application ID | Submission ID | IRC_SUBMISSIONS.SUBMISSION_ID | NUMBER(18) | **STANDARD - Auto generated** |
| Requisition | Requisition | IRC_SUBMISSIONS.REQUISITION_ID | NUMBER(18) | **STANDARD - FK** |
| Candidate | Person | IRC_SUBMISSIONS.PERSON_ID | NUMBER(18) | **STANDARD - FK** |
| Application Date | Submission Date | IRC_SUBMISSIONS.SUBMISSION_DATE | DATE | **STANDARD** |
| Current Phase | Current Phase | IRC_SUBMISSIONS.CURRENT_PHASE_ID | NUMBER(18) | **STANDARD - FK** |
| Current State | Current State | IRC_SUBMISSIONS.CURRENT_STATE_ID | NUMBER(18) | **STANDARD - FK** |
| Internal/External | Internal Flag | IRC_SUBMISSIONS.INTERNAL_FLAG | VARCHAR2(1) | **STANDARD - Y/N** |
| Active Status | Active Flag | IRC_SUBMISSIONS.ACTIVE_FLAG | VARCHAR2(1) | **STANDARD - Y/N** |
| Questionnaire Score | Questionnaire Score | IRC_SUBMISSIONS.QSTNR_SCORE | NUMBER(18) | **STANDARD** |
| Source | Site Number | IRC_SUBMISSIONS.SITE_NUMBER | VARCHAR2(240) | **STANDARD - Career Site** |
| Source Context | Added By Context | IRC_SUBMISSIONS.ADDED_BY_CONTEXT_CODE | VARCHAR2(30) | **STANDARD** |
| Referral Info | Added By Person | IRC_SUBMISSIONS.ADDED_BY_PERSON_ID | NUMBER(18) | **STANDARD - Who added** |

### 3.2 Application DFF - MINIMIZED (Only 3 Segments)

**Context:** GEODIS_APPLICATION

| Segment | Name | Column | Data Type | Value Set | Source Field | Justification |
|---------|------|--------|-----------|-----------|--------------|---------------|
| 1 | Assessment Score | ATTRIBUTE_CHAR1 | VARCHAR2(150) | None | External assessment | Third-party assessment scores |
| 2 | Background Check Status | ATTRIBUTE_CHAR2 | VARCHAR2(150) | GEODIS_BG_STATUS | Sterling status | Pre-hire check tracking |
| 3 | E-Signature Status | ATTRIBUTE_CHAR3 | VARCHAR2(150) | GEODIS_ESIGN_STATUS | DocuSign status | Digital signature tracking |

**REMOVED from DFF (Now Standard or Not Needed):**
- ~~Referral Source~~ → Use ADDED_BY_CONTEXT_CODE + SITE_NUMBER
- ~~Referral Employee ID~~ → Use ADDED_BY_PERSON_ID
- ~~Assessment Date~~ → Use CREATION_DATE of assessment attachment
- ~~Background Check Date~~ → Include in status field value
- ~~Previous Application ID~~ → Query historical submissions by PERSON_ID

---

## 4. Offer Mapping - FIT TO STANDARD

### 4.1 Standard Fields (USE THESE)

| GEODIS Source Field | Oracle Standard Field | Table.Column | Data Type | Notes |
|--------------------|----------------------|--------------|-----------|-------|
| Offer ID | Offer ID | IRC_OFFERS.OFFER_ID | NUMBER(18) | **STANDARD** |
| Application | Submission | IRC_OFFERS.SUBMISSION_ID | NUMBER(18) | **STANDARD - FK** |
| Candidate | Person | IRC_OFFERS.PERSON_ID | NUMBER(18) | **STANDARD - FK** |
| Recruiter | Recruiter | IRC_OFFERS.RECRUITER_ID | NUMBER(18) | **STANDARD** |
| Hiring Manager | Hiring Manager | IRC_OFFERS.HIRING_MANAGER_ID | NUMBER(18) | **STANDARD** |
| Expiration Date | Expiration Date | IRC_OFFERS.EXPIRATION_DATE | DATE | **STANDARD** |
| Status | Object Status | IRC_OFFERS.OBJECT_STATUS | VARCHAR2(30) | **STANDARD** |
| Draft Date | Drafted Date | IRC_OFFERS.DRAFTED_DATE | TIMESTAMP | **STANDARD** |
| Approved Date | Approved Date | IRC_OFFERS.APPROVED_DATE | TIMESTAMP | **STANDARD** |
| Extended Date | Extended Date | IRC_OFFERS.EXTENDED_DATE | TIMESTAMP | **STANDARD** |
| Accepted Date | Accepted Date | IRC_OFFERS.ACCEPTED_DATE | TIMESTAMP | **STANDARD** |
| Comments | Offer Comments | IRC_OFFERS.OFFER_COMMENTS | CLOB | **STANDARD** |
| Additional Text | Additional Text 1/2 | IRC_OFFERS.ADDITIONALTEXT1/2 | CLOB | **STANDARD** |
| **Salary Info** | **Job Offer Salary Section** | CMP_SALARY + Assignment | Multiple | **STANDARD - Via UI/API** |
| **Compensation Plans** | **Other Compensation Section** | CMP_* tables | Multiple | **STANDARD - Via UI/API** |

### 4.2 Offer Salary - STANDARD APPROACH

Oracle Recruiting handles offer salary through the **Job Offer Salary Section** (not stored in IRC_OFFERS):

| Field | Location | Standard? |
|-------|----------|-----------|
| Salary Basis | Job Offer UI → CMP_SALARY_BASES | YES |
| Salary Amount | Job Offer UI → CMP_SALARY.SALARY_AMOUNT | YES |
| Currency | Derived from Salary Basis | YES |
| Frequency | Derived from Salary Basis | YES |
| Grade Rate | Pre-filled from Grade selection | YES |
| Min/Max Range | Displayed from Grade setup | YES |

**No DFF needed for standard salary fields!**

### 4.3 Offer DFF - MINIMIZED (Only 2 Segments)

**Context:** GEODIS_OFFER

| Segment | Name | Column | Data Type | Value Set | Source Field | Justification |
|---------|------|--------|-----------|-----------|--------------|---------------|
| 1 | Relocation Package | ATTRIBUTE_CHAR1 | VARCHAR2(150) | YES_NO | Custom | Not in standard Oracle offer |
| 2 | Relocation Amount | ATTRIBUTE_NUMBER1 | NUMBER | None | Custom | Relocation budget |

**REMOVED from DFF (Now Standard or Not Needed):**
- ~~Salary Type~~ → Use Salary Basis (standard)
- ~~Variable Compensation~~ → Use Other Compensation section (standard)
- ~~Sign-On Bonus~~ → Use Other Compensation section (standard)
- ~~Work Schedule~~ → Part of Assignment Info (standard)
- ~~Remote Work~~ → Use WORKPLACE_TYPE_CODE from requisition
- ~~Contract Duration~~ → Part of Assignment setup (standard)
- ~~Probation Period~~ → Part of Assignment setup (standard)
- ~~Counter Offer Flag~~ → Track via offer versions/REDRAFT_COUNT

---

## 5. Interview Mapping - FIT TO STANDARD

### 5.1 Standard Fields (Pending Oracle Schema)

| GEODIS Source Field | Oracle Standard Field | Notes |
|--------------------|----------------------|-------|
| Interview ID | Interview ID | **STANDARD** |
| Application | Submission ID | **STANDARD - FK** |
| Interview Type | Interview Type | **STANDARD - Lookup** |
| Date/Time | Interview Date/Time | **STANDARD** |
| Duration | Duration | **STANDARD** |
| Interviewer | Interviewer ID | **STANDARD - FK** |
| Status | Status | **STANDARD - Lookup** |
| Feedback | Comments | **STANDARD - CLOB** |
| Rating | Overall Rating | **STANDARD** |
| Recommendation | Recommendation | **STANDARD - Lookup** |

### 5.2 Interview DFF - MINIMIZED (Only 1 Segment)

**Context:** GEODIS_INTERVIEW

| Segment | Name | Column | Data Type | Value Set | Source Field | Justification |
|---------|------|--------|-----------|-----------|--------------|---------------|
| 1 | Video Platform | ATTRIBUTE_CHAR1 | VARCHAR2(150) | GEODIS_VIDEO_PLATFORM | Custom | Track virtual interview platform |

**REMOVED from DFF (Not Needed):**
- ~~Interview Guide Used~~ → Track via interview type/template
- ~~Technical Score~~ → Use structured feedback or rating categories
- ~~Cultural Fit Score~~ → Use structured feedback or rating categories
- ~~Leadership Score~~ → Use structured feedback or rating categories

---

## 6. REVISED Value Sets (Reduced from 12 to 8)

### Active Value Sets

| Value Set | Purpose | Used By |
|-----------|---------|---------|
| GEODIS_LOB | Line of Business | Requisition DFF |
| GEODIS_LICENSE_CAT | Driving License | Candidate DFF |
| GEODIS_NOTICE_PERIOD | Notice Period | Candidate DFF |
| GEODIS_MOBILITY | Geographic Mobility | Candidate DFF |
| GEODIS_SOURCE_MEDIUM | Candidate Source | Candidate DFF |
| GEODIS_BG_STATUS | Background Check | Application DFF |
| GEODIS_ESIGN_STATUS | E-Signature | Application DFF |
| GEODIS_VIDEO_PLATFORM | Video Interview | Interview DFF |

### REMOVED Value Sets (Now Standard)

| Value Set | Replaced By |
|-----------|-------------|
| ~~GEODIS_FTE_PCT~~ | NUMBER_TO_HIRE (integer) |
| ~~GEODIS_PRIORITY~~ | HOT_JOB_FLAG (Y/N) |
| ~~GEODIS_CURRENCY~~ | FND_CURRENCIES (standard) |
| ~~GEODIS_SALARY_TYPE~~ | CMP_SALARY_BASIS (standard) |
| ~~GEODIS_REMOTE~~ | ORA_IRC_WORKPLACE_TYPE (standard) |
| ~~GEODIS_PROBATION~~ | Assignment setup (standard) |

---

## 7. Implementation Summary

### 7.1 What Changed

| Area | Before (v1.0) | After (v2.0) | Benefit |
|------|---------------|--------------|---------|
| Salary Range | DFF ATTRIBUTE5/6 | MIN_SALARY/MAX_SALARY | Standard reporting, no config |
| FTE | DFF ATTRIBUTE1 | NUMBER_TO_HIRE | Standard tracking, aggregation |
| Currency | DFF ATTRIBUTE7 | SALARY_CURRENCY_CODE | FK to FND_CURRENCIES |
| Priority | DFF ATTRIBUTE8 | HOT_JOB_FLAG | Standard urgent job tracking |
| Incumbent | DFF ATTRIBUTE4 | COMMENTS + JUSTIFICATION_CODE | Position-based tracking |
| Remote Work | Offer DFF ATTRIBUTE7 | WORKPLACE_TYPE_CODE | Standard lookup |
| Salary Type | Offer DFF ATTRIBUTE1 | Salary Basis (UI) | Standard compensation |

### 7.2 Migration Impact

| Item | Impact |
|------|--------|
| HDL Templates | Simpler - use standard columns |
| Data Conversion | Easier - standard field mappings |
| Reporting (OTBI) | Better - no custom subject areas for DFFs |
| UI Configuration | Less - fewer DFF segments to configure |
| Testing | Reduced - fewer custom fields to validate |
| Maintenance | Lower - standard fields maintained by Oracle |

### 7.3 Remaining DFFs Summary

| Object | DFF Segments | Purpose |
|--------|--------------|---------|
| Requisition | 4 | Budget tracking, GEODIS classification |
| Candidate | 8 | License, certifications, mobility, France-specific |
| Application | 3 | Third-party integrations (assessment, background, e-sign) |
| Offer | 2 | Relocation package |
| Interview | 1 | Video platform tracking |
| **TOTAL** | **18** | **Reduced from 50 (-64%)** |

---

## 8. Configuration Checklist - REVISED

### 8.1 Standard Field Configuration (Priority 1)

- [ ] Verify MIN_SALARY/MAX_SALARY fields enabled on requisition form
- [ ] Verify NUMBER_TO_HIRE field enabled and labeled as "Headcount/FTE"
- [ ] Verify SALARY_CURRENCY_CODE linked to FND_CURRENCIES
- [ ] Verify SALARY_FREQUENCY_CODE lookup: CMP_SALARY_BASIS
- [ ] Verify HOT_JOB_FLAG enabled and labeled as "Priority"
- [ ] Verify WORKPLACE_TYPE_CODE lookup: ORA_IRC_WORKPLACE_TYPE
- [ ] Verify JUSTIFICATION_CODE lookup includes "REPLACEMENT" value
- [ ] Configure Job Offer Salary Section
- [ ] Configure Job Offer Other Compensation Section

### 8.2 DFF Configuration (Priority 2)

- [ ] Create 4 Requisition DFF segments
- [ ] Create 8 Candidate DFF segments
- [ ] Create 3 Application DFF segments
- [ ] Create 2 Offer DFF segments
- [ ] Create 1 Interview DFF segment
- [ ] Deploy flexfield configurations

### 8.3 Value Set Configuration (Priority 2)

- [ ] Create GEODIS_LOB value set
- [ ] Create GEODIS_LICENSE_CAT value set
- [ ] Create GEODIS_NOTICE_PERIOD value set
- [ ] Create GEODIS_MOBILITY value set
- [ ] Create GEODIS_SOURCE_MEDIUM value set
- [ ] Create GEODIS_BG_STATUS value set
- [ ] Create GEODIS_ESIGN_STATUS value set
- [ ] Create GEODIS_VIDEO_PLATFORM value set

### 8.4 Testing Checklist

- [ ] Test NUMBER_TO_HIRE tracking and aggregation
- [ ] Test MIN_SALARY/MAX_SALARY display and validation
- [ ] Test HOT_JOB_FLAG filtering
- [ ] Test WORKPLACE_TYPE_CODE values
- [ ] Test Job Offer Salary Section flow
- [ ] Test DFF data entry and display
- [ ] Validate OTBI reporting on standard fields

---

## Document Information

| Attribute | Value |
|-----------|-------|
| Document ID | 16_Oracle_IRC_REVISED_Field_Mapping_FitToStandard |
| Version | 2.0 |
| Created | 2025-12-07 |
| Supersedes | 15_Oracle_IRC_Field_Mapping_Flexfields (v1.0) |
| Total DFF Segments | 18 (reduced from 50) |
| Value Sets | 8 (reduced from 12) |
| Standard Field Usage | 90%+ |

---

*End of Revised Document*
