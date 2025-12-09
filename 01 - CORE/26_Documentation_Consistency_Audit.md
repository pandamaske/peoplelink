# Documentation Consistency Audit

**Project:** GEODIS New HCM - AMARIS
**Phase:** 02 - Define
**Created:** 2025-12-07
**Purpose:** Cross-reference audit of all documentation files vs actual Excel repository counts

---

## 1. Executive Summary

This audit cross-references record counts stated in documentation files against actual Excel file contents in the `04 - SHEETS` folder.

**Key Findings:**
- **70 total Excel files** in `04 - SHEETS`
- **58,460 total records** across all populated sheets
- **15 significant discrepancies** identified requiring documentation updates
- **01_Agent_Session_Tracker.md** contains the most outdated counts (from earlier sessions)

---

## 2. Actual Record Counts (Source of Truth)

### 2.1 Organization Structure (16 files)

| Repository | Actual Records | Status |
|------------|---------------:|:------:|
| Enterprise HCM | 1 | OK |
| Legislative Data Group | 62 | OK |
| Legal Entity | 364 | OK |
| Legal Address | 2,046 | OK |
| Division | 19 | OK |
| Business Unit | 2,175 | OK |
| Data Set | 1 | OK |
| BU Set Assignment | 2,175 | OK |
| Department | 10,803 | OK |
| Department Tree | 10,802 | OK |
| Organization Tree | 40 | OK |
| Location | 919 | OK |
| Reporting Establishment | 2,046 | OK |
| Country Code | 0 | Oracle Seeded |
| Geography | 0 | Oracle Seeded |
| Time Zone | 0 | Oracle Seeded |

**Subtotal:** 31,453 records

### 2.2 Workforce Structure (9 files)

| Repository | Actual Records | Status |
|------------|---------------:|:------:|
| Job | 688 | OK |
| Job Family | 27 | OK |
| Job Sub Family | 79 | OK |
| Job Function | 236 | OK |
| Management Level | 5 | OK |
| Grade | 20 | OK |
| Grade Step | 0 | TBD |
| Position | 24,398 | OK |
| Currencies | 0 | Oracle Seeded |

**Subtotal:** 25,453 records

### 2.3 Personal Details (24 files)

| Repository | Actual Records | Status |
|------------|---------------:|:------:|
| Titles | 7 | OK |
| Gender | 3 | OK |
| Marital Statuses | 6 | OK |
| Highest Education Level | 10 | OK |
| Document Category | 26 | OK |
| Document Type | 98 | OK |
| Other (18 files) | 0 | Oracle Seeded |

**Subtotal:** 150 records

### 2.4 Employment Details (10 files)

| Repository | Actual Records | Status |
|------------|---------------:|:------:|
| Collective Agreement | 112 | OK |
| Contract Type | 151 | OK |
| Assignment Category | 4 | OK |
| Assignment Status | 4 | OK |
| Worker Category | 4 | OK |
| Hourly-Salaried | 2 | OK |
| Regular or Temporary | 2 | OK |
| Manager Type | 6 | OK |
| Seniority Rules | 3 | OK |
| Frequency Working Hours | 8 | OK |

**Subtotal:** 296 records

### 2.5 Compensation Details (6 files)

| Repository | Actual Records | Status |
|------------|---------------:|:------:|
| Comp. Elements | 35 | OK |
| Salary Basis | 4 | OK |
| Frequence Salary | 8 | OK |
| Payroll Relationship | 2 | OK |
| Individual Compensation Plan | 3 | OK |
| Compensation History | 1 | OK |

**Subtotal:** 53 records

### 2.6 Process and Security (5 files)

| Repository | Actual Records | Status |
|------------|---------------:|:------:|
| Action | 44 | OK |
| Action & Reasons | 70 | OK |
| Security Matrix | 308 | OK |
| Approval Workflows | 34 | OK |
| Core Data Model | 599 | OK |

**Subtotal:** 1,055 records

---

## 3. Discrepancy Analysis by Document

### 3.1 01_Agent_Session_Tracker.md (CRITICAL - Many Outdated)

This document contains counts from earlier sessions (Session 3, 2025-11-28) that are now outdated.

| Repository | Doc Value | Actual | Variance | Action |
|------------|----------:|-------:|---------:|--------|
| Legislative Data Group | 80 | 62 | -18 | UPDATE |
| Legal Entity | 367 | 364 | -3 | UPDATE |
| Legal Address | 367 | 2,046 | +1,679 | UPDATE |
| Division | 35 | 19 | -16 | UPDATE |
| **Business Unit** | **27** | **2,175** | **+2,148** | **UPDATE** |
| Location | 2,046 | 919 | -1,127 | UPDATE |
| Department | 10,811 | 10,803 | -8 | UPDATE |
| Department Tree | 10,811 | 10,802 | -9 | UPDATE |
| Reporting Establishment | 2,049 | 2,046 | -3 | UPDATE |
| **Job Family** | **842** | **27** | **-815** | **UPDATE** |
| **Job** | **334** | **688** | **+354** | **UPDATE** |
| Grade | 22 | 20 | -2 | UPDATE |
| **Assignment Category** | **75** | **4** | **-71** | **UPDATE** |

**Root Cause:** Document reflects Session 3 counts before major data restructuring. Job Family 842 was the old hierarchy approach; current approach has 27 Job Families with 79 Sub Families and 236 Functions below them.

---

### 3.2 16_Repository_Population_Methodology.md (Mostly Correct)

