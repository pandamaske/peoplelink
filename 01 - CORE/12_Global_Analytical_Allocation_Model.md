# Global Analytical Allocation Model for Employees

> **⚠️ ARCHIVED DOCUMENT**
>
> This document has been superseded by **14_Multialocation_MAB.md** which consolidates:
> - All content from this document (Sections 0-8)
> - Governance of Analytical IDs (Section 12)
>
> **Please refer to document 14 for the current version.**

---

## 0. Purpose & Scope

This document defines a **single, holistic model** to represent how a **single employee** can be allocated across:

- Multiple **SOU** (group operational units)
- Multiple **Local SOUs** (per ERP / per ledger)
- Multiple **Analytical codes** (Activity / Product / Contract / etc.) inside each Local SOU
- Multiple **ERPs** (AX, ANAEL, GP …)

It also explains how to transform this model into:

- **GL account combinations** for financial posting
- **Oracle HCM Payroll costing lines** (multiple allocations per employee)
- **Analytical axes for FTE KPIs** (Non-Financial KPIs model)

The model must handle both simple and complex cases, including the example:

```text
SOU      Local Sou                            Occ  Local Sou %  Analytical code             Analytical %  ERP
SHAOF04  MY01MY01PC3L002-MY001L - Mapletree   1    60           83200/MISC/83200/AUTRES    100           AX
BWEOL30  LLC                                  2    20           0074C0000                   100           GP
LPTHC01  0006IT                               3    5            2HRPA/DIVERS/SSSTRU         50            ANAEL
LPTHC01  0006IT                               3    5            1MANU/AMAZON/SSSTRU         50            ANAEL
LPTHC01  000606                               3    10           2FIBC/DIVERS/SSSTRU         100           ANAEL
```

where a single employee:

- Belongs to **3 SOUs** (SHAOF04, BWEOL30, LPTHC01)
- Has **3 Local SOU occurrences** across **3 ERPs** (AX, GP, ANAEL)
- Has **5 analytical codes** overall, with nested percentages.

---

## 1. Key Concepts & Objects

### 1.1 SOU (Global)

**Source:** `SOUs View.csv`

Represents a **group-level operational unit** used for P&L and FTE KPIs.

Key fields:

- `SOU Code` (e.g. `SHAOF04`, `BWEOL30`, `LPTHC01`)
- `Name`
- `Type` (Operational / Support …)
- `Reporting Unit Code`
- `Legal Entity Code - DILITRUST`
- `Alpha-2 Country Code`, `UN LOCODE`
- `Activation Date`, `Deactivation Date`, `Status Calculated`

In our model, SOU is **a dimension**, not the primary key for allocations. Allocations are done at the level of **Local Analytical IDs**, which always point back to a SOU via Local SOU.

---

### 1.2 Local SOU

**Source:** `Local SOUs.csv`

Represents an **implementation of a SOU in a specific system/ledger**.

Key fields (typical):

- `Application Code` (AX, ANAEL, GP, ERP_ANL, etc.)
- `Local SOU Code` (e.g. `MY01MY01PC3L002-MY001L`, `LLC`, `0006IT`, `000606`)
- `Local Analytical Identification Code` (optional, may point to a generic analytical ID)
- `Name`
- `SOU Code` (link to global SOU)
- `Local Legal Entity Code`
- `Management Line Code`
- `Activation Date`, `Deactivation Date`, `Status Calculated`

**Role in the model:**

- Provides the **Cost Center dimension** for GL / costing.
- Connects each Local Analytical ID to a **global SOU** and **ERP**.

---

### 1.3 Local Analytical ID & Mapping

**Source:** `Local Analytical Mapping IDs.csv`

Defines the **granular analytical axes** used for allocations.

Key fields (typical):

- `Local Analytical Identification Code` (LA ID)
- `Local CoA Identification Code` (CoA ID)
- `Local SOU Code`
- `Local Activity Code`
- `Local Product Code`
- `Contract Code`
- `ImportExport Code`
- `System / ERP` (AX, ANAEL, GP …)

**Role in the model:**

> The **Local Analytical ID is the true allocation key** for employees.

Each Local Analytical ID corresponds to **one GL account pattern**, hanging off **one Local SOU**, in **one ERP**.

---

### 1.4 Local CoA Mapping

**Source:** `Local CoA Mapping IDs.csv`

