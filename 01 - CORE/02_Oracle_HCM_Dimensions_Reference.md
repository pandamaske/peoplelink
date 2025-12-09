# Oracle HCM – Holistic Dimension Model

**Scope**  
This document defines **all structural dimensions** used in the GEODIS Oracle HCM Cloud implementation and explains:

- What each dimension represents functionally
- The **authoritative data source** (Hub libraries, MAB referentials, people extract)
- How it is **configured in Oracle** (HCM & GL)
- How dimensions **relate to each other** (hierarchies, trees, joins)
- Basic **governance & change management** rules

The goal is to have *one single reference* for integrators, HRIS, Finance and MDM when discussing “structures” in Oracle HCM.

---

## 1. Overview of Dimensions

### 1.1 High-level list

**Enterprise & Legal**
- Enterprise
- Legal Entity
- Legal Employer
- Legislative Data Group (LDG)

**Management & Operational Structure**
- Division (LoB / Region)
- Business Unit (BU)
- Department (Organizational Unit – OU)

**Analytical & Financial Structure**
- Reporting Unit (RU)
- SOU (global)
- Local SOU (local)
- Cost Center (GL Segment)

**Geographical Structure**
- Country / Geography
- Location (site)

**Workforce Structures**
- Job
- Position (if used)
- Grade & Grade Ladder

**Trees / Hierarchies**
- Department Tree (HCM)
- Organization Tree (HCM)
- GL Cost Center Hierarchy (Financials)

---

## 2. Enterprise & Legal Dimensions

### 2.1 Enterprise

**Definition**  
Single global GEODIS enterprise in Oracle HCM. Root owner of all HR data.

**Oracle object**  
- `Enterprise` (HCM common)

**Authoritative source**  
- Corporate master data (group level)

**Configuration instructions**
1. In FSM: *Setup and Maintenance* → *Global Human Resources* → *Enterprise Structures*.
2. Create one Enterprise:
   - Name: `GEODIS`
   - Code: `GEODIS`
   - Headquarters address: group HQ.
3. Enterprise acts as **root node** in Organization Trees.

**Governance**
- Single enterprise only.
- Changes to name or HQ address are rare and controlled by Group HRIS.

---

### 2.2 Legal Entities & Legal Employers

**Definition**  
A **Legal Entity** is a company recognized by law; a **Legal Employer** is the entity that employs workers in Oracle HCM.

**Oracle objects**  
- `Legal Entity`
- `Legal Employer`

**Authoritative sources**  
- MAB: `Local Legal Entities.csv`
- Possibly Hub `LegalStructure` library for cross-check

**Key fields from MAB**
- `Local Legal Entity Name`
- `Local Legal Entity Code`
- `Local Analytical Identification Code`
- `Legal Entity Code - DILITRUST`
- `Local CoA Identification Code`
- `Management Line Code`
- `Activation Date`, `Deactivation Date`, `Status Calculated`

**Configuration instructions**
1. Filter `Local Legal Entities` to `Status Calculated = 'ACTIVATED'`.
2. For each row in scope for HCM:
   - Create **Legal Entity** in Oracle:
     - Name = `Local Legal Entity Name`
     - Legal Entity Identifier = `Local Analytical Identification Code`
     - Code = `Local Legal Entity Code` (or DFF)
     - DFF for `Legal Entity Code - DILITRUST`, `Local CoA Identification Code`, `Management Line Code`.
   - Enable as **Legal Employer** if it actually employs workers.
3. Associate each Legal Entity to the correct **LDG** (per country/legislation).

**Governance**
- Creation / closure of Legal Entities driven by MAB & corporate legal team.
- HCM must **not** create new Legal Entities outside MAB.
- End-dating in Oracle must follow MAB `Deactivation Date`.

---

### 2.3 Legislative Data Groups (LDGs)

**Definition**  
Groups data and payroll rules by **legislation** (country).

**Oracle object**  
- `Legislative Data Group`

**Authoritative sources**  
- Country list from MAB country referentials and Hub geographies.

**Configuration instructions**
1. Define one LDG per **legislation** where GEODIS employs workers.
2. Associate each LDG to the correct **currency and regime**.
3. Attach Legal Entities to LDGs according to the country of registration.

**Governance**
- LDGs change only if GEODIS enters a **new country**.
- Controlled by HRIS & Global Payroll.

---

## 3. Management & Operational Structure

### 3.1 Division (LoB / Region)

