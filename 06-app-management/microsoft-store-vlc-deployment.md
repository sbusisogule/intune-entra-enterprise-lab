# Lab 4  Microsoft Intune Application Deployment

## Objective

Deploy a Windows application through Microsoft Intune and verify that the application is successfully installed on the managed Windows device.

This lab demonstrates the basic Intune application lifecycle:

**Add application → Configure application → Assign application → Sync device → Verify installation**

## Lab Environment

| Component              | Configuration        |
| ---------------------- | -------------------- |
| Microsoft Entra tenant | Existing lab tenant  |
| Microsoft Intune       | Enabled              |
| Test user              | `Intune Test User`   |
| Pilot group            | `INTUNE-Pilot-Users` |
| Windows device         | `DESKTOP-48ASFDI`    |
| Operating system       | Windows 11           |
| Windows build          | `10.0.26200.6584`    |
| Application            | VLC                  |
| Publisher              | VideoLAN             |

## Application Configuration

### Application

**VLC**

The application was selected from the **Microsoft Store app (new)** catalog.

### Platform

**Windows**

### App Type

**Microsoft Store app (new)**

### Installer Type

**Win32**

The selected VLC package was identified by Intune as a Win32 application.

### Install Behavior

**System**

The application was configured to install in the system context rather than only for an individual user.

### Package Identifier

`XPDM1ZW6815MQM`

### Application Version

`3.0.23`

## Assignment

The application was configured as a **Required** application.

### Assignment Configuration

| Setting              | Value                |
| -------------------- | -------------------- |
| Assignment type      | Required             |
| Included group       | `INTUNE-Pilot-Users` |
| Assignment status    | Active               |
| Filter mode          | None                 |
| Available assignment | None                 |
| Uninstall assignment | None                 |

A Required assignment tells Intune to automatically deploy the application to targeted devices.

## Deployment Process

The deployment followed this process:

```text
VLC selected from Microsoft Store catalog
              ↓
Application added to Intune
              ↓
Required assignment created
              ↓
INTUNE-Pilot-Users assigned
              ↓
Windows device synchronized with Intune
              ↓
Intune processed the application assignment
              ↓
VLC installed on DESKTOP-48ASFDI
```

## Device Synchronization

After assigning VLC, the Windows device was manually synchronized from:

**Windows Settings → Accounts → Access work or school → Info → Sync**

The synchronization completed successfully.

The device subsequently received the VLC application deployment.

## Deployment Verification

The installation was verified in two ways.

### 1. Windows Device Verification

On `DESKTOP-48ASFDI`, VLC appeared in the Windows Start menu as:

**VLC media player**

This confirmed that the application was installed on the Windows device.

### 2. Intune Device Install Status

In Microsoft Intune:

**Apps → All apps → VLC → Monitor → Device install status**

the following result was reported:

| Device            | User                                           | Windows Version   | App Version | Status        |
| ----------------- | ---------------------------------------------- | ----------------- | ----------- | ------------- |
| `DESKTOP-48ASFDI` | `intune.testuser@labentratune.onmicrosoft.com` | `10.0.26200.6584` | `3.0.23`    | **Installed** |

This provided Intune-side confirmation that the application deployment succeeded.

## Key Concepts Learned

### Required vs Available

A **Required** application is automatically deployed to targeted users or devices.

An **Available for enrolled devices** application is made available to the user through the Company Portal, allowing the user to choose whether to install it.

An **Uninstall** assignment instructs Intune to remove the application from targeted users or devices.

### Assignment

Adding an application to Intune does not automatically mean it will be installed.

The application must be assigned to a target such as a user or group.

In this lab:

`INTUNE-Pilot-Users`

was used as the target group.

### System Install Behavior

The VLC application was configured with:

**Install behavior: System**

This means the application installation occurs in the system context rather than being limited to the signed-in user's profile.

### Synchronization

A device synchronization causes the Windows device to contact Intune and retrieve updated management information.

The synchronization itself does not prove that an application has installed.

The actual installation result must be verified separately.

### Deployment Verification

Successful Intune application deployment should be verified using Intune's installation status as well as, where appropriate, checking the device itself.

In this lab:

**Intune = Installed**

and

**Windows = VLC available**

Both confirmed successful deployment.

## Result

**Lab 4 completed successfully.**

VLC version `3.0.23` was deployed through Microsoft Intune as a required Microsoft Store Win32 application and successfully installed on the managed Windows device `DESKTOP-48ASFDI`.
