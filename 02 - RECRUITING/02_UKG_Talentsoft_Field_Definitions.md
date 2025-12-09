# UKG to Talentsoft Field Definitions Dictionary

**Document Version:** 1.0  
**Date:** 2025-11-22  
**Total Fields:** 594  
**Purpose:** Complete field-by-field mapping with definitions for UKG Talent Acquisition to Talentsoft migration

---

## Quick Reference

| Gap Status | Count | Description |
|------------|-------|-------------|
| MAPPED | 454 | Direct field mapping available |
| MAPPED (Reference) | 84 | Reference/lookup data mapping |
| SYSTEM | 22 | System-generated field |
| MUST CALCULATE | 13 | Requires BI calculation |
| NOT AVAILABLE | 13 | No equivalent - data loss risk |
| MAPPED (Custom) | 8 | Uses GEODIS custom field |

---

## Legend

- **[P-...]** = PreliminaryJobRequest (Vacancy Request) field
- **[O-...]** = Offer (Vacancy) field
- **[A-...]** = Applicant (Candidate) field
- **CALCULATE** = Build BI calculated measure from events/applications

---

## IMPORTANT: Tag Prefix Corrections (2025-11-23)

**34 mapping corrections applied** based on PDF documentation review. Key rules:

| Object Type | Correct Prefix | Example Fields |
|-------------|----------------|----------------|
| **Manager/Supervisor/Recruiter** | P- or O- | `[P-OperationalManagerEmail]`, `[O-MainSupervisorEmail]` |
| **Applicant/Candidate** | A- | `[A-Email]`, `[A-Name]` |
| **Job Request** | P- | `[P-JobTitle]`, `[P-Location]` |
| **Vacancy/Offer** | O- | `[O-JobTitle]`, `[O-JobLocation]` |

### Common Errors Fixed:
- **Manager Email**: `[A-Address]` → `[P-OperationalManagerEmail] / [O-OperationalManagerEmail]`
- **Candidate Email**: `[A-Address]` → `[A-Email]` (semantic error: Address ≠ Email)
- **Opportunity Title**: `[A-Civility]` → `[P-JobTitle] / [O-JobTitle]`
- **Opportunity City**: `[A-City]` → `[O-JobLocation]`

See `UKG_Talentsoft_Mapping_CORRECTIONS.xlsx` for full list.

---

## Application

**Talentsoft Equivalent:** Application (JobApplication)  
**Field Count:** 106

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Application Created By  | Contains the concatenated name, including their title, if any, of the individual applied on behalf o | CreationDate |  | MAPPED |
| Application Created By  | Contains the name of the opportunity application created by (concatenated) that had the change made  | CreationDate |  | MAPPED |
| Email Address  | Contains the email address of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-Address] | MAPPED |
| Email Address  | Contains the email address of the individual who deleted the application. | JobApplicationEvent | [A-Address] | MAPPED |
| First Name  | Contains the first name of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-FirstName] | MAPPED |
| First Name  | Contains the first name of the individual who deleted the application. | JobApplicationEvent | [A-FirstName] | MAPPED |
| Description  | Contains the optional additional information describing the candidates school experience. | educations[] | [A-...] | MAPPED |
| From Month  | Contains the month the candidate started at the school. | educations[] | [A-...] | MAPPED |
| From Year  | Contains the year the candidate started at the school. | educations[].yearOfGraduation | [A-...] | MAPPED |
| Level of Education/Degree  | Contains the level of education the candidate achieved at the school. | educations[].diploma | [A-...] | MAPPED (Reference) |
| Major  | Contains the major, if any, the candidate had at the school. | educations[] | [A-...] | MAPPED |
| Minor  | Contains the minor, if any, the candidate had at the school. | educations[] | [A-...] | MAPPED |
| School Name  | Contains the name of the school the candidate attended. | educations[].school | [A-College] | MAPPED |
| To Month  | Contains the month the candidate completed their studies at the school. | educations[] | [A-...] | MAPPED |
| To Year  | Contains the year the candidate completed their studies at the school. | educations[].yearOfGraduation | [A-...] | MAPPED |
| Years In School  | Contains the calculated number of years (1 decimal position) the candidate was in school. | educations[].school | [A-College] | MAPPED |
| Date Achieved  | Contains the date candidate achieved the license/certification. | JobApplicationEvent | [A-...] | MAPPED |
| License Number  | Contains the number of license, if any. | CustomField | [A-Diploma_ShortText2] | MAPPED (Custom) |
| License/Certification Name  | Contains the license/certification earned by the candidate. | CustomField | [A-Diploma_LongText2] | MAPPED (Custom) |
| Months To Renewal  | Contains the calculated number of months before the candidate's license/certification needs to be re | JobApplicationEvent | [A-...] | NOT AVAILABLE |
| Renewal Date  | Contains the date the license/certification must be renewed. | JobApplicationEvent | [A-...] | MAPPED |
| Company/Organization  | Contains the name of the organization where the candidate previously worked. | Company | [P-Entity] / [O-Entity] | MAPPED |
| Description  | Contains the optional additional information describing the candidates work experience. | experiences[] | [A-...] | MAPPED |
| From Month  | Contains the starting month for the work experience. | experiences[] | [A-...] | MAPPED |
| From Year  | Contains the starting year for the work experience. | experiences[] | [A-...] | MAPPED |
| Job Title  | Contains the title of the job/position the candidate previously held. | Function | [P-JobTitle] / [O-JobTitle] | MAPPED |
| Location Name  | Contains the name of the location where the candidate previously worked. | experiences[] | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| To Month  | Contains the ending month for the work experience.  If the candidate is still employed, this field w | experiences[] | [A-...] | MAPPED |
| To Year  | Contains the ending year for the work experience.  If the candidate is still employed, this field wi | experiences[] | [A-...] | MAPPED |
| Years Employed  | Contains the calculated number of years (1 decimal position) the candidate was employed for. | experiences[] | [A-...] | MAPPED |
| Application Deleted By  | Contains the concatenated name, including their title, if any, of the individual who deleted the app | - |  | SYSTEM |
| Application Deleted By  | Contains the name of the opportunity application deleted by (concatenated) that had the change made  | - |  | SYSTEM |
| Last Name  | Contains the last name of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-Name] | MAPPED |
| Last Name  | Contains the last name of the individual who deleted the application. | JobApplicationEvent | [A-Name] | MAPPED |
| Middle Name  | Contains the middle name of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Middle Name  | Contains the middle name of the individual who deleted the application. | JobApplicationEvent | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Suffix  | Contains the name suffix (e.g. Jr.) of the individual who applied on behalf of the candidate. | JobApplicationEvent |  | MAPPED |
| From Step | Contains the applicant's original step. | JobApplicationStatus |  | MAPPED (Reference) |
| Important | Indicates if the step movement/note was marked as important. | JobApplicationStatus |  | MAPPED (Reference) |
| Note | Contains the text, if any, of the note when the applicant's step was changed. | Comment |  | MAPPED |
| Reason | Contains the reason for the step change. | JobApplicationStatus |  | MAPPED (Reference) |
| Step Change Date/Time | Contains the date/time the applicant's step was changed. | JobApplicationStatus |  | MAPPED (Reference) |
| To Step | Contains the applicant's current step. | JobApplicationStatus |  | MAPPED (Reference) |
| Referral Email | Contains the email address of the employee who referred the candidate. | JobApplicationEvent | [A-RecommendedBy2] | MAPPED |
| Referral Name | Contains the name of the employee who referred the candidate. | JobApplicationEvent |  | MAPPED |
| Referral Phone | Contains the phone number of the employee who referred the candidate. | JobApplicationEvent | [A-RecommendedBy3] | MAPPED |
| Days Between Accept and Offer Dates | Time from offer sent to candidate acceptance. Calculate from event dates. | Calculated | CALCULATE: EventDate(Accept) - EventDate(Offer) | MUST CALCULATE |
| Days Between Accept and Start Dates | Time from acceptance to actual start date. Calculate from event dates. | Calculated | CALCULATE: EventDate(Accept) - StartDate | MUST CALCULATE |
| Days Between Hire and Publish Dates | Total time-to-hire from job posting. Calculate from event dates. | Calculated | CALCULATE: HireDate - FirstPublicationDate | MUST CALCULATE |
| Days Between Offer and Start Dates | Notice period / onboarding time. Calculate from event dates. | Calculated | CALCULATE: EventDate(Offer) - StartDate | MUST CALCULATE |
| Days Between Start and Publish Dates | Total time-to-fill metric. Calculate from event dates. | Calculated | CALCULATE: StartDate - FirstPublicationDate | MUST CALCULATE |
| Accept Date | Contains the date the applicant accepted the hire offer. | EventDate |  | MAPPED |
| Actual Start Date | Contains the date the candidate is scheduled to being employment. | EventDate | [O-BeginningDate] | MAPPED |
| Employee Type | Indicates if the applicant is identified as a full-time or part time employee. | JobApplicationEvent |  | MAPPED |
| FTE | Contains the number of full time equivalents the applicant will account for. | JobApplicationEvent |  | MAPPED |
| Hire Date | Contains the date the applicant was hired. | EventDate |  | MAPPED |
| Offer Date | Contains the date an offer was made to the applicant. | EventDate |  | MAPPED |
| Salary/Hourly Rate | Contains the rate the application will be paid.  The value is either an hourly rate or an annual sal | JobApplicationEvent |  | MAPPED |
| Salary/Hourly Rate Currency | Contains the associated currency for the annual salary or hourly rate. | JobApplicationEvent | [P-PreliminaryJobDescription_CustomCodeTableValue1] / [O-JobDescription_CustomCodeTableValue2] | MAPPED |
| Salary Type | Indicates if the applicant is identified as an hourly or salaried employee. | JobApplicationEvent |  | MAPPED |
| Tax Location Code | Contains the code for the location where the job exists. | JobApplicationEvent | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Tax Location | Contains the description for the location where the job exists. | JobApplicationEvent | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Tax Location Name | Contains the name for the location where the job exists. | JobApplicationEvent | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Work Hours | Contains the number of hours the applicant is expected to work. | JobApplicationEvent |  | MAPPED |
| Application Created By  | Contains the name of the recruiter who applied for the candidate. If the candidate applied, Self is  | CreationDate |  | MAPPED |
| Application Created By  | Contains the name of the opportunity application created by (concatenated) that had the change made  | CreationDate |  | MAPPED |
| Application Deleted | Indicates if the application has been deleted from the system. | - |  | SYSTEM |
| Application Deleted By  | Contains the name of the individual who deleted the application. | - |  | SYSTEM |
| Application Deleted By  | Contains the name of the opportunity application created by (concatenated) that had the change made  | - |  | SYSTEM |
| Application Deleted Date | Contains the date the application was deleted from the system. | - |  | SYSTEM |
| Application Internal/External | Indicates if the candidate is an internal (e.g. employee) or external candidate when they applied to | Type |  | MAPPED (Reference) |
| Candidate  | Contains the concatenated name of candidate. | ApplicantCode |  | MAPPED |
| Candidate  | Contains the name of the opportunity candidate (concatenated) that had the change made to, Format is | ApplicantCode |  | MAPPED |
| Candidate  | Contains the candidate's concatenated name, including their title, if any. | ApplicantCode |  | MAPPED |
| Candidate Active/Inactive | Indicates if the candidate was active or inactive when they applied to the opportunity.  All externa | ApplicantCode |  | MAPPED |
| Candidate Email Address | Contains the candidate's email address. | ApplicantCode | [A-Address] | MAPPED |
| Candidate Primary Phone | Contains the candidate's primary phone number. | ApplicantCode | [A-PhoneNumber1] | MAPPED |
| Candidate Secondary Phone | Contains the candidate's secondary phone number. | ApplicantCode | [A-PhoneNumber2] | MAPPED |
| Date Applied | Contains the date the candidate applied to the opportunity. | Date |  | MAPPED |
| Disability | Indicates if the candidate has self-identified as having a disability. | JobApplicationEvent | [A-IncapacityStatus] | MAPPED |
| Electronic Signature | Contains the name entered for simulating an electronic signature.  | JobApplicationEvent |  | MAPPED |
| Electronic Signature Date | Contains the date entered for the electronic signature. | JobApplicationEvent |  | MAPPED |
| Ethnic Origin | Contains the self-identified ethnicity for the candidate. | JobApplicationEvent |  | MAPPED |
| Gender | Contains the self-identified gender for the candidate. | JobApplicationEvent | [A-Sex] | MAPPED |
| Internal/External | Indicates if the candidate is CURRENTLY an internal (e.g. employee) or external candidate. Note: Thi | Type |  | MAPPED (Reference) |
| Recruiting Hire Date | Contains the date Recruiting started the hiring process. | JobApplicationEvent |  | MAPPED |
| Source | Contains the name of source in which the candidate became aware of the opportunity. | PublicationSupport | [A-Source] | MAPPED (Reference) |
| Start Date | Contains the date the candidate is able to start. | JobApplicationEvent | [O-BeginningDate] | MAPPED |
| Status Code | Initial, Accepted or Rejected | JobApplicationEvent |  | MAPPED |
| Status | Initial, Accepted or Rejected | JobApplicationEvent |  | MAPPED |
| Step | Contains the name of the step in the recruiting process the candidate is in. | JobApplicationEvent |  | MAPPED |
| Step Date | Contains the date the candidate entered the step. | JobApplicationEvent |  | MAPPED |
| Veteran | Indicates if the candidate has self-identified as being a veteran. | JobApplicationEvent |  | MAPPED |
| Application Created By  | Contains the unique identifier for an application created  in the Dimension table.  | CreationDate |  | MAPPED |
| Application Deleted By  | Contains the unique identifier for an application deleted in the Dimension table.  | OfferStatus |  | SYSTEM |
| Application Key  | Contains the unique identifier for an application in the Dimension table. Can be use to join to Fact | CustomField |  | MAPPED |
| Application Key  | Contains the unique identifier for an application in the Fact table. Can be use to join to Recruiter | CustomField |  | MAPPED |
| Suffix  | Contains the name suffix (e.g. Jr.) of the individual who deleted the application. | JobApplicationEvent |  | MAPPED |
| Preferred Name  | Contains the preferred name of the individual who applied on behalf of the candidate. | JobApplicationEvent |  | MAPPED |
| Preferred Name  | Contains the preferred name of the individual who deleted the application. | JobApplicationEvent |  | MAPPED |
| Primary Phone  | Contains the primary phone number of the individual who deleted the application. | JobApplicationEvent | [A-PhoneNumber1] | MAPPED |
| Secondary Phone  | Contains the secondary phone number of the individual who deleted the application. | JobApplicationEvent | [A-PhoneNumber2] | MAPPED |
| Title  | Contains the title of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-Civility] / [A-Title] | MAPPED |
| Title  | Contains the title of the individual who deleted the application. | JobApplicationEvent | [A-Civility] / [A-Title] | MAPPED |
| Primary Phone  | Contains the unformatted primary phone number of the individual who applied on behalf of the candida | JobApplicationEvent | [A-PhoneNumber1] | MAPPED |
| Secondary Phone  | Contains the unformatted secondary phone number of the individual who applied on behalf of the candi | JobApplicationEvent | [A-PhoneNumber2] | MAPPED |

