---
title: Available Data
description: Use financial reporting data to reconcile reporting with non-Commerce systems.
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
---
# Available Data

Some order and payouts data is available to you so that you can coordinate Adobe Commerce financial reporting across external systems.

## Reconcile with ERP system

You can reconcile Adobe Commerce financial reporting with your non-Adobe Enterprise Resource Planning (ERP) system using the increment ID associated with a specific order.

When Payment Services sends the Commerce order to PayPal, the increment ID is included as the `custom_id` _and_ in the `invoice_id` (which also contains a random string after the `increment_id`).

The IDs are easily accessible in both the merchant activity detail for a payout and in the PayPal webhook.

The `invoice_id` and `custom_id` are displayed near the bottom of the merchant activity detail for a payout:

![`custom_id` in merchant activity detail](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

`custom_id` and `invoice_id` in the details in PayPal's webhook:

``` json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

See PayPal's REST APIs documentation for more information:

* [`purchase_unit`, in which `custom_id` and `invoice_id` reside](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [Show order details](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
