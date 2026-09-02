# Lab 3 — Microsoft Entra Conditional Access

## Objective

Configure a Microsoft Entra Conditional Access policy that requires a device to be marked as compliant before access is granted.

The purpose of this lab is to demonstrate how Microsoft Intune compliance status integrates with Microsoft Entra Conditional Access.

## Lab Environment

| Component                 | Configuration                        |
| ------------------------- | ------------------------------------ |
| Microsoft Entra tenant    | Existing lab tenant                  |
| Test user                 | `Intune Test User`                   |
| Pilot group               | `INTUNE-Pilot-Users`                 |
| Windows device            | `DESKTOP-48ASFDI`                    |
| Device management         | Microsoft Intune                     |
| Device join               | Microsoft Entra joined               |
| Compliance policy         | `LAB-WIN-02-Basic-Compliance`        |
| Conditional Access policy | `LAB-CA-01-Require-Compliant-Device` |
| License                   | Microsoft 365 Business Premium       |

## Conditional Access Policy Configuration

### Policy Name

`LAB-CA-01-Require-Compliant-Device`

### Policy State

**Report-only**

The policy was intentionally configured in Report-only mode so that its effect could be tested without blocking the test user.

### Users, Agents or Workload Identities

The policy targets the lab test user.

* Included: 1 user
* Excluded: 0 users
* Groups excluded: None

### Target Resources

**All resources**

No individual application was selected.

### Grant Access Requirement

**Require device to be marked as compliant**

This connects the Conditional Access decision to the device compliance status reported by Microsoft Intune.

### Device Platforms

**Any device**

### Client Apps

The configured client application condition was left enabled.

## Testing

The Windows 11 lab device:

`DESKTOP-48ASFDI`

was enrolled into Microsoft Intune and had a **Compliant** status through the `LAB-WIN-02-Basic-Compliance` policy.

A sign-in was then examined in the Microsoft Entra sign-in logs.

Under the **Conditional Access** section, the following result was observed:

```text
LAB-CA-01-Require-Compliant-Device
RequireCompliantDevice
Report-only: Success
```

This confirmed that Conditional Access evaluated the policy and that the device satisfied the requirement to be marked as compliant.

## Compliance → Conditional Access Flow

```text
Windows 11 Device
       |
       v
Microsoft Entra Joined
       |
       v
Microsoft Intune
       |
       v
Compliance Policy Evaluation
       |
       v
Device = Compliant
       |
       v
Compliance Status Available to Entra ID
       |
       v
Conditional Access Evaluation
       |
       v
Require Device to be Marked as Compliant
       |
       v
Report-only: Success
```

## Key Concepts Learned

### 1. Intune determines device compliance

Microsoft Intune evaluates the device against the configured compliance policy.

In this lab, the device was evaluated as **Compliant**.

### 2. Conditional Access consumes the compliance signal

Conditional Access does not itself determine whether the Windows device satisfies the Intune compliance policy.

Instead, Microsoft Entra uses the compliance status provided by Intune when evaluating the Conditional Access policy.

### 3. Report-only allows safe testing

The Conditional Access policy was left in **Report-only** mode.

This means the policy is evaluated during sign-in, but it does not enforce the access decision.

The observed `Report-only: Success` confirmed that the policy requirement was satisfied.

### 4. Sign-in logs provide evidence

The Microsoft Entra sign-in logs can be used to determine whether a Conditional Access policy was evaluated and what the result would have been.

This provides an important troubleshooting and auditing capability.

## Result

**Lab 3 successfully configured and tested.**

The lab demonstrated the relationship between:

**Microsoft Intune Compliance → Microsoft Entra Conditional Access → Sign-in Evaluation**

The policy remains in **Report-only** mode for continued testing before any enforcement is considered.
