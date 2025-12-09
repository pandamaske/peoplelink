# UKG Fields That Will Be MISSED in Talentsoft

**Purpose:** Critical checklist of UKG data that has NO equivalent in Talentsoft and will be LOST during migration.

---

## CRITICAL: Data Loss Summary

| Category | Fields Lost | Risk Level |
|----------|-------------|------------|
| **Incumbent Tracking** | 3 | HIGH |
| **Name Details (Title/Middle/Suffix)** | 12 | MEDIUM |
| **FTE Granularity** | 4 | HIGH |
| **Pre-calculated Metrics** | 5 | HIGH |
| **Licenses/Certifications** | 2 | MEDIUM |
| **Total** | **26** | - |

---

## 1. INCUMBENT INFORMATION - NO EQUIVALENT

**Risk: HIGH - Complete data loss**

| UKG Field | Description | Talentsoft Status |
|-----------|-------------|-------------------|
| `Incumbent First Name` | Current job holder's first name | **NOT AVAILABLE** |
| `Incumbent Last Name` | Current job holder's last name | **NOT AVAILABLE** |
| `Incumbent Name (Last, First)` | Full name concatenated | **NOT AVAILABLE** |
| `Last Day Worked` | Incumbent's last working day | **NOT AVAILABLE** |

**Impact:**
- Cannot track who currently holds the position being recruited for
- No replacement context for hiring managers
- Historical incumbent data will be lost

**Workaround:**
- Store in `Offer CustomFields` as free text
- Or maintain separate incumbent tracking system

---

## 2. NAME GRANULARITY - SIMPLIFIED IN TALENTSOFT

**Risk: MEDIUM - Partial data loss**

Talentsoft only stores **First Name + Last Name** for managers/recruiters. These fields will be LOST:

### Hiring Manager
| UKG Field | Talentsoft |
|-----------|------------|
| `Title (Mr., Mrs., Dr.)` | **LOST** |
| `Middle Name` | **LOST** |
| `Suffix (Jr., Sr., III)` | **LOST** |

### Onboarding Owner
| UKG Field | Talentsoft |
|-----------|------------|
| `Title` | **LOST** |
| `Middle Name` | **LOST** |
| `Suffix` | **LOST** |

### Supervisor
| UKG Field | Talentsoft |
|-----------|------------|
| `Title` | **LOST** |
| `Middle Name` | **LOST** |
| `Suffix` | **LOST** |

### Recruiter
| UKG Field | Talentsoft |
|-----------|------------|
| `Title` | **LOST** |
| `Middle Name` | **LOST** |
| `Suffix` | **LOST** |

**Impact:**
- Formal name prefixes/suffixes not preserved
- May affect formal communications
- 12 fields total across 4 roles

**Workaround:**
- Concatenate into First Name field: "Dr. John Michael Jr." → FirstName
- Accept loss if not business critical

---

## 3. FTE/HEADCOUNT GRANULARITY - COLLAPSED TO SINGLE FIELD

**Risk: HIGH - Loss of tracking capability**

| UKG Field | What It Tracks | Talentsoft |
|-----------|----------------|------------|
| `Budgeted FTE` | Planned FTE allocation | `NumberOfVacancies` only |
| `Filled FTE` | FTEs already hired | **NOT TRACKED** |
| `Remaining FTE` | FTEs still to fill | **NOT TRACKED** |
| `Hired Headcount` | People hired count | **Must calculate** |
| `Maximum Headcount` | Max people allowed | `NumberOfVacancies` |
| `Remaining Headcount` | People still to hire | **NOT TRACKED** |
| `Is Opening Budgeted?` | Budget approval flag | **NOT AVAILABLE** |

**Impact:**
- Cannot distinguish between FTE and headcount
- Cannot track partial fills (e.g., 2.5 FTE filled of 3.0)
- No budget approval tracking
- Reporting on fill rates requires calculation

**Workaround:**
- Calculate from hired application count
- Use custom fields for FTE tracking
- Build calculated measures in BI

---

## 4. PRE-CALCULATED HIRING METRICS - MUST REBUILD

**Risk: HIGH - Requires development effort**

