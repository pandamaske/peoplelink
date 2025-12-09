# Global Analytical Allocation Model for Employees

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

At GEODIS, each employee can have up to **4 separate assignments** in HCM. We model this by using:

- `Local Sou Occurrence = 1` → Assignment A1  
- `Local Sou Occurrence = 2` → Assignment A2  
- `Local Sou Occurrence = 3` → Assignment A3  
- `Local Sou Occurrence = 4` → Assignment A4

All analytical lines for a given `Person_ID` + `Local Sou Occurrence` belong to the **same HCM assignment** and must carry Final % values that sum to **100% for that assignment block**.

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

- `Local_SOU_Occurrence` – occurrence number from the MAB export identifying the **assignment-level allocation block** for that person (1, 2, 3, 4). This is used to map from MAB rows to the correct HCM `Assignment_ID` (A1–A4).
- `Local_Analytical_ID` – Local Analytical Identification Code  
- `Local_CoA_ID` – Local CoA Identification Code  
- `Local_SOU_Code` – Local SOU Code (e.g. `MY01MY01PC3L002-MY001L`, `LLC`, `0006IT`, `000606`)  
- `SOU_Code` – Global SOU Code (from `SOUs View`)  
- `Local_Activity_Code` – from Local ActivitiesFunctions  
- `Local_Product_Code` – from Local Products Hierarchy  
- `Contract_Code` – if used in the analytical axis  
- `ImportExport_Code` – if used

**GL account segments** (expanded via Local CoA Mapping)** (expanded via Local CoA Mapping)** (expanded via Local CoA Mapping)

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

2. **Validation per employee and assignment (Local Sou Occurrence)**:
   2.1. For each combination of `Person_ID` + `Local_SOU_Occurrence` (i.e. for each assignment block), sum all `Final_Allocation_Percent` across rows.  
   2.2. If the sum for a given block ≠ 100 (within tolerance), set `Is_Valid = 0` for those rows and log a data-quality error for that **assignment**.  
   2.3. Optionally, also check the **global sum per employee** (across all occurrences) if required by the FTE KPI model.  
   2.4. If the sum for a block = 100 (within tolerance), set `Is_Valid = 1` and allow downstream usage for that assignment.

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
- `Local Sou Occurrence` – **index of the assignment block** for this person (values 1, 2, 3, 4). Each occurrence groups the Local SOU + analytical lines that belong to a given **assignment/contract** for the employee. At GEODIS, a person can have up to **4 concurrent assignments**, so there are at most 4 occurrences. All lines with the same Local Sou Occurrence must sum to **100% for that assignment**.
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

**Case 1 – All lines belong to the same assignment (simplified example)**

In the very first version of this example, we assumed all 5 allocation lines belonged to a **single HCM assignment** (A1). In that simplification, the table looks like this:

| Person_ID | Assignment_ID | ERP_System_Code | Local_Analytical_ID | Local_CoA_ID | Local_SOU_Code | SOU_Code | Activity_Segment | Product_Segment | Cost_Center_Segment | Final_Allocation_Percent | Is_Valid |
|----------:|---------------|-----------------|---------------------|-------------|----------------|----------|------------------|-----------------|---------------------|---------------------------|---------|
| P12345    | A1            | AX              | LA_AX_001           | C_AX_001    | MY01MY01…      | SHAOF04  | 83200            | MISC             | [from CoA]          | 60                        | 1       |
| P12345    | A1            | GP              | LA_GP_002           | C_GP_002    | LLC            | BWEOL30  | [from 0074C0000] | [from 0074C0000] | [from CoA]          | 20                        | 1       |
| P12345    | A1            | ANAEL           | LA_AN_003           | C_AN_003    | 0006IT         | LPTHC01  | 2HRPA            | DIVERS           | [from CoA]          | 5                         | 1       |
| P12345    | A1            | ANAEL           | LA_AN_004           | C_AN_004    | 0006IT         | LPTHC01  | 1MANU            | AMAZON           | [from CoA]          | 5                         | 1       |
| P12345    | A1            | ANAEL           | LA_AN_005           | C_AN_005    | 000606         | LPTHC01  | 2FIBC            | DIVERS           | [from CoA]          | 10                        | 1       |

