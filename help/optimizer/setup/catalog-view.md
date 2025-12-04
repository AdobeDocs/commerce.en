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

1. Click **[!UICONTROL Add]** to create the catalog view with the linked price books and policies.

The Catalog views page updates to display the new catalog view.​

After you complete these steps, the catalog view is now configured to display products and pricing based on your selected sources and policies.

Catalog overlays (also called catalog layers) allow you to modify product data without changing the original source data. Overlays apply changes to specific product attributes—such as name, description, images, links, and metadata—by creating a layer on top of your base catalog. This non-destructive approach ensures your original product data remains intact while allowing flexible customizations for different use cases.

### How catalog overlays work

When a customer views your storefront, the system combines your base catalog data with active catalog overlays to display the final product information. Here's how the process works:

1. **Layer application**—When a request is made with a channel ID and environment ID, the store service retrieves the relevant catalog view.

1. **Data merging**—The system applies catalog overlays to product data based on layer priority order.

1. **Field handling**—Different field types are processed differently:
   
   - **Override fields**—Text fields like name, description, and meta titles are replaced by the overlay value (higher-priority layer wins).
   - **Merge fields**—Array fields like images, links, and attributes are combined from multiple layers, providing a unified response.

1. **Priority resolution**—The order field determines which layer takes precedence. Higher order numbers have higher priority when multiple layers modify the same field.

### Overlay use cases

Catalog overlays are commonly used for:

- **SEO optimization**—Override product meta titles and descriptions based on AI recommendations from Sites Optimizer.
- **Seasonal campaigns**—Temporarily update product names, descriptions, or images for promotions without changing source data.
- **Regional customization**—Display different product information based on geographic location or language.
- **A/B testing**—Test different product presentations to optimize conversion rates.
- **Multi-brand management**—Customize product attributes for different brand catalog views.

### Add an overlay via data ingestion

You can add catalog overlays to your products during the data ingestion process. This method is ideal for bulk operations or automated workflows.

**Prerequisites:**

- API credentials with permission to access the data ingestion service
- Product SKUs that already exist in your base catalog

**Steps:**

1. Prepare your overlay data in the required format with the product attributes you want to modify.

1. Use the Product Layers API endpoint to ingest the overlay data.

1. Verify the overlay was successfully ingested by checking the catalog view configuration.

For detailed API specifications and payload examples, see [Product Layers](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) in the developer documentation.

### Add an overlay manually in the UI

The catalog view UI allows you to manually create and manage overlays, which is particularly useful for integrations like Sites Optimizer that generate AI-powered recommendations.

>[!NOTE]
>
>Manual overlay creation in the UI is primarily used for Sites Optimizer integration. For bulk overlay operations, use the data ingestion API method described above.

**To create a manual overlay:**

1. Navigate to **Store setup** > **Catalog views**.

1. Select the catalog view where you want to apply the overlay.

1. In the catalog layers section, click **Add layer**.

1. Configure the overlay properties:
   
   - **Layer name**—Enter a descriptive name to identify the overlay purpose.
   - **Products**—Select the products to which this overlay applies.
   - **Attributes**—Choose which product attributes to modify (name, description, images, meta tags, etc.).
   - **Values**—Enter the new values for each selected attribute.

1. Click **Save** to create the overlay.

The new overlay is added to the catalog view and is automatically assigned the next available order number.

### Manage overlay priorities

The order in which overlays are applied determines which values appear on your storefront when multiple overlays modify the same product attribute. Managing priorities ensures the correct data is displayed.

**Understanding priority order:**

- Each overlay has an order number (1, 2, 3, and so on.)
- Lower order numbers take precedence over higher numbers
- Order 1 is the highest priority; lower numbers override higher ones
- Only applies to override fields (name, description, meta tags)
- Merge fields (images, links, attributes) combine data from all layers


- **Non-destructive changes**—Auto-fix creates optimization layers that override product attributes without modifying the original product data.
- **Priority ordering**—Layers are prioritized by order number. Order 1 (highest priority) takes precedence over lower-priority layers.
- **Layer updates**—If you apply additional suggestions to the same product, the existing layer is updated with new attributes rather than creating duplicate layers.
- **Manual management**—You can manually adjust layer priorities through your catalog view settings, though this may affect which optimizations are applied.
- **Adobe Sites Optimizer layer**—If an Adobe Sites Optimizer (ASO) layer does not exist in your catalog view, auto-fix automatically creates one and assigns it order 1 (highest priority). If you delete this layer, it will be recreated the next time auto-fix runs and will shift existing layers to lower order numbers. If the ASO layer already exists at a different order number, auto-fix will not change its priority.


**To reorder overlay priorities:**

