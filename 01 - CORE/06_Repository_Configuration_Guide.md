# GEODIS Oracle Fusion HCM Cloud
## Repository Configuration Guide - Detailed Specifications

---

**Project:** GEODIS New HCM - AMARIS
**Phase:** 02 - Define
**Document:** Detailed Repository Configuration Guide
**Version:** 1.0
**Date:** 2025-11-27

---

## Table of Contents

1. [Organization Structure Repositories](#1-organization-structure-repositories)
2. [Workforce Structure Repositories](#2-workforce-structure-repositories)
3. [Personal Details Repositories](#3-personal-details-repositories)
4. [Employment Details Repositories](#4-employment-details-repositories)
5. [Compensation Details Repositories](#5-compensation-details-repositories)
6. [Process and Security Repositories](#6-process-and-security-repositories)
7. [GEODIS-Specific Configuration Notes](#7-geodis-specific-configuration-notes)

---

## 1. Organization Structure Repositories

### 1.1 Country Code

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | No |
| **Priority** | P1 - Foundation |
| **Dependencies** | None |

**Description:**
Standard ISO country codes provided by Oracle. Used for all location-based configurations and legislative compliance.

**GEODIS Countries in Scope:**
Based on Legal Entities data, GEODIS operates in:
- Americas: US, CA, BR, CL, AR, CO, MX, PE
- APAC: AU, NZ, CN, HK, JP, KR, SG, MY, TH, VN, IN, ID, TW, BD, PH
- Europe: FR, DE, GB, NL, BE, PL, HU, CZ, SK, RO, IT, ES, IE, SE, DK, NO, CH, TR
- Middle East: AE, SA, QA, BH
- Africa: ZA, MA, TN, CM, CI, BF, TD

**Configuration Actions:**
- No configuration required - Oracle-provided
- Validate all required countries are available in system

---

### 1.2 Geography

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | No |
| **Priority** | P1 - Foundation |
| **Dependencies** | Country Code |

**Description:**
Hierarchical geographic structures (Country > State/Province > City) provided by Oracle for address validation.

**Configuration Actions:**
- No configuration required
- Used for address format validation
- Ensure geographic data is current for all GEODIS operating countries

---

### 1.3 Legislative Data Group (LDG)

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 - Critical |
| **Dependencies** | Country Code |

**Description:**
Legislative Data Groups define the legislative context for payroll and HR compliance. Each LDG is associated with one country and one currency.

**GEODIS LDG Design:**
One LDG per country where GEODIS has legal entities with employees:

| LDG Code | LDG Name | Country | Currency |
|----------|----------|---------|----------|
| LDG_US | GEODIS US | United States | USD |
| LDG_CA | GEODIS Canada | Canada | CAD |
| LDG_FR | GEODIS France | France | EUR |
| LDG_DE | GEODIS Germany | Germany | EUR |
| LDG_GB | GEODIS UK | United Kingdom | GBP |
| LDG_NL | GEODIS Netherlands | Netherlands | EUR |
| LDG_BE | GEODIS Belgium | Belgium | EUR |
| LDG_PL | GEODIS Poland | Poland | PLN |
| LDG_CN | GEODIS China | China | CNY |
| LDG_JP | GEODIS Japan | Japan | JPY |
| LDG_AU | GEODIS Australia | Australia | AUD |
| LDG_SG | GEODIS Singapore | Singapore | SGD |
| LDG_IN | GEODIS India | India | INR |
| *[Additional countries as required]* | | | |

**Configuration Actions:**
1. Create LDG for each country with GEODIS employees
2. Associate with correct country and currency
3. Link to Legislative Data for country-specific compliance

---

### 1.4 Enterprise HCM

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | No |
| **Priority** | P1 - Foundation |
| **Dependencies** | None |

**Description:**
The Enterprise is the highest-level organization in Oracle Fusion HCM, representing the entire corporation. Only one Enterprise exists per implementation.

**GEODIS Enterprise:**
- **Enterprise Name:** GEODIS
- **Description:** GEODIS - Global Supply Chain Operator

**Configuration Actions:**
- Verify Enterprise is correctly named during implementation setup
- No ongoing configuration required

---

### 1.5 Legal Address

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 - Critical |
| **Dependencies** | Geography |

**Description:**
Legal addresses are the registered addresses for Legal Entities. They must comply with local address format requirements.

**GEODIS Address Formats:**
Different countries require different address components:

| Country | Address Format Components |
|---------|--------------------------|
| US | Street, City, State, ZIP Code |
| FR | Street, City, Postal Code |
| GB | Street, City, County, Postal Code |
| DE | Street, City, Postal Code |
| CN | Street, District, City, Province, Postal Code |

**Configuration Actions:**
1. Configure legal addresses for all GEODIS Legal Entities
2. Use Oracle-provided address formats
3. Ensure addresses match legal registration documents

---

### 1.6 Legal Entity

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 - Critical |
| **Dependencies** | LDG, Legal Address |

**Description:**
Legal Entities are the legally registered companies. In Oracle HCM, a Legal Entity can serve as:
- **Legal Employer**: Employs workers
- **Payroll Statutory Unit (PSU)**: Tax reporting entity

**GEODIS Legal Entity Structure:**
Based on MDM MAB data, key Legal Entities include:

| Region | Sample Legal Entities |
|--------|----------------------|
| Americas | GEODIS LOGISTICS LLC, GEODIS USA Inc., GEODIS LOGISTICS (CANADA) INC. |
| APAC | GEODIS Singapore Pte Ltd, GEODIS Australia Pty Ltd, GEODIS China Ltd, GEODIS India Pvt Ltd, GEODIS JAPAN Co. Ltd |
| Europe | GEODIS France entities (CL, FF, D&E, RT), GEODIS United Kingdom Ltd, GEODIS Poland Sp. z.o.o. |
| MEA | GEODIS entities in UAE, Saudi Arabia, South Africa |

**Configuration Attributes:**
- Legal Entity Identifier (Registration Number)
- Legal Entity Name
- Legal Address
- Classification (Legal Employer, PSU)
- Associated LDG
- Start/End Dates

**Configuration Actions:**
1. Define all GEODIS Legal Entities with registration details
2. Mark entities as Legal Employer where employees exist
3. Configure PSU relationships for tax reporting
4. Associate each with appropriate LDG

---

### 1.7 Division

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P2 |
| **Dependencies** | Enterprise |

**Description:**
Divisions are optional organizational groupings that span Legal Entities, typically representing business segments or product lines.

**GEODIS Division Structure:**
Based on Business Hierarchy (Lines of Business):

| Division Code | Division Name | Description |
|--------------|---------------|-------------|
| CL | Contract Logistics | Global Contract Logistics |
| FF | Freight Forwarding | Global Freight Forwarding |
| DE | Distribution & Express | Distribution & Express |
| RT | European Road Network | European Road Transport |
| NO | Corporate | Non-Allocated & Corporate |
| TOF | Trans-O-Flex | Trans-O-Flex Operations |
| UF | Urban Fox | Urban Fox Delivery |
| UP | Upply | Upply Platform |

**Configuration Actions:**
1. Create divisions aligned with GEODIS Lines of Business
2. Determine if divisions will be used for reporting
3. Associate Legal Entities with appropriate divisions

---

### 1.8 Business Unit

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 - Critical |
| **Dependencies** | Legal Entity |

**Description:**
Business Units are the primary operational units for transaction processing. They are associated with a primary Legal Entity and enable segregation of transactional data.

**GEODIS Business Unit Design:**
BUs typically align with regional/functional combinations:

| BU Code | BU Name | Primary Legal Entity | Region |
|---------|---------|---------------------|--------|
| BU_CLAM | Contract Logistics Americas | GEODIS LOGISTICS LLC | Americas |
| BU_CLEU | Contract Logistics Europe | GEODIS CL entities | Europe |
| BU_CLFR | Contract Logistics France | GEODIS CL France | France |
| BU_FFAM | Freight Forwarding Americas | GEODIS USA | Americas |
| BU_FFAP | Freight Forwarding APAC | GEODIS APAC entities | APAC |
| BU_FFEU | Freight Forwarding Europe | GEODIS FF entities | Europe |
| BU_RTEU | Road Transport Europe | GEODIS RT entities | Europe |
| BU_CORP | Corporate | GEODIS SA | Global |

**Configuration Actions:**
1. Define Business Units based on GEODIS operating model
2. Associate each BU with primary Legal Entity
3. Configure BU-level security and transaction processing rules

---

### 1.9 Location

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 - Critical |
| **Dependencies** | Legal Entity, Geography |

**Description:**
Locations represent physical work sites where employees are based. They are critical for compliance, tax calculations, and organizational reporting.

**GEODIS Location Data:**
Based on Legal Sites data, GEODIS has 1000+ locations globally including:

| Location Type | Examples |
|--------------|----------|
| Warehouses/Distribution Centers | GEODIS Logistics centers (US, EU, APAC) |
| Regional Offices | Americas HQ (Brentwood, TN), APAC HQ (Singapore) |
| Branch Offices | Country-level operational offices |
| Freight Stations | Transport and logistics hubs |

**Key Location Attributes:**
- Location Code (unique identifier)
- Location Name
- Address (Street, City, State/Province, Postal Code, Country)
- Location Type (Office, Warehouse, Distribution Center)
- Geographic Coordinates (optional)
- Associated Legal Entity
- Time Zone
- Ship-to/Bill-to Indicator

**Configuration Actions:**
1. Import all GEODIS operational locations
2. Assign locations to Legal Entities
3. Configure location types for reporting
4. Set up time zones for each location

---

### 1.10 Department

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 - Critical |
| **Dependencies** | Business Unit, Location |

**Description:**
Departments represent functional or organizational groupings within Business Units. They are used for cost allocation, reporting, and organizational hierarchy.

**GEODIS Department Design:**
Departments typically follow functional structure:

| Dept Code | Department Name | Function |
|-----------|----------------|----------|
| DEPT_OPS | Operations | Warehouse/Transport Operations |
| DEPT_FIN | Finance | Finance & Accounting |
| DEPT_HR | Human Resources | HR & Payroll |
| DEPT_IT | Information Technology | IT & Digital |
| DEPT_SAL | Sales | Commercial & Sales |
| DEPT_CUS | Customer Service | Customer Operations |
| DEPT_QUA | Quality | Quality & Compliance |
| DEPT_HSE | Health Safety Environment | HSE Functions |

**Configuration Actions:**
1. Define department structure aligned with GEODIS organization
2. Create hierarchical department codes
3. Associate departments with Business Units and locations
4. Set up department managers

---

### 1.11 Department Tree / Organization Tree

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P2 |
| **Dependencies** | Department |

**Description:**
Trees provide hierarchical views of organizational structures for reporting, approval routing, and data access.

**GEODIS Tree Requirements:**

| Tree Name | Purpose | Structure |
|-----------|---------|-----------|
| Department Hierarchy | Organizational reporting | LoB > Region > Country > Department |
| Manager Hierarchy | Approval routing | Based on reporting relationships |
| Cost Center Hierarchy | Financial reporting | Aligned with GL structure |

**Configuration Actions:**
1. Design tree structures based on GEODIS reporting needs
2. Create tree versions for different effective dates
3. Configure tree flattening for performance
4. Set up security based on tree position

---

### 1.12 Additional Organization Repositories

#### Reporting Establishment
Required for legal/statutory reporting in specific countries (e.g., France DADS).

#### Time Zone
Standard time zones - configure for each location.

#### Cost Center
Financial dimension - align with GEODIS Chart of Accounts.

#### Source System Owner
For data migration - configure if using HDL.

---

## 2. Workforce Structure Repositories

### 2.1 Job Family

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 |
| **Dependencies** | None |

**Description:**
Job Families group related jobs together for career path management, compensation analysis, and reporting.

**GEODIS Job Family Design:**

| Family Code | Job Family Name | Description |
|-------------|-----------------|-------------|
| JF_OPS | Operations | Warehouse, Transport, Logistics Operations |
| JF_CUS | Customer Service | Customer Operations & Support |
| JF_SAL | Sales & Commercial | Sales, Business Development |
| JF_FIN | Finance | Accounting, Finance, Treasury |
| JF_HR | Human Resources | HR, Payroll, Talent |
| JF_IT | Information Technology | IT, Digital, Data |
| JF_SUP | Support Functions | Admin, Legal, Communications |
| JF_EXE | Executive | Leadership & Executive roles |
| JF_ENG | Engineering | Technical & Engineering |
| JF_QUA | Quality & Compliance | Quality, HSE, Compliance |

**Configuration Actions:**
1. Define job families aligned with GEODIS functional structure
2. Configure job family attributes (benchmark data, compensation range)
3. Set up job family security if required

---

### 2.2 Job Function

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes (basic set) |
| **Modifiable** | Yes |
| **Priority** | P1 |
| **Dependencies** | None |

**Description:**
Job Functions categorize jobs by their primary activity or discipline. Oracle provides standard values that can be extended.

**GEODIS Job Functions:**

| Function Code | Job Function |
|--------------|--------------|
| EXEC | Executive/Management |
| PROF | Professional |
| TECH | Technical |
| ADMIN | Administrative |
| OPER | Operations |
| SALES | Sales |
| SERV | Service |

**Configuration Actions:**
1. Review Oracle-provided job functions
2. Add GEODIS-specific functions as needed
3. Map existing roles to job functions

---

### 2.3 Job

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 - Critical |
| **Dependencies** | Job Family, Job Function |

**Description:**
Jobs define the type of work performed, independent of organizational structure. A job describes a role that can exist across multiple departments or locations.

**GEODIS Job Structure:**

| Job Code | Job Name | Job Family | Job Function | Management Level |
|----------|----------|------------|--------------|------------------|
| JOB_WH_OPR | Warehouse Operator | Operations | Operations | Individual Contributor |
| JOB_WH_SUP | Warehouse Supervisor | Operations | Operations | Supervisor |
| JOB_WH_MGR | Warehouse Manager | Operations | Management | Manager |
| JOB_TRK_DRV | Truck Driver | Operations | Operations | Individual Contributor |
| JOB_TRP_SUP | Transport Supervisor | Operations | Operations | Supervisor |
| JOB_CUS_REP | Customer Service Rep | Customer Service | Service | Individual Contributor |
| JOB_SAL_REP | Sales Representative | Sales | Sales | Individual Contributor |
| JOB_SAL_MGR | Sales Manager | Sales | Management | Manager |
| JOB_FIN_ANA | Financial Analyst | Finance | Professional | Individual Contributor |
| JOB_HR_BUS | HR Business Partner | HR | Professional | Individual Contributor |

**Key Job Attributes:**
- Job Code (unique identifier)
- Job Name
- Job Family
- Job Function
- Management Level
- Regular/Temporary indicator
- Full-time/Part-time eligible
- Benchmark Job indicator
- FLSA Status (US)
- EEO Category (US)

**Configuration Actions:**
1. Define GEODIS job catalog with standardized naming
2. Associate jobs with job families and functions
3. Configure country-specific job attributes
4. Set up job-grade relationships

---

### 2.4 Grade

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 |
| **Dependencies** | LDG |

**Description:**
Grades define compensation levels and progression within the organization. They can be legislative (country-specific) or enterprise-wide.

**GEODIS Grade Structure Options:**

**Option A: Global Grading Framework**
| Grade | Level Description | Typical Roles |
|-------|------------------|---------------|
| G01-G03 | Support/Entry | Entry-level operational roles |
| G04-G06 | Professional | Experienced individual contributors |
| G07-G09 | Senior Professional | Senior ICs, Team Leads |
| G10-G12 | Manager | People managers |
| G13-G15 | Senior Manager | Department heads |
| G16-G18 | Director | Regional/Functional directors |
| G19-G21 | Executive | VP and above |

**Option B: Country-Specific Grades**
Use local grading systems where required by legislation or collective agreements.

**Configuration Actions:**
1. Decide on global vs. local grading approach
2. Create grade structures by LDG
3. Define grade rates/ranges for compensation
4. Configure grade ladders for progression

---

### 2.5 Position (If Used)

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P2 (Optional) |
| **Dependencies** | Job, Department, Location, Grade |

**Description:**
Positions represent specific roles within the organization - a position is a job in a specific department and location. Position management enables headcount control.

**GEODIS Position Decision:**
Position management is optional. Consider using if:
- Headcount budgeting is required
- Detailed workforce planning needed
- Multiple incumbents not allowed per role

**Configuration Actions:**
1. Decide if position management is required
2. If yes, define position creation rules
3. Configure position synchronization with jobs
4. Set up position approval workflows

---

### 2.6 Management Level

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes (basic set) |
| **Modifiable** | Yes |
| **Priority** | P2 |
| **Dependencies** | None |

**Description:**
Management levels categorize jobs by their organizational level for reporting and succession planning.

**GEODIS Management Levels:**

| Level Code | Level Name |
|------------|------------|
| IC | Individual Contributor |
| TL | Team Lead |
| SUP | Supervisor |
| MGR | Manager |
| SR_MGR | Senior Manager |
| DIR | Director |
| SR_DIR | Senior Director |
| VP | Vice President |
| SVP | Senior Vice President |
| EXEC | Executive/C-Suite |

---

## 3. Personal Details Repositories

### 3.1 Person Type

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes (standard types) |
| **Modifiable** | Yes (add custom) |
| **Priority** | P1 |

**Standard Oracle Person Types:**
- Employee
- Contingent Worker
- Pending Worker
- Nonworker
- Contact

**GEODIS Custom Person Types:**
If needed, extend for specific worker categories (e.g., Apprentice, Intern).

---

### 3.2 Name Formats & Styles

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes (country-specific) |
| **Modifiable** | Yes |
| **Priority** | P2 |

**Description:**
Name formats define how person names are structured and displayed by country.

**Key Country Variations:**
| Country | Name Format |
|---------|-------------|
| US/UK | First, Middle, Last |
| FR/DE | Last, First |
| CN | Family Name, Given Name |
| JP | Family Name, Given Name (with Kanji support) |

---

### 3.3 Address Types & Formats

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | Yes |
| **Priority** | P2 |

**Standard Address Types:**
- Home
- Mailing
- Work Location

**Configuration:** Configure address validation rules per country.

---

### 3.4 Contact & Emergency Contact

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | Yes |
| **Priority** | P2 |

**Contact Relationships:**
- Spouse/Partner
- Child
- Parent
- Emergency Contact
- Beneficiary

---

### 3.5 National Identifiers

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes (country-specific) |
| **Modifiable** | Yes |
| **Priority** | P1 |

**Key National ID Types by Country:**
| Country | ID Type | Format |
|---------|---------|--------|
| US | SSN | XXX-XX-XXXX |
| FR | INSEE | 13 digits |
| GB | NI Number | XX NNNNNN X |
| DE | Tax ID | 11 digits |
| IN | PAN/Aadhaar | Various |

---

### 3.6 Document Types & Categories

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | Yes |
| **Priority** | P2 |

**Standard Document Categories:**
- Identity Documents
- Employment Documents
- Qualification Documents
- Medical Documents
- Legal Documents

---

## 4. Employment Details Repositories

### 4.1 Worker Category

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | Yes (custom values) |
| **Priority** | P1 |

**Standard Categories:**
- Blue Collar
- White Collar
- Management

**GEODIS Custom Categories:**
Define based on collective agreement requirements (especially France).

---

### 4.2 Assignment Category

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | Yes |
| **Priority** | P1 |

**Standard Categories:**
- Full-Time Regular
- Part-Time Regular
- Full-Time Temporary
- Part-Time Temporary

---

### 4.3 Assignment Status

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | Yes |
| **Priority** | P1 |

**Standard Statuses:**
| Status | Type | Payroll Eligible |
|--------|------|-----------------|
| Active - Payroll Eligible | Active | Yes |
| Active - No Payroll | Active | No |
| Suspended - Payroll Eligible | Suspended | Yes |
| Suspended - No Payroll | Suspended | No |
| Inactive - No Payroll | Inactive | No |

---

### 4.4 Contract Type

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes |
| **Modifiable** | Yes |
| **Priority** | P1 |

**GEODIS Contract Types:**

| Country | Contract Types |
|---------|---------------|
| Global | Permanent, Fixed-Term, Temporary |
| France | CDI, CDD, Contrat d'apprentissage, Contrat de professionnalisation |
| Germany | Unbefristet, Befristet |
| US | At-Will, Fixed-Term |

---

### 4.5 Collective Agreement

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P2 |
| **Dependencies** | Legal Entity, LDG |

**Description:**
Collective agreements define employment terms negotiated with unions or worker representatives. Critical for European operations.

**GEODIS Collective Agreements:**
Define for countries with applicable agreements (France, Germany, Netherlands, etc.).

---

## 5. Compensation Details Repositories

### 5.1 Salary Basis

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 |

**Description:**
Salary basis defines how salary is expressed (annual, monthly, hourly) and the associated annualization factor.

**GEODIS Salary Bases:**

| Salary Basis | Frequency | Annualization Factor |
|-------------|-----------|---------------------|
| Annual Salary | Year | 1 |
| Monthly Salary | Month | 12 |
| Bi-Weekly Salary | Bi-Weekly | 26 |
| Weekly Salary | Week | 52 |
| Hourly Rate | Hour | 2080 (US standard) |

---

### 5.2 Compensation Elements

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | No |
| **Modifiable** | Yes |
| **Priority** | P1 |

**Description:**
Elements define the components of employee compensation (base pay, allowances, bonuses, etc.).

**GEODIS Compensation Elements:**
- Base Salary
- Bonus/Variable Pay
- Allowances (Housing, Transport, etc.)
- Overtime
- Shift Premium
- Country-specific elements

---

## 6. Process and Security Repositories

### 6.1 Actions & Action Reasons

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Yes (standard actions) |
| **Modifiable** | Yes (add reasons) |
| **Priority** | P1 |

**Standard HR Actions:**

| Action | Typical Reasons |
|--------|-----------------|
| Hire | New Hire, Rehire, Transfer In |
| Termination | Resignation, Retirement, Dismissal, End of Contract |
| Promotion | Merit, Position Change |
| Transfer | Location Change, Department Change |
| Salary Change | Merit Increase, Promotion, Market Adjustment |
| Leave of Absence | Medical, Parental, Personal, Military |

**Configuration Actions:**
1. Review Oracle-provided actions
2. Add GEODIS-specific reasons
3. Configure action security by role

---

### 6.2 Security Matrix

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Partial (roles provided) |
| **Modifiable** | Yes |
| **Priority** | P1 |

**GEODIS Role Categories:**

| Role Category | Examples |
|--------------|----------|
| HR Roles | HR Administrator, HR Analyst, HR Manager |
| Manager Roles | Line Manager, Department Manager |
| Employee Roles | Employee Self-Service |
| Executive Roles | Executive Access |
| IT Roles | IT Security Administrator |

**Data Security:**
- Legal Entity based access
- Business Unit based access
- Department hierarchy based access

---

### 6.3 Approval Workflows

| Attribute | Value |
|-----------|-------|
| **Oracle Provided** | Partial (templates provided) |
| **Modifiable** | Yes |
| **Priority** | P2 |

**GEODIS Approval Requirements:**

| Transaction | Approval Levels |
|-------------|-----------------|
| Hire | Manager > HR > (Budget if applicable) |
| Termination | Manager > HR |
| Salary Change | Manager > HR > Compensation (if threshold) |
| Promotion | Manager > HR > Senior Manager |
| Transfer | Both Managers > HR |

---

## 7. GEODIS-Specific Configuration Notes

### 7.1 Organization Alignment with MDM MAB

The GEODIS HCM organization structure should align with the MDM Master Data repository:

| MDM Concept | Oracle HCM Equivalent |
|-------------|----------------------|
| Legal Entity (Dilitrust) | Legal Entity/Legal Employer |
| Business Hierarchy (LoB) | Division |
| Managerial Hierarchy | Department Tree |
| Legal Sites | Locations |
| SOUs | Business Units |

### 7.2 Integration Considerations

Key integrations to consider:
- MDM MAB for master organization data
- Payroll systems per country
- Finance/ERP for cost centers
- Time & Attendance systems
- Learning Management (if applicable)

### 7.3 Data Migration Approach

**Migration Phases:**
1. Foundation data (Countries, LDGs, Legal Entities)
2. Organization structures (BUs, Departments, Locations)
3. Workforce structures (Jobs, Grades, Positions)
4. Employee data (Workers, Assignments)
5. Compensation data

**HDL Templates:** Use Oracle HCM Data Loader for bulk data migration.

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-11-27 | HCM Team | Initial creation |

---

*This document follows Oracle Fusion HCM Cloud implementation best practices and is customized for GEODIS organizational requirements.*
