# UPDATED Gap Analysis: UKG vs Talentsoft (GEODIS Configuration)

**Document Version:** 2.2
**Date:** 2025-11-23
**Based on:** Actual GEODIS Talentsoft UI Screenshots + PDF Documentation Review
**Excel Reference:** `UKG_Talentsoft_Holistic_Mapping_CORRECTED.xlsx` (594 fields mapped, 34 corrections)

---

## IMPORTANT UPDATES FROM SCREENSHOTS

After reviewing the actual GEODIS Talentsoft field configuration, several gaps identified earlier are **NOW ADDRESSED** through custom fields or standard fields.

---

## CRITICAL: WordPlus Tag Corrections (2025-11-23)

A mismatch analysis was performed comparing the Excel mapping against the official PDF documentation. **34 tag corrections** were identified and applied.

### Tag Prefix Rules (from PDF Documentation)

| Prefix | Object Type | Description |
|--------|-------------|-------------|
| **P-** | Vacancy Request | Job Request fields (PreliminaryJobRequest) |
| **O-** | Vacancy/Offer | Published vacancy fields |
| **A-** | Applicant | Candidate personal data fields |

### Corrections Summary by Category

| Category | Count | Issue | Correction |
|----------|-------|-------|------------|
| **Manager fields** | 9 | Used `[A-...]` prefix | Changed to `[P-OperationalManager...] / [O-OperationalManager...]` |
| **Supervisor fields** | 5 | Used `[A-...]` prefix | Changed to `[O-MainSupervisor...]` |
| **Recruiter fields** | 5 | Used `[A-...]` prefix | Changed to `[O-MainSupervisor...]` |
| **Onboarding fields** | 2 | Email → Address error | Changed to `[O-PublicationEmail]` |
| **Candidate Email** | 7 | `[A-Address]` semantic error | Changed to `[A-Email]` |
| **Opportunity Location** | 3 | Used `[A-City/Country]` | Changed to `[O-JobLocation]` / `[O-Location_...]` |
| **Opportunity Title** | 3 | Used `[A-Civility]` | Changed to `[P-JobTitle] / [O-JobTitle]` |

### Key Corrections Applied

| Excel Row | UKG Field | FROM (Wrong) | TO (Correct) |
|-----------|-----------|--------------|--------------|
| 51 | Manager Email | `[A-Address]` | `[P-OperationalManagerEmail] / [O-OperationalManagerEmail]` |
| 55, 225 | Manager First Name | `[A-FirstName]` | `[P-OperationalManagerFirstName] / [O-OperationalManagerFirstName]` |
| 57, 228 | Manager Last Name | `[A-Name]` | `[P-OperationalManagerName] / [O-OperationalManagerName]` |
| 73 | Supervisor Email | `[A-Address]` | `[O-MainSupervisorEmail]` |
| 84 | Recruiter Email | `[A-Address]` | `[O-MainSupervisorEmail]` |
| 164-167, 287, 402 | Candidate Email | `[A-Address]` | `[A-Email]` |
| 128, 363-364 | Opportunity Title | `[A-Civility] / [A-Title]` | `[P-JobTitle] / [O-JobTitle]` |

### Files Generated

| File | Description |
|------|-------------|
| `UKG_Talentsoft_Holistic_Mapping_BACKUP.xlsx` | Original file backup |
| `UKG_Talentsoft_Holistic_Mapping_CORRECTED.xlsx` | **Corrected mapping file** |
| `UKG_Talentsoft_Mapping_CORRECTIONS.xlsx` | Detailed corrections report |

---

## 1. GAPS NOW ADDRESSED IN GEODIS TALENTSOFT

### 1.1 INCUMBENT / REPLACEMENT - ADDRESSED

| UKG Field | Talentsoft Field (GEODIS) | Location |
|-----------|---------------------------|----------|
| Incumbent First Name | `Name of person being replaced` | Vacancy Request → Reason for Request |
| Incumbent Last Name | [P-RequestMotive_ShortText1] | Single text field (First + Last) |
| Replacement Reason | `Replacement after internal promotion` | Vacancy Request → General Info |
| | [P-PreliminaryJobRequest_CustomCodeTableValue1] | Selection list |

