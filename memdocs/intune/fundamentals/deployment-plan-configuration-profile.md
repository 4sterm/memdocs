---
# required metadata

title: Configure security, email, VPN, and Wi-Fi device configuration profiles
titleSuffix: Microsoft Intune
description: Step 4 to deploy device configuration profiles as part of the minimum set of policies for your devices using Microsoft Intune. The starting point is to enable the firewall, install AV, scan for malware, install software updates, create a strong PIN policy, and create email, VPN, and Wi-Fi device configuration profiles.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/02/2023
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

# Step 4 - Configure device features and settings to secure devices and access resources

So far, you've set up your Intune subscription, created app protection policies, and created device compliance policies.

In this step, you're ready to configure a minimum or baseline set of security and device features that all devices must have.

This article applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

When you create device configuration profiles, there are different levels and types of policies available. These levels are the minimum Microsoft recommended policies. Know that your environment and business needs may be different.

- Level 1 - Minimum device configuration (this article)
- Level 2 - Enhanced device configuration (see INSERT LINK)
- Level 3 - High device configuration (see INSERT LINK)

In **Level 1 - Minimum device configuration**, Microsoft recommends you create policies that:

- Focus on device security, including installing antivirus, creating a strong password policy, and regularly installing software updates.
- Give users access to their organization email and controlled secure access to your network, wherever they are.

This article lists the **Level 1 - Minimum device configuration** device configuration policies that organizations should use. Most of these policies in this article focus on access to organization resources and security.

These features are configured in device configuration profiles in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). When the profiles are ready, they can be deployed from Intune to your devices.

> [!TIP]
> [Take a tour of Intune and the Endpoint Manager admin center](tutorial-walkthrough-endpoint-manager.md).

## Level 1 - Create your security baseline

To help keep your organization data and devices secure, you create different policies that focus on security. You should create a list of security features that all users and/or all devices must have. This list is your security baseline.

In your baseline, at a minimum, Microsoft recommends the following security policies:

- Install antivirus (AV) and regularly scan for malware
- Use detection and response
- Turn on the firewall
- Install software updates regularly
- Create a strong PIN/password policy

This section lists the Intune and Microsoft services you can use to create these security policies.

If you prefer a more granular list of settings and their recommended values, go to:

- [Android Enterprise security configuration framework](../enrollment/android-configuration-framework.md)
- [iOS/iPadOS personal device security configurations](../enrollment/ios-ipados-personal-device-security-configurations.md)
- [Windows security baselines](../protect/security-baselines.md)

### Antivirus and scanning

✔️ **Install antivirus software and regularly scan for malware**

All devices should have antivirus software installed and be regularly scanned for malware. Intune integrates with third party partner mobile threat defense (MTD) services that provide AV and threat scanning. For macOS and Windows, antivirus and scanning are built in to Intune with Microsoft Defender for Endpoint.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise | - Mobile threat defense partner </br>- Microsoft Defender for Endpoint for Android can scan for malware |
| iOS/iPadOS | Mobile threat defense partner |
| macOS | Intune Endpoint Security antivirus profile (Microsoft Defender for Endpoint) |
| Windows client | - Intune security baselines (recommended)</br>- Intune Endpoint Security antivirus profile (Microsoft Defender for Endpoint) </br>- Mobile threat defense partner |

For more information on these features, go to:

- [**Android Enterprise** and **iOS/iPadOS** mobile threat defense integration](../protect/mobile-threat-defense.md)
- [**Android Enterprise** Microsoft Defender for Endpoint overview](/microsoft-365/security/defender-endpoint/mtd)
- [**Windows** security baselines](../protect/security-baselines.md)
- [**macOS** and **Windows** antivirus policy](../protect/endpoint-security-antivirus-policy.md)

### Detection and response

✔️ **Detect attacks and act on these threats**

