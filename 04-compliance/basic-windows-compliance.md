# Lab 2 — Windows Compliance Policy

## Objective

Create and test a Microsoft Intune compliance policy for Windows devices.

The objective was to enforce a minimum Windows operating system version and verify that Intune can evaluate a device as compliant or noncompliant based on the configured requirement.

---

## Lab Environment

| Component          | Configuration                   |
| ------------------ | ------------------------------- |
| Microsoft Intune   | Microsoft Intune                |
| Microsoft Entra ID | Microsoft Entra ID              |
| Windows device     | `DESKTOP-48ASFDI`               |
| VMware VM          | `WIN11-INTUNE-01`               |
| Pilot group        | `INTUNE-Pilot-Users`            |
| Compliance policy  | `LAB-WIN-02-Basic-Compliance`   |
| Platform           | Windows 10 and later            |
| Profile type       | Windows 10/11 compliance policy |

---

## Compliance Policy Configuration

### Policy

**Name:** `LAB-WIN-02-Basic-Compliance`

**Description:**

> Baseline Windows compliance policy for the Intune pilot environment.

### Assignment

The policy was assigned to:

`INTUNE-Pilot-Users`

No groups were excluded.

### Device Properties

The following compliance requirement was configured:

**Minimum OS version:**

`10.0.26100.0`

The following settings were left unconfigured:

* Maximum OS version
* Minimum OS version for mobile devices

### Actions for Noncompliance

The policy was configured to:

**Mark device noncompliant — Immediately**

---

## Testing

### Test 1 — Compliant Device

After the policy was assigned, the Windows device was synchronized with Intune.

The device was evaluated against the minimum operating system requirement.

**Result:**

**Compliant**

This confirmed that the Windows device met the configured minimum OS version requirement.

---

### Test 2 — Deliberate Noncompliance

A controlled test was performed by temporarily increasing the minimum OS version requirement to a value higher than the Windows device's installed version.

After Intune evaluated the updated policy, the device was reported as:

**Noncompliant**

This demonstrated that Intune correctly detects when a device does not satisfy a compliance requirement.

---

### Test 3 — Remediation

The minimum OS version requirement was restored to:

`10.0.26100.0`

The Windows device was synchronized with Intune again.

After the compliance evaluation completed, the device returned to:

**Compliant**

---

## Compliance Lifecycle Demonstrated

The lab demonstrated the complete compliance workflow:

```text
Compliance Policy
       ↓
Assignment to Pilot Group
       ↓
Device Sync
       ↓
Compliance Evaluation
       ↓
Compliant
       ↓
Policy Requirement Changed
       ↓
Noncompliant
       ↓
Requirement Remediated
       ↓
Compliant
```

---

## Key Concepts Learned

### Compliance Policy

A compliance policy defines the conditions a device must satisfy to be considered compliant.

### Assignment

The policy was assigned to the `INTUNE-Pilot-Users` group. Assignment determines which users or devices are targeted by the policy.

### Compliance Evaluation

After the device synchronized with Intune, Intune evaluated the device against the configured compliance requirement.

### Noncompliance

When the device did not meet the minimum OS requirement, Intune reported the Windows device as noncompliant.

### Remediation

After the policy requirement was restored to an appropriate value and the device synchronized again, Intune reevaluated the device and returned it to a compliant state.

### Important Operational Observation

A successful device synchronization does not necessarily mean that the compliance status will update immediately in the Intune portal.

The synchronization and subsequent compliance evaluation are separate steps, so the administrator may need to allow time for the compliance result to update.

---

## Result

**Lab 2 completed successfully.**

The lab demonstrated the configuration, assignment, evaluation, deliberate failure, and remediation of a Windows compliance policy using Microsoft Intune.
