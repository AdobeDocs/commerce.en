---
title: Create Custom Events
description: Learn how to create custom events to connect your Adobe Commerce data to other Adobe DX products.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
---
# Create Custom Events

You can extend the [eventing platform](events.md) by creating your own storefront events to collect data unique to your industry. When you create and configure a custom event, it is sent to the [Adobe Commerce Events Collector](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector).

## Handle custom events

Custom events are supported for the Adobe Experience Platform only. Custom data is not forwarded to Adobe Commerce dashboards and metrics trackers.

For any `custom` event, the collector:

- Adds `identityMap` with `ECID` as a primary identity
- Includes `email` in `identityMap` as a secondary identity _if_ `personalEmail.address` is set in the event
- Wraps the full event inside an `xdm` object before forwarding to the Edge

Example:

Custom event published through Adobe Commerce Events SDK:

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

In Experience Platform Edge:

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> Using custom events may affect default Adobe Analytics reports.

## Handle event overrides (custom attributes)

For any event with a set `customContext`, the collector overrides joins fields set in the relevant contexts with fields in `customContext`. The use case for overrides is when a developer wants to reuse and extend contexts set by other parts of the page in already supported events.

Event overrides are only applicable when forwarding to Experience Platform. They are not applied to Adobe Commerce and Sensei analytics events. The Adobe Commerce Events Collector [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md) provides additional info.

>[!NOTE]
>
>When augmenting `productListItems` with custom attributes in Experience Platform event payloads, match products using SKU. This requirement does not apply to `product-page-view` events.

### Usage

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### Example 1 - adding `productCategories`

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### Example 2 - adding custom context before publishing event

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### Example 3 - the custom context set in the publisher overwrites the custom context previously set in Adobe Client Data Layer.

In this example, the `pageView` event will have **Custom Page Name 2** in the `web.webPageDetails.name` field.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### Example 4 - adding custom context to `productListItems` with events with multiple products

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

>[!NOTE]
>
> Overriding events with custom attributes may affect default Adobe Analytics reports.