**Definition**  
High-level management segmentation: **Line of Business (LoB)** or **Region**.

**Oracle object**  
- `Division`

**Authoritative sources**  
- MAB `Business Hierarchy.csv` (LoB levels)
- Region codes from people extract (e.g. `FRA - FRANCE`, `APAC - ASIA PACIFIC`).

**Design choice**
- Primary Divisions = **LoB L1** (e.g. FFW, Road, Contract Logistics, Distribution & Express, Corporate).
- Optional Divisions = Regional Divisions under each LoB.

**Configuration instructions**
1. In FSM: *Manage Divisions*.
2. For each LoB L1 in MAB Business Hierarchy (Status = ACTIVATED):
   - Division Code = LoB Code
   - Division Name = LoB Name
   - Start/End dates from MAB activation data.
3. Optionally create region-specific divisions if required.

**Hierarchy usage**
- Divisions appear as nodes in the **Organization Tree** under Enterprise.

**Governance**
- LoB changes are driven by Group Strategy / MAB Business Hierarchy.
- HRIS does not invent new Divisions; they mirror MAB LoB.

---

### 3.2 Business Units (BUs)

**Definition**  
Transactional units responsible for HR, payroll and/or financial processes.

**Oracle object**  
- `Business Unit`

**Authoritative source**  
- MAB `Reporting Units View.csv` (Reporting Units)

**Key MAB fields**
- `Reporting Unit Code`
- `Name - EN`, `Name - FR`
- `Country`
- `Currency`
- `LoB Code BFC - L4`
- `Activation Date`, `Deactivation Date`, `Status Calculated`

**Design rule**
> **1 Reporting Unit = 1 Oracle Business Unit** (for HCM transactional scope).

**Configuration instructions**
1. Filter `Reporting Units` to `Status Calculated = 'ACTIVATED'` and in HCM scope.
2. In FSM: *Manage Business Units*.
3. Per Reporting Unit:
   - BU Name = `Name - EN`
   - BU Code (optional) = `Reporting Unit Code`
   - Country = `Country`
   - Default reference data set = `COMMON` (or agreed set).
4. Associate BUs to Legal Entities via implementation workbook rules.

**Hierarchy usage**
- BUs are displayed as nodes in the **Organization Tree** under Divisions.
- They remain technically flat; the hierarchy is maintained in the tree.

**Governance**
- BUs follow MAB Reporting Units.
- Creation/closure driven by MDM & Finance, coordinated with HRIS.

---

### 3.3 Departments (Organizational Units – OU)

**Definition**  
Departments represent **organizational units** where people belong for HR purposes.

**Oracle object**  
- `Department` (Workforce Structure)

**Authoritative sources**  
- Hub `OrganisationalStructure` JSON (Departments library)
- People structure extract (`Organisational unit`, `Client code`)

**Key Hub fields**
- `ClientCode` (org unit code)
- `ShortName` / description
- `ParentClientCode`
- `IsActive`
- `ManagerUniqueID`, `AssistantUniqueIDs`
- `CostCenterClientCodes`

**Design rule**
> **1 Organizational Unit (ClientCode) = 1 Oracle Department**

**Configuration instructions**
1. Build a list of Organizational Units from the Hub:
   - Include only `IsActive = Y`, or as defined by scope.
2. In FSM: *Manage Departments*.
3. For each OU:
   - Department Code = `ClientCode`
   - Department Name = `ShortName`
   - Effective Start Date = hub `StartEffectDate` or agreed baseline.
   - Effective End Date = hub end date if inactive.
   - Manager: resolved later by mapping `ManagerUniqueID` to person.
4. Use **Department Set** = `COMMON`.

**Hierarchy usage – Department Tree**
- Parent Department = department whose Code = `ParentClientCode`.
- Full **Department Tree** is built from this parent/child structure.

**Governance**
- OU lifecycle managed by MDM & HR (creation, move, closure).  
- HCM must **mirror** the approved OU structure from the Hub.

---

## 4. Analytical & Financial Dimensions

### 4.1 Reporting Units (RU)

**Definition**  
Reporting Unit is a structured MAB object grouping SOUs for financial and managerial reporting.

**Oracle representation**  
- Primarily as **Business Units**.
- Also stored as attributes (DFFs) on Departments or employees if needed.

**Authoritative source**  
- MAB `Reporting Units View.csv`

