# GEODIS MDM MAB to Oracle HCM Repository Mapping
## Data Model Analysis & Field Mapping Guide

---

**Project:** GEODIS New HCM - AMARIS
**Document:** MDM to HCM Repository Mapping
**Version:** 1.1
**Date:** 2025-11-29
**Reference:** Position Paper - Organizational MDM (July 2023, V3)

---

## 1. MDM MAB Data Model Summary

### 1.1 Available MDM Files (15 Files)

| # | MDM File | Records | Description | HCM Relevance |
|---|----------|---------|-------------|---------------|
| 1 | Legal Entities View.csv | 500+ | Legal company information | HIGH - Legal Entity |
| 2 | Legal Sites.csv | 1000+ | Physical location addresses | HIGH - Location |
| 3 | SOUs View.csv | 2000+ | Strategic Operating Units | HIGH - Department/Location |
| 4 | Business Hierarchy.csv | 45 | Lines of Business hierarchy | MEDIUM - Division |
| 5 | Managerial Hierarchy.csv | 500+ | Management structure | HIGH - Department Tree |
| 6 | Reporting Units View.csv | 200+ | Financial reporting units | MEDIUM - Cost Center |
| 7 | Local Legal Entities.csv | 500+ | Local LE mappings | MEDIUM - Reference |
| 8 | Local SOUs.csv | 1000+ | Local SOU mappings | MEDIUM - Reference |
| 9 | Systems.csv | 30+ | ERP/Applications | LOW - Integration |
| 10 | ActivitiesFunctions View.csv | 100+ | Job functions/activities | HIGH - Job Family/Function |
| 11 | Local ActivitiesFunctions View.csv | 500+ | Local function mappings | MEDIUM - Job |
| 12 | MAB Products Hierarchy.csv | 100+ | Product/Service hierarchy | LOW - Not HCM |
| 13 | Local Products Hierarchy.csv | 1000+ | Local product mappings | LOW - Not HCM |
| 14 | Local Analytical Mapping IDs.csv | 100+ | Analytics reference | LOW - Reporting |
| 15 | Local CoA Mapping IDs.csv | 100+ | Chart of Accounts | LOW - Finance |

---

### 1.2 MDM Target IT Architecture

**Source:** Position Paper - Organizational MDM (July 2023)

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  LEGAL SOURCE   │     │      MDM        │     │ SLAVE APPS      │
│  (Dilitrust)    │────▶│   (EBX + BAW)   │────▶│ (G-Talent+,     │
│                 │     │                 │     │  EPM, Payroll)  │
└─────────────────┘     └────────┬────────┘     └─────────────────┘
                                 │
                                 ▼
                        ┌─────────────────┐
                        │   DATA LAYER    │
                        │  (Central Hub)  │
                        └─────────────────┘
```

| Component | Tool | Purpose |
|-----------|------|---------|
| Source of Truth | **Dilitrust** | Legal entities management |
| MDM Platform | **EBX (TIBCO)** | Master data centralization & quality |
| BPM Workflow | **BAW** | Lifecycle management of local referential |
| Data Hub | **Data Layer** | Central data distribution |
| HR System | **G-Talent+** | HR/HCM application (being replaced) |
| Finance | **EPM (Oracle)** | Financial reporting |

---

### 1.3 SOU - The Cornerstone Concept

The **Smallest Operating Unit (SOU)** is the pivot table connecting all organizational hierarchies:

```
┌─────────────────┐                              ┌─────────────────┐
│ LEGAL HIERARCHY │                              │ GEOGRAPHICAL/   │
│                 │                              │ LOBS HIERARCHY  │
│    L1 ─ LE      │     ┌─────────────────┐     │  REGION         │
│                 │     │                 │     │  SUB-REGION     │
│  LEGAL ENTITIES │◀────│      SOU        │────▶│  COUNTRY        │
│                 │     │   (PIVOT)       │     │  LoBs           │
└─────────────────┘     └────────┬────────┘     └─────────────────┘
                                 │
        ┌────────────────────────┼────────────────────────┐
        ▼                        ▼                        ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│ BFC LOBS        │     │ MANAGERIAL      │     │ BUSINESS        │
