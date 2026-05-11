---
title: Handle Cookie Restrictions
description: Learn how Product Recommendations handle cookie restrictions and privacy compliance.
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
TQID: https://experienceleague.adobe.com/qqgwO4KI4koSBcYu9mdrjb6AQFW4guxk6dfLDBEwVb8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
    internal-label: Behavioral data
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
---
# Handle Cookie Restrictions

Both Adobe Commerce and Magento Open Source ask for consent before data is stored in browser cookies. For more information, refer to [Cookie restriction mode](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html).

## How Product Recommendations handle cookie restrictions

When you deploy the `magento/product-recommendations` module to production, it begins collecting shopper interaction events on your storefront. This data can be stored in browser cookies or local storage to power recommendation algorithms.

>[!IMPORTANT]
>
>Product Recommendations now respects cookie restriction mode by not collecting or storing any data in cookies or local storage when cookie restrictions are enabled. This includes behavioral data used for personalized recommendations.

### Data affected by cookie restrictions

The following Product Recommendations data is not collected when cookie restriction mode is enabled:

- **Behavioral data**: Product views, add-to-cart actions, purchases, and other shopper interactions.
- **Session data**: Shopper session information and recommendation unit interactions.
- **Personalization data**: Data used for recommendation types like "Recently viewed" and "Most purchased".

### Impact on recommendation types

When cookie restriction mode is enabled and shoppers haven't accepted cookies, certain recommendation types may not display or may show limited results:

- **Recently viewed products**: Requires session data stored in cookies/local storage.
- **Recommended for you**: Requires behavioral data for personalization.
- **Bought this, bought that**: Requires purchase history data.

>[!NOTE]
>
>Recommendation types that do not rely on behavioral data, such as "Most viewed" and "Visual similarity" will continue to work normally even with cookie restrictions enabled.

## Third-party cookie consent solutions

Product Recommendations may not automatically integrate with third-party cookie consent solutions. It is the merchant's responsibility to ensure that data collection complies with applicable privacy laws and regulations.

If you use a custom cookie consent solution, you can implement the do-not-track cookie mechanism to control data collection.

### Implementing do-not-track cookies

You can use the `mg_dnt` cookie to programmatically control data collection:

#### Cookie name

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### Disable data collection

Set the do-not-track cookie when users decline cookies:

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### Enable data collection

Clear the do-not-track cookie when users accept cookies:

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## Testing cookie restriction mode

To test how Product Recommendations behave with cookie restrictions:

1. Enable cookie restriction mode in your Adobe Commerce configuration.
1. Visit your storefront without accepting cookies.
1. Verify that recommendation units display appropriate fallback content.
1. Accept cookies and verify that recommendations begin collecting data.

## Privacy compliance

Product Recommendations data collection does not include personally identifiable information (PII). All user identifiers, such as cookie IDs and IP addresses, are anonymized. For more information, see the [Adobe Privacy Policy](https://www.adobe.com/privacy/policy.html).

>[!TIP]
>
>For healthcare customers using the Data Services HIPAA extension, additional configuration may be required. See [HIPAA Readiness](../data-connection/hipaa-readiness.md) for more information.