Defines **full Chart of Accounts (CoA) combinations** per CoA ID.

Key fields (typical):

- `Local CoA Identification Code`
- Segment columns (Company, Cost Center, Activity, Product, Contract, etc.)

**Role in the model:**

- Provides the **exact GL segments** for each Local Analytical ID.
- Used to build GL account combinations and Oracle costing accounts.

---

### 1.5 Activities & Products

**Sources:**

- `ActivitiesFunctions View.csv` (global)
- `Local ActivitiesFunctions View.csv` (local per ERP)
- `MAB Products Hierarchy.csv` (global)
- `Local Products Hierarchy.csv` (local per ERP)

These define the **Activity / Function** and **Product** dimensions that appear inside Analytical codes like:

- `2HRPA/DIVERS/SSSTRU`
- `1MANU/AMAZON/SSSTRU`
- `2FIBC/DIVERS/SSSTRU`

**Role in the model:**

- Provide **canonical codes + hierarchies** for Activity and Product.
- Allow FTE and cost reporting by **Sub-Activity/Sub-Function** and **Product / Cluster**.

---

### 1.6 ERP / System

**Source:** `Systems.csv` and `Application Code` fields.

Each Local SOU / Local Analytical ID belongs to a **system** or **ERP**:

- AX
- ANAEL
- GP
- …

**Role in the model:**

- Distinguish analytical lines that belong to different ledgers/ERPs.
- Allow reporting by `SOU × ERP`, and control which IDs HCM is allowed to use.

---

## 2. The Allocation Model – Two Levels

### 2.1 Level A – SOU / Local SOU split

At the first level, an employee’s FTE or cost can be allocated across **multiple Local SOUs**, potentially in different ERPs.

For a given employee, we can have a table like:

| SOU     | Local Sou                           | Local Sou Occurrence | Local Sou % | ERP   |
|---------|-------------------------------------|----------------------|-------------|-------|
| SHAOF04 | MY01MY01PC3L002-MY001L - Mapletree  | 1                    | 60          | AX    |
| BWEOL30 | LLC                                 | 2                    | 20          | GP    |
| LPTHC01 | 0006IT                              | 3                    | 5           | ANAEL |
| LPTHC01 | 000606                              | 3                    | 10          | ANAEL |

The **Local Sou %** values must sum to **100%** per employee:

```text
60 + 20 + 5 + 10 = 95%  (illustrative; in production must be 100%)
```

> In practice, any deviation from 100% should be flagged as a **data quality issue**.

### 2.2 Level B – Analytical split inside each Local SOU

Within a Local SOU share, we further split into **Analytical codes** (Activity/Product combinations) using `Analytical %`.

Example for LPTHC01 Local SOUs from the complex case:

| SOU     | Local Sou | Local Sou % | Analytical code          | Analytical % | ERP   |
|---------|-----------|-------------|--------------------------|--------------|-------|
| LPTHC01 | 0006IT    | 5           | 2HRPA/DIVERS/SSSTRU     | 50           | ANAEL |
| LPTHC01 | 0006IT    | 5           | 1MANU/AMAZON/SSSTRU     | 50           | ANAEL |
| LPTHC01 | 000606    | 10          | 2FIBC/DIVERS/SSSTRU     | 100          | ANAEL |

Within **Local SOU 0006IT**, 5% is split into 2 analytical codes (50/50).  
Within **Local SOU 000606**, 10% is fully on one analytical code.

### 2.3 Final allocation per Analytical code

The **global allocation** per analytical line is computed as:

> **Final % = Local Sou % × Analytical % ÷ 100**

Compute this for the full complex example:

| SOU     | Local Sou                           | Local Sou % | Analytical code              | Analytical % | ERP   | Final % (Local Sou % × Analytical % / 100) |
|---------|-------------------------------------|-------------|------------------------------|--------------|-------|---------------------------------------------|
| SHAOF04 | MY01MY01PC3L002-MY001L - Mapletree  | 60          | 83200/MISC/83200/AUTRES     | 100          | AX    | 60 × 100 / 100 = **60**                      |
| BWEOL30 | LLC                                 | 20          | 0074C0000                   | 100          | GP    | 20 × 100 / 100 = **20**                      |
| LPTHC01 | 0006IT                              | 5           | 2HRPA/DIVERS/SSSTRU         | 50           | ANAEL | 5 × 50 / 100 = **2.5**                       |
| LPTHC01 | 0006IT                              | 5           | 1MANU/AMAZON/SSSTRU         | 50           | ANAEL | 5 × 50 / 100 = **2.5**                       |
| LPTHC01 | 000606                              | 10          | 2FIBC/DIVERS/SSSTRU         | 100          | ANAEL | 10 × 100 / 100 = **10**                      |

