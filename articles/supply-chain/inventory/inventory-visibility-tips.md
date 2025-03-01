---
title: Inventory Visibility tips
description: This article provides a few tips that you should consider when you set up and use the Inventory Visibility Add-in.
author: yufeihuang
ms.date: 08/02/2021
ms.topic: article
ms.search.form:
audience: Application User
ms.reviewer: kamaybac
ms.search.region: Global
ms.author: yufeihuang
ms.search.validFrom: 2021-08-02
ms.dyn365.ops.version: 10.0.21
---

# Inventory Visibility tips

[!include [banner](../includes/banner.md)]

Here are a few tips that you should consider when you set up and use the Inventory Visibility Add-in:

- Currently, the Inventory Visibility Add-in supports only Microsoft Dataverse environments that were created by using Microsoft Dynamics Lifecycle Services. If your Dataverse environment was created in some other way (for example, by using the Power Apps admin center), and if it's linked to your Dynamics 365 Supply Chain Management environment, you must first ask the Inventory Visibility product team to fix the mapping issue. You can contact the team at [inventvisibilitysupp@microsoft.com](mailto:inventvisibilitysupp@microsoft.com). The team will let you know when your environment is ready for you to install Inventory Visibility.
- If you have more than one Lifecycle Services environment, create a different Microsoft Entra application for each environment. If you use the same application ID and tenant ID to install the Inventory Visibility Add-in for different environments, a token issue will occur for older environments. Only the last instance of the Inventory Visibility Add-in that was installed will be valid.
- Inventory Visibility isn't currently supported for cloud-hosted environments. It's supported only for Tier-2+ environments.
- The application programming interface (API) allows multiple `SiteID` and `LocationID` values to be specified in each query. The maximum limit is defined by the following equation: `NumOf(SiteID)` &times; `NumOf(LocationID)` &le; 100.
- The `fno` data source is reserved for Supply Chain Management. If your Inventory Visibility Add-in is integrated with a Supply Chain Management environment, we recommend that you not delete configurations that are related to `fno` in the [data source](inventory-visibility-configuration.md#data-source-configuration).
- Inventory Visibility can't change any data for the `fno` data source. The data flow is one-way, which means that all quantity changes for the `fno` data source must come from your Supply Chain Management environment. Therefore, you can't use the API to send on-hand change or reservation requests for the `fno` data source.
- If you add one or more new measures to your Supply Chain Management environment, you should also add them in Inventory Visibility. However, all quantity changes for new measures must come from your Supply Chain Management environment.
- A [partition configuration](inventory-visibility-power-platform.md#partition-configuration) controls how data is distributed. Operations that are performed inside the same partition provide better performance, at lower cost, than operations that cross partitions. By default, partition configuration is automatically set up and should not be customized.
- Base dimensions that are reserved in a partition configuration (set number *0*) should not be included in other [on-hand index configurations](inventory-visibility-power-platform.md#index).
- Your [on-hand index configuration](inventory-visibility-power-platform.md#index) must include at least one on-hand index besides the partition configuration (set number *0*). If you aren't interested in querying specific dimension combinations, you can set up an index that has only one base dimension, `Empty`. Otherwise, queries fail, and you receive the following error: "No index hierarchy has been set."
- Data source `@iv` is a predefined data source and the physical measures defined in `@iv` with prefix `@` are predefined measures. These measures are a predefined configuration for the allocation feature, so don't change or delete them or you're likely to encounter unexpected errors when using the allocation feature.
- You can add new physical measures to the predefined calculated measure `@iv.@available_to_allocate`, but you must not change its name.
- If you restore a Supply Chain Management database, then your restored database might contain data that's no longer consistent with data previously synced by Inventory Visibility to Dataverse. This data inconsistency can cause system errors and other issues. Therefore, it's important that you always clean all related Inventory Visibility data from Dataverse before you restore a Supply Chain Management database. For details, see [Clean Inventory Visibility data from Dataverse before restoring the Supply Chain Management database](inventory-visibility-setup.md#restore-environment-database).

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
