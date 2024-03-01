---
# required metadata

title: Configure Platform SSO for macOS devices
description: Use Microsoft Intune to configure Platform SSO for macOS devices. Platform SSO enables single sign-on (SSO) using a Microsoft Entra ID.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/29/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Configure Platform SSO for macOS devices in Microsoft Intune

> [!IMPORTANT]
> This article is a final draft and ready for PM review. It will go live when Platform SSO goes live. **Delete this note before publishing**.

On your macOS devices, you can configure Platform SSO to enable single sign-on (SSO) using a Microsoft Entra ID. Platform SSO signs users into the device using their Microsoft Entra ID.

This article applies to:

- macOS

On macOS devices, users sign in with a local account. Then, they sign into apps and websites with their Microsoft Entra ID.

When Platform SSO is configured, users sign into the device with their Microsoft Entra ID instead of their local account. When they sign into the device with their Microsoft Entra ID, then they get access to device features that use Microsoft Entra ID for authentication.

The [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) in Microsoft Entra includes two SSO features - **Platform SSO** and the **SSO app extension**.

When you use configure Platform SSO, you also need to configure the [SSO app extension](use-enterprise-sso-plug-in-macos-with-intune.md). Platform SSO and the SSO app extension work together. Platform SSO handles the initial device sign-in, and the SSO app extension handles the sign-in for apps and websites that use Microsoft Entra ID for authentication, including Microsoft 365 apps.

Some benefits of Platform SSO include:

- Helps minimize the number of times users need to enter their Microsoft Entra credentials.
- Helps reduce the number of passwords users need to remember.
- Similar experience to signing into a Windows device with a work account, like users do with Windows Hello for Business.
- Get the benefits of Microsoft Entra ID join, which allows any organization user to sign into the device.

Platform SSO uses the Microsoft Intune [settings catalog](settings-catalog.md) to configure the policy. When the policy is ready, you assign the policy to your users or devices. Microsoft recommends you assign the policy when the device enrolls in Intune. But, it can be assigned at any time, including on existing devices.

This article shows you how to configure Platform SSO for macOS devices in Intune.

## Prerequisites

- Devices must be macOS 13.0 and newer devices.only the SSO extension can access the WPJ cert.
- Supported web browsers include:
  - Microsoft Edge
  - Safari

  When macOS client devices join a Microsoft Entra tenant, the devices get a workplace join (WPJ) certificate. To access protected resources, web browsers need this WPJ certificate. With Platform SSO, the SSO app extension uses the WPJ certificate to act as a broker between the devices and Apple. Only the SSO extension can access the WPJ cert.

  These browsers are broker-aware and allow the SSO app extension to use the WPJ certificate.

- To create the Intune policy, at a minimum, sign in with an account that has the **Policy and Profile Manager** Intune RBAC role. For more information on RBAC roles in Intune, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Step 1 - Configure the SSO app extension policy in Intune

Platform SSO requires the SSO app extension be configured for your apps using a Microsoft Intune policy. Platform SSO is only available with Microsoft Intune. So, make sure you follow the Intune steps when creating the SSO app extension policy.

For the specific steps and SSO app extension requirements, go to [Use the Microsoft Enterprise SSO app extension on macOS devices](use-enterprise-sso-plug-in-macos-with-intune.md).

## Step 2 - Create the Platform SSO policy in Intune

To configure the Platform SSO policy, use the following steps to create an [Intune settings catalog](settings-catalog.md) policy.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration** > **Create**.
3. Enter the following properties:

    - **Platform**: Select **macOS**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, name the policy **macOS - Platform SSO**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Add settings**. In the settings picker, expand **Authentication**, and select **Extensible Single Sign On (SSO)**:

    :::image type="content" source="./media/platform-sso-macos/settings-picker-authentication-extensible-sso.png" alt-text="Screenshot that shows the Settings Catalog settings picker, and selecting authentication and extensible SSO category in Microsoft Intune.":::

    In the list, select the following settings:

    - **Authentication Method (Deprecated)** (macOS 13 only)
    - **Extension Identifier**
    - Expand **Platform SSO** > select **Authentication Method** (macOS 14+)
    - **Registration Token**
    - **Screen Locked Behavior**
    - **Team Identifier**
    - **Type**
    - **URLs**

    Close the settings picker.

