# GEODIS IRC Configuration Tables - Oracle EDM Mapping (Corrected)

**Document:** 18_IRC_Configuration_Tables_Oracle_EDM_Mapping.md
**Version:** 1.0
**Created:** 2025-12-07
**Module:** Oracle Recruiting Cloud (IRC)
**Purpose:** Accurate mapping of configuration workbooks to Oracle HCM EDM tables/entities
**Reference:** Oracle OEDMH Documentation (https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/)

---

## Executive Summary

This document provides the **corrected hybrid mapping** between GEODIS configuration workbooks and actual Oracle HCM EDM tables/views. Key distinctions:

- **Real IRC/HCM tables** are referenced where they exist
- **Functional entities** (lookups, content library, events) are clearly marked where no dedicated config table exists
- All Oracle object names are verified against OEDMH documentation

### Configuration Status Summary

| Category | Total | EXISTS | MISSING/Functional |
|----------|-------|--------|-------------------|
| Requisition | 8 | 3 | 5 |
| Candidate | 11 | 4 | 7 |
| Interview | 7 | 2 | 5 |
| Assessment | 4 | 0 | 4 |
| Offer | 6 | 2 | 4 |
| Job Posting | 5 | 1 | 4 |
| Communication | 4 | 0 | 4 |
| Background Check | 3 | 0 | 3 |
| Integration | 5 | 0 | 5 |
| Security & Compliance | 5 | 0 | 5 |
| Reference Data | 5 | 4 | 1 |
| **TOTAL** | **63** | **16** | **47** |

---

## 1. Requisition Configuration (8)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 1 | **Requisition Template.xlsx** | EXISTS | **IRC_REQUISITIONS_B / IRC_REQUISITIONS_VL** | Templates flagged via `REQ_USAGE_CODE` (ORA_IRC_REQUISITION_USAGE lookup) |
| 2 | **Requisition Phase.xlsx** | EXISTS | **IRC_PHASES_B / IRC_PHASES_VL** | Phases of lifecycle (used by requisitions & submissions) |
| 3 | **Requisition Reason.xlsx** | MISSING | Functional: Lookup codes on **IRC_REQUISITIONS_B** | `JUSTIFICATION_CODE`, `REQ_USAGE_CODE` → HCM lookups (ORA_IRC_REQ_JUSTIFICATION) |
| 4 | **Requisition Flexfield.xlsx** | MISSING | Functional: DFF/EFF on **IRC_REQUISITIONS_B / IRC_REQUISITIONS_VL** | ATTRIBUTE* columns and transaction model, not separate table |
| 5 | **Requisition Approval Rule.xlsx** | EXISTS | Functional: HCM/BPM approval rules | Events via **HRC_EVT_SOURCE_OBJECTS / HRC_EVT_CONSTRUCTION_METHODS** |
| 6 | **Requisition Default Value.xlsx** | MISSING | Functional: UI rules + profile options | Defaulting over **IRC_REQUISITIONS_B**, no dedicated table |
| 7 | **Hiring Team Role.xlsx** | MISSING | Functional: Relationships between tables | **IRC_REQUISITIONS_B** → **PER_PERSONS / PER_ALL_ASSIGNMENTS_M**; role types are lookup-driven |
| 8 | **Requisition Collaborator Type.xlsx** | MISSING | Functional: Lookups + security profiles | Data via **IRC_REQUISITIONS_VL / IRC_REC_SEC_PROFILES** |

### Key Requisition Tables

```
IRC_REQUISITIONS_B (Base table)
├── REQ_USAGE_CODE → Template type
├── JUSTIFICATION_CODE → Reason for opening
├── HIRING_MANAGER_ID → FK to PER_PERSONS
├── RECRUITER_ID → FK to PER_PERSONS
├── NUMBER_TO_HIRE → Headcount/FTE
├── MIN_SALARY / MAX_SALARY → Salary range
├── HOT_JOB_FLAG → Priority
├── WORKPLACE_TYPE_CODE → Remote/Onsite/Hybrid
├── INT_PUBLISH_JOB_* → Internal posting dates
├── EXT_PUBLISH_JOB_* → External posting dates
└── ATTRIBUTE1-30 → DFF segments
```