---

## Candidate

**Talentsoft Equivalent:** Applicant (Candidate)  
**Field Count:** 152

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| First Name  | Contains the first name of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-FirstName] | MAPPED |
| First Name  | Contains the first name of the individual who deleted the application. | JobApplicationEvent | [A-FirstName] | MAPPED |
| Preferred Name  | Contains the first name of the individual who deleted the application. | JobApplicationEvent | [A-...] | MAPPED |
| Last Name  | Contains the last name of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-Name] | MAPPED |
| Last Name  | Contains the last name of the individual who deleted the application. | JobApplicationEvent | [A-Name] | MAPPED |
| Middle Name  | Contains the middle name of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Middle Name  | Contains the middle name of the individual who deleted the application. | JobApplicationEvent | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| First Name  | Contains the first name of the individual who created the candidate's profile. | FirstName | [A-FirstName] | MAPPED |
| Preferred Name  | Contains the preferred name of the individual who created the candidate's profile. | To be mapped | [A-...] | MAPPED |
| Last Name  | Contains the last name of the individual who created the candidate's profile. | Name | [A-Name] | MAPPED |
| Middle Name  | Contains the middle name of the individual who created the candidate's profile. | MiddleName | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Primary Phone  | Contains the primary phone number of the individual who created the candidate's profile. | PhoneNumber1 | [A-PhoneNumber1] | MAPPED |
| Profile Created By  | Contains the concatenated name, including their title, if any, of the individual who created the can | To be mapped | [A-...] | MAPPED |
| Profile Created By  | Contains the name of the opportunity created by (concatenated) that had the change made to, Format i | To be mapped | [A-...] | MAPPED |
| Secondary Phone  | Contains the secondary phone number of the individual who created the candidate's profile. | PhoneNumber2 | [A-PhoneNumber2] | MAPPED |
| Suffix  | Contains the name suffix (e.g. Jr.) of the individual who created the candidate's profile. | To be mapped | [A-...] | MAPPED |
| Title  | Contains the title of the individual who created the candidate's profile. | To be mapped | [A-Civility] / [A-Title] | MAPPED |
| Application Created By  | Contains the concatenated name, including their title, if any, of the individual applied on behalf o | CreationDate | [A-...] | MAPPED |
| Application Created By  | Contains the name of the opportunity application created by (concatenated) that had the change made  | CreationDate | [A-...] | MAPPED |
| Suffix  | Contains the name suffix (e.g. Jr.) of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-...] | MAPPED |
| Suffix  | Contains the name suffix (e.g. Jr.) of the individual who deleted the application. | JobApplicationEvent | [A-...] | MAPPED |
| Preferred Name  | Contains the preferred name of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-...] | MAPPED |
| Primary Phone  | Contains the primary phone number of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-PhoneNumber1] | MAPPED |
| Primary Phone  | Contains the primary phone number of the individual who deleted the application. | JobApplicationEvent | [A-PhoneNumber1] | MAPPED |
| Application Deleted By  | Contains the concatenated name, including their title, if any, of the individual who deleted the app | - | [A-...] | SYSTEM |
| Application Deleted By  | Contains the name of the opportunity deleted by (concatenated) that had the change made to, Format i | - | [A-...] | SYSTEM |
| Secondary Phone  | Contains the secondary phone number of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-PhoneNumber2] | MAPPED |
| Secondary Phone  | Contains the secondary phone number of the individual who deleted the application. | JobApplicationEvent | [A-PhoneNumber2] | MAPPED |
| Title  | Contains the title of the individual who applied on behalf of the candidate. | JobApplicationEvent | [A-Civility] / [A-Title] | MAPPED |
| Title  | Contains the title of the individual who deleted the application. | JobApplicationEvent | [A-Civility] / [A-Title] | MAPPED |
| From Step | Contains the applicant's original step. | JobApplicationStatus | [A-...] | MAPPED (Reference) |
| Important | Indicates if the step movement/note was marked as important. | JobApplicationStatus | [A-...] | MAPPED (Reference) |
| Note | Contains the text, if any, of the note when the applicant's step was changed. | Comment | [A-...] | MAPPED |
| Reason | Contains the reason for the step change. | JobApplicationStatus | [A-...] | MAPPED (Reference) |
| Step Change Date/Time | Contains the date/time the applicant's step was changed. | JobApplicationStatus | [A-...] | MAPPED (Reference) |
| To Step | Contains the applicant's current step. | JobApplicationStatus | [A-...] | MAPPED (Reference) |
| Days Between Accept and Offer Dates | Time from offer sent to candidate acceptance. Calculate from event dates. | Calculated | CALCULATE: EventDate(Accept) - EventDate(Offer) | MUST CALCULATE |
| Days Between Accept and Start Dates | Time from acceptance to actual start date. Calculate from event dates. | Calculated | CALCULATE: EventDate(Accept) - StartDate | MUST CALCULATE |
| Days Between Hire and Publish Dates | Total time-to-hire from job posting. Calculate from event dates. | Calculated | CALCULATE: HireDate - FirstPublicationDate | MUST CALCULATE |
| Days Between Offer and Start Dates | Notice period / onboarding time. Calculate from event dates. | Calculated | CALCULATE: EventDate(Offer) - StartDate | MUST CALCULATE |
| Days Between Start and Publish Dates | Total time-to-fill metric. Calculate from event dates. | Calculated | CALCULATE: StartDate - FirstPublicationDate | MUST CALCULATE |
| Hiring Manager  | Contains the concatenated name including title, if any, for the Hiring Manager associated to the app | OperationalManager* | [A-...] | MAPPED |
| Hiring Manager  | Contains the name of the opportunity hiring manager (concatenated) that had the change made to, Form | OperationalManager* | [A-...] | MAPPED |
| Prefix  | Contains the salutation for the hiring manager. | JobApplicationEvent | [A-...] | MAPPED |
| First Name  | Contains the first name of the hiring manager. | JobApplicationEvent | [A-FirstName] | MAPPED |
| Preferred Name  | Contains the preferred name of the hiring manager. | JobApplicationEvent | [A-...] | MAPPED |
| Middle Name  | Contains the middle name of the hiring manager. | JobApplicationEvent | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Last Name  | Contains the last name of the hiring manager. | JobApplicationEvent | [A-Name] | MAPPED |
| Suffix  | Contains the suffix (Jr, Sr, etc) of the hiring manager. | JobApplicationEvent | [A-...] | MAPPED |
| Onboarding Owner  | Contains the concatenated name including title, if any, for the Onboarding Owner associated to the a | JobApplicationEvent | [A-...] | MAPPED |
| Onboarding Owner  | Contains the name of the opportunity onboarding owner (concatenated) that had the change made to, Fo | JobApplicationEvent | [A-...] | MAPPED |
| Prefix  | Contains the salutation for the onboarding owner. | JobApplicationEvent | [A-...] | MAPPED |
| First Name  | Contains the first name of the onboarding owner. | JobApplicationEvent | [A-FirstName] | MAPPED |
| Preferred Name  | Contains the preferred name of the onboarding owner. | JobApplicationEvent | [A-...] | MAPPED |
| Middle Name  | Contains the middle name of the onboarding owner. | JobApplicationEvent | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Last Name  | Contains the last name of the onboarding owner. | JobApplicationEvent | [A-Name] | MAPPED |
| Suffix  | Contains the suffix (Jr, Sr, etc) of the onboarding owner. | JobApplicationEvent | [A-...] | MAPPED |
| Accept Date | Contains the date the applicant accepted the hire offer. | EventDate | [A-...] | MAPPED |
| Actual Start Date | Contains the date the candidate is scheduled to being employment. | EventDate | [O-BeginningDate] | MAPPED |
| Employee Type | Indicates if the applicant is identified as a full-time or part time employee. | JobApplicationEvent | [A-...] | MAPPED |
| FTE | Contains the number of full time equivalents the applicant will account for. | JobApplicationEvent | [A-...] | MAPPED |
| Hire Date | Contains the date the applicant was hired. | EventDate | [A-...] | MAPPED |
| Hiring Manager  | Contains the concatenated name of the hiring manager using the format: First MI Last  Suffix. | OperationalManager* | [A-...] | MAPPED |
| Hiring Manager  | Contains the name of the opportunity hiring manager (concatenated) that had the change made to, Form | OperationalManager* | [A-...] | MAPPED |
| Hiring Manager  | Contains the concatenated name of the hiring manager using the format:  Last, Suffix First MI. | OperationalManager* | [A-...] | MAPPED |
| Hiring Manager  | Contains the name of the opportunity hiring manager (concatenated) that had the change made to, Form | OperationalManager* | [A-...] | MAPPED |
| Hiring Manager Primary Phone  | Contains the primary phone number for the Hiring Manager associated to the application's hire detail | OperationalManager* | [A-PhoneNumber1] | MAPPED |
| Hiring Manager Secondary Phone  | Contains the secondary phone number for the Hiring Manager associated to the application's hire deta | OperationalManager* | [A-PhoneNumber2] | MAPPED |
| Offer Date | Contains the date an offer was made to the applicant. | EventDate | [A-...] | MAPPED |
| Onboarding Owner  | Contains the concatenated name of the onboarding owner - First MI Last  Suffix. | JobApplicationEvent | [A-...] | MAPPED |
| Onboarding Owner  | Contains the name of the opportunity onboarding owner (concatenated) that had the change made to, Fo | JobApplicationEvent | [A-...] | MAPPED |
| Onboarding Owner  | Contains the concatenated name of the onboarding owner - Last, Suffix First MI. | JobApplicationEvent | [A-...] | MAPPED |
| Onboarding Owner  | Contains the name of the opportunity onboarding owner (concatenated) that had the change made to, Fo | JobApplicationEvent | [A-...] | MAPPED |
| Onboarding Owner Primary Phone  | Contains the primary phone number for the Onboarding Owner associated to the application's hire deta | JobApplicationEvent | [A-PhoneNumber1] | MAPPED |
| Onboarding Owner Secondary Phone  | Contains the secondary phone number for the Onboarding Owner associated to the application's hire de | JobApplicationEvent | [A-PhoneNumber2] | MAPPED |
| Salary/Hourly Rate | Contains the rate the application will be paid.  The value is either an hourly rate or an annual sal | JobApplicationEvent | [A-...] | MAPPED |
| Salary/Hourly Rate Currency | Contains the associated currency for the annual salary or hourly rate. | JobApplicationEvent | [P-PreliminaryJobDescription_CustomCodeTableValue1] / [O-JobDescription_CustomCodeTableValue2] | MAPPED |
| Salary Type | Indicates if the applicant is identified as an hourly or salaried employee. | JobApplicationEvent | [A-...] | MAPPED |
| Tax Location Code | Contains the code for the location where the job exists. | JobApplicationEvent | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Tax Location | Contains the description for the location where the job exists. | JobApplicationEvent | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Tax Location Name | Contains the name for the location where the job exists. | JobApplicationEvent | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Work Hours | Contains the number of hours the applicant is expected to work. | JobApplicationEvent | [A-...] | MAPPED |
| Application Id | Application Id for a candidate. | JobApplicationEvent | [A-...] | MAPPED |
| Application Created By  | Contains the name of the recruiter who applied for the candidate. If the candidate applied, Self is  | CreationDate | [A-...] | MAPPED |
| Application Created By  | Contains the name of the opportunity application created by (concatenated) that had the change made  | CreationDate | [A-...] | MAPPED |
| Application Deleted | Indicates if the application has been deleted from the system. | - | [A-...] | SYSTEM |
| Application Deleted By  | Contains the name of the individual who deleted the application. | - | [A-...] | SYSTEM |
| Application Deleted By  | Contains the name of the opportunity application deleted by (concatenated) that had the change made  | - | [A-...] | SYSTEM |
| Application Deleted Date | Contains the date the application was deleted from the system. | - | [A-...] | SYSTEM |
| Application Internal/External | Indicates if the candidate is an internal (e.g. employee) or external candidate when they applied to | Type | [A-...] | MAPPED (Reference) |
| Candidate  | Contains the concatenated name of candidate. | ApplicantCode | [A-...] | MAPPED |
| Candidate  | Contains the name of the opportunity candidate (concatenated) that had the change made to, Format is | ApplicantCode | [A-...] | MAPPED |
| Candidate Active/Inactive | Indicates if the candidate was active or inactive when they applied to the opportunity.  All externa | ApplicantCode | [A-...] | MAPPED |
| Date Applied | Contains the date the candidate applied to the opportunity. | Date | [A-...] | MAPPED |
| Disability | Indicates if the candidate has self-identified as having a disability. | JobApplicationEvent | [A-IncapacityStatus] | MAPPED |
| Electronic Signature | Contains the name entered for simulating an electronic signature.  | JobApplicationEvent | [A-...] | MAPPED |
| Electronic Signature Date | Contains the date entered for the electronic signature. | JobApplicationEvent | [A-...] | MAPPED |
| Ethnic Origin | Contains the self-identified ethnicity for the candidate. | JobApplicationEvent | [A-...] | MAPPED |
| Gender | Contains the self-identified gender for the candidate. | JobApplicationEvent | [A-Sex] | MAPPED |
| Opportunity Title | Contains the title for the opportunity. | JobApplicationEvent | [A-Civility] / [A-Title] | MAPPED |
| Recruiting Hire Date | Contains the date Recruiting started the hiring process. | JobApplicationEvent | [A-...] | MAPPED |
| Requisition Number | Contains the requisition number for the opportunity. | JobApplicationEvent | [P-ReferenceEditable] / [O-ReferenceEditable] | MAPPED |
| Source | Contains the name of source in which the candidate became aware of the opportunity. | PublicationSupport | [A-Source] | MAPPED (Reference) |
| Start Date | Contains the date the candidate is able to start. | JobApplicationEvent | [O-BeginningDate] | MAPPED |
| Status Code | Contains the code for the standard Initial, Accepted or Rejected status. | JobApplicationEvent | [A-...] | MAPPED |
| Status | Contains the description for the standard Initial, Accepted or Rejected status. | JobApplicationEvent | [A-...] | MAPPED |
| Step | Contains the name of the step in the recruiting process the candidate is in. | JobApplicationEvent | [A-...] | MAPPED |
| Step Date | Contains the date the candidate entered the step. | JobApplicationEvent | [A-...] | MAPPED |
| Veteran | Indicates if the candidate has self-identified as being a veteran. | JobApplicationEvent | [A-...] | MAPPED |
| Application Created By  | Contains the unique identifier for an application created  in the Dimension table. | To be mapped | [A-...] | MAPPED |
| Application Created By  | Contains the unique identifier for an application created in the User Dimension table.  | To be mapped | [A-...] | MAPPED |
| Application Deleted By  | Contains the unique identifier for an application deleted in the Dimension table.  | To be mapped | [A-...] | MAPPED |
| Application Deleted By  | Contains the unique identifier for an application deleted in the User Dimension table.  | To be mapped | [A-...] | MAPPED |
| Application Key  | Contains the unique identifier for an application in the Dimension table. Can be use to join to Fact | To be mapped | [A-...] | MAPPED |
| Application Key  | Contains the unique identifier for an application in the Fact table. Can be use to join to applicati | To be mapped | [A-...] | MAPPED |
| Candidate Opportunity Key  | Contains the unique identifier for a candidate in the Fact table. Can be use to join to Candidate Di | To be mapped | [A-...] | MAPPED |
| Candidate Opportunity Key  | Contains the unique identifier for a candidate in the Dimension table. Can be use to join to Fact ta | To be mapped | [A-...] | MAPPED |
| Candidate Source Key  | Contains the unique identifier for a candidate source in the Fact table. Can be use to join to Candi | To be mapped | [A-Source] | MAPPED |
| Candidate Source Key  | Contains the unique identifier for a candidate source in the Dimension table. Can be use to join to  | To be mapped | [A-Source] | MAPPED |
| Disposition Status Key  | Contains the unique identifier for a disposition status in the Fact table. Can be use to join to Dis | To be mapped | [A-...] | MAPPED |
| Disposition Status Key  | Contains the unique identifier for a disposition status in the Dimension table. Can be use to join t | To be mapped | [A-...] | MAPPED |
| Disposition Note Key  | Contains the unique identifier for an disposition note in the Fact table. Can be use to join to Disp | To be mapped | [A-...] | MAPPED |
| Disposition Note Key  | Contains the unique identifier for a disposition note in the Dimension table. Can be use to join to  | To be mapped | [A-...] | MAPPED |
| Disposition Reason Key  | Contains the unique identifier for a disposition reason in the Dimension table. Can be use to join t | To be mapped | [A-...] | MAPPED |
| Disposition Reason Key  | Contains the unique identifier for a disposition reason in the Dimension table.  | To be mapped | [A-...] | MAPPED |
| Opportunity Key  | Contains the unique identifier for an opportunity in the Fact table. Can be use to join to Opportuni | To be mapped | [A-...] | MAPPED |
| Opportunity Key  | Contains the unique identifier for an opportunity in the Dimension table. Can be use to join to Fact | To be mapped | [A-...] | MAPPED |
| Process Step Key  | Contains the unique identifier for a process step in the Dimension table. Can be use to join to Fact | To be mapped | [A-...] | MAPPED |
| Process Step Key  | Contains the unique identifier for a process step in the Fact table. Can be use to join to Step Dime | To be mapped | [A-...] | MAPPED |
| Profile Created Key  | Contains the unique identifier for a profile created  in the Dimension table. | To be mapped | [A-...] | MAPPED |
| Profile Created Key  | Contains the unique identifier for a profile created in the User Dimension table.  | To be mapped | [A-...] | MAPPED |
| Recruiting Person ID  | Recruiting Person ID | To be mapped | [A-...] | MAPPED |
| Active/Inactive | Indicates if the candidate is an active employee or inactive employee.  This field only pertains to  | ApplicantStatus | [A-...] | MAPPED (Reference) |
| Candidate  | Contains the full name of the candidate.   | To be mapped | [A-...] | MAPPED |
| Candidate  | Contains the name of the opportunity candidate (concatenated) that had the change made to, Format is | To be mapped | [A-...] | MAPPED |
| Candidate  | Contains the candidate's concatenated name, including their title, if any. | To be mapped | [A-...] | MAPPED |
| Candidate  | Contains the name of the opportunity candidate (concatenated) that had the change made to, Format is | To be mapped | [A-...] | MAPPED |
| Consent Status | Contains the candidate's response to the GDPR consent question presented to them. | consents[] | [A-Consent] | MAPPED |
| Consent Version | Contains the version of the GDPR consent question the candidate responded to. | consents[] | [A-Consent] | MAPPED |
| First Name | Contains the candidate's first name. | FirstName | [A-FirstName] | MAPPED |
| Preferred Name | Contains the candidate's preferred name. | To be mapped | [A-FirstName] (alias) | MAPPED |
| Former Name | Contains the candidate's former last name, if any. | To be mapped | [A-...] | MAPPED |
| Internal/External | Indicates if the candidate is CURRENTLY an internal (e.g. employee) or external candidate.  Note:  T | To be mapped | [A-...] | MAPPED |
| Last Name | Contains the candidate's last name. | Name | [A-Name] | MAPPED |
| Middle Name | Contains the candidate's middle name. | MiddleName | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Primary Phone | Contains the candidate's formatted primary phone number. | PhoneNumber1 | [A-PhoneNumber1] | MAPPED |
| Profile Created By | Contains the name of the Recruiter who created the candidate's profile.  If the candidate created th | To be mapped | [A-...] | MAPPED |
| Profile Created Date | Contains the date the candidate's profile was added to UltiPro. | To be mapped | [A-...] | MAPPED |
| Secondary Phone | Contains the candidate's formatted secondary phone number. | PhoneNumber2 | [A-PhoneNumber2] | MAPPED |
| Suffix | Contains the candidate's name suffix (e.g. Jr.). | To be mapped | [A-...] | MAPPED |
| Title | Contains the candidate's title. | To be mapped | [A-Civility] / [A-Title] | MAPPED |
| Willing To Relocate | Indicates if the candidate is willing to travel. | TotalMobility | [A-...] | MAPPED |