When you detect threats quickly, you can help minimize the impact of the threat. When you combine these policies with conditional access, you can block users and devices from accessing organization resources if a threat is detected.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise | - Mobile threat defense partner</br>- Microsoft Defender for Endpoint on Android |
| iOS/iPadOS | - Mobile threat defense partner</br>- Microsoft Defender for Endpoint on iOS/iPadOS |
| macOS | Not available |
| Windows client | - Intune security baselines (recommended)</br>- Intune endpoint detection and response profile (Microsoft Defender for Endpoint) </br>- Mobile threat defense partner |

For more information on these features, go to:

- **Android Enterprise** and **iOS/iPadOS**:
  - [Mobile threat defense integration with Intune](../protect/mobile-threat-defense.md)
  - [Microsoft Defender for Endpoint overview](/microsoft-365/security/defender-endpoint/mtd)
- [**Windows** security baselines](../protect/security-baselines.md)
- [**Windows** endpoint detection and response policy](../protect/endpoint-security-edr-policy.md)

### Firewall

✔️ **Enable the firewall on all devices**

Some platforms come with a built-in firewall and on others, you may have to install a firewall separately. Intune integrates with third party partner mobile threat defense (MTD) services that can manage a firewall for Android and iOS/iPadOS devices. For macOS and Windows, firewall security is built in to Intune with Microsoft Defender for Endpoint.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise | Mobile threat defense partner |
| iOS/iPadOS | Mobile threat defense partner |
| macOS | Intune Endpoint Security firewall profile (Microsoft Defender for Endpoint) |
| Windows client | - Intune security baselines (recommended)</br>- Intune Endpoint Security firewall profile (Microsoft Defender for Endpoint) </br>- Mobile threat defense partner |

For more information on these features, go to:

- [**Android Enterprise** and **iOS/iPadOS** mobile threat defense integration](../protect/mobile-threat-defense.md)
- [**Windows** security baselines](../protect/security-baselines.md)
- [**macOS** and **Windows** firewall policy](../protect/endpoint-security-firewall-policy.md)

### Password policy

✔️ **Create a strong password/PIN policy and block simple passcodes**

PINs unlock devices. On devices that access organization data, including personally owned devices, you should require strong PINs/passcodes and support biometrics. Using biometrics is part of a password-less approach, which is recommended.

Intune uses device restrictions profiles to create and configure password requirements.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise | Intune device restrictions profile to manage the: <br/>- Device password<br/>- Work profile password |
| AOSP | Intune device restrictions profile |
| iOS/iPadOS | Intune device restrictions profile |
| macOS | Intune device restrictions profile |
| Windows client | - Intune security baselines (recommended) </br>- Intune device restrictions profile |

For a list of the settings you can configure, go to:

- **Android Enterprise** device restrictions profile:
  - [Corporate owned devices > **Device password** and **Work profile password**](../configuration/device-restrictions-android-for-work.md)
  - [Personally owned devices with a work profile > **Work profile password** and **Password**](../configuration/device-restrictions-android-enterprise-personal.md)
- [**Android AOSP** device restrictions profile > **Device password**](../configuration/device-restrictions-android-aosp.md)
- [**iOS/iPadOS** device restrictions profile > **Password**](../configuration/device-restrictions-ios.md)
- [**macOS** device restrictions profile > **Password**](../configuration/device-restrictions-macos.md)
- [**Windows** security baselines](../protect/security-baselines.md)
- [**Windows** client device restrictions profile > **Password**](../configuration/device-restrictions-windows-10.md)
- [**Windows**: Manage Windows Hello for Business when devices enroll](../protect/windows-hello.md)
- [**Windows**: Manage Windows Hello for Business after devices enroll](../protect/identity-protection-configure.md)

### Software updates

✔️ **Regularly install software updates**

All devices should be updated regularly and policies should be created to make sure these updates are successfully installed. For most platforms, Intune has dedicated policies that focus on managing and installing updates.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise organization owned devices | System update settings using Intune device restrictions profile |
| Android Enterprise personally owned devices | Not available <br/><br/>Can use compliance policies to set a minimum patch level, min/max OS version, and more. |
| iOS/iPadOS | Intune update policy |
| macOS | Intune update policy |
| Windows client | - Intune feature updates policy </br>- Intune expedited updates policy |