---

## 2. Candidate Configuration (11)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 9 | **Candidate Phase.xlsx** | EXISTS | **IRC_PHASES_B / IRC_PHASES_VL** | Same phase engine, candidate context via type codes |
| 10 | **Candidate State.xlsx** | EXISTS | **IRC_STATES_VL** | States + references from **IRC_SUBMISSIONS.PUBLIC_STATE_ID** |
| 11 | **Candidate Source.xlsx** | EXISTS | Functional: **IRC_SOURCE_TRACKING** | Source metadata + campaign tables; source types are lookups |
| 12 | **Candidate Pool Type.xlsx** | EXISTS | **HRT_POOLS_VL** | `POOL_TYPE_CODE` column for pool types in ORC |
| 13 | **Candidate Flexfield.xlsx** | MISSING | Functional: DFF/EFF on **IRC_CANDIDATES / IRC_SUBMISSIONS** | Attributes/transaction model, not separate EFF table |
| 14 | **Screening Question.xlsx** | MISSING | **IRC_DESCRIPTIONS_VL + IRC_DESC_VERSIONS_VL** | Question Library (prescreen/interview content) via type codes |
| 15 | **Knockout Question.xlsx** | MISSING | **IRC_DESCRIPTIONS_VL / IRC_DESC_VERSIONS_VL** | Knockout behavior is lifecycle/action config |
| 16 | **Duplicate Check Rule.xlsx** | MISSING | Functional: **IRC_CANDIDATES**, **IRC_CAND_DUP_CHECK_DETAILS**, **IRC_CAND_DUP_CHECK_SUMMARY** | Duplicate check features |
| 17 | **Candidate Merge Rule.xlsx** | MISSING | **IRC_CAND_MERGE_LOGS** + **IRC_CANDIDATES.DELETION_QUALIFIER** | Merge vs GDPR delete rules are application logic |
| 18 | **Talent Community.xlsx** | MISSING | **HRT_POOLS_VL**, **IRC_REC_EVENT_POOL_MEMBERS** | Pools & audiences + marketing tables |
| 19 | **Candidate Profile Section.xlsx** | MISSING | Functional: **IRC_CANDIDATES**, **IRC_SUBMISSIONS**, **HRT_PROFILES_VL** | Profile sections via UI, no dedicated section table |

### Key Candidate Tables

```
IRC_CANDIDATES (Candidate master)
├── PERSON_ID → FK to PER_ALL_PEOPLE_F
├── AVAILABILITY_DATE → When available to start
├── CAND_PREF_LANGUAGE_CODE → Preferred language
├── DELETION_QUALIFIER → GDPR merge/delete flag
└── ATTRIBUTE1-30 → DFF segments

IRC_SUBMISSIONS (Job applications)
├── SUBMISSION_ID → Primary key
├── REQUISITION_ID → FK to IRC_REQUISITIONS_B
├── PERSON_ID → FK to PER_ALL_PEOPLE_F
├── CURRENT_PHASE_ID → FK to IRC_PHASES_B
├── CURRENT_STATE_ID → FK to IRC_STATES_VL
├── PUBLIC_STATE_ID → Candidate-visible state
├── QSTNR_SCORE → Questionnaire score
├── SITE_NUMBER → Career site/source
├── ADDED_BY_CONTEXT_CODE → Source context
└── ADDED_BY_PERSON_ID → Referrer

IRC_SOURCE_TRACKING (Source attribution)
└── Campaign and source metadata
```

---