This is **valid only if business confirms** that, for this person, all the AX/GP/ANAEL allocations belong to a **single physical assignment/contract**.

---

**Case 2 – GEODIS model with up to 4 assignments (recommended)**

In the GEODIS target model, we use `Local Sou Occurrence` (1–4) to represent **up to four separate assignments** in HCM for the same person:

- Occurrence 1 → Assignment A1  
- Occurrence 2 → Assignment A2  
- Occurrence 3 → Assignment A3  
- Occurrence 4 → Assignment A4

For the revised split example, the input breakdown is:

| SOU     | Local Sou                           | Local Sou Occurrence | Local Sou % | Analytical code | Analytical % | ERP   |
|---------|-------------------------------------|----------------------|-------------|-----------------|--------------|-------|
| SHAOF04 | MY01MY01PC3L002-MY001L - Mapletree  | 1                    | 60          | 83200/MISC/83200/AUTRES     | 100          | AX    |
| BWEOL30 | LLC                                 | 2                    | 20          | 0074C0000                   | 100          | GP    |
| LPTHC01 | 0006IT                              | 3                    | 10          | 2HRPA/DIVERS/SSSTRU         | 50           | ANAEL |
| LPTHC01 | 0006IT                              | 3                    | 10          | 1MANU/AMAZON/SSSTRU         | 50           | ANAEL |
| LPTHC01 | 000606                              | 4                    | 10          | 2FIBC/DIVERS/SSSTRU         | 100          | ANAEL |

Mapping occurrences to assignments gives:

- Occurrence 1 → Assignment `A1`  
- Occurrence 2 → Assignment `A2`  
- Occurrence 3 → Assignment `A3`  
- Occurrence 4 → Assignment `A4`

After computing Final_Allocation_Percent for each line (60, 20, 5, 5, 10), the **Global Analytical Allocation** table becomes:

| Person_ID | Assignment_ID | ERP_System_Code | Local_Analytical_ID | Local_CoA_ID | Local_SOU_Code | SOU_Code | Activity_Segment | Product_Segment | Cost_Center_Segment | Final_Allocation_Percent | Is_Valid |
|----------:|---------------|-----------------|---------------------|-------------|----------------|----------|------------------|-----------------|---------------------|---------------------------|---------|
| P12345    | A1            | AX              | LA_AX_001           | C_AX_001    | MY01MY01…      | SHAOF04  | 83200            | MISC             | [from CoA]          | 60                        | 1       |
| P12345    | A2            | GP              | LA_GP_002           | C_GP_002    | LLC            | BWEOL30  | [from 0074C0000] | [from 0074C0000] | [from CoA]          | 20                        | 1       |
| P12345    | A3            | ANAEL           | LA_AN_003           | C_AN_003    | 0006IT         | LPTHC01  | 2HRPA            | DIVERS           | [from CoA]          | 5                         | 1       |
| P12345    | A3            | ANAEL           | LA_AN_004           | C_AN_004    | 0006IT         | LPTHC01  | 1MANU            | AMAZON           | [from CoA]          | 5                         | 1       |
| P12345    | A4            | ANAEL           | LA_AN_005           | C_AN_005    | 000606         | LPTHC01  | 2FIBC            | DIVERS           | [from CoA]          | 10                        | 1       |

**Assignment-level validation**

- For Assignment A1 (occurrence 1): sum of Final % = 60 → must equal 100 *for that assignment* if A1 represents 100% of a contract. If, for example, A1 is only a 0.6 FTE contract, then 60% here represents 100% of that 0.6 FTE.  
- For Assignment A2 (occurrence 2): sum of Final % = 20 → same logic.  
- For Assignment A3 (occurrence 3): 5 + 5 = 10 → lines within A3 sum to 10; business rules must clarify whether this 10 is "100% of a 0.1 FTE assignment" or part of a larger contract.  
- For Assignment A4 (occurrence 4): sum of Final % = 10.

In the strictest interpretation, for each `Person_ID + Assignment_ID`, the **relative weights within that assignment** must sum to 100% of that assignment’s base FTE. If the Local Sou % already encodes the fraction of total FTE belonging to that assignment, then the percentages here can be interpreted as \"% of total FTE\" rather than \"% of this assignment only\". The implementation team must choose one convention and apply it consistently.

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