For more information on these features and/or the settings you can configure, go to:

- [**Android Enterprise** device restrictions profile > **System update**](../configuration/device-restrictions-android-for-work.md)
- [**iOS/iPadOS** software update policies](../protect/software-updates-ios.md)
- [**macOS** software update policies](../protect/software-updates-macos.md)
- **Windows**:

  - [Feature updates policy](../protect/windows-10-feature-updates.md)
  - [Expedited updates policy](../protect/windows-10-expedite-updates.md)

## Level 1 - Access organization email, connect to VPN or Wi-Fi

This section focuses on accessing resources in your organization. These resources include:

- Email for work or school accounts
- VPN connection for remote connectivity
- Wi-Fi connection for on-premises connectivity

:::image type="content" source="./media/deployment-plan-configuration-profile/deploy-email-vpn-wifi.png" alt-text="Image that shows an email, VPN and Wi-Fi profiles deployed from Microsoft Intune to end user devices.":::

### Email

Many organizations deploy email profiles with preconfigured settings to user devices.

✔️ **Automatically connect to user email accounts**

The profile includes the email configuration settings that connect to your email server.

Depending on the settings you configure, the email profile can also automatically connect the users to their individual email account settings.

✔️ **Use enterprise level email apps**

Email profiles in Intune use common and popular email apps, like Outlook. The email app is deployed to user devices. After it's deployed, you deploy the email device configuration profile with the settings that configure the email app.

The email device configuration profile includes settings that connect to your Exchange.

✔️ **Access work or school email**

Creating an email profile is a common minimum baseline policy for organizations with users that use email on their devices.

Intune has built in email settings for Android, iOS/iPadOS, and Windows client devices. When users open their email app, they can automatically connect, authenticate, and synchronize their organizational email accounts on their devices.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the email app during the enrollment process. When enrollment completes, then deploy the email device configuration policy.

If you have existing devices, then deploy the email app at any time, and deploy the email device configuration policy.

#### Get started with email profiles

To get started:

1. Deploy an email app to your devices. For some guidance, go to [Add email settings to devices using Intune](../configuration/email-settings-configure.md).

2. [Create an email device configuration profile in Intune](../configuration/email-settings-configure.md). Depending on the email app your organization uses, the email device configuration profile might not be needed.

    For some guidance, go to [Add email settings to devices using Intune](../configuration/email-settings-configure.md).

3. In the email device configuration profile, configure the settings for your platform:

    - [Android Enterprise personally owned devices with a work profile email settings](../configuration/email-settings-android-enterprise.md)

      Android Enterprise organization-owned devices don't use email device configuration profiles.

    - [iOS/iPadOS email settings](../configuration/email-settings-ios.md)
    - [Windows email settings](../configuration/email-settings-windows-10.md)

4. [Assign the email device configuration profile](../configuration/device-profile-assign.md) to your users or user groups.

### VPN

Many organizations deploy VPN profiles with preconfigured settings to user devices. The VPN connects your devices to your internal organization network.

If your organization uses cloud services with modern authentication and secure identities, then you probably don't need a VPN profile. Cloud-native services don't require a VPN connection.

If your apps or services aren't cloud-based or aren't cloud-native, then it's recommended to deploy a VPN profile to connect to your internal organization network.

✔️ **Work from anywhere**

Creating a VPN profile is a common minimum baseline policy for organizations with remote workers and hybrid workers.

As users work from anywhere, they can use the VPN profile to securely connect to your organization's network to access resources.

Intune has built in VPN settings for Android, iOS/iPadOS, macOS, and Windows client devices. On user devices, your VPN connection is shown as an available connection. Users select it. And, depending on the settings in your VPN profile, users can automatically authenticate and connect to the VPN on their devices.

✔️ **Use enterprise level VPN apps**

