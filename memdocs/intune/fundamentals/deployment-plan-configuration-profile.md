---
# required metadata

title: Configure email, VPN, and Wi-Fi device configuration profiles
titleSuffix: Microsoft Intune
description: Use Microsoft Intune to create email, VPN, and Wi-Fi device configuration profiles as part of the minimum set of policies for your devices.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/17/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite:
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: 
  - M365-identity-device-management 
  - highpri
---

# Step 4: Create device configuration profiles to apply email, VPN and Wi-Fi connections

In this step, you're ready to configure a minimum or baseline set of device features that all devices must have, which typically includes:

- Email for work or school accounts
- VPN connection for remote connectivity
- Wi-Fi connection for on-premises connectivity

These features are configured in device configuration profiles in the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). When the profiles are ready, they can be deployed from Intune to your devices.

:::image type="content" source="./media/deployment-plan-configuration-profile/deploy-email-vpn-wifi.png" alt-text="Image that shows an email, VPN and Wi-Fi profiles deployed from Microsoft Intune to end user devices.":::

This article lists some common baselines device configuration policies that organizations use. Most of these policies in this article focus on access to organization resources. In your organization, you may have a different set of baseline device configuration policies.

This article applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

## Email

Many organizations deploy email profiles with preconfigured settings to user devices.

✔️ **Automatically connect to user email accounts**

The profile includes the email configuration settings that connect to your email server.

Depending on the settings you configure, the email profile can automatically connect the users to their individual email account settings. Users don't have to manually configure their email accounts.

✔️ **Use enterprise level email apps**

Email profiles in Intune use common and popular email apps, such as Gmail and Outlook. The email app is deployed to user devices. After it's deployed, you deploy the email device configuration profile with settings that configure the email app.

The email device configuration profile includes settings that connect to your Exchange.

✔️ **Access work or school email**

Creating an email profile is a common minimum baseline policy for organizations with users that use email on their devices.

Intune has built-in email settings for Android, iOS/iPadOS, and Windows client devices. When users open their email app, they can automatically connect, authenticate, and synchronize their organizational email accounts on their devices.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the email app during the enrollment process. When enrollment completes, then deploy the email device configuration policy. If you have existing devices, deploy the email app at any time, and then deploy the email device configuration policy.

### Get started with email profiles

To get started, use the following links:

1. Deploy an email app to your devices. For some guidance, go to [Add email settings to devices using Intune](../configuration/email-settings-configure.md).

2. [Create an email device configuration profile in Intune](../configuration/email-settings-configure.md). Depending on the email app your organization uses, the email device configuration profile might not be needed.

    - If you use an app configuration policy to deploy an email app, then don't create an email device configuration profile. The email app configuration policy configures the email app for you.
    - If you don't use an app configuration policy to deploy an email app, then create an email device configuration profile.

    For some guidance, go to [Add email settings to devices using Intune](../configuration/email-settings-configure.md).

3. In the email device configuration profile, configure the settings for your platform:

    - [Android Enterprise personally owned devices with a work profile email settings](../configuration/email-settings-android-enterprise.md); Android Enterprise organization-owned devices don't use email device configuration profiles
    - [iOS/iPadOS email settings](../configuration/email-settings-ios.md)
    - [Windows email settings](../configuration/email-settings-windows-10.md)

4. [Assign the email device configuration profile](../configuration/device-profile-assign.md) to your users or user groups.

## VPN

Many organizations deploy VPN profiles with preconfigured settings to user devices. 

✔️ **Work from anywhere**

As users work from anywhere, they can use the VPN profile to securely connect to your organization's network to access resources.

✔️ **Use enterprise level VPN apps**

VPN profiles in Intune use common enterprise VPN apps, such as Check Point, Cisco, Microsoft Tunnel, and more. The VPN app is deployed to user devices. After the app is deployed, then you deploy the VPN connection profile with settings that configure the VPN app.

The VPN device configuration profile includes settings that connect to your VPN server.

✔️ **Support remote workers**

Creating a VPN profile is a common minimum baseline policy for organizations with remote workers and hybrid workers.

Intune has built-in VPN settings for Android, iOS/iPadOS, macOS, and Windows client devices. On user devices, your VPN connection is shown as an available connection. Users select it. And, depending on the settings in your VPN profile, users can automatically authenticate and connect to the VPN on their devices.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the VPN app during the enrollment process. When enrollment completes, then deploy the VPN device configuration policy. If you have existing devices, deploy the VPN app at any time, and then deploy the VPN device configuration policy.