│ HIERARCHIES     │     │ HIERARCHY       │     │ HIERARCHY       │
│ L1-L3 + RU      │     │ L1-L7 + REGIONS │     │ L1-L2 + LoBs    │
│ REPORTING UNITS │     │                 │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

**SOU Definition:**
- Unique combination of **Line of Business + Local Geography**
- Lowest level for **P&L and Balance Sheet** delivery
- Must be **Operational** (profit center) AND receive **allocations** (cost center)

**SOU Types:**
| Type | Code | Description | Example |
|------|------|-------------|---------|
| Operational | O | P&L per D&E Agency, RT Branch, CL Warehouse, FF Branch, SCO site | ATLOF01 |
| Holding & Overhead | H | P&L for LoB/Region HQ, Real Estate, Corporate | PARHO01 |
| Technical | T | Budget entries for consolidation | TOPASIA |

**SOU Code Structure:**
```
9SBOL01
│││││└─ 2 digits: Distinguish SOUs at same location
││││└── LoB: D=D&E, R=ERN, F=FF, L=CL, S=SCO, C=Corporate
│││└─── Type: O=Operational, H=Holding, T=Technical
└└└──── 3 chars: City location (UN LOCODE)
```

---

### 1.4 MDM Tables Overview (from EBX)

| Table Name | Application Source | Update Method | Update System | Responsible |
|------------|-------------------|---------------|---------------|-------------|
| **SOUs** | Creation in EBX | Manual | BAW or EBX | LRDS & GDDS |
| **Managerial Hierarchy** | Creation in EBX | Manual | BAW or EBX | LRDS & GDDS |
| **Business Hierarchy** | Creation in EBX | Manual | EBX | LoB LRDS & GDDS |
| **Legal Entities** | Dilitrust | Automatic | Dilitrust | Legal dept & GDDS |
| **Local SOUs** | ERP | Manual | BAW | LRDS |
| **Local Legal Entities** | ERP | Manual | BAW | LRDS |
| **Reporting Units** | BFC Finance | Semi-automatic | BFC Finance | GDDS |
| **Reporting Units Geodis** | BFC Finance | Automatic | BFC Finance | GDDS |
| **LoB BFC Hierarchy** | BFC Finance | Manual | BFC Finance | GDDS |
| **Geographical Regions** | Geodata | Automatic | Geodata | EBX IT Team |
| **Countries** | Geodata | Automatic | Geodata | EBX IT Team |
| **Country Subdivisions** | Geodata | Automatic | Geodata | EBX IT Team |
| **UN LOCODE Locations** | Geodata | Automatic | Geodata | EBX IT Team |

---

### 1.5 MDM Governance Roles

| Level | Role | Responsibilities |
|-------|------|------------------|
| **GROUP** | **GDDO** (Group Data Domain Owner) | Accountable for data policies, access, security, quality |
| **GROUP** | **GDDS** (Group Data Domain Steward) | Define governance procedures, quality controls, key management |
| **LOCAL** | **LRDS** (LoB Region Data Stewards) | Execute MDM at local level, map local referential with MAB |

**Governance per Table:**
| Table | GDDS Validation | GDDO Validation |
|-------|-----------------|-----------------|
| SOUs | YES | YES |
| Managerial Hierarchy | YES | YES |
| Business Hierarchy | - | - (No workflow needed) |
| Legal Entities | - | - (Legal dept responsible) |
| Local SOUs | - | - (LRDS requested suppression during project) |
| Local Legal Entities | - | - (LRDS requested suppression during project) |
| Reporting Units Geodis | - | - (GDDS responsible, no workflow) |

---

### 1.6 Slave Applications Integration Matrix

