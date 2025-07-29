---
title: Catalog View
description: Learn what catalog views are and how to create them to organize your product catalog by business structure, policies, and pricing.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
---

# Catalog Views for Merchandising Services

Catalog views are the foundation of Adobe Commerce Optimizer Merchandising Services, enabling you to organize your product catalog by business structure, policies, and pricing. This flexible data model supports multi-brand, multi-business unit, and multi-language scenarios while maintaining operational efficiency.

## What are Catalog Views?

Catalog views define how your product catalog is organized and displayed. They act as filters that determine:

- **Which products are visible** based on business structure (brands, regions, dealers)
- **What pricing is shown** through linked price books
- **How products are filtered** using policies (attributes like brand, model, category)
- **What catalog source is used** based on attributes like locale
  
Think of catalog views as different "lenses" through which customers see your catalog. For example:

- A dealer catalog view might show only products available to that specific dealer
- A regional catalog view might show products and pricing specific to a geographic area
- A brand catalog view might show only products from a particular brand

## Create a Catalog View

In this section, you create a catalog view, select a [policy](policies.md), and a [price book](pricebooks.md).

Before creating a catalog view, ensure you have:

- [Created policies](policies.md) to define product filters

- [Ingested price books](pricebooks.md) for pricing

1. From the left menu, go to _Store setup_ , and click **[!UICONTROL Catalog views]**.

1. Click **[!UICONTROL Create catalog view]**. ​

1. Configure the catalog view details:

    - **Name**—Enter the name of the catalog view, for example `Celport`. ​
    - **Catalog sources**—Select the catalog source (locale), for example `en-US`.
    - **Policies**—Use the drop-down to select the relevant policies. For example, "Brand," "Model". ​Make sure you have already [created a policy](policies.md).

1. Select the price book to link to the catalog view.

    - **Use all available price books**-This option pulls pricing data from all available price books.
    - **Allow selected price books only**-This option displays the **Add allowed price books** dialog where you can select which specific price book to use for the catalog view.
    - **Disable pricing**-This option is not available at this time.

1. Click **[!UICONTROL Add]** to create the catalog view with the linked price book and policies.

The Catalog views page updates to display the new catalog view.​

After you complete these steps, the catalog view is now configured to display products and pricing based on your selected sources and policies.

## Architecture Overview

Catalog views are part of the Merchandising Services framework that replaces the website, store, storeview framework used in Adobe Commerce foundations with a more flexible model:

![[!DNL Merchandising Services] Architecture](../assets/merchandising-svcs-architecture.png)

### How It Works

**1. Data Ingestion**
Catalog data from PIM, ERP, and other systems is ingested into the Merchandising Services framework. Each SKU contains locale information and product attributes that map to catalog views, policies, and locales. For more information about data ingestion, see the [developer documentation](https://developer-stage.adobe.com/commerce/services/composable-catalog).

**2. Unified Base Catalog**
The ingested data creates a unified base catalog in the Catalog Service data pipeline. This single source eliminates data duplication across business units.

**3. Catalog Views**
Multiple catalog views represent different business units (for example, "Texas Retail," "Texas Retail Seasonal"). Locales, policies, and price books can be shared across catalog views for flexibility.

**4. Multi-Channel Delivery**
The filtered catalog data is delivered to various destinations including Edge Delivery Services storefronts, marketplaces, advertising platforms, and custom micro-storefronts. For more information about catalog data delivery, see the [developer documentation](https://developer-stage.adobe.com/commerce/services/composable-catalog).

### Key Components

|Component|Purpose|Example|
|---|---|---|
|**Catalog View**|Business unit or distribution channel|Dealer network, Regional store|
|**Policy**|Product filter based on attributes|Brand, Model, Category|
|**Locale**|Language/region setting|en-US, fr-CA, es-MX|
|**Price Book**|Pricing structure|Retail, Wholesale, Employee|

### Data Flow

1. **Ingest** - Product data from PIM/ERP systems
2. **Process** - Apply catalog views, policies, and pricing
3. **Deliver** - Serve filtered catalog to storefronts, marketplaces, etc.

## Key Features

|Feature|Benefit|
|---|---|
|**Single Base Catalog**|Eliminate data duplication across business units|
|**Flexible Pricing**|Multiple price books per SKU for different customer segments|
|**Scalable**|Manage 200M+ SKUs efficiently|
|**Multi-Channel**|Serve catalogs to storefronts, marketplaces, and advertising platforms|
|**Real-time Updates**|Quickly update catalog data for promotions and campaigns|

## Use Cases

### Multi-Brand Conglomerate

**Challenge**: Manage multiple brands, countries, and languages<br>
**Solution**: Single catalog with catalog views for each brand/region combination

### Automotive Parts Dealer

**Challenge**: 3,000 dealers with same products but different pricing<br>
**Solution**: One catalog with dealer-specific catalog views and price books

### Multi-Location Retailer

**Challenge**: Different pricing and inventory per location<br>
**Solution**: Location-based catalog views with region-specific policies

>[!INFO]
>
>For detailed information about catalog data ingestion and delivery, see the [developer documentation](https://developer-stage.adobe.com/commerce/services/composable-catalog).