---

## Candidate - Education

**Talentsoft Equivalent:** Applicant - Education  
**Field Count:** 30

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Education Description | Contains the optional additional information describing the candidates school experience. | To be mapped | [A-...] | MAPPED |
| From Month  | Contains the month the candidate started at the school. | To be mapped | [A-...] | MAPPED |
| From Year  | Contains the year the candidate started at the school. | To be mapped | [A-...] | MAPPED |
| Level of Education/Degree | Contains the level of education the candidate achieved at the school. | To be mapped | [A-...] | MAPPED |
| Major | Contains the major, if any, the candidate had at the school. | To be mapped | [A-...] | MAPPED |
| Minor | Contains the minor, if any, the candidate had at the school. | To be mapped | [A-...] | MAPPED |
| School Name | Contains the name of the school the candidate attended. | To be mapped | [A-College] | MAPPED |
| To Month  | Contains the month the candidate completed their studies at the school. | To be mapped | [A-...] | MAPPED |
| To Year  | Contains the year the candidate completed their studies at the school. | To be mapped | [A-...] | MAPPED |
| Years In School | Contains the calculated number of years (1 decimal position) the candidate was in school. | To be mapped | [A-College] | MAPPED |
| Date Achieved | Contains the date candidate achieved the license/certification. | To be mapped | [A-...] | MAPPED |
| License Number | Certification ID number. Maps to If yes, Number field. | To be mapped | [A-Diploma_ShortText2] | MAPPED (Custom) |
| License/Certification | Contains the license/certification earned by the candidate. | To be mapped | [A-...] | MAPPED |
| Months To Renewal | Months until license renewal required. NOT AVAILABLE in Talentsoft. | To be mapped | NOT AVAILABLE | NOT AVAILABLE |
| Renewal Date | Contains the date the license/certification must be renewed. | To be mapped | [A-...] | MAPPED |
| Description  | Contains the optional additional information describing the candidates school experience. | educations[] | [A-...] | MAPPED |
| From Month  | Contains the month the candidate started at the school. | educations[] | [A-...] | MAPPED |
| From Year  | Contains the year the candidate started at the school. | educations[].yearOfGraduation | [A-...] | MAPPED |
| Level of Education/Degree  | Contains the level of education the candidate achieved at the school. | educations[].diploma | [A-...] | MAPPED (Reference) |
| Major  | Contains the major, if any, the candidate had at the school. | educations[] | [A-...] | MAPPED |
| Minor  | Contains the minor, if any, the candidate had at the school. | educations[] | [A-...] | MAPPED |
| School Name  | Contains the name of the school the candidate attended. | educations[].school | [A-College] | MAPPED |
| To Month  | Contains the month the candidate completed their studies at the school. | educations[] | [A-...] | MAPPED |
| To Year  | Contains the year the candidate completed their studies at the school. | educations[].yearOfGraduation | [A-...] | MAPPED |
| Years In School  | Contains the calculated number of years (1 decimal position) the candidate was in school. | educations[].school | [A-College] | MAPPED |
| Date Achieved  | Contains the date candidate achieved the license/certification. | JobApplicationEvent | [A-...] | MAPPED |
| License Number  | Contains the number of license, if any. | CustomField | [A-Diploma_ShortText2] | MAPPED (Custom) |
| License/Certification Name  | Contains the license/certification earned by the candidate. | CustomField | [A-Diploma_LongText2] | MAPPED (Custom) |
| Months To Renewal  | Contains the calculated number of months before the candidate's license/certification needs to be re | JobApplicationEvent | [A-...] | NOT AVAILABLE |
| Renewal Date  | Contains the date the license/certification must be renewed. | JobApplicationEvent | [A-...] | MAPPED |

