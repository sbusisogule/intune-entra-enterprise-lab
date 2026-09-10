# Lab 08 — Windows Autopilot

## Objective

Register a Windows 11 Enterprise device with Windows Autopilot, deploy a user-driven Autopilot profile, and enroll the device into Microsoft Intune with Microsoft Entra join.

## Environment

| Component | Configuration |
|---|---|
| Identity | Microsoft Entra ID |
| Device Management | Microsoft Intune |
| Operating System | Windows 11 Enterprise 25H2 |
| Device | Windows 11 Enterprise VM |
| User | Intune Test User |
| Assignment Group | INTUNE-Pilot-Users |
| Management | Microsoft Intune |
| Ownership | Corporate |

## Configuration

Windows Autopilot was configured using the Intune **Windows enrollment** node.

### Autopilot Device Registration

The device hardware hash was captured using the `Get-WindowsAutopilotInfo` PowerShell script and imported into Intune.

**Hardware hash file:**

`AutopilotHWID.csv`

### Deployment Profile

**Name:**

`AutopilotUserDrivenProduction`

**Platform:**

Windows PC

**Deployment mode:**

User-Driven

**Join type:**

Microsoft Entra joined

**Device name template:**

`AUTOPILOT-%RAND:5%`

### Assignment

The profile was assigned using an **Included group**:

`INTUNE-Pilot-Users`

No excluded groups were configured.

## Deployment Process

The deployment followed this workflow:

```text
Capture Hardware Hash
            |
            v
Import into Intune
            |
            v
Create Autopilot Profile
            |
            v
Assign to INTUNE-Pilot-Users
            |
            v
Assign Profile to Device
            |
            v
Reset Windows Device
            |
            v
Autopilot OOBE
            |
            v
Entra Join + Intune Enrollment
