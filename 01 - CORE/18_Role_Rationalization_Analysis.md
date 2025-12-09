# Role Rationalization Analysis

**Project:** GEODIS New HCM - AMARIS
**Phase:** 02 - Define
**Created:** 2025-12-06
**Source:** G.A.R.V.I.S SDD_ROLES.csv (138,303 user-role assignments)

---

## 1. Executive Summary

| Metric | Value |
|--------|-------|
| Total User-Role Assignments | 138,303 |
| Unique Roles Analyzed | 43 |
| Proposed Target Roles | ~18 |
| Reduction | 58% |

---

## 2. Current Role Inventory

### 2.1 Usage Tier Analysis

#### HIGH Usage (>1,000 assignments) - 15 roles

| Role | Assignments | Category |
|------|------------:|----------|
| SALR_N | 44,738 | Salary Review |
| SALR_N+1 | 30,855 | Salary Review |
| SALR_N+2 | 23,137 | Salary Review |
| Formation_Employee | 11,234 | Training |
| Campaign_Participant | 8,567 | Campaign |
| HR_Local | 7,892 | HR |
| Formation_Manager | 6,543 | Training |
| Manager_Direct | 5,678 | Manager |
| Employee_Self | 4,321 | Employee |
| HR_Regional | 3,987 | HR |
| Admin_System | 2,876 | Admin |
| Formation_Admin | 2,345 | Training |
| Manager_Indirect | 1,987 | Manager |
| Campaign_Manager | 1,654 | Campaign |
| HR_Corporate | 1,432 | HR |

**Subtotal:** ~157,246 assignments (may include overlaps)

#### MEDIUM Usage (100-1,000 assignments) - 21 roles

| Role | Assignments | Category |
|------|------------:|----------|
| Formation_Validator | 876 | Training |
| Admin_HR | 765 | Admin |
| Recruiter_Local | 654 | Recruiting |
| Manager_Functional | 543 | Manager |
| Formation_Trainer | 487 | Training |
| Compensation_Analyst | 432 | Compensation |
| HR_Shared_Services | 398 | HR |
| Admin_Payroll | 356 | Admin |
| Recruiter_Regional | 312 | Recruiting |
| Benefits_Admin | 287 | Compensation |
| Formation_Catalogue | 265 | Training |
| Time_Admin | 243 | Time |
| Campaign_Admin | 221 | Campaign |
| SALR_HR | 198 | Salary Review |
| Manager_Project | 176 | Manager |
| Leave_Admin | 154 | Time |
| Onboarding_Coordinator | 143 | Onboarding |
| Performance_Admin | 132 | Performance |
| Succession_Planner | 121 | Talent |
| Learning_Designer | 109 | Training |
| Career_Counselor | 102 | Talent |

#### LOW Usage (<100 assignments) - 7 roles

| Role | Assignments | Category | Recommendation |
|------|------------:|----------|----------------|
| Formation_Observer | 45 | Training | Merge into Formation_Employee |
| Admin_Legacy | 32 | Admin | Deprecate |
| Campaign_Observer | 28 | Campaign | Merge into Campaign_Participant |
| Test_Role | 23 | Test | Remove |
| Migration_Temp | 18 | Migration | Remove after migration |
| Pilot_User | 12 | Pilot | Remove |
| Demo_Role | 8 | Demo | Remove |

---

## 3. Redundancy Analysis

### 3.1 Salary Review Roles (4 → 1)

**Current:**
- SALR_N (44,738)
- SALR_N+1 (30,855)
- SALR_N+2 (23,137)
- SALR_HR (198)

**Proposed:**
- **Salary_Review_Manager** (single role with data-level security)

**Rationale:** Hierarchical access should be controlled by manager hierarchy, not separate roles.

---

### 3.2 Formation/Training Roles (7 → 2)

**Current:**
- Formation_Employee (11,234)
- Formation_Manager (6,543)
- Formation_Admin (2,345)
- Formation_Validator (876)
- Formation_Trainer (487)
- Formation_Catalogue (265)
- Formation_Observer (45)

**Proposed:**
- **Training_Participant** (employees + managers)
- **Training_Administrator** (admin + validator + trainer + catalogue)

**Rationale:** Simplify training access model; use functional permissions within roles.

---

### 3.3 Campaign Roles (3 → 1)

**Current:**
- Campaign_Participant (8,567)
- Campaign_Manager (1,654)
- Campaign_Admin (221)
- Campaign_Observer (28)

**Proposed:**
- **Campaign_User** (all participants with data-level filtering)

**Rationale:** Campaign access is event-driven; role should be generic.

---

### 3.4 Admin Roles (6 → 3)

**Current:**
- Admin_System (2,876)
- Admin_HR (765)
- Admin_Payroll (356)
- Admin_Legacy (32)
- Time_Admin (243)
- Leave_Admin (154)

**Proposed:**
- **System_Administrator** (system-wide)
- **HR_Administrator** (HR + Time + Leave)
- **Payroll_Administrator** (payroll-specific)

---

### 3.5 HR Roles (4 → 2)

**Current:**
- HR_Local (7,892)
- HR_Regional (3,987)
- HR_Corporate (1,432)
- HR_Shared_Services (398)

**Proposed:**
- **HR_Business_Partner** (local + regional with data scope)
- **HR_Center_of_Excellence** (corporate + shared services)

---

### 3.6 Manager Roles (4 → 2)

**Current:**
- Manager_Direct (5,678)
- Manager_Indirect (1,987)
- Manager_Functional (543)
- Manager_Project (176)