| Table | EPM | G-Talent+ | Qliksense | LDAP | Jira | BAPS | Geofleet | Iporta | Cubicus | CCA Report |
|-------|-----|-----------|-----------|------|------|------|----------|--------|---------|------------|
| SOUs | YES | YES | YES | YES | YES | YES | YES | YES | YES | YES |
| Managerial Hierarchy | YES | - | - | YES | YES | YES | YES | YES | YES | YES |
| Business Hierarchy | YES | YES | - | - | - | - | - | - | - | - |
| Legal Entities | YES | Preferable* | - | - | - | YES | YES | YES | YES | YES |
| Local SOUs | YES | YES | YES | - | - | YES | YES | YES | YES | YES |
| Local Legal Entities | - | YES | - | - | - | YES | YES | YES | YES | YES |
| Reporting Units Geodis | YES | YES | YES | YES | YES | YES | YES | YES | YES | YES |

*G-Talent+ Legal Entities: Under discussion with iTHR & GEOBUS

---

### 1.7 Data Quality Metrics (Current State)

| Table | Errors | Impact on EPM |
|-------|--------|---------------|
| Reporting Units | 151 | **No impact** - 128 linked to Managerial Hierarchy mapping |
| Reporting Units GEODIS | 94 | **No impact** - MDM rules to be updated |
| SOUs | 74 | **No impact** - 21 Technical SOUs + 53 CL embedded FF |
| **Total** | **319** | Most errors linked to MDM rules, not data quality |

---

## 2. MDM Data Model Structure

### 2.1 Legal Entities View

**File:** `Legal Entities View.csv`
**Delimiter:** Semicolon (;)

| MDM Column | Data Type | Sample Value | Description |
|------------|-----------|--------------|-------------|
| Legal Entity Code - EBX | String | FR005 | Internal EBX code |
| Legal Entity Code - DILITRUST | String | 200001 | Dilitrust reference code |
| Legal Entity Name | String | GEODIS SA | Official legal name |
| Country | String | FR | ISO 2-letter country code |
| Currency | String | EUR | ISO currency code |
| Registration ID | String | 542 084 322 | Company registration number |
| Code APE/NAF | String | 7010Z | Activity code (France) |
| Legal form | String | Société anonyme | Legal structure type |
| Legal representative | String | Mme MARIE-CHRISTINE LOMBARD | Company officers |
| Registration Date | Date | 1926-07-25 | Date of incorporation |
| Shareholder equity | Number | 404461760 | Capital amount |
| City of registration | String | NANTERRE | Registration location |
| Tax ID | String | FR60542084322 | Tax identification number |
| Consolidation method | String | Full consolidation | Accounting method |
| Activity status | String | En activité | Active/Inactive |
| Address | String | 26 Quai Charles Pasqua | Registered address |
| DUNS code | String | 275146629 | D&B identifier |
| LoB Owner | String | - | Line of Business |
| Activation Date | Date | 2021-01-01 | MDM activation |
| Deactivation Date | Date | - | MDM deactivation |
| Status Calculated | String | ACTIVATED | Current status |

---

### 2.2 Legal Sites

**File:** `Legal Sites.csv`
**Delimiter:** Semicolon (;)

| MDM Column | Data Type | Sample Value | Description |
|------------|-----------|--------------|-------------|
| Legal Site code Dilitrust | String | 10a77tr-3765oo9 | Site identifier |
| Legal Site name | String | GEODIS Australia Pty Ltd | Site name |
| Legal Entity code Dilitrust | String | 300222 | Parent legal entity |
| Adress field street | String | 501 - 503 Dowling Street | Street address |
| Adress field city | String | Wendouree | City |
| Adress field province | String | TBD | State/Province |
| Adress field postal code | String | Vic, 3355 | Postal code |
| Address Field Country | String | AU | Country code |
| Legal site type | String | branch-office | Site classification |
| Legal site code DUNS | String | 000000000 | DUNS number |
| LoB Owner | String | - | Line of Business |

---

### 2.3 SOUs View (Strategic Operating Units)

**File:** `SOUs View.csv`
**Delimiter:** Semicolon (;)