**Status:** PARTIALLY ADDRESSED - Name available as single field, not split First/Last

---

### 1.2 BUDGETED OPENING - FULLY ADDRESSED

| UKG Field | Talentsoft Field (GEODIS) | Location |
|-----------|---------------------------|----------|
| Is Opening Budgeted? | `Budgeted vacancy request` | Vacancy Request → General Info |
| | [P-Planned] | Radio buttons (Yes/No) |
| Budget Justification | `If not planned, please justify` | Vacancy Request → General Info |
| | [P-PreliminaryJobRequest_LongText1] | Text area |

**Status:** FULLY ADDRESSED

---

### 1.3 FTE TRACKING - PARTIALLY ADDRESSED

| UKG Field | Talentsoft Field (GEODIS) | Location |
|-----------|---------------------------|----------|
| FTE % | `FTE %` [P-PreliminaryJobDescription_ShortText1] | Vacancy Request → Position Description |
| | `Working time (%)` [O-JobDescription_ShortText2] | Vacancy → Position Description |
| Budgeted FTE | Can use FTE % field | - |
| Filled FTE | **NOT AVAILABLE** | Must calculate |
| Remaining FTE | **NOT AVAILABLE** | Must calculate |

**Status:** PARTIALLY ADDRESSED - FTE % available, but no tracking of Filled/Remaining

---

### 1.4 LICENSES & CERTIFICATIONS - FULLY ADDRESSED

| UKG Field | Talentsoft Field (GEODIS) | Location |
|-----------|---------------------------|----------|
| License/Certification Name | `Certifications` [A-Diploma_LongText2] | Candidate → Education |
| License Number | `If yes, Number` [A-Diploma_ShortText2] | Candidate → Education |
| Driving License | `Driving license (category)` [A-Diploma_ShortText1] | Candidate → Education |
| | `Driving licence(s)` [P-...CustomBlock4_LongText1] | Vacancy Request → Custom Section 4 |
| | `Driving license` [O-ApplicantCriteria_LongText1] | Vacancy → Candidate Criteria |

**Status:** FULLY ADDRESSED

---

### 1.5 CANDIDATE MIDDLE NAME - AVAILABLE

| UKG Field | Talentsoft Field (GEODIS) | Location |
|-----------|---------------------------|----------|
| Middle Name | `Middle name` [A-MiddleName] | Candidate → Candidate section |
| | `Middle name` [A-PersonalInformation_ShortText1] | Candidate → Personal Information |

**Status:** AVAILABLE (may need to be activated)

---

## 2. REMAINING GAPS - STILL NOT AVAILABLE

### 2.1 MANAGER NAME DETAILS - NOT AVAILABLE

| UKG Field | Talentsoft Status | Impact |
|-----------|-------------------|--------|
| Hiring Manager Title (Mr., Mrs., Dr.) | **NOT AVAILABLE** | Low |
| Hiring Manager Middle Name | **NOT AVAILABLE** | Low |
| Hiring Manager Suffix (Jr., Sr., III) | **NOT AVAILABLE** | Low |
| Onboarding Owner Title/Middle/Suffix | **NOT AVAILABLE** | Low |
| Supervisor Title/Middle/Suffix | **NOT AVAILABLE** | Low |
| Recruiter Title/Middle/Suffix | **NOT AVAILABLE** | Low |

**Available Manager Fields in GEODIS (CORRECTED):**
- Manager last name: `[P-OperationalManagerName] / [O-OperationalManagerName]`
- Manager first name: `[P-OperationalManagerFirstName] / [O-OperationalManagerFirstName]`
- Email: `[P-OperationalManagerEmail] / [O-OperationalManagerEmail]`
- Manager phone number: `[P-OperationalManagerPhoneNumber] / [O-OperationalManagerPhoneNumber]`
- Hiring Manager's language: `[P-OperationalManagerLanguage] / [O-OperationalManagerLanguage]`

**Note:** Use `P-` prefix for Vacancy Request context, `O-` prefix for Vacancy/Offer context.