## 12. Governance of Analytical IDs – Allowed Combinations, Non‑Freetext, Time‑Bound

This section explains how to ensure that **Analytical IDs are never freetext**, are always **consistent with Local SOU / ERP / CoA**, and that **allocations can vary over time** in a controlled, effective‑dated way.

### 12.1 Target principles

1. **No freetext analytical codes** in HCM or staging: every analytical value must exist in the MAB referentials.  
2. **Allowed combinations only**: for a given `(ERP, Local SOU, Local CoA)` set, only a **finite list** of Analytical IDs is valid.  
3. **Time‑bound validity**: Analytical IDs and their mappings are effective‑dated; employees’ allocations are also effective‑dated.  
4. **Max 4 assignments per person**: each assignment has its **own allocation block** over time (using `Local Sou Occurrence` as the assignment index).

### 12.2 Referential design for Analytical IDs

We enforce the above principles by designing the MAB referentials with:

#### 12.2.1 Local Analytical Mapping table

Logical structure (can be an extension of `Local Analytical Mapping IDs.csv` loaded into a governed DB/table):

| Column                          | Description                                                                |
|---------------------------------|----------------------------------------------------------------------------|
| `Local_Analytical_ID`          | Primary key for the analytical axis (used in all downstream systems)      |
| `ERP_System_Code`              | AX / ANAEL / GP / …                                                        |
| `Local_SOU_Code`               | Local SOU Code (cost center)                                              |
| `Local_CoA_ID`                 | Foreign key to Local CoA Mapping                                          |
| `Activity_Code`                | Local Activity / Function code                                            |
| `Product_Code`                 | Local Product code                                                         |
| `Contract_Code`                | Contract dimension (if used)                                              |
| `ImportExport_Code`           | Import/Export flag (if used)                                              |
| `Effective_Start_Date`         | Date from which this analytical combination is valid                      |
| `Effective_End_Date`           | Date until which this analytical combination is valid (open‑ended if null)|
| `Status`                       | ACTIVE / INACTIVE                                                          |

**Governance rules**:

- `(Local_Analytical_ID, ERP_System_Code)` must be **unique** across time, with **no overlapping effective dates**.  
- `(ERP_System_Code, Local_SOU_Code, Local_CoA_ID, Activity_Code, Product_Code, Contract_Code, ImportExport_Code)` should be **unique per effective date range** – i.e. one physical combination = one Local Analytical ID.  
- New analytical combinations are created **only** via MDM/MAB, never directly in HCM.

#### 12.2.2 Local CoA Mapping table

The Local CoA mapping table remains the **single source** for full GL combinations, but we add effective dating:

| Column                  | Description                                   |
|-------------------------|-----------------------------------------------|
| `Local_CoA_ID`         | Primary key                                   |
| `ERP_System_Code`      | AX / ANAEL / GP                               |
| `Company_Segment`      | CoA segment                                   |
| `Cost_Center_Segment`  | CoA segment (linked to Local SOU)             |
| `Activity_Segment`     | CoA segment                                   |
| `Product_Segment`      | CoA segment                                   |
| `…`                    | Additional CoA segments                        |
| `Effective_Start_Date` | Valid from                                     |
| `Effective_End_Date`   | Valid to                                       |
| `Status`               | ACTIVE / INACTIVE                              |

Any Analytical ID pointing to an **inactive or expired** Local CoA ID is considered **invalid**.

### 12.3 Making Analytical IDs non‑freetext in HCM

There are two complementary strategies, depending on how much you want users to touch analytics in HCM.

#### 12.3.1 Recommended: keep Analytical IDs out of the user UI

- The **primary flow** is: MAB → ETL → Global Analytical Allocation → HCM costing / GL.  
- HCM users **do not key** Analytical IDs; they only maintain HR data (Legal Employer, BU, Department, Job, etc.).  
- All analytical allocations (SOU splits, Local SOUs, Analytical IDs, CoA) are built and validated in the **staging/ETL layer**, and then **loaded** to HCM costing.

Benefits:

