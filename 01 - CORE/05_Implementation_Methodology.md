# GEODIS Oracle Fusion HCM Cloud Implementation
## Core HR Repositories - Implementation Methodology & Progress Tracker

---

**Project:** GEODIS New HCM - AMARIS
**Phase:** 02 - Define
**Document:** Implementation Methodology & Knowledge Base
**Version:** 1.0
**Date:** 2025-11-27
**Prepared By:** HCM Implementation Team

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Implementation Methodology](#implementation-methodology)
3. [Repository Categories Overview](#repository-categories-overview)
4. [Oracle Documentation Mapping](#oracle-documentation-mapping)
5. [Configuration Workstreams](#configuration-workstreams)
6. [Progress Tracker](#progress-tracker)
7. [Technical Reference Guide](#technical-reference-guide)

---

## 1. Executive Summary

This document serves as the master implementation guide for configuring Oracle Fusion HCM Cloud Core HR repositories for GEODIS. Following industry best practices from leading consulting firms (Accenture, Deloitte, PwC, KPMG), this methodology ensures:

- **Structured Approach**: Systematic configuration following Oracle's recommended sequence
- **Traceability**: Clear mapping between business requirements and technical configuration
- **Quality Assurance**: Validation checkpoints at each configuration milestone
- **Knowledge Transfer**: Comprehensive documentation for client enablement

### Scope Overview

| Category | # of Repositories | Status |
|----------|------------------|--------|
| Organization Structure | 18 | To fill-in |
| Workforce Structure | 6 | To fill-in |
| Personal Details | 20 | To fill-in |
| Employment Details | 11 | To fill-in |
| Compensation Details | 4 | To fill-in |
| Process and Security | 5 | To fill-in |
| **Total** | **64** | **In Progress** |

---

## 2. Implementation Methodology

### 2.1 Oracle Fusion HCM Configuration Sequence

Following Oracle's recommended implementation sequence (Critical Path):

```
Phase 1: Foundation Setup
├── Enterprise Definition
├── Legal Entity Configuration
├── Legislative Data Groups
└── Geographic Structures

Phase 2: Organization Structures
├── Business Units
├── Departments
├── Locations
└── Organization Hierarchies (Trees)

Phase 3: Workforce Structures
├── Job Families & Functions
├── Jobs
├── Grades & Grade Ladders
└── Positions

Phase 4: Person Configuration
├── Person Types
├── Name/Address Formats
├── Document Types
└── Legislative Data (Country-specific)

Phase 5: Employment Configuration
├── Assignment Statuses
├── Worker Categories
├── Contract Types
└── Collective Agreements

Phase 6: Compensation Configuration
├── Salary Basis
├── Compensation Elements
└── Payroll Relationships

Phase 7: Security & Workflows
├── Actions & Action Reasons
├── Security Roles
├── Approval Workflows
└── Quick Actions
```

### 2.2 Repository Configuration Approach (RACI)

| Activity | Business (GEODIS) | Implementation Partner | Oracle |
|----------|-------------------|----------------------|--------|
| Provide Business Requirements | **R/A** | C | I |
| Configure Standard Values | I | **R/A** | C |
| Configure Custom Values | C | **R/A** | I |
| Validate Configuration | **R/A** | C | I |
| Sign-off | **R/A** | I | I |

**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed

---

## 3. Repository Categories Overview

### 3.1 Organization Structure (18 Repositories)

| # | Repository | Oracle Provided | Modifiable | Priority | Dependencies |
|---|------------|-----------------|------------|----------|--------------|
| 1 | Country Code | Yes | No | P1 | None |
| 2 | Geography | Yes | No | P1 | Country Code |
| 3 | Legislative Data Group | No | Yes | P1 | Country Code |
| 4 | Enterprise HCM | Yes | No | P1 | None |
| 5 | Legal Address | No | Yes | P1 | Geography |
| 6 | Legal Entity | No | Yes | P1 | LDG, Legal Address |
| 7 | Division | No | Yes | P2 | Enterprise |
| 8 | Data Set | Partial | Yes | P2 | Business Unit |
| 9 | Business Unit | No | Yes | P1 | Legal Entity |
| 10 | BU Set Assignment | Partial | Yes | P2 | Data Set, BU |
| 11 | Location | No | Yes | P1 | Legal Entity, Geography |
| 12 | Department | No | Yes | P1 | Business Unit, Location |
| 13 | Department Tree | No | Yes | P2 | Department |
| 14 | Organization Tree | No | Yes | P2 | Multiple Orgs |
| 15 | Reporting Establishment | No | Yes | P2 | Legal Entity |
| 16 | Time Zone | Yes | Yes | P3 | None |
| 17 | Cost Center | No | Yes | P2 | Department |
| 18 | Source System Owner | Partial | Yes | P3 | None |

### 3.2 Workforce Structure (6 Repositories)

| # | Repository | Oracle Provided | Modifiable | Priority | Dependencies |
|---|------------|-----------------|------------|----------|--------------|
| 1 | Job Family | No | Yes | P1 | None |
| 2 | Job Function | Yes | Yes | P1 | None |
| 3 | Management Level | Yes | Yes | P2 | None |
| 4 | Job | No | Yes | P1 | Job Family, Job Function |
| 5 | Grade | No | Yes | P1 | LDG |
| 6 | Position | No | Yes | P2 | Job, Department, Location, Grade |
| 7 | Grade Step | No | Yes | P3 | Grade |
| 8 | Currency | Yes | Yes | P1 | None |

### 3.3 Personal Details (20 Repositories)

| # | Repository | Oracle Provided | Modifiable | Priority |
|---|------------|-----------------|------------|----------|
| 1 | Person Type | Yes | Yes | P1 |
| 2 | Name Styles | Yes | Yes | P2 |
| 3 | Name Formats | Yes | Yes | P2 |
| 4 | Titles | Yes | Yes | P3 |
| 5 | Address Format | Yes | Yes | P2 |
| 6 | Address Type | Yes | Yes | P2 |
| 7 | E-Mail Type | Yes | Yes | P3 |
| 8 | Gender | Yes | No | P1 |
| 9 | Phone Type | Yes | Yes | P3 |
| 10 | Marital Statuses | Yes | Yes | P2 |
| 11 | Highest Education Level | Yes | Yes | P3 |
| 12 | National ID | Yes | Yes | P1 |
| 13 | Contact | Yes | Yes | P2 |
| 14 | Statutory Dependent | Yes | Yes | P2 |
| 15 | Passport | Yes | Yes | P3 |
| 16 | Citizenship Status | Yes | Yes | P3 |
| 17 | Driver Licence | Yes | Yes | P3 |
| 18 | Visa & Permits | Yes | Yes | P2 |
| 19 | Document Type | Yes | Yes | P2 |
| 20 | Document Category | Yes | Yes | P2 |

### 3.4 Employment Details (11 Repositories)

| # | Repository | Oracle Provided | Modifiable | Priority |
|---|------------|-----------------|------------|----------|
| 1 | Worker Category | Yes | Yes | P1 |
| 2 | Assignment Category | Yes | Yes | P1 |
| 3 | Assignment Status | Yes | Yes | P1 |
| 4 | Hourly-Salaried | Yes | Yes | P2 |
| 5 | Regular or Temporary | Yes | Yes | P2 |
| 6 | Seniority Rules | Yes | Yes | P3 |
| 7 | Frequency Working Hours | Yes | No | P1 |
| 8 | Manager Type | Yes | Yes | P2 |
| 9 | Contract Type | Yes | Yes | P1 |
| 10 | Collective Agreement | No | Yes | P2 |
| 11 | Mandat Type | Yes | Yes | P3 |

### 3.5 Compensation Details (4 Repositories)

| # | Repository | Oracle Provided | Modifiable | Priority |
|---|------------|-----------------|------------|----------|
| 1 | Payroll Relationship | No | Yes | P1 |
| 2 | Comp. Elements | No | Yes | P1 |
| 3 | Salary Basis | No | Yes | P1 |
| 4 | Frequency Salary | Yes | No | P1 |

### 3.6 Process and Security (5 Repositories)

| # | Repository | Oracle Provided | Modifiable | Priority |
|---|------------|-----------------|------------|----------|
| 1 | Action | Yes | Yes | P1 |
| 2 | Action & Reasons | Yes | Yes | P1 |
| 3 | Security Matrix | Partial | Yes | P1 |
| 4 | Core Data Model | N/A | N/A | P2 |
| 5 | Approval Workflows | Partial | Yes | P2 |

---

## 4. Oracle Documentation Mapping

### 4.1 Primary Documentation Sources

| Document | Relevant Repositories | Key Topics |
|----------|----------------------|------------|
| `understanding-enterprise-structures.pdf` | Enterprise, Legal Entity, BU, Division, LDG | Enterprise structure design, Legal employer setup |
| `using-common-features-for-hcm.pdf` | All repositories | Common features, lookups, profiles |
| `implementing-talent-management-base.pdf` | Job, Position, Grade, Person | Core workforce configuration |
| `hcm-data-loader.pdf` | All repositories | Data migration, bulk loading |
| `securing-hcm.pdf` | Security Matrix, Roles | Security configuration |
| `configuring-and-extending-applications.pdf` | All repositories | Customization, flexfields |
| `security-reference-for-hcm.pdf` | Security Matrix | Role hierarchy, data security |

### 4.2 Country-Specific Documentation

For GEODIS operations in multiple countries, refer to:
- Legislative Data Group setup per country
- Country-specific person types
- National identifier formats
- Statutory compliance requirements

---

## 5. Configuration Workstreams

### Workstream 1: Enterprise Foundation
**Owner:** [TBD]
**Status:** Not Started

**Deliverables:**
- [ ] Enterprise structure defined
- [ ] Legal Entities configured
- [ ] Legislative Data Groups created
- [ ] Legal addresses maintained

### Workstream 2: Organization Design
**Owner:** [TBD]
**Status:** Not Started

**Deliverables:**
- [ ] Business Units created
- [ ] Departments defined
- [ ] Locations configured
- [ ] Organization trees built

### Workstream 3: Workforce Structures
**Owner:** [TBD]
**Status:** Not Started

**Deliverables:**
- [ ] Job families & functions defined
- [ ] Jobs configured
- [ ] Grades & grade ladders set up
- [ ] Positions created (if applicable)

### Workstream 4: Person & Employment
**Owner:** [TBD]
**Status:** Not Started

**Deliverables:**
- [ ] Person types validated
- [ ] Name/address formats configured
- [ ] Employment lookups customized
- [ ] Contract types defined

### Workstream 5: Security & Process
**Owner:** [TBD]
**Status:** Not Started

**Deliverables:**
- [ ] Actions & reasons configured
- [ ] Security roles defined
- [ ] Approval workflows designed
- [ ] Quick actions enabled

---

## 6. Progress Tracker

### Overall Progress

| Phase | Status | % Complete | Last Updated |
|-------|--------|------------|--------------|
| Foundation Setup | Not Started | 0% | 2025-11-27 |
| Organization Structures | Not Started | 0% | 2025-11-27 |
| Workforce Structures | Not Started | 0% | 2025-11-27 |
| Person Configuration | Not Started | 0% | 2025-11-27 |
| Employment Configuration | Not Started | 0% | 2025-11-27 |
| Compensation Configuration | Not Started | 0% | 2025-11-27 |
| Security & Workflows | Not Started | 0% | 2025-11-27 |

### Detailed Repository Status

#### Organization Structure Repositories

| Repository | Design | Build | Test | Sign-off |
|------------|--------|-------|------|----------|
| Country Code | N/A | N/A | N/A | N/A |
| Geography | - | - | - | - |
| Legislative Data Group | - | - | - | - |
| Enterprise HCM | - | - | - | - |
| Legal Address | - | - | - | - |
| Legal Entity | - | - | - | - |
| Division | - | - | - | - |
| Data Set | - | - | - | - |
| Business Unit | - | - | - | - |
| BU Set Assignment | - | - | - | - |
| Location | - | - | - | - |
| Department | - | - | - | - |
| Department Tree | - | - | - | - |
| Organization Tree | - | - | - | - |
| Reporting Establishment | - | - | - | - |
| Time Zone | N/A | N/A | N/A | N/A |

---

## 7. Technical Reference Guide

### 7.1 Oracle Fusion HCM Data Model Concepts

#### Enterprise Structure Hierarchy
```
Enterprise (Single Instance)
└── Legal Entity (Can be Legal Employer & Payroll Statutory Unit)
    ├── Business Unit (Operational unit)
    │   ├── Department
    │   │   └── Cost Center
    │   └── Location
    └── Division (Optional grouping)
```

#### Workforce Structure Hierarchy
```
Job Family
└── Job
    └── Position (Optional)
        └── Grade/Grade Ladder
```

### 7.2 Key Oracle Configuration Objects

| Object | Setup Task | Navigation |
|--------|-----------|------------|
| Enterprise | Define Enterprise | Setup > Enterprise |
| Legal Entity | Manage Legal Entities | Setup > Legal Entity |
| Business Unit | Manage Business Units | Setup > Business Unit |
| Department | Manage Departments | Setup > Organization |
| Job | Manage Jobs | Setup > Workforce Structures |
| Position | Manage Positions | Setup > Workforce Structures |
| Grade | Manage Grades | Setup > Workforce Structures |

### 7.3 HCM Data Loader (HDL) Reference

For bulk data loading, use HCM Data Loader with these business objects:

| Repository | HDL Business Object | File Template |
|------------|--------------------| --------------|
| Legal Entity | LegalEntity.dat | LegalEntity_Template |
| Business Unit | BusinessUnit.dat | BusinessUnit_Template |
| Department | Department.dat | Department_Template |
| Location | Location.dat | Location_Template |
| Job | Job.dat | Job_Template |
| Position | Position.dat | Position_Template |
| Grade | Grade.dat | Grade_Template |
| Worker | Worker.dat | Worker_Template |

### 7.4 Common Value Sets & Lookups

| Lookup Type | Purpose | Modifiable |
|-------------|---------|------------|
| HWM_PERSON_TYPE | Person types | Yes (add custom) |
| PER_ASSIGNMENT_STATUS | Assignment statuses | Yes (add custom) |
| PER_CONTACT_RELSHIP_TYPE | Contact relationships | Yes (add custom) |
| HR_ACTION | HR Actions | Yes (add reasons) |
| PER_ACTN_REASON | Action reasons | Yes |

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-11-27 | HCM Team | Initial document creation |

---

*This document follows Oracle Fusion HCM Cloud implementation best practices and methodology guidelines.*
