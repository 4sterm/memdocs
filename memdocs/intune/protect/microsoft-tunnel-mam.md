---
title: Learn about using Microsoft Tunnel with Mobile Application Management
description: Use Microsoft Tunnel for MAM with Android and iOS devices. Tunnel support for MAM expands access to your organizational resources for devices that can't or haven't enrolled with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/18/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Microsoft Tunnel for Mobile Application Management

When you use the Microsoft Tunnel VPN Gateway, you can extend Tunnel support by adding Tunnel for Mobile Application Management (MAM). Tunnel MAM extends the Microsoft Tunnel VPN gateway to support devices that run Android or iOS, and that aren't enrolled with Microsoft Intune. With this solution, your users can use a single device that hasn't enrolled with Intune to gain secure access to the organizations on-premises apps and resources using modern authentication, Single Sign On and conditional access. With Tunnel for MAM, your users can use their own device (BYOD) for both work and personal use, without having to grant the organization’s IT department control over that device.

Applies to:

- Android  (In public preview)
- iOS/iPadOS (In public preview)

> [!NOTE]
> While in public preview, Microsoft Tunnel for MAM is available at no additional cost. When Tunnel for MAM becomes generally available, it will be available as a [**premium add-on**](/fundamentals/premium-add-ons.md) and require an additional cost to the licensing options that include Microsoft Endpoint Manager or Intune.

## Platform requirements and feature overview

Before you begin, you must already have deployed the Microsoft Tunnel gateway. To learn more about Microsoft Tunnel gateway and how to install and configure it,  see:

- [Learn about the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-overview.md)
- [Identify the prerequisites to install and use the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-prerequisites.md)
- [Install and configure Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-configure.md)

Microsoft Tunnel for MAM supports the following platforms:

- Android Enterprise version 10.0 or higher
- iOS version 14.0 or higher

The following table identifies key features for the supported platforms:

|                  |Tunnel for Android     | Tunnel for iOS           |
|------------------|-----------------------|--------------------------|
| Requirements:    | - Company Portal app (sign-in not required)<br><br> - Defender for Endpoint app     | - No Company Portal app or Defender for Endpoint app requirement   |
| Features:        | - VPN is provided via the Defender for Endpoint app: <br> --- Per App VPN <br> --- Device Wide VPN <br><br> - *Auto-launch*: VPN automatically starts on app launch   | - VPN is provided via Tunnel for MAM iOS SDK integration <br><br> - Per-App VPN. Tunnel connection is restricted to each targeted app <br><br> - *Auto-launch*: VPN automatically starts on app launch <br><br>   -  No Device Wide VPN <br><br> - Trusted root certificate support for on-premises CA trust (available for public preview) <br><br>  |
| Line of Business app requirements| - MAM-SDK <br><br> - MSAL integration  | - MAM-SDK <br><br> - MSAL integration <br> --- Azure AD App registration <br><br> -  MAM Tunnel-SDK    |
| Microsoft Edge browser support:| - *Identity switch*: VPN connects when using a work or school account and disconnects when switching to a personal account or in-Private browsing <br><br> - Device-wide and Per-App VPN support  | - *Identity switch*: VPN connects when using a work/school account and disconnects when switching to a personal account or in-Private browsing   |
| Third-party browser support:     | - Only with device-wide VPN enabled  | - None  |

## Next steps

[Learn about the Microsoft Tunnel VPN solution for Microsoft Intune](../protect/microsoft-tunnel-overview.md)