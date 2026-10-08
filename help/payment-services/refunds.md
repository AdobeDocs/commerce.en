---
title: Refunds
description: Create refunds for [!DNL Payment Services] orders in the Admin as part of the credit memo process.
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
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
# Refunds

Refunds for [!DNL Payment Services] orders are created in the Admin as part of the credit memo process. A credit memo is a document that shows the amount that is due to the customer, for a full or partial refund, which can be applied toward a purchase or refunded directly to the customer. Credit memos can only be issued for orders that are [invoiced](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}.

See [Credit Memos](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"} in our core user guide for more information and to learn how to issue and print credit memos.

For orders processed with PayPal or a credit card you can:

* Refund the entire amount of the order
* Refund a partial amount of an order (or multiple partial amounts)
* Refund an amount less than the value of a specific order item

See [Issuing a Credit Memo](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"} in our core user guide for more information.

>[!NOTE]
>
>An error occurs for PayPal or credit card-processed orders if you attempt to partially refund an order for more than the remaining order amount (original amount minus the total of existing refunds), or if you issue a refund for an amount greater than the full order amount.

The [!UICONTROL Payment Action] setting in your [!UICONTROL Payment Settings] configuration---Either `Authorize` or `Authorize and Capture`---determines the [basic refund workflow](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"} for orders.

See the [Payment action setting section](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"} of _Issuing a Credit Memo_ for more information.
