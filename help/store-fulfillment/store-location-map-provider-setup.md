---
title: Store Location and Mapping System Configuration
description: Configure a distance provider to support store location mapping in the storefront UI. The Store Fulfillment solutions requires a distance provider to enable retail store search and other mapping and scheduling capabilities for the end-to-end fulfillment workflow.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
exl-id: 6ceafdac-b409-458b-ad65-fb22c1bcadc2
---
# Store Location and Mapping Setup

Enable the store location and mapping capabilities for Store Fulfillment by configuring a [distance provider](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/distance-priority-algorithm) to search for retail store locations.

**Requirements**

During the configuration process, you provide a Google API key for the Google Maps platform. If you do not have one, [generate one from the Google Maps platform](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps).

To configure the distance provider:

1. From the **[!UICONTROL Stores > General]** configuration in the Admin, add the Google Maps integration for the Map content type.

   - Go to **[!UICONTROL Stores > Configuration  > General > Content Management]**.

   - Add your Google API Key to **[!UICONTROL Google Maps API Key]** field.

1. From the **[!UICONTROL Stores > Inventory]** configuration in the Admin, select the distance provider for Store Fulfillment.

   - Go to **[!UICONTROL Stores > Configuration > Catalog > Inventory]**.

   - Expand the **[!UICONTROL Distance Provider for Distance Based SSA]** section.

   - Set the **Provider** to **Google Map**.

1. Configure settings for the **[!UICONTROL Google Distance Provider]**.

   - Add your **Google API key**.

   - Set **[!UICONTROL Computation Mode]** to `Driving` and **[!UICONTROL Value]** to `Distance`
