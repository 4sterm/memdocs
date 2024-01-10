---
# required metadata

title: See device profiles with Microsoft Intune
description: See and manage the device configuration profile details in Microsoft Intune. Look at a graphical chart of the number of devices assigned to a profile, and see which devices have profiles assigned or deployed. Can also troubleshoot profiles that have conflict settings. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: 9deaed87-fb4b-4689-ba88-067bc61686d7

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Monitor device configuration profiles in Microsoft Intune

Intune includes some features to help monitor and manage your device configuration profiles. For example, you can check the status of a profile, go to the devices are assigned to the profile, and update the properties of an existing profile.

This article shows you how to view existing profiles for assignment status, making changes, and how to troubleshoot any conflicts.

## View existing profiles

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration**.

All of your profiles are shown. You also see the platform, the type of profile, and if the profile is assigned.

> [!NOTE]
> For more in-depth reporting information about device configuration profiles, go to [Intune reports](../fundamentals/reports.md).

## View details on a profile

After you create your device profile, Intune provides graphical charts. These charts display the status of a profile, such as it being successfully assigned to devices, or if the profile shows a conflict.

1. In **Devices** > **Configuration**, select an existing profile.
2. The following statuses are shown:

    - **Succeeded**: Policy is applied successfully.
    - **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
    - **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
    - **Pending**: The device hasn't checked in with Intune to receive the policy yet.
    - **Not applicable**: The device can't receive the policy. For example, the policy updates a setting specific to iOS 11.1, but the device is using iOS 10.

3. The top graphical chart shows the number of devices assigned to the device profile. For example, if the configuration device profile applies to macOS devices, the chart lists the count of the macOS devices.

    When you monitor a Windows profile, the count in the **Profile assignment status** is per device per user. So, if two users sign in to the same device, then that device is counted twice.

4. Select the top graphical chart. Or, select **Device status**.

    In **Device status**, the devices assigned to the profile are listed, and the deployment status is shown. It only lists the devices with the specific platform, like macOS.

    Close the **Device status** details.

5. Select the circle in the bottom graphical chart. Or, select **User status**.

    In **User status**, the users assigned to the profile are listed, and the deployment status is shown. It only lists the users with the specific platform, like macOS.

    Close the **User status** details.

6. Back in the **Profiles** list, select a specific profile.

    - **Properties**: Change the policy name, or update any existing configuration settings. You can also update:

      - **Scope tags**: See any existing [scope tags](../fundamentals/scope-tags.md) used in the policy. Select **Edit** to add or remove a scope tag.
      - **Assignments**: See the users and groups that receive policy, and see any existing [filters](../fundamentals/filters.md) in the policy. Select **Edit** to update the policy assignment, and add or remove a filter.
      - **Applicability Rules**: On your Windows devices, go to the [applicability rules](device-profile-create.md#applicability-rules) used in the policy. Select **Edit** to add or remove an applicability rule.

    - **Device and user check-in status**: Shows the number of **all** users or devices that checked-in with the profile. If one device has multiple users, this report shows the status for each user. When the user or device check-in, they receive the settings in your profile.

      Select **View report** to see the following information:

      - The devices that received the profile
      - The user names with devices that received the profile
      - The check-in status and the last time the user/device checked in with the profile

      You can also select a specific device to get more details and use the filter column to see the assignment filter options.

    - **Device assignment status**: Shows information for the user that last checked-in. Select **Generate report** to see the latest profile assignment states for the devices that received the profile. You can also filter the assignment status to see only errors, conflicts, and more.

      It's normal for the numbers in the **Device and user check-in status** and **Device assignment status** reports to be different.

    - **Per setting status**: Shows the individual settings in the profile, and their status.

> [!TIP]
> [Intune reports](../fundamentals/reports.md) is a great resource, and describes all the reporting features you can use.

## View conflicts

In **Devices** > **All devices**, you can see any settings that are causing a conflict. When there's a conflict, you also see all the configuration profiles that contain this setting.

Administrators can use this feature to help troubleshoot, and fix any discrepancies with the profiles.

1. In Intune, select **Devices** > **All Devices** > select an existing device in the list. An end user can get the device name from their Company Portal app.
2. Select **Configuration**. All configuration policies that apply to the device are listed.
3. Select the policy. It shows you all the settings in that policy that apply to the device. If a device has a **Conflict** state, select that row. In the new window, you see all the profiles, and the profile names that have the setting causing the conflict.

Now that you know the conflicting setting, and the policies that include that setting, it should be easier to resolve the conflict.

> [!TIP]
> In **Devices** > **Monitor**, a list of all reports are shown. The **Configuration policy assignment failures** report helps troubleshoot errors and conflicts for configuration profiles that are assigned. For more information on the available reporting data, go to [Intune reports](../fundamentals/reports.md).

## Device Firmware Configuration Interface (DFCI) profile reporting

DFCI profiles are reported on a per-setting basis, just like other device configuration profiles. Depending on the manufacturer's support of DFCI, some settings may not apply.

With your DFCI profile settings, you may see the following states:

- **Compliant**: This state shows when a setting value in the profile matches the setting on the device. This state can happen in the following scenarios:

  - The DFCI profile successful configured the setting in the profile.
  - The device doesn't have the hardware feature controlled by the setting, and the profile setting is **Disabled**.
  - UEFI doesn't allow DFCI to disable the feature, and the profile setting is **Enabled**.
  - The device lacks the hardware to disable the feature, and the profile setting is **Enabled**.

- **Not Applicable**: This state shows when a setting value in the profile is **Enabled** or **Allowed**, and the matching setting on the device isn't found. This state can happen if the device hardware doesn't have the feature.

- **Noncompliant**: This state shows when a setting value in the profile doesn't match the setting on the device. This state can happen in the following scenarios:

  - UEFI doesn't allow DFCI to disable a setting, and the profile setting is **Disabled**.
  - The device lacks the hardware to disable the feature, and the profile setting is **Disabled**.
  - The device doesn't have the latest DFCI firmware version.
  - DFCI was disabled before being enrolled in Intune using a local "opt-out" control in the UEFI menu.
  - The device was enrolled to Intune outside of Autopilot enrollment.
  - The device wasn't registered to Autopilot by a Microsoft CSP, or registered directly by the OEM.

## Related content

- [Common questions, issues, and resolutions with device profiles](device-profile-troubleshoot.md)
- [Troubleshoot policies and profiles and in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
