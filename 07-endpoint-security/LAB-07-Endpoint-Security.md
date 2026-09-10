# Lab 07 — Endpoint Security

## Objective

Deploy and validate a comprehensive endpoint security baseline on a Windows 11 Enterprise device using Intune Endpoint Security policies, including antivirus, firewall, disk encryption, and attack surface reduction.

## Environment

| Component | Configuration |
|---|---|
| Identity | Microsoft Entra ID |
| Device Management | Microsoft Intune |
| Operating System | Windows 11 Enterprise 25H2 |
| Device | DESKTOP-48ASFDI |
| User | Intune Test User |
| Assignment Group | INTUNE-Pilot-Users |
| Management | Microsoft Intune |
| Ownership | Corporate |

## Configuration

Endpoint security policies were created using the Intune **Endpoint Security** node.

### Policies

**7A — Microsoft Defender Antivirus**

**Name:**

`LAB-ENDPOINT-07A-Defender-Antivirus`

**Platform:**

Windows 10 and later

**Profile type:**

Antivirus

**7B — Windows Firewall**

**Name:**

`LAB-ENDPOINT-07B-Windows-Firewall`

**Platform:**

Windows 10 and later

**Profile type:**

Firewall

**7C — Firewall Rule (Allow RDP)**

**Name:**

`LAB-ENDPOINT-07C-Firewall-Rule-RDP`

**Platform:**

Windows 10 and later

**Profile type:**

Firewall Rules

**7D — BitLocker Drive Encryption**

**Name:**

`LAB-ENDPOINT-07D-BitLocker`

**Platform:**

Windows 10 and later

**Profile type:**

Disk Encryption

**7E — Attack Surface Reduction**

**Name:**

`LAB-ENDPOINT-07E-ASR`

**Platform:**

Windows 10 and later

**Profile type:**

Attack Surface Reduction

### Assignment

All policies were assigned using an **Included group**:

`INTUNE-Pilot-Users`

No excluded groups were configured.

## Deployment Process

The deployment followed this workflow:

```text
Create Endpoint Security Policy
            |
            v
Configure Settings
            |
            v
Assign to INTUNE-Pilot-Users
            |
            v
Device/User Targeted
            |
            v
Windows Device Checks In
            |
            v
Policy Processed
            |
            v
Deployment Result
