# Process Mapping Guide

Use this guide when you build the As-Is process map.

## 1. Key Process Actors & Systems 
### Operational Actors 
**Customer:** The account holder who has breached standard payment terms across Credit Card ($45.3\%$), Personal Loan ($39.2\%$), or Auto Finance ($15.5\%$) products. They interact passively via incoming phone calls, email replies, or letters.

**Collections Agent:** The core operator driving manual account reviews, customer outreach, and cross-system data synchronization.

**Team Leader / Manager:** The operational supervisor who monitors performance and tracking metrics primarily through localized spreadsheet files rather than core databases.

### Underlying Systems

**Legacy Collections System (legacy_db):** The primary system of record where delinquent accounts are initially flagged. It houses core financial details but contains significant information gaps.

**Spreadsheet Tracker (spreadsheet):** Disconnected local files manually updated by agents to manage day-to-day workflow tracking and team-level productivity reporting.

**Email & Manual Channels (email / phone):** Unlinked interaction layers used to manage communication histories, customer requests, and informal internal handoffs.

## 2. As-is workflow diagram

```mermaid
graph TD
    %% Define Styles
    classDef actor fill:#f9f,stroke:#333,stroke-width:2px;
    classDef system fill:#bbf,stroke:#333,stroke-width:2px;
    classDef process fill:#fff,stroke:#333,stroke-width:1px;
    classDef decision fill:#ffb,stroke:#333,stroke-width:1px;
    classDef risk fill:#f8d7da,stroke:#dc3545,stroke-width:1.5px;
    classDef painpoint fill:#ffcccc,stroke:#cc0000,stroke-width:2px;
    
    %% --- 1. CLIENT CASE ENTRY ---
    subgraph Stage_1 [1. Client Case Entry]
        Entry([Account Crosses Delinquency Threshold])
        LegacyDB[(Legacy Collections System)]:::system
    end
    
    Entry --> LegacyDB

    %% --- 2. MANUAL CASE INVESTIGATION & TRIAGE ---
    subgraph Stage_2 [2. Manual Case Investigation & Triage]
        Agent((Collections Agent)):::actor
        Investigation[Manual Triage Loop]:::process
        Spreadsheet[(Spreadsheet Tracker)]:::system
        Email[Email Channels / Outlook History]:::system
        Peer[Ask Colleagues / Verbal Check]:::actor
        CombineHistory[Consolidate Account Picture]:::process
        
        %% Pain Point 1
        PP1["💥 PAIN POINT 1: Duplicate Status Checks & Triage Overlap<br>• Evidence: 1,400 'status_check' entries in recovery_activity_tracker.csv<br>• Stakeholder: 'Simple cases take days because they get stuck in the wrong queue' (Priya Nair)"]:::painpoint
    end

    LegacyDB -->|Queue Intake| Agent
    Agent --> Investigation
    
    %% Investigation paths pulling from systems
    Investigation -->|Query Incomplete Details| LegacyDB
    Investigation -->|Check Local Team Rows| Spreadsheet
    Investigation -->|Search Inbox Threads| Email
    Investigation -->|Verbal Memory Check| Peer
    Investigation -.-> PP1
    
    %% Paths combining into consolidation before outreach
    LegacyDB --> CombineHistory
    Spreadsheet --> CombineHistory
    Email --> CombineHistory
    Peer --> CombineHistory

    %% --- 3. CONTACT & OUTCOME LOGGING ---
    subgraph Stage_3 [3. Customer Contact & Duplicate Entry]
        Outreach[Execute Outreach: Call, Email, SMS]:::process
        Customer((Customer)):::actor
        LogOutcome{Determine Outcome}:::decision
        DupEntry[Duplicate Data Entry Process]:::process
        TeamLead((Team Leader / Manager)):::actor
        
        %% Pain Point 2 & 3
        PP2["💥 PAIN POINT 2: Manual Promise-to-Pay Tracking & Stalled Dates<br>• Evidence: 1,195 PTP outcomes in recovery_activity_tracker.csv but missing tracking rules<br>• Stakeholder: 'Cases sit in awaiting callback for months because promise date wasn't recorded' (Lawrence Bennett)"]:::painpoint
        
        PP3["💥 PAIN POINT 3: Heavy Spreadsheet Reconciliation Effort<br>• Evidence: 1,458 'spreadsheet_reconcile' entries in recovery_activity_tracker.csv<br>• Stakeholder: 'The audit trail is scattered... making compliance reviews a nightmare' (Andrea Hunt)"]:::painpoint
    end

    CombineHistory --> Outreach
    Outreach --> Customer
    Customer --> LogOutcome
    
    LogOutcome -->|Next Action Unclear / No Response| Investigation
    LogOutcome -->|Outcome Captured / Promise Made| DupEntry
    DupEntry -.-> PP2
    
    %% Duplicate entry paths
    DupEntry -->|Manual Update| LegacyDB
    DupEntry -->|Manual Update for Team Metrics| Spreadsheet
    DupEntry -->|Optional Progress Summary| TeamLead
    Spreadsheet -.-> PP3

    %% --- 4. REGULATORY & FINAL DISPOSITION ---
    subgraph Stage_4 [4. Compliance & Final Disposition]
        Compliance{Compliance Review /<br>Regulatory Audit?}:::decision
        FinalStatus{Final Resolution State}:::decision
        Resolved([Case Closed: Paid / Arrangement Set])
        Escalated([Case Escalated: Legal / Write-off])
        SyncFailure{Data Sync Breaks or Payment Fails?}:::decision
        
        %% Pain Point 4 & 5
        PP4["💥 PAIN POINT 4: Poor Visibility for Managers & Broken Reports<br>• Evidence: Missing follow-up rate at 14% in finance_assumptions.csv<br>• Stakeholder: 'Data quality is so poor we stopped running management reports altogether' (Ms Andrea Lamb)"]:::painpoint
        
        PP5["💥 PAIN POINT 5: Missed / Delayed Follow-Ups & Phantom Loops<br>• Evidence: 14% missed follow-up rate in finance_assumptions.csv<br>• Operational Observation: Blended hourly agent cost is £22/hr wasted on repetitive outreach due to un-synced data"]:::painpoint
    end

    DupEntry --> Compliance
    Compliance -->|Where Applicable / Audit Check| FinalStatus
    TeamLead -.-> PP4
    
    FinalStatus -->|Escalation Triggered| Escalated
    FinalStatus -->|Resolution Achieved| Resolved
    
    Resolved --> SyncFailure
    SyncFailure -->|Yes: Phantom Re-entry| LegacyDB
    SyncFailure -.-> PP5
    SyncFailure -->|No| EndState([Permanent Resolution])

    %% Set flow direction formatting adjustments
    style Entry fill:#d4edda,stroke:#28a745,stroke-width:2px;
    style EndState fill:#f8d7da,stroke:#dc3545,stroke-width:2px;
    style Escalated fill:#fff3cd,stroke:#ffc107,stroke-width:2px;
    style Compliance fill:#f8d7da,stroke:#dc3545,stroke-width:1.5px;
```

