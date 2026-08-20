# Microsoft Sentinel Incident Response Playbook with Defender for Endpoint

### Cloud SIEM | Endpoint Detection & Response | Incident Response | KQL | MITRE ATT&CK | Detection Engineering | SOC Operations

---

## Project Overview

This project demonstrates the design, implementation, and operation of a cloud-based Security Operations Centre (SOC) lab using **Microsoft Sentinel**, **Microsoft Defender for Endpoint**, **Microsoft Entra ID**, and a Windows endpoint.

The objective was to build a realistic security monitoring and incident response environment capable of collecting endpoint and identity telemetry, detecting suspicious activity, generating security incidents, supporting analyst investigation, performing containment actions, and documenting the complete incident lifecycle.

Rather than simply creating a few Sentinel analytics rules, the project follows a structured SOC investigation methodology designed to simulate how a Security Operations Centre analyst would handle an alert from initial detection through investigation, containment, recovery, and post-incident improvement.

The project covers the complete detection-to-response lifecycle:

```text
Telemetry Collection
        ↓
Detection Engineering
        ↓
Alert Generation
        ↓
Incident Creation
        ↓
Initial Triage
        ↓
Investigation
        ↓
Evidence Collection
        ↓
Containment
        ↓
Remediation
        ↓
Recovery
        ↓
Post-Incident Review
        ↓
Detection Tuning
```

Each simulated attack is treated as an individual investigation and documented using evidence from Microsoft Sentinel, Defender for Endpoint, Microsoft Entra ID, and endpoint telemetry.

The investigation process includes:

- Attack simulation
- Endpoint telemetry collection
- Identity telemetry analysis
- KQL threat hunting
- Process tree reconstruction
- Command-line analysis
- Network activity investigation
- Authentication analysis
- Indicator of Compromise (IoC) identification
- MITRE ATT&CK mapping
- Incident classification
- Containment
- Detection tuning
- False-positive analysis
- Incident reporting
- Lessons learned

---

# Project Objectives

The objective of this project was to:

- Build a cloud-hosted SOC monitoring environment
- Deploy Microsoft Sentinel
- Create and configure a Log Analytics Workspace
- Onboard a Windows endpoint into Microsoft Defender for Endpoint
- Integrate Defender for Endpoint with Microsoft Sentinel
- Ingest Microsoft Entra ID identity telemetry
- Validate endpoint and identity data ingestion
- Learn and apply Kusto Query Language (KQL)
- Develop custom Sentinel analytics rules
- Map detections to MITRE ATT&CK
- Simulate suspicious security activity in an isolated laboratory
- Generate Sentinel incidents
- Investigate incidents using Defender and Sentinel
- Perform endpoint containment
- Develop SOC incident response playbooks
- Tune detections to reduce false positives
- Document investigation findings
- Produce professional SOC-quality incident reports
- Demonstrate practical SIEM, EDR, threat hunting, and incident response skills

---

# Architecture

The laboratory was designed around a centralized SIEM and endpoint detection architecture.

```text
                         Microsoft Azure
                              │
                              │
                       Log Analytics
                          Workspace
                              │
                              ▼
                    Microsoft Sentinel
                              │
              ┌───────────────┼────────────────┐
              │               │                │
              ▼               ▼                ▼
        Analytics Rules   Incidents       Hunting / KQL
              │               │                │
              └───────────────┼────────────────┘
                              │
                              ▼
                    Microsoft Defender XDR
                              │
                    Defender for Endpoint
                              │
                              ▼
                       Windows 11 VM
                              │
                ┌─────────────┴─────────────┐
                │                           │
                ▼                           ▼
          Endpoint Events              Process Activity
                │                           │
                └─────────────┬─────────────┘
                              │
                              ▼
                     SOC Investigation
                              │
                              ▼
                   Incident Response
                              │
                 ┌────────────┼─────────────┐
                 ▼            ▼             ▼
             Containment   Recovery      Reporting
```

The architecture separates the major security functions:

### Endpoint

Microsoft Defender for Endpoint provides visibility into endpoint activity.

### Identity

Microsoft Entra ID provides authentication and identity-related telemetry.

### SIEM

Microsoft Sentinel provides centralized security monitoring, analytics, incident management, and investigation.

### Query Layer

KQL provides the investigation and detection language used to search security telemetry.

### Response Layer

Defender for Endpoint and Sentinel provide response capabilities such as device investigation and endpoint isolation.

### Documentation Layer

GitHub contains the detection rules, investigation reports, response playbooks, architecture documentation, and supporting evidence.

---

📷 **Screenshot Placeholder**

> Insert an architecture diagram showing the relationship between the Windows endpoint, Defender for Endpoint, Microsoft Entra ID, Log Analytics, Microsoft Sentinel, detection rules, incidents, and response actions.

Suggested filename:

```text
screenshots/architecture/sentinel-defender-architecture.png
```

---

# Security Architecture Principles

The project was designed around several fundamental SOC principles.

## 1. Centralized Visibility

Security telemetry should be collected into a central location where analysts can correlate activity.

Without centralized visibility, an analyst may need to manually investigate multiple systems.

---

## 2. Detection Before Response

The system should identify suspicious behaviour before containment actions are taken.

This allows analysts to establish whether activity is genuinely malicious.

---

## 3. Evidence-Based Investigation

Analysts should avoid assumptions.

Instead of:

> "The attacker definitely downloaded malware."

The investigation should state:

> "Network telemetry showed an outbound connection associated with the suspicious PowerShell process."

The second statement can be supported by evidence.

---

## 4. Detection Engineering

A detection is not finished when it generates an alert.

It must also be:

- Tested
- Investigated
- Tuned
- Validated
- Documented

---

## 5. Least-Privilege Response

Containment actions should be proportional to the incident.

A suspicious PowerShell event does not automatically mean an entire environment should be shut down.

---

## 6. Continuous Improvement

Every investigation should produce lessons that improve:

- Detection rules
- Alert quality
- Playbooks
- Analyst procedures
- Monitoring coverage

---

# Lab Environment

## Cloud Platform

Microsoft Azure

---

## Security Platform

Microsoft Security ecosystem:

- Microsoft Sentinel
- Microsoft Defender for Endpoint
- Microsoft Defender XDR
- Microsoft Entra ID
- Log Analytics

---

## Endpoint

Windows 11 virtual machine.

Example hostname:

```text
SOC-WIN11-ENDPOINT-01
```

---

## Test Account

A dedicated laboratory account should be used rather than a personal or production identity.