| MDM Column | Data Type | Sample Value | Description |
|------------|-----------|--------------|-------------|
| SOU Code | String | 9SBOL01 | SOU identifier |
| SOU Digits | String | 01 | Sub-unit number |
| Name | String | Satolas 3 | SOU name |
| Type | String | Operational | SOU type |
| Reporting Unit Code | String | TA46 | Reporting unit |
| BOF site code | String | LOG133 | BOF reference |
| Managerial Parent Code | String | FRBURE | Mgmt hierarchy parent |
| Management Line Code | String | FRCL - FRANCE CL | Management line |
| Business Parent Code | String | CLFR | Business hierarchy |
| Alpha-2 Country Code | String | FR | Country |
| UN LOCODE | String | FR9SB | UN location code |
| Legal Entity Code - DILITRUST | String | 200384 | Legal entity |
| Country Subdivision Code | String | FR38 | Region code |
| Historical LoB Code | String | CL | Historical LoB |
| Site ID | String | 910 | Site identifier |
| SOU Responsible | String | x@geodis.com | Contact email |
| Activation Date | Date | 2021-01-01 | Activation |
| Deactivation Date | Date | - | Deactivation |
| Status Calculated | String | ACTIVATED | Status |

---

### 2.4 Business Hierarchy (Lines of Business)

**File:** `Business Hierarchy.csv`
**Delimiter:** Semicolon (;)

| MDM Column | Data Type | Sample Value | Description |
|------------|-----------|--------------|-------------|
| LoB Code | String | CL | Line of Business code |
| Name | String | GLOBAL CONTRACT LOGISTICS | Full name |
| Short name | String | GCL | Abbreviation |
| Hierarchy level | String | L1, L2, L3, L4 | Level in hierarchy |
| Parent Code | String | PARENT | Parent LoB |
| Activation Date | Date | 2021-01-01 | Activation |
| Deactivation Date | Date | - | Deactivation |
| Status Calculated | String | ACTIVATED | Status |

**Hierarchy Structure:**
```
PARENT (GEODIS)
├── CL (Contract Logistics) - L1
│   ├── CLAM (CL Americas) - L2
│   ├── CLAP (CL APAC) - L2
│   ├── CLFR (CL France) - L2
│   └── CLNE (CL Europe) - L2
├── FF (Freight Forwarding) - L1
│   ├── FFAM (FF Americas) - L2
│   ├── FFAP (FF APAC) - L2
│   └── FFNE (FF Europe) - L2
├── DE (Distribution & Express) - L1
├── RT (European Road Network) - L1
├── NO (Corporate) - L1
├── TOF (Trans-O-Flex) - L1
├── UF (Urban Fox) - L1
└── UP (Upply) - L1
```

---

### 2.5 Managerial Hierarchy

**File:** `Managerial Hierarchy.csv`
**Delimiter:** Semicolon (;)

| MDM Column | Data Type | Sample Value | Description |
|------------|-----------|--------------|-------------|
| Managerial Unit Code | String | AM | Regional code |
| Name | String | AMERICAS | Full name |
| Short name | String | AMS | Abbreviation |
| Hierarchy level | String | L1-L7 | Level (up to 7) |
| Parent Code | String | PARENT | Parent unit |
| Activation Date | Date | 2021-01-01 | Activation |
| Deactivation Date | Date | - | Deactivation |
| Status Calculated | String | ACTIVATED | Status |

---

### 2.6 Activities/Functions View

**File:** `ActivitiesFunctions View.csv`
**Delimiter:** Semicolon (;)

| MDM Column | Data Type | Sample Value | Description |
|------------|-----------|--------------|-------------|
| MAB Activity/Function Code | String | 1CUS0 | Function code |
| English Name | String | Customer Service | Name (EN) |
| French Name | String | Relations Clients | Name (FR) |
| English Definition | String | Post-Sales administration... | Description (EN) |
| French Definition | String | Administration après-vente... | Description (FR) |
| Hierarchy level | String | L4, L5 | Level |
| MAB Activity/Function Parent Code | String | 3ACT | Parent code |
| Activation Date | Date | 2021-01-01 | Activation |
| Deactivation Date | Date | - | Deactivation |
| Status Calculated | String | ACTIVATED | Status |