---

## Candidate - Experience

**Talentsoft Equivalent:** Applicant - Experience  
**Field Count:** 18

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Company/Organization | Contains the name of the organization where the candidate previously worked. | To be mapped | [P-Entity] / [O-Entity] | MAPPED |
| From Month  | Contains the starting month for the work experience. | To be mapped | [A-...] | MAPPED |
| From Year  | Contains the starting year for the work experience. | To be mapped | [A-...] | MAPPED |
| Job Title | Contains the title of the job/position the candidate previously held. | To be mapped | [P-JobTitle] / [O-JobTitle] | MAPPED |
| Location | Contains the name of the location where the candidate previously worked. | To be mapped | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| To Month  | Contains the ending month for the work experience.  If the candidate is still employed, this field w | To be mapped | [A-...] | MAPPED |
| To Year  | Contains the ending year for the work experience.  If the candidate is still employed, this field wi | To be mapped | [A-...] | MAPPED |
| Work Experience Description | Contains the optional additional information describing the candidates work experience. | To be mapped | [A-...] | MAPPED |
| Years Employed | Contains the calculated number of years (1 decimal position) the candidate was employed for. | To be mapped | [A-...] | MAPPED |
| Company/Organization  | Contains the name of the organization where the candidate previously worked. | Company | [P-Entity] / [O-Entity] | MAPPED |
| Description  | Contains the optional additional information describing the candidates work experience. | experiences[] | [A-...] | MAPPED |
| From Month  | Contains the starting month for the work experience. | experiences[] | [A-...] | MAPPED |
| From Year  | Contains the starting year for the work experience. | experiences[] | [A-...] | MAPPED |
| Job Title  | Contains the title of the job/position the candidate previously held. | Function | [P-JobTitle] / [O-JobTitle] | MAPPED |
| Location  | Contains the name of the location where the candidate previously worked. | experiences[] | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| To Month  | Contains the ending month for the work experience.  If the candidate is still employed, this field w | experiences[] | [A-...] | MAPPED |
| To Year  | Contains the ending year for the work experience.  If the candidate is still employed, this field wi | experiences[] | [A-...] | MAPPED |
| Years Employed  | Contains the calculated number of years (1 decimal position) the candidate was employed for. | experiences[] | [A-...] | MAPPED |

---

## Candidate - Personal

**Talentsoft Equivalent:** Applicant (Candidate)
**Field Count:** 19