Example:

```text
soc-test-user
```

---

## Workspace

Example:

```text
SOC-Sentinel-Workspace
```

---

## Resource Group

Example:

```text
SOC-Sentinel-Lab-RG
```

---

📷 **Screenshot Placeholder**

> Insert Azure Resource Group showing the Sentinel laboratory resources.

---

📷 **Screenshot Placeholder**

> Insert Windows endpoint overview showing the laboratory VM.

---

# Lab Components

| Component | Purpose |
|---|---|
| Microsoft Sentinel | Cloud SIEM and incident management |
| Log Analytics Workspace | Central telemetry repository |
| Defender for Endpoint | Endpoint Detection and Response |
| Microsoft Defender XDR | Unified security investigation |
| Microsoft Entra ID | Identity and authentication telemetry |
| Windows 11 | Investigation endpoint |
| KQL | Detection and threat hunting |
| MITRE ATT&CK | Adversary behaviour classification |
| Atomic Red Team | Controlled attack simulation |
| GitHub | Documentation and portfolio repository |

---

# Why These Technologies Were Selected

## Microsoft Sentinel

Sentinel acts as the central SIEM.

It provides:

- Log collection
- Analytics rules
- Incident management
- Hunting
- Workbooks
- Automation
- Investigation capabilities

The purpose of Sentinel in this project is to demonstrate how a cloud SIEM can centralize security telemetry and support SOC operations.

---

## Microsoft Defender for Endpoint

Defender for Endpoint provides endpoint-level visibility.

It allows analysts to investigate:

- Processes
- Command lines
- Files
- Network connections
- Devices
- Alerts
- Device timelines
- Suspicious behaviour

This makes Defender the endpoint investigation layer of the architecture.

---

## Microsoft Entra ID

Entra ID provides identity telemetry.

This becomes particularly important when investigating:

- Failed authentication
- Password spraying
- Suspicious sign-ins
- Account abuse
- Privilege changes
- Identity compromise

---

## KQL

KQL is the investigation and detection language used by Microsoft security products.

The project uses KQL for both:

```text
Threat Hunting
```

and:

```text
Detection Engineering
```

---

## MITRE ATT&CK

MITRE ATT&CK provides a standardized vocabulary for describing adversary behaviour.

Instead of simply saying:

> "Suspicious PowerShell"

the detection can be mapped to:

```text
T1059.001
Command and Scripting Interpreter: PowerShell
```

This makes the detection easier to understand and compare against other security controls.

---

# Phase 1 — Azure Environment Preparation

The first phase involved preparing the Azure environment that would host Microsoft Sentinel.

---

# Step 1 — Create the Resource Group

Open the Azure Portal.

Navigate to:

```text
Resource Groups
```

Select:

```text
Create
```

Example:

```text
Resource Group:
SOC-Sentinel-Lab-RG
```

Choose the appropriate Azure region.

---

## Why?

A resource group provides a logical container for the resources used by the project.

This makes the environment easier to:

- Manage
- Monitor
- Delete
- Document
- Control for cost

---

📷 **Screenshot Placeholder**

> Insert Azure "Create Resource Group" screen.

---

📷 **Screenshot Placeholder**

> Insert completed Resource Group overview.

---

# Step 2 — Create the Log Analytics Workspace

Search Azure for:

```text
Log Analytics Workspaces
```

Create:

```text
SOC-Sentinel-Workspace
```

Place the workspace inside:

```text
SOC-Sentinel-Lab-RG
```

---

## Why?

Microsoft Sentinel requires a Log Analytics Workspace.

The workspace acts as the data platform where security logs can be stored and queried.

Conceptually:

```text
Data Sources
     ↓
Log Analytics
     ↓
KQL
     ↓
Sentinel
```

---

📷 **Screenshot Placeholder**

> Insert Log Analytics Workspace creation screen.

---

📷 **Screenshot Placeholder**

> Insert completed Log Analytics Workspace overview.

---

# Phase 2 — Deploy Microsoft Sentinel

Open:

```text
Microsoft Sentinel
```

Select:

```text
Create
```

Choose:

```text
SOC-Sentinel-Workspace
```

Deploy Sentinel.

---

## Why?

Sentinel provides the security operations layer on top of the Log Analytics environment.

After deployment, the workspace can be used for:

- Analytics rules
- Incidents
- Hunting
- Workbooks
- Data connectors
- Automation

---

📷 **Screenshot Placeholder**

> Insert Sentinel workspace overview showing the connected Log Analytics Workspace.

---

# Phase 3 — Prepare the Windows Endpoint

A Windows 11 endpoint was used as the laboratory endpoint.

The endpoint represents a normal employee workstation.

Example:

```text
SOC-WIN11-ENDPOINT-01
```

The endpoint should contain normal applications and activity so that the investigation environment resembles a real workstation rather than an empty VM.

---

# Why Use a Realistic Endpoint?

Attackers rarely interact with completely empty systems.

A realistic endpoint creates:

- Normal processes
- Normal network connections
- Normal user activity
- Normal authentication
- Background Windows activity

This creates the context required for detection engineering.

---

# Phase 4 — Onboard Windows to Defender for Endpoint

Open the Microsoft Defender portal.

Navigate to the endpoint onboarding section.

Select:

```text
Windows
```

Choose an appropriate onboarding method for the lab.

For a laboratory environment, the local script method can be used where available.

Download the onboarding package.

Transfer it to the Windows endpoint.

Run the onboarding process with administrative privileges.

---

📷 **Screenshot Placeholder**

> Insert Defender for Endpoint device onboarding configuration.

---

📷 **Screenshot Placeholder**

> Insert the onboarding script being executed on the Windows endpoint.

---

# Verify Endpoint Registration

After onboarding, verify that the endpoint appears in Defender.

The device should eventually show as active/healthy.

Example:

```text
SOC-WIN11-ENDPOINT-01
Status: Active
```

---

📷 **Screenshot Placeholder**

> Insert Defender portal showing the Windows endpoint as onboarded.

---

# Why Is Endpoint Onboarding Important?

Without onboarding:

```text
Windows
   │
   X
   │
Defender
```

Defender cannot provide meaningful endpoint telemetry.

After onboarding:

```text
Windows
   │
   │ Endpoint Sensor
   ▼
Defender for Endpoint
   │
   ▼
Security Investigation
```

The endpoint becomes a source of security telemetry.

---

# Phase 5 — Connect Defender to Sentinel

Inside Sentinel, open:

```text
Content Hub
```

Search for:

```text
Microsoft Defender
```

Install the appropriate Defender solution if required.

Then navigate to:

```text
Data Connectors
```

Locate the Microsoft Defender integration.

Configure the connector.

---

## Why?

Defender and Sentinel serve different operational purposes.

Defender provides detailed endpoint security visibility.

Sentinel provides centralized SIEM capabilities.

Connecting them allows an analyst to correlate endpoint activity with other security data.

---

📷 **Screenshot Placeholder**

> Insert Sentinel Content Hub showing the Defender solution.

---

📷 **Screenshot Placeholder**

> Insert Defender/Sentinel data connector configuration.

---

# Phase 6 — Connect Microsoft Entra ID

Configure the appropriate Microsoft Entra ID data connectors.

Relevant telemetry includes:

- Sign-in logs
- Audit logs
- Authentication activity
- Identity changes

---

## Why?

An attacker may compromise an identity without immediately compromising an endpoint.

For example:

```text
Password Spray
      ↓
Successful Login
      ↓
Compromised Account
      ↓
Endpoint Access
```

Identity telemetry therefore provides another layer of visibility.

---

📷 **Screenshot Placeholder**

> Insert Entra ID connector configuration.

---

# Phase 7 — Validate Data Ingestion

Before creating detections, verify that data actually exists.

This is a critical SOC engineering step.

Do not create analytics rules before validating the underlying telemetry.

---

# Test Defender Endpoint Data

Open:

```text
Sentinel → Logs
```

Run:

```kusto
DeviceEvents
| take 10
```

Then:

```kusto
DeviceProcessEvents
| take 10
```

Then:

```kusto
DeviceNetworkEvents
| take 10
```

---

## Why?

These queries establish whether endpoint telemetry is arriving.

If they return no results, the problem is probably with:

- Endpoint onboarding
- Connector configuration
- Permissions
- Data source configuration
- Workspace selection
- Ingestion delay

---

📷 **Screenshot Placeholder**

> Insert `DeviceProcessEvents` results.

---

📷 **Screenshot Placeholder**

> Insert `DeviceNetworkEvents` results.

---

# Validate Identity Telemetry

Run:

```kusto
SigninLogs
| take 10
```

And:

```kusto
AuditLogs
| take 10
```

---

📷 **Screenshot Placeholder**

> Insert Entra Sign-in Logs query results.

---

# Phase 8 — Learn KQL

KQL is fundamental to this project.

A basic query:

```kusto
DeviceProcessEvents
| where Timestamp > ago(24h)
| project
    Timestamp,
    DeviceName,
    AccountName,
    FileName,
    ProcessCommandLine
| order by Timestamp desc
```

---

# Understanding the Query

## Table

```kusto
DeviceProcessEvents
```

Specifies the dataset being searched.

---

## Where

```kusto
| where Timestamp > ago(24h)
```

Limits the search to the last 24 hours.

---

## Project

```kusto
| project DeviceName, FileName
```

Controls which fields are displayed.

---

## Order By

```kusto
| order by Timestamp desc
```

Displays newest events first.

---

# Why KQL Matters

A SOC analyst rarely investigates an incident by looking at every log manually.

Instead, the analyst asks questions.

For example:

> Which processes ran on the affected endpoint?

```kusto
DeviceProcessEvents
| where DeviceName == "SOC-WIN11-ENDPOINT-01"
| project Timestamp, FileName, ProcessCommandLine
| order by Timestamp desc
```

Another question:

> Which PowerShell commands executed?

```kusto
DeviceProcessEvents
| where FileName =~ "powershell.exe"
| project Timestamp, DeviceName, AccountName, ProcessCommandLine
| order by Timestamp desc
```

---

# Phase 9 — Detection Engineering

Three primary detection scenarios were developed.

```text
Detection 01
Suspicious PowerShell
        ↓
T1059.001

Detection 02
Credential Abuse
        ↓
T1110

Detection 03
Suspicious Tool Transfer
        ↓
T1105
```

---

# Detection 01 — Suspicious PowerShell

## MITRE ATT&CK

```text
T1059.001
Command and Scripting Interpreter: PowerShell
```

---

## Detection Objective

Detect PowerShell activity containing command-line characteristics frequently associated with suspicious execution.

---

## KQL

```kusto
DeviceProcessEvents
| where Timestamp > ago(1h)
| where FileName =~ "powershell.exe"
| where ProcessCommandLine has_any (
    "-enc",
    "-EncodedCommand",
    "Invoke-WebRequest",
    "IEX",
    "DownloadString",
    "Net.WebClient"
)
| project
    Timestamp,
    DeviceName,
    AccountName,
    InitiatingProcessFileName,
    FileName,
    ProcessCommandLine
| order by Timestamp desc
```

---

# Why This Detection Exists

PowerShell is a legitimate administrative tool.

Therefore:

```text
PowerShell ≠ Malware
```

The detection focuses on suspicious characteristics rather than simply alerting whenever PowerShell runs.

This is an important detection engineering principle.

---

# Investigation Questions

When the alert fires, the analyst should determine:

1. Who executed PowerShell?
2. Which endpoint was affected?
3. What was the command line?
4. What process started PowerShell?
5. Did PowerShell create child processes?
6. Did it communicate with the network?
7. Were files created?
8. Did persistence occur?
9. Was the activity authorized?
10. Does the behaviour correspond to a known ATT&CK technique?

---

📷 **Screenshot Placeholder**

> Insert Sentinel analytics rule configuration for the PowerShell detection.

---

📷 **Screenshot Placeholder**

> Insert Sentinel incident generated by the PowerShell detection.

---

# Detection 02 — Credential Abuse

## MITRE ATT&CK

```text
T1110
Brute Force
```

---

## Detection Objective

Identify repeated authentication failures that may indicate password spraying or brute-force behaviour.

---

## KQL

```kusto
SigninLogs
| where ResultType != 0
| summarize
    FailedAttempts = count()
    by UserPrincipalName,
       IPAddress,
       bin(TimeGenerated, 15m)
| where FailedAttempts >= 10
| order by FailedAttempts desc
```

---

# Investigation Questions

The analyst should determine:

- Which account was targeted?
- Which IP address generated the attempts?
- How many attempts occurred?
- Were multiple accounts targeted?
- Was there eventually a successful authentication?
- Is the source IP expected?
- Is the account privileged?
- Did the account access an endpoint after authentication?

---

📷 **Screenshot Placeholder**