The **Final %** values should sum to **100%** per employee.  
In this illustrative dataset they sum to **95%**, which indicates a missing 5% allocation line; such inconsistencies must be detected and handled.

After this step, we no longer need `Local Sou %` or `Analytical %` separately; we work only with **Final % per analytical line**.

---

## 3. Canonical "Global Analytical Allocation" table

For all downstream systems (GL, Oracle HCM, FTE KPIs), we define a **canonical fact table** at the grain:

> **Employee × Local Analytical ID (per ERP) × Effective period**

### 3.1 Columns

**Identity & period**

- `Person_ID` – Internal person/employee identifier (e.g. GEODIS ID)  
- `Assignment_ID` – HCM assignment key (if available)  
- `Effective_Start_Date` – Start date of allocation  
- `Effective_End_Date` – End date of allocation (open-ended if null)

**ERP / system context**

- `ERP_System_Code` – AX, ANAEL, GP … (from `Application Code` / `Systems.csv`)  
- `Source_System_ID` – technical identifier of the source system/instance (optional)

**Analytical referencing**

- `Local_Analytical_ID` – Local Analytical Identification Code  
- `Local_CoA_ID` – Local CoA Identification Code  
- `Local_SOU_Code` – Local SOU Code (e.g. `MY01MY01PC3L002-MY001L`, `LLC`, `0006IT`, `000606`)  
- `SOU_Code` – Global SOU Code (from `SOUs View`)  
- `Local_Activity_Code` – from Local ActivitiesFunctions  
- `Local_Product_Code` – from Local Products Hierarchy  
- `Contract_Code` – if used in the analytical axis  
- `ImportExport_Code` – if used

**GL account segments** (expanded via Local CoA Mapping)

- `Company_Segment`  
- `Cost_Center_Segment` – typically identical or linked to `Local_SOU_Code`  
- `Activity_Segment`  
- `Product_Segment`  
- `Contract_Segment`  
- `ImportExport_Segment`  
- Any additional CoA segments as needed.

**Weights**

- `Final_Allocation_Percent` – fraction of the employee’s FTE/cost allocated to this line (e.g. 60, 20, 2.5, …)  
- Optionally: `Final_Allocation_Ratio` – same value divided by 100 (0.60, 0.20, …)  
- `Is_Valid` – flag after validation (1 if included; 0 if excluded due to errors)

**Audit & metadata**

- `Created_Timestamp`, `Updated_Timestamp`  
- `Source_File_Name`, `Source_Record_ID`  
- `Validation_Status` / `Validation_Message`

---

### 3.2 How to populate the canonical table from the detailed breakdown

Given an input table of the form:

- `SOU`, `LocalSou`, `LocalSouOccurrence`, `LocalSouPercent`, `AnalyticalCodeRank`, `AnalyticalCode`, `AnalyticalPercent`, `ERP` (exactly like your examples)

Algorithm per **employee**:

1. **For each row** in the detailed table:
   1.1. Compute `Final_Allocation_Percent = LocalSouPercent × AnalyticalPercent / 100`.
   1.2. Use (`AnalyticalCode`, `ERP`) to find the **Local Analytical ID** in `Local Analytical Mapping IDs`.
   1.3. From Local Analytical Mapping, retrieve:
       - `Local CoA ID`  
       - `Local SOU Code`  
       - `Local Activity Code`  
       - `Local Product Code`  
       - `Contract Code`, `ImportExport Code` (if applicable)
   1.4. From `Local SOUs` using `Local SOU Code`, retrieve:
       - `SOU Code` (global)  
       - `Local Legal Entity Code`  
       - `Application Code` (ERP system)
   1.5. From `Local CoA Mapping IDs` using `Local CoA ID`, expand all **GL segments**.
   1.6. Insert a row in the **Global Analytical Allocation** table with all these fields filled in.