## 3. The Human Impact: How the Process Feels
### For a Customer: Confusing, Repetitive, and Interrogative
**The Experience:**
Customers are caught in an exhausting cycle of inconsistent communications. Because records don't automatically sync, a customer who already negotiated a payment arrangement via email might receive an aggressive automated SMS or a collection phone call the next day asking for the exact same information.
**The Feeling:**
It feels like the organization doesn't communicate internally. Customers report having to call back multiple times simply to remember or re-verify details because they are told different things by different agents, turning an already stressful debt situation into a frustrating administrative ordeal.

### For an Agent: Frustrating, Fragmented, and Bureaucratic
**The Experience:**
Agents spend a massive portion of their workdays acting as data-entry clerks rather than actual relationship managers. To handle a single customer, they have to jump between incomplete legacy systems, manual spreadsheets, and team-specific logs to cobble together basic account context. They must routinely manually record duplicate entries into spreadsheets just so their managers have visibility.
**The Feeling:**
It feels like fighting against the tools to get the job done. Straightforward cases that should take 10 minutes take 18 minutes instead because of the sheer volume of spreadsheet reconciliation and blind status checks. Agents feel forced to rely on unlogged personal "workarounds" rather than standard systems to keep up with performance goals.

### For a Team Leader or Manager: Blind, Reactive, and Stressed 
**The Experience:**
Managers are trapped operating with broken tracking instruments. Because data across the core systems is out-of-sync and unreliable, running standardized executive or operations reports is practically impossible. They are forced to micromanage via localized spreadsheet trackers to understand what their team achieved on a given day.
**The Feeling:**
It feels like navigating an operational minefield. With a $14\%$ missed follow-up rate and a compliance audit trail scattered across disparate emails and spreadsheets, managers are constantly worried about regulatory breaches, lost revenue, and cases quietly rotting in "awaiting callback" queues for months without their knowledge.