> Insert KQL query showing repeated failed sign-ins.

---

📷 **Screenshot Placeholder**

> Insert Sentinel incident showing the credential abuse detection.

---

# Detection 03 — Suspicious Tool Transfer

## MITRE ATT&CK

```text
T1105
Ingress Tool Transfer
```

---

## Detection Objective

Identify suspicious outbound connections from endpoint processes that may indicate the retrieval of tools or payloads.

---

## Example KQL

```kusto
DeviceNetworkEvents
| where Timestamp > ago(1h)
| where RemoteUrl has_any (
    "pastebin",
    "raw.githubusercontent",
    "anonfiles"
)
| project
    Timestamp,
    DeviceName,
    InitiatingProcessFileName,
    InitiatingProcessCommandLine,
    RemoteUrl,
    RemoteIP
| order by Timestamp desc
```

---

## Important Detection Engineering Note

This detection should **not** automatically treat every connection to these services as malicious.

Legitimate developers and users may access these services.

Therefore the analyst must correlate:

```text
Destination
+
Process
+
Command Line
+
User
+
Device
+
Time
```

A PowerShell process accessing a suspicious destination is more interesting than a browser accessing a legitimate GitHub repository.

---

# Phase 10 — Simulated Attack Activity

The project uses controlled attack simulation to generate realistic telemetry.

Atomic Red Team can be used where appropriate within the isolated laboratory environment.

The simulations should be performed only against laboratory systems.

---

# Attack Scenario 1 — Suspicious PowerShell

The first scenario generates suspicious PowerShell telemetry.

The objective is not to deploy malware.

The objective is to generate telemetry that resembles suspicious PowerShell execution.

Expected telemetry includes:

```text
powershell.exe
        │
        ├── Command Line
        │
        ├── Parent Process
        │
        └── Child Process
```

---

📷 **Screenshot Placeholder**

> Insert the controlled PowerShell simulation being executed.

---

📷 **Screenshot Placeholder**

> Insert Defender device timeline showing the generated activity.

---

# Attack Scenario 2 — Credential Abuse

A dedicated test identity is used to generate controlled authentication failures.

The goal is to produce:

```text
Failed Login
Failed Login
Failed Login
Failed Login
...
```

The Sentinel detection should eventually identify the abnormal pattern.

---

📷 **Screenshot Placeholder**

> Insert Entra ID sign-in logs showing the simulated failed authentication activity.

---

# Attack Scenario 3 — Suspicious Download / Tool Transfer

A harmless test file can be transferred within the controlled environment to generate network and process telemetry.

The investigation focuses on:

- Process responsible
- Destination
- Command line
- File creation
- Network connection
- User context

---

📷 **Screenshot Placeholder**

> Insert Defender network activity associated with the simulated transfer.

---

# Phase 11 — Incident Investigation Methodology

Every incident follows the same methodology.

```text
Alert Generated
      ↓
Initial Triage
      ↓
Validate Alert
      ↓
Identify User
      ↓
Identify Endpoint
      ↓
Review Timeline
      ↓
Review Process Tree
      ↓
Review Command Line
      ↓
Review Network Activity
      ↓
Identify IoCs
      ↓
Map MITRE ATT&CK
      ↓
Determine Scope
      ↓
Contain
      ↓
Remediate
      ↓
Recover
      ↓
Document
      ↓
Tune Detection
```

---

# Incident Classification

Each incident should be assigned a severity.

Example:

| Severity | Meaning |
|---|---|
| Informational | Expected activity |
| Low | Suspicious but low risk |
| Medium | Confirmed suspicious activity |
| High | Confirmed malicious activity |
| Critical | Significant compromise or widespread impact |

Severity should be based on evidence and business impact rather than the alert name alone.

---

# Incident Report — INC-001

# Suspicious PowerShell Investigation

---

## Incident Summary

| Field | Value |
|---|---|
| Incident ID | INC-001 |
| Detection | Suspicious PowerShell |
| MITRE ATT&CK | T1059.001 |
| Severity | High |
| Detection Source | Microsoft Sentinel |
| Endpoint | SOC-WIN11-ENDPOINT-01 |
| Investigation Platform | Defender for Endpoint |
| Status | Investigating |

---

# Investigation Objective

Determine whether the PowerShell activity was:

- Legitimate administration
- User activity
- Security testing
- Malicious execution

The investigation should determine:

- Who executed PowerShell
- What command was executed
- Which process launched it
- Which child processes appeared
- Whether files were created
- Whether network communication occurred
- Whether persistence occurred
- Whether credential access occurred
- Whether additional endpoints were affected

---

# Step 1 — Validate the Alert

Open the Sentinel incident.

Review:

- Alert name
- Entity information
- Device
- User
- Timestamp
- Command line
- Related alerts

The first objective is to confirm that the alert represents actual activity.

---

📷 **Screenshot Placeholder**

> Insert Sentinel incident overview.

---

# Step 2 — Identify the Endpoint

Determine the affected endpoint.

Example:

```text
SOC-WIN11-ENDPOINT-01
```

Open the device in Defender for Endpoint.

---

# Step 3 — Review the Device Timeline

The device timeline provides chronological context.

Look for:

```text
Process Creation
File Creation
Network Activity
Registry Activity
Security Alerts
```

---

📷 **Screenshot Placeholder**

> Insert Defender for Endpoint device timeline.

---

# Step 4 — Review the Process Tree

The process tree is one of the most important investigative sources.

Example:

```text
explorer.exe
      │
      ▼
cmd.exe
      │
      ▼
powershell.exe
      │
      ├── whoami.exe
      │
      └── hostname.exe
```

The analyst should ask:

> Why did this parent process start this child process?

This question frequently reveals malicious execution chains.

---

📷 **Screenshot Placeholder**

> Insert Defender process tree showing the suspicious PowerShell execution.

---

# Step 5 — Analyse Command Line

Example:

```text
powershell.exe -EncodedCommand <BASE64>
```

The analyst should determine:

- Is encoding present?
- Is obfuscation present?
- Is download functionality present?
- Is execution policy modification present?
- Is a suspicious destination present?
- Is the command associated with an approved administrative task?

---

📷 **Screenshot Placeholder**

> Insert Defender process details showing the complete command line.

---

# Step 6 — Investigate Network Activity

Use:

```kusto
DeviceNetworkEvents
| where DeviceName == "SOC-WIN11-ENDPOINT-01"
| where InitiatingProcessFileName =~ "powershell.exe"
| project
    Timestamp,
    RemoteIP,
    RemotePort,
    RemoteUrl,
    InitiatingProcessCommandLine
| order by Timestamp desc
```