**Recommendation:** Accept data loss or concatenate Title/Suffix into name field

---

### 2.2 INCUMBENT LAST DAY WORKED - NOT AVAILABLE

| UKG Field | Talentsoft Status |
|-----------|-------------------|
| Last Day Worked | **NOT AVAILABLE** |

**Workaround:** Could add custom date field in Vacancy Request form

---

### 2.3 FTE TRACKING GRANULARITY - NOT AVAILABLE

| UKG Field | Talentsoft Status | Workaround |
|-----------|-------------------|------------|
| Filled FTE | **NOT TRACKED** | Calculate from hired applications |
| Remaining FTE | **NOT TRACKED** | Calculate: Budgeted - Filled |
| Filled Headcount | **NOT TRACKED** | Count applications with Hired status |
| Remaining Headcount | **NOT TRACKED** | Calculate: NumberOfVacancies - Filled |

**Calculation Required:**
```sql
Filled = COUNT(applications WHERE status = 'Hired')
Remaining = NumberOfVacancies - Filled
```

---

### 2.4 DAYS-TO-HIRE METRICS - MUST CALCULATE

| UKG Metric | Talentsoft Status |
|------------|-------------------|
| Days Between Accept and Offer Dates | **CALCULATE** |
| Days Between Accept and Start Dates | **CALCULATE** |
| Days Between Hire and Publish Dates | **CALCULATE** |
| Days Between Offer and Start Dates | **CALCULATE** |
| Days Between Start and Publish Dates | **CALCULATE** |

**Data Sources:**
- Event dates from: `SDD_APPLICATION_EVENTS.csv`
- Publication date from: `SDD_VACANCIES.csv` → `FirstPublicationDate`

---

## 3. FIELD MAPPING: UKG TO GEODIS TALENTSOFT

### 3.1 Vacancy Request Fields

| UKG Field | GEODIS Talentsoft Field | WordPlus Tag |
|-----------|------------------------|--------------|
| Requisition Number | Reference | [P-ReferenceEditable] |
| Request Date | Request date | [P-PreliminaryJobRequest_Date1] |
| Is Budgeted | Budgeted vacancy request | [P-Planned] |
| Reason for Opening | Recruitment reason | [P-RecruitingReason] |
| **Incumbent Name** | **Name of person being replaced** | **[P-RequestMotive_ShortText1]** |
| Target Start Date | Preferred entry date | [P-RequestMotive_Date1] |
| Headcount | Number of positions to be opened | [P-NumberOfVacancies] |
| Job Title | Job title | [P-JobTitle] |
| Professional Category | Status | [P-ProfessionalCategory] |
| Contract Type | Type of contract | [P-Contract] |
| Contract Duration | Contract duration | [P-ContractLength] |
| Full-time/Part-time | Full-time/Part-time | [P-JobTime] |
| **FTE %** | **FTE %** | **[P-PreliminaryJobDescription_ShortText1]** |
| Min Salary | Minimum gross annual base salary | [P-PreliminaryJobDescription_ShortText2] |
| Max Salary | Maximum gross annual base salary | [P-PreliminaryJobDescription_ShortText3] |
| Currency | Currency | [P-PreliminaryJobDescription_CustomCodeTableValue1] |
| Salary Range | Salary range | [P-SalaryRange] |
| Job Description | Job description | [P-PreliminaryJobDescription1] |
| Required Profile | Applicant's profile | [P-PreliminaryJobDescription2] |
| Job Family | Position | [P-Profile] |
| Education Level | Minimum level of education required | [P-EducationLevel] |
| Experience Level | Years of experience in similar position | [P-ExperienceLevel] |
| Languages | Languages | [P-RequiredLanguageCollection] |
| Location | Employee Location | [P-Location_GeographicalAreaCollection] |
| Location Text | Location | [P-JobLocation] |
| Company/Entity | Entity | [P-Entity] |
| Org Level | Pole / Line Of Business | [P-CompanyInformation_CustomCodeTableValue1/2] |
| Department | Requesting department | [P-Service] |
| Hiring Manager Last Name | Manager last name | [P-OperationalManagerName] |
| Hiring Manager First Name | Manager first name | [P-OperationalManagerFirstName] |
| Hiring Manager Email | Email | [P-OperationalManagerEmail] |
| Hiring Manager Phone | Manager phone number | [P-OperationalManagerPhoneNumber] |