---

## 3. Oracle HCM Repository Mapping

### 3.1 Legal Entity Repository

**Excel Sheet:** `Legal Entity`

| HCM Field | MDM Source | MDM Column | Transformation |
|-----------|------------|------------|----------------|
| * Country | Legal Entities View | Country | Direct mapping |
| * Name (EN) | Legal Entities View | Legal Entity Name | Direct mapping |
| * Legal entity identifier | Legal Entities View | Legal Entity Code - DILITRUST | Direct mapping |
| * Start Date | Legal Entities View | Registration Date or Activation Date | Date format |
| End Date | Legal Entities View | Deactivation Date | Date format |
| * Payroll Statutory Unit | - | - | Set to "Yes" for active LEs |
| * Legal Employer | - | - | Set to "Yes" for active LEs |
| * Legal Address Associated | Legal Entities View | Address | Parse address |
| Place of Registration | Legal Entities View | City of registration | Direct mapping |
| *Legal Entity Registration Number | Legal Entities View | Registration ID | Direct mapping |
| * Unit Registration Number | Legal Entities View | Tax ID | Direct mapping |

**Sample Mapping Logic:**
```python
# Legal Entity Mapping
hcm_legal_entity = {
    "Country": mdm["Country"],
    "Name_EN": mdm["Legal Entity Name"],
    "Legal_Entity_ID": mdm["Legal Entity Code - DILITRUST"],
    "Start_Date": parse_date(mdm["Registration Date"]) or parse_date(mdm["Activation Date"]),
    "End_Date": parse_date(mdm["Deactivation Date"]) if mdm["Status Calculated"] == "DEACTIVATED" else None,
    "PSU": "Yes" if mdm["Status Calculated"] == "ACTIVATED" else "No",
    "Legal_Employer": "Yes" if mdm["Status Calculated"] == "ACTIVATED" else "No",
    "Registration_Number": mdm["Registration ID"],
    "Tax_ID": mdm["Tax ID"],
    "Place_Registration": mdm["City of registration"],
}
```

---

### 3.2 Location Repository

**Excel Sheet:** `Location`

| HCM Field | MDM Source | MDM Column | Transformation |
|-----------|------------|------------|----------------|
| Location Code | Legal Sites / SOUs | Legal Site code Dilitrust / SOU Code | Direct mapping |
| Location Name | Legal Sites / SOUs | Legal Site name / Name | Direct mapping |
| Country | Legal Sites / SOUs | Address Field Country / Alpha-2 Country Code | Direct mapping |
| Address Line 1 | Legal Sites | Adress field street | Direct mapping |
| City | Legal Sites | Adress field city | Direct mapping |
| State/Province | Legal Sites | Adress field province | Map to Oracle state codes |
| Postal Code | Legal Sites | Adress field postal code | Direct mapping |
| Location Type | Legal Sites | Legal site type | Map to Oracle values |
| Legal Entity | Legal Sites | Legal Entity code Dilitrust | Lookup to Legal Entity |

**Location Type Mapping:**
| MDM Value | Oracle HCM Value |
|-----------|------------------|
| etablissement-principal | Head Office |
| etablissement-secondaire | Branch |
| branch-office | Branch |
| localisation-de-lactivite | Work Site |

---

### 3.3 Division Repository

**Excel Sheet:** `Division`

| HCM Field | MDM Source | MDM Column | Transformation |
|-----------|------------|------------|----------------|
| Division Code | Business Hierarchy | LoB Code | Direct mapping |
| Division Name | Business Hierarchy | Name | Direct mapping |
| Division Short Name | Business Hierarchy | Short name | Direct mapping |
| Status | Business Hierarchy | Status Calculated | Map ACTIVATED/DEACTIVATED |
| Start Date | Business Hierarchy | Activation Date | Date format |
| End Date | Business Hierarchy | Deactivation Date | Date format |