---

## Investigation Questions

- Did PowerShell communicate externally?
- Where did it connect?
- Was DNS involved?
- Was HTTPS used?
- Was the destination expected?
- Did the process download content?

---

📷 **Screenshot Placeholder**

> Insert network investigation results.

---

# Step 7 — Investigate File Activity

Search for files created around the incident timestamp.

```kusto
DeviceFileEvents
| where DeviceName == "SOC-WIN11-ENDPOINT-01"
| where Timestamp between (
    datetime(2026-01-01T10:00:00Z)
    ..
    datetime(2026-01-01T10:30:00Z)
)
| project
    Timestamp,
    ActionType,
    FileName,
    FolderPath,
    InitiatingProcessFileName
| order by Timestamp asc
```

The timestamps above are examples and should be replaced with the actual investigation timeframe.

---

# Step 8 — Investigate Persistence

Look for:

- Scheduled tasks
- Registry Run keys
- Services
- Startup folders
- New accounts
- Suspicious scripts

---

# Step 9 — Determine Scope

The analyst must determine whether the incident was isolated.

Search for:

```text
Same user
Same command
Same hash
Same destination
Same process
Same IoC
```

across other devices.

---

# Step 10 — Determine Verdict

Possible verdicts:

```text
True Positive
False Positive
Benign Positive
Suspicious / Inconclusive
```

Example:

```text
Verdict:
True Positive — Suspicious PowerShell

Confidence:
High

Reason:
Encoded PowerShell was executed by an unexpected parent process and generated outbound network activity inconsistent with normal user behaviour.
```

---

# Phase 12 — Endpoint Containment

If the investigation confirms compromise, the endpoint can be isolated through Defender for Endpoint.

The purpose of isolation is to prevent the compromised endpoint from communicating with other systems while preserving the ability to investigate and remediate it.

Conceptually:

```text
Compromised Endpoint
        │
        X
        │
Corporate Network
```

---

## When to Isolate

Isolation may be appropriate when:

- Malware is executing
- Credential theft is suspected
- Command-and-control activity is observed
- Lateral movement is suspected
- Ransomware activity is detected
- The endpoint is actively compromised

---

## When Not to Immediately Isolate

Avoid automatic isolation when:

- Activity is clearly legitimate
- The alert is a known false positive
- The endpoint is business-critical and the risk is low
- Additional evidence is required

This demonstrates the importance of balancing security risk with business impact.

---

📷 **Screenshot Placeholder**

> Insert Defender for Endpoint device response menu showing the isolation option.

---

📷 **Screenshot Placeholder**

> Insert endpoint status after isolation.

---

# Phase 13 — Identity Containment

If credential compromise is suspected, investigate the affected identity.

Potential response actions include:

- Revoke sessions
- Reset credentials
- Require MFA
- Disable the account where appropriate
- Review sign-in history
- Review privilege changes
- Search for additional authentication activity

---

# Phase 14 — Recovery

Recovery should not simply mean:

> "The alert disappeared."

The endpoint must be validated.

Recovery checklist:

- Malicious activity stopped
- Persistence removed
- Credentials protected
- Endpoint healthy
- Security tooling operational
- Network activity normal
- No related alerts
- Monitoring continued

---

# Phase 15 — Detection Tuning

Detection engineering is an iterative process.

The initial PowerShell rule may produce legitimate alerts.

Example:

```text
Alert:
PowerShell -EncodedCommand

Result:
Legitimate IT automation
```

Instead of simply disabling the rule, investigate why it triggered.

---

# Tuning Strategy

### Step 1

Identify the legitimate process.

### Step 2

Identify the account.

### Step 3

Identify the endpoint.

### Step 4

Determine whether the activity is predictable.

### Step 5

Create a narrow exclusion if appropriate.

### Step 6

Retest.

### Step 7

Confirm malicious behaviour is still detected.

---

# Example Tuning

Instead of:

```kusto
where FileName == "powershell.exe"
```

use additional context:

```kusto
where FileName =~ "powershell.exe"
| where ProcessCommandLine has_any (
    "-EncodedCommand",
    "-enc"
)
| where InitiatingProcessFileName !in~ (
    "approved-management-tool.exe"
)
```

The exact exclusion should be based on evidence from the environment.

---

# Why False-Positive Tuning Matters

An SOC analyst can receive hundreds or thousands of alerts.

If most alerts are irrelevant:

```text
High Alert Volume
       ↓
Analyst Fatigue
       ↓
Missed True Positive
       ↓
Security Incident
```

Good detection engineering attempts to maximize:

```text
Signal
```

while minimizing:

```text
Noise
```

---

# Phase 16 — SOC Incident Response Playbooks

Three primary playbooks were created.

---

# Playbook 01 — Suspicious PowerShell

## Trigger

Sentinel analytics rule:

```text
Suspicious PowerShell Execution
```

## Triage

1. Identify user.
2. Identify endpoint.
3. Review command line.
4. Review parent process.
5. Review child processes.
6. Review network connections.
7. Review file creation.
8. Search for persistence.

## Containment

If malicious:

```text
Isolate endpoint
```

If identity compromise is suspected:

```text
Protect account
```

## Escalation

Escalate when:

- Malware is confirmed
- Credential theft is suspected
- Multiple endpoints are involved
- Persistence is identified
- Lateral movement is suspected

## Recovery

- Remove malicious activity
- Validate endpoint health
- Monitor endpoint
- Review credentials
- Close incident only after validation

---

📷 **Screenshot Placeholder**

> Insert the completed Suspicious PowerShell response playbook.

---

# Playbook 02 — Credential Abuse

## Trigger

Repeated authentication failures.

## Triage

Determine:

- Target account
- Source IP
- Number of attempts
- Time period
- Number of targeted accounts
- Successful authentication following failures

## Containment

Depending on severity:

- Reset password
- Revoke sessions
- Disable account
- Require MFA
- Block suspicious source

## Escalation

Escalate when:

- Successful compromise occurred
- Privileged account was targeted
- Multiple accounts were attacked
- Lateral movement occurred

---

📷 **Screenshot Placeholder**

> Insert Credential Abuse response playbook.

---

# Playbook 03 — Endpoint Compromise

## Trigger

Confirmed malicious endpoint activity.

## Triage

- Identify device
- Identify user
- Determine initial execution
- Review process tree
- Review network activity
- Identify IoCs
- Search for additional affected devices