## 3. Interview Configuration (7)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 20 | **Interview Type.xlsx** | EXISTS | Functional: **IRC_SUBMISSIONS** + calendar integration | "Type" driven by lookups, no IRC_INTERVIEW_TYPES table |
| 21 | **Interview Guide.xlsx** | EXISTS | **IRC_DESCRIPTIONS_VL / IRC_DESC_VERSIONS_VL** | Content items (category = Interview Guide) |
| 22 | **Questionnaire.xlsx** | MISSING | **IRC_DESCRIPTIONS_VL / IRC_DESC_VERSIONS_VL** | Content library with specific description types |
| 23 | **Scorecard Template.xlsx** | MISSING | **HRT_CUSTOM_RATING_ITEMS_V** + profile content | Rating questions/sections; no separate IRC scorecard table |
| 24 | **Interview Slot Configuration.xlsx** | MISSING | Functional: **IRC_CX_JOBS_QUEUE** + scheduling tables | Slot rules in scheduling logic, not single config table |
| 25 | **Interview Feedback Question.xlsx** | MISSING | **IRC_DESCRIPTIONS_VL** | Type = feedback question, mapped to scorecards |
| 26 | **Interview Reminder Rule.xlsx** | MISSING | Functional: **IRC_JA_NOTIF_PROCESS** + Alert Composer | Notification process, not standalone config table |

### Key Interview/Content Tables

```
IRC_DESCRIPTIONS_VL (Content Library - CENTRAL)
├── DESCRIPTION_ID → Primary key
├── DESCRIPTION_TYPE → Interview Guide / Questionnaire / Email Template / etc.
├── CONTENT_TYPE_CODE → Content format
└── Used for: Questions, Guides, Templates, JD Sections

IRC_DESC_VERSIONS_VL (Content versions)
├── VERSION_ID → Primary key
├── DESCRIPTION_ID → FK to IRC_DESCRIPTIONS_VL
└── Active/inactive versioning

IRC_JA_NOTIF_PROCESS (Job Application Notifications)
├── Notification rules
├── Reminder scheduling
└── Event-triggered communications
```

---

## 4. Assessment Configuration (4)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 27 | **Assessment Type.xlsx** | MISSING | **IRC_ASMT_REQ_PACKAGES** | Assessment packages on requisitions |
| 28 | **Assessment Provider.xlsx** | MISSING | Functional: **IRC_LC_EVENTMSG** | Partner metadata via lifecycle/event tables |
| 29 | **Assessment Scoring Rule.xlsx** | MISSING | Functional: Application logic | Scoring rules interpreted when reading results |
| 30 | **Assessment Threshold.xlsx** | MISSING | Functional: Scoring model | Thresholds based on scores, no dedicated table |

### Key Assessment Tables

```
IRC_ASMT_REQ_PACKAGES (Assessment packages per requisition)
├── REQUISITION_ID → FK to IRC_REQUISITIONS_B
├── Package configuration
└── Assessment type/provider linkage

IRC_LC_EVENTMSG (Lifecycle events)
├── Assessment events
├── Partner integration events
└── Status change messages
```

---

## 5. Offer Configuration (6)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 31 | **Offer Letter Template.xlsx** | EXISTS | **IRC_DESCRIPTIONS_VL / IRC_DESC_VERSIONS_VL** | HTML/RTF content linked to **IRC_OFFERS** |
| 32 | **Offer Approval Rule.xlsx** | EXISTS | Functional: HCM approvals/BPM on **IRC_OFFERS** | Events via **HRC_EVT_SOURCE_OBJECTS** |
| 33 | **Offer Compensation Component.xlsx** | MISSING | **IRC_OFFERS** + **PER_ALL_ASSIGNMENTS_M** + CMP tables | Component model in assignment/comp tables |
| 34 | **Offer Expiry Rule.xlsx** | MISSING | Functional: Attributes on **IRC_OFFERS** | Expiry dates/flags stored, rules in app logic |
| 35 | **Counter Offer Rule.xlsx** | MISSING | Functional: Offer state machine | **IRC_OFFERS** + **PER_ACTIONS_B / PER_ACTION_REASONS_B** |
| 36 | **Offer Condition.xlsx** | MISSING | **IRC_BC_CAND_RESULTS** + **IRC_OFFERS** fields | Conditions tracked indirectly, no conditions table |

### Key Offer Tables

```
IRC_OFFERS (Offer master)
├── OFFER_ID → Primary key
├── SUBMISSION_ID → FK to IRC_SUBMISSIONS
├── PERSON_ID → FK to PER_ALL_PEOPLE_F
├── HIRING_MANAGER_ID → FK to PER_PERSONS
├── RECRUITER_ID → FK to PER_PERSONS
├── OBJECT_STATUS → Offer status
├── EXPIRATION_DATE → Offer expiry
├── DRAFTED_DATE / APPROVED_DATE / EXTENDED_DATE / ACCEPTED_DATE
├── OFFER_COMMENTS → Notes
├── ADDITIONALTEXT1 / ADDITIONALTEXT2 → Custom text
├── REDRAFT_COUNT → Counter offer tracking
└── ATTRIBUTE_CHAR1-90 → DFF segments (90 char columns!)
```