8. Configure the following settings:

    - **URLs**: Enter the following array of URL prefixes. These URL prefixes are the identity providers that do SSO app extensions. The URLs are required for **redirect** payloads and are ignored for **credential** payloads.

      - `https://login.microsoftonline.com`
      - `https://login.microsoft.com`
      - `https://sts.windows.net`
      - `https://login.partner.microsoftonline.cn`
      - `https://login.chinacloudapi.cn`
      - `https://login.microsoftonline.us`
      - `https://login-us.microsoftonline.com`

      For the URLs to work, they must meet the following requirements:

      - The URLs must begin with `http://` or `https://`.
      - The scheme and host name must match and are case-insensitive.
      - Query parameters and URL fragments aren't allowed.
      - The URLs of all installed Extensible SSO payloads must be unique.

      > [!NOTE]
      > These URLs are required by the Microsoft Enterprise SSO plug-in. For more information, go to [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin).

    - **Team Identifier**: Enter `UBF8T346G9`, which is the team identifier of the Enterprise SSO plug-in app extension.
    - **Screen Locked Behavior**: Select **Do Not Handle**. When set to **Do Not Handle**, the request continues without SSO.
    - **Registration token**: Enter the token the device uses for registration with Platform SSO. This token silently registers with the Identity Provider.

      For example, enter `{{DEVICEREGISTRATION}}`. You must include the curly braces.

      This setting requires that you also configure the `AuthenticationMethod` setting. If you use macOS 13 devices, then configure the **Authentication Method (Deprecated)** setting. If you use macOS 14+ devices, then configure the **Platform SSO** > **Authentication Method** setting. If you have a mix of macOS 13 and macOS 14+ devices, then configure both authentication settings in same profile.

    - **Platform SSO** > **Authentication Method** (macOS 14+): Select the Platform SSO authentication method that the app extension uses. The SSO app extension must also support the method.

      This setting applies to macOS 14 and later. For macOS 13, use the **Authentication Method (Deprecated)** setting.

      Your options:

      - **Password** (default): Enables SSO across apps that use Microsoft Entra ID for authentication. This option:

        - The Microsoft Entra password​ replaces the local account password, and then keeps the password in sync.
        - Leaves the local account username as-is. The username isn't changed.
        - Requires fewer passwords for users and admins to remember and manage.​
        - Requires users to enter their Microsoft Entra password after a device reboots. After this initial machine unlock​, Touch ID can be used to unlock local machine.
        - After unlock, the device gets the hardware-bound Primary Refresh Token (PRT) credential for Microsoft Entra SSO.​

        This option doesn't completely remove the local account machine password. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

        Any password policy you configure also also affect this setting. For example, if you have a password policy that blocks simple passwords, then simple passwords are also blocked for this setting. Make sure your Intune password policy and/or compliance policy matches your Microsoft Entra password policy. If the policies don't match, then the password might not sync and end users are denied access.

      - **UserSecureEnclaveKey**: Enables SSO across apps that use Microsoft Entra ID for authentication by provisioning a [Secure Enclave](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/protecting_keys_with_the_secure_enclave) cryptographic key. This option:

        - Is considered a password-less and phish-resistant option. It's conceptually similar to Windows Hello for Business. It can use the same features as Windows Hello for Business, like Conditional Access.
        - Leaves the local account username and password as-is. These values aren't changed.​
        - After a device reboots, users must enter the local account password. After this initial machine unlock​, Touch ID can be used to unlock local machine.
        - After unlock, device gets the hardware-backed Primary Refresh Token (PRT) for device-wide SSO.​
        - In web browsers, this key can be used as a passkey using [WebAuthN APIs](https://webauthn.guide).
        - Its setup can be bootstrapped with an authentication app for multifactor authentication or Microsoft [Temporary Access Pass (TAP)](/entra/identity/authentication/howto-authentication-temporary-access-pass).

        This option doesn't completely remove the local account machine password. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

      - **SmartCard**: Enables SSO across apps that use Microsoft Entra ID for authentication. It uses a smart card or smart card-compatible hard token, like a YubiKey. This token acts as a local machine password.​ This option:

        - Is considered a password-less option.
        - Leaves the local account username and password as-is. These values aren't changed.​

    - **Authentication Method (Deprecated)** (macOS 13 only): Select the Platform SSO authentication method that the app extension uses. The SSO app extension must also support the method.

      This setting applies to macOS 13 only. For macOS 14.0 and later, use the **Platform SSO** > **Authentication Method** setting.

      Your options:

      - **Password** (default): Enables SSO across apps that use Microsoft Entra ID for authentication and:

        - The Microsoft Entra password​ replaces the local account password, and then keeps the password in sync.
        - Leaves the local account username as-is. The username isn't changed.
        - Requires fewer passwords for users and admins to remember and manage.​
        - Requires users to enter their Microsoft Entra password after a device reboots. After this initial machine unlock​, Touch ID can be used to unlock local machine.
        - After unlock, the device gets the hardware-bound Primary Refresh Token (PRT) credential for Microsoft Entra SSO.​

        This option doesn't completely remove the local account machine password. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

      - **UserSecureEnclaveKey**: Enables SSO across apps that use Microsoft Entra ID for authentication by provisioning a [Secure Enclave](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/protecting_keys_with_the_secure_enclave) cryptographic key. And:

        - Is considered a password-less and phish-resistant option. It's conceptually similar to Windows Hello for Business, as it can use the same features as Windows Hello for Business, like Conditional Access.
        - Leaves the local account username and password as-is. These values aren't changed.​
        - After a device reboots, users must enter the local account password. After this initial machine unlock​, Touch ID can be used to unlock local machine.
        - After unlock, the device gets the hardware-backed Primary Refresh Token (PRT) for device-wide SSO.​
        - In web browsers, this key can be used as a passkey using [WebAuthN APIs](https://webauthn.guide).
        - Its setup can be bootstrapped with an authentication app for multifactor authentication or Microsoft [Temporary Access Pass (TAP)](/entra/identity/authentication/howto-authentication-temporary-access-pass).

        This option doesn't completely remove the local account machine password. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

    - **Extension Identifier**: Enter `com.microsoft.CompanyPortalMac.ssoextension`. This ID is the SSO app extension that the profile needs for SSO work.

      The **Extension Identifier** and **Team Identifier** values work together.

    - **Type**: Select **Redirect**.

9. Select **Next**.
10. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC roles and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

11. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied.

## Step 3 - Deploy the Company Portal app for macOS

The Company Portal app for macOS deploys and installs the Microsoft Enterprise SSO plug-in. This plug-in also enables Platform SSO.

Using Intune policies, you add the Company Portal app, make it a required app, and then deploy the app to your macOS devices:

1. Add the Company Portal app for macOS to Intune and make it a required app. For the steps, go to [Add the Company Portal app for macOS](../apps/apps-company-portal-macos.md).
2. Configure the Company Portal app to include your organization information. For the steps, go to [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

    There aren't any specific steps to configure the app for Platform SSO. Just make sure the latest Company Portal app is added to Intune and deployed to your macOS devices. If you have an older version of the Company Portal app installed, then Platform SSO won't work.

For information on the end user experience, go to [Join a Mac device with Microsoft Entra ID during the out of box experience with macOS Platform SSO](/entra/identity/devices/device-join-macos-platform-single-sign-on).

## Step 4 - Enroll the devices and apply the policies

To use Platform SSO, the devices must be MDM enrolled in Intune using one of the following methods:

- For **organization-owned devices, create an [Automated device enrollment](../enrollment/device-enrollment-program-enroll-macos.md) policy** using Apple Business Manager or Apple School Manager. Assign this enrollment profile to your macOS devices.
- For **personally-owned devices, create a [Device enrollment](../fundamentals/deployment-guide-enrollment-macos.md#byod-device-enrollment) policy**. With this enrollment method, end users open the Company Portal app and sign in with their Microsoft Entra ID. When they successfully sign-in, the enrollment policy applies.

If the devices are **new devices**, then we recommend you precreate and configure all the necessary policies, including the enrollment policy. Then, when the devices enroll in Intune, the policies automatically apply.

If the devices are **existing devices** that are already enrolled, then you can assign the policies to the devices. The next time the devices sync or check-in with the Intune services, they receive the Platform SSO policy settings you create.

## Step 5 - Confirm the settings on the device

When the enrollment completes and the policies are applied, you can confirm the Platform SSO is configured. For the steps, go to [Microsoft Entra ID - Check your device registration status](/entra/identity/devices/device-join-macos-platform-single-sign-on#check-your-device-registration-status).

On an enrolled device, you can also go to **Settings** > **Privacy and security** > **Profiles**. Your Platform SSO profile should be listed. Select the profile to see the settings you configured, including the URLs.

## Related content

- [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin)
- [Use the Microsoft Enterprise SSO app extension on macOS devices](use-enterprise-sso-plug-in-macos-with-intune.md)
- [What is a Primary Refresh Token (PRT)?](/entra/identity/devices/concept-primary-refresh-token)