## 4. Strategic Automation Opportunities
The following automation initiatives target high-volume, highly repeatable, and rules-driven segments of the workflow.

### Automation Opportunities List
**Unified Digital Self-Service Portal:** Authenticates users, provides automated balance overviews, and allows customers to select standard payment configurations.

**Automated Multi-Channel Outreach Engine:** Programmatically triggers SMS and email notifications based on milestone dates, eliminating manual text/email dispatching.

**Centralized CRM System Integration:** Consolidates phone logs, local spreadsheets, email lines, and core account records into a unified agent dashboard.

**Automated Promise-to-Pay Ledger System:** Digitally tracks confirmed arrangement timelines, cross-references incoming bank statements, and flags payment defaults automatically without human intervention.

**Rules-Based Automated Ingestion and Triage Routing:** Auto-triages early-stage delinquencies via specific routing rules, preventing simple portfolios from bottlenecking manual queues.

**Automated Compliance Logging Engine:** Systematically writes non-editable timestamp logs for every status modification, eliminating manual reporting data entry.

### Traceability Matrix
| Opportunity ID | Proposed Automation Opportunity | Target Process Pain Point | Target Job-to-be-Done (JTBD) Framework |
| :--- | :--- | :--- | :--- |
| **OPP-01** | Unified Digital Self-Service Portal | **PP-02:** Manual PTP tracking errors & stranded files. | **Customer:** "When I default on a monthly statement, I need a private web portal to choose a repayment plan, so I can fix the issue without speaking to an agent." |
| **OPP-02** | Automated Multi-Channel Outreach Engine | **PP-05:** Missed or delayed customer touchpoints ($14\%$ rate). | **Operations:** "When an account enters early-stage default, we need to prompt them instantly via automated SMS/Email, so agents only touch complex accounts." |
| **OPP-03** | Centralized CRM System Integration | **PP-03:** Heavy manual reconciliation workloads ($1,458$ activities). | **Agent:** "When reviewing an account case, I need an integrated portal history, so I do not waste time cross-referencing multiple local team sheets." |
| **OPP-04** | Automated Promise-to-Pay Ledger System | **PP-02:** Cases languishing in callback status with unrecorded dates. | **Operations:** "When an arrangement window is set, we must track the bank balance automatically, so accounts never sit stale inside a queue." |
| **OPP-05** | Rules-Based Ingestion and Triage Routing | **PP-01:** Redundant status checks ($1,400$ entries) trapping low-tier portfolios. | **Manager:** "When collections portfolios spike, we need simple accounts auto-routed to digital paths, saving human resources for high-risk accounts." |
| **OPP-06** | Automated Compliance Logging Engine | **PP-04:** Complete lack of centralized management visibility & broken reports. | **Compliance:** "When a regulatory audit occurs, we need an automated system ledger of all histories, so we can verify compliance without file-hunting." |

## 5. Operational Guardrails: Agent-Led Boundaries
To safeguard the business against credit risk and regulatory compliance issues, specific strategic zones must remain strictly agent-led:

**Vulnerability & Vulnerable Customer Hardship Assessments:** As emphasized in the team reviews, “We cannot automate the decision about whether a customer is genuinely in hardship or just dodging contact”. Determining true vulnerability demands deep human empathy, investigative flexibility, and adherence to consumer protection rules that strict code logic cannot substitute.
**Collateralized Asset Configurations:** Accounts tied to asset-backed portfolios, such as Auto Finance ($15.5\%$ of current volume), cannot follow a completely automated recovery path. Asset valuation, repossession protocols, and voluntary surrender management involve complex logistics requiring human oversight and negotiation.
**Late-Stage Delinquency & Litigation Pathing:** High-severity accounts sitting in Late Delinquency ($15.9\%$) or labeled as legal_watch or specialist_review require delicate legal and financial management. Decisions relating to writing off debt balances or approving formal litigation should always require manual manager approval to minimize legal exposure.