> **CORRECTED 2025-11-23:** Email fields must use `[A-Email]`, NOT `[A-Address]` (semantic error)

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Email Address  | Contains the email address of the individual who applied on behalf of the candidate. | JobApplicationEvent | **[A-Email]** | MAPPED |
| Email Address  | Contains the email address of the individual who deleted the application. | JobApplicationEvent | **[A-Email]** | MAPPED |
| Address 1 | Contains the candidate's address line 1. | Address | [A-Address] | MAPPED |
| Address 2 | Contains the candidate's address line 2. | Address | [A-Address] | MAPPED |
| City | Contains the candidate's city. | City | [A-City] | MAPPED |
| Country Code | Contains the code for the country. | ResidenceCountry | [A-ResidenceCountry] | MAPPED (Reference) |
| Country | Contains the description for the country. | ResidenceCountry | [A-ResidenceCountry] | MAPPED (Reference) |
| State/Province Code | Contains the candidate's state or province code. | Region | [A-...] | MAPPED (Reference) |
| State/Province | Contains the candidate's state or province description. | Region | [A-...] | MAPPED (Reference) |
| Zip/Postal Code | Contains the candidate's zip or postal code. | PostalCode | [A-PostalCode] | MAPPED |
| Tax Location City | The tax location city for the opportunity | City | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Tax Location Country Code | The tax location code for the country of the opportunity | ResidenceCountry | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Tax Location Country | The tax location country name of the opportunity | ResidenceCountry | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Tax Location State Code | The tax location state code for the opportunity | Region | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Tax Location State | The tax location state for the opportunity | Region | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Email Address  | Contains the email address of the individual who created the candidate's profile. | Email | [A-Address] | MAPPED |
| Hiring Manager Email Address  | Contains the email address for the Hiring Manager associated to the application's hire details. | OperationalManager* | [P-OperationalManagerEmail] / [O-OperationalManagerEmail] | MAPPED |
| Onboarding Owner Email Address  | Contains the email address for the Onboarding Owner associated to the application's hire details. | JobApplicationEvent | [A-Address] | MAPPED |
| Email Address | Contains the candidate's email address. | Email | [A-Email] | MAPPED |

---

## Candidate - Referral

**Talentsoft Equivalent:** Applicant - Referral  
**Field Count:** 3

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Referral Email | Contains the email address of the employee who referred the candidate. | JobApplicationEvent | [A-RecommendedBy2] | MAPPED |
| Referral Name | Contains the name of the employee who referred the candidate. | JobApplicationEvent | [A-...] | MAPPED |
| Referral Phone | Contains the phone number of the employee who referred the candidate. | JobApplicationEvent | [A-RecommendedBy3] | MAPPED |

---

## Opportunity

