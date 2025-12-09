# MDM MAB Files Analysis Report

**Date:** 2025-11-30
**Path:** `01 - Repositories/01 - MDM MAB`
**Purpose:** Analysis of Management Accounting Blueprint (MAB) referential files

---

## Executive Summary

| Metric | Value |
|--------|-------|
| Total Files | 15 CSV files |
| Total Size | ~3.9 MB |
| Key Objects | SOUs, Local SOUs, Legal Entities, Activities, Products |

---

## Files Inventory

| File | Size | Key Columns | HCM Relevance |
|------|------|-------------|---------------|
| Local ActivitiesFunctions View.csv | 1.3 MB | Activity/Function codes per ERP | Cost Allocation |
| Local Products Hierarchy.csv | 936 KB | Product hierarchy per ERP | Cost Allocation |
| Local SOUs.csv | 473 KB | Local SOU per ERP/ledger | Costing |
| SOUs View.csv | 390 KB | Global SOU (operational units) | Department/Cost Center |
| Legal Sites.csv | 295 KB | Physical locations | Location |
| Legal Entities View.csv | 121 KB | Legal entities (Dilitrust) | Legal Entity |
| Reporting Units View.csv | 106 KB | Reporting units | Business Unit |
| ActivitiesFunctions View.csv | 52 KB | Global activities/functions | Job Function |
| Local Legal Entities.csv | 38 KB | Local LE per ERP | Integration |
| Managerial Hierarchy.csv | 35 KB | Managerial structure | Division |
| MAB Products Hierarchy.csv | 23 KB | Global product hierarchy | Cost Allocation |
| Local Analytical Mapping IDs.csv | 7 KB | Analytical mapping codes | Costing |
| Local CoA Mapping IDs.csv | 5 KB | Chart of Accounts mapping | GL Integration |
| Business Hierarchy.csv | 3 KB | Business LoB structure | Division/BU |
| Systems.csv | 1 KB | ERP systems list | Source System |

---

## Detailed File Analysis

### 1. SOUs View.csv (Global SOUs)

**Purpose:** Smallest Operating Units - the cornerstone of MAB allocation model

**Key Columns:**
| Column | Description |
|--------|-------------|
| SOU Code | Unique identifier (e.g., 76COD01, 9SBOL01) |
| Name | SOU description |
| Type | Operational / Support / Technical |
| Reporting Unit Code | Link to reporting unit |
| Managerial Parent Code | Managerial hierarchy link |
| Business Parent Code | Business hierarchy link (LoB) |
| Legal Entity Code - DILITRUST | Legal entity reference |
| Alpha-2 Country Code | Country (DE, FR, US, etc.) |
| UN LOCODE | Location code |
| Status Calculated | ACTIVATED / DEACTIVATED |

**HCM Usage:** Maps to Department, Cost Center, or operational Location

---

### 2. Local SOUs.csv

**Purpose:** SOU implementation per ERP/ledger system

**Key Columns:**
| Column | Description |
|--------|-------------|
| Application Code | ERP system (ERP_DAX, ERP_ANL, etc.) |
| Local SOU Code | Local identifier in ERP |
| SOU Code | Link to global SOU |
| Local Analytical Identification Code | Analytical ID reference |
| Local Legal Entity Code | Local LE in ERP |
| Management Line Code | Management hierarchy |

**HCM Usage:** Enables multi-ERP cost allocation per employee

---

### 3. Local Analytical Mapping IDs.csv

**Purpose:** Granular analytical axes for cost allocation

**Key Columns:**
| Column | Description |
|--------|-------------|
| Local Analytical Identification Code | Unique analytical ID |
| Application Code | ERP system |
| LoB Code | Line of Business (FF, CL, etc.) |
| Alpha-2 Country Code | Country |
| Region Code | Region |

**HCM Usage:** Primary allocation key for employee costing

---

### 4. Systems.csv

**Purpose:** Master list of ERP and application systems

**Sample Systems:**
| Application Code | Application Name | Domain |
|-----------------|------------------|--------|
| ERP_ANL | ANAEL | Finance |
| ERP_DAX | Dynamics AX | Finance |
| ERP_DEM | DEAMSY | Finance |
| BIS_GBI | GBI | BI |
| CRM_EDN | EDEN | CRM |

**HCM Usage:** Source System Owner definition

---

### 5. ActivitiesFunctions View.csv (Global)

**Purpose:** Corporate activity and function taxonomy

**HCM Usage:** Job Function hierarchy, cost allocation dimensions

---

### 6. MAB Products Hierarchy.csv

**Purpose:** Global product hierarchy for cost allocation

**HCM Usage:** Product dimension in costing, FTE KPI reporting

---

### 7. Legal Entities View.csv

**Purpose:** Legal entities from Dilitrust (master source)

**HCM Usage:** Legal Entity, Legal Employer configuration

---

### 8. Business Hierarchy.csv / Managerial Hierarchy.csv

**Purpose:** LoB and managerial organization structures

**HCM Usage:** Division, Business Unit hierarchies

---

## Integration with Global Analytical Allocation Model

The MDM MAB files directly support the allocation model defined in `12_Global_Analytical_Allocation_Model.md`:

```
Employee Allocation Flow:

Employee → SOU (global) → Local SOU (per ERP) → Analytical Code → GL Account
    |           |              |                     |               |
    |      SOUs View      Local SOUs.csv      Local Analytical   Local CoA
    |           |              |              Mapping IDs        Mapping IDs
    └─────────────────────────────────────────────────────────────────┘
                     Global Analytical Allocation Table
```

---

## Key Relationships

| From | To | Relationship |
|------|-----|-------------|
| Local SOU | SOU | Many-to-One (multiple ERPs per SOU) |
| Local Analytical ID | Local SOU | Many-to-One |
| Local SOU | Local Legal Entity | Many-to-One |
| SOU | Legal Entity (Dilitrust) | Many-to-One |
| SOU | Reporting Unit | One-to-One |
| Local Analytical ID | Local CoA ID | One-to-One |

---

## Recommendations for HCM Configuration

### High Priority
1. **SOUs View.csv** → Use for Department hierarchy (operational units)
2. **Local SOUs.csv** → Use for Cost Center mapping per ERP
3. **Systems.csv** → Configure as Source System Owners

### Medium Priority
4. **ActivitiesFunctions View.csv** → Map to Job Function
5. **Local Analytical Mapping IDs.csv** → Configure Cost Allocation segments
6. **Local CoA Mapping IDs.csv** → GL account combination setup

### For Payroll Costing
7. Use **Global Analytical Allocation Model** to create multi-line cost allocations
8. Ensure Final_Allocation_Percent sums to 100% per employee

---

## Data Quality Observations

| Check | Status |
|-------|--------|
| SOU codes unique | OK |
| Local SOU → SOU reference valid | Verify |
| Application codes match Systems.csv | Verify |
| Status flags consistent | OK |

---

## Document Control

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-11-30 | Initial analysis |

---

*This report supports the Global Analytical Allocation Model implementation.*
