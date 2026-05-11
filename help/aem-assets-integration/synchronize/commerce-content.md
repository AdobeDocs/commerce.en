---
title: Maintain accurate and relevant content
description: An eCommerce platform is one of the most crucial engagement channels. Ensuring seamless updates in the asset management system guarantees that commerce storefronts always display the most up-to-date product information.
feature: CMS, Media, Integration
exl-id: 2c749e84-fcc4-4bf9-90b2-87438329889e
TQID: https://experienceleague.adobe.com/cTeAl0vABSDcqSR9S7pGkV2yGnFHz11VmXtPoE0C86M
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
---
# Maintain accurate and relevant content

A true content supply involves a combination of key pillars across **Creation and Production**, **Workflow and Planning**, and **Delivery and Activation**. Each of these pillars is valuable on its own and helps drive significant value for organizations:

![Key Pillars](../assets/key-pillars.png){width="600" zoomable="yes"}

An eCommerce platform is one of the most crucial engagement channels. Ensuring seamless updates in the asset management system guarantees that commerce storefronts always display the most up-to-date product information. This is essential to achieving the three main objectives of any **DAM (Digital Asset Management system)** <> **Commerce integration**:

* Improve **Time-to-Market (TTM)** for new product launches.

* Eliminate operational inefficiencies and reduce manual interactions.

* Ensure brand consistency by always serving approved content that aligns with brand guidelines.

To achieve these objectives, the AEM Assets integration for Commerce is subscribed to both **Adobe Commerce** and **AEM Assets** events, ensuring dynamic synchronization between content and commerce.

## Adobe Commerce Catalog Changes

The AEM Assets integration listens for product creation events triggered when products are created in the  **Admin** or by using the **API**. When triggered, it syncs approved assets from the DAM that are associated with the new product SKU.

By decoupling content creation from catalog management, businesses gain several advantages:

* Content teams can operate independently, ensuring that high-quality assets are ready for product launches.

* Product updates remain fast because asset creation does not delay catalog changes, enabling greater agility in managing new products.

* Automation improves efficiency and accuracy, reducing mismatches between product data and associated content.

>[!NOTE]
>
> CSV product imports in PaaS and SaaS do not trigger update events. Use the API for catalog imports and updates.

## AEM Assets Lifecycle Changes

The integration also listens for asset status changes in AEM Assets. Because Adobe Commerce serves as an engagement channel, only approved assets are displayed in the storefront.

The integration automates asset lifecycle management to ensure that storefront content remains accurate and brand-compliant.

* Only approved assets are published, maintaining brand integrity and regulatory compliance.

* Outdated or irrelevant assets are automatically removed, preventing stale content from appearing.

* Seamless synchronization between asset approval and product display reduces manual efforts and delays.

By leveraging the AEM Asset Selector integration, businesses can maintain a streamlined, accurate, and efficient content supply change—enhancing both customer experience and operational efficiency.