**Talentsoft Equivalent:** Vacancy Request / Vacancy (Offer)  
**Field Count:** 136

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Company Code | Contains the code for the company associated to the opportunity. | EntityCode | [P-Entity] / [O-Entity] | MAPPED (Reference) |
| Company | Contains the name for the company associated to the opportunity. | EntityLabel | [P-Entity] / [O-Entity] | MAPPED (Reference) |
| Location Code | Contains the code for the location(s) which apply to the opportunity. | Entity (Location level) | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Location | Contains the description for the location(s) that have been assigned to the opportunity. | Entity (Location level) | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Location Name | Contains the name for the location(s) that have been assigned the opportunity. | Entity (Location level) | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Org Level 1 Code | Contains the code for the first organization level associated to the opportunity.  The organization  | Entity (hierarchical) | [O-...] | MAPPED (Reference) |
| Org Level 1 | Contains the description for the first organization level associated to the opportunity.  The organi | Entity (hierarchical) | [O-...] | MAPPED (Reference) |
| Org Level 2 Code | Contains the code for the second organization level associated to the opportunity.  The organization | Entity (hierarchical) | [O-...] | MAPPED (Reference) |
| Org Level 2 | Contains the description for the second organization level associated to the opportunity.  The organ | Entity (hierarchical) | [O-...] | MAPPED (Reference) |
| Org Level 3 Code | Contains the code for the third organization level associated to the opportunity.  The organization  | Entity (hierarchical) | [O-...] | MAPPED (Reference) |
| Org Level 3 | Contains the description for the third organization level associated to the opportunity.  The organi | Entity (hierarchical) | [O-...] | MAPPED (Reference) |
| Org Level 4 Code | Contains the code for the fourth organization level associated to the opportunity.  The organization | Entity (hierarchical) | [O-...] | MAPPED (Reference) |
| Org Level 4 | Contains the description for the fourth organization level associated to the opportunity.  The organ | Entity (hierarchical) | [O-...] | MAPPED (Reference) |
| Full-Time Or Part-Time | Contains the description indicating if the opportunity is a full-time or part-time position. | JobTime | [O-...] | MAPPED (Reference) |
| Rate | Contains the salary or the hourly rate the opportunity is expected to pay. | SalaryRange | [O-...] | MAPPED (Reference) |
| Rate Visibility | Indicates which job boards (Internal, External, All, None) will show the pay rate. | SalaryRange | [O-...] | MAPPED (Reference) |
| Salary Or Hourly | Contains the description indicating if the opportunity is a salary or hourly position. | SalaryRange | [O-...] | MAPPED (Reference) |
| Salary/Hourly Currency Code | Contains the code for currency the opportunity will be paid in. | SalaryRange | [P-PreliminaryJobDescription_CustomCodeTableValue1] / [O-JobDescription_CustomCodeTableValue2] | MAPPED (Reference) |
| Show Compensation On | Indicates if the compensation is to be displayed on the internal, external or all job boards. | To be mapped | [O-...] | MAPPED (Reference) |
| Recruiting Process | Contains the name of the recruiting process used by the opportunity. | OperationalManager* | [O-...] | MAPPED |
| Recruiting Process Steps | Contains the names of the individual steps used in the recruiting process. | OperationalManager* | [O-...] | MAPPED |
| Shared With Everyone | Indicates if the opportunity is to be available to all recruiters. | OperationalManager* | [O-...] | MAPPED |
| City | Contains the name of city the opportunity is available in. | JobLocation | [A-City] | MAPPED |
| Country Code | Contains the code for the country the opportunity is available in. | Country | [A-ResidenceCountry] | MAPPED (Reference) |
| Country | Contains the description for the country the opportunity is available in. | Country | [A-ResidenceCountry] | MAPPED (Reference) |
| State/Province Code | Contains the code for the State the opportunity is available in. | OfferLocation / Region | [O-...] | MAPPED |
| State/Province | Contains the description for the State/Province the opportunity is available in. | OfferLocation / Region | [O-...] | MAPPED |
| Tax Location City | The tax location city for the opportunity | JobLocation | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Tax Location Country Code | The tax location code for the country of the opportunity | Country | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Tax Location Country | The tax location country name of the opportunity | Country | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED (Reference) |
| Tax Location State Code | The tax location state code for the opportunity | OfferLocation / Region | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Tax Location State | The tax location state for the opportunity | OfferLocation / Region | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Email Address  | Contains the email address of the individual who deleted the opportunity. | CustomField | [A-Address] | MAPPED |
| First Name  | Contains the first name of the individual who deleted the opportunity. | CustomField | [A-FirstName] | MAPPED |
| Preferred Name  | Contains the Preferred name of the individual who deleted the opportunity. | CustomField | [O-...] | MAPPED |
| Last Name  | Contains the last name of the individual who deleted the opportunity. | CustomField | [A-Name] | MAPPED |
| Middle Name  | Contains the middle name of the individual who deleted the opportunity. | CustomField | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Opportunity Deleted By  | Contains the concatenated name, including their title, if any, of the individual who deleted the opp | OfferStatus | [O-...] | SYSTEM |
| Opportunity Deleted By  | Contains the name of the opportunity deleted by (concatenated) that had the change made to, Format i | OfferStatus | [O-...] | SYSTEM |
| Primary Phone  | Contains the unformatted primary phone number of the individual who deleted the opportunity. | CustomField | [A-PhoneNumber1] | MAPPED |
| Secondary Phone  | Contains the unformatted secondary phone number of the individual who deleted the opportunity. | CustomField | [A-PhoneNumber2] | MAPPED |
| Suffix  | Contains the name suffix (e.g. Jr.) of the individual who deleted the opportunity. | CustomField | [O-...] | MAPPED |
| Title  | Contains the title of the individual who deleted the opportunity. | JobTitle | [A-Civility] / [A-Title] | MAPPED |
| Degree | Indicates the level of education (degree) the opportunity is seeking. | CustomField | [A-TreeNode_Diploma] | MAPPED |
| Education Required | Indicates if the opportunity considers the degree/major to be required. | CustomField | [O-...] | MAPPED |
| Major | Indicates the desired major the opportunity is seeking. | CustomField | [O-...] | MAPPED |
| Related | Indicates if the opportunity considers any related degree/major acceptable to the one specified. | CustomField | [O-...] | MAPPED |
| License/Certification | Contains the name of the license/certification identified for the opportunity. | CustomField | [O-...] | MAPPED |
| Licenses and Certifications Required | Indicates if the opportunity considers the license to be required. | CustomField | [A-Diploma_LongText2] | MAPPED |
| Maximum Years | Contain the maximum number of years required for the work experience.  This field is only populated  | CustomField | [O-...] | MAPPED |
| Minimum Years | Contain the minimum number of years required for the work experience.  This field is always populate | CustomField | [O-...] | MAPPED |
| Work Description | Contains the description for the desired work experience for the opportunity. | Description1 | [O-...] | MAPPED |
| Work Experience Required | Indicates if the opportunity considers the work experience to be required. | CustomField | [O-...] | MAPPED |
| Approval Comment Created Date | Contains the Approval Comment Created Date for reporting on opportunity details | CreationDate | [O-...] | MAPPED |
| Approval Comment ID | Contains the Approval Comment ID for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Approval Comment Last Modified | Contains the Approval Comment Last Modified for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Approval Comment Type | Contains the Approval Comment Type for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Approval Reassigned From | Contains the Approval Reassigned From for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Approval Reassigned From Name | Contains the name of the Reassigned from | CustomField | [O-...] | MAPPED |
| Approval Reassigned To | Contains the Approval Reassigned To for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Approval Reassigned To Name | Contains the name of the Reassigned to | CustomField | [O-...] | MAPPED |
| Comment | Contains the Comment for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Comment Creator ID | Contains the Comment Creator ID for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Comment Date | Contains the Comment Date for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Comment Sent Via Email | Contains the Comment Sent Via Email for reporting on opportunity details | CustomField | [A-Email] | MAPPED |
| Opportunity ID | Contains the Opportunity ID for reporting on opportunity details | CustomField | [O-...] | MAPPED |
| Approval Process Type | Contains the approval process type for the opportunity approval | CustomField | [O-...] | MAPPED |
| Approval Status | Contains the approval status for the opportunity approval | OfferStatus | [O-...] | MAPPED (Reference) |
| Approval Status Date | Contains the approval status date for the opportunity approval | OfferStatus | [O-...] | MAPPED (Reference) |
| Approver ID | Contains the approver ID for the opportunity approval | CustomField | [O-...] | MAPPED |
| Approver Lost Role | Contains the approver lost role for the opportunity approval | CustomField | [O-...] | MAPPED |
| Opportunity Approver Name | Contains the name of opportunity approver | CustomField | [O-...] | MAPPED |
| Closed By | Contains the Closed By of the Opportunity | CustomField | [O-...] | MAPPED |
| Closed By Name | Contains the Closed By Name of the Opportunity | CustomField | [O-...] | MAPPED |
| Closing Reason Name | Contains the Closing Reason Name of the Opportunity | CustomField | [O-...] | MAPPED |
| Comment Creator ID Name | Contains the name of the comment creator | CustomField | [O-...] | MAPPED |
| Candidate Source Key  | Contains the unique identifier for a candidate source in the Fact table. Can be use to join to Recru | CustomField | [A-Source] | MAPPED |
| Candidate Source Key  | Contains the unique identifier for a candidate source in the Dimension table. Can be use to join to  | CustomField | [A-Source] | MAPPED |
| Company Key  | Contains the unique identifier for a company in the Dimension table. Can be use to join to Fact tabl | CustomField | [P-Entity] / [O-Entity] | MAPPED |
| Company Key  | Contains the unique identifier for a company in the Fact table. Can be use to join to Company Dimens | CustomField | [P-Entity] / [O-Entity] | MAPPED |
| Company Key  | Contains the unique identifier for a company in the Fact table. Can be use to join to Company Dimens | CustomField | [P-Entity] / [O-Entity] | MAPPED |
| Current Process Step Key  | Contains the unique identifier for a current process step in the Fact table. Can be use to join to R | CustomField | [O-...] | MAPPED |
| Current Process Step Key  | Contains the unique identifier for a current process step in the Dimension table. Can be use to join | CustomField | [O-...] | MAPPED |
| Deleted By Key  | Contains the unique identifier for an opportunity deleted  in the Dimension table.  | OfferStatus | [O-...] | SYSTEM |
| Disposition Note Key  | Contains the unique identifier for an disposition note in the Fact table. Can be use to join to Disp | CustomField | [O-...] | MAPPED |
| Disposition Note Key  | Contains the unique identifier for an disposition note in the Dimension table.  | CustomField | [O-...] | MAPPED |
| Disposition Reason Key  | Contains the unique identifier for a disposition reason in the Disposition Note Dimension table. | CustomField | [O-...] | MAPPED |
| Disposition Reason Key  | Contains the unique identifier for a disposition reason in the Dimension table. Can be use to join t | CustomField | [O-...] | MAPPED |
| Disposition Status Key  | Contains the unique identifier for a disposition status in the Fact table. Can be use to join to Rec | OfferStatus | [O-...] | MAPPED (Reference) |
| Disposition Status Key  | Contains the unique identifier for a disposition status step in the Dimension table. Can be use to j | OfferStatus | [O-...] | MAPPED (Reference) |
| Job Key  | Contains the unique identifier for a job in the Dimension table. Can be use to join to Fact table. | CustomField | [O-...] | MAPPED |
| Job Key  | Contains the unique identifier for a job in the Fact table. Can be use to join to Job Dimension. | CustomField | [O-...] | MAPPED |
| Opportunity Candidate Key  | Contains the unique identifier for a candidate in the Fact table. Can be use to join to Candidate Di | CustomField | [O-...] | MAPPED |
| Opportunity Candidate Key  | Contains the unique identifier for a candidate in the Dimension table. Can be use to join to Fact ta | CustomField | [O-...] | MAPPED |
| Opportunity ID  | Contains the unique identifier for the opportunity.  This value is visible in the URL when viewing t | CustomField | [O-...] | MAPPED |
| Opportunity Key  | Contains the unique identifier for an opportunity in the Fact table. Can be use to join to Opportuni | CustomField | [O-...] | MAPPED |
| Opportunity Key  | Contains the unique identifier for the application.  Used to the link to the application table. | CustomField | [O-...] | MAPPED |
| Opportunity Key  | Contains the unique identifier for an opportunity in the work location bridge table. | CustomField | [O-...] | MAPPED |
| Opportunity Key  | Contains the unique identifier for an opportunity in the Dimension table. Can be use to join to Fact | CustomField | [O-...] | MAPPED |
| Opportunity Key  | Contains the unique identifier for an opportunity in the Fact table. Can be use to join to Opportuni | CustomField | [O-...] | MAPPED |
| Opportunity Key  | Contains the unique identifier for the opportunity.  Used to link to the Opportunity table. | CustomField | [O-...] | MAPPED |
| Process Key  | Contains the unique identifier for a process in the Fact table. Can be use to join to Process Dimens | CustomField | [O-...] | MAPPED |
| Process Key  | Contains the unique identifier for a process in the Dimension table. Can be use to join to Fact tabl | CustomField | [O-...] | MAPPED |
| Question Key  | Contains the unique identifier for the question. | CustomField | [O-...] | MAPPED |
| Question Key  | Contains the unique identifier for the question.  Used to the link to the question table. | CustomField | [O-...] | MAPPED |
| Question Key  | Contains the unique identifier for the question. | CustomField | [O-...] | MAPPED |
| Work Location Key  | Contains the unique identifier for a work location in the bridge table. Can be use to join to the di | CustomField | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Work Location Key  | Contains the unique identifier for a work location in the Dimension table. Can be use to join to the | CustomField | [P-Location_GeographicalAreaCollection] / [O-Location_GeographicalAreaCollection] | MAPPED |
| Closed Date | Contains the date the opportunity was closed. | CustomField | [O-...] | MAPPED |
| Created Date | Contains the date the opportunity was created. | CreationDate | [O-...] | MAPPED |
| Deleted | Indicates if the opportunity was deleted/removed. | OfferStatus | [O-...] | SYSTEM |
| Deleted By  | Contains the name of the individual who deleted the opportunity. | OfferStatus | [O-...] | SYSTEM |
| Deleted By  | Contains the name of the opp deleted by (concatenated) that had the change made to, Format is Last S | OfferStatus | [O-...] | SYSTEM |
| Deleted Date | Contains the date the opportunity was deleted. | OfferStatus | [O-...] | SYSTEM |
| Detailed Description | Contains the opportunity detailed description. | Description1 | [O-...] | MAPPED |
| Detailed Description  | Contains the opportunity detailed description used for internal postings only. This field may be emp | Description1 | [O-...] | MAPPED |
| EEO Category Code | Contains the code for the EEO category assigned to the job associated to the opportunity. | EEOCode | [O-OfferCategory] | MAPPED (Reference) |
| EEO Category | Contains the description for the EEO category assigned to the job associated to the opportunity. | EEOCode | [O-OfferCategory] | MAPPED (Reference) |
| EOE Message Displayed | Indicates if the Equal Opportuntity Employer message is displayed when viewing the opportunity. | CustomField | [O-...] | MAPPED |
| Featured | Indicates that the opportunity is a featured opportunity or not. | CustomField | [O-...] | MAPPED |
| First Published Date | Contains the date the opportunity was first published. | Publication* | [O-...] | MAPPED |
| Job Family Code | Contains the code for the job family associated to the job.  | PrimaryProfile | [P-Profile] / [O-PrimaryProfile] | MAPPED (Reference) |
| Job Family | Contains the description for the job family associated to the job.  | PrimaryProfile | [P-Profile] / [O-PrimaryProfile] | MAPPED (Reference) |
| Notes/Comments  | Contains the internal notes, or comments, if any, made on the opportunity. | CustomField | [A-Comment] | MAPPED |
| Opportunity Status | Contains the status for the opportunity (e.g. draft, approved…). | OfferStatus | [O-...] | MAPPED (Reference) |
| Opportunity Title | Contains the title for the opportunity. | JobTitle | [A-Civility] / [A-Title] | MAPPED |
| Opportunity Title  | Contains the opportunity title used for internal postings only. This field may be empty. | JobTitle | [A-Civility] / [A-Title] | MAPPED |
| Pay Transparency Message Displayed | Indicates if the Pay Transparency message is displayed when viewing the opportunity. | CustomField | [O-...] | MAPPED |
| Requisition Number | Contains the requisition number for the opportunity. | OfferReference | [P-ReferenceEditable] / [O-ReferenceEditable] | MAPPED |
| Short Description | Contains a short synopsis of the opportunity visible to external candidates. | Description1 | [O-...] | MAPPED |
| Short Description  | Contains the opportunity short description used for internal postings only. This field may be empty. | Description1 | [O-...] | MAPPED |
| Source Job Code | Contains the code for the job for which the opportunity is based on. | CustomField | [A-Source] | MAPPED |
| Source Job | Contains the description for the job for which the opportunity is based on. | CustomField | [A-Source] | MAPPED |
| Travel Details | Contains the optional text entered explaining the details for the travel. | CustomField | [O-...] | MAPPED |
| Travel Required | Indicates if travel is required for this opportunity. | CustomField | [O-...] | MAPPED |
| Travel Visibility | Indicates which job boards (Internal, External, All, None) will show the travel requirements. | CustomField | [O-...] | MAPPED |

---

## Opportunity - Manager

**Talentsoft Equivalent:** Vacancy Request / Vacancy (Offer)
**Field Count:** 28