UKG stores these metrics pre-calculated. Talentsoft does NOT store them - you must calculate from event dates:

| UKG Metric | What It Measures | Talentsoft Status |
|------------|------------------|-------------------|
| `Days Between Accept and Offer Dates` | Time from offer to acceptance | **CALCULATE** |
| `Days Between Accept and Start Dates` | Time from acceptance to start | **CALCULATE** |
| `Days Between Hire and Publish Dates` | Time-to-hire from posting | **CALCULATE** |
| `Days Between Offer and Start Dates` | Notice period / onboarding time | **CALCULATE** |
| `Days Between Start and Publish Dates` | Total time-to-fill | **CALCULATE** |

**Impact:**
- Historical metrics need recalculation
- Requires event date extraction from `SDD_APPLICATION_EVENTS`
- BI development needed for dashboards

**Required Calculation:**
```
Event dates stored in: SDD_APPLICATION_EVENTS.csv
Column: JobApplicationChildEvent_EventDate_
Event types: JobApplicationChildEvent_JobApplicationChildEventType_

Metric = EventDate(Type2) - EventDate(Type1)
```

---

## 5. LICENSES/CERTIFICATIONS - NO NATIVE FIELD

**Risk: MEDIUM - Requires custom field setup**

| UKG Field | Description | Talentsoft |
|-----------|-------------|------------|
| `License Number` | Certification ID | **Custom Field needed** |
| `License/Certification Name` | Name of license | **Custom Field needed** |
| `Months To Renewal` | Expiry tracking | **NOT AVAILABLE** |

**Impact:**
- Must configure custom fields before migration
- Renewal tracking not natively supported

---

## 6. SCREENING QUESTION DETAILS - NOT IN STANDARD EXPORTS

**Risk: MEDIUM - Different access method**

| UKG Field | Talentsoft Status |
|-----------|-------------------|
| `Answer Choice` | API only |
| `Correct Answer` | API only |
| `Disqualifying Answer` | API only |
| `Points` | API only |
| `Question Position` | API only |

**Impact:**
- Question/answer data not in SDD exports
- Requires API integration for reporting
- Historical screening scores need separate extraction

---

## 7. OTHER FIELDS AT RISK

### Opening Information
| UKG Field | Status |
|-----------|--------|
| `Impact To Staffing Plan` | Custom field |
| `Hours Per Shift` | Derived from Contract |
| `Hours Per Week` | Derived from JobTime |
| `Priority` | Custom field |
| `Continuous Opening (Evergreen)` | `RegularOffer` flag |

### Application Details
| UKG Field | Status |
|-----------|--------|
| `Request Candidate Availability` | Not available |

---

## MIGRATION CHECKLIST

### Before Migration:
- [ ] Configure custom fields for Licenses/Certifications
- [ ] Configure custom fields for FTE tracking (if needed)
- [ ] Configure custom fields for Incumbent info (if needed)
- [ ] Document event type codes for metric calculations
- [ ] Build BI calculated measures for Days-to-X metrics

### During Migration:
- [ ] Export incumbent data separately for reference
- [ ] Concatenate Title/Middle/Suffix into name fields if critical
- [ ] Map FTE values to NumberOfVacancies
- [ ] Preserve historical metrics in archive

### After Migration:
- [ ] Validate calculated metrics match historical values
- [ ] Verify custom field data populated correctly
- [ ] Update reports to use new calculation logic
- [ ] Train users on differences in FTE tracking

---

## QUICK REFERENCE: What's LOST vs What's DIFFERENT

### COMPLETELY LOST (No workaround):
1. Incumbent tracking (First/Last Name, Last Day Worked)
2. Title/Middle Name/Suffix for managers
3. Months To Renewal for licenses
4. Is Opening Budgeted flag

### LOST BUT RECOVERABLE (Custom fields):
1. License Number/Name → Custom fields
2. Priority → Custom field
3. Impact To Staffing Plan → Custom field

### DIFFERENT APPROACH NEEDED:
1. FTE tracking → Calculate from applications
2. Days-to-X metrics → Calculate from events
3. Screening details → API access

---

*Document generated: 2025-11-22*
*Source: UKG vs Talentsoft Gap Analysis*
