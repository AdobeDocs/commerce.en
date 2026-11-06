---
title: Set Up Commerce Services
description: Learn how to connect Adobe Commerce to merchandising services and Magento Open Source to Payment Services using the Commerce Services Connector.
role: Admin, Developer
feature: Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:14:04.410Z'
TQID: 'https://experienceleague.adobe.com/yyUDw1y5CYHxdLlC3bNo0DKK0byamPAKUjK-wwxVEX4'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
---

# Set up Commerce services

Adobe Commerce on cloud infrastructure and on-premises projects connect to services such as [!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations], and [!DNL Payment Services] through the Commerce Services Connector. On [!DNL Adobe Commerce as a Cloud Service], this connection is configured automatically.

Magento Open Source uses the Commerce Services Connector for [!DNL Payment Services]. [!DNL Catalog Service], [!DNL Live Search], and [!DNL Product Recommendations] require Adobe Commerce and are not available for Magento Open Source.

>[!NOTE]
>
>Adobe Commerce Optimizer provides catalog and merchandising capabilities natively, instead of using the separate [!DNL Live Search], [!DNL Catalog Service], and [!DNL Product Recommendations] services. Its catalog synchronization does not require the Commerce Services Connector. Other integrations on the Commerce backend, such as [!DNL Payment Services] and [!DNL Data Connection], still require the connector. See [Enable Adobe Commerce Optimizer](enable-aco.md) for Optimizer setup.


## Getting started

1. Review the [Commerce Services Connector](/help/landing/saas.md) documentation to obtain and configure your API keys.

1. See the [Adobe Commerce Services Guides](/help/landing/home.md) for the individual services available through the connector.

## Related guidance

- [Configure payments](configure-payments.md)
- [Connect AEM Assets](connect-aem-assets.md)
- [Integrate with Adobe Experience Platform](integrate-aep.md)
