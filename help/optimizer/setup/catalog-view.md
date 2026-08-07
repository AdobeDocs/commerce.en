---
title: Catalog views
description: Learn what catalog views are and how to create them to organize your product catalog by business structure, policies, and pricing.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
---
# Catalog views for Merchandising Services

A catalog view defines the products and pricing that a client can retrieve. It combines catalog sources, catalog layers, policies, and price books to support different brands, regions, business units, or channels.

## What are catalog views?

Catalog views define how your product catalog is organized and displayed. They act as filters that determine:

- **Which products are visible** based on business structure (brands, regions, dealers)
- **What pricing is shown** through linked price books
- **How products are filtered** using policies (attributes like brand, model, category)
- **What [catalog source](catalog-sources.md) is used** based on attributes like locale
- **Who can access the view's data** through [Catalog Protection](private-catalog-view.md) and [restricted access keys](restricted-access-keys.md)

For example, you can create separate catalog views for:

- A brand or business unit
- A geographic region
- A dealer or partner channel
- A customer segment with specific pricing

## Create a catalog view

Before creating a catalog view, prepare the following items as needed:

- A [catalog source](catalog-sources.md)
- [Policies](policies.md) that define product filters
- [Catalog layers](catalog-layer.md) if you need to override product attributes
- [Price books](pricebooks.md) for the pricing displayed in the view
- [Restricted access keys](restricted-access-keys.md) if you want to create a private catalog view

### Configuration

In this section, you create a catalog view, select a [policy](policies.md), and a [price book](pricebooks.md).

1. From the left menu, go to _Store setup_ , and click **[!UICONTROL Catalog views]**.

1. Click **[!UICONTROL Create catalog view]**. ​

1. Configure the catalog view details:

    - **Name**—Enter the name of the catalog view, for example `Celport`. ​
    - **Catalog sources**—Select the [catalog source](catalog-sources.md), for example `en-US`.
    - **Catalog layers**—Review ingested layers and priority.
    - **Policies**—Use the drop-down to select the relevant policies. For example, "Brand," "Model". ​Make sure you have already [created a policy](policies.md).

1. Select the price book to link to the catalog view.

    - **Use all available price books**—This option pulls pricing data from all available price books.
    - **Allow selected price books only**—This option displays the **Add allowed price books** dialog. Use this dialog to select which specific price book to use for the catalog view.
    - **Disable pricing**—This option is not available at this time.

   >[!NOTE]
   >
   >A price book ID controls which pricing is requested. It does not restrict access to the catalog view. To restrict access, enable Catalog Protection to create a [private catalog view](private-catalog-view.md).

1. (Optional) Toggle **[!UICONTROL Catalog Protection]** to **[!UICONTROL Enabled]** to restrict this catalog view's data to clients with a valid signed token. See [Protect a catalog view](private-catalog-view.md#protect-a-catalog-view) for setup steps.

1. Click **[!UICONTROL Add]** to create the catalog view with the linked price books and policies.

The Catalog views page updates to display the new catalog view.​

After you complete these steps, the catalog view is now configured to display products and pricing based on your selected sources and policies.

### Specify catalog views for recommendations and product discovery rules

You can specify a catalog view when you [create recommendation units](../merchandising/recommendations/create.md) or [merchandising rules](../merchandising/rules/add.md).

## Catalog layers

Catalog layers let you override selected product attributes without changing the source catalog data. Use layers to customize names, descriptions, images, links, or metadata for a catalog view.

See [Catalog layers](catalog-layer.md).

## Make a catalog view private

By default, a catalog view is public to client applications that can access the GraphQL Merchandising API. To restrict access, configure a private catalog view by enabling **[!UICONTROL Catalog Protection]**.

To learn how to protect a catalog view and verify that access is enforced, see [Private catalog views](private-catalog-view.md).

## Manage catalog views

To update or view the properties of existing catalog views, follow these instructions.

### Edit a catalog view

1. In the *Catalog views* workspace, locate the catalog view.
1. To open the actions menu, select (**[!UICONTROL ...]**).
1. Select **Edit** to access the catalog view editor.
1. Update the name, catalog sources, policies, price book information, and **[!UICONTROL Catalog Protection]** settings (including assigned restricted access keys) as needed.
1. Save the changes.

### Delete a catalog view

1. In the *Catalog views* workspace, locate the catalog view.
1. To open the actions menu, select (**[!UICONTROL ...]**).
1. Select **Delete**.
1. Confirm the deletion.

   When the confirmation dialog appears, click **[!UICONTROL Delete]**.