## Containment

```text
Isolate Endpoint
```

## Investigation

Determine:

```text
Initial Access
     ↓
Execution
     ↓
Persistence
     ↓
Privilege Escalation
     ↓
Credential Access
     ↓
Discovery
     ↓
Lateral Movement
     ↓
Impact
```

Not every incident will contain all phases.

---

# Phase 17 — Incident Documentation

Each investigation should produce an incident report.

Recommended structure:

```text
Incident ID

Executive Summary

Detection

Affected Assets

Timeline

Initial Findings

Technical Investigation

IoCs

MITRE ATT&CK Mapping

Containment

Eradication

Recovery

Root Cause

Detection Gaps

False Positives

Recommendations

Lessons Learned

Final Verdict
```

---

# Incident Timeline

Example:

| Time | Event |
|---|---|
| 10:01 | Suspicious PowerShell executed |
| 10:02 | Network connection observed |
| 10:03 | Sentinel analytics rule triggered |
| 10:04 | Incident created |
| 10:06 | Analyst began investigation |
| 10:10 | Endpoint isolated |
| 10:20 | Evidence collected |
| 10:35 | Malicious activity removed |
| 10:45 | Endpoint validated |
| 11:00 | Monitoring continued |
| 11:30 | Incident closed |

Actual timestamps should be replaced with those recorded during the laboratory exercise.

---

# Phase 18 — IoC Collection

Indicators collected during investigations may include:

```text
IP Addresses
Domains
URLs
File Hashes
File Names
File Paths
Process Names
Command Lines
Registry Keys
User Accounts
Hostnames
Scheduled Tasks
```

---

# IoC Documentation

Example:

| Indicator | Type | Source | Confidence |
|---|---|---|---|
| powershell.exe | Process | Defender | High |
| Suspicious URL | URL | Network telemetry | High |
| Test account | Identity | Entra ID | High |
| Suspicious command line | Command | Process telemetry | High |

---

# Phase 19 — MITRE ATT&CK Mapping

The project maps detections and investigations to MITRE ATT&CK.

| Technique | Description | Detection |
|---|---|---|
| T1059.001 | PowerShell | Suspicious PowerShell |
| T1110 | Brute Force | Credential Abuse |
| T1105 | Ingress Tool Transfer | Suspicious Download |
| T1087 | Account Discovery | Endpoint Investigation |
| T1057 | Process Discovery | Process Investigation |

The final mapping should contain only techniques actually demonstrated or investigated in the lab.

---

📷 **Screenshot Placeholder**

> Insert MITRE ATT&CK Navigator heatmap showing the techniques covered by the project.

---

# Detection Coverage

The project should maintain a detection coverage matrix.

| Detection | Data Source | MITRE | Status |
|---|---|---|---|
| Suspicious PowerShell | Defender | T1059.001 | Tested |
| Credential Abuse | Entra ID | T1110 | Tested |
| Tool Transfer | Defender Network | T1105 | Tested |
| Process Discovery | Defender | T1057 | Investigated |
| Account Discovery | Defender | T1087 | Investigated |

---

# Phase 20 — Threat Hunting

Threat hunting goes beyond waiting for alerts.

Instead of asking:

> "Did Sentinel alert?"

the analyst asks:

> "Does this behaviour exist anywhere in the environment?"

---

# Hunt Query — PowerShell

```kusto
DeviceProcessEvents
| where Timestamp > ago(7d)
| where FileName =~ "powershell.exe"
| summarize
    Count=count()
    by DeviceName,
       AccountName
| order by Count desc
```

---

# Hunt Query — Encoded PowerShell

```kusto
DeviceProcessEvents
| where Timestamp > ago(7d)
| where FileName =~ "powershell.exe"
| where ProcessCommandLine has_any (
    "-enc",
    "-EncodedCommand"
)
| project
    Timestamp,
    DeviceName,
    AccountName,
    ProcessCommandLine
| order by Timestamp desc
```

---

# Hunt Query — Failed Authentication

```kusto
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != 0
| summarize
    FailedAttempts=count()
    by UserPrincipalName,
       IPAddress
| order by FailedAttempts desc
```

---

📷 **Screenshot Placeholder**

> Insert Sentinel Hunting page showing a completed threat hunt.

---

# Phase 21 — Detection Validation

Each detection should be tested against both malicious and legitimate activity.

Example:

```text
Test Case
   │
   ├── Expected detection
   │
   ├── Actual detection
   │
   ├── False Positive?
   │
   ├── Investigation Result
   │
   └── Tuning Required?
```

---

# Detection Test Matrix

| Detection | Simulation | Triggered | False Positive | Tuned |
|---|---|---:|---:|---:|
| PowerShell | Controlled execution | Yes | No | Yes |
| Credential Abuse | Failed authentication | Yes | No | Yes |
| Tool Transfer | Test transfer | Yes | Possible | Yes |

---

# Phase 22 — Incident Response Metrics

The project can also demonstrate basic SOC metrics.

## Mean Time to Detect

```text
MTTD =
Detection Time - Attack Time
```

Example:

```text
Attack:
10:01

Detection:
10:03

MTTD:
2 minutes
```

---

## Mean Time to Respond

```text
MTTR =
Containment Time - Detection Time
```

Example:

```text
Detection:
10:03

Containment:
10:10

MTTR:
7 minutes
```

These metrics help demonstrate how quickly the detection and response process operates.

---

# Phase 23 — Detection Improvement

The project follows a continuous improvement cycle.

```text
Attack Simulation
       ↓
Telemetry
       ↓
Detection
       ↓
Alert
       ↓
Investigation
       ↓
False Positive Analysis
       ↓
Detection Tuning
       ↓
Retest
       ↓
Improved Detection
```

---

# Detection Gap Analysis

The project identified potential areas for improvement.

Examples include:

- Additional endpoint telemetry
- Improved PowerShell logging
- Better identity correlation
- More network visibility
- Additional detection rules
- More granular exclusions
- Better alert prioritization
- Automated enrichment
- Automated response
- Additional ATT&CK coverage

---

# Example Detection Gap

Current detection:

```text
PowerShell -EncodedCommand
```

Potential weakness:

An attacker could avoid the exact string.

Improvement:

Correlate:

```text
PowerShell
+
Obfuscation
+
Unusual Parent Process
+
Network Connection
+
File Creation
```

This produces a higher-confidence detection.

---

# Phase 24 — Automation Opportunities