---

### 3.2 Vacancy (Offer) Fields

| UKG Field | GEODIS Talentsoft Field | WordPlus Tag |
|-----------|------------------------|--------------|
| Requisition Number | Reference | [O-ReferenceEditable] |
| Company/Entity | Legal entity | [O-Entity] |
| Confidential | Confidential vacancy | [O-Private] |
| Category | Vacancy category | [O-OfferCategory] |
| Evergreen | Regular vacancy | [O-RegularOffer] |
| Contract Type | Type of assignment | [O-Contract] |
| Contract Duration | Contract duration | [O-ContractLength] |
| Job Family | Function | [O-PrimaryProfile] |
| Secondary Profile | Secondary function | [O-ProfileCollection] |
| Job Title | Job title | [O-JobTitle] |
| Professional Category | Employment status | [O-ProfessionalCategory] |
| Hours/Constraints | Position requirements and constraints | [O-JobDescription_LongText1] |
| Full-time/Part-time | Full-time/Part-time | [O-JobTime] |
| Salary Range | Salary range | [O-SalaryRange] |
| Job Description | Job description | [O-Description1] |
| Required Profile | Applicant's profile | [O-Description2] |
| **Working Time %** | **Working time (%)** | **[O-JobDescription_ShortText2]** |
| Min Salary | Minimum gross annual base salary | [O-JobDescription_ShortText1] |
| Max Salary | Maximum gross annual base salary | [O-JobDescription_ShortText3] |
| Currency | Currency | [O-JobDescription_CustomCodeTableValue2] |
| Location | Position place | [O-Location_GeographicalAreaCollection] |
| Location Text | Location | [O-JobLocation] |
| Education Level | Minimum level of education required | [O-EducationLevel] |
| Experience Level | Years of experience in similar position | [O-ExperienceLevel] |
| Driving License | Driving license | [O-ApplicantCriteria_LongText1] |
| **Certifications** | **Certifications** | **[O-ApplicantCriteria_ShortText1]** |
| Languages | Languages | [O-RequiredLanguageCollection] |
| Skills | Competencies | [O-Offer_SkillCollection] |
| Hiring Manager Last Name | Manager last name | [O-OperationalManagerName] |
| Hiring Manager First Name | Manager first name | [O-OperationalManagerFirstName] |
| Hiring Manager Email | Email | [O-OperationalManagerEmail] |
| Hiring Manager Phone | Manager phone number | [O-OperationalManagerPhoneNumber] |
| Start Date | Position start date | [O-BeginningDate] |
| Reason for Opening | Recruitment reason | [O-RecruitingReason] |
| Headcount | Number of positions to be opened | [O-NumberOfVacancies] |
| Recruiter | Handled by / Primary recruiter | [O-UsersInChargeOf] / [O-MainSupervisor] |
| Publication Start | Default publication start date | [O-DefaultPublicationBeginDate] |
| Publication End | Default publication end date | [O-DefaultPublicationEndDate] |

---

### 3.3 Candidate/Applicant Fields

