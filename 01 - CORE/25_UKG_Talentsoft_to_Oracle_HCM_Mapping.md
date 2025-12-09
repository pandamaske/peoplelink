# UKG & Talentsoft to Oracle HCM Cloud - Field Mapping & Gap Analysis

**Project:** GEODIS New HCM - AMARIS
**Document Type:** Data Model Mapping & Gap Analysis
**Version:** 1.4
**Date:** 2025-12-07
**Status:** Draft

---

## Executive Summary

This document provides a comprehensive field-level mapping from two source systems (UKG for US operations and Talentsoft/G-Talent+ for global) to Oracle HCM Cloud. It identifies Core HR fields, LDG-specific (Legislative Data Group) fields, and Payroll-specific fields, along with gaps that require resolution.

| Source System | Total Fields | Core HR | LDG/Country | Payroll | Gaps |
|---------------|--------------|---------|-------------|---------|------|
| **UKG** | 1,617 | 180 | 420 | 850 | 47 |
| **Talentsoft** | 427 | 285 | 45 | 35 | 28 |

---

## Table of Contents

1. [Source System Overview](#1-source-system-overview)
2. [Oracle HCM Target Data Model](#2-oracle-hcm-target-data-model)
3. [UKG to Oracle HCM Mapping](#3-ukg-to-oracle-hcm-mapping)
4. [Talentsoft to Oracle HCM Mapping](#4-talentsoft-to-oracle-hcm-mapping)
5. [Gap Analysis](#5-gap-analysis)
6. [Recommendations](#6-recommendations)
7. [Repository Sheets Reference](#7-repository-sheets-reference)

---

## 1. Source System Overview

### 1.1 UKG (US Operations)

**File:** `Employee Information Package.xls`
**Total Fields:** 1,617
**Region:** United States
**Primary Use:** HR, Payroll, Time & Attendance, Benefits

**Field Categories:**

| Category | Field Count | Scope |
|----------|-------------|-------|
| Employee Demographics | ~150 | Core HR |
| Employment Information | ~200 | Core HR |
| Job & Organization | ~100 | Core HR |
| Compensation & Salary | ~180 | Payroll |
| Benefits & Accruals | ~350 | Payroll/LDG |
| Time & Attendance | ~250 | LDG (US) |
| Leave Management | ~150 | LDG (US) |
| Supervisor Information | ~80 | Core HR |
| Compliance (I-9, EEO) | ~80 | LDG (US) |
| User-Defined Fields | ~77 | Custom |

**Key Tables Identified:**
- `fn_BI_EmpPers` - Personal Information
- `fn_BI_EmpComp` - Compensation/Employment
- `fn_BI_Company` - Company/Legal Entity
- `fn_BI_SupervisorInfo` - Manager Information
- `JobCode` - Job Catalog
- `Location` - Work Locations
- `OrgLevel` - Organization Hierarchy
- `EmpHStat` - Employment Status History
- `PayrollPendingItemAccruals` - Payroll Accruals
- `intUTAPRInfo` - Time & Attendance

### 1.2 Talentsoft / G-Talent+ (Global)

**File:** `Employee Core HR Data Model.xlsx`
**Total Fields:** 427
**Region:** Global (primarily Europe)
**Primary Use:** Core HR, Talent Management, Compensation

**Field Categories:**

| Category | Field Count | Scope |
|----------|-------------|-------|
| Personal Identity | 45 | Core HR |
| Address Information | 35 | Core HR |
| Employment Dates | 20 | Core HR |
| Job & Position | 25 | Core HR |
| Organization Structure | 30 | Core HR |
| Compensation | 25 | Core HR |
| Bank Details | 40 | LDG/Payroll |
| Manager Relationships | 15 | Core HR |
| Contract Details | 35 | Core HR |
| Government IDs | 15 | LDG |
| Medical/Disability | 25 | LDG |
| Family Information | 15 | Core HR |
| Probation | 10 | Core HR |
| Cost Allocation | 25 | Finance |
| Other | 67 | Various |

**Data Status Column Analysis:**
- LEGACY SOURCE: 201 fields (existing data)
- COREHR: 226 fields (new Core HR structure)
  - DUPLICATE: 85 fields (mapped to legacy)
  - UNIQUE - NEW VALUE: 141 fields (new fields)

**Excel Structure:**
- Single sheet: `Sheet1`
- Fields organized by prefix categories (e.g., `BankDetails - *`, `Contract - *`, `Identity - *`)

**Field Categories by Prefix:**

| Category Prefix | LEGACY | COREHR | Total | Oracle Scope |
|-----------------|--------|--------|-------|--------------|
| PersonalData (no prefix) | 186 | - | 186 | Core HR |
| BankDetails | - | 35 | 35 | LDG/Payroll |
| Contract | - | 25 | 25 | Core HR |
| Relative | - | 22 | 22 | Core HR |
| Situation | - | 17 | 17 | Core HR |
| MainPostalAddress | - | 10 | 10 | Core HR |
| OtherPostalAddress | - | 10 | 10 | Core HR |
| Identity | - | 9 | 9 | Core HR |
| ContactInformation | - | 8 | 8 | Core HR |
| ProbationaryPeriod | - | 8 | 8 | Core HR |
| WorkAccident | - | 8 | 8 | LDG (France) |
| GovernmentID | - | 6 | 6 | LDG |
| MedicalCheckUp | - | 6 | 6 | LDG (France) |
| Qualification | - | 6 | 6 | Core HR |
| CivilRegistration | - | 5 | 5 | Core HR |
| Disability | - | 5 | 5 | LDG |
| FamilyStatus | - | 5 | 5 | Core HR |
| OccupationalDisease | - | 5 | 5 | LDG (France) |
| EmployeeIDs | - | 4 | 4 | Core HR |
| KeyDates | - | 4 | 4 | Core HR |
| MedicalInsurance | - | 4 | 4 | LDG |
| Birth | 3 | - | 3 | Core HR |
| Compensation | - | 3 | 3 | Payroll |
| Competency | - | 3 | 3 | Talent |
| Representative | - | 3 | 3 | LDG (France) |
| Other categories | 12 | 28 | 40 | Various |

---

## 2. Oracle HCM Target Data Model

### 2.1 Core HR Objects

| Oracle Object | Description | Source Mapping |
|---------------|-------------|----------------|
| **PER_ALL_PEOPLE_F** | Person master record | UKG: EmpPers, TS: Identity |
| **PER_PERSON_NAMES_F** | Name components | Both sources |
| **PER_ALL_ASSIGNMENTS_F** | Job assignment | Both sources |
| **PER_PERIODS_OF_SERVICE** | Employment tenure | Both sources |
| **PER_ADDRESSES_F** | Addresses | Both sources |
| **PER_PHONES** | Phone numbers | Both sources |
| **PER_EMAIL_ADDRESSES** | Email addresses | Both sources |
| **PER_NATIONAL_IDENTIFIERS** | SSN, Tax IDs | Both sources |
| **PER_PERSONS_LEGISLATIVE** | LDG-specific data | LDG fields |
| **PER_PERSON_TYPE_USAGES_F** | Person type | Both sources |
| **PER_CONTACT_RELATIONSHIPS** | Emergency contacts | Both sources |
| **PER_DOCUMENTS_OF_RECORD** | Documents | TS: GovernmentID |

### 2.2 Assignment Objects

| Oracle Object | Description | Source Mapping |
|---------------|-------------|----------------|
| **PER_ASSIGNMENT_EXTRA_INFO_F** | Assignment DFF | Custom fields |
| **HR_ALL_ORGANIZATION_UNITS** | Departments | Both sources |
| **PER_JOBS** | Job catalog | Both sources |
| **PER_POSITIONS** | Positions | TS: Job Position |
| **PER_GRADES** | Grade structure | TS: Band |
| **PER_LOCATIONS** | Locations | Both sources |

### 2.3 Compensation Objects (LDG/Payroll)

| Oracle Object | Description | Scope |
|---------------|-------------|-------|
| **CMP_SALARY** | Base salary | Payroll |
| **PAY_ELEMENT_ENTRIES_F** | Pay elements | Payroll |
| **PAY_PERSONAL_PAYMENT_METHODS** | Bank details | Payroll |
| **PAY_PAYROLL_ASSIGNMENTS** | Payroll assignment | Payroll |

### 2.4 GEODIS Confirmed Repository Sources

The following repository sheets in `04 - SHEETS` folder contain the confirmed Oracle HCM configuration data:

#### Organization Structure (Confirmed)

| Oracle Object | Repository Sheet | Records | Status | Key Fields |
|---------------|------------------|---------|--------|------------|
| **Enterprise** | Enterprise HCM.xlsx | 1 | ✅ Confirmed | GEODIS (root) |
| **Division** | Division.xlsx | 19 | ✅ Confirmed | Lines of Business groupings |
| **Legal Entity** | Legal Entity.xlsx | 364 | ✅ Confirmed | Legal employers by country |
| **Business Unit** | Business Unit.xlsx | **2,175** | ✅ Confirmed | Site/Allocation Center level |
| **Department** | Department.xlsx | **10,803** | ✅ Configured | Organizational units |
| **Location** | Location.xlsx | 919 | ✅ Confirmed | Work locations |
| **Legislative Data Group** | Legislative Data Group.xlsx | 62 | ✅ Confirmed | Country payroll groups |

#### Business Unit Detail

| Attribute | Value | Notes |
|-----------|-------|-------|
| Total Records | 2,175 | Cross-validated with BU Set Assignment.xlsx |
| Default Sets | 30 | LoB groupings (CL, FF, DE, RT, SC, TOF, etc.) |
| Unique Locations | 822 | Location references |
| Status | All Active | Ready for Oracle load |

**Default Set Distribution (Top 10):**

| Set Code | Records | Line of Business |
|----------|---------|------------------|
| CLAM | 347 | Contract Logistics Americas |
| CLNIND | 299 | Contract Logistics North India |
| FFAP | 179 | Freight Forwarding Asia Pacific |
| DEFR | 166 | Distribution & Express France |
| RTNPH | 160 | Road Transport Netherlands |
| CLFR | 158 | Contract Logistics France |
| CLNE | 152 | Contract Logistics North Europe |
| TOF | 142 | Transport Operations France |
| FFNE | 130 | Freight Forwarding North Europe |
| FFPF | 94 | Freight Forwarding Pacific |

#### GEODIS Organization Hierarchy

```
Enterprise (1: GEODIS)
    └── Division (19)
        └── Legal Entity (364)
            └── Business Unit (2,175) ← Sites/Allocation Centers
                └── Department (10,803)
                    └── Location (919)
```

#### Workforce Structure (Confirmed)

| Oracle Object | Repository Sheet | Records | Status |
|---------------|------------------|---------|--------|
| **Job** | Job.xlsx | 334 | ✅ Confirmed |
| **Job Family** | Job Family.xlsx | 842 | ✅ Confirmed |
| **Job Sub Family** | Job Sub Family.xlsx | TBD | ✅ Template |
| **Position** | Position.xlsx | TBD | ✅ Template |
| **Grade** | Grade.xlsx | 22 | ✅ Confirmed |

#### Employment & Compensation (Confirmed)

| Oracle Object | Repository Sheet | Records | Status |
|---------------|------------------|---------|--------|
| **Contract Type** | Contract Type.xlsx | TBD | ✅ Template |
| **Assignment Category** | Assignment Category.xlsx | 75 | ✅ Confirmed |
| **Assignment Status** | Assignment Status.xlsx | TBD | ✅ Template |
| **Salary Basis** | Salary Basis.xlsx | 5 | ✅ Confirmed |
| **Compensation Elements** | Comp. Elements.xlsx | 36 | ✅ Confirmed |

---

## 3. UKG to Oracle HCM Mapping

### 3.1 Core HR Fields (Person)

| UKG Field | UKG Table.Column | Oracle Object | Oracle Field | Category |
|-----------|------------------|---------------|--------------|----------|
| Employee Number | fn_BI_EmpComp.EecEmpNo | PER_ALL_PEOPLE_F | PERSON_NUMBER | Core HR |
| SSN (Unformatted) | - | PER_NATIONAL_IDENTIFIERS | NATIONAL_IDENTIFIER_NUMBER | Core HR |
| Employee Name (First MI Last Suffix) | - (calculated) | PER_PERSON_NAMES_F | FIRST_NAME, MIDDLE_NAMES, LAST_NAME | Core HR |
| Preferred First Name | fn_BI_EmpPers.EepNamePreferred | PER_PERSON_NAMES_F | KNOWN_AS | Core HR |
| Email Address | fn_BI_EmpPers.EepAddressEMail | PER_EMAIL_ADDRESSES | EMAIL_ADDRESS | Core HR |
| Alternate Email | fn_BI_EmpPers.eepAddressEMailAlternate | PER_EMAIL_ADDRESSES | EMAIL_ADDRESS (secondary) | Core HR |
| Home Phone | fn_BI_EmpPers.EepPhoneHomeNumber | PER_PHONES | PHONE_NUMBER | Core HR |
| Work Phone | fn_BI_EmpComp.EecPhoneBusinessNumber | PER_PHONES | PHONE_NUMBER | Core HR |
| Work Extension | fn_BI_EmpComp.EecPhoneBusinessExt | PER_PHONES | PHONE_NUMBER (ext) | Core HR |
| Address Line 1 | - | PER_ADDRESSES_F | ADDRESS_LINE_1 | Core HR |
| Address Line 2 | - | PER_ADDRESSES_F | ADDRESS_LINE_2 | Core HR |
| City | - | PER_ADDRESSES_F | TOWN_OR_CITY | Core HR |
| State | fn_BI_EmpPers.EepAddressState | PER_ADDRESSES_F | REGION_1 | Core HR |
| Zip Code | fn_BI_EmpPers.EepAddressZipCode | PER_ADDRESSES_F | POSTAL_CODE | Core HR |
| Country Code | fn_BI_EmpPers.EepAddressCountry | PER_ADDRESSES_F | COUNTRY | Core HR |
| Date Deceased | fn_BI_EmpPers.EepDateDeceased | PER_ALL_PEOPLE_F | DATE_OF_DEATH | Core HR |

### 3.2 Core HR Fields (Employment)

| UKG Field | UKG Table.Column | Oracle Object | Oracle Field | Category |
|-----------|------------------|---------------|--------------|----------|
| Company Code | fn_BI_Company.CmpCompanyCode | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID | Core HR |
| Company | fn_BI_Company.CmpCompanyName | HR_ALL_ORGANIZATION_UNITS | NAME | Core HR |
| Employment Status Code | fn_BI_EmpComp.EecEmplStatus | PER_ALL_ASSIGNMENTS_F | ASSIGNMENT_STATUS_TYPE | Core HR |
| Employment Status | fn_BI_EmpComp.EmplStatusDesc | PER_ALL_ASSIGNMENTS_F | ASSIGNMENT_STATUS_TYPE (lookup) | Core HR |
| Status As Of | fn_BI_EmpComp.EecEmplStatusStartDate | PER_PERIODS_OF_SERVICE | DATE_START | Core HR |
| Employment Type Code | fn_BI_EmpComp.EecEEType | PER_ALL_ASSIGNMENTS_F | EMPLOYMENT_CATEGORY | Core HR |
| Full/Part Time Code | fn_BI_EmpComp.EecFullTimeOrPartTime | PER_ALL_ASSIGNMENTS_F | FULL_PART_TIME | Core HR |
| Original Hire | fn_BI_EmpComp.EecDateOfOriginalHire | PER_PERIODS_OF_SERVICE | DATE_START (original) | Core HR |
| Last Hire | fn_BI_EmpComp.EecDateOfLastHire | PER_PERIODS_OF_SERVICE | DATE_START (current) | Core HR |
| Seniority Date | fn_BI_EmpComp.EecDateOfSeniority | PER_PERIODS_OF_SERVICE | ADJUSTED_SVC_DATE | Core HR |

### 3.3 Core HR Fields (Job & Organization)

| UKG Field | UKG Table.Column | Oracle Object | Oracle Field | Category |
|-----------|------------------|---------------|--------------|----------|
| Job Code | - | PER_JOBS | JOB_ID | Core HR |
| Job | JobCode.JbcDesc | PER_JOBS | NAME | Core HR |
| Job Family Code | - | PER_JOB_FAMILIES | JOB_FAMILY_ID | Core HR |
| Job Family | fn_LocalizeCodesForCognos.codDesc | PER_JOB_FAMILIES | NAME | Core HR |
| Location Code | fn_BI_EmpComp.EecLocation | PER_LOCATIONS | LOCATION_ID | Core HR |
| Location | Location.LocDesc | PER_LOCATIONS | LOCATION_NAME | Core HR |
| Org Level 1 Code | - | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID (L1) | Core HR |
| Org Level 2 Code | - | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID (L2) | Core HR |
| Org Level 3 Code | - | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID (L3) | Core HR |
| Org Level 4 Code | - | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID (L4) | Core HR |

### 3.4 Core HR Fields (Manager)

| UKG Field | UKG Table.Column | Oracle Object | Oracle Field | Category |
|-----------|------------------|---------------|--------------|----------|
| Supervisor Employee Number | fn_BI_SupervisorInfo.EecEmpNo | PER_ALL_ASSIGNMENTS_F | MANAGER_ID | Core HR |
| Supervisor Email Address | fn_BI_SupervisorInfo.EepAddressEMail | - | (lookup) | Core HR |
| Supervisor First Name | fn_BI_SupervisorInfo.EepNameFirst | - | (lookup) | Core HR |
| Supervisor Last Name | fn_BI_SupervisorInfo.EepNameLast | - | (lookup) | Core HR |

### 3.5 LDG-Specific Fields (US)

| UKG Field | UKG Table.Column | Oracle Object | Oracle Field | LDG |
|-----------|------------------|---------------|--------------|-----|
| SIN | EmpIntl.einNationalID | PER_NATIONAL_IDENTIFIERS | NATIONAL_IDENTIFIER_NUMBER | US |
| SIN Expiration Date | EmpIntl.einNationalIDExpireDate | PER_NATIONAL_IDENTIFIERS | (DFF) | US |
| EEO Establishment Name | -.UnitName | PER_LEGISLATIVE_DATA | (DFF) | US |
| EEO Establishment Unit Number | -.UnitNumber | PER_LEGISLATIVE_DATA | (DFF) | US |
| FMLA Qualified | fn_BI_EmpComp.CurrentLeaveFMLAQualified | HWM_ABS_REQUEST | (DFF) | US |
| Leave Type Code | fn_BI_EmpComp.CurrentLeaveType | HWM_ABS_TYPES | ABSENCE_TYPE_ID | US |
| Hire Source Code | - | PER_ALL_PEOPLE_F | (DFF) | US |

### 3.6 Payroll-Specific Fields

| UKG Field | UKG Table.Column | Oracle Object | Oracle Field | Category |
|-----------|------------------|---------------|--------------|----------|
| Pay Group Code | - | PAY_PAYROLL_ASSIGNMENTS | PAYROLL_ID | Payroll |
| Paid Automatically | fn_BI_EmpComp.EecIsAutopaid | PAY_PAYROLL_ASSIGNMENTS | (DFF) | Payroll |
| Accrual Code | PayrollPendingItemAccruals.Code | HWM_ACCRUAL_PLANS | PLAN_ID | Payroll |
| Balance | PayrollPendingItemAccruals.Balance | HWM_ACCRUAL_BALANCES | BALANCE | Payroll |
| Arrears - Suspend From | fn_BI_EmpComp.EecArrearsSuspFromDate | PAY_ELEMENT_ENTRIES_F | (DFF) | Payroll |
| PTO Benefits - Suspend From | fn_BI_EmpComp.EecAccrSuspTimePdFromDate | HWM_ACCRUAL_BALANCES | (DFF) | Payroll |

### 3.7 Time & Attendance Fields (LDG - US)

| UKG Field | UKG Table.Column | Oracle Object | Oracle Field | Category |
|-----------|------------------|---------------|--------------|----------|
| Badge Number | intUTAPRInfo.iupBadgeNumber | - | Custom/Integration | T&A |
| Calc Group | intUTACodes.iucUTADesc | - | Custom/Integration | T&A |
| Shift Pattern | intUTAPRInfo.iupShiftPattern | PER_ALL_ASSIGNMENTS_F | (DFF) | T&A |
| Time Zone | intUTAPRInfo.iupTimeZone | PER_ALL_ASSIGNMENTS_F | (DFF) | T&A |
| Day Start Time | intUTAPRInfo.iupDayStartTime | - | Custom/Integration | T&A |

---

## 4. Talentsoft to Oracle HCM Mapping

> **Note:** Source file has single sheet `Sheet1`. Fields are categorized by prefix (e.g., `Identity - *`, `Contract - *`).
> Legacy fields without prefix are grouped as "PersonalData".

### 4.1 Core HR Fields (Person - Identity)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| ID / GEODIS ID | PersonalData | LEGACY | PER_ALL_PEOPLE_F | PERSON_NUMBER | Core HR | Person Identifier Type for Ext.xlsx |
| EmployeeIDs - UniqueID | EmployeeIDs | COREHR | PER_ALL_PEOPLE_F | PERSON_NUMBER | Core HR | Person Identifier Type for Ext.xlsx |
| EmployeeIDs - Username | EmployeeIDs | COREHR | PER_ALL_PEOPLE_F | (DFF) | Core HR | - |
| EmployeeIDs - CandidateId | EmployeeIDs | COREHR | PER_ALL_PEOPLE_F | (DFF) | Core HR | - |
| EmployeeIDs - LegacyID | EmployeeIDs | COREHR | PER_ALL_PEOPLE_F | (DFF) | Core HR | - |
| Surname | PersonalData | LEGACY | PER_PERSON_NAMES_F | LAST_NAME | Core HR | Name Styles.xlsx |
| First name | PersonalData | LEGACY | PER_PERSON_NAMES_F | FIRST_NAME | Core HR | Name Styles.xlsx |
| Middle name | PersonalData | LEGACY | PER_PERSON_NAMES_F | MIDDLE_NAMES | Core HR | Name Styles.xlsx |
| Nick name | PersonalData | LEGACY | PER_PERSON_NAMES_F | KNOWN_AS | Core HR | Name Styles.xlsx |
| Maiden name | PersonalData | LEGACY | PER_PERSON_NAMES_F | PREVIOUS_LAST_NAME | Core HR | Name Styles.xlsx |
| Common name | PersonalData | LEGACY | PER_PERSON_NAMES_F | (DFF) | Core HR | - |
| Affix | PersonalData | LEGACY | PER_PERSON_NAMES_F | SUFFIX | Core HR | Name Styles.xlsx |
| Title | PersonalData | LEGACY | PER_PERSON_NAMES_F | TITLE | Core HR | Titles.xlsx |
| Identity - FirstName | Identity | COREHR | PER_PERSON_NAMES_F | FIRST_NAME | Core HR | Name Styles.xlsx |
| Identity - LastName | Identity | COREHR | PER_PERSON_NAMES_F | LAST_NAME | Core HR | Name Styles.xlsx |
| Identity - BirthName | Identity | COREHR | PER_PERSON_NAMES_F | PREVIOUS_LAST_NAME | Core HR | Name Styles.xlsx |
| Identity - FirstNameSecond | Identity | COREHR | PER_PERSON_NAMES_F | MIDDLE_NAMES | Core HR | Name Styles.xlsx |
| Identity - FirstNameThird | Identity | COREHR | PER_PERSON_NAMES_F | (DFF) | Core HR | - |
| Identity - NickName | Identity | COREHR | PER_PERSON_NAMES_F | KNOWN_AS | Core HR | Name Styles.xlsx |
| Identity - NationalityTwo | Identity | COREHR | PER_CITIZENSHIPS | CITIZENSHIP_STATUS | Core HR | Citizenship Status.xlsx |
| Identity - OtherFirstNames | Identity | COREHR | PER_PERSON_NAMES_F | (DFF) | Core HR | - |
| Identity - OtherLastNames | Identity | COREHR | PER_PERSON_NAMES_F | (DFF) | Core HR | - |
| Gender | PersonalData | LEGACY | PER_ALL_PEOPLE_F | SEX | Core HR | Gender.xlsx |
| Date of birth | PersonalData | LEGACY | PER_ALL_PEOPLE_F | DATE_OF_BIRTH | Core HR | - |
| Marital status | PersonalData | LEGACY | PER_ALL_PEOPLE_F | MARITAL_STATUS | Core HR | Marital Statuses.xlsx |
| FamilyStatus - MaritalStatus | FamilyStatus | COREHR | PER_ALL_PEOPLE_F | MARITAL_STATUS | Core HR | Marital Statuses.xlsx |
| FamilyStatus - NumberOfChildren | FamilyStatus | COREHR | PER_ALL_PEOPLE_F | (DFF) | Core HR | Statutory Dependent.xlsx |
| FamilyStatus - NumberOfDependents | FamilyStatus | COREHR | PER_ALL_PEOPLE_F | (DFF) | Core HR | Statutory Dependent.xlsx |
| FamilyStatus - NumberOfDependentChildren | FamilyStatus | COREHR | PER_ALL_PEOPLE_F | (DFF) | Core HR | Statutory Dependent.xlsx |
| Number of children | PersonalData | LEGACY | PER_ALL_PEOPLE_F | (DFF) | Core HR | Statutory Dependent.xlsx |
| Nationality | PersonalData | LEGACY | PER_CITIZENSHIPS | CITIZENSHIP_STATUS | Core HR | Citizenship Status.xlsx |
| Second nationality | PersonalData | LEGACY | PER_CITIZENSHIPS | CITIZENSHIP_STATUS (2) | Core HR | Citizenship Status.xlsx |

### 4.2 Core HR Fields (Address)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| House number | PersonalData | LEGACY | PER_ADDRESSES_F | (part of ADDRESS_LINE_1) | Core HR | Address Format.xlsx |
| House number suffix | PersonalData | LEGACY | PER_ADDRESSES_F | (part of ADDRESS_LINE_1) | Core HR | Address Format.xlsx |
| Street type | PersonalData | LEGACY | PER_ADDRESSES_F | (part of ADDRESS_LINE_1) | Core HR | Address Format.xlsx |
| Street name | PersonalData | LEGACY | PER_ADDRESSES_F | ADDRESS_LINE_1 | Core HR | Address Format.xlsx |
| Additional information | PersonalData | LEGACY | PER_ADDRESSES_F | ADDRESS_LINE_2 | Core HR | Address Format.xlsx |
| Personal - Zip Code | Personal | LEGACY | PER_ADDRESSES_F | POSTAL_CODE | Core HR | Address Format.xlsx |
| Personal - City | Personal | LEGACY | PER_ADDRESSES_F | TOWN_OR_CITY | Core HR | Address Format.xlsx |
| Personal - Area State | Personal | LEGACY | PER_ADDRESSES_F | REGION_1 | Core HR | Geography.xlsx |
| Personal - Country | Personal | LEGACY | PER_ADDRESSES_F | COUNTRY | Core HR | Country Code.xlsx |
| MainPostalAddress - Street | MainPostalAddress | COREHR | PER_ADDRESSES_F | ADDRESS_LINE_1 | Core HR | Address Format.xlsx |
| MainPostalAddress - StreetNumber | MainPostalAddress | COREHR | PER_ADDRESSES_F | (part of ADDRESS_LINE_1) | Core HR | Address Format.xlsx |
| MainPostalAddress - StreetType | MainPostalAddress | COREHR | PER_ADDRESSES_F | (part of ADDRESS_LINE_1) | Core HR | Address Format.xlsx |
| MainPostalAddress - StreetNumberComplement | MainPostalAddress | COREHR | PER_ADDRESSES_F | (part of ADDRESS_LINE_1) | Core HR | Address Format.xlsx |
| MainPostalAddress - AdditionalAddressInformation | MainPostalAddress | COREHR | PER_ADDRESSES_F | ADDRESS_LINE_2 | Core HR | Address Format.xlsx |
| MainPostalAddress - AdditionalDeliveryInstructions | MainPostalAddress | COREHR | PER_ADDRESSES_F | ADDRESS_LINE_3 | Core HR | Address Format.xlsx |
| MainPostalAddress - PostalCode | MainPostalAddress | COREHR | PER_ADDRESSES_F | POSTAL_CODE | Core HR | Address Format.xlsx |
| MainPostalAddress - TownOrCity | MainPostalAddress | COREHR | PER_ADDRESSES_F | TOWN_OR_CITY | Core HR | Address Format.xlsx |
| MainPostalAddress - AreaOrState | MainPostalAddress | COREHR | PER_ADDRESSES_F | REGION_1 | Core HR | Geography.xlsx |
| MainPostalAddress - Country | MainPostalAddress | COREHR | PER_ADDRESSES_F | COUNTRY | Core HR | Country Code.xlsx |
| OtherPostalAddress - Street | OtherPostalAddress | COREHR | PER_ADDRESSES_F | ADDRESS_LINE_1 (secondary) | Core HR | Address Type.xlsx |
| OtherPostalAddress - PostalCode | OtherPostalAddress | COREHR | PER_ADDRESSES_F | POSTAL_CODE (secondary) | Core HR | Address Type.xlsx |
| OtherPostalAddress - TownOrCity | OtherPostalAddress | COREHR | PER_ADDRESSES_F | TOWN_OR_CITY (secondary) | Core HR | Address Type.xlsx |
| OtherPostalAddress - Country | OtherPostalAddress | COREHR | PER_ADDRESSES_F | COUNTRY (secondary) | Core HR | Country Code.xlsx |
| Birth - Country | Birth | LEGACY | PER_ALL_PEOPLE_F | COUNTRY_OF_BIRTH | Core HR | Country Code.xlsx |
| Birth - Town/city | Birth | LEGACY | PER_ALL_PEOPLE_F | TOWN_OF_BIRTH | Core HR | Geography.xlsx |
| Birth - Postcode | Birth | LEGACY | PER_ALL_PEOPLE_F | (DFF) | Core HR | - |
| CivilRegistration - Country | CivilRegistration | COREHR | PER_ALL_PEOPLE_F | COUNTRY_OF_BIRTH | Core HR | Country Code.xlsx |
| CivilRegistration - TownOrCity | CivilRegistration | COREHR | PER_ALL_PEOPLE_F | TOWN_OF_BIRTH | Core HR | Geography.xlsx |
| CivilRegistration - PostalCode | CivilRegistration | COREHR | PER_ALL_PEOPLE_F | (DFF) | Core HR | - |
| CivilRegistration - AreaOrState | CivilRegistration | COREHR | PER_ALL_PEOPLE_F | REGION_OF_BIRTH | Core HR | Geography.xlsx |
| CivilRegistration - DateOfBirth | CivilRegistration | COREHR | PER_ALL_PEOPLE_F | DATE_OF_BIRTH | Core HR | - |

### 4.3 Core HR Fields (Contact)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| Email | PersonalData | LEGACY | PER_EMAIL_ADDRESSES | EMAIL_ADDRESS (WORK) | Core HR | E-Mail Type.xlsx |
| Personal Email | PersonalData | LEGACY | PER_EMAIL_ADDRESSES | EMAIL_ADDRESS (PERSONAL) | Core HR | E-Mail Type.xlsx |
| Phone number | PersonalData | LEGACY | PER_PHONES | PHONE_NUMBER (EMERGENCY) | Core HR | Phone Type.xlsx |
| Personal Number | PersonalData | LEGACY | PER_PHONES | PHONE_NUMBER (PERSONAL) | Core HR | Phone Type.xlsx |
| ContactInformation - BusinessEmail | ContactInformation | COREHR | PER_EMAIL_ADDRESSES | EMAIL_ADDRESS (WORK) | Core HR | E-Mail Type.xlsx |
| ContactInformation - PersonalEmail | ContactInformation | COREHR | PER_EMAIL_ADDRESSES | EMAIL_ADDRESS (PERSONAL) | Core HR | E-Mail Type.xlsx |
| ContactInformation - BusinessPhone | ContactInformation | COREHR | PER_PHONES | PHONE_NUMBER (WORK) | Core HR | Phone Type.xlsx |
| ContactInformation - BusinessMobile | ContactInformation | COREHR | PER_PHONES | PHONE_NUMBER (MOBILE) | Core HR | Phone Type.xlsx |
| ContactInformation - PersonalPhone | ContactInformation | COREHR | PER_PHONES | PHONE_NUMBER (PERSONAL) | Core HR | Phone Type.xlsx |
| ContactInformation - PersonalMobile | ContactInformation | COREHR | PER_PHONES | PHONE_NUMBER (PERSONAL MOBILE) | Core HR | Phone Type.xlsx |
| ContactInformation - BusinessFax | ContactInformation | COREHR | PER_PHONES | PHONE_NUMBER (FAX) | Core HR | Phone Type.xlsx |
| ContactInformation - PersonalFax | ContactInformation | COREHR | PER_PHONES | PHONE_NUMBER (PERSONAL FAX) | Core HR | Phone Type.xlsx |
| Emergency contact / or / Next of kin | PersonalData | LEGACY | PER_CONTACT_RELATIONSHIPS | CONTACT_NAME | Core HR | Contact.xlsx |

### 4.4 Core HR Fields (Employment)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| Group Start Date | PersonalData | LEGACY | PER_PERIODS_OF_SERVICE | DATE_START | Core HR | - |
| Company Start Date | PersonalData | LEGACY | PER_PERIODS_OF_SERVICE | DATE_START (LE) | Core HR | - |
| Senority date (recalculated) | PersonalData | LEGACY | PER_PERIODS_OF_SERVICE | ADJUSTED_SVC_DATE | Core HR | Seniority Rules.xlsx |
| Group Exit Date | PersonalData | LEGACY | PER_PERIODS_OF_SERVICE | ACTUAL_TERMINATION_DATE | Core HR | Action & Reasons.xlsx |
| Hiring reason | PersonalData | LEGACY | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | Action & Reasons.xlsx |
| Reason for leaving (Code) | PersonalData | LEGACY | PER_PERIODS_OF_SERVICE | LEAVING_REASON | Core HR | Action & Reasons.xlsx |
| Reason for leaving | PersonalData | LEGACY | PER_PERIODS_OF_SERVICE | LEAVING_REASON (desc) | Core HR | Action & Reasons.xlsx |
| Is currently employed | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | ASSIGNMENT_STATUS_TYPE | Core HR | Assignment Status.xlsx |
| Role | PersonalData | LEGACY | PER_PERSON_TYPE_USAGES_F | PERSON_TYPE_ID | Core HR | Person Type.xlsx |
| Employee status | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | WORKER_CATEGORY | Core HR | Worker Category.xlsx |
| KeyDates - GroupStartDate | KeyDates | COREHR | PER_PERIODS_OF_SERVICE | DATE_START | Core HR | - |
| KeyDates - CompanyStartDate | KeyDates | COREHR | PER_PERIODS_OF_SERVICE | DATE_START (LE) | Core HR | - |
| KeyDates - RecalculatedSeniorityDate | KeyDates | COREHR | PER_PERIODS_OF_SERVICE | ADJUSTED_SVC_DATE | Core HR | Seniority Rules.xlsx |
| KeyDates - GroupEndDate | KeyDates | COREHR | PER_PERIODS_OF_SERVICE | ACTUAL_TERMINATION_DATE | Core HR | Action & Reasons.xlsx |
| EmployeeFileStatus - Status | EmployeeFileStatus | COREHR | PER_ALL_ASSIGNMENTS_F | ASSIGNMENT_STATUS_TYPE | Core HR | Assignment Status.xlsx |
| EmployeeFileStatus - Comments | EmployeeFileStatus | COREHR | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | - |
| PopulationType - Value | PopulationType | COREHR | PER_PERSON_TYPE_USAGES_F | PERSON_TYPE_ID | Core HR | Person Type.xlsx |
| PopulationType - Comments | PopulationType | COREHR | PER_PERSON_TYPE_USAGES_F | (DFF) | Core HR | - |

### 4.5 Core HR Fields (Job & Organization)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| Line of Business - OU | Line of Business | LEGACY | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID (DIV) | Core HR | Division.xlsx |
| Organisational Unit | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID (BU) | Core HR | Business Unit.xlsx |
| Legal Entity | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID (LE) | Core HR | Legal Entity.xlsx |
| Legal Entity Code | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID | Core HR | Legal Entity.xlsx |
| Legal Entity Country | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | (attribute) | Core HR | Country Code.xlsx |
| Allocation Center | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID (DEPT) | Core HR | Department.xlsx |
| Allocation center's Legal Entity | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | (parent) | Core HR | Organization Tree.xlsx |
| AC Code | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID | Core HR | Department.xlsx |
| UO Code | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | ORGANIZATION_ID | Core HR | Business Unit.xlsx |
| Activity | PersonalData | LEGACY | PER_JOB_FAMILIES | JOB_FAMILY_ID | Core HR | Job Family.xlsx |
| Function | PersonalData | LEGACY | PER_JOBS | JOB_FUNCTION_ID | Core HR | Job Function.xlsx |
| Sub-Function | PersonalData | LEGACY | PER_JOBS | (DFF) | Core HR | Job Sub Family.xlsx |
| Job Category | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | JOB_CATEGORY | Core HR | Assignment Category.xlsx |
| New Job Reference | PersonalData | LEGACY | PER_JOBS | JOB_ID | Core HR | Job.xlsx |
| New Job Reference Code | PersonalData | LEGACY | PER_JOBS | JOB_CODE | Core HR | Job.xlsx |
| Job Ref Name | PersonalData | LEGACY | PER_JOBS | NAME | Core HR | Job.xlsx |
| Job Ref Code | PersonalData | LEGACY | PER_JOBS | JOB_CODE | Core HR | Job.xlsx |
| Job Position | PersonalData | LEGACY | PER_POSITIONS | POSITION_ID | Core HR | Position.xlsx |
| Band | PersonalData | LEGACY | PER_GRADES | GRADE_ID | Core HR | Grade.xlsx |
| TopEx | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | Management Level.xlsx |
| Local Classification L0 | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF - France) | LDG | - |
| Local Classification L1 | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF - France) | LDG | - |
| Local Classification L2 | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF - France) | LDG | - |
| Business Segment | PersonalData | LEGACY | HR_ALL_ORGANIZATION_UNITS | (DFF) | Core HR | Division.xlsx |
| LocalZone L1 | PersonalData | LEGACY | PER_LOCATIONS | (hierarchy) | Core HR | Location.xlsx |
| LocalZone L2 | PersonalData | LEGACY | PER_LOCATIONS | (hierarchy) | Core HR | Location.xlsx |
| Lvl 2 : BU | Sub - Product | Local Zone | Lvl 2 | LEGACY | HR_ALL_ORGANIZATION_UNITS | (hierarchy) | Core HR | Organization Tree.xlsx |
| Situation - CostCenter | Situation | COREHR | PER_ALL_ASSIGNMENTS_F | DEFAULT_CODE_COMB_ID | Finance | - |
| Situation - Fte | Situation | COREHR | PER_ALL_ASSIGNMENTS_F | FTE | Core HR | Frequency Working Hours.xlsx |
| Situation - FtePaid | Situation | COREHR | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | - |
| Situation - CollectiveAgreement | Situation | COREHR | PER_CONTRACTS_F | (DFF - France) | LDG | Collective Agreement.xlsx |

### 4.6 Core HR Fields (Contract)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| ContractCode | PersonalData | LEGACY | PER_CONTRACTS_F | CONTRACT_ID | Core HR | Contract Type.xlsx |
| Contract Start Date | PersonalData | LEGACY | PER_CONTRACTS_F | START_DATE | Core HR | - |
| Contract End Date | PersonalData | LEGACY | PER_CONTRACTS_F | END_DATE | Core HR | - |
| Type of Contract | PersonalData | LEGACY | PER_CONTRACTS_F | CONTRACT_TYPE | Core HR | Contract Type.xlsx |
| Nature of contract | PersonalData | LEGACY | PER_CONTRACTS_F | (DFF) | Core HR | Contract Type.xlsx |
| Default Situation FTE% | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | FTE | Core HR | Frequency Working Hours.xlsx |
| Current Situation FTE% | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | WORKING_HOURS | Core HR | Frequency Working Hours.xlsx |
| End of probation period | PersonalData | LEGACY | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| Contract - AddendumNumber | Contract | COREHR | PER_CONTRACTS_F | (DFF) | Core HR | - |
| Contract - AddendumReason | Contract | COREHR | PER_CONTRACTS_F | (DFF) | Core HR | Action & Reasons.xlsx |
| Contract - AnnualSalary | Contract | COREHR | CMP_SALARY | SALARY_ANNUALIZED | Payroll | Salary Basis.xlsx |
| Contract - AnnualIncentive | Contract | COREHR | CMP_SALARY | (DFF) | Payroll | Comp. Elements.xlsx |
| Contract - AnnualIncentiveCurrency | Contract | COREHR | CMP_SALARY | (DFF) | Payroll | Currencies.xlsx |
| Contract - BudgetReference | Contract | COREHR | PER_CONTRACTS_F | (DFF) | Core HR | - |
| Contract - Comments | Contract | COREHR | PER_CONTRACTS_F | (DFF) | Core HR | - |
| Contract - Currency | Contract | COREHR | CMP_SALARY | SALARY_BASIS_ID | Payroll | Currencies.xlsx |
| Contract - DateOfLastWorkingDay | Contract | COREHR | PER_PERIODS_OF_SERVICE | LAST_WORKING_DATE | Core HR | - |
| Contract - FinalProcessDate | Contract | COREHR | PER_PERIODS_OF_SERVICE | FINAL_PROCESS_DATE | Core HR | - |
| Contract - FixedTermContractReason | Contract | COREHR | PER_CONTRACTS_F | (DFF) | Core HR | Contract Type.xlsx |
| Contract - HiringReason | Contract | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | Action & Reasons.xlsx |
| Contract - HourlyRate | Contract | COREHR | CMP_SALARY | SALARY_AMOUNT | Payroll | Salary Basis.xlsx |
| Contract - JobTitle | Contract | COREHR | PER_ALL_ASSIGNMENTS_F | ASSIGNMENT_NAME | Core HR | Job.xlsx |
| Contract - MonthlySalary | Contract | COREHR | CMP_SALARY | SALARY_AMOUNT | Payroll | Salary Basis.xlsx |
| Contract - NatureOfContract | Contract | COREHR | PER_CONTRACTS_F | (DFF) | Core HR | Contract Type.xlsx |
| Contract - NoticeEndDate | Contract | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| Contract - NoticeStartDate | Contract | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| Contract - NoticeStatus | Contract | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| Contract - NumberOfHours | Contract | COREHR | PER_ALL_ASSIGNMENTS_F | NORMAL_HOURS | Core HR | Frequency Working Hours.xlsx |
| Contract - NumberOfMonths | Contract | COREHR | PER_CONTRACTS_F | DURATION | Core HR | Contract Type.xlsx |
| Contract - StandingInForEmployeeUniqueID | Contract | COREHR | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | - |
| Contract - Status | Contract | COREHR | PER_CONTRACTS_F | STATUS | Core HR | Assignment Status.xlsx |
| Contract - TerminationDate | Contract | COREHR | PER_PERIODS_OF_SERVICE | ACTUAL_TERMINATION_DATE | Core HR | Action & Reasons.xlsx |
| Contract - TerminationReason | Contract | COREHR | PER_PERIODS_OF_SERVICE | LEAVING_REASON | Core HR | Action & Reasons.xlsx |
| ProbationaryPeriod - FirstPeriodStartDate | ProbationaryPeriod | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| ProbationaryPeriod - FirstPeriodEndDate | ProbationaryPeriod | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| ProbationaryPeriod - FirstPeriodStatus | ProbationaryPeriod | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| ProbationaryPeriod - FirstPeriodComments | ProbationaryPeriod | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| ProbationaryPeriod - SecondPeriodStartDate | ProbationaryPeriod | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| ProbationaryPeriod - SecondPeriodEndDate | ProbationaryPeriod | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| ProbationaryPeriod - SecondPeriodStatus | ProbationaryPeriod | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |
| ProbationaryPeriod - SecondPeriodComments | ProbationaryPeriod | COREHR | PER_PERIODS_OF_SERVICE | (DFF) | Core HR | - |

### 4.7 Core HR Fields (Manager Relationships)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| Is a Manager | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | MANAGER_FLAG | Core HR | Manager Type.xlsx |
| Hierarchical ID | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | MANAGER_ID | Core HR | Manager Type.xlsx |
| Hierarchical Name | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| Hierarchical Email | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| Is Active | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | ASSIGNMENT_STATUS_TYPE | Core HR | Assignment Status.xlsx |
| HR Manager ID | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | Manager Type.xlsx |
| HR Manager Name | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| HR Manager Email | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| Salary Review Manager ID | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | Manager Type.xlsx |
| Salary Review Manager Name | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| Travel Approver ID | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | Approval Workflows.xlsx |
| Travel Approver Name | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| Expense Report Approver ID | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | Approval Workflows.xlsx |
| Expense Report Approver | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| Leaves Validator ID | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | Approval Workflows.xlsx |
| Leaves Validator | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| Correspondant Formation | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | Manager Type.xlsx |
| Email of the handler of organisation Working Manager | PersonalData | LEGACY | - | (lookup) | Core HR | - |
| TransversalReferent - ReferentUniqueId | TransversalReferent | COREHR | PER_ALL_ASSIGNMENTS_F | (DFF) | Core HR | Manager Type.xlsx |

### 4.8 Compensation Fields (Payroll)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| Base Salary Effective Date | PersonalData | LEGACY | CMP_SALARY | DATE_FROM | Payroll | Compensation History.xlsx |
| Base Salary Value | PersonalData | LEGACY | CMP_SALARY | SALARY_AMOUNT | Payroll | Salary Basis.xlsx |
| Annual FTE base salary | PersonalData | LEGACY | CMP_SALARY | SALARY_ANNUALIZED | Payroll | Salary Basis.xlsx |
| Base Salary currency | PersonalData | LEGACY | CMP_SALARY | SALARY_BASIS_ID | Payroll | Currencies.xlsx |
| Frequency | PersonalData | LEGACY | PAY_SALARY_BASES | PAY_BASIS | Payroll | Frequence Salary.xlsx |
| Reason | PersonalData | LEGACY | CMP_SALARY | (DFF) | Payroll | Action & Reasons.xlsx |
| Nb of Paid Periods/year | PersonalData | LEGACY | PAY_SALARY_BASES | (DFF) | Payroll | Frequence Salary.xlsx |
| Bonus - Theorical | Bonus | LEGACY | CMP_SALARY | (DFF) | Payroll | Comp. Elements.xlsx |
| Bonus Start Date | PersonalData | LEGACY | PAY_ELEMENT_ENTRIES_F | EFFECTIVE_START_DATE | Payroll | Comp. Elements.xlsx |
| Bonus - Theorical amount | Bonus | LEGACY | PAY_ELEMENT_ENTRIES_F | SCREEN_ENTRY_VALUE | Payroll | Comp. Elements.xlsx |
| Last paid Premium Type | PersonalData | LEGACY | PAY_ELEMENT_ENTRIES_F | ELEMENT_NAME | Payroll | Comp. Elements.xlsx |
| Last paid Premium Amount | PersonalData | LEGACY | PAY_ELEMENT_ENTRIES_F | SCREEN_ENTRY_VALUE | Payroll | Comp. Elements.xlsx |
| Last paid Premium Currency | PersonalData | LEGACY | PAY_ELEMENT_ENTRIES_F | (DFF) | Payroll | Currencies.xlsx |
| Last paid Premium Date | PersonalData | LEGACY | PAY_ELEMENT_ENTRIES_F | EFFECTIVE_START_DATE | Payroll | Comp. Elements.xlsx |
| Compensation - Amount | Compensation | COREHR | CMP_SALARY | SALARY_AMOUNT | Payroll | Salary Basis.xlsx |
| Compensation - ContractNumber | Compensation | COREHR | CMP_SALARY | (DFF) | Payroll | - |
| Compensation - Currency | Compensation | COREHR | CMP_SALARY | (DFF) | Payroll | Currencies.xlsx |

### 4.9 Bank Details (LDG/Payroll)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| Account holder | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | ACCOUNT_NAME | LDG | Payroll Relationship.xlsx |
| Payment method | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | PAYMENT_TYPE | LDG | Payroll Relationship.xlsx |
| IBAN or ABA/Sort Code | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | ATTRIBUTE1 (DFF) | LDG | Payroll Relationship.xlsx |
| BIC or SWIFT Code | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | ATTRIBUTE2 (DFF) | LDG | Payroll Relationship.xlsx |
| Bank name | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | BANK_NAME | LDG | Payroll Relationship.xlsx |
| Bank address | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| Account number | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | ACCOUNT_NUMBER | LDG | Payroll Relationship.xlsx |
| Clearing number | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| Payment method for fees reports | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | PAYMENT_TYPE (2nd) | LDG | Payroll Relationship.xlsx |
| Account holder for fees reports | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | ACCOUNT_NAME (2nd) | LDG | Payroll Relationship.xlsx |
| IBAN or ABA/Sort Code for fees reports | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | ATTRIBUTE1 (2nd) | LDG | Payroll Relationship.xlsx |
| BIC or SWIFT code for fees reports | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | ATTRIBUTE2 (2nd) | LDG | Payroll Relationship.xlsx |
| Bank name for fees reports | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | BANK_NAME (2nd) | LDG | Payroll Relationship.xlsx |
| Bank address for fees reports | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | (DFF) (2nd) | LDG | - |
| Account number for fees reports | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | ACCOUNT_NUMBER (2nd) | LDG | Payroll Relationship.xlsx |
| Expense clearing number | PersonalData | LEGACY | PAY_PERSONAL_PAYMENT_METHODS | (DFF) (2nd) | LDG | - |
| BankDetails - AccountHolder | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | ACCOUNT_NAME | LDG | Payroll Relationship.xlsx |
| BankDetails - AccountNumber | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | ACCOUNT_NUMBER | LDG | Payroll Relationship.xlsx |
| BankDetails - BankName | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | BANK_NAME | LDG | Payroll Relationship.xlsx |
| BankDetails - BicOrSwift | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| BankDetails - IBANOrABA | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| BankDetails - PaymentMethod | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | PAYMENT_TYPE | LDG | Payroll Relationship.xlsx |
| BankDetails - ClearingNumber | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| BankDetails - Country | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | Country Code.xlsx |
| BankDetails - Street | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| BankDetails - StreetNumber | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| BankDetails - PostalCode | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| BankDetails - TownOrCity | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| BankDetails - UseSameAccountForExpense | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (DFF) | LDG | - |
| BankDetails - ExpenseAccount* | BankDetails | COREHR | PAY_PERSONAL_PAYMENT_METHODS | (2nd account) | LDG | Payroll Relationship.xlsx |

### 4.10 Government IDs (LDG)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| Social security number | PersonalData | LEGACY | PER_NATIONAL_IDENTIFIERS | NATIONAL_IDENTIFIER_NUMBER | LDG (FR/EU) | National ID.xlsx |
| ID card | PersonalData | LEGACY | PER_DOCUMENTS_OF_RECORD | DOCUMENT_NUMBER | LDG | Document Type.xlsx |
| Passport | PersonalData | LEGACY | PER_PASSPORTS | PASSPORT_NUMBER | Core HR | Passport.xlsx |
| Residence permit | PersonalData | LEGACY | PER_VISAS_PERMITS | PERMIT_NUMBER | Core HR | Visa & Permits.xlsx |
| Tax number | PersonalData | LEGACY | PER_NATIONAL_IDENTIFIERS | NATIONAL_IDENTIFIER_NUMBER | LDG | National ID.xlsx |
| Driving licence | PersonalData | LEGACY | PER_DRIVER_LICENSES | LICENSE_NUMBER | Core HR | Driver Licence.xlsx |
| GovernmentID - NationalID | GovernmentID | COREHR | PER_NATIONAL_IDENTIFIERS | NATIONAL_IDENTIFIER_NUMBER | LDG | National ID.xlsx |
| GovernmentID - NationalIDType | GovernmentID | COREHR | PER_NATIONAL_IDENTIFIERS | NATIONAL_IDENTIFIER_TYPE | LDG | National ID.xlsx |
| GovernmentID - NationalIDCountry | GovernmentID | COREHR | PER_NATIONAL_IDENTIFIERS | ISSUING_COUNTRY | LDG | Country Code.xlsx |
| GovernmentID - PassportNumber | GovernmentID | COREHR | PER_PASSPORTS | PASSPORT_NUMBER | Core HR | Passport.xlsx |
| GovernmentID - PassportExpiryDate | GovernmentID | COREHR | PER_PASSPORTS | EXPIRATION_DATE | Core HR | Passport.xlsx |
| GovernmentID - PassportCountry | GovernmentID | COREHR | PER_PASSPORTS | COUNTRY | Core HR | Country Code.xlsx |

### 4.11 Cost Allocation (Finance)

| Talentsoft Field | TS Category | Source | Oracle Object | Oracle Field | Scope | Repository Sheet |
|------------------|-------------|--------|---------------|--------------|-------|------------------|
| Cost Center Code | PersonalData | LEGACY | PER_ALL_ASSIGNMENTS_F | DEFAULT_CODE_COMB_ID | Finance | Department.xlsx |
| Cost Center LVL1 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT (CC) | Finance | Department.xlsx |
| Cost Center LVL2 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT (CC) | Finance | Department.xlsx |
| MAB Function Code | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT (Activity) | Finance | Job Function.xlsx |
| MAB Sub Fuction Code | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT (Sub-Act) | Finance | Job Sub Family.xlsx |
| Cost Center A/B/C | PersonalData | LEGACY | PAY_COSTING_RULES | (Multi-alloc) | Finance | - |
| % A/B/C | PersonalData | LEGACY | PAY_COSTING_RULES | PERCENTAGE | Finance | - |
| S.O.U Managerial - Code | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT (SOU) | Finance | Business Unit.xlsx |
| Accounting Entry 1 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT1 | Finance | - |
| Accounting Entry 2 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT2 | Finance | - |
| Accounting Entry 3 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT3 | Finance | - |
| Accounting Entry 4 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT4 | Finance | - |
| Accounting Entry 5 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT5 | Finance | - |
| Accounting Entry 6 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT6 | Finance | - |
| Accounting Entry 7 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT7 | Finance | - |
| Accounting Entry 8 | PersonalData | LEGACY | GL_CODE_COMBINATIONS | SEGMENT8 | Finance | - |

---

## 5. Gap Analysis

### 5.1 UKG Gaps (US → Oracle)

| # | Gap Type | UKG Field | Issue | Resolution |
|---|----------|-----------|-------|------------|
| 1 | **No Direct Mapping** | Chinese Name | Oracle doesn't have dedicated field | Use DFF on Person Names |
| 2 | **No Direct Mapping** | Legal Birth Name | France-specific | Use DFF on Person Names |
| 3 | **No Direct Mapping** | Name of Father | Mexico-specific | Use DFF on Person Names |
| 4 | **No Direct Mapping** | Name of Mother | Mexico-specific | Use DFF on Person Names |
| 5 | **No Direct Mapping** | Legal Name in Kanji | Japan-specific | Use DFF on Person Names |
| 6 | **No Direct Mapping** | Legal Name in Furigana | Japan-specific | Use DFF on Person Names |
| 7 | **US LDG-Specific** | EEO Establishment | US compliance | Configure US Legislative |
| 8 | **US LDG-Specific** | FMLA Qualified | US leave | Configure Absence DFF |
| 9 | **Integration Required** | Badge Number | Time & Attendance | External integration |
| 10 | **Integration Required** | Time Clock | Time & Attendance | External integration |
| 11 | **Transformation** | Employment Status (Planned) | Future status concept | Use Oracle Future Actions |
| 12 | **Custom Fields** | iupUDField01-15 | User-defined fields | Map to Assignment DFF |
| 13 | **Calculated** | Years In Job | Calculated field | Oracle formula |
| 14 | **Calculated** | Seniority Years | Calculated field | Oracle formula |
| 15 | **Calculated** | Last Hire Years | Calculated field | Oracle formula |
| 16 | **Payroll-Specific** | Arrears processing | US payroll | Configure US Payroll |
| 17 | **Payroll-Specific** | PTO Accruals | US benefits | Configure Absence Plans |
| 18 | **Data Quality** | Photo Available | Binary indicator | Document Management |

### 5.2 Talentsoft Gaps (Global → Oracle)

| # | Gap Type | Talentsoft Field | Issue | Resolution |
|---|----------|------------------|-------|------------|
| 1 | **Multi-value** | Cost Center A/B/C + % | Multiple cost allocations | Configure Payroll Costing Rules |
| 2 | **France-Specific** | Local Classification L0/L1/L2 | French labor categories | Use FR LDG DFF |
| 3 | **France-Specific** | Last 6 years Development interview | French legal requirement | Use DFF or Custom Table |
| 4 | **France-Specific** | Collective Agreement | French labor law | Configure FR Collective Agreements |
| 5 | **Medical** | MedicalCheckUp fields (10+) | Occupational health | External integration or DFF |
| 6 | **Medical** | OccupationalDisease fields (5+) | French compliance | External integration or DFF |
| 7 | **Custom Managers** | Travel Approver | Non-hierarchical approver | Configure Approval Chains |
| 8 | **Custom Managers** | Expense Report Approver | Non-hierarchical approver | Configure Approval Chains |
| 9 | **Custom Managers** | Leaves Validator | Non-hierarchical approver | Configure Approval Chains |
| 10 | **Custom Managers** | Correspondant Formation | Training contact | Use Assignment DFF |
| 11 | **Duplicate Fields** | 85 fields marked DUPLICATE | Data consolidation | Map to single Oracle field |
| 12 | **Profile Metrics** | My Profile completion rate | G-Talent+ specific | Not migrated |
| 13 | **Vacancy Link** | Vacancy Request - Old/Core HR | Recruitment link | Configure Recruiting |
| 14 | **Country-Specific** | Health Entity (Chile) | Chilean healthcare | Use CHL LDG DFF |
| 15 | **Country-Specific** | AFP (Chile) | Chilean pension | Use CHL LDG DFF |
| 16 | **Germany-Specific** | GermanRegulation fields | German compliance | Use DEU LDG DFF |
| 17 | **Integration** | Accounting Entry 1-8 | GL integration | Configure Costing |
| 18 | **Assigned Employee** | Assigned Employee field | Secondary assignment | Oracle Global Transfer |

### 5.3 Common Gaps (Both Systems)

| # | Gap Type | Fields | Impact | Resolution |
|---|----------|--------|--------|------------|
| 1 | **Multi-Manager** | Multiple approver types | Different manager per action | Configure multiple Manager Types |
| 2 | **Cost Allocation** | Split percentages | Multi-ERP allocation | See 14_Multialocation_MAB.md |
| 3 | **Bank Details Expense** | Separate expense account | Two payment methods | Configure as secondary bank |
| 4 | **Probation Periods** | First + Second probation | Two periods tracked | Use DFF or Custom Table |
| 5 | **Job Hierarchy** | Activity > Function > Sub-Function | 3-level job classification | Use Job Family + Job + DFF |
| 6 | **Local Zones** | L1/L2 geographic zones | Regional organization | Use Location Hierarchy |

---

## 6. Recommendations

### 6.1 Core HR Configuration

1. **Person DFF Setup:**
   - Number of Children
   - TopEx Flag
   - Local Classification (France)
   - Country-specific name fields

2. **Assignment DFF Setup:**
   - Travel Approver
   - Expense Approver
   - Leave Validator
   - Training Contact
   - UKG User-Defined Fields (map selectively)

3. **Multiple Manager Types:**
   - Line Manager (default)
   - HR Manager
   - Salary Review Manager
   - Functional Manager

### 6.2 LDG Configuration by Country

| Country | LDG Requirements |
|---------|------------------|
| **US** | EEO Establishment, FMLA tracking, I-9 compliance |
| **France** | Local Classifications L0/L1/L2, Collective Agreement, 6-year interview tracking |
| **Germany** | German Regulation fields |
| **Chile** | Health Entity, AFP |
| **All** | National ID formats per country |

### 6.3 Payroll Integration

1. **UKG US Payroll:**
   - Time & Attendance integration
   - Accrual balance migration
   - Pay suspension tracking

2. **Global Payroll:**
   - Bank details by country format
   - Multi-cost allocation (see MAB model)
   - Salary frequency mapping

### 6.4 Data Migration Priority

| Priority | Category | Source | Volume |
|----------|----------|--------|--------|
| 1 | Person Demographics | Both | All active |
| 2 | Employment Dates | Both | All active |
| 3 | Job & Organization | Both | All active |
| 4 | Manager Relationships | Both | All active |
| 5 | Compensation | Both | Current + 2 years history |
| 6 | Bank Details | Talentsoft | All active |
| 7 | Government IDs | Both | All with expiry dates |
| 8 | Cost Allocation | Talentsoft | All active |

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-06 | HCM Agent | Initial field mapping and gap analysis |
| 1.1 | 2025-12-06 | HCM Agent | Added TS Category column to all Talentsoft mapping tables (sections 4.1-4.11), expanded GovernmentID COREHR fields, added Accounting Entry fields |
| 1.2 | 2025-12-06 | HCM Agent | Added Section 7: Repository Sheets Reference - maps 69 Excel sheets from 04-SHEETS folder to mapping categories |
| 1.3 | 2025-12-06 | HCM Agent | Added Repository Sheet column to all Talentsoft mapping tables (4.1-4.11) - direct field-to-sheet reference for each mapped field |
| 1.4 | 2025-12-07 | HCM Agent | Added Section 2.4: GEODIS Confirmed Repository Sources - validated record counts (Business Unit: 2,175, Department: 10,803, Legal Entity: 364, etc.) with organization hierarchy |

---

## 7. Repository Sheets Reference

The following repository sheets in `04 - SHEETS` folder contain the Oracle HCM configuration values for each mapping category.

### 7.1 Personal Details (Section 4.1-4.3)

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| Person Identity | `Name Formats .xlsx` | Personal Details\ |
| Person Identity | `Name Styles.xlsx` | Personal Details\ |
| Person Identity | `Titles.xlsx` | Personal Details\ |
| Person Identity | `Gender.xlsx` | Personal Details\ |
| Person Identity | `Marital Statuses.xlsx` | Personal Details\ |
| Person Identity | `Citizenship Status.xlsx` | Personal Details\ |
| Person Identity | `Person Type.xlsx` | Personal Details\ |
| Person Identity | `Person Identifier Type for Ext.xlsx` | Personal Details\ |
| Address | `Address Format.xlsx` | Personal Details\ |
| Address | `Address Type.xlsx` | Personal Details\ |
| Contact | `Contact.xlsx` | Personal Details\ |
| Contact | `Phone Type.xlsx` | Personal Details\ |
| Contact | `E-Mail Type.xlsx` | Personal Details\ |
| Contact | `Correspondence Language.xlsx` | Personal Details\ |

### 7.2 Employment Details (Section 4.4)

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| Employment Status | `Assignment Status.xlsx` | Employment Details\ |
| Employment Category | `Assignment Category.xlsx` | Employment Details\ |
| Worker Type | `Worker Category.xlsx` | Employment Details\ |
| Regular/Temporary | `Regular or Temporary.xlsx` | Employment Details\ |
| Hourly/Salaried | `Hourly-Salaried.xlsx` | Employment Details\ |
| Working Hours | `Frequency Working Hours.xlsx` | Employment Details\ |
| Seniority | `Seniority Rules.xlsx` | Employment Details\ |

### 7.3 Job & Organization (Section 4.5)

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| Enterprise | `Enterprise HCM.xlsx` | Organization Structure\ |
| Division | `Division.xlsx` | Organization Structure\ |
| Business Unit | `Business Unit.xlsx` | Organization Structure\ |
| Legal Entity | `Legal Entity.xlsx` | Organization Structure\ |
| Department | `Department.xlsx` | Organization Structure\ |
| Location | `Location.xlsx` | Organization Structure\ |
| Legal Address | `Legal Address.xlsx` | Organization Structure\ |
| Reporting Establishment | `Reporting Establishment .xlsx` | Organization Structure\ |
| Legislative Data Group | `Legislative Data Group.xlsx` | Organization Structure\ |
| Geography | `Geography.xlsx` | Organization Structure\ |
| Country Code | `Country Code.xlsx` | Organization Structure\ |
| Time Zone | `Time Zone.xlsx` | Organization Structure\ |
| Department Tree | `Department Tree.xlsx` | Organization Structure\ |
| Organization Tree | `Organization Tree.xlsx` | Organization Structure\ |
| BU Set Assignment | `BU Set Assignment.xlsx` | Organization Structure\ |
| Data Set | `Data Set.xlsx` | Organization Structure\ |

### 7.4 Workforce Structure (Section 4.5)

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| Job | `Job.xlsx` | Workforce Structure\ |
| Job Family | `Job Family.xlsx` | Workforce Structure\ |
| Job Sub Family | `Job Sub Family.xlsx` | Workforce Structure\ |
| Job Function | `Job Function.xlsx` | Workforce Structure\ |
| Position | `Position.xlsx` | Workforce Structure\ |
| Grade | `Grade.xlsx` | Workforce Structure\ |
| Grade Step | `Grade Step.xlsx` | Workforce Structure\ |
| Management Level | `Management Level.xlsx` | Workforce Structure\ |
| Currencies | `Currencies.xlsx` | Workforce Structure\ |

### 7.5 Contract (Section 4.6)

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| Contract Type | `Contract Type.xlsx` | Employment Details\ |
| Collective Agreement | `Collective Agreement.xlsx` | Employment Details\ |

### 7.6 Manager Relationships (Section 4.7)

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| Manager Type | `Manager Type.xlsx` | Employment Details\ |

### 7.7 Compensation & Payroll (Section 4.8-4.9)

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| Salary Basis | `Salary Basis.xlsx` | Compensation Details\ |
| Salary Frequency | `Frequence Salary.xlsx` | Compensation Details\ |
| Compensation Elements | `Comp. Elements.xlsx` | Compensation Details\ |
| Compensation History | `Compensation History.xlsx` | Compensation Details\ |
| Individual Comp Plan | `Individual Compensation Plan.xlsx` | Compensation Details\ |
| Payroll Relationship | `Payroll Relationship.xlsx` | Compensation Details\ |

### 7.8 Government IDs (Section 4.10)

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| National ID | `National ID.xlsx` | Personal Details\ |
| Passport | `Passport.xlsx` | Personal Details\ |
| Visa & Permits | `Visa & Permits.xlsx` | Personal Details\ |
| Driver Licence | `Driver Licence.xlsx` | Personal Details\ |
| Document Category | `Document Category.xlsx` | Personal Details\ |
| Document Type | `Document Type.xlsx` | Personal Details\ |

### 7.9 Additional Reference Sheets

| Mapping Section | Repository Sheet | Path |
|-----------------|------------------|------|
| Statutory Dependent | `Statutory Dependent.xlsx` | Personal Details\ |
| Highest Education | `Highest Education Level.xlsx` | Personal Details\ |
| Mandat Type | `Mandat type.xlsx` | Personal Details\ |
| Source System Owner | `Source Sytem Owner.xlsx` | Personal Details\ |

### 7.10 Process & Security

| Repository Sheet | Description | Path |
|------------------|-------------|------|
| `Core Data Model.xlsx` | Core HR data model definition | Process and Security\ |
| `Action & Reasons.xlsx` | HR actions and reasons | Process and Security\ |
| `Action.xlsx` | Action catalog (41 actions) | Process and Security\ |
| `Approval Workflows.xlsx` | Approval chain configurations | Process and Security\ |
| `Security Matrix.xlsx` | Role-based access (9 GEODIS roles, 308 objects) | Process and Security\ |

---

## Related Documents

- `02_Oracle_HCM_Dimensions_Reference.md` - Oracle HCM dimensions
- `14_Multialocation_MAB.md` - Cost allocation model
- `19_Repository_Schema_Reference.md` - Oracle field structures
- `20_GEODIS_HR_Workflows_Catalog.md` - HR process workflows