The project can be expanded using Sentinel automation.

Possible automation:

```text
Alert
 ↓
Enrichment
 ↓
Determine Severity
 ↓
Create Incident
 ↓
Notify Analyst
 ↓
Optional Containment
 ↓
Create Ticket
```

Automation should be carefully designed.

Not every alert should automatically isolate a device.

---

# Phase 25 — Recommended SOC Escalation Model

```text
                    Alert
                      │
                      ▼
                 Tier 1 Triage
                      │
             ┌────────┴────────┐
             │                 │
          Benign            Suspicious
             │                 │
          Close             Tier 2
                               │
                        Investigation
                               │
                  ┌────────────┴───────────┐
                  │                        │
             Contained                 Widespread
                  │                        │
               Recover                 Tier 3 / IR
```

---

# Tier 1 Analyst Responsibilities

- Validate alerts
- Identify affected user
- Identify endpoint
- Determine severity
- Gather initial evidence
- Escalate suspicious incidents

---

# Tier 2 Analyst Responsibilities

- Perform deeper investigation
- Reconstruct process trees
- Conduct threat hunting
- Analyse network activity
- Identify persistence
- Determine scope
- Recommend containment

---

# Tier 3 / Incident Response

- Major compromise
- Widespread malware
- Credential theft
- Lateral movement
- Ransomware
- Data exfiltration
- Advanced persistence

---

# Phase 26 — Final Incident Report

Each completed investigation should answer five major questions:

## What happened?

Describe the activity.

## How did it happen?

Explain the execution chain.

## What was affected?

Identify users, endpoints, and systems.

## What did we do?

Document containment and remediation.

## How do we prevent recurrence?

Document detection and security improvements.

---

# Analyst Assessment

The final assessment should be evidence-based.

Example:

> The investigation confirmed suspicious PowerShell execution on the laboratory endpoint. Process telemetry identified PowerShell as the executing process and provided the associated command line and parent process context. Additional endpoint and network telemetry was reviewed to determine whether the activity resulted in persistence, network communication, or additional endpoint compromise. The activity was classified based on the available evidence and the corresponding MITRE ATT&CK technique was documented.

The wording should be adjusted to reflect the actual evidence observed during the investigation.

---

# Lessons Learned

The project demonstrates several important SOC principles.

## 1. Telemetry Is the Foundation

A detection is only as useful as the telemetry behind it.

---

## 2. Alerts Are Starting Points

An alert does not automatically mean compromise.

It starts an investigation.

---

## 3. Process Trees Matter

Understanding:

```text
Parent
  ↓
Child
  ↓
Grandchild
```

often reveals how suspicious activity began.

---

## 4. Context Matters

A PowerShell command may be:

```text
Normal administration
```

or:

```text
Malicious execution
```

The difference is context.

---

## 5. KQL Is a Core SOC Skill

KQL allows analysts to transform millions of events into meaningful evidence.

---

## 6. Detection Engineering Is Iterative

The first version of a detection is rarely the final version.

---

## 7. False Positives Must Be Investigated

A false positive is not simply an annoyance.

It provides information about how the environment behaves.

---

## 8. Containment Must Be Deliberate

Isolation can stop an attack, but it can also disrupt business operations.

The response must therefore consider:

```text
Security Risk
+
Business Impact
```

---

# Project Results

The completed project demonstrates the ability to:

- Deploy a cloud SIEM environment
- Configure Microsoft Sentinel
- Configure Defender for Endpoint
- Integrate endpoint and identity telemetry
- Validate security data ingestion
- Write KQL
- Develop custom detections
- Map detections to MITRE ATT&CK
- Generate incidents
- Investigate endpoint activity
- Investigate authentication activity
- Perform threat hunting
- Execute containment
- Develop incident response playbooks
- Tune detections
- Document false positives
- Produce SOC-quality investigation reports

---

# Repository Structure

```text
Microsoft-Sentinel-Incident-Response-Playbook/
│
├── README.md
│
├── architecture/
│   ├── sentinel-defender-architecture.png
│   └── data-flow-diagram.png
│
├── detections/
│   ├── suspicious-powershell.kql
│   ├── credential-abuse.kql
│   └── suspicious-tool-transfer.kql
│
├── playbooks/
│   ├── suspicious-powershell.md
│   ├── credential-abuse.md
│   └── endpoint-compromise.md
│
├── incident-reports/
│   ├── INC-001-Suspicious-PowerShell.md
│   ├── INC-002-Credential-Abuse.md
│   └── INC-003-Endpoint-Compromise.md
│
├── hunt-queries/
│   ├── powershell-hunting.kql
│   ├── authentication-hunting.kql
│   └── network-hunting.kql
│
├── mitre/
│   ├── attack-mapping.md
│   └── attack-navigator.json
│
├── iocs/
│   └── investigation-iocs.csv
│
├── screenshots/
│   ├── architecture/
│   ├── azure/
│   ├── sentinel/
│   ├── defender/
│   ├── entra/
│   ├── detections/
│   ├── incidents/
│   └── investigations/
│
├── documentation/
│   ├── environment-setup.md
│   ├── detection-engineering.md
│   ├── investigation-methodology.md
│   └── tuning-decisions.md
│
└── LICENSE
```

---

# Screenshot Directory

Recommended screenshot organization:

```text
screenshots/
│
├── architecture/
│   └── sentinel-defender-architecture.png
│
├── azure/
│   ├── resource-group.png
│   ├── log-analytics-workspace.png
│   └── sentinel-overview.png
│
├── defender/
│   ├── device-onboarding.png
│   ├── device-inventory.png
│   ├── device-timeline.png
│   └── process-tree.png
│
├── entra/
│   ├── signin-logs.png
│   └── audit-logs.png
│
├── detections/
│   ├── powershell-rule.png
│   ├── credential-rule.png
│   └── tool-transfer-rule.png
│
├── incidents/
│   ├── powershell-incident.png
│   ├── credential-incident.png
│   └── endpoint-incident.png
│
└── investigations/
    ├── process-investigation.png
    ├── network-investigation.png
    └── timeline-investigation.png
```

---

# Recommended GitHub Screenshots

The most valuable screenshots for a portfolio are:

### 1. Architecture

Shows that you understand the entire system.

### 2. Sentinel Overview

Demonstrates practical Sentinel experience.

### 3. Data Connectors

Shows integration knowledge.

### 4. Defender Endpoint

Shows EDR experience.

### 5. KQL Detection

Shows detection engineering.