**Configuration instructions**
- See **Business Unit** configuration (Section 3.2).

**Governance**
- Changes controlled by Finance & MDM.

---

### 4.2 SOU (Global)

**Definition**  
SOU is a **group-level operational unit** used for consolidated reporting.

**Oracle representation**  
- As **attributes**, not as structural objects:
  - DFF on Department (or Cost Center)
  - Dimension in reporting (OTBI, OAC)

**Authoritative source**  
- MAB `SOUs View.csv`

**Key fields**
- `SOU Code`, `SOU Digits`
- `Name`
- `Type` (Operational/Support…)
- `Reporting Unit Code`
- `Managerial Parent Code` (MAB level, not used as HCM tree)
- `Legal Entity Code - DILITRUST`
- `Alpha-2 Country Code`, `UN LOCODE`
- `Activation Date`, `Deactivation Date`, `Status Calculated`

**Configuration instructions**
1. Create a **flexfield** (e.g. Department DFF or Costing DFF) to store:
   - `SOU Code`
   - `SOU Name`
   - Optionally `SOU Type`, `Reporting Unit Code`.
2. During migration, populate these fields based on current org & costing mappings.

**Governance**
- SOU definitions managed centrally in MAB.
- HCM must only reference existing SOUs, not create new ones.

---

### 4.3 Local SOU & Cost Centers

**Definition**  
Local SOU is the **local analytical object** used by each application/ledger, usually one-to-one with **cost center** in GL.

**Oracle representation**  
- **GL Cost Center segment values** in the Chart of Accounts.

**Authoritative source**  
- MAB `Local SOUs.csv`

**Key MAB fields**
- `Local SOU Code`
- `Local Analytical Identification Code`
- `Name`
- `SOU Code`
- `Local Legal Entity Code`
- `Management Line Code`
- `Activation Date`, `Deactivation Date`, `Status Calculated`

**Design rule**
> **1 Local SOU = 1 GL Cost Center segment value**

**Configuration instructions (GL)**
1. In ERP Cloud (GL): define a **Cost Center value set**.
2. For each Local SOU (Status = ACTIVATED):
   - Segment Value = `Local SOU Code` or `Local Analytical Identification Code`.
   - Description = `Name`.
   - Attributes: store `SOU Code`, `Local Legal Entity Code`, `Management Line Code`.
3. Build **GL Cost Center Hierarchy**:
   - Group Local SOUs under SOU-level nodes, then RU, then LoB/Region as required by Finance.

**HCM usage**
- HCM **costing** (Payroll, Element, Department costing) references the cost center **segment values**.
- Departments from OU structure can store a **default cost center** pointing to Local SOUs via costing rules.

**Governance**
- Local SOUs governed by MDM & Finance.
- Any change must be coordinated between GL and HCM costing.

---

## 5. Geographical Dimensions

### 5.1 Country & Geographies

**Definition**  
Countries and regions used for locations, LDG, and reporting.

**Oracle representation**  
- **Countries** and **Geographies** are seeded / configurable in HCM & GL.

**Authoritative sources**  
- Hub `GeographicOrganisationStructure` JSON
- MAB country codes (`Alpha-2 Country Code`)

**Configuration instructions**
1. Align Hub country codes (FR, DE, AE…) with Oracle seeded countries.
2. Optional: configure **Geography Hierarchies** (Country → Region → City) if needed.

---

### 5.2 Locations (Sites)

**Definition**  
Physical places where people work or where legal reporting occurs.

**Oracle object**  
- `Location`

**Authoritative sources**  
- Hub Legal Sites / Addresses JSON
- MAB SOUs (`UN LOCODE`, `Site ID`) and people `Location Center`.

**Configuration instructions**
1. Build a **site master**:
   - Key: Site ID or Location Center code.
   - Attributes: Country, City, Postal Code, Address lines, UN LOCODE.
2. In FSM: *Manage Locations*.
3. For each site used by people or SOUs:
   - Location Code = site ID or structured code (e.g. `FR-PAR-HQ`).
   - Location Name = `[Country] – [City] – [Site]`.
   - Country = `Alpha-2 Country Code`.
   - Address fields from site master.
4. Use Location Set = `COMMON`.

**Governance**
- Site creation/closure harmonized between Real Estate, MDM and HRIS.

---

## 6. Workforce Structures

### 6.1 Jobs

**Definition**  
Jobs represent generic roles / profiles (e.g. “Warehouse Operative”, “Ops Supervisor”).