VPN profiles in Intune use common enterprise VPN apps, like Check Point, Cisco, Microsoft Tunnel, and more. The VPN app is deployed to user devices. After the app is deployed, then you deploy the VPN connection profile with settings that configure the VPN app.

The VPN device configuration profile includes settings that connect to your VPN server.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the VPN app during the enrollment process. When enrollment completes, then deploy the VPN device configuration policy.

If you have existing devices, deploy the VPN app at any time, and then deploy the VPN device configuration policy.

#### Get started with VPN profiles

To get started:

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

### Wi-Fi

Many organizations deploy Wi-Fi profiles with preconfigured settings to user devices. If your organization has a remote-only workforce, then you don't need to deploy Wi-Fi connection profiles. Wi-Fi profiles are optional and are used for on-premises connectivity.

✔️ **Connect wirelessly**

As users work from different mobile devices, they can use the Wi-Fi profile to wirelessly and securely connect to your organization's network.

The profile includes the Wi-Fi configuration settings that automatically connect to your network and/or SSID (service set identifier). Users don't have to manually configure their Wi-Fi settings.

✔️ **Support mobile devices on-premises**

Creating a Wi-Fi profile is a common minimum baseline policy for organizations with mobile devices that work on-premises.

Intune has built in Wi-Fi settings for Android, iOS/iPadOS, macOS, and Windows client devices. On user devices, your Wi-Fi connection is shown as an available connection. Users select it. And, depending on the settings in your Wi-Fi profile, users can automatically authenticate and connect to the Wi-Fi on their devices.

✔️ **Deploy anytime**

On new devices, it's recommended to deploy the Wi-Fi device configuration policy when devices enroll in Intune.

If you have existing devices, you can deploy the Wi-Fi device configuration policy at any time.

#### Get started with Wi-Fi profiles

To get started:

1. [Create a Wi-Fi device configuration profile in Intune](../configuration/wi-fi-settings-configure.md).
2. Configure the settings for your platform:

    - [Android Enterprise Wi-Fi settings](../configuration/wi-fi-settings-android-enterprise.md)
    - [iOS/iPadOS Wi-Fi settings](../configuration/wi-fi-settings-ios.md)
    - [macOS Wi-Fi settings](../configuration/wi-fi-settings-macos.md)
    - [Windows Wi-Fi settings](../configuration/vpn-settings-windows-10.md)

3. [Assign the Wi-Fi device configuration profile](../configuration/device-profile-assign.md) to your users or user groups.

## Level 2 - Enhanced protection and configuration