- Zero risk of “creative” freetext codes.  
- Full control via MAB referentials and data‑quality checks.  
- HCM remains a **consumer** of analytical data, not a maintenance point.

#### 12.3.2 If HCM must expose analytical info: table‑validated LOVs

If there is a requirement that HCM users can **view or (exceptionally) adjust** analytical assignments (e.g. via an Assignment or Costing DFF), then:

1. Create a **custom DB table** in the Fusion schema (e.g. `XX_MAB_ANALYTICAL_REF`) loaded from the MAB `Local Analytical Mapping` extract.  
2. Create a **table‑validated Value Set** for the Analytical ID segment that:
   - Selects `Local_Analytical_ID` and description from `XX_MAB_ANALYTICAL_REF`.  
   - Has a WHERE clause restricting values to:
     - `ERP_System_Code = :XX_ERP_FIELD`  
     - `Local_SOU_Code = :XX_LOCAL_SOU_FIELD`  
     - Optional: `Local_CoA_ID = :XX_LOCAL_COA_FIELD` or matching CoA segments  
     - `TRUNC(SYSDATE) BETWEEN Effective_Start_Date AND NVL(Effective_End_Date, DATE '4712-12-31')`  
     - `Status = 'ACTIVE'`
3. Attach that Value Set to a **DFF segment** on the relevant entity:
   - Assignment DFF, or  
   - Cost Allocation DFF (person/assignment/element costing).
4. If needed, make the Analytical ID segment **read‑only** in the UI and only updatable via integration.

Result:

- HCM will **only show valid Analytical IDs** for the selected `(ERP, Local SOU, CoA)` **and** only those that are **active on today’s date**.  
- No freetext; all values are driven from the referential.

### 12.4 Time‑bound affectations (allocations varying over time)

Allocations can change over time because:

- Employees change assignments (A1 → A2, etc.).  
- The split of an assignment across Local SOUs / Analytical IDs changes (e.g. 60/20/20 → 50/30/10/10).  
- The underlying Analytical IDs / CoA combinations are re‑designed by Finance.

We handle this at **two levels**:

#### 12.4.1 Referential level (Analytical IDs and CoA)

- Every Analytical ID and Local CoA ID is **effective‑dated** with `Effective_Start_Date` and `Effective_End_Date`.  
- Changes to mappings (e.g. moving a product to another SOU) are managed by **creating a new record** with a new effective start date and end‑dating the old one.  
- There is **no in‑place overwrite** of historical referential data.

#### 12.4.2 Employee allocation level (Global Analytical Allocation table)

For each **Person_ID + Assignment_ID (A1–A4)**:

- Each allocation line in the Global Analytical Allocation table includes:  
  - `Effective_Start_Date`  
  - `Effective_End_Date`  
  - `Final_Allocation_Percent`  
- When an allocation changes (e.g. from 60/20/10/10 to 50/30/10/10):
  1. Close the previous allocation set by setting `Effective_End_Date` to the day before the change.  
  2. Insert a **new set of rows** (one per analytical line) with the new percentages and a new `Effective_Start_Date`.
- Validation is done **per Person + Assignment + period**:
  - For each continuous period, the sum of `Final_Allocation_Percent` across lines for that assignment must be **100%** (or 0% if the assignment is inactive).

In Oracle HCM Payroll costing:

- Cost Allocation objects are also **effective‑dated**.  
- Each time we change the allocation, we **create a new costing record** with a new start date; Fusion will end‑date the previous costing automatically if configured correctly.

## 12.5 End‑to‑end flow with governance

This section describes the **operating model** for governed, time‑bound analytical allocations from MAB → Integration → Oracle HCM / GL / FTE KPIs.

The goal is to ensure that:

- Analytical IDs are **never freetext**.  
- Only combinations consistent with **ERP / Local SOU / Local CoA** and their dates are allowed.  
- Allocations are **effective‑dated**, **assignment‑specific**, and always sum to **100%** per period.

---

### 12.5.1 Step 1 – Maintain referentials in MAB

**Owners:** MDM / Finance / Group Controlling.

Activities:

