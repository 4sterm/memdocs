---
title: Windows Autopilot self-deploying mode - Step 6 of 6 - Deploy the device
description: How to - Windows Autopilot self-deploying mode - Step 5 of 5 - Step 6 of 6 - Deploy the device.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/07/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Self-deploying mode: Deploy the device

Autopilot self-deploying mode steps:
- Step 1: [Set up Windows automatic Intune enrollment](self-deploying-automatic-enrollment.md)
- Step 2: [Register devices as Autopilot devices](self-deploying-register-device.md)
- Step 3: [Create a device group](self-deploying-device-group.md)

- Step 4: [Configure and assign Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)
- Step 5: [Create and assign Autopilot profile](self-deploying-autopilot-profile.md)
> [!div class="checklist"]
> - **Step 6: Deploy the device**

For an overview of the Windows Autopilot self-deploying mode workflow, see [Windows Autopilot self-deploying overview](self-deploying-workflow.md#workflow)

## Deploy the device

> [!TIP]
>
> Although a user isn't assigned to a device for Windows Autopilot self-deploying mode, for testing purposes, assigning at least one policy and at least one application to users is still recommended since User ESP still runs when a user first signs into the device.

Once all of the configurations for the Windows Autopilot user-driven Azure AD join deployment have been completed on the Intune and Azure AD side, the next step is to start the Autopilot deployment process on the device. If desired, deploy any additional applications and policies that should run during the Autopilot deployment to a device group that the device is a member of.

[!INCLUDE [Assignment tip](../includes/assignment-tip.md)]

To start the Autopilot deployment process on the device, select a device that is part of the device group created in the previous [Create a device group](self-deploying-device-group.md) step, and then follow these steps:

[!INCLUDE [Network connectivity](../includes/network-connectivity.md)]

4. The Enrollment Status Page (ESP) appears. The Enrollment Status Page (ESP) displays progress during the provisioning process across three phases:

   - **Device preparation** (Device ESP)
   - **Device setup** (Device ESP)
   - **Account setup** (User ESP)

    The first two phases of **Device preparation** and **Device setup** are part of the Device ESP while the final phase of **Account setup** is part of the User ESP. For Windows Autopilot self-deploying mode, only the Device ESP and its related two related phases (**Device preparation** and **Device setup**) run. User ESP and **Account setup** don't run until after the Windows Autopilot self-deploying deployment is complete and a user signs in.

    > [!TIP]
    >
    > To view and hide detailed progress information in the ESP during the provisioning process:
    >
    > - Windows 10: To show details, next to the appropriate phase select **Show details**. To hide the details, next to the appropriate phase select **Hide details**.
    > - Windows 11: To show details, next to the appropriate phase select **∨**. To hide the details, next to the appropriate phase select **∧**.

5. Once **Device setup** and the device ESP process completes, the Windows Autopilot self-deploying deployment is complete, and the Windows sign-on screen appears.

6. At this point, the end-user can sign into the device using their Azure AD credentials. When the user signs in, the user ESP and **Account setup** phase runs. Once user ESP and **Account setup** completes, the provisioning process completes, the Desktop appears, and the end-user can start using the device.

> [!NOTE]
>
> Depending on how the Autopilot profile was configured at the [Create and assign Autopilot profile](self-deploying-autopilot-profile.md) step, the Keyboard screen may appear at the start of the deployment.

## More information