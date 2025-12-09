# MDM HR Files Analysis Report
**Date:** 2025-11-29
**Path:** `02 - Define\01 - Repositories\02 - MDM HR`

---

## Executive Summary

| Metric | Value |
|--------|-------|
| Total Files | 12 (8 CSV + 4 JSON) |
| Total Size | ~114 MB |
| Total Records | ~1,233,417 |

---

## Files Inventory

| File | Size | Records | Columns | Type |
|------|------|---------|---------|------|
| HubLibraries20251119_1141.csv | 36 MB | 488,291 | 6 | CSV |
| Organisations.csv | 20 MB | 395,174 | 6 | CSV |
| SDD_PPC_LEVELS.csv | 16 MB | 87,994 | 20 | CSV |
| HubLibraries_Departments.json | 15 MB | 89,585 | 6 | JSON |
| JobRepositoryNewIE.csv | 9 MB | 7,865 | 26 | CSV |
| HubLibraries_LegalSitesAdressses.json | 6 MB | 38,432 | 6 | JSON |
| KeyPropertiesNewIE.csv | 6 MB | 79,801 | 6 | CSV |
| GenericLibrary.csv | 1.5 MB | 18,606 | 6 | CSV |
| HubProductValuesListLibrary.csv | 1 MB | 26,399 | 4 | CSV |
| HubLibraries_LegalStructure.json | 1 MB | ~10,000 | 6 | JSON |
| ValuesListLibrary.csv | 208 KB | 1,271 | 5 | CSV |
| document_types.json | 39 KB | 32 | - | JSON |

---

## Detailed File Analysis

### 1. HubLibraries20251119_1141.csv (36 MB - 488,291 rows)

**Purpose:** Hub libraries data export - multilingual organizational data

**Columns:**
| Column | Unique Values | Description |
|--------|---------------|-------------|
| starteffectdate | 1,219 | Effective date |
| library | 34 | Library type |
| clientcode | 57,664 | Client identifier |
| culture | 26 | Language code (en-gb, fr-fr, etc.) |
| field | 31 | Field name |
| value | 93,463 | Field value |

**Library Distribution:**
- OrganisationalStructure: 202,400 (41.5%)
- GeographicOrganisationStructure: 89,724 (18.4%)
- RegulationRegion: 66,395 (13.6%)
- CostCenter: 57,532 (11.8%)
- Institution: 40,385 (8.3%)
- LegalStructure: 23,010 (4.7%)

**HCM Relevance:** HIGH - Contains organizational units, cost centers, legal structures

---

### 2. Organisations.csv (20 MB - 395,174 rows)

**Purpose:** Manager-employee relationships across organization types

**Columns:**
| Column | Unique Values | Description |
|--------|---------------|-------------|
| organization | 15 | Organization/relationship type |
| username | 194,603 | Employee username |
| employeenumber | 194,600 | Employee ID |
| managerusername | 11,383 | Manager username |
| managernumber | 11,382 | Manager ID |
| action | 0 | Action flag (empty) |

**Organization Types:**
- Hiérarchique (Line Manager): 194,603 (49.2%)
- Administrative Management: 122,373 (31.0%)
- ORGA309c2cf7... (Custom): 22,037 (5.6%)
- Travel Approver: 19,212 (4.9%)
- corresp_form: 11,558 (2.9%)
- Career Management: 8,100 (2.0%)
- Expense Reports: 8,031 (2.0%)
- HRBP: 5,340 (1.4%)
- Vacation: 3,077 (0.8%)
- Responsable Formation: 715 (0.2%)

**HCM Relevance:** HIGH - Manager types, reporting relationships

---

### 3. SDD_PPC_LEVELS.csv (16 MB - 87,994 rows)

**Purpose:** Hierarchical referential data with levels (0-12)

**Columns:**
| Column | Description |
|--------|-------------|
| Referential | Type of referential (67 types) |
| Client code | Unique identifier |
| IdUnique | Unique ID |
| ParentId | Parent reference |
| Name | Display name |
| Level | Hierarchy level (0-20) |
| Is active | Active flag |
| 0-12 | Hierarchy breadcrumb columns |

**Referential Distribution:**
- OrganisationalUnit: 21,835 (24.8%)
- MAD: 17,083 (19.4%)
- CentreCout (Cost Center): 16,867 (19.2%)
- REF_METIER: 8,858 (10.1%)
- REF8 (Jobs): 7,864 (8.9%)
- AllocationCenter: 5,186 (5.9%)
- GeographicalUnit: 2,026 (2.3%)

**Active Status:** 56.8% Active, 43.2% Inactive

**HCM Relevance:** HIGH - Department hierarchy, cost centers, job structure

---

### 4. JobRepositoryNewIE.csv (9 MB - 7,865 rows)

**Purpose:** Job repository with descriptions and metadata

**Key Columns:**
| Column | Description | Values |
|--------|-------------|--------|
| referentielcode | REF8 (99.99%), TRASH (0.01%) | - |
| nodecode | Unique job code | 7,863 unique |
| parentnodecode | Parent job/family | 1,024 unique |
| nodename | Job title | 5,783 unique |
| active | Active flag | 15% True, 85% False |
| band | Direct/Indirect | 1,371 Indirect, 237 Direct |

**Active Jobs:** 1,177 (15% of total)

**HCM Relevance:** HIGH - Job catalog, job families, job descriptions

---

### 5. KeyPropertiesNewIE.csv (6 MB - 79,801 rows)

**Purpose:** Key properties for all referentials

**Columns:**
| Column | Unique Values | Description |
|--------|---------------|-------------|
| referentielcode | 62 | Type of referential |
| nodecode | 53,706 | Unique code |
| parentnodecode | 9,688 | Parent code |
| nodename | 50,319 | Display name |
| nodedescription | 3,913 | Description |
| active | 2 | Active flag (60.8% True) |