2. **Validation per employee**:
   2.1. Sum all `Final_Allocation_Percent` for that employee across all rows.  
   2.2. If sum ≠ 100 (within tolerance), set `Is_Valid = 0` for all rows and log a data-quality error.  
   2.3. If sum = 100 (within tolerance), set `Is_Valid = 1` and allow downstream usage.

The result is a stable, coherent table where **each row is one analytical allocation line** for that employee, with all context (ERP, SOU, Local SOU, Activity, Product, GL segments).

---

## 4. Mapping to Oracle GL and HCM Payroll Costing

### 4.1 GL postings

For each row in the Global Analytical Allocation table where `Is_Valid = 1`:

- Use the **GL segments** (Company, Cost Center, Activity, Product, etc.) to form an **account combination**.
- When processing payroll costs (from Oracle or external payroll):
  - Multiply the **cost base** (e.g. monthly salary, employer charges) by `Final_Allocation_Ratio` to determine the amount for this line.
  - Post this amount to the GL account combination.

This ensures that GL postings reflect the **same analytical splits** used for FTE KPIs.

### 4.2 Oracle HCM Payroll costing (Fusion Payroll scenario)

If payroll is run in Oracle HCM, we use the **Global Analytical Allocation** table to create **Costing for Person / Assignment / Element** entries.

Per employee and assignment:

1. For each row (allocation line):
   - `distributionPercentage` = `Final_Allocation_Percent`  
   - `accountCombination` = GL combination derived from CoA segments.
2. Load these via HDL or UI into **Cost Allocation** objects:

   - `CostAllocation` – header for person/assignment/element  
   - `CostAllocationAccount` – multiple lines, one per analytical allocation

3. Ensure that distribution percentages for all lines for a given header sum to **100**.

Example for the complex case (assuming corrected numbers summing to 100):

```text
CostAllocation (Person X, Assignment A)
  • CostAllocationAccount 1: Account = CoA(83200/MISC/83200/AUTRES), Percentage = 60
  • CostAllocationAccount 2: Account = CoA(0074C0000),             Percentage = 20
  • CostAllocationAccount 3: Account = CoA(2HRPA/DIVERS/SSSTRU),   Percentage = 2.5
  • CostAllocationAccount 4: Account = CoA(1MANU/AMAZON/SSSTRU),   Percentage = 2.5
  • CostAllocationAccount 5: Account = CoA(2FIBC/DIVERS/SSSTRU),   Percentage = 10
```

Fusion Payroll will then automatically apply these ratios when calculating costs and generating GL entries.

---

## 5. Mapping to FTE KPIs (Non-Financial KPIs)

The FTE KPIs model (MAB_NF_KPIs_FTE_User_Guide) states that:

- FTE KPIs (Internal Paid, Apprenticeship, etc.) are **aggregated by SOU**.
- Additional dimensions (Activity/Function, Product, Contract, Import/Export) are **deduced from analytical axes** (accounting entries) per employee.
- Each employee can have up to **9 analytical splits**, which must sum to **100%**; otherwise their analytical axes are ignored and FTEs fall back to job-based mapping.

Our Global Analytical Allocation table is designed precisely to satisfy these conditions.

### 5.1 FTE computation steps

For a given employee:

1. Compute their **base FTE** for the period (from contract type, days worked, etc.).
2. Multiply that base FTE by each row’s `Final_Allocation_Ratio` to get:

   - FTE per **Local Analytical ID**
   - FTE per **SOU**, **Local SOU**, **Activity**, **Product**, etc.

3. Aggregate FTEs at the desired grain, e.g.:

   - by `SOU` (managerial SOU)  
   - by `SOU × Activity`  
   - by `SOU × Product`  
   - by `SOU × ERP`

4. For workers with invalid allocations (`Is_Valid = 0`), apply the fallback rules defined in the FTE KPIs guide (e.g. using **Job Category → Sub-Activity/Sub-Function** mapping).

---

## 6. Governance & Data Quality Rules

To keep the model stable and auditable, the following rules apply:

1. **Single Source of Truth**
   - SOUs: `SOUs View.csv`
   - Local SOUs: `Local SOUs.csv`
   - Local Analytical IDs: `Local Analytical Mapping IDs.csv`
   - Local CoA IDs: `Local CoA Mapping IDs.csv`
   - Activities/Functions: `ActivitiesFunctions` / `Local ActivitiesFunctions`
   - Products: `MAB Products Hierarchy` / `Local Products Hierarchy`