### Get started with VPN profiles

To get started, use the following links:

1. Deploy a VPN app to your devices.

    - For a list of supported VPN apps, go to [Supported VPN connection apps in Intune](../configuration/vpn-settings-configure.md#vpn-connection-types).
    - For the steps to add apps to Intune, go to [Add apps to Microsoft Intune](../apps/apps-add.md).

2. [Create a VPN configuration profile in Intune](../configuration/vpn-settings-configure.md).
3. In the VPN device configuration profile, configure the settings for your platform:

    - [Android Enterprise VPN settings](../configuration/vpn-settings-android-enterprise.md)
    - [iOS/iPadOS VPN settings](../configuration/vpn-settings-ios.md)
    - [macOS VPN settings](../configuration/vpn-settings-macos.md)
    - [Windows VPN settings](../configuration/vpn-settings-windows-10.md)

4. [Assign the VPN device configuration profile](../configuration/device-profile-assign.md) to your users or user groups.

## Wi-Fi

Many organizations deploy Wi-Fi profiles with preconfigured settings to user devices. 

✔️ **Connect wirelessly**

As users work from different mobile devices, they can use the Wi-Fi profile to wirelessly and securely connect to your organization's network.

The profile includes the Wi-Fi configuration settings that automatically connect to your network and/or SSID (service set identifier). Users don't have to manually configure their Wi-Fi settings.

✔️ **Support mobile devices on-premises**

Creating a Wi-Fi profile is a common minimum baseline policy for organizations with mobile devices that work on-premises.

Intune has built-in Wi-Fi settings for Android, iOS/iPadOS, macOS, and Windows client devices. On user devices, your Wi-Fi connection is shown as an available connection. Users select it. And, depending on the settings in your Wi-Fi profile, users can automatically authenticate and connect to the Wi-Fi on their devices.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the Wi-Fi device configuration policy when devices enroll in Intune. If you have existing devices, you can deploy the Wi-Fi device configuration policy at any time.

### Get started with Wi-Fi profiles

To get started, use the following links:

1. [Create a Wi-Fi device configuration profile in Intune](../configuration/wi-fi-settings-configure.md).
2. Configure the settings for your platform:

    - [Android Enterprise Wi-Fi settings](../configuration/wi-fi-settings-android-enterprise.md)
    - [iOS/iPadOS Wi-Fi settings](../configuration/wi-fi-settings-ios.md)
    - [macOS Wi-Fi settings](../configuration/wi-fi-settings-macos.md)
    - [Windows Wi-Fi settings](../configuration/vpn-settings-windows-10.md)

3. [Assign the Wi-Fi device configuration profile](../configuration/device-profile-assign.md) to your users or user groups.

## Do more

Intune has more built-in device settings, depending on how much you want to manage on your devices. The following list includes some other features you can configure:

- **[Administrative templates](../configuration/administrative-templates-windows.md)**: Intune includes built-in ADMX settings that you add to a policy and then deploy the policy to your devices. You don't need to download any files; they're already built in.
- **[Device restrictions](../configuration/device-restrictions-configure.md)**: There are many built-in settings that can control different parts of the devices, including security, hardware, data sharing, and more.
- **[PKCS or SCEP certificates](../protect/certificates-configure.md)**: Use certificates to authenticate and authorize Wi-Fi connections, VPN connections, and user email account access.
- **[Analyze your on-premises GPOs and import them in Intune](../configuration/group-policy-analytics.md)**: If you use on-premises GPOs, then you can use Group Policy Analytics to analyze your policies and determine if your settings are supported in the cloud. If they're supported, they can be imported into an Intune policy and deployed to your devices.
- **[Settings catalog](../configuration/settings-catalog.md)**: The settings catalog is a list of all the settings you can configure in Intune. If you use on-premises GPOs to manage your devices, then the settings catalog is a natural transition to cloud-based policies.

For a complete list of all the device configuration profiles you can create, go to [Apply features and settings on your devices using device profiles in Microsoft Intune](../configuration/device-profiles.md).

## Follow the minimum recommended baseline policies

1. Set up Microsoft Intune
2. Add and protect apps
3. Create compliance policies
4. 🡺 **Create device configuration profiles to apply email, VPN and Wi-Fi connections** (*You are here*)
5. Enroll devices