- Enable **disk encryption, secure boot, and TPM** on your devices. These features combined with a strong PIN policy or biometric unlocking are recommended at this level.

  Your options:

  | Platform | Use Intune |
  | --- | --- |
  | **Android** |✔️ On Android devices, disk encryption and Samsung Knox might be built into the operating system. Disk encryption might be automatically enabled *when* you configure the lock screen settings. In Intune, you can create a device restrictions policy that configures lock screen settings. <br/><br/>For a list of the password and lock screen settings you can configure, go to the following articles:<br/><br/>- [Organization owned devices - Device password](../configuration/device-restrictions-android-for-work.md#device-password)<br/>- [Organization owned devices - Work profile password](../configuration/device-restrictions-android-for-work.md#work-profile-password)<br/>- [Personally owned devices - Work profile password](../configuration/device-restrictions-android-enterprise-personal.md#work-profile-password)<br/>- [Personally owned devices - Device password](../configuration/device-restrictions-android-enterprise-personal.md#password) |
  | **iOS/iPadOS** | ❌ On iOS/iPadOS devices, disk encryption and Secure Enclave are built into the operating and automatically enabled. There aren't any Intune settings to configure these features. There are Intune policies that focus on password settings and encrypting backups. <br/><br/>For more specific information, go to [Introduction to Apple platform security](https://support.apple.com/guide/security/intro-to-apple-platform-security-seccd5016d31/web) and [Secure Enclave](https://support.apple.com/guide/security/secure-enclave-sec59b0b31ff/web) (opens Apple's web site). |
  | **macOS** | ✔️ On macOS devices, you can [configure and use FileVault](../protect/encrypt-devices-filevault.md) policies in Intune for disk encryption. |
  | **Windows** | ✔️ On Windows devices, there are Intune endpoint protection policies that [manage BitLocker, including TPM](../protect/encrypt-devices.md) and [manage Windows settings, including secure boot](../protect/endpoint-protection-windows-10.md#windows-encryption). |

- **Expire passwords and regulate reusing old passwords**. In Level 1, you created a strong PIN or password policy. If you haven't already, be sure you configure your PINs & passwords to expire and set some password-reuse rules.

  Your options:

  | Platform | Use Intune |
  | --- | --- |
  | **Android** |✔️ On Android devices, you can use Intune to create a device restrictions policy that configures these settings. <br/><br/>For a list of the password settings you can configure, go to the following articles:<br/><br/>- [Organization owned devices - Device password](../configuration/device-restrictions-android-for-work.md#device-password)<br/>- [Organization owned devices - Work profile password](../configuration/device-restrictions-android-for-work.md#work-profile-password)<br/>- [Personally owned devices - Work profile password](../configuration/device-restrictions-android-enterprise-personal.md#work-profile-password)<br/>- [Personally owned devices - Device password](../configuration/device-restrictions-android-enterprise-personal.md#password) |
  | **iOS/iPadOS** | ✔️ On iOS/iPadOS devices, you can use Intune to create a device restrictions policy that configures these settings. <br/><br/>For a list of the password settings you can configure, go to [iOS/iPadOS password settings](../configuration/device-restrictions-ios.md#password). <br/><br/>The [settings catalog](../configuration/settings-catalog.md) may also have some relevant password settings.|
  | **macOS** | ✔️ On macOS devices, you can use Intune to create a device restrictions policy that configures these settings. <br/><br/>For a list of the password settings you can configure, go to [macOS password settings](../configuration/device-restrictions-macos.md#password).<br/><br/>The [settings catalog](../configuration/settings-catalog.md) may also have some relevant password settings.|
  | **Windows** | ✔️ On Windows devices, you can use Intune to create a device restrictions policy that configures these settings. <br/><br/>For a list of the password settings you can configure, go to [iOS/iPadOS password settings](../configuration/device-restrictions-windows-10.md#password).<br/><br/>The [settings catalog](../configuration/settings-catalog.md) may also have some relevant password settings. |

- Intune includes **hundreds of settings that can manage devices features** and settings, like disabling the built-in camera, controlling notifications, allowing bluetooth, blocking games, and more. You can use the built-in templates or the settings catalog to see all the settings and configure the settings.

  - [**Device restrictions**: Many built-in settings that can control different parts of the devices, including security, hardware, data sharing, and more](../configuration/device-restrictions-configure.md)
  - [**iOS/iPadOS, macOS, Windows**: Use the Settings catalog to see all the available settings](../configuration/settings-catalog.md)
  - **Windows 10/11**:
    - [Use built-in administrative templates](../configuration/administrative-templates-windows.md)

- If you use **on-premises GPOs** and want to know if these same settings are available in Intune, then use Group Policy analytics. This feature analyzes your GPOs and depending on the analysis, can import them into an Intune policy.

  For more information, go to [Analyze your on-premises GPOs and import them in Intune](../configuration/group-policy-analytics.md).

## Level 3 - High protection and configuration

THIS SECTION IS STILL BEING WRITTEN

- **Expand password-less authentication** to other services used by your workforce. In level 1, you enabled biometrics so users can sign in to their devices with a fingerprint or facial recognition. In this level, expand password-less to other parts of the organization.

  - **Use certificates to authenticate** email, VPN, and Wi-Fi connections. Certificates are deployed to users and devices, and are then used by users to get access to resources in your organization through these email, VPN, and Wi-Fi connections.

    To learn more about using certificate in Intune, go to:

    - [Use PKCS or SCEP certificates for authentication](../protect/certificates-configure.md)
    - [Use derived credentials](../protect/derived-credentials.md)

  - **Configure single sign-on** (SSO) for a more seamless experience when users open business apps, like Microsoft 365 apps. Users sign-in once and then are automatically signed-in to all the apps that support your SSO configuration.

    To learn about using SSO in Intune and Azure AD, go to:

    - [**Android**: Enable cross-app SSO on Android using MSAL in Azure AD](/azure/active-directory/develop/msal-android-single-sign-on)
    - [**iOS/iPadOS, macOS**: Use the Enterprise SSO plug-in in Intune and other MDMs](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)
    - [**Windows**: Configure SSO with Azure AD](/azure/active-directory/manage-apps/what-is-single-sign-on)

  - When you move to password-less, enable and **use multi-factor authentication** (MFA). MFA adds an extra layer of security, and can help protect your organization from phishing attacks. You can use MFA with authenticator apps, like Microsoft Authenticator, or with a phone call or text message. You can also use MFA when users enroll their devices in Intune.

    Multi-factor authentication is a feature of Azure AD and can be used with Azure AD accounts. For more information, go to:

    - [Azure AD identity protection overview](/azure/active-directory/identity-protection/overview-identity-protection)
    - [Azure AD multi-factor authentication](/azure/active-directory/authentication/concept-mfa-howitworks)
    - [Require multi-factor authentication for Intune device enrollments](/enrollment/multi-factor-authentication.md)

- [Android Common Criteria mode](../configuration/device-restrictions-android-for-work.md#system-security)

- Microsoft Tunnel: For your Android or iOS/iPadOS devices, use the **Microsoft Tunnel VPN gateway** solution. Microsoft Tunnel uses Linux to allow these devices access to on-premises resources using modern authentication and conditional access.

  [Microsoft Tunnel for Microsoft Intune](../protect/microsoft-tunnel-overview.md)

- Create policies that apply to the Windows firmware layer

  Prevent malware from communicating with the Windows OS processes. On your Windows devices, create policies that apply to the Windows firmware layer.

  - [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices](../configuration/device-firmware-configuration-interface-windows.md)

- Configure kiosks, shared devices, and other specialized devices:

  - **Android device administrator**
    - [Use and manage Zebra devices with Zebra Mobility Extensions](../configuration/android-zebra-mx-overview.md)
    - [Device settings to run as a kiosk](../configuration/device-restrictions-android.md#kiosk)

  - **Android Enterprise**:
    - [Use and manage Android Enterprise devices with OEMConfig](../configuration/android-oem-configuration-overview.md)
    - [Dedicated devices that run as a kiosk device settings](../configuration/device-restrictions-android-for-work.md#dedicated-devices)

  - **iOS/iPadOS**
    - [Device settings to run in autonomous single app mode (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam)
    - [Device settings to run as a kiosk](../configuration/device-restrictions-ios.md#kiosk)

  - **Windows**
    - [Device settings to run as a dedicated kiosk](../configuration/kiosk-settings.md)
    - [Device settings to run as a kiosk](../configuration/kiosk-settings-windows.md)
    - [Shared PC or multi-user devices](../configuration/shared-user-device-settings.md)
  - **Windows Holographic for Business**
    - [Device settings to run as a kiosk](../configuration/kiosk-settings-holographic.md)
    - [Device settings to run as a dedicated kiosk](../configuration/kiosk-settings.md)

- Deploy scripts:
  - [**macOS**: Use shell scripts](../apps/macos-shell-scripts.md)
  - [**Windows**: Use Windows PowerShell scripts](../apps/intune-management-extension.md)

## Follow the minimum recommended baseline policies

1. [Set up Microsoft Intune](deployment-plan-setup.md)
2. [Add, configure, and protect apps](deployment-plan-protect-apps.md)
3. [Plan for compliance policies](deployment-plan-compliance-policies.md)
4. 🡺 **Configure device features** (*You are here*)
5. [Enroll devices](deployment-guide-enrollment.md)