---

## 6. Job Posting Configuration (5)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 37 | **Posting Channel.xlsx** | EXISTS | **IRC_CX_SITES_VL**, **IRC_CX_JOBS_QUEUE** | CX site config + posting changes |
| 38 | **Job Description Section.xlsx** | MISSING | **IRC_DESCRIPTIONS_VL / IRC_DESC_VERSIONS_VL** | Description type = JD_SECTION |
| 39 | **Job Posting Template.xlsx** | MISSING | **IRC_DESCRIPTIONS_VL** linked to **IRC_REQUISITIONS_VL** | Content items for postings |
| 40 | **Posting Duration Rule.xlsx** | MISSING | Functional: **IRC_REQUISITIONS_B** columns | `INT_PUBLISH_JOB_*`, `EXT_PUBLISH_JOB_*` dates |
| 41 | **Internal Posting Rule.xlsx** | MISSING | Functional: **IRC_REQUISITIONS_B** + security profiles | Internal publish flags |

### Key Posting Tables

```
IRC_CX_SITES_VL (Career Experience Sites)
├── SITE_ID → Primary key
├── Site configuration
├── Branding settings
└── Job board distribution config

IRC_CX_JOBS_QUEUE (Job posting queue)
├── Posting changes/updates
├── Distribution tracking
└── Sync status
```

---

## 7. Communication Configuration (4)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 42 | **Email Template.xlsx** | MISSING | **IRC_DESCRIPTIONS_VL / IRC_DESC_VERSIONS_VL** | Content Library; orchestration via **IRC_JA_NOTIF_PROCESS** |
| 43 | **SMS Template.xlsx** | MISSING | Same content model as email | Delivery via SMS integration |
| 44 | **Correspondence Rule.xlsx** | MISSING | Functional: **IRC_JA_NOTIF_PROCESS** + **HRC_EVT_SOURCE_OBJECTS** | Notification rules tied to templates |
| 45 | **Notification Preference.xlsx** | MISSING | **IRC_CANDIDATES** + **IRC_CAND_OPTIN_HISTORY** | GDPR marketing/job-alert consent |

### Key Communication Tables

```
IRC_JA_NOTIF_PROCESS (Notification orchestration)
├── Notification rules
├── Template linkage
├── Trigger events
└── Recipient configuration

IRC_CAND_OPTIN_HISTORY (Consent tracking)
├── CANDIDATE_ID → FK to IRC_CANDIDATES
├── Opt-in/opt-out history
├── Marketing consent
└── Job alert preferences
```

---

## 8. Background Check Configuration (3)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 46 | **Background Check Provider.xlsx** | MISSING | **IRC_BC_ACTIVATION_CONFIG** | Partner activation for background check |
| 47 | **Background Check Type.xlsx** | MISSING | **IRC_BC_CAND_SCREENINGS** | Screening types per package |
| 48 | **Background Check Package.xlsx** | MISSING | **IRC_BC_ACTIVATION_CONFIG** + **IRC_BC_CAND_RESULTS**, **IRC_BC_CAND_SCREENINGS** | Package config & usage |

### Key Background Check Tables

```
IRC_BC_ACTIVATION_CONFIG (Provider activation)
├── Provider configuration
├── Package definitions
└── Integration settings

IRC_BC_CAND_SCREENINGS (Candidate screenings)
├── Screening types ordered
├── Status tracking
└── Package linkage

IRC_BC_CAND_RESULTS (Screening results)
├── Result data from provider
├── Pass/fail status
├── Adjudication tracking
└── Condition satisfaction
```

---