1. Maintain the following referentials in MAB (or equivalent master data platform):
   - `SOUs View` – global SOUs.  
   - `Local SOUs` – Local SOU Code, ERP, Legal Entity, Management Line.  
   - `Local Analytical Mapping IDs` – Local Analytical ID ↔ Local SOU + Local CoA + Activity + Product + Contract + Import/Export.  
   - `Local CoA Mapping IDs` – Local CoA ID ↔ CoA segments.  
   - `ActivitiesFunctions` / `Local ActivitiesFunctions` – Activity / Function dictionaries & hierarchies.  
   - `MAB Products` / `Local Products` – Product & Cluster hierarchies.

2. Apply **effective dating** and status to all referential rows:
   - `Effective_Start_Date`  
   - `Effective_End_Date` (or open‑ended)  
   - `Status` = ACTIVE / INACTIVE

3. Changes in business logic (e.g. re‑segmenting a product, moving a Local SOU to another SOU) are implemented by:
   - **End‑dating** existing rows.  
   - **Inserting new rows** with new dates and values.  
   - **Never overwriting** historical records.

Outcome: MAB holds the **single source of truth** for all analytical structures, with full history.

---

### 12.5.2 Step 2 – Load referentials into Fusion & GL

**Owners:** Integration team, Oracle technical team.

Activities:

1. On a regular schedule (e.g. nightly):
   - Extract referential changes from MAB.  
   - Load them into:
     - A **Fusion custom reference table** (e.g. `XX_MAB_ANALYTICAL_REF`) used for Value Sets / DFFs.  
     - GL segment value sets / hierarchies (e.g. Cost Centers, Activities, Products).

2. Apply filtering/transformations:
   - Keep only rows where `Status = 'ACTIVE'`.  
   - Ensure `TRUNC(SYSDATE)` is between `Effective_Start_Date` and `Effective_End_Date` for values exposed as selectable.  
   - Optionally materialise **denormalised views** that combine Local Analytical ID, Local SOU, Local CoA, Activity, Product, etc.

3. Synchronise code sets so that:
   - Every Local SOU Code exists as a **GL Cost Center segment value**.  
   - Every Activity/Product used in CoA is defined in the relevant GL segments.

Outcome: Fusion and GL always see an **up‑to‑date, controlled list** of allowed analytical values.

---

### 12.5.3 Step 3 – Build the Global Analytical Allocation table

**Owners:** Integration / Data Engineering.

For each **Person_ID + Assignment (A1–A4) + period**, the ETL process:

1. Reads the detailed MAB allocation input:
   - `Local Sou Occurrence` (1–4) → assignment index.  
   - `Local Sou %`  
   - `Analytical code` + `Analytical %`  
   - `ERP` (AX / ANAEL / GP)  
   - Person identifiers, dates.

2. Resolves each row to referentials:
   - Use `ERP + Analytical code + Local SOU` to find the **Local Analytical ID**.  
   - From Local Analytical ID, retrieve `Local CoA ID`, `Local SOU Code`, `Activity_Code`, `Product_Code`, etc.  
   - From Local CoA ID, expand to full **CoA segments**.  
   - From Local SOU, retrieve the **SOU Code** and legal context.

3. Computes the **Final Allocation Percent** for each analytical line:

   > `Final_Allocation_Percent = Local_Sou_% × Analytical_% ÷ 100`

4. Inserts rows into the **Global Analytical Allocation** table at the grain:

   > `Person_ID × Assignment_ID (via Local Sou Occurrence) × Local_Analytical_ID × Effective period`

   Including:
   - `ERP_System_Code`  
   - `Local_SOU_Occurrence` (1–4 → A1–A4)  
   - `Local_Analytical_ID`, `Local_CoA_ID`, `Local_SOU_Code`, `SOU_Code`  
   - `Activity_Code`, `Product_Code`, Contract, Import/Export  
   - CoA segments  
   - `Effective_Start_Date`, `Effective_End_Date`  
   - `Final_Allocation_Percent`  
   - `Is_Valid` (initially null or 0).

5. Validates allocations:
   - For each **Person + Assignment + continuous period**:  
     - Sum of `Final_Allocation_Percent` must be **100%** (or 0% if no allocation).  
   - Checks that all referenced Analytical IDs and CoA IDs are **ACTIVE** and valid for the period.  
   - If any check fails: flag those rows with `Is_Valid = 0` and log errors for remediation.