**Recommended Divisions (L1 Level):**
| Code | Name | Description |
|------|------|-------------|
| CL | Contract Logistics | Global Contract Logistics |
| FF | Freight Forwarding | Global Freight Forwarding |
| DE | Distribution & Express | Distribution & Express |
| RT | European Road Network | Road Transport |
| NO | Corporate | Non-Allocated & Corporate |
| TOF | Trans-O-Flex | Trans-O-Flex Operations |

---

### 3.4 Business Unit Repository

**Excel Sheet:** `Business Unit`

| HCM Field | MDM Source | MDM Column | Transformation |
|-----------|------------|------------|----------------|
| * Name | Derived | Combination | LoB + Region pattern |
| Location | SOUs View | Name | First operational location |
| Manager | - | - | Manual entry required |
| * Default Set | - | - | Set to "Common Set" |

**Recommended Business Unit Design:**
Based on MDM Management Line structure:

| BU Code | BU Name | Primary Legal Entity | Region | LoB |
|---------|---------|---------------------|--------|-----|
| BU_FRCL | France Contract Logistics | GEODIS CL France entities | France | CL |
| BU_FRFF | France Freight Forwarding | GEODIS FF France | France | FF |
| BU_FRDE | France Distribution & Express | GEODIS D&E entities | France | DE |
| BU_AMCL | Americas Contract Logistics | GEODIS Logistics LLC | Americas | CL |
| BU_AMFF | Americas Freight Forwarding | GEODIS USA | Americas | FF |
| BU_APCL | APAC Contract Logistics | GEODIS APAC entities | APAC | CL |
| BU_APFF | APAC Freight Forwarding | GEODIS APAC entities | APAC | FF |
| BU_NECL | Europe Contract Logistics | GEODIS NE CL entities | Europe | CL |
| BU_NEFF | Europe Freight Forwarding | GEODIS NE FF entities | Europe | FF |
| BU_RT | Road Transport Europe | GEODIS RT entities | Europe | RT |
| BU_CORP | Corporate | GEODIS SA | Global | NO |

---

### 3.5 Department Repository

**Excel Sheet:** `Department`

| HCM Field | MDM Source | MDM Column | Transformation |
|-----------|------------|------------|----------------|
| Department Code | Managerial Hierarchy / SOUs | Managerial Unit Code / SOU Code | Direct mapping |
| Department Name | Managerial Hierarchy / SOUs | Name | Direct mapping |
| Parent Department | Managerial Hierarchy | Parent Code | Lookup |
| Location | SOUs View | UN LOCODE | Lookup to Location |
| Business Unit | SOUs View | Management Line Code | Map to BU |
| Manager | SOUs View | SOU Responsible | Parse email |

**Department Hierarchy Design:**
```
Enterprise (GEODIS)
├── Americas (AM) - Region
│   ├── AMF (FF Americas)
│   ├── AML (CL Americas)
│   └── AMN (NIND Americas)
├── APAC (AP) - Region
│   ├── APM (APAC & ME)
│   └── APMOOS (Urban Fox)
├── Europe (NE) - Region
│   ├── NECL (CL Europe)
│   ├── NEFF (FF Europe)
│   └── NETOF (Trans-O-Flex)
├── France (FR) - Region
│   ├── FRCL (CL France)
│   ├── FRFF (FF France)
│   └── DE (D&E France)
└── Corporate (NO)
    ├── NOCORP
    └── NORE
```

---

### 3.6 Job Family Repository

**Excel Sheet:** `Job Family`

| HCM Field | MDM Source | MDM Column | Transformation |
|-----------|------------|------------|----------------|
| Job Family Code | ActivitiesFunctions View | MAB Activity/Function Code (L2-L3) | Direct mapping |
| Job Family Name | ActivitiesFunctions View | English Name | Direct mapping |
| Description | ActivitiesFunctions View | English Definition | Direct mapping |

