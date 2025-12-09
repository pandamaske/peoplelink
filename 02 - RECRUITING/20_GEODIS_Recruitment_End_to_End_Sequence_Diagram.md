# GEODIS Recruitment Process - End-to-End Sequence Diagram

**Document:** 20_GEODIS_Recruitment_End_to_End_Sequence_Diagram.md
**Version:** 1.0
**Created:** 2025-12-08
**Module:** Oracle Recruiting Cloud (IRC)
**Project:** GEODIS HCM Transformation

---

## Table of Contents

1. [Master End-to-End Sequence Diagram](#1-master-end-to-end-sequence-diagram)
2. [Phase 1: Requisition Creation & Approval](#2-phase-1-requisition-creation--approval)
3. [Phase 2: Job Posting & Sourcing](#3-phase-2-job-posting--sourcing)
4. [Phase 3: Application & Screening](#4-phase-3-application--screening)
5. [Phase 4: Interview & Assessment](#5-phase-4-interview--assessment)
6. [Phase 5: Selection & Decision](#6-phase-5-selection--decision)
7. [Phase 6: Offer Management](#7-phase-6-offer-management)
8. [Phase 7: Background Check & Compliance](#8-phase-7-background-check--compliance)
9. [Phase 8: Hire & Onboarding Handoff](#9-phase-8-hire--onboarding-handoff)
10. [Complete Integrated Sequence](#10-complete-integrated-sequence)

---

## 1. Master End-to-End Sequence Diagram

### 1.1 Complete Recruitment Lifecycle Overview

```mermaid
sequenceDiagram
    autonumber

    participant HM as Hiring Manager
    participant REC as Recruiter
    participant HR as HR Business Partner
    participant ORC as Oracle Recruiting
    participant JB as Job Boards<br/>(Indeed/LinkedIn)
    participant CAND as Candidate
    participant INT as Interviewer(s)
    participant COMP as Compensation
    participant DOCU as DocuSign
    participant STER as Sterling<br/>(Background)
    participant CORE as Oracle Core HR

    rect rgb(227, 242, 253)
    Note over HM,CORE: PHASE 1: REQUISITION CREATION & APPROVAL
    HM->>ORC: Create Requisition (Select Template)
    HM->>ORC: Define Job Details, Requirements, Compensation Range
    HM->>ORC: Assign Hiring Team (Recruiter, HRBP)
    HM->>ORC: Submit for Approval
    ORC->>HR: Route to N+1 Manager for Approval
    HR-->>ORC: Approve/Reject
    alt Salary >= EUR 125K
        ORC->>HR: Route to HRBP
        HR-->>ORC: Approve
        alt Salary >= EUR 155K or TOPEX
            ORC->>HR: Route to EVP HR / CHRO
            HR-->>ORC: Final Approval
        end
    end
    ORC->>REC: Notify: Requisition Approved & Activated
    end

    rect rgb(243, 229, 245)
    Note over HM,CORE: PHASE 2: JOB POSTING & SOURCING (7-Day Internal Rule)
    REC->>ORC: Post Job Internally (Employee Portal)
    ORC->>ORC: Start 7-Day Internal Timer
    ORC-->>CAND: Internal Job Alert Emails

    Note over ORC: After 7 Days (or with Exception)
    REC->>ORC: Activate External Posting
    ORC->>JB: Publish to Career Site, Indeed, LinkedIn
    JB-->>CAND: Job Visible on External Sites
    end

    rect rgb(232, 245, 233)
    Note over HM,CORE: PHASE 3: APPLICATION & SCREENING
    CAND->>JB: View Job Posting
    CAND->>ORC: Submit Application (Resume, Questions)
    ORC->>ORC: Auto-Screen (Minimum Qualifications)
    alt Fails Auto-Screen
        ORC-->>CAND: Rejection Email (Auto)
    else Passes Auto-Screen
        ORC->>REC: New Application in Queue
        REC->>ORC: Review Application
        REC->>ORC: Calculate Score & Rank
        alt Qualified
            REC->>ORC: Move to Screening Phase
            REC->>CAND: Schedule Phone Screen
            CAND-->>REC: Confirm Time Slot
            REC->>CAND: Conduct Phone Screen
            REC->>ORC: Log Screening Notes & Decision
        else Not Qualified
            REC->>ORC: Reject with Reason
            ORC-->>CAND: Rejection Email
        end
    end
    end

    rect rgb(255, 243, 224)
    Note over HM,CORE: PHASE 4: INTERVIEW & ASSESSMENT
    REC->>ORC: Move Candidate to Interview Phase
    REC->>INT: Request Interview Availability
    INT-->>REC: Provide Available Slots
    REC->>CAND: Send Interview Invitation
    CAND-->>REC: Confirm Interview
    ORC->>INT: Calendar Invite + Candidate Profile
    ORC->>CAND: Interview Confirmation + Details

    Note over INT,CAND: Interview Day
    INT->>CAND: Conduct Interview
    INT->>ORC: Submit Interview Feedback (Scorecard)
    ORC->>HM: Notify: Feedback Received

    alt Multiple Interview Rounds
        REC->>CAND: Schedule Additional Interviews
        INT->>CAND: Conduct Panel/Technical Interview
        INT->>ORC: Submit All Feedback
    end
    end

    rect rgb(252, 228, 236)
    Note over HM,CORE: PHASE 5: SELECTION & DECISION
    REC->>ORC: Compile All Interview Feedback
    REC->>HM: Schedule Debrief Meeting
    HM->>INT: Debrief Discussion
    HM->>ORC: Record Final Decision
    alt Candidate Selected
        HM->>ORC: Approve Candidate for Offer
        ORC->>REC: Notify: Ready for Offer
    else Candidate Not Selected
        HM->>ORC: Reject Candidate
        ORC-->>CAND: Rejection Email
        REC->>ORC: Add to Talent Pool (Silver Medalist)?
    end
    end

    rect rgb(255, 248, 225)
    Note over HM,CORE: PHASE 6: OFFER MANAGEMENT
    REC->>ORC: Create Offer (Select Template by Country)
    REC->>COMP: Request Compensation Validation
    COMP-->>REC: Validate Salary within Range
    alt Salary Exception Required
        COMP->>HR: Exception Approval Request
        HR-->>COMP: Approve/Deny Exception
    end
    REC->>ORC: Submit Offer for Approval
    ORC->>HM: Route for Manager Approval
    HM-->>ORC: Approve Offer
    alt High Value Offer (>= EUR 125K)
        ORC->>HR: Route to HRBP/EVP HR
        HR-->>ORC: Final Approval
    end

    ORC->>DOCU: Generate Offer Letter (E-Signature)
    DOCU-->>CAND: Email: Offer Letter for Signature
    CAND->>DOCU: Review & Sign Offer
    DOCU-->>ORC: Signed Offer Returned
    ORC->>REC: Notify: Offer Accepted
    ORC->>HM: Notify: Offer Accepted
    end

    rect rgb(224, 242, 241)
    Note over HM,CORE: PHASE 7: BACKGROUND CHECK & COMPLIANCE
    ORC->>STER: Initiate Background Check Request
    STER-->>CAND: Email: Consent & Information Request
    CAND->>STER: Provide Consent & Details
    STER->>STER: Run Background Checks
    Note over STER: Criminal, Employment, Education, References
    STER-->>ORC: Background Check Results
    alt All Clear
        ORC->>HR: Notify: Background Cleared
    else Issues Found
        ORC->>HR: Flag for Review
        HR->>HR: Assess Risk
        alt Proceed with Conditions
            HR->>ORC: Clear with Notes
        else Rescind Offer
            HR->>ORC: Rescind Offer
            ORC-->>CAND: Offer Rescinded Notification
        end
    end
    end

    rect rgb(225, 245, 254)
    Note over HM,CORE: PHASE 8: HIRE & ONBOARDING HANDOFF
    HR->>CAND: Request Pre-Hire Documents
    CAND-->>HR: Submit Documents (ID, Tax Forms, etc.)
    HR->>ORC: Verify Documents Complete
    HR->>ORC: Confirm Start Date

    ORC->>CORE: Create Worker Record (Pending Worker)
    CORE->>CORE: Generate Employee ID
    CORE->>CORE: Trigger System Integrations
    Note over CORE: Payroll, Benefits, IT Provisioning

    ORC->>REC: Update Requisition Status: Filled
    REC->>ORC: Close Requisition

    CORE-->>CAND: Welcome Email + Portal Access
    CORE-->>HM: Notify: New Hire Ready
    HM->>CAND: Welcome & Onboarding Schedule

    Note over HM,CORE: RECRUITMENT PROCESS COMPLETE
    end
```

---

## 2. Phase 1: Requisition Creation & Approval

### Detailed Requisition Workflow

```mermaid
sequenceDiagram
    autonumber

    participant HM as Hiring Manager
    participant ORC as Oracle Recruiting
    participant MGR as N+1 Manager
    participant HRBP as HR Business Partner
    participant EVP as EVP HR
    participant CHRO as CHRO
    participant REC as Recruiter

    Note over HM,REC: REQUISITION CREATION

    HM->>ORC: Login to Oracle Recruiting
    HM->>ORC: Click "Create Requisition"
    ORC-->>HM: Display Template Selection

    alt Standard Position
        HM->>ORC: Select GEODIS_STD Template
    else Executive Position
        HM->>ORC: Select GEODIS_EXEC Template
    else France Position
        HM->>ORC: Select GEODIS_FR Template
    else US Position
        HM->>ORC: Select GEODIS_US Template
    else Intern Position
        HM->>ORC: Select GEODIS_INTERN Template
    end

    ORC-->>HM: Pre-populate from Job Code

    HM->>ORC: Enter Job Details
    Note right of HM: Job Title, Department<br/>Location, Grade/Level

    HM->>ORC: Define Compensation Range
    Note right of HM: Min/Max Salary, Currency<br/>Pay Transparency Flag

    HM->>ORC: Set Requirements
    Note right of HM: Skills, Experience<br/>Education, Certifications

    HM->>ORC: Assign Hiring Team
    Note right of HM: Recruiter, HRBP<br/>Interview Panel

    HM->>ORC: Add Screening Questions
    HM->>ORC: Set Reason for Opening
    Note right of HM: Replacement, Growth<br/>New Position

    HM->>ORC: Submit for Approval
    ORC->>ORC: Validate Required Fields
    ORC->>ORC: Determine Approval Path

    Note over HM,REC: APPROVAL WORKFLOW

    ORC->>MGR: Route to N+1 Manager
    ORC-->>MGR: Email: Requisition Pending Approval

    alt Manager Approves
        MGR->>ORC: Approve Requisition

        ORC->>ORC: Check Salary Level

        alt Salary < EUR 125K (Standard)
            ORC->>HRBP: Route to HRBP
            HRBP->>ORC: Final Approval
            ORC->>ORC: Status: APPROVED

        else Salary EUR 125K-155K (Senior)
            ORC->>HRBP: Route to HRBP
            HRBP->>ORC: Approve
            ORC->>ORC: Status: APPROVED

        else Salary >= EUR 155K or TOPEX (Executive)
            ORC->>HRBP: Route to HRBP
            HRBP->>ORC: Approve
            ORC->>EVP: Route to EVP HR
            EVP->>ORC: Approve
            alt TOPEX Position
                ORC->>CHRO: Route to CHRO
                CHRO->>ORC: Final Approval
            end
            ORC->>ORC: Status: APPROVED
        end

    else Manager Rejects
        MGR->>ORC: Reject with Comments
        ORC-->>HM: Notify: Requisition Rejected
        HM->>ORC: Revise and Resubmit
    else Manager Requests Info
        MGR->>ORC: Request More Information
        ORC-->>HM: Notify: Info Requested
        HM->>ORC: Provide Additional Info
        ORC->>MGR: Re-route for Approval
    end

    Note over HM,REC: REQUISITION ACTIVATED

    ORC->>ORC: Auto-Activate Requisition
    ORC->>ORC: Status: OPEN
    ORC-->>REC: Notify: Requisition Ready for Posting
    ORC-->>HM: Notify: Requisition Approved
```

---

## 3. Phase 2: Job Posting & Sourcing

### Job Posting Workflow with 7-Day Internal Rule

```mermaid
sequenceDiagram
    autonumber

    participant REC as Recruiter
    participant ORC as Oracle Recruiting
    participant PORTAL as Internal Portal<br/>(InJob)
    participant CAREER as Career Site<br/>(geodis.com)
    participant INDEED as Indeed API
    participant LINKEDIN as LinkedIn API
    participant EMP as Internal Employees
    participant CAND as External Candidates

    Note over REC,CAND: INTERNAL POSTING (Days 1-7)

    REC->>ORC: Open Approved Requisition
    REC->>ORC: Review Job Description
    REC->>ORC: Optimize for Search Keywords
    REC->>ORC: Click "Post Job"

    ORC-->>REC: Select Posting Channels
    REC->>ORC: Select Internal Portal Only
    REC->>ORC: Confirm Internal Posting

    ORC->>PORTAL: Publish to Internal Portal
    PORTAL-->>ORC: Posting Live (Internal)
    ORC->>ORC: Start 7-Day Timer

    PORTAL-->>EMP: Job Alert Email (Subscribed Employees)
    EMP->>PORTAL: View Internal Posting

    loop During 7-Day Internal Period
        EMP->>ORC: Submit Internal Application
        ORC->>ORC: Flag as Internal Candidate (Yellow Tag)
        ORC-->>REC: Notify: New Internal Application
        REC->>ORC: Review Internal Candidate
    end

    Note over REC,CAND: INTERNAL REVIEW CHECKPOINT

    alt Strong Internal Candidate Found
        REC->>ORC: Proceed with Internal Candidate
        Note over REC,ORC: Skip External Posting
    else No Suitable Internal Candidate
        ORC->>ORC: 7-Day Timer Complete
        ORC-->>REC: Notify: External Posting Enabled
    else Urgent Hiring Exception
        REC->>ORC: Request Exception (with Justification)
        ORC->>ORC: HRBP Approval for Exception
        ORC-->>REC: Exception Approved - Post Externally
    end

    Note over REC,CAND: EXTERNAL POSTING (Day 8+)

    REC->>ORC: Activate External Posting
    ORC-->>REC: Select External Channels

    par Post to All Channels
        ORC->>CAREER: Publish to Career Site
        CAREER-->>ORC: Posting Live (geodis.com)
    and
        ORC->>INDEED: POST /jobs (XML Feed)
        INDEED-->>ORC: Job ID Confirmed
    and
        ORC->>LINKEDIN: POST /jobs (API)
        LINKEDIN-->>ORC: Job URN Returned
    end

    Note over REC,CAND: APPLICATION FLOW

    CAND->>CAREER: View on Career Site
    CAND->>INDEED: View on Indeed
    CAND->>LINKEDIN: View on LinkedIn

    CAND->>ORC: Submit Application
    Note right of CAND: Resume, Cover Letter<br/>Screening Questions

    loop Application Sync (Every 15 min)
        INDEED-->>ORC: New Applications (Webhook)
        LINKEDIN-->>ORC: New Applications (API)
        ORC->>ORC: Create Candidate Records
        ORC->>ORC: Set Source Attribution
    end

    ORC-->>REC: New Applications in Queue

    Note over REC,CAND: POSTING MANAGEMENT

    alt Requisition Filled
        REC->>ORC: Fill Requisition
        ORC->>CAREER: Remove Posting
        ORC->>INDEED: DELETE /jobs/{id}
        ORC->>LINKEDIN: DELETE /jobs/{urn}
    else Requisition On Hold
        REC->>ORC: Put Requisition On Hold
        ORC->>ORC: Pause All Postings
    end
```

---

## 4. Phase 3: Application & Screening

### Candidate Screening Workflow

```mermaid
sequenceDiagram
    autonumber

    participant CAND as Candidate
    participant ORC as Oracle Recruiting
    participant REC as Recruiter
    participant HM as Hiring Manager

    Note over CAND,HM: APPLICATION SUBMISSION

    CAND->>ORC: Access Job Posting
    CAND->>ORC: Click "Apply"
    ORC-->>CAND: Display Application Form

    CAND->>ORC: Upload Resume/CV
    ORC->>ORC: Parse Resume (AI)
    ORC-->>CAND: Pre-fill Profile from Resume

    CAND->>ORC: Complete Profile
    Note right of CAND: Contact Info, Experience<br/>Education, Skills

    CAND->>ORC: Answer Screening Questions
    Note right of CAND: Disqualifying Questions<br/>Scored Questions

    CAND->>ORC: Submit Application
    ORC-->>CAND: Application Confirmation Email

    Note over CAND,HM: AUTO-SCREENING

    ORC->>ORC: Run Auto-Screening Rules

    ORC->>ORC: Check Minimum Qualifications
    alt Fails Minimum Requirements
        ORC->>ORC: Status: Auto-Rejected
        ORC-->>CAND: Rejection Email (Automated)
        Note over ORC: Process Ends
    end

    ORC->>ORC: Check Right to Work
    alt No Right to Work
        ORC->>ORC: Status: Auto-Rejected
        ORC-->>CAND: Rejection Email (Automated)
    end

    ORC->>ORC: Check Location Requirements
    ORC->>ORC: Calculate Screening Score
    ORC->>ORC: Rank Against Other Candidates

    ORC->>ORC: Check for Duplicate Candidate
    alt Duplicate Found
        ORC->>ORC: Merge with Existing Record
        ORC->>ORC: Link to New Requisition
    end

    ORC->>ORC: Status: NEW - Pending Review
    ORC-->>REC: Notify: New Application

    Note over CAND,HM: RECRUITER SCREENING

    REC->>ORC: Access Application Queue
    REC->>ORC: Filter by Score/Date/Source
    REC->>ORC: View Candidate Profile
    REC->>ORC: Review Resume
    REC->>ORC: Review Screening Answers

    alt Candidate Qualified
        REC->>ORC: Move to Screening Phase
        REC->>ORC: Schedule Phone Screen

        ORC-->>CAND: Email: Phone Screen Invitation
        Note right of CAND: Self-Schedule Link<br/>Available Time Slots

        CAND->>ORC: Select Time Slot
        ORC-->>CAND: Phone Screen Confirmation
        ORC-->>REC: Calendar: Phone Screen Scheduled

        Note over REC,CAND: Phone Screen (30 min)
        REC->>CAND: Conduct Phone Screen
        Note right of REC: Skills Assessment<br/>Culture Fit<br/>Salary Expectations<br/>Availability

        REC->>ORC: Log Phone Screen Notes
        REC->>ORC: Update Screening Status

        alt Pass Phone Screen
            REC->>ORC: Status: Screening Passed
            REC->>ORC: Move to Interview Phase
        else Fail Phone Screen
            REC->>ORC: Reject with Reason
            ORC-->>CAND: Rejection Email
            REC->>ORC: Add to Talent Pool?
        end

    else Candidate Not Qualified
        REC->>ORC: Reject with Reason
        Note right of REC: Select Rejection Reason<br/>from Standard List
        ORC-->>CAND: Rejection Email

    else Maybe - Hold for Review
        REC->>ORC: Add to Hold/Review List
        REC->>HM: Request Hiring Manager Opinion
        HM->>ORC: Review Candidate
        HM-->>REC: Proceed / Reject
    end

    Note over CAND,HM: SHORTLIST CREATION

    REC->>ORC: Review All Screened Candidates
    REC->>ORC: Create Shortlist (Top 5-10)
    REC->>HM: Share Shortlist for Review
    HM->>ORC: Review Shortlisted Candidates
    HM-->>REC: Approve Shortlist / Request Changes
```

---

## 5. Phase 4: Interview & Assessment

### Interview Process Workflow

```mermaid
sequenceDiagram
    autonumber

    participant CAND as Candidate
    participant REC as Recruiter
    participant ORC as Oracle Recruiting
    participant INT as Interviewer(s)
    participant HM as Hiring Manager
    participant CAL as Calendar System

    Note over CAND,CAL: INTERVIEW SCHEDULING

    REC->>ORC: Move Candidate to Interview Phase
    REC->>ORC: Select Interview Type
    Note right of REC: Phone, Video, Onsite<br/>Panel, Technical

    REC->>ORC: Select Interviewers
    ORC->>CAL: Check Interviewer Availability
    CAL-->>ORC: Available Time Slots

    alt Self-Schedule Enabled
        REC->>ORC: Enable Self-Schedule
        ORC-->>CAND: Email: Self-Schedule Interview
        CAND->>ORC: Select Preferred Slot
    else Recruiter Schedules
        REC->>ORC: Select Time Slot
        ORC-->>CAND: Email: Interview Scheduled
        CAND-->>ORC: Confirm Attendance
    end

    ORC->>CAL: Create Calendar Event
    ORC-->>INT: Calendar Invite + Candidate Profile
    ORC-->>CAND: Interview Confirmation
    Note right of CAND: Date, Time, Location<br/>Video Link, Instructions

    Note over CAND,CAL: PRE-INTERVIEW

    ORC-->>INT: Reminder: 24 Hours Before
    ORC-->>CAND: Reminder: 24 Hours Before

    INT->>ORC: Review Candidate Profile
    INT->>ORC: Access Interview Guide
    INT->>INT: Prepare Questions

    ORC-->>INT: Reminder: 1 Hour Before
    ORC-->>CAND: Reminder: 1 Hour Before

    Note over CAND,CAL: INTERVIEW EXECUTION

    CAND->>INT: Join Interview (Video/Onsite)
    INT->>CAND: Conduct Structured Interview
    Note right of INT: Competency Questions<br/>Technical Assessment<br/>Culture Fit Evaluation

    INT->>CAND: Answer Candidate Questions
    INT->>CAND: Explain Next Steps

    Note over CAND,CAL: POST-INTERVIEW FEEDBACK

    ORC-->>INT: Request: Submit Feedback
    Note right of ORC: Immediate Request<br/>24hr Reminder<br/>48hr Escalation

    INT->>ORC: Access Interview Scorecard
    INT->>ORC: Rate Competencies (1-5)
    INT->>ORC: Provide Written Feedback
    INT->>ORC: Overall Recommendation
    Note right of INT: Strong Yes / Yes<br/>Maybe / No / Strong No

    INT->>ORC: Submit Feedback
    ORC-->>REC: Notify: Feedback Received
    ORC-->>HM: Notify: Feedback Received

    Note over CAND,CAL: MULTIPLE INTERVIEW ROUNDS

    alt Additional Interview Required
        HM->>REC: Request Additional Round
        REC->>ORC: Schedule Panel Interview

        ORC->>INT: Assign Interview Panel
        Note right of INT: Technical Lead<br/>Team Member<br/>HR Representative

        ORC-->>CAND: Email: Panel Interview Scheduled

        loop Each Panel Member
            INT->>CAND: Conduct Interview Portion
            INT->>ORC: Submit Individual Feedback
        end

    else Assessment Required
        REC->>ORC: Send Assessment Invitation
        ORC-->>CAND: Email: Assessment Link
        Note right of CAND: Technical Test<br/>Cognitive Assessment<br/>Personality Profile

        CAND->>ORC: Complete Assessment
        ORC->>ORC: Auto-Score Assessment
        ORC-->>REC: Assessment Results Ready
        REC->>ORC: Review Results
    end

    Note over CAND,CAL: FEEDBACK AGGREGATION

    REC->>ORC: View All Feedback
    ORC->>ORC: Calculate Aggregate Score
    REC->>ORC: Generate Candidate Summary
    REC->>HM: Send Interview Summary Report
```

---

## 6. Phase 5: Selection & Decision

### Candidate Selection Workflow

```mermaid
sequenceDiagram
    autonumber

    participant REC as Recruiter
    participant ORC as Oracle Recruiting
    participant INT as Interviewer(s)
    participant HM as Hiring Manager
    participant HR as HR Business Partner
    participant CAND as Candidate

    Note over REC,CAND: FEEDBACK COMPILATION

    REC->>ORC: Access Requisition
    REC->>ORC: View All Candidates in Interview Phase

    loop For Each Candidate
        REC->>ORC: Review Interview Feedback
        REC->>ORC: Review Assessment Results
        REC->>ORC: Compile Summary Report
    end

    REC->>ORC: Generate Comparison Matrix
    Note right of REC: Side-by-side scores<br/>Strengths/Weaknesses<br/>Recommendations

    Note over REC,CAND: DEBRIEF MEETING

    REC->>ORC: Schedule Debrief Meeting
    ORC-->>HM: Calendar: Debrief Scheduled
    ORC-->>INT: Calendar: Debrief Scheduled

    REC->>HM: Share Candidate Summary Reports

    Note over HM,INT: Debrief Discussion
    HM->>INT: Review Each Candidate
    INT->>HM: Share Interview Observations
    HM->>INT: Discuss Strengths & Concerns

    alt Consensus Reached
        HM->>HM: Select Top Candidate
        HM->>HM: Identify Backup Candidate
    else No Consensus
        HM->>HR: Escalate for Mediation
        HR->>HM: Provide Objective Input
        HR->>HM: Facilitate Decision
        HM->>HM: Make Final Decision
    end

    Note over REC,CAND: RECORD DECISION

    HM->>ORC: Access Selected Candidate
    HM->>ORC: Record Selection Decision
    HM->>ORC: Document Decision Rationale
    Note right of HM: Objective criteria<br/>Compliance documentation

    HM->>ORC: Status: Manager Approved
    ORC-->>REC: Notify: Selection Complete

    Note over REC,CAND: PROCESS NON-SELECTED CANDIDATES

    loop For Each Non-Selected Candidate
        REC->>ORC: Access Candidate Record
        REC->>ORC: Set Status: Rejected
        REC->>ORC: Select Rejection Reason
        Note right of REC: Position Filled<br/>Not Best Fit<br/>Skills Gap

        ORC-->>CAND: Rejection Email
        Note right of CAND: Professional, timely<br/>Thank for interest

        alt Strong Candidate (Silver Medalist)
            REC->>ORC: Add to Talent Pool
            REC->>ORC: Select Pool Type
            Note right of REC: Silver Medalists<br/>Future Consideration
            ORC-->>CAND: Talent Pool Notification
        end
    end

    Note over REC,CAND: PROCEED TO OFFER

    REC->>ORC: Move Selected Candidate to Offer Phase
    REC->>ORC: Status: Ready for Offer
    ORC-->>REC: Notify: Proceed with Offer Creation
```

---

## 7. Phase 6: Offer Management

### Offer Creation & Approval Workflow

```mermaid
sequenceDiagram
    autonumber

    participant REC as Recruiter
    participant ORC as Oracle Recruiting
    participant COMP as Compensation Team
    participant HM as Hiring Manager
    participant HR as HR Business Partner
    participant EVP as EVP HR
    participant DOCU as DocuSign
    participant CAND as Candidate

    Note over REC,CAND: OFFER CREATION

    REC->>ORC: Access Selected Candidate
    REC->>ORC: Click "Create Offer"

    ORC-->>REC: Display Offer Form
    ORC->>ORC: Pre-fill from Candidate Profile
    ORC->>ORC: Pre-fill from Requisition

    REC->>ORC: Select Offer Template
    Note right of REC: By Country & Job Family

    alt US Position
        REC->>ORC: Select US_STD or US_EXEC Template
    else France Position
        REC->>ORC: Select FR_CDI, FR_CDD, or FR_CADRE Template
    else UK Position
        REC->>ORC: Select UK_STD Template
    else Germany Position
        REC->>ORC: Select DE_STD Template
    else Netherlands Position
        REC->>ORC: Select NL_STD Template
    end

    REC->>ORC: Enter Compensation Details
    Note right of REC: Base Salary, Currency<br/>Bonus Target %<br/>Sign-on Bonus

    REC->>ORC: Set Start Date
    REC->>ORC: Add Benefits Summary
    REC->>ORC: Add Special Conditions

    Note over REC,CAND: COMPENSATION VALIDATION

    REC->>COMP: Request Salary Validation
    COMP->>ORC: Review Proposed Salary
    COMP->>ORC: Check Against Grade Range

    alt Within Salary Range
        COMP-->>REC: Salary Approved
    else Outside Salary Range
        COMP->>HR: Request Exception Approval
        HR->>ORC: Review Exception Request
        alt Exception Approved
            HR-->>COMP: Exception Granted
            COMP-->>REC: Proceed with Offer
        else Exception Denied
            HR-->>COMP: Exception Denied
            COMP-->>REC: Revise Compensation
            REC->>ORC: Adjust Salary
        end
    end

    Note over REC,CAND: OFFER APPROVAL WORKFLOW

    REC->>ORC: Submit Offer for Approval
    ORC->>ORC: Determine Approval Path

    ORC->>HM: Route to Hiring Manager
    ORC-->>HM: Email: Offer Pending Approval

    HM->>ORC: Review Offer Details
    alt Approve
        HM->>ORC: Approve Offer
    else Request Changes
        HM->>ORC: Return with Comments
        ORC-->>REC: Revise Offer
        REC->>ORC: Resubmit
    end

    ORC->>ORC: Check Salary Threshold

    alt Salary < EUR 125K (Standard)
        ORC->>HR: Route to HRBP
        HR->>ORC: Final Approval

    else Salary >= EUR 125K (High Value)
        ORC->>HR: Route to HRBP
        HR->>ORC: Approve
        ORC->>EVP: Route to EVP HR
        EVP->>ORC: Final Approval

    else TOPEX Position
        ORC->>HR: Route to CHRO
        HR->>ORC: Final Approval
    end

    ORC->>ORC: Status: Offer Approved
    ORC-->>REC: Notify: Ready to Extend

    Note over REC,CAND: OFFER EXTENSION (E-SIGNATURE)

    REC->>ORC: Click "Extend Offer"
    ORC->>ORC: Generate Offer Letter PDF
    ORC->>DOCU: Send to DocuSign

    DOCU->>DOCU: Prepare Envelope
    DOCU->>DOCU: Apply Signature Fields
    DOCU-->>CAND: Email: Offer Letter Ready for Signature

    Note over REC,CAND: CANDIDATE RESPONSE

    CAND->>DOCU: Open Offer Letter
    CAND->>DOCU: Review Terms

    alt Accept Offer
        CAND->>DOCU: Sign Electronically
        DOCU-->>ORC: Webhook: Offer Signed
        ORC->>ORC: Attach Signed Offer
        ORC->>ORC: Status: Offer Accepted
        ORC-->>REC: Notify: Offer Accepted
        ORC-->>HM: Notify: Offer Accepted
        ORC-->>CAND: Confirmation: Welcome to GEODIS

    else Negotiate
        CAND->>REC: Counter-Offer Request
        REC->>HM: Discuss Counter Terms
        alt Accept Counter
            REC->>ORC: Revise Offer
            REC->>ORC: Resubmit for Approval
            Note over REC: Return to Approval Process
        else Decline Counter
            REC-->>CAND: Final Offer - No Changes
            CAND->>DOCU: Accept or Decline
        end

    else Decline Offer
        CAND->>DOCU: Decline
        DOCU-->>ORC: Webhook: Offer Declined
        ORC->>ORC: Status: Offer Declined
        ORC-->>REC: Notify: Offer Declined
        REC->>ORC: Capture Decline Reason

        alt Backup Candidate Available
            REC->>ORC: Proceed with Backup Candidate
        else No Backup
            REC->>ORC: Reopen Requisition
        end

    else No Response (5 Days)
        ORC-->>CAND: Reminder Day 3
        ORC-->>CAND: Final Notice Day 5
        ORC->>ORC: Status: Offer Expired
        ORC-->>REC: Notify: No Response
    end
```

---

## 8. Phase 7: Background Check & Compliance

### Background Check Integration Workflow

```mermaid
sequenceDiagram
    autonumber

    participant REC as Recruiter
    participant ORC as Oracle Recruiting
    participant OIC as Oracle Integration Cloud
    participant STER as Sterling API
    participant CAND as Candidate
    participant HR as HR Business Partner
    participant LEGAL as Legal Team

    Note over REC,LEGAL: INITIATE BACKGROUND CHECK

    ORC->>ORC: Offer Accepted Trigger
    ORC->>ORC: Move to Background Check Phase
    ORC-->>REC: Notify: Initiate Background Check

    REC->>ORC: Click "Request Background Check"
    ORC->>ORC: Select Check Package
    Note right of ORC: GEODIS NON-EXEMPT<br/>GEODIS EXEMPT<br/>GEODIS EXECUTIVE

    ORC->>OIC: Background Check Request
    OIC->>OIC: Transform to Sterling Format
    OIC->>STER: POST /orders (Candidate Info)
    STER-->>OIC: Order ID
    OIC-->>ORC: Store Order Reference

    ORC->>ORC: Status: Background Initiated
    ORC-->>REC: Notify: Background Check Started

    Note over REC,LEGAL: CANDIDATE CONSENT

    STER-->>CAND: Email: Consent Request
    Note right of CAND: Authorization Form<br/>Information Request

    CAND->>STER: Open Consent Portal
    CAND->>STER: Provide Authorization
    CAND->>STER: Enter Required Information
    Note right of CAND: SSN, Address History<br/>Employment Details<br/>Education Details

    STER-->>OIC: Webhook: Consent Received
    OIC-->>ORC: Update Status
    ORC->>ORC: Status: Background In Progress

    Note over REC,LEGAL: BACKGROUND INVESTIGATION

    STER->>STER: Run Background Checks

    par Parallel Checks
        STER->>STER: SSN Trace
    and
        STER->>STER: County Criminal Records
    and
        STER->>STER: National Criminal Search
    and
        STER->>STER: Sex Offender Registry
    and
        STER->>STER: Employment Verification
    and
        STER->>STER: Education Verification
    end

    Note right of STER: Processing: 3-7 Business Days

    loop Status Polling (Daily)
        OIC->>STER: GET /orders/{id}/status
        STER-->>OIC: Status Update
        OIC-->>ORC: Update Progress
    end

    Note over REC,LEGAL: RESULTS DELIVERY

    STER->>STER: All Checks Complete
    STER-->>OIC: Webhook: Order Complete

    OIC->>STER: GET /orders/{id}/report
    STER-->>OIC: Full Report (PDF + JSON)

    OIC->>ORC: Send Results
    ORC->>ORC: Parse Results
    ORC->>ORC: Attach Report Document

    alt All Clear
        ORC->>ORC: Status: Background Cleared
        ORC-->>REC: Notify: Background Cleared
        ORC-->>HR: Notify: Proceed with Hire

    else Issues Found
        ORC->>ORC: Status: Background Issue
        ORC-->>HR: Alert: Review Required

        HR->>ORC: Review Findings
        HR->>ORC: Access Full Report

        alt Minor Issue - Proceed
            HR->>ORC: Clear with Notes
            ORC->>ORC: Status: Background Cleared
            ORC->>ORC: Document Decision

        else Concern - Legal Review
            HR->>LEGAL: Escalate to Legal
            LEGAL->>ORC: Review Case
            LEGAL->>HR: Legal Opinion

            alt Proceed with Conditions
                HR->>ORC: Clear with Conditions
                HR->>ORC: Document Conditions
                ORC->>ORC: Status: Background Cleared

            else Do Not Proceed
                HR->>ORC: Fail Background
                ORC->>ORC: Status: Background Failed
                ORC-->>REC: Notify: Rescind Offer
                REC->>ORC: Initiate Offer Rescission
                ORC-->>CAND: Formal Rescission Notice
            end

        else Serious Issue - Fail
            HR->>ORC: Fail Background
            ORC->>ORC: Status: Background Failed
            ORC-->>REC: Notify: Rescind Offer

            REC->>ORC: Rescind Offer
            ORC-->>CAND: Adverse Action Notice
            Note right of CAND: Pre-Adverse Letter<br/>Wait Period<br/>Final Adverse Letter
        end
    end

    Note over REC,LEGAL: PROCEED TO HR PROCESSING

    ORC->>ORC: Background Phase Complete
    ORC->>ORC: Move to HR Processing Phase
    ORC-->>HR: Notify: Ready for Document Collection
```

---

## 9. Phase 8: Hire & Onboarding Handoff

### Hire Processing & Core HR Integration

```mermaid
sequenceDiagram
    autonumber

    participant CAND as Candidate /<br/>New Employee
    participant REC as Recruiter
    participant ORC as Oracle Recruiting
    participant HR as HR Business Partner
    participant CORE as Oracle Core HR
    participant PAY as Payroll
    participant BEN as Benefits
    participant IT as IT Systems
    participant HM as Hiring Manager

    Note over CAND,HM: HR DOCUMENT COLLECTION

    ORC->>ORC: Background Cleared
    ORC->>ORC: Move to HR Processing Phase
    ORC-->>HR: Notify: Collect Pre-Hire Documents

    HR->>ORC: Generate Document Request
    ORC-->>CAND: Email: Required Documents
    Note right of CAND: Government ID / Passport<br/>Work Authorization (I-9)<br/>Tax Forms (W-4, State)<br/>Bank Details (Direct Deposit)<br/>Emergency Contact<br/>Signed Policies

    CAND->>ORC: Upload Documents via Portal

    loop Document Verification
        HR->>ORC: Review Submitted Documents
        alt Document Valid
            HR->>ORC: Mark Document Verified
        else Document Invalid/Missing
            HR->>ORC: Request Resubmission
            ORC-->>CAND: Email: Resubmit Document
            CAND->>ORC: Upload Corrected Document
        end
    end

    HR->>ORC: All Documents Verified
    ORC->>ORC: Status: Documents Complete

    Note over CAND,HM: CONFIRM START DATE

    HR->>CAND: Confirm Start Date
    CAND-->>HR: Confirm or Request Change
    HR->>ORC: Set Official Start Date

    ORC->>ORC: Status: Pre-Hire Complete
    ORC->>ORC: Move to Hire Phase

    Note over CAND,HM: CREATE WORKER RECORD

    HR->>ORC: Initiate Hire Process
    ORC->>ORC: Validate All Required Data
    ORC->>ORC: Click "Convert to Employee"

    ORC->>CORE: Create Pending Worker
    Note right of CORE: Person Record<br/>Assignment Details<br/>Compensation<br/>Manager Link

    CORE->>CORE: Validate Worker Data
    CORE->>CORE: Generate Employee ID
    CORE->>CORE: Create Employment Record

    Note over CAND,HM: SYSTEM INTEGRATIONS

    CORE->>CORE: Trigger Integration Events

    par Parallel System Updates
        CORE->>PAY: Create Payroll Record
        PAY-->>CORE: Payroll Setup Complete
    and
        CORE->>BEN: Create Benefits Eligibility
        BEN-->>CORE: Benefits Ready for Enrollment
    and
        CORE->>IT: Trigger IT Provisioning
        IT->>IT: Create User Account
        IT->>IT: Setup Email
        IT->>IT: Provision Access
        IT-->>CORE: IT Setup Complete
    end

    CORE->>CORE: Verify All Systems Ready

    Note over CAND,HM: COMPLETE HIRING PROCESS

    CORE-->>ORC: Worker Created Successfully
    ORC->>ORC: Status: Hire Confirmed

    REC->>ORC: Update Requisition
    ORC->>ORC: Decrement Positions to Fill

    alt All Positions Filled
        REC->>ORC: Requisition Status: Filled
        REC->>ORC: Close Requisition
    else More Positions Remain
        REC->>ORC: Continue Recruiting
    end

    Note over CAND,HM: NOTIFICATIONS & WELCOME

    ORC-->>REC: Notify: Hire Complete
    ORC-->>HR: Notify: Worker Record Created
    ORC-->>HM: Notify: New Team Member Hired

    CORE-->>CAND: Welcome Email
    Note right of CAND: Employee ID<br/>Portal Login<br/>First Day Instructions<br/>Onboarding Checklist

    Note over CAND,HM: ONBOARDING HANDOFF

    CORE->>CORE: Launch Onboarding Workflow

    CORE-->>CAND: Onboarding Tasks Assigned
    Note right of CAND: Complete Personal Info<br/>Benefits Enrollment<br/>Policy Acknowledgments<br/>Training Assignments

    CORE-->>HM: Manager Onboarding Tasks
    Note right of HM: Prepare Workspace<br/>Schedule Intro Meetings<br/>Assign Buddy/Mentor<br/>Plan First Week

    HM-->>CAND: Personal Welcome Message
    HM->>CAND: First Day Details

    Note over CAND,HM: DAY 1

    CAND->>CAND: Report to Work
    HM->>CAND: Welcome & Office Tour
    IT->>CAND: Equipment & System Access
    HR->>CAND: HR Orientation

    CAND->>CORE: Complete Day 1 Tasks
    CORE->>CORE: Update Onboarding Status

    Note over CAND,HM: RECRUITMENT PROCESS COMPLETE

    ORC->>ORC: Archive Candidate Record
    ORC->>ORC: Update Analytics
    Note right of ORC: Time to Fill<br/>Source Attribution<br/>Cost per Hire
```

---

## 10. Complete Integrated Sequence

### Full End-to-End Summary Timeline

```mermaid
sequenceDiagram
    autonumber

    participant HM as Hiring<br/>Manager
    participant REC as Recruiter
    participant HR as HRBP
    participant ORC as Oracle<br/>Recruiting
    participant EXT as External<br/>Systems
    participant CAND as Candidate
    participant CORE as Core HR

    Note over HM,CORE: WEEK 1-2: REQUISITION
    HM->>ORC: Create Requisition
    ORC->>HR: Approval Workflow
    HR-->>ORC: Approved
    ORC-->>REC: Ready for Posting

    Note over HM,CORE: WEEK 2-3: INTERNAL POSTING (7 Days)
    REC->>ORC: Post Internally
    ORC->>EXT: Internal Portal
    Note over ORC: 7-Day Timer

    Note over HM,CORE: WEEK 3-4: EXTERNAL POSTING
    REC->>ORC: Post Externally
    ORC->>EXT: Indeed, LinkedIn, Career Site
    EXT-->>CAND: Job Visible

    Note over HM,CORE: WEEK 4-6: APPLICATIONS & SCREENING
    CAND->>ORC: Submit Applications
    ORC->>ORC: Auto-Screen
    REC->>ORC: Review & Phone Screen
    REC->>ORC: Create Shortlist

    Note over HM,CORE: WEEK 6-8: INTERVIEWS
    REC->>CAND: Schedule Interviews
    HM->>CAND: Conduct Interviews
    HM->>ORC: Submit Feedback
    HM->>ORC: Selection Decision

    Note over HM,CORE: WEEK 8-9: OFFER
    REC->>ORC: Create Offer
    ORC->>HR: Approval Workflow
    HR-->>ORC: Approved
    ORC->>EXT: DocuSign
    EXT-->>CAND: Offer Letter
    CAND->>EXT: Sign & Accept
    EXT-->>ORC: Offer Accepted

    Note over HM,CORE: WEEK 9-10: BACKGROUND CHECK
    ORC->>EXT: Sterling Request
    EXT-->>CAND: Consent Request
    CAND->>EXT: Provide Info
    EXT->>EXT: Run Checks
    EXT-->>ORC: Results: Cleared

    Note over HM,CORE: WEEK 10-11: PRE-HIRE
    HR->>CAND: Request Documents
    CAND->>ORC: Submit Documents
    HR->>ORC: Verify & Confirm
    ORC->>CORE: Create Worker
    CORE->>CORE: System Setup

    Note over HM,CORE: START DATE: DAY 1
    CORE-->>CAND: Welcome!
    HM->>CAND: Onboarding Begins

    Note over HM,CORE: TOTAL: ~10-12 WEEKS
```

---

## Key Metrics & SLAs

### Process Timeline Summary

| Phase | Duration | SLA | Owner |
|-------|----------|-----|-------|
| Requisition Approval | 2-5 days | 3 days standard | HRBP |
| Internal Posting | 7 days | Mandatory | Recruiter |
| External Posting | 14-21 days | - | Recruiter |
| Screening | 3-5 days | 48hr first review | Recruiter |
| Interviews | 7-14 days | - | Hiring Manager |
| Selection Decision | 2-3 days | 48hr post-interview | Hiring Manager |
| Offer Approval | 2-5 days | 3 days standard | HRBP |
| Offer Response | 5 days | Candidate deadline | Candidate |
| Background Check | 3-7 days | - | Sterling |
| Document Collection | 3-5 days | - | HR |
| Worker Creation | 1-2 days | Before start date | HR |

### Average Time to Fill

| Position Type | Target | Current |
|--------------|--------|---------|
| Hourly/Frontline | 30 days | 35 days |
| Professional | 45 days | 52 days |
| Management | 60 days | 68 days |
| Executive | 90 days | 95 days |

---

## Document Information

| Attribute | Value |
|-----------|-------|
| Document ID | 20_GEODIS_Recruitment_End_to_End_Sequence_Diagram |
| Version | 1.0 |
| Created | 2025-12-08 |
| Format | Mermaid Sequence Diagrams |
| Total Diagrams | 10 |
| Related Documents | 11_Business_Requirements, 12_Workflows, 13_Mermaid_Diagrams, 17_Workflow_Config, 19_Swimlane_Diagrams |

---

*End of Document*