**Oracle object**  
- `Job`

**Authoritative sources**  
- People extract job catalog tabs: `Job Cat EN&FR`, `Job Ref EN&FR`.
- MAB `ActivitiesFunctions View.csv` for function/family classification.

**Key existing fields**
- `Job Category`, `Job Category Code`
- `Job Reference`, `Job REF code`
- `Job Title`
- `Function`, `Sub Function`

**Design rule**
> **1 Job REF code = 1 Oracle Job**

**Configuration instructions**
1. Build job master from job catalog:
   - Job Code = `Job REF code`.
   - Job Name = `Job Reference` / English label.
   - Job Category / Family from `Job Category`.
   - Function & Sub Function from MAB Activity/Function.
2. In FSM: *Manage Jobs*.
3. Align job sharing through `COMMON` data set.

**Governance**
- Job creation controlled by Global HR with inputs from LoBs.
- MAB Activities/Functions used for classification, not as structural objects.

---

### 6.2 Positions (optional)

**Definition**  
Positions represent concrete seats (role-in-context) that workers occupy.

**Oracle object**  
- `Position`

**Authoritative sources**  
- Local HR design; not directly from MAB.

**Design options**
- Phase 1: no position management (assign to Job + Department + Location).
- Phase 2+: create Positions as needed, mirroring org chart.

**Configuration instructions (if used)**
1. Define position naming standard (e.g. `[DeptCode]_[JobCode]_[Sequence]`).
2. In FSM: *Manage Positions*.
3. Optionally configure **Position Hierarchy** separate from Department Tree.

**Governance**
- Local HR coordinates with HRIS.

---

### 6.3 Grades & Grade Ladders

**Definition**  
Grades represent compensation levels; ladders represent progression paths.

**Oracle objects**  
- `Grade`
- `Grade Ladder`

**Authoritative sources**  
- Corporate compensation framework (outside MAB).

**Configuration instructions**
1. Define global grade structure and grade ladders per job family.
2. In FSM: *Manage Grades*, *Manage Grade Ladders*.
3. Attach grades/ladders to jobs and assignments as per policy.

**Governance**
- Controlled by Compensation & HR.

---

## 7. Trees & Hierarchies

### 7.1 Department Tree (HCM)

**Definition**  
Tree representing the hierarchy of **Departments (Organizational Units)**.

**Oracle object**  
- `Department Tree` using HCM Tree Manager.

**Authoritative source**  
- Hub OrganizationalStructure parent-child relationships (`ClientCode`, `ParentClientCode`).

**Configuration instructions**
1. In HCM: open **Tree Manager**.
2. Create a new Department Tree (e.g. `GEODIS_DEPT_TREE`).
3. Load nodes:
   - Node = Department (OU) from Section 3.3.
   - Parent Node = parent OU using `ParentClientCode`.
4. Effective dates must align with Department effective dates.

**Usage**
- Security
- Org charts
- Management reporting

---

### 7.2 Organization Tree (HCM)

**Definition**  
High-level structure combining Enterprise, Divisions, BUs and key Departments.

**Oracle object**  
- `Organization Tree`

**Authoritative sources**  
- Enterprise, Divisions, BUs, and possibly top-level Departments.

**Configuration instructions**
1. In Tree Manager, create `GEODIS_ORG_TREE`.
2. Level structure:
   - Level 0: Enterprise (GEODIS)
   - Level 1: Divisions (LoB L1)
   - Level 2: Business Units (Reporting Units)
   - Level 3+: Selected high-level Departments
3. Use this tree for **high-level navigation & reporting**.

---

### 7.3 GL Cost Center Hierarchy (Financials)

**Definition**  
Hierarchy of cost center segment values used for Finance reporting and allocations.

**Oracle object**  
- GL Account Hierarchy (in ERP Cloud)

**Authoritative source**  
- MAB Local SOUs and SOUs.

**Configuration instructions (GL)**
1. For each **Local SOU** defined as cost center value, assign it to a node in the hierarchy.
2. Build parents based on:
   - SOU Code (global)
   - Reporting Unit
   - LoB / Region
3. Maintain consistency between HCM costing rules and GL hierarchy.

**Usage**
- Financial reporting
- Allocations
- Costing analysis

---

## 8. End-to-end Example: Person → Dimensions

For each worker in the people extract, we can map to all dimensions:

