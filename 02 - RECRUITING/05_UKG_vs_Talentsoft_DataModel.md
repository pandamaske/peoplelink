# UKG vs Talentsoft Recruitment Data Model Comparison

## Overview

| Aspect | UKG (UltiPro) | Talentsoft |
|--------|---------------|------------|
| **Architecture** | Star schema for BI/Reporting | Normalized relational + API |
| **Total Fields** | 594 (in Tableau1) | 234 API schemas, 172+ CSV entities |
| **Main Entities** | Opportunities, Candidates | Offer (Vacancy), Applicant (Candidate) |
| **Multilingual** | Single language per field | Full i18n (Translation tables) |
| **Custom Fields** | Limited visibility | 4 custom blocks per entity |

---

## Entity Mapping

| Concept | UKG Entity | Talentsoft Entity |
|---------|------------|-------------------|
| Job Requisition | **Opportunity** (372 fields) | **Offer** (40 fields + translations) |
| Candidate Profile | **Candidate** (222 fields) | **Applicant** (33 fields + custom) |
| Application | Opportunities.Applications | **JobApplicationEvent** |
| Hiring Manager | Recruiting Process Details | OperationalManager (embedded in Offer) |
| Organization | Company Information | **Entity** (hierarchical) |
| Workflow Events | System Fields | **OfferEvent**, **ApplicantEvent** |

---

## Detailed Field Comparison

### Job/Vacancy (Opportunity vs Offer)

| Data Category | UKG Fields | Talentsoft Fields |
|---------------|------------|-------------------|
| **Basic Info** | Opportunity Title, Requisition Number | OfferReference, JobTitle |
| **Description** | Detailed Description, Short Description | Description1 (Mission), Description2 (Profil) |
| **Status** | Opportunity Status | OfferStatus (via referential) |
| **Compensation** | Rate, Salary Or Hourly, Rate Visibility | SalaryRange (referential) |
| **Work Type** | Full-Time Or Part-Time, Hours Per Week | JobTime (referential), Contract |
| **Location** | City, State, Country, Tax Location | JobLocation, OfferLocation (+ Country) |
| **Organization** | Company, Org Level 1-4, Location | Entity (hierarchical) |
| **Headcount** | Budgeted FTE, Maximum Headcount, Remaining | NumberOfVacancies |
| **Hiring Manager** | First Name, Last Name, Email, Phone | OperationalManager* (4 fields) |
| **Job Classification** | EEO Category, Job Family | PrimaryProfile, EEOCode, ProfessionalCategory |
| **Criteria** | N/A | Diploma, ExperienceLevel, EducationLevel, Skills |
| **Publishing** | Internal/External visibility | Publication table (support, dates, status) |

**Key Differences:**
- UKG has richer FTE/headcount tracking (Budgeted, Filled, Remaining)
- Talentsoft has structured candidate criteria (Diploma, Experience Level)
- Talentsoft separates publication to job boards as distinct entity

---

### Candidate (Candidate vs Applicant)

| Data Category | UKG Fields | Talentsoft Fields |
|---------------|------------|-------------------|
| **Identity** | First/Last/Middle Name, Suffix, Title | Name, FirstName, MiddleName, Title |
| **Contact** | Email, Primary/Secondary Phone | Email, PhoneNumber1, PhoneNumber2 |
| **Address** | Address 1/2, City, State, Country, Zip | Address, PostalCode, City, ResidenceCountry |
| **Demographics** | (via Applications) | Sex, BirthDate, Race, Ethnicity |
| **Status** | Active/Inactive | ApplicantStatus |
| **Consent** | Consent Status/Version | (via API: consents array) |
| **Internal Flag** | Internal/External | EmployeeCode (link to employee) |
| **Experience** | Candidate Work Experience Details | ApplicantExperience + ExperienceLevel |
| **Education** | Candidate Education Details | (via API: educations array) |
| **Skills** | (via Applications) | PrimaryProfile |
| **Disability** | N/A | VeteranStatus, IncapacityStatus, FrenchDisabledWorkerStatus |
| **Referral** | Employee Referral | RecommendedBy1, RecommendedBy2 |

**Key Differences:**
- Talentsoft has French-specific fields (FrenchDisabledWorkerStatus, FrenchPriorityNeighbourhood)
- UKG embeds candidate details within Applications context
- Talentsoft separates experience as linked entity