Outcome: a clean, effective‑dated **Global Analytical Allocation** fact table ready for GL, HCM and FTE KPIs.

---

### 12.5.4 Step 4 – Push allocations to GL and/or HCM Payroll

**Scenario A – Payroll outside Fusion (e.g. local payroll + GL only)**

1. For each valid row (`Is_Valid = 1`) in the allocation table:
   - Compute monetary amounts by applying `Final_Allocation_Percent` to the payroll cost base.  
   - Build GL posting lines with the CoA segments from `Local_CoA_ID`.

2. Post these lines to GL, ensuring that **per employee/assignment/period**, the amounts sum to the total payroll cost.

**Scenario B – Payroll in Fusion**

1. For each **Person + Assignment + period** with valid allocations:
   - Create or update a **CostAllocation** object for that assignment with appropriate effective dates.  
   - Create one **CostAllocationAccount** line per analytical row:
     - GL account combination = CoA from `Local_CoA_ID`.  
     - `distributionPercentage = Final_Allocation_Percent`.

2. Ensure that, per CostAllocation header and period, the sum of distribution percentages = **100%**.

Outcome: GL postings and/or Fusion Payroll costing reflect the same governed analytical splits.

---

### 12.5.5 Step 5 – Use the same allocations for FTE KPIs

**Owners:** FP&A / EPM / DataLayer team.

Activities:

1. Consume the **Global Analytical Allocation** table as the source for analytical axes.  
2. For each **Person + Assignment + period**:
   - Compute the base FTE for the assignment (from HR data: contract type, working pattern, dates).  
   - Apply each `Final_Allocation_Percent` to split that FTE across analytical lines.

3. Aggregate FTEs by the desired dimensions:
   - SOU, Local SOU  
   - Activity / Sub‑Function  
   - Product / Cluster  
   - ERP  
   - Legal Entity, Region, LoB.

4. Because both **costs** (GL / Payroll) and **FTEs** (EPM) use the same analytical axes and percentages:
   - Financial and non‑financial KPIs are **fully reconcilable**.  
   - Management can compare "FTEs by SOU/Activity" to "Costs by SOU/Activity" consistently.

Outcome: A single analytical truth for both cost and FTE metrics.

---

### 12.5.6 Step 6 – Optional HCM UI exposure (table‑validated, non‑freetext)

If Oracle HCM must display or (exceptionally) allow manual adjustment of analytical data:

1. Create a **custom reference table** in Fusion (e.g. `XX_MAB_ANALYTICAL_REF`) populated from MAB.
2. Create **table‑validated Value Sets** that:
   - Select `Local_Analytical_ID`, description, and related fields.  
   - Restrict rows by:
     - `ERP_System_Code = :<ERP segment/DFF>`  
     - `Local_SOU_Code = :<Local SOU segment/DFF>`  
     - Optional CoA segment filters  
     - `TRUNC(SYSDATE)` between `Effective_Start_Date` and `Effective_End_Date`  
     - `Status = 'ACTIVE'`.
3. Attach these Value Sets to **DFF segments** on Assignment or Cost Allocation.
4. Optionally, set these DFF segments to **read‑only** so that they are only populated by integration.

Result:

- Even when visible in HCM, analytical fields are **not freetext** and always refer to controlled, time‑valid values.

---

### 12.5.7 Step 7 – Audit, history, and change management

- Because both referentials and allocations are **effective‑dated**, the organisation can always answer:
  - Which Analytical IDs / CoA combinations were valid on any historical date.  
  - How a given employee’s costs and FTEs were allocated at that date.
- No historical records are overwritten; new changes always create new rows with new dates.
- Change management is centralised in MAB/MDM; Oracle HCM and GL are **consumers** of governed data.

---

**Result:**

- Analytical IDs are **never freetext**, but always selected from a governed referential consistent with **ERP / Local SOU / Local CoA**.  
- Allocations are **time‑bound**, per‑assignment, and validated to sum to **100%** per period.  
- Oracle HCM Enterprise Structures remain clean and simple, while GL, Payroll costing, and FTE KPIs all consume the **same controlled analytical allocation model**.