| UKG Field | GEODIS Talentsoft Field | WordPlus Tag |
|-----------|------------------------|--------------|
| Title | Title | [A-Civility] / [A-Title] |
| Sex | Sex | [A-Sex] |
| Last Name | Last name | [A-Name] |
| First Name | First name | [A-FirstName] |
| **Middle Name** | **Middle name** | **[A-MiddleName]** |
| Birthdate | Birthdate | [A-BirthDate] |
| Nationality | Nationality | [A-ApplicantNationalityCollection] |
| Address | Address | [A-Address] |
| Postal Code | Postcode | [A-PostalCode] |
| City | City | [A-City] |
| Country | Country of residence | [A-ResidenceCountry] |
| Primary Phone | Phone number | [A-PhoneNumber1] |
| Secondary Phone | Other phone number | [A-PhoneNumber2] |
| Email | E-mail address | [A-Email] |
| Work Email | Work email | [A-ProfessionalEmail] |
| Consent | Consent | [A-Consent] |
| Internal/External | Associated organisation / Employee number | [A-Entity] / [A-TS_EmployeeNumber] |
| Education Level | Level of education | [A-EducationLevel] |
| Diploma | Qualification | [A-TreeNode_Diploma] |
| Field of Study | Field | [A-Specialisation] |
| Graduation Year | Year of graduation | [A-YearObtained] |
| School | School | [A-College] |
| School City | School city | [A-CollegeCity] |
| **Certifications** | **Certifications** | **[A-Diploma_LongText2]** |
| **Driving License** | **Driving license (category)** | **[A-Diploma_ShortText1]** |
| **License Number** | **If yes, Number** | **[A-Diploma_ShortText2]** |
| Computer Skills | Computer skills | [A-Diploma_LongText1] |
| Languages | Candidate languages | [A-StudiedLanguageCollection] |
| Experience Level | Years of experience in similar position | [A-ExperienceLevel] |
| Company | Company | [A-Company] |
| Function/Title | Function | [A-Function] |
| Contract Type | Contract type (Experience) | [A-Contract] |
| Duration | Duration | [A-Length] |
| Sought Position | Sought position | [A-PrimaryProfile] |
| Job Time Preference | Contractual hours | [A-JobTime] |
| Availability Date | Availability | [A-DateOfAvailability] |
| Notice Period | In case of notice period | [A-NoticeDuration] |
| Salary Expectations | Salary expectations | [A-SalaryPretensions] |
| Mobility | Geographical mobility | [A-Mobility] |
| Skills | Competencies | [A-SkillCollection] |
| Screening Answers | Answers to questions | [A-AnswerCollection] |
| Race | Race | [A-Race] |
| Ethnicity | Ethnic group | [A-Ethnicity] |
| Veteran Status | Veteran status | [A-VeteranStatus] |
| Disability Status | Incapacity status | [A-IncapacityStatus] |
| French Disabled Worker | French disabled worker status (RQTH) | [A-FrenchDisabledWorkerStatus] |
| Referrer Name | Recommended by | [A-RecommendedBy1] |
| Referrer Email | Email (Referrer) | [A-RecommendedBy2] |
| Comments | Comments | [A-Comment] |

---

## 4. REVISED GAP SUMMARY

### 4.1 Fields FULLY COVERED in GEODIS Talentsoft

| Category | UKG Fields | GEODIS Coverage |
|----------|------------|-----------------|
| Vacancy Basic Info | 15+ | FULL |
| Vacancy Location | 5+ | FULL |
| Compensation | 8+ | FULL |
| Job Description | 5+ | FULL |
| Requirements | 6+ | FULL |
| Hiring Manager | 4 (Name, Email, Phone, Language) | FULL |
| Publication | 4+ | FULL |
| Candidate Personal | 15+ | FULL |
| Candidate Education | 10+ | FULL |
| Candidate Experience | 6+ | FULL |
| Candidate Preferences | 10+ | FULL |
| EEO/Affirmative Action | 6 | FULL |
| Referral | 2 | FULL |
| **Incumbent Name** | 1 | **FULL** |
| **Is Budgeted** | 1 | **FULL** |
| **FTE %** | 1 | **FULL** |
| **Licenses/Certs** | 3 | **FULL** |

### 4.2 Fields STILL MISSING (from 594-field analysis)

#### NOT AVAILABLE - 13 fields (Data Loss Risk)
| UKG Field | Count | Impact | Workaround |
|-----------|-------|--------|------------|
| Incumbent Name (concatenated) | 1 | Low | Use First+Last fields |
| Last Day Worked | 1 | Medium | Add custom date field |
| Manager/Owner Title (Mr., Mrs., Dr.) | 4 | Low | Accept loss |
| Manager/Owner Suffix (Jr., Sr., III) | 4 | Low | Accept loss |
| Months To Renewal (License) | 3 | Medium | Track externally |

