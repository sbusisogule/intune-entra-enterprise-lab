# Microsoft Intune + Microsoft Entra ID Enterprise Lab

A hands on enterprise endpoint management lab built with Microsoft Intune, Microsoft Entra ID, and Windows 11 Enterprise.

## Project Objective

The objective of this project is to design, deploy, manage, secure, and troubleshoot Windows endpoints using Microsoft Intune and Microsoft Entra ID.

The lab follows Microsoft's current Intune and Entra management concepts and focuses on practical administrator skills. 

## Lab Environment

| Component | Configuration |
|---|---|
| Identity | Microsoft Entra ID |
| Device Management | Microsoft Intune |
| License | Microsoft 365 Business Premium |
| Operating System | Windows 11 Enterprise 25H2 |
| Virtualization | VMware Workstation |
| Test Device | Windows 11 Enterprise VM |
| Enrollment | Microsoft Entra Join + Automatic Intune Enrollment |
| Device Ownership | Corporate |
| Pilot Group | INTUNE-Pilot-Users |
| Test User | Intune Test User |

## Current Architecture

Microsoft Entra ID
        |
        | Identity
        v
Intune Test User
        |
        v
INTUNE-Pilot-Users
        |
        v
Windows 11 Enterprise
        |
        | Microsoft Entra Join
        v
DESKTOP-48ASFDI
        |
        | MDM Enrollment
        v
Microsoft Intune
