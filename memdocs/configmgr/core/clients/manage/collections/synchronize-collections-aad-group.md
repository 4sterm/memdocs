---
title: Synchronize collection members to Azure AD groups
titleSuffix: Configuration Manager
description: Synchronize collection members to Azure AD groups.
ms.date: 11/30/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to synchronize collection members to Azure AD groups

<!--3607475-->

You can enable the synchronization of collection memberships to an Azure Active Directory (Azure AD) group. This synchronization allows you to use your existing on premises grouping rules in the cloud by creating Azure AD group memberships based on collection membership results. You can synchronize device or user collections. Only resources with an Azure AD record are reflected in the Azure AD group. Both hybrid Azure AD-joined and Azure AD-joined devices are supported. The synchronization of collection memberships is a one-way process from Configuration Manager to Azure AD. Ideally, Configuration Manager should be the authority for managing the membership for the target Azure AD groups.

Synchronizations can either be full or incremental and they have slightly different behaviors: <!--9718854-->

- Full synchronization: Occurs on the first synchronization after enabling it. You can force a full synchronization by selecting the collection, and then choosing **Synchronize Membership** from the ribbon. A full synchronization will overwrite members of the Azure AD group.

- Incremental synchronization: Occurs every 5 minutes. Changes made in Azure AD aren't reflected in Configuration Manager collections, but they aren't overwritten by Configuration Manager. <!--For example, if the Configuration Manager collection has two devices, and the Azure AD group has three different devices, after an incremental synchronization, the Azure AD group has five devices.-->

Example synchronization scenario:
1. From Azure AD, create a group called `Group1` and add `DeviceA`, `DeviceB`, and `DeviceC`.
   - Ideally, objects wouldn't be added from Azure AD since Configuration Manager should manage the group membership. 
1. From Configuration Manager, create a collection called `Collection1` then add `DeviceB`, and `DeviceC`.
1. [Enable synchronization](#enable-the-collection-to-synchronize) for `Collection1` to `Group1`.
1. The first synchronization is a full synchronization so, `Group1` now contains `DeviceB`, and `DeviceC`. `DeviceA` was removed from the group during the full synchronization.
1. Remove `DeviceC` from `Collection1` and wait for an incremental synchronization.
1. `Group1` now contains only `DeviceB`.
1. From Azure AD, add `DeviceD` to `Group1` and wait for an incremental synchronization.
1. `Group1` now contains `DeviceB` and `DeviceD`.
1. From Configuration Manager, select `Collection1`, and choose **Synchronize Membership** from the ribbon to force a full synchronization.
1. `Group1` now contains only `DeviceB`

## Prerequisites for Azure AD synchronization

- Integration with Azure AD for [cloud management](../../../servers/deploy/configure/azure-services-wizard.md)

- [Azure AD user discovery](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)

- An HTTPS or [Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md)-enabled management point

- Access to the **All Systems** collection

## Create a group and set the owner in Azure AD

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Navigate to **Azure Active Directory** > **Groups** > **All groups**.

1. Select **New group**, enter a **Group name**, and optionally enter a **Group description**.

1. Make sure that **Membership type** is **Assigned**.

1. Select **Owners**, then add the identity that will create the synchronization relationship in Configuration Manager.

1. Select **Create** to finish creating the Azure AD group.

## Enable collection synchronization for the Azure service

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services**, and select the **Azure Services** node.

1. Select the cloud management service for the Azure AD tenant where you created the group. Then in the ribbon, select **Properties**.

1. Switch to the **Collection Synchronization** tab, and select the option to **Enable Azure Directory Group Sync**.

1. Select **OK** to save the setting.

## Enable the collection to synchronize

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select either the **Device Collections** or **User Collections** node.

1. Select the collection to sync. Then in the ribbon, select **Properties**.

1. Switch to the **Cloud Sync** tab, and select **Add**.

1. If necessary, change the **Tenant** to where you created the Azure AD group.

1. Type in your search criteria in the **Name starts with** field, then select **Search**. If you leave the criteria blank, the search returns all groups from the tenant. If it prompts you to sign in, use the identity you specified as the owner for the Azure AD group.

1. Choose the target group, and then select **OK** to add the group. Select **OK** again to exit the collection's properties.

Wait about five to seven minutes before you can verify the group memberships in the Azure portal. To start a full synchronization, select the collection, and then in the ribbon select **Synchronize Membership**.

## <a name="bkmk_powershell"></a> Use PowerShell

You can use PowerShell to synchronize collections. For more information, see the following cmdlet article:

[Set-CMCollectionCloudSync](https://learn.microsoft.com/en-us/powershell/module/configurationmanager/set-cmcollectioncloudsync)

## Monitor the collection synchronization status

1. In the Configuration Manager console, go to the **Monitoring** workspace

1. select **Collection Cloud Sync** and select either the **Device Collections** or **User Collections** node.

1. The view lists all the collections that are enabled for cloud sync and relevant details.

1. Right click on column header and add additional columns to view more information. 

Default Columns: 

- Collection Id – Id of Collection 

- Collection Name – Name of Collection 

- AAD Group Id – Configured Azure AD Group Id 

- AAD Group Name – Configured Azure AD Group Name  

- Cloud Sync Status 

    Success: If all members are synchronized to target Azure AD Group 

    Partial Success: If at least one member is synchronized to target Azure AD Group 

    Failed: If all members failed to synchronize to target Azure AD Group 

    In Progress: Synchronization is in progress. 

- Member Count – Count of members of collection 

- Sync Completed – Count of members successfully synchronized 

- Sync InProgress – Count of members pending synchronization 

- Sync Failed – Count of members failed to synchronize 

Optional Columns: 

- Cloud Service Id – Azure Service Id which is used for Cloud Sync 

- Collection Type – Type of Collection (Device or User) 

- Last Full Sync Member Count – Count of members synchronized during last full sync 

- Last Full Sync Status – Status of last full sync cycle 

- Last Full Sync Time – Time of last full sync cycle 

- Last Sync Member Count - Count of members synchronized during last sync 

- Last Sync Status - Status of last sync cycle 

- Last Sync Time - Time of last sync cycle
 
:::image type="content" source="media/collection-aad-group-sync.png" alt-text="Screenshot of Collections Cloud Sync Status." lightbox="media/collection-aad-group-sync.png":::

## Verify the Azure AD group membership

1. Go to the [Azure portal](https://portal.azure.com).

1. Navigate to **Azure Active Directory** > **Groups** > **All groups**.

1. Find the group you created and select **Members**.

1. Confirm that the members reflect the resources in the Configuration Manager collection. Only resources with Azure AD identity show in the group.

:::image type="content" source="media/3607475-sync-collection-to-azuread.png" alt-text="Screenshot of Synchronize collections to Azure AD." lightbox="media/3607475-sync-collection-to-azuread.png":::