2. **No free-text analytical codes** in HCM/GL:
   - All analytical codes (e.g. `2HRPA/DIVERS/SSSTRU`) must resolve to a **Local Analytical ID**.

3. **Percentages must balance**:
   - For each employee and period, the sum of **Final_Allocation_Percent** across all allocation lines must be **100%**.
   - Any deviation → `Is_Valid = 0` and remediation required.

4. **Effective dating**:
   - Allocation lines must have clear start/end dates matching employment and MAB referential dates.

5. **Change management**:
   - Any change in Local SOUs, Local Analytical IDs, or CoA mappings must go through MDM and be synchronized to HCM/GL.

---

## 7. Summary

- Employees can be allocated to **multiple Local SOUs** across **multiple ERPs**.
- Within each Local SOU, they can be further split among **multiple analytical codes** (Activity/Product/Contract), each with its own percentage.
- The **canonical allocation unit** is **Employee × Local Analytical ID**, with a computed **Final %**.
- A single **Global Analytical Allocation** table at that grain feeds:
  - GL postings (via CoA IDs and segments)
  - Oracle HCM Payroll costing (multiple costing lines per person/assignment)
  - FTE KPI calculations (SOU, Activity, Product, etc.).
- All codes and hierarchies are governed by MAB referentials; HCM/GL do not invent new analytical or SOU codes.

This model generalises from the simple apprentice examples to the most complex multi-ERP, multi-Local-SOU scenarios and provides a single, consistent way to handle cost and FTE allocations across the group.


## 8. Worked Example – Multi-ERP, Multi-Local-SOU Split (Revised & Consistent)

This section applies the model to a **realistic complex case** where a single employee:

- Belongs to **3 SOUs** overall (AX, GP, ANAEL)
- Has **4 Local SOU occurrences** (one in AX, one in GP, two in ANAEL)
- Has **5 analytical codes** in total
- Is finally split into **5 analytical allocation lines summing to 100%**

### 8.1 Input breakdown as provided by Finance

Source table (per employee):

| SOU     | Local Sou                           | Local Sou Occurrence | Local Sou % | Analytical code linked | Analytical code              | Analytical % | ERP   |
|---------|-------------------------------------|----------------------|-------------|------------------------|------------------------------|--------------|-------|
| SHAOF04 | MY01MY01PC3L002-MY001L - Mapletree  | 1                    | 60          | 1                      | 83200/MISC/83200/AUTRES     | 100          | AX    |
| BWEOL30 | LLC                                 | 2                    | 20          | 2                      | 0074C0000                   | 100          | GP    |
| LPTHC01 | 0006IT                              | 3                    | 10          | 3                      | 2HRPA/DIVERS/SSSTRU         | 50           | ANAEL |
| LPTHC01 | 0006IT                              | 3                    | 10          | 4                      | 1MANU/AMAZON/SSSTRU         | 50           | ANAEL |
| LPTHC01 | 000606                              | 4                    | 10          | 5                      | 2FIBC/DIVERS/SSSTRU         | 100          | ANAEL |

**Interpretation of each column**

- `SOU` – Global SOU code from `SOUs View.csv`.
- `Local Sou` – Local SOU code from `Local SOUs.csv` (cost center for a specific ERP).
- `Local Sou Occurrence` – purely ordering / grouping indicator, not used in the final math.
- `Local Sou %` – share of the person’s FTE/cost attributed to that **Local SOU** in that ERP **before** analytical split.
- `Analytical code linked` – rank/index of the analytical code, used only for traceability.
- `Analytical code` – human-readable representation of the analytical axis (activity/product/contract, etc.).
- `Analytical %` – share of the **Local Sou %** apportioned to this specific analytical code.
- `ERP` – originating ERP / system (AX, GP, ANAEL…).

### 8.2 Step 1 – Compute final allocation per analytical line

The **global weight** for each analytical code is calculated as:

> **Final_Allocation_Percent = Local_Sou_% × Analytical_% ÷ 100**

Apply this formula row by row:

1. `SHAOF04 / MY01MY01PC3L002-MY001L / AX`  
   - Local Sou % = 60  
   - Analytical % = 100  
   - Final % = 60 × 100 ÷ 100 = **60**

2. `BWEOL30 / LLC / GP`  
   - Local Sou % = 20  
   - Analytical % = 100  
   - Final % = 20 × 100 ÷ 100 = **20**