**Recommended Job Families from MDM:**
| Code | Job Family Name | Based on MAB Activity |
|------|-----------------|----------------------|
| JF_OPS | Operations | 3OPS, 1WH00, 1LN00 |
| JF_CUS | Customer Service | 1CUS0 |
| JF_FRT | Freight Administration | 1FG00 |
| JF_FIN | Finance | 2FIN0 |
| JF_HR | Human Resources | 2HR00 |
| JF_IT | Information Technology | 2IT00 |
| JF_SAL | Sales & Commercial | 2SAL0 |
| JF_QUA | Quality & Compliance | 2QUA0 |
| JF_4PL | 4PL Operations | 14PL0 |

---

### 3.7 Job Repository

**Excel Sheet:** `Job`

| HCM Field | MDM Source | MDM Column | Transformation |
|-----------|------------|------------|----------------|
| Job Code | Local ActivitiesFunctions | Local Activity/Function Code | Direct mapping |
| Job Name | Local ActivitiesFunctions | Name | Direct mapping |
| Job Family | Local ActivitiesFunctions | MAB Activity/Function Code | Lookup to Job Family |
| Effective Start Date | - | - | Implementation go-live |
| Active Status | - | - | Default "Active" |

---

### 3.8 Legislative Data Group Repository

**Excel Sheet:** `Legislative Data Group`

| HCM Field | MDM Source | MDM Column | Transformation |
|-----------|------------|------------|----------------|
| LDG Name | Derived | - | "GEODIS " + Country Name |
| Country | Legal Entities View | Country (distinct) | Direct mapping |
| Currency | Legal Entities View | Currency | Direct mapping |
| Status | - | - | "Active" |

**LDGs to Create (based on distinct countries in Legal Entities):**
| LDG Name | Country | Currency | Legal Entities Count |
|----------|---------|----------|---------------------|
| GEODIS France | FR | EUR | 200+ |
| GEODIS USA | US | USD | 50+ |
| GEODIS Germany | DE | EUR | 20+ |
| GEODIS UK | GB | GBP | 15+ |
| GEODIS Netherlands | NL | EUR | 10+ |
| GEODIS China | CN | CNY | 10+ |
| GEODIS Australia | AU | AUD | 5+ |
| GEODIS Singapore | SG | SGD | 5+ |
| GEODIS Japan | JP | JPY | 5+ |
| GEODIS India | IN | INR | 5+ |
| *[... other countries]* | | | |

---

## 4. Data Transformation Rules

### 4.1 Date Formats
```
MDM Format: YYYY-MM-DD (e.g., 2021-01-01)
Oracle HCM Format: DD-MMM-YYYY (e.g., 01-JAN-2021)

Transformation:
    input_date = "2021-01-01"
    output_date = datetime.strptime(input_date, "%Y-%m-%d").strftime("%d-%b-%Y").upper()
```

### 4.2 Status Mapping
| MDM Status | Oracle HCM Status |
|------------|-------------------|
| ACTIVATED | Active |
| DEACTIVATED | Inactive |

### 4.3 Country Code Standardization
MDM uses ISO 3166-1 alpha-2 codes which are Oracle HCM compatible.

### 4.4 Special Characters
- Remove leading/trailing spaces
- Convert special characters (é, è, ë, etc.) for non-multilingual fields
- Preserve special characters for French/German names where supported

---

## 5. Implementation Recommendations

### 5.1 Data Quality Checks Required

| Check | MDM Field | Issue | Action |
|-------|-----------|-------|--------|
| Missing Province | Legal Sites | "TBD" values | Lookup or manual entry |
| Duplicate Names | Legal Entities | Same name different codes | Add identifier suffix |
| Invalid Characters | All name fields | Non-ASCII in codes | Clean or encode |
| Missing Parents | Hierarchies | Orphan records | Verify parent exists |

### 5.2 Migration Sequence

1. **Phase 1: Foundation**
   - Country Codes (validate MDM countries exist in Oracle)
   - Legislative Data Groups (create per country)
   - Legal Entities (from Legal Entities View)

2. **Phase 2: Organization**
   - Divisions (from Business Hierarchy L1)
   - Business Units (derived from Management Lines)
   - Locations (from Legal Sites + SOUs)
   - Departments (from Managerial Hierarchy)