#### MUST CALCULATE - 13 fields (BI Development Required)
| UKG Field | Count | Calculation Method |
|-----------|-------|-------------------|
| Filled FTE | 1 | COUNT(applications WHERE status='Hired') |
| Remaining FTE | 1 | Budgeted FTE - Filled FTE |
| Remaining Headcount | 1 | NumberOfVacancies - Hired count |
| Days Between Accept and Offer Dates | 2 | EventDate(Accept) - EventDate(Offer) |
| Days Between Accept and Start Dates | 2 | StartDate - EventDate(Accept) |
| Days Between Hire and Publish Dates | 2 | HireDate - FirstPublicationDate |
| Days Between Offer and Start Dates | 2 | StartDate - EventDate(Offer) |
| Days Between Start and Publish Dates | 2 | StartDate - FirstPublicationDate |

### 4.3 Revised Statistics (Aligned with Excel Mapping)

| Gap Status | Field Count | % of Total |
|------------|-------------|------------|
| MAPPED | 454 | 76.4% |
| MAPPED (Reference) | 84 | 14.1% |
| SYSTEM | 22 | 3.7% |
| **MUST CALCULATE** | **13** | **2.2%** |
| **NOT AVAILABLE** | **13** | **2.2%** |
| MAPPED (Custom) | 8 | 1.3% |
| **TOTAL** | **594** | **100%** |

**Coverage Rate: 97.8%** (only 13 fields with no equivalent)

---

## 5. RECOMMENDATIONS

### 5.1 Before Migration - SIMPLIFIED

| Action | Priority | Effort |
|--------|----------|--------|
| ~~Configure custom fields for Licenses~~ | ~~P1~~ | DONE |
| ~~Configure custom fields for Incumbent~~ | ~~P1~~ | DONE |
| ~~Configure custom fields for FTE %~~ | ~~P1~~ | DONE |
| ~~Configure custom fields for Budgeted flag~~ | ~~P1~~ | DONE |
| Add "Incumbent Last Day" date field | P2 | Low |
| Build Days-to-Hire calculations in BI | P1 | Medium |
| Build Filled/Remaining FTE calculations | P1 | Medium |

### 5.2 Data Loss to Accept

| Field | Reason |
|-------|--------|
| Manager Title (Mr., Mrs., Dr.) | Not business critical |
| Manager Middle Name | Not business critical |
| Manager Suffix (Jr., Sr.) | Not business critical |
| Incumbent Last Day (if not added) | Can be tracked separately |

---

## 6. CONCLUSION

The GEODIS Talentsoft configuration is **significantly better aligned** with UKG than the standard Talentsoft model. Key gaps that were identified earlier are already addressed:

| Gap | Status |
|-----|--------|
| Incumbent tracking | **ADDRESSED** via `Name of person being replaced` |
| Budget flag | **ADDRESSED** via `Budgeted vacancy request` |
| FTE percentage | **ADDRESSED** via `FTE %` and `Working time (%)` |
| Licenses/Certifications | **ADDRESSED** via multiple fields |
| Candidate Middle Name | **AVAILABLE** (may need activation) |

**Remaining work:** Build BI calculations for:
1. Days-to-Hire metrics (5 unique calculations, 10 field instances)
2. Filled/Remaining FTE tracking (3 calculations)

---

## 7. CROSS-REFERENCE

This document is aligned with **`UKG_Talentsoft_Holistic_Mapping_CORRECTED.xlsx`** which contains:
- **Complete_Mapping** sheet: All 594 UKG fields with **CORRECTED** Talentsoft mappings
- **Gap_Summary** sheet: Statistics matching section 4.3 above
- **Action_Required** sheet: 26 fields needing attention
- **Fully_Mapped** sheet: 546 fields with direct/custom mappings
- **Entity_Mapping** sheet: UKG to Talentsoft entity crosswalk

### Additional Files:
- **`UKG_Talentsoft_Mapping_CORRECTIONS.xlsx`**: Detailed list of 34 tag corrections
- **`UKG_Talentsoft_Holistic_Mapping_BACKUP.xlsx`**: Original file before corrections

---

*Document updated: 2025-11-23 | Version 2.2 | Includes 34 WordPlus tag corrections*
