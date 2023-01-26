---
# required metadata

title: Microsoft Enterprise SSO plug-in in Microsoft Intune
description: Overview of Microsoft Enterprise SSO plug-in in Microsoft Intune, Jamf Pro and other MDM solution providers. The Enterprise SSO plug-in is available on iOS/iPadOS and macOS devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/25/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: apple-enterprise-sso
---

# Deploy the Microsoft Enterprise SSO plug-in for Apple Devices (preview)

In Microsoft Intune, there's a Microsoft Enterprise SSO plug-in. This plug-in provides single sign-on (SSO) to iOS/iPadOS and macOS apps and websites that use Microsoft Azure Active Directory (Azure AD) for authentication.

This article applies to:

- iOS/iPadOS
- macOS

## Get started with your MDM provider and platform

The Enterprise SSO plug-in can be used in Microsoft Intune, Jamf Pro, or other MDM solutions. For more information about the plug-in, which SSO option to use, and how to create the SSO profile, go to the following articles:

- **Deploy using Intune**
::: zone pivot="all,ios-ipados"
  - [**iOS/iPadOS**: Deploy the Microsoft Enterprise SSO plug-in using Intune](./use-enterprise-sso-plug-in-ios-ipados-with-intune.md)
::: zone-end
::: zone pivot="all,macos"
  - [**macOS**: Deploy the Microsoft Enterprise SSO plug-in using Intune](./use-enterprise-sso-plug-in-macos-with-intune.md)
::: zone-end

- **Deploy using Jamf Pro**
::: zone pivot="all,ios-ipados"
  - [**iOS/iPadOS**: Deploy the Microsoft Enterprise SSO plug-in using Jamf Pro](./use-enterprise-sso-plug-in-ios-ipados-with-jamf-pro.md)
::: zone-end
::: zone pivot="all,macos"
  - [**macOS**: Deploy the Microsoft Enterprise SSO plug-in using Jamf Pro](./use-enterprise-sso-plug-in-macos-with-jamf-pro.md)
::: zone-end

- **Deploy using other MDMs**
::: zone pivot="all,ios-ipados"
  - [**iOS/iPadOS**: Deploy the Microsoft Enterprise SSO plug-in using another MDM](./use-enterprise-sso-plug-in-ios-ipados-with-generic-mdm.md)
::: zone-end
::: zone pivot="all,macos"
  - [**macOS**: Deploy the Microsoft Enterprise SSO plug-in using another MDM](./use-enterprise-sso-plug-in-macos-with-generic-mdm.md)
::: zone-end

## Next steps

- For information about the Microsoft Enterprise SSO plug-in and Azure AD, go to [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, go to [single sign-on extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