### 6. Generated Incident

Shows that your detection actually worked.

### 7. Process Tree

Shows investigation capability.

### 8. Device Timeline

Shows endpoint investigation.

### 9. Entra Sign-In Logs

Shows identity investigation.

### 10. Containment

Shows practical incident response.

### 11. MITRE ATT&CK Mapping

Shows structured threat analysis.

### 12. Final Investigation Report

Shows professional documentation.

---

# Evidence Handling

Screenshots should not expose sensitive information.

Before publishing screenshots:

Remove or obscure:

- Real usernames
- Personal email addresses
- Subscription IDs
- Tenant IDs
- IP addresses where sensitive
- Access tokens
- API keys
- Secrets
- Authentication information

Use laboratory accounts and simulated data whenever possible.

---

# Security Considerations

This project should remain isolated from production environments.

Attack simulations should only be performed against:

```text
Owned laboratory systems
```

Do not execute attack simulations against:

- Production endpoints
- Employer systems
- Third-party infrastructure
- Public websites
- Systems without authorization

The purpose of the simulations is defensive research and detection engineering.

---

# Future Improvements

Potential future improvements include:

- Microsoft Sentinel automation rules
- Logic Apps SOAR workflows
- Automated incident enrichment
- Threat intelligence integration
- Automated IoC enrichment
- Automated ticket creation
- Additional Defender telemetry
- More Entra identity detections
- Additional MITRE ATT&CK coverage
- Sigma rule development
- Custom Sentinel Workbooks
- Executive SOC dashboard
- Advanced hunting queries
- Detection-as-code workflow
- GitHub CI/CD for detection rules
- Automated detection testing
- Additional endpoint simulations
- Multi-endpoint environment
- Simulated lateral movement
- Simulated ransomware behaviour
- Simulated credential theft
- Additional incident response scenarios

---

# Possible Advanced Architecture

The project can eventually be expanded into:

```text
                    Attack Simulation
                           │
                           ▼
                     Windows Endpoints
                           │
                           ▼
                 Defender for Endpoint
                           │
                           ▼
                    Defender XDR
                           │
            ┌──────────────┴──────────────┐
            │                             │
            ▼                             ▼
       Endpoint Data                Identity Data
            │                             │
            └──────────────┬──────────────┘
                           ▼
                  Microsoft Sentinel
                           │
                  ┌────────┴────────┐
                  │                 │
                  ▼                 ▼
              Analytics          Hunting
                  │
                  ▼
               Incident
                  │
                  ▼
              Automation
                  │
        ┌─────────┼──────────┐
        ▼         ▼          ▼
     Enrich    Contain    Notify
        │         │          │
        └─────────┼──────────┘
                  ▼
            Incident Report
                  │
                  ▼
            Lessons Learned
                  │
                  ▼
           Detection Tuning
```

---

# Final Project Deliverables

The completed project should contain:

- [ ] Azure Sentinel environment
- [ ] Log Analytics Workspace
- [ ] Windows endpoint
- [ ] Defender for Endpoint onboarding
- [ ] Microsoft Entra telemetry
- [ ] Defender/Sentinel integration
- [ ] Validated data ingestion
- [ ] Three custom KQL detections
- [ ] MITRE ATT&CK mappings
- [ ] Controlled attack simulations
- [ ] Sentinel incidents
- [ ] Defender investigations
- [ ] Threat hunting queries
- [ ] Endpoint containment demonstration
- [ ] Three incident response playbooks
- [ ] Incident investigation reports
- [ ] Detection tuning documentation
- [ ] False-positive analysis
- [ ] IoC documentation
- [ ] MITRE ATT&CK coverage
- [ ] Architecture diagram
- [ ] Screenshots
- [ ] GitHub repository
- [ ] Final lessons learned

---

# Final SOC Workflow

The completed project demonstrates the following operational workflow:

```text
                 SECURITY EVENT
                       │
                       ▼
              TELEMETRY COLLECTION
                       │
                       ▼
                SENTINEL ANALYTICS
                       │
                       ▼
                     ALERT
                       │
                       ▼
                   INCIDENT
                       │
                       ▼
                 TIER 1 TRIAGE
                       │
                       ▼
                VALIDATE ACTIVITY
                       │
                       ▼
                DEFENDER INVESTIGATION
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
       Process       Network      Identity
       Analysis     Analysis     Analysis
          │            │            │
          └────────────┼────────────┘
                       ▼
                 DETERMINE SCOPE
                       │
                       ▼
                  MITRE MAPPING
                       │
                       ▼
                   CONTAINMENT
                       │
                       ▼
                   REMEDIATION
                       │
                       ▼
                    RECOVERY
                       │
                       ▼
                 INCIDENT REPORT
                       │
                       ▼
                 LESSONS LEARNED
                       │
                       ▼
                DETECTION TUNING
                       │
                       ▼
                 RETEST / IMPROVE
```

---

# Conclusion

This project demonstrates an end-to-end approach to Security Operations Centre monitoring and incident response using Microsoft security technologies.

The primary objective was not simply to deploy Microsoft Sentinel or create several KQL queries. The project was designed to demonstrate the complete operational lifecycle of a security incident:

```text
Detect
   ↓
Investigate
   ↓
Understand
   ↓
Contain
   ↓
Remediate
   ↓
Recover
   ↓
Document
   ↓
Improve
```

Microsoft Sentinel provides the centralized SIEM capability, Defender for Endpoint provides endpoint investigation and response, Microsoft Entra ID provides identity telemetry, KQL provides the analytical capability, and MITRE ATT&CK provides a standardized framework for describing adversary behaviour.

The resulting environment demonstrates practical experience in:

- SIEM administration
- EDR investigation
- KQL
- Detection engineering
- Threat hunting
- Incident response
- Endpoint containment
- Identity investigation
- MITRE ATT&CK
- False-positive tuning
- SOC documentation

The most important lesson from the project is that effective security operations are not based on individual alerts. They depend on the combination of **quality telemetry, meaningful detections, structured investigation, appropriate response, and continuous improvement**.

---

# Disclaimer

This project was performed exclusively within an isolated laboratory environment for defensive security research, detection engineering, incident response training, and educational purposes.

All simulated security activity should be performed only against systems owned or explicitly authorized for testing.

No production systems, unauthorized endpoints, third-party infrastructure, or systems belonging to other individuals were intentionally targeted.

All credentials, identities, network addresses, and security telemetry published in the repository should be laboratory-generated or appropriately sanitized before publication.