| Repository | Doc Value | Actual | Variance | Action |
|------------|----------:|-------:|---------:|--------|
| Approval Workflows | 4 | 34 | +30 | UPDATE |
| Action | 9 | 44 | +35 | UPDATE |
| Action & Reasons | 14 | 70 | +56 | UPDATE |
| Security Matrix | 53 | 308 | +255 | UPDATE |

**Root Cause:** Process and Security section was populated after this document was written.

---

### 3.3 17_Mapping_Organization_Structure.md (Minor Issues)

| Repository | Doc Value | Actual | Variance | Action |
|------------|----------:|-------:|---------:|--------|
| Division | 21 | 19 | -2 | UPDATE |
| Department | 21,834 | 10,803 | -11,031 | UPDATE |

**Root Cause:**
- Division 21 was the initial count from Business Hierarchy L2 before filtering inactive
- Department 21,834 was the raw count from HubLibraries_Departments.json before de-duplication

---

### 3.4 19_Repository_Schema_Reference.md (Correct)

Most counts in this document match actual values. One discrepancy:

| Repository | Doc Value | Actual | Variance | Action |
|------------|----------:|-------:|---------:|--------|
| Contract Type | 62 | 151 | +89 | UPDATE |

**Root Cause:** Contract Type was later enriched with additional GEODIS-specific contract types.

---

### 3.5 00_DOCUMENTATION_INDEX.md (Correct Summary)

The totals listed (~27,000 records in v2 workbook) are from the older consolidated workbook, not the current 04-SHEETS folder structure.

| Section | Doc Value | Actual | Action |
|---------|----------:|-------:|--------|
| Total records | ~27,000 | 58,460 | UPDATE |

---

## 4. Root Cause Analysis

### 4.1 Session 3 vs Current State

**Session 3 (2025-11-28) approach:**
- Job Family: 842 (all AF nodes as families)
- Job: 334 (leaf nodes only)
- Business Unit: 27 (from Business Hierarchy)

**Current State (2025-12-06) approach:**
- Job Family: 27 (AF L4 only)
- Job Sub Family: 79 (AF L5)
- Job Function: 236 (JobRepo parent nodes)
- Job: 688 (active JobRepo leaves)
- Business Unit: 2,175 (from SOUs View)

### 4.2 Source Data Evolution

| Data | Session 3 Source | Current Source |
|------|------------------|----------------|
| Business Unit | Business Hierarchy (27 L2 nodes) | SOUs View (2,175 active) |
| Job Structure | Flat AF hierarchy | 4-level hierarchy (JF > JSF > JFunc > Job) |
| Department | 10,811 from OrganisationalUnit | 10,803 from HubLibraries_Departments.json |
| Location | Legal Sites (2,046) | Site View (919) |

---

## 5. Remediation Plan

### 5.1 Priority 1 - Critical Updates

| Document | Section | Current | Correct |
|----------|---------|--------:|--------:|
| 01_Agent_Session_Tracker.md | Business Unit | 27 | 2,175 |
| 01_Agent_Session_Tracker.md | Job Family | 842 | 27 |
| 01_Agent_Session_Tracker.md | Job | 334 | 688 |
| 01_Agent_Session_Tracker.md | Assignment Category | 75 | 4 |

### 5.2 Priority 2 - Process Updates

| Document | Section | Current | Correct |
|----------|---------|--------:|--------:|
| 16_Repository_Population_Methodology.md | Security Matrix | 53 | 308 |
| 16_Repository_Population_Methodology.md | Action | 9 | 44 |
| 16_Repository_Population_Methodology.md | Action & Reasons | 14 | 70 |
| 16_Repository_Population_Methodology.md | Approval Workflows | 4 | 34 |

### 5.3 Priority 3 - Minor Updates

| Document | Section | Current | Correct |
|----------|---------|--------:|--------:|
| 01_Agent_Session_Tracker.md | Multiple fields | Various | See table above |
| 17_Mapping_Organization_Structure.md | Department | 21,834 | 10,803 |
| 19_Repository_Schema_Reference.md | Contract Type | 62 | 151 |
| 00_DOCUMENTATION_INDEX.md | Total records | ~27,000 | 58,460 |

---

## 6. Confirmed Accurate Documents

The following documents have correct or nearly-correct counts:

| Document | Status | Notes |
|----------|--------|-------|
| 03_MDM_to_HCM_Mapping.md | OK | Contains ranges ("500+", "1000+") not exact counts |
| 05_Implementation_Methodology.md | OK | Contains repository counts, not record counts |
| 19_Repository_Schema_Reference.md | MOSTLY OK | Only Contract Type needs update |

---

## 7. Grand Total Summary

### 7.1 Actual Repository Counts

| Category | Files | Records |
|----------|------:|--------:|
| Organization Structure | 16 | 31,453 |
| Workforce Structure | 9 | 25,453 |
| Personal Details | 24 | 150 |
| Employment Details | 10 | 296 |
| Compensation Details | 6 | 53 |
| Process and Security | 5 | 1,055 |
| **TOTAL** | **70** | **58,460** |

### 7.2 Populated vs Empty

| Status | Files | Records |
|--------|------:|--------:|
| Populated (>0 records) | 47 | 58,460 |
| Oracle Seeded / Empty | 23 | 0 |
| **TOTAL** | **70** | **58,460** |

---

## 8. Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-07 | Claude Code | Initial consistency audit |

---

*This audit establishes the actual Excel file counts as the source of truth. All documentation should be updated to reflect these values.*