- From `Organisational unit` / `Client code` → **Department** (OU) → Department Tree.
- From `RU CODE` → **Business Unit**.
- From `Legal Entity` → **Legal Entity / Legal Employer**.
- From `Geographical Unit` + `Location Center` → **Location**, **Country**, **LDG**.
- From job catalog (`Job REF code`) → **Job**.
- From SOU / Local SOU mappings → **Cost center** (GL segment) and SOU attributes.

This ensures **consistency** between HR structure, financial structure, and group reporting.

---

## 9. Governance & Change Management

### 9.1 Single Sources of Truth

- Enterprise: Corporate HRIS
- Legal Entities: MAB Local Legal Entities
- BUs: MAB Reporting Units
- Divisions: MAB Business Hierarchy
- Departments: Hub OrganizationalStructure (Org Units)
- SOU / Local SOU: MAB SOUs & Local SOUs
- Locations: Hub Legal Sites & addresses
- Jobs: HR job catalog + MAB Activities/Functions

### 9.2 Change process (simplified)

1. **Create / change in MAB / Hub** (Org Unit, SOU, Local SOU, RU, LE, Site).
2. **MDM validation**.
3. **Propagate to Oracle HCM / GL** via agreed integration or manual load.
4. **Verify** via reconciliation reports (counts, key ties).

### 9.3 Design principles

- HCM must **not** introduce structural codes that do not exist in MAB/Hub.
- Only **one primary HR hierarchy**: Department Tree (based on Org Units).
- Cost centers and financial hierarchies live in **GL**, referenced by HCM.
- SOU / Local SOU used for **analytical alignment**, not as visible HR structures.

---

## 10. Concrete Examples by Dimension

### 10.1 Example – Legal Entity

**MAB – Local Legal Entities (simplified row)**
- Local Legal Entity Code: `00053`
- Local Legal Entity Name: `GEODIS D&E Services France`
- Local Analytical Identification Code: `LE_FR_DE_00053`
- Legal Entity Code - DILITRUST: `FR_DE_LE01`
- Local CoA Identification Code: `FR_DE_COA01`
- Management Line Code: `ML_DE_FR`
- Activation Date: `2000-01-01`
- Deactivation Date: (blank)
- Status Calculated: `ACTIVATED`

**Oracle HCM – Legal Entity / Legal Employer**
- Legal Entity Name: `GEODIS D&E Services France`
- Legal Entity Identifier: `LE_FR_DE_00053`
- Legal Entity Code (optional): `00053`
- Legal Employer: `GEODIS D&E Services France` (same record flagged as Employer)
- DFF attributes:
  - DiliTrust Code: `FR_DE_LE01`
  - CoA ID: `FR_DE_COA01`
  - Management Line Code: `ML_DE_FR`

---

### 10.2 Example – Business Unit (Reporting Unit)

**MAB – Reporting Units View (simplified row)**
- Reporting Unit Code: `4DE123`
- Name - EN: `D&E France – Operations`
- Name - FR: `D&E France – Exploitation`
- Country: `FR`
- Currency: `EUR`
- LoB Code BFC - L4: `DE_FR_OPS`
- Activation Date: `2015-01-01`
- Status Calculated: `ACTIVATED`

**Oracle HCM – Business Unit**
- BU Name: `D&E France – Operations`
- BU Code (optional): `4DE123`
- Country: `FR`
- Default Set: `COMMON`
- Division (Org Tree parent): `Distribution & Express` (LoB L1)

---

### 10.3 Example – Department (Organizational Unit)

**Hub – OrganisationalStructure JSON (simplified node)**
- ClientCode: `300145`
- ShortName: `FR – D&E – Tours Hub`
- ParentClientCode: `300100`
- IsActive: `Y`
- ManagerUniqueID: `GEO123456`
- CostCenterClientCodes: `["FR_DETOURS_001", "FR_DETOURS_002"]`

**People extract**
- Organisational unit: `FR – D&E – Tours Hub`
- Client code: `300145`

**Oracle HCM – Department**
- Department Code: `300145`
- Department Name: `FR – D&E – Tours Hub`
- Parent Department: `300100` (FR – D&E France)
- Department Set: `COMMON`
- Manager: person corresponding to `GEO123456` once workers are loaded
- Default Cost Centers (via costing rules): `FR_DETOURS_001`, `FR_DETOURS_002`