## 9. Integration Configuration (5)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 49 | **Job Board Connection.xlsx** | MISSING | **IRC_CX_SITES_VL**, **IRC_CX_JOBS_QUEUE** | CX site & integration settings |
| 50 | **External System Mapping.xlsx** | MISSING | **HRC_CUSTOM_OBJECTS** + **HRC_TXN_DENORM** | Custom object/event mappings |
| 51 | **E-Signature Provider.xlsx** | MISSING | Functional: **HRC_EVT_SOURCE_OBJECTS / HRC_EVT_CONSTRUCTION_METHODS** | E-sign via HCM events |
| 52 | **Calendar Integration.xlsx** | MISSING | Functional: **HRC_EVT_SOURCE_OBJECTS** | External calendar via source objects/events |
| 53 | **Webhook Configuration.xlsx** | MISSING | **HRC_EVT_SOURCE_OBJECTS**, **HRC_EVT_CONSTRUCTION_METHODS** | Source object + delivery method (REST) |

### Key Integration Tables

```
HRC_EVT_SOURCE_OBJECTS (Event sources - CENTRAL for integrations)
├── SOURCE_OBJECT_ID → Primary key
├── Event definitions
├── Integration endpoints
└── Webhook configurations

HRC_EVT_CONSTRUCTION_METHODS (Delivery methods)
├── REST/SOAP endpoints
├── Payload construction
└── Authentication config

HRC_CUSTOM_OBJECTS (Custom integrations)
├── Custom object definitions
├── Field mappings
└── Transaction handling
```

---

## 10. Security & Compliance Configuration (5)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 54 | **Security Role.xlsx** | MISSING | **PER_ROLES_DN / FND_SESSION_ROLES** + **IRC_REC_SEC_PROFILES** | Roles at runtime + recruiting security profiles |
| 55 | **Data Access Rule.xlsx** | MISSING | Functional: **PER_SECURITY_PROFILES** | HCM data roles and security profiles |
| 56 | **Consent Template.xlsx** | MISSING | **IRC_CAND_OPTIN_HISTORY** + **IRC_CANDIDATES** | GDPR consent text & flags |
| 57 | **Retention Policy.xlsx** | MISSING | **FAI_IM_DELETE_ENTITY** + **IRC_CANDIDATES** deletion fields | GDPR deletion workflow |
| 58 | **Audit Configuration.xlsx** | MISSING | Generic: **FND_AUDIT*** tables | HCM-wide audit, not IRC-specific |

### Key Security Tables

```
IRC_REC_SEC_PROFILES (Recruiting security)
├── Security profile definitions
├── Data access rules
└── Requisition/candidate visibility

IRC_CAND_OPTIN_HISTORY (GDPR consent)
├── Consent history
├── Marketing preferences
└── Job alert settings

FAI_IM_DELETE_ENTITY (GDPR deletion)
├── Deletion tracking
├── Candidate/person deletions
└── Compliance audit trail
```

---

## 11. Reference Data Configuration (5)

| # | Configuration Workbook | Status | Oracle Table / Entity (EDM) | Notes |
|---|------------------------|--------|----------------------------|-------|
| 59 | **Rejection Reason.xlsx** | EXISTS | Lookups → **IRC_STATES_VL / IRC_SUBMISSIONS** + **IRC_LC_ACTIONS_VL / IRC_LC_ACTION_USAGES_VL** | State transitions & action usage |
| 60 | **Withdrawal Reason.xlsx** | EXISTS | Lookups → **IRC_SUBMISSIONS** + action history | Lifecycle actions |
| 61 | **Recruiting Action.xlsx** | EXISTS | **IRC_LC_ACTIONS_VL** + **IRC_LC_ACTION_USAGES_VL** | Lifecycle actions and usages |
| 62 | **Document Type.xlsx** | MISSING | **HR_DOCUMENT_TYPES_B / HR_DOCUMENT_TYPES_TL** | Documents of Record, referenced by checklists |
| 63 | **Status Reason Code.xlsx** | MISSING | Functional: Lookups on **IRC_SUBMISSIONS** + **IRC_REQUISITIONS_B** | Status + justification codes |

### Key Lifecycle/Action Tables