### View catalog view details

This option provides a quick way to see all the catalog view parameters, while staying on the *Catalog views* table.

In the **Catalog views** workspace, select the ![information icon](../assets/info-icon.png) for a catalog view to view its configuration details.

![Catalog view details](../assets/catalog-view-details.png)

From here you can see catalog view configuration details, such as:

- View ID
- Name
- Catalog sources
- Policies
- Date Created
- Data Modified

Some of these configuration settings are needed as you set up your storefront or use the data ingestion API.

## Architecture overview

Catalog views are part of the Merchandising Services framework that replaces the website, store, storeview framework used in Adobe Commerce foundations with a more flexible model:

![[!DNL Merchandising Services] Architecture](../assets/merchandising-svcs-architecture.png)

### How it works

**1. Data Ingestion**
Catalog data from PIM, ERP, and other systems is ingested into the Merchandising Services framework. Each SKU contains locale information and product attributes that map to catalog views, policies, and locales. For more information about data ingestion, see the [developer documentation](https://developer.adobe.com/commerce/services/optimizer/).

**2. Unified Base Catalog**
The ingested data creates a unified base catalog in the Catalog Service data pipeline. This single source eliminates data duplication across business units.

**3. Catalog Views**
Multiple catalog views represent different business units (for example, "Texas Retail," "Texas Retail Seasonal"). Locales, policies, and price books can be shared across catalog views for flexibility.

**4. Multi-Channel Delivery**
The filtered catalog data is delivered to destinations like Edge Delivery Services, marketplaces, advertising platforms, and custom micro-storefronts. For more information about catalog data delivery, see the [developer documentation](https://developer.adobe.com/commerce/services/optimizer/).

When a catalog view has **[!UICONTROL Catalog Protection]** enabled, delivery to that destination requires a valid signed token from an assigned [restricted access key](restricted-access-keys.md); unauthorized requests are denied instead of receiving catalog data.

### Key components

|Component|Purpose|Example|
|---|---|---|
|**Catalog view**|Business unit or distribution channel|Dealer network, Regional store|
|**Policy**|Product filter based on attributes|Brand, Model, Category|
|**Locale**|Language/region setting|en-US, fr-CA, es-MX|
|**Price Book**|Pricing structure|Retail, Wholesale, Employee|
|**Restricted access key**|Signed-token credential that gates access to a protected catalog view|Partner portal key, B2B pricing key|

### Data flow

1. **Ingest** - Product data from PIM/ERP systems
2. **Process** - Apply catalog views, policies, and pricing
3. **Deliver** - Serve filtered catalog to storefronts, marketplaces, etc.

## Key features

|Feature|Benefit|
|---|---|
|**Single Base Catalog**|Eliminate data duplication across business units|
|**Flexible Pricing**|Multiple price books per SKU for different customer segments|
|**Scalable**|Manage 200M+ SKUs efficiently|
|**Multi-Channel**|Serve catalogs to storefronts, marketplaces, and advertising platforms|
|**Real-time Updates**|Quickly update catalog data for promotions and campaigns|
|**Private catalog views**|Restrict a catalog view to authorized clients using signed-token validation|

## Use cases

### Multi-brand conglomerate

**Challenge**: Manage multiple brands, countries, and languages<br>
**Solution**: Single catalog with catalog views for each brand/region combination

### Automotive parts dealer

**Challenge**: 3,000 dealers with same products but different pricing<br>
**Solution**: One catalog with dealer-specific catalog views and price books

### Multi-location retailer

**Challenge**: Different pricing and inventory per location<br>
**Solution**: Location-based catalog views with region-specific policies

>[!INFO]
>
>For detailed information about catalog data ingestion and delivery, see the [developer documentation](https://developer.adobe.com/commerce/services/optimizer/).

## More like this

- [Catalog sources](catalog-sources.md)—Define the authoritative scope of products, attributes, and categories for search, filter, and sort behavior
- [Catalog layers](catalog-layer.md)—Learn how to modify product data without changing the original source
- [Private catalog views](private-catalog-view.md)—Create a private catalog view to restrict access to authorized clients
- [Restricted access keys](restricted-access-keys.md)—Create, assign, and rotate the keys used to sign tokens for Catalog Protection
- [Policies](policies.md)—Create policies to filter products in catalog views
- [Price books](pricebooks.md)—Manage pricing structures for different customer segments
