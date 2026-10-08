---
title: Tracking your shipments in [!DNL Payment Services]
description: Customize [!DNL Payment Services] shipments and tracking information displayed in the Paypal Merchant Dashboard.
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
---
# Tracking your shipments in [!DNL Payment Services]

[!DNL Payment Services] enables merchants to see the tracking information for a shipment in their PayPal Merchant Dashboard.

See [shipments](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank} topic for more information on the shipments grid for Adobe Commerce.

## How tracking your shipment works

This functionality is dependent on whether the order has been invoiced, as PayPal must receive a `capture_id` to process the tracking information. If a merchant ships their products before capture, the tracking information is not sent to PayPal.

>[!NOTE]
>
> It is recommended to create one shipment per tracking number, associating the correct items with the shipment.

## Adding the tracking number

The following instructions will walk you through the process to create a shipment in Adobe Commerce with [!DNL Payment Services]:

1. On the _Admin_ sidebar, go to **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.

1. In the **[!UICONTROL Action]** column for the selected order, click **[!UICONTROL View]**.

1. Click **[!UICONTROL Ship]**.

1. Scroll down to the **[!UICONTROL Payment & Shipping Method]** block and click **[!UICONTROL Add Tracking Number]** in **[!UICONTROL Shipping Information]**.

1. Set the **[!UICONTROL Carrier]**.

1. To track the shipment, enter the **[!UICONTROL Title]** and **[!UICONTROL Number]** .

1. Click **[!UICONTROL Submit Shipment]**.

>[!NOTE]
>
> Alternatively, you may be using a shipping module to enter the tracking number information. Ensure that the shipping module is saving the tracking number information in the `tracking_number` field.

### Compatibility with third parties

Any third-party extension is compatible with the functionality when a shipment entity is created through [Commerce API](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}.