**Referential Distribution:**
- OrganisationalUnit: 21,836 (27.4%)
- MAD: 17,084 (21.4%)
- CentreCout: 16,868 (21.1%)
- REF_METIER: 8,859 (11.1%)
- AllocationCenter: 5,187 (6.5%)
- GeographicalUnit: 2,027 (2.5%)
- Prepa_Mob_Geo: 2,024 (2.5%)
- FORMATION: 1,110 (1.4%)
- LegalEntity: 808 (1.0%)

**HCM Relevance:** HIGH - Master data for all organizational entities

---

### 6. GenericLibrary.csv (1.5 MB - 18,606 rows)

**Purpose:** Generic value lists for various domains

**List Types (44 total):**
- ECOLE (Schools): 16,880 (90.7%)
- USERDEFINED4: 580 (3.1%)
- PAYS (Countries): 246 (1.3%)
- USERDEFINED1: 202 (1.1%)
- CERTIFICATIONSTYPE: 198 (1.1%)
- NOMLANGUE (Languages): 193 (1.0%)
- TYPE_ITEM: 39 (0.2%)
- FILIERE: 24 (0.1%)
- REMUNADVANTAGETYPE: 17 (0.1%)
- REMUNAVANTAGEHISTOTYPE: 17 (0.1%)

**HCM Relevance:** MEDIUM - Lookup values, compensation types

---

### 7. HubLibraries_Departments.json (15 MB - 89,585 records)

**Purpose:** Departmental structure with multilingual support

**Fields:**
- Library: OrganisationalStructure
- ClientCode: 21,834 unique departments
- Field: ShortName, IsActive, ParentClientCode, etc.
- Value: Department names/values
- StartEffectDate: Effective dates
- Culture: Language (en-gb, fr-fr)

**HCM Relevance:** HIGH - Department hierarchy, names, relationships

---

### 8. HubLibraries_LegalSitesAdressses.json (6 MB - 38,432 records)

**Purpose:** Legal sites with addresses (GeographicOrganisationStructure)

**Fields:**
- Library: GeographicOrganisationStructure
- ClientCode: Site identifier
- Field: ShortName, Street, TownOrCity, Country, etc.
- Value: Address components
- Culture: Language code

**HCM Relevance:** HIGH - Location addresses, legal sites

---

### 9. HubLibraries_LegalStructure.json (1 MB)

**Purpose:** Legal entity structure

**HCM Relevance:** HIGH - Legal entities, corporate structure

---

### 10. ValuesListLibrary.csv (208 KB - 1,271 rows)

**Purpose:** Custom value lists

**List Types:**
- Hotel_Adresse: 605 (47.6%)
- Hôtel - Adresse: 605 (47.6%)
- Domaine_Metier: 14 (1.1%)
- contract_end_reason: 8 (0.6%)
- TYPE_ACTION: 6 (0.5%)
- EVAL_OBJECTIF: 6 (0.5%)

**HCM Relevance:** LOW - Custom lookup values

---

### 11. HubProductValuesListLibrary.csv (1 MB - 26,399 rows)

**Purpose:** Product value lists with translations

**Types:**
- CountryCode: 7,811 (29.6%)
- Citizenship: 7,780 (29.5%)
- Currency: 7,153 (27.1%)
- TreeType: 1,548 (5.9%)
- GovernmentIdType: 248 (0.9%)

**Languages:** 31 cultures supported

**HCM Relevance:** MEDIUM - Reference data, translations

---

### 12. document_types.json (39 KB - 32 records)

**Purpose:** Document type definitions

**HCM Relevance:** HIGH - Document categories for employee records

---

## Key Findings for HCM Implementation

### 1. Organizational Units
- **21,836 OrganisationalUnits** in KeyPropertiesNewIE.csv
- **21,834 departments** in HubLibraries_Departments.json
- Hierarchy depth: 0-12 levels
- Active rate: ~60%

### 2. Manager Relationships
- **15 organization types** (manager relationship types)
- **194,603 unique employees** with manager assignments
- **11,383 unique managers**
- Key types: Hiérarchique, Administrative Management, HRBP, Career Manager

### 3. Job Structure
- **7,865 jobs** in JobRepositoryNewIE.csv
- **1,177 active jobs** (15%)
- Band categories: Direct (237), Indirect (1,371)
- **1,024 unique parent nodes** (job families)

### 4. Cost Centers
- **16,868 CentreCout** entries
- **5,187 AllocationCenter** entries
- Active rate: ~60%

### 5. Legal Entities
- **808 LegalEntity** entries in KeyPropertiesNewIE.csv
- Detailed structure in HubLibraries_LegalStructure.json

### 6. Geographic Structure
- **38,432 location records** with addresses
- **2,027 GeographicalUnit** entries
- Full address components: Street, City, Country

---

## Recommendations

### High Priority Files for HCM Migration:
1. **KeyPropertiesNewIE.csv** - Master referential data
2. **HubLibraries_Departments.json** - Department hierarchy
3. **JobRepositoryNewIE.csv** - Job catalog
4. **Organisations.csv** - Manager relationships
5. **HubLibraries_LegalSitesAdressses.json** - Locations

### Data Quality Considerations:
- 40% inactive records in KeyPropertiesNewIE.csv
- 85% inactive jobs in JobRepositoryNewIE.csv
- Some duplicate structures (Hotel_Adresse / Hôtel - Adresse)
- Multilingual support needed (26+ cultures)

### Migration Sequence:
1. Legal Entities → Locations → Departments → Jobs → Manager Types

---

*Report generated: 2025-11-29*
