graph TD

  %% ============= ENTERPRISE & LEGISLATION =============
  subgraph "Enterprise & Legislation"
    E[Enterprise: GEODIS]

    LDG_FRA[LDG: GEODIS FRA]
    LDG_DEU[LDG: GEODIS DEU]
    LDG_OTH[Other LDGs...]

    E --> LDG_FRA
    E --> LDG_DEU
    E --> LDG_OTH

    LE_FRA_00860["Legal Entity: 00860<br>GEODIS D&E Méditerranée"]
    LE_FRA_00740["Legal Entity: 00740<br>GEODIS D&E Yvelines"]

    LDG_FRA --> LE_FRA_00860
    LDG_FRA --> LE_FRA_00740
  end

  %% ============= DIVISIONS / LoB =============
  subgraph "Divisions (LoB)"
    DIV_DE[L1 - Distribution & Express]
    DIV_FF[L1 - Freight Forwarding]
    DIV_CL[L1 - Contract Logistics]
    DIV_CORP[L1 - Corporate]

    E --> DIV_DE
    E --> DIV_FF
    E --> DIV_CL
    E --> DIV_CORP
  end

  %% ============= BUSINESS UNITS (Reporting Units) =============
  subgraph "Business Units (Reporting Units)"
    BU_TA46["BU TA46<br>Reporting Unit: TA46"]
    BU_TA40["BU TA40<br>Reporting Unit: TA40"]
    BU_OTH[Other BUs...]

    DIV_DE --> BU_TA46
    DIV_DE --> BU_TA40
  end

  %% ============= LOCATIONS (Sites) =============
  subgraph "Locations (Legal Sites)"
    LOC_NIMES["Location: FR-NIMES<br>0040604-CALBERSON MEDIT.NIMES"]
    LOC_YVELINES["Location: FR-YVELINES<br>0074078-CALBERSON YVELINE"]
  end

  LE_FRA_00860 --> LOC_NIMES
  LE_FRA_00740 --> LOC_YVELINES

  %% ============= DEPARTMENTS (Org Units / ClientCodes) =============
  subgraph "Departments (Org Units)"
    DEPT_DE_SE_NIMES["Dept: FRA - D&E - SE - Nimes<br>ClientCode: 0040604"]
    DEPT_DE_IDF_YVELINES["Dept: FRA - D&E - IDF - Yvelines<br>ClientCode: 0074078"]

    DEPT_DE_FR_ROOT[Dept: FRA - D&E - FR Root]

    DEPT_DE_FR_ROOT --> DEPT_DE_SE_NIMES
    DEPT_DE_FR_ROOT --> DEPT_DE_IDF_YVELINES
  end

  BU_TA46 --> DEPT_DE_SE_NIMES
  BU_TA46 --> DEPT_DE_IDF_YVELINES

  %% ============= JOBS =============
  subgraph "Jobs"
    JOB_PUD_OFF["Job: Pickup & Delivery Officer<br>Code: 1PUDP_PIANDEOEL"]
    JOB_CS_OPER["Job: Customer Service Operator<br>Code: 1CUSE_CUREOPEL"]
  end

  %% ============= PEOPLE & ASSIGNMENTS =============
  subgraph "People & Assignments"
    P12345[["Person: P12345<br>(e.g. Sixte LE ROUX)"]]

    A1[("Assignment A1<br>Local Sou Occ. 1")]
    A2[("Assignment A2<br>Local Sou Occ. 2")]
    A3[("Assignment A3<br>Local Sou Occ. 3")]
    A4[("Assignment A4<br>Local Sou Occ. 4")]

    P12345 --> A1
    P12345 --> A2
    P12345 --> A3
    P12345 --> A4
  end

  %% ============= ASSIGNMENT ATTRIBUTES (HCM) =============
  %% A1 example: Nimes Pickup & Delivery Officer
  A1 -->|Legal Employer| LE_FRA_00860
  A1 -->|BU| BU_TA46
  A1 -->|Location| LOC_NIMES
  A1 -->|Department| DEPT_DE_SE_NIMES
  A1 -->|Job| JOB_PUD_OFF

  %% A2 example: Yvelines Customer Service Operator
  A2 -->|Legal Employer| LE_FRA_00740
  A2 -->|BU| BU_TA46
  A2 -->|Location| LOC_YVELINES
  A2 -->|Department| DEPT_DE_IDF_YVELINES
  A2 -->|Job| JOB_CS_OPER

  %% A3/A4 could be internal splits or other contracts under same legal employer
  A3 -->|Legal Employer| LE_FRA_00860
  A3 -->|BU| BU_TA46
  A3 -->|Department| DEPT_DE_SE_NIMES

  A4 -->|Legal Employer| LE_FRA_00860
  A4 -->|BU| BU_TA46
  A4 -->|Department| DEPT_DE_SE_NIMES