1. Navigate to **Store setup** > **Catalog views**.

1. Select the catalog view containing the overlays you want to reorder.

1. In the catalog layers section, locate the overlay you want to move.

1. Drag and drop the overlay to change its position, or use the reorder controls.

1. The system automatically updates order numbers based on the new sequence.

1. Click **Save** to apply the new priority order.

>[!IMPORTANT]
>
>Changes to overlay priority take effect immediately and may impact what customers see on your storefront. Review the preview before saving to ensure the correct values are applied.

### Preview overlay effects

Before activating overlays or changing priorities, you can preview how they affect product data.

**To preview overlay changes:**

1. Navigate to **Store setup** > **Catalog views**.

1. Select the catalog view with the overlays you want to preview.

1. In the catalog layers section, select a specific product or use the preview function.

1. Review the combined product data showing how overlays modify the base catalog values.

1. Make adjustments to overlay content or priority order as needed.

### Activate or deactivate overlays

You can enable or disable catalog overlays without deleting them, allowing you to control when specific customizations are applied.

**To activate or deactivate an overlay:**

1. Navigate to **Store setup** > **Catalog views**.

1. Select the catalog view containing the overlay.

1. In the catalog layers section, locate the overlay you want to toggle.

1. Click the activation toggle to enable or disable the overlay.

   - **Active**—The overlay is applied to product data.
   - **Inactive**—The overlay is preserved but not applied to product data.

1. The change takes effect immediately on your storefront.

### Best practices

Follow these recommendations when working with catalog overlays:

- **Use descriptive names**—Name overlays clearly to indicate their purpose (e.g., "Holiday 2024 Campaign" or "SEO Optimization - Product Pages").

- **Limit overlay layers**—While the system supports multiple overlays, using too many can impact performance. Consolidate overlays when possible.

- **Test before activating**—Always preview overlay effects before activating them on your live storefront.

- **Document priority logic**—Keep track of which overlays should take precedence to avoid unintended overrides.

- **Review Sites Optimizer overlays**—When using auto-fix from Sites Optimizer, the system creates overlays at the highest priority. Be mindful when adding manual overlays that might override AI recommendations.

- **Monitor performance**—If you notice slow product page loads, review your overlay configuration and consider consolidating layers.

## Manage catalog view

Follow these instructions to update or view the properties of existing catalog views.

### Edit catalog view

1. On the *Catalog views* workspace, find the catalog view in the grid that you want to edit and click **...** to open the actions menu.
1. Click **Edit** to access the catalog view editor.
1. Update the name, catalog sources, policies, and price book information as needed.
1. Save the changes.

### Delete catalog view

1. In the *Catalog views* workspace, find the catalog view in the grid that you want to edit and click **...** to open the actions menu.
1. Click **Delete**.

    When the confirmation dialog appears, click **[!UICONTROL Delete]**.

### View details

This option provides a quick way to see all the catalog view parameters, while staying on the *Catalog views* table.

On the *Catalog views* worksapce, find the catalog view in the grid that you want to edit and click the ![information icon](../assets/info-icon.png).

![Catalog View Details](../assets/catalog-view-details.png)

From here you can see catalog view configuration details, such as:

- View ID
- Name
- Catalog sources
- Policies
- Date Created
- Data Modified

Some of these configuration settings are needed as you set up your storefront or use the data ingestion API.

## Architecture Overview

Catalog views are part of the Merchandising Services framework that replaces the website, store, storeview framework used in Adobe Commerce foundations with a more flexible model:

![[!DNL Merchandising Services] Architecture](../assets/merchandising-svcs-architecture.png)

### How It Works

**1. Data Ingestion**
Catalog data from PIM, ERP, and other systems is ingested into the Merchandising Services framework. Each SKU contains locale information and product attributes that map to catalog views, policies, and locales. For more information about data ingestion, see the [developer documentation](https://developer.adobe.com/commerce/services/optimizer/).

**2. Unified Base Catalog**
The ingested data creates a unified base catalog in the Catalog Service data pipeline. This single source eliminates data duplication across business units.

**3. Catalog Views**
Multiple catalog views represent different business units (for example, "Texas Retail," "Texas Retail Seasonal"). Locales, policies, and price books can be shared across catalog views for flexibility.

**4. Multi-Channel Delivery**
The filtered catalog data is delivered to various destinations including Edge Delivery Services storefronts, marketplaces, advertising platforms, and custom micro-storefronts. For more information about catalog data delivery, see the [developer documentation](https://developer.adobe.com/commerce/services/optimizer/).

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
>For detailed information about catalog data ingestion and delivery, see the [developer documentation](https://developer.adobe.com/commerce/services/optimizer/).