> **CORRECTED 2025-11-23:** Manager fields must use P-/O- prefix, NOT A- prefix

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Email Address  | Contains the email address for the Hiring Manager associated to the opportunity. | OperationalManagerEmail | **[P-OperationalManagerEmail] / [O-OperationalManagerEmail]** | MAPPED |
| Primary Phone  | Contains the primary phone number for the Hiring Manager associated to the opportunity. | OperationalManagerPhoneNumber | **[P-OperationalManagerPhoneNumber] / [O-OperationalManagerPhoneNumber]** | MAPPED |
| Secondary Phone  | Contains the secondary phone number for the Hiring Manager associated to the opportunity. | OperationalManagerPhoneNumber | **[P-OperationalManagerPhoneNumber] / [O-OperationalManagerPhoneNumber]** | MAPPED |
| Title  | Contains the salutation (e.g. Mr., Mrs. Dr., etc.) for the hiring manager associated to the opportun | OperationalManager* | [P-...] / [O-...] | NOT AVAILABLE |
| First Name  | Contains the first name for the Hiring Manager associated to the opportunity. | OperationalManagerFirstName | **[P-OperationalManagerFirstName] / [O-OperationalManagerFirstName]** | MAPPED |
| Preferred Name  | Contains the preferred name for the Hiring Manager associated to the opportunity. | OperationalManager* | [O-...] | MAPPED |
| Last Name  | Contains the last name for the Hiring Manager associated to the opportunity. | OperationalManagerName | **[P-OperationalManagerName] / [O-OperationalManagerName]** | MAPPED |
| Middle Name  | Contains the middle name for the Hiring Manager associated to the opportunity. | OperationalManager* | [P-...] / [O-...] | MAPPED |
| Suffix  | Contains the suffix for the Hiring Manager associated to the opportunity. | OperationalManager* | [O-...] | NOT AVAILABLE |
| Opportunity Hiring Manager  | Contains the Hiring Manager's concatenated name, including their title, if any. | OperationalManager* | [O-...] | MAPPED |
| Opportunity Hiring Manager  | Contains the name of the opportunity hiring manager (concatenated) that had the change made to, Form | OperationalManager* | [O-...] | MAPPED |
| Hiring Manager  | Contains the name of the hiring manager (concatenated) that had the change made to, Format is Prefer | OperationalManager* | [O-...] | MAPPED |
| Hiring Manager | Contains the concatenated name of the hiring manager using the format: Last Suffix, First MI. | OperationalManager* | [O-...] | MAPPED |
| Hiring Manager  | Contains the concatenated name including title, if any, for the Hiring Manager associated to the app | OperationalManager* | [O-...] | MAPPED |
| Hiring Manager  | Contains the name of the opportunity hiring manager (concatenated) that had the change made to, Form | OperationalManager* | [O-...] | MAPPED |
| Prefix  | Contains the salutation for the hiring manager. | JobApplicationEvent | [O-...] | MAPPED |
| First Name  | Contains the first name of the hiring manager. | JobApplicationEvent | [A-FirstName] | MAPPED |
| Preferred Name  | Contains the preferred name of the hiring manager. | JobApplicationEvent | [O-...] | MAPPED |
| Middle Name  | Contains the middle name of the hiring manager. | JobApplicationEvent | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Last Name  | Contains the last name of the hiring manager. | JobApplicationEvent | [A-Name] | MAPPED |
| Suffix  | Contains the suffix (Jr, Sr, etc) of the hiring manager. | JobApplicationEvent | [O-...] | MAPPED |
| Hiring Manager  | Contains the concatenated name of the hiring manager using the format: First MI Last  Suffix. | OperationalManager* | [O-...] | MAPPED |
| Hiring Manager  | Contains the name of the opportunity hiring manager (concatenated) that had the change made to, Form | OperationalManager* | [O-...] | MAPPED |
| Hiring Manager  | Contains the concatenated name of the hiring manager using the format:  Last, Suffix First MI. | OperationalManager* | [O-...] | MAPPED |
| Hiring Manager  | Contains the name of the opportunity hiring manager (concatenated) that had the change made to, Form | OperationalManager* | [O-...] | MAPPED |
| Hiring Manager Email Address  | Contains the email address for the Hiring Manager associated to the application's hire details. | OperationalManager* | [P-OperationalManagerEmail] / [O-OperationalManagerEmail] | MAPPED |
| Hiring Manager Primary Phone  | Contains the primary phone number for the Hiring Manager associated to the application's hire detail | OperationalManager* | [A-PhoneNumber1] | MAPPED |
| Hiring Manager Secondary Phone  | Contains the secondary phone number for the Hiring Manager associated to the application's hire deta | OperationalManager* | [A-PhoneNumber2] | MAPPED |

---

## Opportunity - Onboarding

**Talentsoft Equivalent:** Vacancy (Offer)  
**Field Count:** 28

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Email Address  | Contains the email address for the Onboarding Owner associated to the opportunity. | OperationalManagerEmail | [A-Address] | MAPPED |
| Primary Phone  | Contains the primary phone number for the Onboarding Owner associated to the opportunity. | OperationalManagerPhoneNumber | [A-PhoneNumber1] | MAPPED |
| Secondary Phone  | Contains the secondary phone number for the Onboarding Owner associated to the opportunity. | OperationalManagerPhoneNumber | [A-PhoneNumber2] | MAPPED |
| Title  | Contains the salutation (e.g. Mr., Mrs. Dr., etc.) for the onboarding owner associated to the opport | OperationalManager* | [A-Civility] / [A-Title] | NOT AVAILABLE |
| First Name  | Contains the first name for the Onboarding Owner associated to the opportunity. | OperationalManagerFirstName | [A-FirstName] | MAPPED |
| Preferred Name  | Contains the preferred name for the Onboarding Owner associated to the opportunity. | OperationalManager* | [O-...] | MAPPED |
| Last Name  | Contains the last name for the Onboarding Owner associated to the opportunity. | OperationalManagerName | [A-Name] | MAPPED |
| Middle Name  | Contains the middle name for the Onboarding Owner associated to the opportunity. | OperationalManager* | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Suffix  | Contains the suffix for the Onboarding Owner associated to the opportunity. | OperationalManager* | [O-...] | NOT AVAILABLE |
| Opportunity Onboarding Owner  | Contains the Onboarding Owner's concatenated name, including their title, if any. | OperationalManager* | [O-...] | MAPPED |
| Opportunity Onboarding Owner  | Contains the name of the opportunity onboarding owner (concatenated) that had the change made to, Fo | OperationalManager* | [O-...] | MAPPED |
| Onboarding Owner  | Contains the name of the onboarding owner (concatenated) that had the change made to, Format is Pref | OperationalManager* | [O-...] | MAPPED |
| Onboarding Owner | Contains the concatenated name of the onboarding owner - Last Suffix, First MI. | OperationalManager* | [O-...] | MAPPED |
| Onboarding Owner  | Contains the concatenated name including title, if any, for the Onboarding Owner associated to the a | JobApplicationEvent | [O-...] | MAPPED |
| Onboarding Owner  | Contains the name of the opportunity onboarding owner (concatenated) that had the change made to, Fo | JobApplicationEvent | [O-...] | MAPPED |
| Prefix  | Contains the salutation for the onboarding owner. | JobApplicationEvent | [O-...] | MAPPED |
| First Name  | Contains the first name of the onboarding owner. | JobApplicationEvent | [A-FirstName] | MAPPED |
| Preferred Name  | Contains the preferred name of the onboarding owner. | JobApplicationEvent | [O-...] | MAPPED |
| Middle Name  | Contains the middle name of the onboarding owner. | JobApplicationEvent | [A-MiddleName] / [A-PersonalInformation_ShortText1] | MAPPED |
| Last Name  | Contains the last name of the onboarding owner. | JobApplicationEvent | [A-Name] | MAPPED |
| Suffix  | Contains the suffix (Jr, Sr, etc) of the onboarding owner. | JobApplicationEvent | [O-...] | MAPPED |
| Onboarding Owner  | Contains the concatenated name of the onboarding owner - First MI Last  Suffix. | JobApplicationEvent | [O-...] | MAPPED |
| Onboarding Owner  | Contains the name of the opportunity onboarding owner (concatenated) that had the change made to, Fo | JobApplicationEvent | [O-...] | MAPPED |
| Onboarding Owner  | Contains the concatenated name of the onboarding owner - Last, Suffix First MI. | JobApplicationEvent | [O-...] | MAPPED |
| Onboarding Owner  | Contains the name of the opportunity onboarding owner (concatenated) that had the change made to, Fo | JobApplicationEvent | [O-...] | MAPPED |
| Onboarding Owner Email Address  | Contains the email address for the Onboarding Owner associated to the application's hire details. | JobApplicationEvent | [A-Address] | MAPPED |
| Onboarding Owner Primary Phone  | Contains the primary phone number for the Onboarding Owner associated to the application's hire deta | JobApplicationEvent | [A-PhoneNumber1] | MAPPED |
| Onboarding Owner Secondary Phone  | Contains the secondary phone number for the Onboarding Owner associated to the application's hire de | JobApplicationEvent | [A-PhoneNumber2] | MAPPED |

---

## Opportunity - Opening

**Talentsoft Equivalent:** Vacancy Request / Vacancy (Offer)  
**Field Count:** 18

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Budgeted FTE | Full-Time Equivalent positions planned/budgeted for this opportunity. In Talentsoft, use FTE % field | NumberOfVacancies | [P-PreliminaryJobDescription_ShortText1] | MAPPED (Custom) |
| Continuous Opening  | Indicates if the opportunity is to be kept open until manually closed (evergreen). | CustomField | [O-...] | MAPPED |
| Filled FTE | Number of FTE positions already filled. Must calculate from hired applications count. | NumberOfVacancies | CALCULATE from applications | MUST CALCULATE |
| Hired Headcount | Number of people hired against this opportunity. Calculate from applications with Hired status. | NumberOfVacancies | CALCULATE from applications | MAPPED |
| Hours Per Shift | Expected work hours per shift for this position. | JobTime | [O-JobDescription_LongText1] | MAPPED (Reference) |
| Hours Per Week | Expected weekly work hours. Derived from JobTime (Full-time/Part-time). | JobTime | [O-JobTime] | MAPPED (Reference) |
| Impact To Staffing Plan | How this opening affects overall staffing plans. | CustomField | [O-CustomFields] | MAPPED |
| Incumbent First Name | First name of person currently holding the position being replaced. Maps to Name of person being rep | - | [P-RequestMotive_ShortText1] | MAPPED (Custom) |
| Incumbent Last Name | Last name of person currently holding the position. Combined with first name in Talentsoft. | - | [P-RequestMotive_ShortText1] | MAPPED (Custom) |
| Incumbent Name  | Contains the concatenated name (Last, First) of the individual who is currently holding the job asso | - | [O-...] | NOT AVAILABLE |
| Is Opening Budgeted? | Whether this position was approved in the budget. Maps to Budgeted vacancy request field. | CustomField | [P-Planned] | MAPPED |
| Last Day Worked | Last working day of incumbent. NOT AVAILABLE in Talentsoft - recommend custom field. | CustomField | NOT AVAILABLE | NOT AVAILABLE |
| Maximum Headcount | Maximum number of people allowed to hire for this position. Maps to NumberOfVacancies. | NumberOfVacancies | [P-NumberOfVacancies] / [O-NumberOfVacancies] | MAPPED |
| Priority | Hiring priority level for the opportunity. | CustomField | [O-CustomFields] | MAPPED |
| Reason For Opening | Contains the reason for the opportunity. | RecruitingReason | [P-RecruitingReason] / [O-RecruitingReason] | MAPPED (Reference) |
| Remaining FTE | FTE positions still to fill (Budgeted - Filled). Must calculate. | NumberOfVacancies | CALCULATE: Budgeted - Hired | MUST CALCULATE |
| Remaining Headcount | Positions still available (Maximum - Hired). Must calculate. | NumberOfVacancies | CALCULATE: NumberOfVacancies - HiredCount | MUST CALCULATE |
| Target Start Date | Contains the target start date for individuals who are hired for this opportunity. | BeginningDate | [P-RequestMotive_Date1] | MAPPED |