```
IRC_LC_ACTIONS_VL (Lifecycle actions)
├── ACTION_ID → Primary key
├── Action definitions
├── Available transitions
└── Required/optional data

IRC_LC_ACTION_USAGES_VL (Action usages)
├── Where actions can be used
├── Phase/state combinations
└── Role permissions

IRC_PHASES_B / IRC_PHASES_VL (Phases)
├── PHASE_ID → Primary key
├── Phase sequence
├── Phase type (requisition/candidate)
└── Active/inactive status

IRC_STATES_VL (States within phases)
├── STATE_ID → Primary key
├── PHASE_ID → FK to IRC_PHASES_B
├── State sequence
├── Terminal flag
└── Public visibility
```

---

## Central Content Library Pattern

Many configurations in Oracle Recruiting use a **centralized content library** pattern:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    IRC CONTENT LIBRARY ARCHITECTURE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  IRC_DESCRIPTIONS_VL (Master content table)                                 │
│  ═══════════════════════════════════════════                                │
│  │                                                                          │
│  ├── DESCRIPTION_TYPE = 'INTERVIEW_GUIDE'  → Interview Guides              │
│  ├── DESCRIPTION_TYPE = 'QUESTIONNAIRE'    → Questionnaires                │
│  ├── DESCRIPTION_TYPE = 'SCREENING_Q'      → Screening Questions           │
│  ├── DESCRIPTION_TYPE = 'FEEDBACK_Q'       → Feedback Questions            │
│  ├── DESCRIPTION_TYPE = 'EMAIL_TEMPLATE'   → Email Templates               │
│  ├── DESCRIPTION_TYPE = 'OFFER_LETTER'     → Offer Letter Templates        │
│  ├── DESCRIPTION_TYPE = 'JD_SECTION'       → Job Description Sections      │
│  ├── DESCRIPTION_TYPE = 'JOB_POSTING'      → Job Posting Templates         │
│  └── DESCRIPTION_TYPE = 'SMS_TEMPLATE'     → SMS Templates                 │
│                                                                             │
│  IRC_DESC_VERSIONS_VL (Version control)                                     │
│  ═══════════════════════════════════════                                    │
│  ├── Links to DESCRIPTION_ID                                               │
│  ├── Version numbering                                                      │
│  ├── Active/inactive flag                                                  │
│  └── Effective dates                                                        │
│                                                                             │
│  IMPLICATION: Many "missing" config workbooks should be loaded              │
│  as content items with appropriate DESCRIPTION_TYPE codes                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Event Framework Pattern

Integrations and notifications use the **HCM Event Framework**:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      HCM EVENT FRAMEWORK                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  HRC_EVT_SOURCE_OBJECTS                                                     │
│  ═══════════════════════                                                    │
│  │ Defines what triggers events:                                            │
│  ├── IRC_REQUISITIONS (Requisition events)                                 │
│  ├── IRC_SUBMISSIONS (Application events)                                  │
│  ├── IRC_OFFERS (Offer events)                                             │
│  └── IRC_CANDIDATES (Candidate events)                                     │
│                                                                             │
│  HRC_EVT_CONSTRUCTION_METHODS                                               │
│  ═════════════════════════════                                              │
│  │ Defines how events are delivered:                                        │
│  ├── REST webhook                                                          │
│  ├── SOAP service call                                                     │
│  ├── Email notification                                                    │
│  └── Internal process trigger                                              │
│                                                                             │
│  USED FOR:                                                                  │
│  ├── Approval workflows                                                    │
│  ├── E-signature integration (DocuSign)                                    │
│  ├── Calendar integration (O365/Google)                                    │
│  ├── Job board webhooks                                                    │
│  ├── Background check triggers                                             │
│  └── Custom integrations                                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Implementation Guidance

### For "EXISTS" Items (16 workbooks)

These map to dedicated IRC tables - use standard HDL/HSDL import:

1. **IRC_REQUISITIONS_B** - Requisition templates via REQ_USAGE_CODE
2. **IRC_PHASES_B** - Requisition and candidate phases
3. **IRC_STATES_VL** - Candidate states
4. **IRC_SOURCE_TRACKING** - Source tracking (functional)
5. **HRT_POOLS_VL** - Pool types
6. **IRC_DESCRIPTIONS_VL** - Interview guides, offer templates
7. **IRC_CX_SITES_VL** - Posting channels
8. **IRC_LC_ACTIONS_VL** - Recruiting actions
9. Lookups for rejection/withdrawal reasons