3. **Phase 3: Workforce**
   - Job Families (from Activities/Functions L2-L3)
   - Jobs (from Local Activities/Functions)
   - Positions (if using position management)

### 5.3 Data Gaps (Not in MDM)

The following HCM repositories have no direct MDM source:

| Repository | Action Required |
|------------|-----------------|
| Grades | Design new grading structure |
| Position | Design if using position management |
| Person Types | Use Oracle defaults |
| Assignment Status | Use Oracle defaults |
| Actions & Reasons | Configure standard Oracle actions |
| Security Roles | Design role matrix |

---

## 6. Sample Python Transformation Script

```python
# Sample transformation logic for Legal Entity

import pandas as pd
from datetime import datetime

def transform_legal_entities(mdm_file):
    # Read MDM file
    df = pd.read_csv(mdm_file, delimiter=';', encoding='utf-8')

    # Filter active entities only
    df = df[df['Status Calculated'] == 'ACTIVATED']

    # Transform to HCM format
    hcm_data = []
    for _, row in df.iterrows():
        hcm_record = {
            'Country': row['Country'],
            'Name_EN': row['Legal Entity Name'],
            'Legal_Entity_ID': row['Legal Entity Code - DILITRUST'],
            'Start_Date': format_date(row.get('Registration Date') or row['Activation Date']),
            'End_Date': '',
            'PSU': 'Yes',
            'Legal_Employer': 'Yes',
            'Legal_Address': row['Address'],
            'Place_Registration': row['City of registration'],
            'Registration_Number': row['Registration ID'],
            'Tax_ID': row['Tax ID'],
        }
        hcm_data.append(hcm_record)

    return pd.DataFrame(hcm_data)

def format_date(date_str):
    if pd.isna(date_str) or not date_str:
        return ''
    try:
        dt = datetime.strptime(str(date_str)[:10], '%Y-%m-%d')
        return dt.strftime('%d-%b-%Y').upper()
    except:
        return ''
```

---

## 7. Field Mapping Summary Tables

### 7.1 Organization Structure Mapping

| HCM Repository | Primary MDM Source | Secondary Source | Coverage |
|----------------|-------------------|------------------|----------|
| Legal Entity | Legal Entities View | - | 100% |
| Location | Legal Sites | SOUs View | 90% |
| Division | Business Hierarchy (L1) | - | 100% |
| Business Unit | Management Line (derived) | SOUs View | 80% |
| Department | Managerial Hierarchy | SOUs View | 90% |
| Department Tree | Managerial Hierarchy | - | 100% |
| LDG | Legal Entities View (countries) | - | 100% |

### 7.2 Workforce Structure Mapping

| HCM Repository | Primary MDM Source | Coverage | Notes |
|----------------|-------------------|----------|-------|
| Job Family | ActivitiesFunctions (L2-L3) | 80% | May need additions |
| Job Function | ActivitiesFunctions (L4) | 70% | Use Oracle defaults for rest |
| Job | Local ActivitiesFunctions | 60% | Operational jobs covered |
| Grade | Not in MDM | 0% | Design required |
| Position | Not in MDM | 0% | Design required |

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-11-27 | HCM Team | Initial mapping document |
| 1.1 | 2025-11-29 | HCM Team | Added Position Paper content: IT Architecture, SOU cornerstone concept, MDM Tables overview, Governance roles, Slave applications matrix, Data quality metrics |

---

*This mapping document should be reviewed with business stakeholders to validate transformations and fill data gaps.*

---

## Appendix: Reference Documents

| Document | Version | Date | Description |
|----------|---------|------|-------------|
| Position Paper - Organizational MDM | V3 | September 2023 | MDM MAB structure and governance |
| MDM MAB.pdf | V3 | July 2023 | Organizations & Geographies data domain |
| LOB BFC Hierarchy.xlsm | - | - | Detailed LoB BFC hierarchy |
| Managerial hierarchies.xlsx | - | - | Detailed managerial hierarchies |
| List of LAIC codes.xlsm | - | - | Local Analytical Identification Codes |