**Department Tree snippet**
```text
GEODIS (Enterprise)
  Distribution & Express (Division)
    D&E France – Operations (BU)
      FR – D&E France (Department 300100)
        FR – D&E – Tours Hub (Department 300145)
```

---

### 10.4 Example – Location (Site)

**Site master (from Hub + MAB)**
- Site ID: `FR_TOUL_TOURS01`
- Location Center: `FR–TOURS–SITE1`
- Country: `FR`
- City: `Tours`
- Postal Code: `37000`
- Address Line 1: `12 Rue de la Logistique`
- UN LOCODE: `FRTOU`

**Oracle HCM – Location**
- Location Code: `FR-TOURS-SITE1`
- Location Name: `FR – Tours – Site 1`
- Location Set: `COMMON`
- Country: `FR`
- Address Line 1: `12 Rue de la Logistique`
- Postal Code: `37000`
- City: `Tours`

---

### 10.5 Example – SOU and Local SOU to Cost Center

**MAB – SOUs View (simplified row)**
- SOU Code: `DETOURS01`
- Name: `D&E – Tours Operations`
- Type: `Operational`
- Reporting Unit Code: `4DE123`
- Legal Entity Code - DILITRUST: `FR_DE_LE01`
- Alpha-2 Country Code: `FR`
- UN LOCODE: `FRTOU`
- Activation Date: `2015-01-01`
- Status Calculated: `ACTIVATED`

**MAB – Local SOUs (two rows)**
1. Local SOU Code: `FR_DETOURS_001`
   - Local Analytical Identification Code: `CC_FR_DETOURS_001`
   - Name: `D&E Tours – Operations`
   - SOU Code: `DETOURS01`
   - Local Legal Entity Code: `00053`
2. Local SOU Code: `FR_DETOURS_002`
   - Local Analytical Identification Code: `CC_FR_DETOURS_002`
   - Name: `D&E Tours – Administration`
   - SOU Code: `DETOURS01`
   - Local Legal Entity Code: `00053`

**Oracle GL – Cost Center segment values**
- Segment Value: `FR_DETOURS_001`
  - Description: `D&E Tours – Operations`
  - Attributes: SOU = `DETOURS01`, LE = `00053`, Country = `FR`
- Segment Value: `FR_DETOURS_002`
  - Description: `D&E Tours – Administration`
  - Attributes: SOU = `DETOURS01`, LE = `00053`, Country = `FR`

**GL Cost Center Hierarchy snippet**
```text
DE – Distribution & Express (parent node)
  D&E France (node)
    D&E – Tours (SOU DETOURS01)
      FR_DETOURS_001 (Ops cost center)
      FR_DETOURS_002 (Admin cost center)
```

---

### 10.6 Example – Job

**Job catalog (simplified row)**
- Job REF code: `DE_OPS_SUP_01`
- Job Reference: `Operations Supervisor`
- Job Category: `Operations Management`
- Function: `Operations`
- Sub Function: `Hub Operations`

**Oracle HCM – Job**
- Job Code: `DE_OPS_SUP_01`
- Job Name: `Operations Supervisor`
- Job Family / Category: `Operations Management`
- DFFs:
  - Function: `Operations`
  - Sub Function: `Hub Operations`

---

### 10.7 Example – Person Assignment across Dimensions

**People extract – key structural fields for Employee X (fictional)**
- Organisational unit: `FR – D&E – Tours Hub`
- Client code: `300145`
- Region: `FRA - FRANCE`
- LOB: `DE`
- Legal Entity: `GEODIS D&E Services France`
- RU CODE: `4DE123`
- Contract SOU - Code: `DETOURS01`
- Location Center: `FR–TOURS–SITE1`
- Job Reference: `DE_OPS_SUP_01`

**Oracle HCM – Assignment for Employee X**
- Business Unit: `D&E France – Operations` (from RU `4DE123`)
- Legal Employer: `GEODIS D&E Services France`
- Legal Entity: `GEODIS D&E Services France`
- Department: `FR – D&E – Tours Hub` (Code `300145`)
- Location: `FR – Tours – Site 1`
- Job: `Operations Supervisor` (Code `DE_OPS_SUP_01`)
- Grade: as per comp policy
- Default Cost Center: `FR_DETOURS_001` (via Local SOU for DETOURS01)

This example shows how **all dimensions come together** for a single worker.

---

*End of document – this is the master reference for Oracle HCM structural dimensions at GEODIS, including concrete examples to guide configuration and data migration.*

