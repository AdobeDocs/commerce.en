---
title: Overcapture
description: Learn about overcapture requirements and configuration for the Payment Services extension.
role: Admin, User
level: Intermediate
feature: Payments, Paas
---
# Overcapture

Overcapture allows eligible merchants with a PayPal overcapture agreement to capture more than the originally authorized amount when invoicing an order. For example, the final amount might increase because of weight-based adjustments or changes in material costs between authorization and fulfillment.

PayPal determines the overcapture limit for each merchant account. Enabling overcapture in [!DNL Payment Services] does not establish an agreement or increase the limit approved by PayPal.

>[!NOTE]
>
>This topic describes overcapture in the [!DNL Payment Services] extension. For [!DNL Adobe Commerce as a Cloud Service], see [Custom capture amounts](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) for the separate availability and enablement requirements.

## Prerequisites

Before enabling overcapture:

* Overcapture is only available in [!DNL Payment Services] 2.17.0 or later.
* Overcapture is only available to US-based businesses. PayPal's [overcapture requirements (PSD2)](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954) also apply to US-based merchants selling to PayPal buyers in the European Economic Area (EEA).
* Overcapture is not available for alternative payment methods (APMs).
* Obtain an overcapture agreement with PayPal and confirm the limit approved for your merchant account with your PayPal account manager.
* Set the payment method's **[!UICONTROL Payment Action]** to `Authorize`. Overcapture applies to authorized orders captured later during invoicing, not to orders automatically captured with `Authorize and Capture`. See [Set [!DNL Payment Services] as payment method](production.md#set-payment-services-as-payment-method).

## Enable overcapture

1. On the _Admin_ sidebar, go to **[!UICONTROL Stores]** > _[!UICONTROL Settings]_ > **[!UICONTROL Configuration]**.
1. In the left panel, expand **[!UICONTROL Sales]** and choose **[!UICONTROL Payment Methods]**.
1. Select the website to configure using the store scope selector.
1. Expand the _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_ section.
1. In the _[!UICONTROL Payment Services]_ section, expand the _[!UICONTROL General Configuration]_ section.
1. Set **[!UICONTROL Over Capture Enabled]** to `Yes`.
1. Click **[!UICONTROL Save Config]** to save your changes.
1. Navigate to **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, and then click **[!UICONTROL Flush Cache]** to refresh all invalid caches.

## Capture an authorized payment

Overcapture takes place during invoicing in the Admin. The requested capture amount must be within the limit approved by PayPal for your merchant account. See [Create an invoice](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice) for the standard invoicing workflow.

1. On the _Admin_ sidebar, go to **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. Open an order with an authorized payment that has not yet been captured.
1. Click **[!UICONTROL Invoice]**.
1. In the custom capture amount field, enter the total amount to capture. For example, if the authorized amount is USD 100 and the agreed final charge is USD 110, enter `110`, not `10`. The requested amount must be within your PayPal-approved limit.
1. Select online capture for the invoice to request payment through the payment provider.
1. Review the invoice and click **[!UICONTROL Submit Invoice]**.

### Capture using the Invoice API

Use the standard [Create an invoice](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice) endpoint:

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

Use the store code for the order and the order's internal ID. Authenticate with an authorized Admin or integration token and set `Content-Type: application/json`.

The following example payload requests a full invoice with online capture of USD 110 for an order authorized for USD 100, provided the merchant's PayPal agreement permits that amount:

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

In this example: 

1. `capture` requests online capture.
1. `notify` controls whether Commerce sends the invoice notification email.
1. `custom_capture_amount` is the final amount to capture, not the increase over the authorized amount.

## Troubleshoot a rejected capture

If PayPal rejects an overcapture request:

* Confirm that an overcapture agreement is active for the PayPal merchant account used for the payment.
* Check that the requested amount is within the approved limit. If it exceeds the limit, request a lower amount or contact your PayPal account manager to discuss an increase.