3. `LPTHC01 / 0006IT / ANAEL / 2HRPA/DIVERS/SSSTRU`  
   - Local Sou % = 10  
   - Analytical % = 50  
   - Final % = 10 × 50 ÷ 100 = **5**

4. `LPTHC01 / 0006IT / ANAEL / 1MANU/AMAZON/SSSTRU`  
   - Local Sou % = 10  
   - Analytical % = 50  
   - Final % = 10 × 50 ÷ 100 = **5**

5. `LPTHC01 / 000606 / ANAEL / 2FIBC/DIVERS/SSSTRU`  
   - Local Sou % = 10  
   - Analytical % = 100  
   - Final % = 10 × 100 ÷ 100 = **10**

The **flattened analytical allocation** is thus:

| ERP   | SOU     | Local Sou   | Analytical code              | Final % |
|-------|---------|-------------|------------------------------|---------|
| AX    | SHAOF04 | MY01MY01…   | 83200/MISC/83200/AUTRES     | 60      |
| GP    | BWEOL30 | LLC         | 0074C0000                   | 20      |
| ANAEL | LPTHC01 | 0006IT      | 2HRPA/DIVERS/SSSTRU         | 5       |
| ANAEL | LPTHC01 | 0006IT      | 1MANU/AMAZON/SSSTRU         | 5       |
| ANAEL | LPTHC01 | 000606      | 2FIBC/DIVERS/SSSTRU         | 10      |

**Validation checks**

1. **Per analytical line:** all Final % values are between 0 and 100.  
2. **Global sum per employee:** 60 + 20 + 5 + 5 + 10 = **100%** ✅  
3. **Per Local SOU:**
   - MY01MY01… (AX) = 60
   - LLC (GP) = 20
   - 0006IT (ANAEL) = 5 + 5 = 10
   - 000606 (ANAEL) = 10  
   → 60 + 20 + 10 + 10 = **100%** ✅
4. **Per SOU (global):**
   - SHAOF04 = 60
   - BWEOL30 = 20
   - LPTHC01 = 5+5+10 = 20  
   → 60 + 20 + 20 = **100%** ✅

This confirms the revised split is **internally consistent across all levels**.

### 8.3 Step 2 – Resolve each analytical line into MAB IDs & GL segments

For each row of the flattened table we perform the following joins:

1. **Analytical code → Local Analytical ID**  
   - Use `Analytical code` + `ERP` to look up the **Local Analytical Identification Code** in `Local Analytical Mapping IDs.csv`.
   - Retrieve:
     - `Local_Analytical_ID`
     - `Local_CoA_ID`
     - `Local_SOU_Code` (validated against the `Local Sou` column from the input)
     - `Local_Activity_Code` (e.g. `2HRPA`, `1MANU`, `2FIBC`)
     - `Local_Product_Code` (e.g. `DIVERS`, `AMAZON`)
     - Other analytic flags (Contract, Import/Export).

2. **Local SOU → SOU and legal context**  
   - Use `Local_SOU_Code` in `Local SOUs.csv` to retrieve:
     - `SOU_Code` (global) – should match the `SOU` column of the input line
     - `Local_Legal_Entity_Code`
     - `Application_Code` (ERP validation)
     - `Management_Line_Code`

3. **Local CoA ID → GL segments**  
   - Use `Local_CoA_ID` in `Local CoA Mapping IDs.csv` to expand:
     - `Company_Segment`
     - `Cost_Center_Segment` (usually linked to Local SOU)
     - `Activity_Segment`
     - `Product_Segment`
     - `Contract_Segment`
     - `ImportExport_Segment`
     - Other CoA segments as needed.

4. **Activity & Product dictionary**  
   - Use `Local_Activity_Code` in `Local ActivitiesFunctions View.csv` to retrieve official Activity / Sub-Function labels and hierarchies.
   - Use `Local_Product_Code` in `Local Products Hierarchy.csv` to retrieve Product / Cluster levels.

After these joins, each analytical line contains:

- Full ERP / SOU / Local SOU context
- Local Analytical ID and its **full GL account definition**
- Explicit Activity and Product dimensions
- The **Final_Allocation_Percent** computed earlier.

### 8.4 Step 3 – Insert lines into the Global Analytical Allocation table

Using the structure defined in Section 3, we insert **5 rows** for this employee:

Example (conceptual):