### For "MISSING/Functional" Items (47 workbooks)

Use these patterns:

| Pattern | Configuration Items | Oracle Approach |
|---------|--------------------|-----------------|
| **Content Library** | Questions, Templates, Guides | Load to IRC_DESCRIPTIONS_VL with DESCRIPTION_TYPE |
| **Lookups** | Reasons, Types, Codes | Configure HCM Lookups (ORA_IRC_*) |
| **DFF/EFF** | Flexfields | Configure via Setup and Maintenance |
| **Event Framework** | Integrations, Webhooks | Configure HRC_EVT_SOURCE_OBJECTS |
| **BPM Approvals** | Approval rules | Configure via Approval Management |
| **Security Profiles** | Data access, Roles | Configure IRC_REC_SEC_PROFILES |

---

## Quick Reference: Key IRC Tables

| Table | Purpose | Key Columns |
|-------|---------|-------------|
| IRC_REQUISITIONS_B | Requisitions & templates | REQ_USAGE_CODE, JUSTIFICATION_CODE, NUMBER_TO_HIRE |
| IRC_PHASES_B | Lifecycle phases | PHASE_TYPE_CODE, SEQUENCE |
| IRC_STATES_VL | States within phases | PHASE_ID, SEQUENCE, TERMINAL_FLAG |
| IRC_CANDIDATES | Candidate master | PERSON_ID, AVAILABILITY_DATE |
| IRC_SUBMISSIONS | Job applications | REQUISITION_ID, CURRENT_PHASE_ID, CURRENT_STATE_ID |
| IRC_OFFERS | Offers | SUBMISSION_ID, OBJECT_STATUS, EXPIRATION_DATE |
| IRC_DESCRIPTIONS_VL | Content library | DESCRIPTION_TYPE (multi-purpose) |
| IRC_SOURCE_TRACKING | Source attribution | Campaign and source data |
| IRC_CX_SITES_VL | Career sites | Site config, job board integration |
| IRC_LC_ACTIONS_VL | Lifecycle actions | Available actions per phase/state |
| IRC_JA_NOTIF_PROCESS | Notifications | Rules, templates, triggers |
| IRC_BC_ACTIVATION_CONFIG | Background checks | Provider configuration |
| HRC_EVT_SOURCE_OBJECTS | Events/integrations | Webhooks, triggers |
| HRT_POOLS_VL | Talent pools | POOL_TYPE_CODE |

---

## Document Information

| Attribute | Value |
|-----------|-------|
| Document ID | 18_IRC_Configuration_Tables_Oracle_EDM_Mapping |
| Version | 1.0 |
| Created | 2025-12-07 |
| Total Configuration Items | 63 |
| EXISTS (Dedicated Tables) | 16 |
| MISSING/Functional | 47 |
| Reference | Oracle OEDMH Documentation |

---

## References

- [Oracle HCM Tables and Views](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/)
- [IRC_REQUISITIONS_B](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircrequisitionsb-10407.html)
- [IRC_PHASES_B](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircphasesb-6699.html)
- [IRC_STATES_VL](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircstatesvl-8901.html)
- [IRC_CANDIDATES](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/irccandidates-27722.html)
- [IRC_SUBMISSIONS](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircsubmissions-29233.html)
- [IRC_OFFERS](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircoffers-13977.html)
- [IRC_DESCRIPTIONS_VL](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircdescriptionsvl-4399.html)
- [IRC_SOURCE_TRACKING](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircsourcetracking-4317.html)
- [HRT_POOLS_VL](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/hrtpoolsvl-5329.html)
- [IRC_LC_ACTIONS_VL](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/)
- [IRC_JA_NOTIF_PROCESS](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircjanotifprocess-26556.html)
- [IRC_BC_ACTIVATION_CONFIG](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/ircbcactivationconfig-12549.html)
- [HRC_EVT_SOURCE_OBJECTS](https://docs.oracle.com/en/cloud/saas/human-resources/oedmh/hrcevtsourceobjects-27519.html)

---

*End of Document*
