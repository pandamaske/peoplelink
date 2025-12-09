# GEODIS Recruitment Process - Swimlane Diagrams

**Document:** 19_GEODIS_Recruitment_Swimlane_Diagrams.md
**Version:** 1.0
**Created:** 2025-12-07
**Module:** Oracle Recruiting Cloud (IRC)
**Project:** GEODIS HCM Transformation

---

## Table of Contents

1. [End-to-End Master Swimlane](#1-end-to-end-master-swimlane)
2. [Requisition Creation & Approval](#2-requisition-creation--approval)
3. [Job Posting & Sourcing](#3-job-posting--sourcing)
4. [Candidate Screening & Shortlisting](#4-candidate-screening--shortlisting)
5. [Interview & Assessment](#5-interview--assessment)
6. [Selection & Decision](#6-selection--decision)
7. [Offer Management](#7-offer-management)
8. [Background Check & Pre-Hire](#8-background-check--pre-hire)
9. [Hire & Onboarding Handoff](#9-hire--onboarding-handoff)

---

## 1. End-to-End Master Swimlane

### Complete Recruitment Lifecycle by Role

```mermaid
flowchart TB
    subgraph CANDIDATE["CANDIDATE"]
        direction LR
        C1[Apply for Job] --> C2[Complete Profile]
        C2 --> C3[Take Assessment]
        C3 --> C4[Attend Interview]
        C4 --> C5[Receive Offer]
        C5 --> C6[Accept/Decline]
        C6 --> C7[Submit Documents]
        C7 --> C8[Start Work]
    end

    subgraph HIRING_MANAGER["HIRING MANAGER"]
        direction LR
        HM1[Identify Need] --> HM2[Create Requisition]
        HM2 --> HM3[Define Requirements]
        HM3 --> HM4[Review Candidates]
        HM4 --> HM5[Conduct Interview]
        HM5 --> HM6[Select Candidate]
        HM6 --> HM7[Approve Offer]
        HM7 --> HM8[Welcome New Hire]
    end

    subgraph RECRUITER["RECRUITER"]
        direction LR
        R1[Receive Requisition] --> R2[Post Job]
        R2 --> R3[Source Candidates]
        R3 --> R4[Screen Applications]
        R4 --> R5[Shortlist]
        R5 --> R6[Schedule Interviews]
        R6 --> R7[Collect Feedback]
        R7 --> R8[Create Offer]
        R8 --> R9[Extend Offer]
        R9 --> R10[Coordinate Hire]
    end

    subgraph HR_PARTNER["HR BUSINESS PARTNER"]
        direction LR
        HR1[Validate Headcount] --> HR2[Approve Requisition]
        HR2 --> HR3[Support Process]
        HR3 --> HR4[Review Compensation]
        HR4 --> HR5[Approve Offer]
        HR5 --> HR6[Process Background]
        HR6 --> HR7[Create Worker Record]
    end

    subgraph INTERVIEWER["INTERVIEWER"]
        direction LR
        I1[Accept Interview] --> I2[Review CV]
        I2 --> I3[Conduct Interview]
        I3 --> I4[Submit Feedback]
        I4 --> I5[Participate in Debrief]
    end

    %% Cross-lane connections
    HM1 --> HR1
    HR2 --> R1
    R2 -.-> C1
    R4 --> HM4
    R6 --> I1
    R6 -.-> C4
    HM5 --> I3
    I4 --> R7
    HM6 --> R8
    HR5 --> R9
    R9 -.-> C5
    C6 --> R10
    HR7 --> HM8
    HR7 -.-> C8

    style CANDIDATE fill:#E8F5E9,stroke:#4CAF50
    style HIRING_MANAGER fill:#E3F2FD,stroke:#2196F3
    style RECRUITER fill:#FFF3E0,stroke:#FF9800
    style HR_PARTNER fill:#FCE4EC,stroke:#E91E63
    style INTERVIEWER fill:#F3E5F5,stroke:#9C27B0
```

### Legend
| Lane Color | Role | Primary Responsibility |
|------------|------|----------------------|
| Green | Candidate | Apply, interview, accept offer |
| Blue | Hiring Manager | Define need, interview, select |
| Orange | Recruiter | Source, screen, coordinate |
| Pink | HR Business Partner | Approve, compliance, process |
| Purple | Interviewer | Assess, provide feedback |

---

## 2. Requisition Creation & Approval

### Detailed Requisition Workflow by Role

```mermaid
flowchart TB
    subgraph HM["HIRING MANAGER"]
        direction LR
        HM1([Identify Hiring Need]) --> HM2[Check Budget Slot]
        HM2 --> HM3{Budgeted<br/>Position?}
        HM3 -->|Yes| HM4[Create Requisition]
        HM3 -->|No| HM5[Request Exception]
        HM4 --> HM6[Select Template]
        HM6 --> HM7[Enter Job Details]
        HM7 --> HM8[Define Requirements]
        HM8 --> HM9[Set Compensation Range]
        HM9 --> HM10[Assign Hiring Team]
        HM10 --> HM11[Submit for Approval]
    end

    subgraph FINANCE["FINANCE / BUDGET OWNER"]
        direction LR
        HM5 --> FIN1[Review Exception]
        FIN1 --> FIN2{Approve<br/>Exception?}
        FIN2 -->|Yes| HM4
        FIN2 -->|No| FIN3[Deny - End Process]
    end

    subgraph MGR["MANAGER'S MANAGER"]
        direction LR
        HM11 --> MGR1[Review Requisition]
        MGR1 --> MGR2{Approve?}
        MGR2 -->|Yes| MGR3[Forward to HR]
        MGR2 -->|No| MGR4[Return with Comments]
        MGR4 --> HM7
    end

    subgraph HRBP["HR BUSINESS PARTNER"]
        direction LR
        MGR3 --> HR1[Validate Job Details]
        HR1 --> HR2[Check Compensation Range]
        HR2 --> HR3[Verify Compliance]
        HR3 --> HR4{All Valid?}
        HR4 -->|Yes| HR5[Approve Requisition]
        HR4 -->|No| HR6[Return for Correction]
        HR6 --> HM7
    end

    subgraph SENIOR["SENIOR APPROVAL (if > EUR 125K)"]
        direction LR
        HR5 --> SR1{Salary ><br/>EUR 125K?}
        SR1 -->|No| REC1
        SR1 -->|Yes| SR2[Director Approval]
        SR2 --> SR3{Salary ><br/>EUR 155K?}
        SR3 -->|No| REC1
        SR3 -->|Yes| SR4[VP Approval]
        SR4 --> SR5[CHRO Approval]
        SR5 --> REC1
    end

    subgraph REC["RECRUITER"]
        direction LR
        REC1([Requisition Activated]) --> REC2[Assign to Requisition]
        REC2 --> REC3[Begin Posting Process]
    end

    style HM fill:#E3F2FD,stroke:#2196F3
    style FINANCE fill:#FFF9C4,stroke:#FFC107
    style MGR fill:#DCEDC8,stroke:#8BC34A
    style HRBP fill:#FCE4EC,stroke:#E91E63
    style SENIOR fill:#FFCCBC,stroke:#FF5722
    style REC fill:#FFF3E0,stroke:#FF9800
```

### Approval Matrix Reference

| Salary Band | Approval Chain | SLA |
|-------------|---------------|-----|
| < EUR 125K | Manager → HRBP | 2 days |
| EUR 125K - 155K | Manager → Director → HRBP | 3 days |
| > EUR 155K / TOPEX | Manager → Director → VP → CHRO | 5 days |

---

## 3. Job Posting & Sourcing

### Multi-Channel Posting Workflow

```mermaid
flowchart TB
    subgraph RECRUITER["RECRUITER"]
        direction LR
        R1([Requisition Active]) --> R2[Review Job Description]
        R2 --> R3[Optimize for Search]
        R3 --> R4[Select Posting Channels]
        R4 --> R5[Post Internally]
        R5 --> R6[Start 7-Day Timer]
        R6 --> R7{7 Days<br/>Elapsed?}
        R7 -->|No| R8[Monitor Internal Apps]
        R8 --> R7
        R7 -->|Yes| R9[Post Externally]
        R9 --> R10[Monitor All Channels]
        R10 --> R11[Track Source Metrics]
    end

    subgraph SYSTEM["ORACLE RECRUITING SYSTEM"]
        direction LR
        R5 --> SYS1[Internal Portal]
        SYS1 --> SYS2[Email Notifications]
        R9 --> SYS3[Career Site]
        R9 --> SYS4[Indeed API]
        R9 --> SYS5[LinkedIn API]
        R9 --> SYS6[Other Job Boards]
        SYS3 --> SYS7[Application Received]
        SYS4 --> SYS7
        SYS5 --> SYS7
        SYS6 --> SYS7
        SYS7 --> SYS8[Auto-Screening Rules]
        SYS8 --> SYS9[Candidate Queue]
    end

    subgraph CANDIDATE["CANDIDATE"]
        direction LR
        SYS2 -.-> C1[View Internal Posting]
        SYS3 -.-> C2[View Career Site]
        SYS4 -.-> C3[View on Indeed]
        SYS5 -.-> C4[View on LinkedIn]
        C1 --> C5[Apply]
        C2 --> C5
        C3 --> C5
        C4 --> C5
        C5 --> C6[Complete Application Form]
        C6 --> C7[Upload Resume]
        C7 --> C8[Answer Screening Questions]
        C8 --> SYS7
    end

    subgraph HM["HIRING MANAGER"]
        direction LR
        SYS9 --> HM1[View Application Queue]
        HM1 --> HM2[Express Interest in Candidates]
    end

    style RECRUITER fill:#FFF3E0,stroke:#FF9800
    style SYSTEM fill:#E0E0E0,stroke:#757575
    style CANDIDATE fill:#E8F5E9,stroke:#4CAF50
    style HM fill:#E3F2FD,stroke:#2196F3
```

### Posting Channel Matrix

| Channel | Type | Auto-Post | Application Sync |
|---------|------|-----------|-----------------|
| Internal Portal | Internal | Yes | Real-time |
| GEODIS Career Site | External | Yes | Real-time |
| Indeed | External | API | 15 min |
| LinkedIn | External | API | 15 min |
| Glassdoor | External | Manual | Daily |
| Agencies | External | Manual | Manual |

---

## 4. Candidate Screening & Shortlisting

### Screening Workflow by Role

```mermaid
flowchart TB
    subgraph SYSTEM["SYSTEM (AUTO-SCREENING)"]
        direction LR
        SYS1([Application Received]) --> SYS2[Parse Resume]
        SYS2 --> SYS3[Check Minimum Quals]
        SYS3 --> SYS4{Meets<br/>Minimum?}
        SYS4 -->|No| SYS5[Auto-Reject]
        SYS5 --> SYS6[Send Rejection Email]
        SYS4 -->|Yes| SYS7[Calculate Score]
        SYS7 --> SYS8[Check Duplicates]
        SYS8 --> SYS9[Add to Queue]
    end

    subgraph RECRUITER["RECRUITER"]
        direction LR
        SYS9 --> R1[Review Application Queue]
        R1 --> R2[Assess Against Criteria]
        R2 --> R3{Qualified?}
        R3 -->|No| R4[Reject with Reason]
        R4 --> R5[Send Rejection Email]
        R4 --> R6[Add to Talent Pool?]
        R3 -->|Yes| R7[Shortlist Candidate]
        R7 --> R8[Add Notes/Tags]
        R8 --> R9[Move to Phone Screen]
        R9 --> R10[Schedule Phone Screen]
    end

    subgraph CANDIDATE["CANDIDATE"]
        direction LR
        SYS6 -.-> C1[Receive Rejection]
        R5 -.-> C1
        R10 -.-> C2[Receive Schedule Request]
        C2 --> C3[Select Available Slot]
        C3 --> C4[Confirm Appointment]
    end

    subgraph RECRUITER2["RECRUITER (Phone Screen)"]
        direction LR
        C4 --> R11[Conduct Phone Screen]
        R11 --> R12[Ask Screening Questions]
        R12 --> R13[Assess Fit & Interest]
        R13 --> R14{Pass Phone<br/>Screen?}
        R14 -->|No| R15[Reject - Not Fit]
        R14 -->|Yes| R16[Move to Interview Phase]
    end

    subgraph HM["HIRING MANAGER"]
        direction LR
        R16 --> HM1[Review Shortlist]
        HM1 --> HM2[Rank Candidates]
        HM2 --> HM3[Select for Interview]
        HM3 --> HM4[Define Interview Panel]
    end

    style SYSTEM fill:#E0E0E0,stroke:#757575
    style RECRUITER fill:#FFF3E0,stroke:#FF9800
    style RECRUITER2 fill:#FFF3E0,stroke:#FF9800
    style CANDIDATE fill:#E8F5E9,stroke:#4CAF50
    style HM fill:#E3F2FD,stroke:#2196F3
```

### Screening Criteria Checklist

| Criterion | Auto-Check | Manual Review |
|-----------|------------|---------------|
| Right to Work | Yes | If unclear |
| Minimum Education | Yes | No |
| Minimum Experience | Yes | No |
| Required Skills | Partial | Yes |
| Location Match | Yes | If remote |
| Salary Expectations | No | Yes |
| Cultural Fit | No | Yes |

---

## 5. Interview & Assessment

### Interview Process Swimlane

```mermaid
flowchart TB
    subgraph RECRUITER["RECRUITER"]
        direction LR
        R1([Candidate Shortlisted]) --> R2[Define Interview Format]
        R2 --> R3[Identify Interviewers]
        R3 --> R4[Check Calendars]
        R4 --> R5[Propose Time Slots]
        R5 --> R6[Send Interview Invite]
        R6 --> R7[Book Meeting Room/Video]
        R7 --> R8[Send Confirmation]
        R8 --> R9[Send Reminders -24h, -1h]
    end

    subgraph CANDIDATE["CANDIDATE"]
        direction LR
        R6 -.-> C1[Receive Invite]
        C1 --> C2[Select Time Slot]
        C2 --> C3[Confirm Attendance]
        R8 -.-> C4[Receive Details]
        C4 --> C5[Prepare for Interview]
        R9 -.-> C6[Receive Reminders]
        C6 --> C7[Join Interview]
        C7 --> C8[Complete Assessment]
    end

    subgraph INTERVIEWER["INTERVIEWER(S)"]
        direction LR
        R8 -.-> I1[Receive Meeting Invite]
        I1 --> I2[Review Candidate CV]
        I2 --> I3[Review Interview Guide]
        I3 --> I4[Prepare Questions]
        R9 -.-> I5[Receive Reminder]
        I5 --> I6[Conduct Interview]
        C7 --> I6
        I6 --> I7[Ask Structured Questions]
        I7 --> I8[Evaluate Responses]
        I8 --> I9[Complete Scorecard]
        I9 --> I10[Submit Feedback]
    end

    subgraph HM["HIRING MANAGER"]
        direction LR
        R8 -.-> HM1[Receive Meeting Invite]
        HM1 --> HM2[Lead Interview Panel]
        I6 --> HM2
        HM2 --> HM3[Assess Cultural Fit]
        HM3 --> HM4[Complete Own Scorecard]
        I10 --> HM5[Review All Feedback]
        HM4 --> HM5
        HM5 --> HM6[Lead Debrief Session]
        HM6 --> HM7[Make Recommendation]
    end

    subgraph HRBP["HR (for compliance)"]
        direction LR
        I10 --> HR1[Audit Interview Documentation]
        HR1 --> HR2[Flag Any Concerns]
        HR2 --> HR3[Validate Process Compliance]
    end

    style RECRUITER fill:#FFF3E0,stroke:#FF9800
    style CANDIDATE fill:#E8F5E9,stroke:#4CAF50
    style INTERVIEWER fill:#F3E5F5,stroke:#9C27B0
    style HM fill:#E3F2FD,stroke:#2196F3
    style HRBP fill:#FCE4EC,stroke:#E91E63
```

### Interview Type Matrix

| Interview Type | Format | Duration | Participants |
|---------------|--------|----------|--------------|
| Phone Screen | Phone/Video | 30 min | Recruiter |
| Technical | Video/Onsite | 60 min | Technical Lead |
| Behavioral | Video/Onsite | 45 min | Hiring Manager |
| Panel | Video/Onsite | 90 min | 3-4 Interviewers |
| Case Study | Video/Onsite | 60 min | Senior Manager |
| Executive | Onsite | 2 hours | VP/Director |

---

## 6. Selection & Decision

### Decision-Making Swimlane

```mermaid
flowchart TB
    subgraph INTERVIEWER["INTERVIEWERS"]
        direction LR
        I1([Interviews Complete]) --> I2[Submit Individual Scores]
        I2 --> I3[Provide Written Feedback]
        I3 --> I4[Make Recommendation]
        I4 --> I5[Flag Any Concerns]
    end

    subgraph RECRUITER["RECRUITER"]
        direction LR
        I5 --> R1[Compile All Feedback]
        R1 --> R2[Calculate Aggregate Score]
        R2 --> R3[Prepare Candidate Summary]
        R3 --> R4[Schedule Debrief Meeting]
        R4 --> R5[Facilitate Discussion]
    end

    subgraph HM["HIRING MANAGER"]
        direction LR
        R5 --> HM1[Review All Feedback]
        HM1 --> HM2[Discuss with Panel]
        HM2 --> HM3{Consensus<br/>Reached?}
        HM3 -->|Yes| HM4[Select Finalist]
        HM3 -->|No| HM5[Escalate Decision]
        HM4 --> HM6[Rank Backup Candidates]
        HM6 --> HM7[Document Decision Rationale]
        HM7 --> HM8[Initiate Offer Request]
    end

    subgraph HRBP["HR BUSINESS PARTNER"]
        direction LR
        HM5 --> HR1[Mediate Discussion]
        HR1 --> HR2[Provide Objective Input]
        HR2 --> HM4
        HM8 --> HR3[Review Selection]
        HR3 --> HR4[Validate Compliance]
        HR4 --> HR5{Approved?}
        HR5 -->|Yes| HR6[Authorize Offer Creation]
        HR5 -->|No| HR7[Return for Review]
        HR7 --> HM1
    end

    subgraph REJECTED["REJECTED CANDIDATES"]
        direction LR
        HM4 --> REJ1[Identify Non-Selected]
        REJ1 --> REJ2[Prepare Rejection Messages]
        REJ2 --> REJ3[Send Rejections]
        REJ3 --> REJ4[Add to Talent Pool?]
    end

    style INTERVIEWER fill:#F3E5F5,stroke:#9C27B0
    style RECRUITER fill:#FFF3E0,stroke:#FF9800
    style HM fill:#E3F2FD,stroke:#2196F3
    style HRBP fill:#FCE4EC,stroke:#E91E63
    style REJECTED fill:#FFEBEE,stroke:#F44336
```

### Decision Criteria Framework

| Factor | Weight | Evaluators |
|--------|--------|------------|
| Technical Skills | 30% | Technical Interviewers |
| Experience | 25% | Hiring Manager |
| Cultural Fit | 20% | All Interviewers |
| Communication | 15% | All Interviewers |
| Growth Potential | 10% | Hiring Manager + HR |

---

## 7. Offer Management

### Offer Creation & Approval Swimlane

```mermaid
flowchart TB
    subgraph RECRUITER["RECRUITER"]
        direction LR
        R1([Selection Approved]) --> R2[Gather Offer Details]
        R2 --> R3[Determine Base Salary]
        R3 --> R4[Add Benefits Package]
        R4 --> R5[Set Start Date Options]
        R5 --> R6[Select Offer Template]
        R6 --> R7[Generate Offer Letter]
        R7 --> R8[Submit for Approval]
    end

    subgraph COMPENSATION["COMPENSATION TEAM"]
        direction LR
        R3 --> COMP1[Validate Salary Range]
        COMP1 --> COMP2{Within<br/>Range?}
        COMP2 -->|Yes| COMP3[Approve Compensation]
        COMP2 -->|No| COMP4[Exception Required]
        COMP4 --> COMP5[Review Market Data]
        COMP5 --> COMP6{Justify<br/>Exception?}
        COMP6 -->|Yes| COMP7[Approve with Exception]
        COMP6 -->|No| COMP8[Reject - Revise Offer]
        COMP8 --> R3
        COMP3 --> R7
        COMP7 --> R7
    end

    subgraph HM["HIRING MANAGER"]
        direction LR
        R8 --> HM1[Review Offer Package]
        HM1 --> HM2{Approve?}
        HM2 -->|Yes| HM3[Approve Offer]
        HM2 -->|No| HM4[Request Changes]
        HM4 --> R2
    end

    subgraph HRBP["HR BUSINESS PARTNER"]
        direction LR
        HM3 --> HR1[Final Compliance Check]
        HR1 --> HR2[Verify Legal Requirements]
        HR2 --> HR3{All Clear?}
        HR3 -->|Yes| HR4[Final Approval]
        HR3 -->|No| HR5[Flag Issues]
        HR5 --> R2
    end

    subgraph SENIOR["SENIOR APPROVAL (if required)"]
        direction LR
        HR4 --> SR1{Salary ><br/>EUR 125K?}
        SR1 -->|No| EXT1
        SR1 -->|Yes| SR2[Director Approval]
        SR2 --> SR3{Salary ><br/>EUR 155K?}
        SR3 -->|No| EXT1
        SR3 -->|Yes| SR4[VP Approval]
        SR4 --> SR5[CHRO Approval]
        SR5 --> EXT1
    end

    subgraph EXTEND["EXTEND OFFER"]
        direction LR
        EXT1([Offer Approved]) --> EXT2[Recruiter Extends Offer]
        EXT2 --> EXT3[Send via DocuSign]
        EXT3 --> EXT4[Track Response]
    end

    subgraph CANDIDATE["CANDIDATE"]
        direction LR
        EXT3 -.-> C1[Receive Offer Email]
        C1 --> C2[Review Offer Letter]
        C2 --> C3{Decision}
        C3 -->|Accept| C4[Sign Electronically]
        C3 -->|Negotiate| C5[Request Changes]
        C3 -->|Decline| C6[Decline Offer]
        C5 --> EXT4
        C4 --> C7[Confirmation Received]
    end

    style RECRUITER fill:#FFF3E0,stroke:#FF9800
    style COMPENSATION fill:#FFF9C4,stroke:#FFC107
    style HM fill:#E3F2FD,stroke:#2196F3
    style HRBP fill:#FCE4EC,stroke:#E91E63
    style SENIOR fill:#FFCCBC,stroke:#FF5722
    style EXTEND fill:#C8E6C9,stroke:#4CAF50
    style CANDIDATE fill:#E8F5E9,stroke:#4CAF50
```

### Offer Templates by Region

| Region | Contract Type | Template Code |
|--------|--------------|---------------|
| USA | At-Will | US_STD, US_EXEC |
| France | CDI/CDD | FR_CDI, FR_CDD, FR_CADRE |
| Germany | Standard/Fixed | DE_STD, DE_EXEC |
| UK | Standard | UK_STD, UK_EXEC |
| Netherlands | Standard | NL_STD, NL_EXEC |

---

## 8. Background Check & Pre-Hire

### Background & Document Collection Swimlane

```mermaid
flowchart TB
    subgraph HRBP["HR BUSINESS PARTNER"]
        direction LR
        HR1([Offer Accepted]) --> HR2[Initiate Background Check]
        HR2 --> HR3[Send Consent Request]
        HR3 --> HR4[Submit to Sterling]
        HR4 --> HR5[Monitor Progress]
        HR5 --> HR6{Results<br/>Received?}
        HR6 -->|No| HR5
        HR6 -->|Yes| HR7[Review Results]
        HR7 --> HR8{All Clear?}
        HR8 -->|Yes| HR9[Proceed to Hire]
        HR8 -->|No| HR10[Escalate for Review]
    end

    subgraph STERLING["STERLING (BACKGROUND CHECK)"]
        direction LR
        HR4 --> ST1[Receive Request]
        ST1 --> ST2[Send Candidate Link]
        ST2 --> ST3[Run Checks]
        ST3 --> ST4[Generate Report]
        ST4 --> HR6
    end

    subgraph CANDIDATE["CANDIDATE"]
        direction LR
        HR3 -.-> C1[Receive Consent Request]
        C1 --> C2[Provide Authorization]
        ST2 -.-> C3[Receive Sterling Link]
        C3 --> C4[Complete Information]
        C4 --> ST3
        HR9 -.-> C5[Receive Document Request]
        C5 --> C6[Gather Documents]
        C6 --> C7[Submit via Portal]
    end

    subgraph LEGAL["LEGAL (if issues)"]
        direction LR
        HR10 --> L1[Review Finding]
        L1 --> L2[Assess Risk]
        L2 --> L3{Proceed?}
        L3 -->|Yes - Proceed| HR9
        L3 -->|Yes - Conditional| L4[Add Conditions]
        L4 --> HR9
        L3 -->|No| L5[Rescind Offer]
    end

    subgraph HRBP2["HR (Document Collection)"]
        direction LR
        C7 --> HR11[Receive Documents]
        HR11 --> HR12[Validate Documents]
        HR12 --> HR13{Complete?}
        HR13 -->|No| HR14[Request Missing]
        HR14 -.-> C5
        HR13 -->|Yes| HR15[Clear for Hire]
    end

    style HRBP fill:#FCE4EC,stroke:#E91E63
    style STERLING fill:#E0E0E0,stroke:#757575
    style CANDIDATE fill:#E8F5E9,stroke:#4CAF50
    style LEGAL fill:#FFCCBC,stroke:#FF5722
    style HRBP2 fill:#FCE4EC,stroke:#E91E63
```

### Background Check Components

| Check Type | Standard | Executive | Intern |
|------------|----------|-----------|--------|
| Criminal History | Yes | Yes | Yes |
| Employment Verification | 7 years | 10 years | N/A |
| Education Verification | Highest | All | Yes |
| Reference Checks | 2 | 3 | 1 |
| Credit Check | If Financial | Yes | No |
| Drug Screening | US Only | US Only | US Only |

---

## 9. Hire & Onboarding Handoff

### Worker Creation & System Sync Swimlane

```mermaid
flowchart TB
    subgraph HRBP["HR BUSINESS PARTNER"]
        direction LR
        HR1([Cleared for Hire]) --> HR2[Confirm Start Date]
        HR2 --> HR3[Create Worker Record]
        HR3 --> HR4[Enter Personal Details]
        HR4 --> HR5[Assign Job]
        HR5 --> HR6[Set Compensation]
        HR6 --> HR7[Assign Manager]
        HR7 --> HR8[Set Location/Cost Center]
        HR8 --> HR9[Submit Worker Record]
    end

    subgraph ORACLE["ORACLE HCM CORE"]
        direction LR
        HR9 --> ORC1[Validate Data]
        ORC1 --> ORC2[Generate Employee ID]
        ORC2 --> ORC3[Create Assignments]
        ORC3 --> ORC4[Trigger Integrations]
    end

    subgraph SYSTEMS["DOWNSTREAM SYSTEMS"]
        direction LR
        ORC4 --> SYS1[Payroll Setup]
        ORC4 --> SYS2[Benefits Enrollment]
        ORC4 --> SYS3[Time & Attendance]
        ORC4 --> SYS4[Learning Management]
        ORC4 --> SYS5[IT Provisioning]
        SYS1 --> SYS6{All Systems<br/>Ready?}
        SYS2 --> SYS6
        SYS3 --> SYS6
        SYS4 --> SYS6
        SYS5 --> SYS6
    end

    subgraph RECRUITER["RECRUITER"]
        direction LR
        HR9 --> R1[Update Requisition Status]
        R1 --> R2[Close Requisition]
        R2 --> R3[Archive Application]
        R3 --> R4[Update Metrics]
    end

    subgraph HM["HIRING MANAGER"]
        direction LR
        SYS6 -->|Yes| HM1[Receive New Hire Notification]
        HM1 --> HM2[Prepare Workspace]
        HM2 --> HM3[Plan First Week]
        HM3 --> HM4[Assign Buddy/Mentor]
        HM4 --> HM5[Schedule Intro Meetings]
    end

    subgraph CANDIDATE["NEW EMPLOYEE"]
        direction LR
        SYS6 -->|Yes| C1[Receive Welcome Email]
        C1 --> C2[Access Employee Portal]
        C2 --> C3[Complete Onboarding Tasks]
        C3 --> C4[Enroll in Benefits]
        C4 --> C5[Complete Compliance Training]
        C5 --> C6[Day 1 Ready]
    end

    subgraph ONBOARD["ONBOARDING TEAM"]
        direction LR
        C6 --> ONB1[Welcome Session]
        ONB1 --> ONB2[Office Tour]
        ONB2 --> ONB3[IT Setup]
        ONB3 --> ONB4[Policy Review]
        ONB4 --> ONB5[Team Introduction]
    end

    style HRBP fill:#FCE4EC,stroke:#E91E63
    style ORACLE fill:#E0E0E0,stroke:#757575
    style SYSTEMS fill:#E1F5FE,stroke:#03A9F4
    style RECRUITER fill:#FFF3E0,stroke:#FF9800
    style HM fill:#E3F2FD,stroke:#2196F3
    style CANDIDATE fill:#E8F5E9,stroke:#4CAF50
    style ONBOARD fill:#F3E5F5,stroke:#9C27B0
```

### Onboarding Checklist by Role

| Task | Owner | Timing |
|------|-------|--------|
| Create Worker Record | HR | D-5 |
| IT Account Setup | IT | D-3 |
| Workspace Prep | Manager | D-2 |
| Welcome Email | HR | D-1 |
| Day 1 Orientation | Onboarding Team | D |
| Benefits Enrollment | Employee | D+1 to D+30 |
| Compliance Training | Employee | D+1 to D+7 |
| 30-Day Check-in | Manager | D+30 |
| 90-Day Review | Manager + HR | D+90 |

---

## Summary: Key Actors & Responsibilities

### Actor Responsibility Matrix

| Actor | Key Responsibilities | Tools Used |
|-------|---------------------|------------|
| **Hiring Manager** | Define need, interview, select, welcome | Oracle Recruiting, Outlook |
| **Recruiter** | Post, source, screen, schedule, coordinate | Oracle Recruiting, LinkedIn, Indeed |
| **HR Business Partner** | Approve, compliance, process hire | Oracle Recruiting, Core HR |
| **Interviewer** | Assess, provide structured feedback | Oracle Recruiting (Scorecard) |
| **Compensation Team** | Validate salary, approve exceptions | Oracle Compensation |
| **Legal** | Review background issues, compliance | Case Management |
| **IT** | Provision accounts, equipment | ServiceNow |
| **Candidate/Employee** | Apply, interview, accept, onboard | Career Site, Employee Portal |

---

## Document Information

| Attribute | Value |
|-----------|-------|
| Document ID | 19_GEODIS_Recruitment_Swimlane_Diagrams |
| Version | 1.0 |
| Created | 2025-12-07 |
| Total Diagrams | 9 |
| Format | Mermaid Markdown (Swimlane style) |
| Related Docs | 12_Workflows, 13_Mermaid_Diagrams |

---

*End of Document*