| Person_ID | Assignment_ID | ERP_System_Code | Local_Analytical_ID | Local_CoA_ID | Local_SOU_Code | SOU_Code | Activity_Segment | Product_Segment | Cost_Center_Segment | Final_Allocation_Percent | Is_Valid |
|----------:|---------------|-----------------|---------------------|-------------|----------------|----------|------------------|-----------------|---------------------|---------------------------|---------|
| P12345    | A1            | AX              | LA_AX_001           | C_AX_001    | MY01MY01…      | SHAOF04  | 83200            | MISC             | [from CoA]          | 60                        | 1       |
| P12345    | A1            | GP              | LA_GP_002           | C_GP_002    | LLC            | BWEOL30  | [from 0074C0000] | [from 0074C0000] | [from CoA]          | 20                        | 1       |
| P12345    | A1            | ANAEL           | LA_AN_003           | C_AN_003    | 0006IT         | LPTHC01  | 2HRPA            | DIVERS           | [from CoA]          | 5                         | 1       |
| P12345    | A1            | ANAEL           | LA_AN_004           | C_AN_004    | 0006IT         | LPTHC01  | 1MANU            | AMAZON           | [from CoA]          | 5                         | 1       |
| P12345    | A1            | ANAEL           | LA_AN_005           | C_AN_005    | 000606         | LPTHC01  | 2FIBC            | DIVERS           | [from CoA]          | 10                        | 1       |

Validation flag `Is_Valid = 1` because the Final_Allocation_Percent values sum to 100.

### 8.5 Step 4 – Generate Oracle HCM Payroll costing lines

For employees whose payroll is handled in Oracle Fusion, we derive **Cost Allocation** objects from the Global Analytical Allocation table.

For this example employee and assignment `A1`:

1. Create a `CostAllocation` header for the person/assignment (or element), with the relevant effective dates.
2. Create **5 `CostAllocationAccount` lines**:

   - Line 1:  
     - Account combination = GL combination from `C_AX_001` (CoA derived from `83200/MISC/83200/AUTRES`)  
     - `distributionPercentage = 60`
   - Line 2:  
     - Account combination = GL combination from `C_GP_002` (`0074C0000`)  
     - `distributionPercentage = 20`
   - Line 3:  
     - Account combination = GL combination from `C_AN_003` (`2HRPA/DIVERS/SSSTRU`)  
     - `distributionPercentage = 5`
   - Line 4:  
     - Account combination = GL combination from `C_AN_004` (`1MANU/AMAZON/SSSTRU`)  
     - `distributionPercentage = 5`
   - Line 5:  
     - Account combination = GL combination from `C_AN_005` (`2FIBC/DIVERS/SSSTRU`)  
     - `distributionPercentage = 10`

3. Confirm that the sum of distributionPercentage values is 100 – Oracle will enforce this.

### 8.6 Step 5 – Use the same allocations for FTE KPIs

When computing FTE-based KPIs for this employee:

1. Determine their **base FTE** for the period (e.g. 1.0 FTE if full-time).
2. For each of the 5 allocation lines, compute **FTE share**:

   - AX / SHAOF04 / 83200/MISC/83200/AUTRES → FTE × 60%
   - GP / BWEOL30 / 0074C0000 → FTE × 20%
   - ANAEL / LPTHC01 / 0006IT / 2HRPA/DIVERS/SSSTRU → FTE × 5%
   - ANAEL / LPTHC01 / 0006IT / 1MANU/AMAZON/SSSTRU → FTE × 5%
   - ANAEL / LPTHC01 / 000606 / 2FIBC/DIVERS/SSSTRU → FTE × 10%

3. Roll these FTEs up by the required dimensions:

   - By **SOU** (global operational unit)  
   - By **SOU × Activity** (via Local Activity → Activity hierarchy)  
   - By **SOU × Product** (via Local Product → Product hierarchy)  
   - By **SOU × ERP** (AX, GP, ANAEL)

Because the analytic splits are the same for **costs** (GL) and **FTEs** (KPI model), the organisation can reconcile “headcount/FTE by SOU/Activity/Product” with financial performance by the same axes.

---

This worked example demonstrates concretely how the Global Analytical Allocation model handles a **multi-ERP, multi-SOU, multi-Local-SOU** scenario, and how the revised split is propagated consistently into GL, Oracle HCM Payroll, and FTE KPI reporting.