---

## Opportunity - Recruiter

**Talentsoft Equivalent:** Vacancy (Offer)
**Field Count:** 19

> **CORRECTED 2025-11-23:** Recruiter fields must use O- prefix (MainSupervisor), NOT A- prefix

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Email Address  | Contains the recruiter's email address. | OperationalManagerEmail | **[O-MainSupervisorEmail]** | MAPPED |
| First Name  | Contains the recruiter's first name. | OperationalManagerFirstName | **[O-MainSupervisorFirstName]** | MAPPED |
| Preferred Name  | Contains the recruiter's preferred name. | OperationalManager* | [O-...] | MAPPED |
| Last Name  | Contains the recruiter's last name. | OperationalManagerName | **[O-MainSupervisorName]** | MAPPED |
| Middle Name  | Contains the recruiter's middle name. | OperationalManager* | [O-...] | MAPPED |
| Primary Phone  | Contains the recruiter's unformatted primary phone number. | OperationalManagerPhoneNumber | **[O-MainSupervisorPhoneNumber]** | MAPPED |
| Recruiter  | Contains the recruiter's concatenated name, including their title, if any. | BackOfficeUser | [O-...] | MAPPED |
| Recruiter  | Contains the name of the opportunity recruiter (concatenated) that had the change made to, Format is | BackOfficeUser | [O-...] | MAPPED |
| Secondary Phone  | Contains the recruiter's unformatted secondary phone number. | OperationalManagerPhoneNumber | **[O-MainSupervisorPhoneNumber]** | MAPPED |
| Suffix  | Contains the recruiter's name suffix (e.g. Jr.). | OperationalManager* | [O-...] | NOT AVAILABLE |
| Title  | Contains the recruiter's title. | OperationalManager* | [A-Civility] / [A-Title] | NOT AVAILABLE |
| Recruiter  | Contains the name of the recruiter associated to the opportunity.   | BackOfficeUser | [O-...] | MAPPED |
| Recruiter  | Contains the name of the recruiter (concatenated) that had the change made to, Format is Last, Suffi | BackOfficeUser | [O-...] | MAPPED |
| Application Recruiter Elected Not To Answer | Indicates if the recruiter declined to answer the question for the candidate. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Created By  | Contains the unique identifier for an application created in the User Dimension table.  | CreationDate | [O-...] | MAPPED |
| Application Deleted By  | Contains the unique identifier for an application deleted in the User Dimension table.  | OfferStatus | [O-...] | SYSTEM |
| Deleted By Key  | Contains the unique identifier for an opportunity deleted in the User Dimension table.  | OfferStatus | [O-...] | SYSTEM |
| Recruiter Key  | Contains the unique identifier for a recruiter in the Fact table. Can be use to join to Recruiter Di | CustomField | [O-...] | MAPPED |
| Recruiter Key  | Contains the unique identifier for a recruiter in the Dimension table. Can be use to join to Fact ta | CustomField | [O-...] | MAPPED |

---

## Opportunity - Screening

**Talentsoft Equivalent:** Vacancy (Offer) - Questions  
**Field Count:** 22

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Answer Choice | Contains the given answer for a multiple choice question. | JobApplicationQuestion | [O-QuestionCollection] / API | MAPPED (Reference) |
| Correct Answer | Indicates if the answer is a noted as a correct answer.  Only applies multiple choice questions. | JobApplicationQuestion | [O-QuestionCollection] / API | MAPPED (Reference) |
| Disqualifying Answer | Indicates if the answer is a noted as a disqualifying answer.  Only applies multiple choice and numb | JobApplicationQuestion | [O-QuestionCollection] / API | MAPPED (Reference) |
| Answer Type | Contains the type of answer the question requires:  Multiple Choice, Text Field, or Number Range | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Question | Contains the question associated to the opportunity. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Disqualify | Indicates if the candidate supplies disqualifying answer, they will be disqualified from the opportu | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Library Question | Indicates if the question was pulled from the Question Library. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Maximum | Contains the maximum value for a number range question. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Minimum | Contains the minimum value for a number range question. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Points | Contains the score, if any, for the question. | JobApplicationQuestion | [O-QuestionCollection] / API | MAPPED (Reference) |
| Question Position | Contains the position the question appears in the list of opportunity screening questions. | JobApplicationQuestion | [O-QuestionCollection] / API | MAPPED (Reference) |
| Request Candidate Availability | Indicates if the recruiter should request the candidate's availability. | JobApplicationQuestion | [P-...] | MAPPED (Reference) |
| Application Answer  | Contains the answer provided.  This field includes the answer for all question types. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Answer  | Contains only the answers for multiple choice style questions. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Answer  | Contains only the answers for number range style questions. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Answer  | Contains only the answers for text field style questions. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Answer Type | Contains the type of answer the question requires:  Multiple Choice, Text Field, or Number Range | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Candidate Score | Contains the score the candidate earned for answering the question. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Correct Answer | Indicates if the answer is a noted as a correct answer.  Only applies multiple choice and number ran | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Disqualifying Answer | Indicates if the answer is noted as a disqualifying answer.  Only applies multiple choice and number | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Question Score | Contains the maximum score a candidate can earn for answering the question. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |
| Application Screening Question | Contains the question answered on the application. | JobApplicationQuestion | [O-...] | MAPPED (Reference) |

---

## Opportunity - Supervisor

**Talentsoft Equivalent:** Vacancy (Offer)
**Field Count:** 15

> **CORRECTED 2025-11-23:** Supervisor fields must use O- prefix (MainSupervisor), NOT A- prefix

| UKG Field | Definition | TS Field | WordPlus Tag | Gap Status |
|-----------|------------|----------|--------------|------------|
| Email Address  | Contains the Supervisor's email address. | OperationalManagerEmail | **[O-MainSupervisorEmail]** | MAPPED |
| First Name  | Contains the first name for the Supervisor associated to the opportunity. | OperationalManagerFirstName | **[O-MainSupervisorFirstName]** | MAPPED |
| Preferred Name  | Contains the preferred name for the Supervisor associated to the opportunity. | OperationalManager* | [O-...] | MAPPED |
| Last Name  | Contains the last name for the Supervisor associated to the opportunity. | OperationalManagerName | **[O-MainSupervisorName]** | MAPPED |
| Middle Name  | Contains the middle name for the Supervisor associated to the opportunity. | OperationalManager* | [O-...] | MAPPED |
| Opportunity Supervisor  | Contains the Supervisor's concatenated name, including their title, if any. | OperationalManager* | [O-...] | MAPPED |
| Opportunity Supervisor  | Contains the name of the opportunity supervisor (concatenated) that had the change made to, Format i | OperationalManager* | [O-...] | MAPPED |
| Primary Phone  | Contains the primary phone number for the Supervisor associated to the opportunity. | OperationalManagerPhoneNumber | **[O-MainSupervisorPhoneNumber]** | MAPPED |
| Secondary Phone  | Contains the secondary phone number for the Supervisor associated to the opportunity. | OperationalManagerPhoneNumber | **[O-MainSupervisorPhoneNumber]** | MAPPED |
| Suffix  | Contains the suffix for the Supervisor associated to the opportunity. | OperationalManager* | [O-...] | NOT AVAILABLE |
| Title  | Contains the salutation (e.g. Mr., Mrs. Dr., etc.) for the Supervisor associated to the opportunity. | OperationalManager* | [A-Civility] / [A-Title] | NOT AVAILABLE |
| Supervisor | Contains the concatenated name of the Supervisor using the format: Last Suffix, First MI. | OperationalManager* | [O-...] | MAPPED |
| Supervisor  | Contains the concatenated name of the Supervisor using the format: First MI Last  Suffix. | OperationalManager* | [O-...] | MAPPED |
| Supervisor  | Contains the name of the supervisor (concatenated) that had the change made to, Format is Preferred  | OperationalManager* | [O-...] | MAPPED |
| Supervisor Visibility | Indicates which job boards (Internal, External, All, None) will show the supervisor name. | OperationalManager* | [O-...] | MAPPED |

---

## Calculated Fields - Formulas

These fields must be calculated in your BI tool (Power BI, Tableau, etc.):

### FTE/Headcount Calculations



### Days-to-Hire Metrics



---

## SDD File Reference

| SDD File | Purpose | Key Fields |
|----------|---------|------------|
| SDD_VACANCIES.csv | Vacancy/Offer data | Offer_Reference_, JobTitle, Entity, Status |
| SDD_APPLICATION.csv | Application data | Applicant link, Status, Offer reference |
| SDD_APPLICATION_EVENTS.csv | Application timeline | Event dates and types |
| SDD_VACANCY_REQUESTS_LIST.csv | Pre-approval requests | Request data, approval status |
| SDD_VACANCY_REQUESTS_EVENTS.csv | Request timeline | Event dates |
| SDD_VACANCY_REQUESTS_VALIDATION.csv | Approval workflow | Validators, decisions |

---

## Migration Notes

### Fields Requiring Action

| Field | Action Required |
|-------|-----------------|
| Filled FTE | Build BI calculation from event dates or application counts. |
| Incumbent Name  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Last Day Worked | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Remaining FTE | Build BI calculation from event dates or application counts. |
| Remaining Headcount | Build BI calculation from event dates or application counts. |
| Title  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Suffix  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Title  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Suffix  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Suffix  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Title  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Suffix  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Title  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Months To Renewal  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Days Between Accept and Offer Dates | Build BI calculation from event dates or application counts. |
| Days Between Accept and Start Dates | Build BI calculation from event dates or application counts. |
| Days Between Hire and Publish Dates | Build BI calculation from event dates or application counts. |
| Days Between Offer and Start Dates | Build BI calculation from event dates or application counts. |
| Days Between Start and Publish Dates | Build BI calculation from event dates or application counts. |
| Months To Renewal | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Months To Renewal  | Data will be LOST - no Talentsoft equivalent. Consider archiving or custom field |
| Days Between Accept and Offer Dates | Build BI calculation from event dates or application counts. |
| Days Between Accept and Start Dates | Build BI calculation from event dates or application counts. |
| Days Between Hire and Publish Dates | Build BI calculation from event dates or application counts. |
| Days Between Offer and Start Dates | Build BI calculation from event dates or application counts. |
| Days Between Start and Publish Dates | Build BI calculation from event dates or application counts. |

---

*Generated: 2025-11-22*  
*Source: UKG Talent Acquisition Package + GEODIS Talentsoft Configuration*