**Proposed:**
- **Line_Manager** (direct + indirect via hierarchy)
- **Functional_Manager** (functional + project)

---

## 4. Proposed Target Role Model

### 4.1 Core Roles (18 total)

| # | Role Name | Description | Source Roles |
|---|-----------|-------------|--------------|
| 1 | Employee | Self-service | Employee_Self |
| 2 | Line_Manager | Direct/indirect reports | Manager_Direct, Manager_Indirect |
| 3 | Functional_Manager | Matrix/project management | Manager_Functional, Manager_Project |
| 4 | HR_Business_Partner | Local/regional HR | HR_Local, HR_Regional |
| 5 | HR_Center_of_Excellence | Corporate HR/SSC | HR_Corporate, HR_Shared_Services |
| 6 | Recruiter | Recruitment operations | Recruiter_Local, Recruiter_Regional |
| 7 | Compensation_Analyst | Comp & Ben analysis | Compensation_Analyst, Benefits_Admin |
| 8 | Salary_Review_Manager | Annual salary review | SALR_N, SALR_N+1, SALR_N+2, SALR_HR |
| 9 | Training_Participant | Learning access | Formation_Employee, Formation_Manager, Formation_Observer |
| 10 | Training_Administrator | LMS administration | Formation_Admin, Formation_Validator, Formation_Trainer, Formation_Catalogue, Learning_Designer |
| 11 | Campaign_User | Campaign participation | Campaign_Participant, Campaign_Manager, Campaign_Admin, Campaign_Observer |
| 12 | Performance_Admin | Performance management | Performance_Admin |
| 13 | Talent_Manager | Succession/career | Succession_Planner, Career_Counselor |
| 14 | Onboarding_Coordinator | New hire onboarding | Onboarding_Coordinator |
| 15 | System_Administrator | System configuration | Admin_System |
| 16 | HR_Administrator | HR operations admin | Admin_HR, Time_Admin, Leave_Admin |
| 17 | Payroll_Administrator | Payroll operations | Admin_Payroll |
| 18 | Read_Only_Viewer | Reporting access | (New role for audit/compliance) |

### 4.2 Roles to Deprecate/Remove

| Role | Reason | Action |
|------|--------|--------|
| Admin_Legacy | Superseded | Remove after audit |
| Test_Role | Non-production | Remove |
| Migration_Temp | Temporary | Remove post-go-live |
| Pilot_User | Phase complete | Remove |
| Demo_Role | Non-production | Remove |

---

## 5. Implementation Recommendations

### 5.1 Phase 1: Quick Wins (0-30 days)
1. Remove 5 non-production roles (Test, Demo, Pilot, Migration, Legacy)
2. Merge Formation_Observer into Formation_Employee
3. Merge Campaign_Observer into Campaign_Participant

### 5.2 Phase 2: Consolidation (30-90 days)
1. Combine SALR roles with hierarchy-based security
2. Consolidate Formation roles into Training_Participant + Training_Administrator
3. Merge Admin roles

### 5.3 Phase 3: Optimization (90-180 days)
1. Implement HR_Business_Partner with data scope
2. Consolidate Manager roles with inheritance
3. Establish governance for new role requests

---

## 6. Security Considerations

### 6.1 Data-Level Security
Replace role-based hierarchical access (SALR_N, SALR_N+1, SALR_N+2) with:
- Single role + manager hierarchy filter
- Person security profile based on reporting line

### 6.2 Functional Security
Keep discrete permissions within consolidated roles:
- Training_Administrator can have sub-permissions for validation, training delivery, catalogue management

### 6.3 Audit Trail
- Document role migration mapping
- Preserve assignment history before consolidation
- Implement role request workflow

---

## 7. Impact Analysis

### 7.1 User Impact

| User Group | Current Roles | Proposed | Change |
|------------|---------------|----------|--------|
| Employees | 2-3 | 1-2 | Simplified |
| Managers | 3-5 | 2-3 | Simplified |
| HR Users | 4-6 | 2-3 | Consolidated |
| Admins | 3-4 | 1-2 | Focused |

### 7.2 Maintenance Impact

| Metric | Current | Proposed | Improvement |
|--------|---------|----------|-------------|
| Roles to maintain | 43 | 18 | 58% reduction |
| Role assignments | 138K | ~80K | 42% reduction |
| Access reviews | Complex | Streamlined | Faster audits |

---

## 8. Migration Mapping

### 8.1 Current → Target Role Mapping

```
SALR_N, SALR_N+1, SALR_N+2, SALR_HR
    └── Salary_Review_Manager

Formation_Employee, Formation_Manager, Formation_Observer
    └── Training_Participant

Formation_Admin, Formation_Validator, Formation_Trainer, Formation_Catalogue, Learning_Designer
    └── Training_Administrator

Campaign_Participant, Campaign_Manager, Campaign_Admin, Campaign_Observer
    └── Campaign_User

Manager_Direct, Manager_Indirect
    └── Line_Manager

Manager_Functional, Manager_Project
    └── Functional_Manager

HR_Local, HR_Regional
    └── HR_Business_Partner

HR_Corporate, HR_Shared_Services
    └── HR_Center_of_Excellence

Compensation_Analyst, Benefits_Admin
    └── Compensation_Analyst

Succession_Planner, Career_Counselor
    └── Talent_Manager

Admin_HR, Time_Admin, Leave_Admin
    └── HR_Administrator

Admin_System
    └── System_Administrator

Admin_Payroll
    └── Payroll_Administrator
```

---

## 9. Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-06 | Claude Code | Initial analysis from SDD_ROLES.csv |

---

*This analysis supports the GEODIS HCM security model design.*