---

### Application/Hiring Process

| Data Category | UKG Fields | Talentsoft Fields |
|---------------|------------|-------------------|
| **Application ID** | (embedded in path) | ApplicantCode + OfferReference + Entity |
| **Date Applied** | Date Applied | CreationDate, Date (EventDate) |
| **Source** | Application Internal/External | PublicationSupport, Site |
| **Status** | (via disposition) | JobApplicationStatus |
| **Event Type** | N/A | JobApplicationChildEventType |
| **Motivation** | N/A | Motivation field |
| **Deadline** | N/A | DeadlineDate |

**Hiring Metrics (UKG-specific):**
- Days Between Accept and Offer Dates
- Days Between Accept and Start Dates
- Days Between Hire and Publish Dates
- Days Between Offer and Start Dates

**Talentsoft Events:**
- Structured event types via `ApplicantEvent`, `OfferEvent`
- Publication workflow tracking

---

## Referential/Lookup Tables

| UKG Approach | Talentsoft Approach |
|--------------|---------------------|
| Embedded descriptions in paths | 98+ separate referential tables |
| Limited lookup customization | Full mapping tables (`mapref*`) |
| Single language | Translation tables for each ref |

**Talentsoft Referentials include:**
- Country, Region, Department
- Contract, JobTime, SalaryRange
- Diploma, EducationLevel, ExperienceLevel
- Profile (Job Family), Specialisation
- PublicationSupport (job boards)
- ApplicantEventType, OfferEventType
- Custom code tables

---

## Architecture Differences

```
UKG (Star Schema for Reporting)
================================
[Presentation Layer]
    └── [Unified Reporting - Talent Acquisition]
            ├── [Opportunities] ─────────┐
            │       ├── Opening Info     │
            │       ├── Company Info     ├── Denormalized
            │       ├── Compensation     │   for BI
            │       ├── Applications ────┤
            │       │     ├── Hire Details
            │       │     ├── Screening
            │       │     └── Education/Experience
            │       └── ...              │
            └── [Candidates] ────────────┘
                    ├── Candidate Details
                    └── Applications (same structure)

Talentsoft (Normalized Relational + API)
=========================================
┌─────────────┐     ┌─────────────────┐
│   Offer     │────→│   Publication   │
│  (Vacancy)  │     └─────────────────┘
└──────┬──────┘
       │ FK          ┌─────────────────┐
       └────────────→│    Entity       │ (Organization)
                     └─────────────────┘
┌─────────────┐     ┌─────────────────┐
│  Applicant  │────→│ ApplicantEvent  │
│ (Candidate) │     └─────────────────┘
└──────┬──────┘
       │            ┌─────────────────┐
       ├───────────→│  Experience     │
       │            └─────────────────┘
       │            ┌─────────────────┐
       └───────────→│ CustomFields    │ (4 blocks)
                    └─────────────────┘

+ 98 Referential tables with translations
```

---

## Summary: Migration Considerations

| Challenge | Notes |
|-----------|-------|
| **Flattening vs Normalization** | UKG is denormalized for reporting; Talentsoft requires joins |
| **Multilingual** | Talentsoft requires translation table management |
| **Custom Fields** | Map UKG custom fields to Talentsoft's 4 custom blocks |
| **FTE Tracking** | UKG has richer headcount/FTE; may need custom fields in Talentsoft |
| **Hiring Metrics** | UKG calculates days-between metrics; Talentsoft needs computation |
| **French Specifics** | Talentsoft has built-in French labor law fields |
| **Event Tracking** | Different event models - mapping required |

---

## Talentsoft File Structure (from extractions)

### Core Entities
- `applicant.csv` - Candidate profiles (33 fields)
- `offer.csv` - Job vacancies (40 fields)
- `publication.csv` - Job board publications (8 fields)

### Events
- `applicantevent.csv` - Candidate workflow events
- `offerevent.csv` - Vacancy lifecycle events

### Related Data
- `applicantexperience.csv` - Work history
- `experience.csv` - Experience definitions
- `entity.csv` - Organizations
- `backofficeuser.csv` - Recruiters/Users

### Referentials (98 files)
- `mapref*.csv` - Mapping tables for all lookups
- `ref*.csv` - Reference value tables with translations
