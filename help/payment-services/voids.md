---
title: Voids
description: Voids allow you to free the funds in a credit or debit card account that are blocked or held aside by an authorization for the amount of a purchase.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
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
# Voids

[!DNL Payment Services] supports Commerce's existing functionality for voiding transactions. A void releases funds in a credit or debit card account that are being held by an authorization for the purchase amount. Transactions can only be voided if payment has not yet been captured.

* If your store is [configured](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} to authorize only (not capture) funds at the point of sale, a purchase from your store results in an order with a `Processing` status in the Commerce Admin.

* You can also [cancel an order](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} that is not invoiced. Any uncaptured authorizations are also voided as part of that cancellation process.

>[!NOTE]
>
>Canceling an order also produces a void, but voiding an order does not trigger a cancellation.

To learn more about the basic steps an order goes through, see the [Order Workflow](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} topic in the core user guide.

To learn about the void functionality and how to void an order transaction, see [Processing an Order](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} in the core user guide.
