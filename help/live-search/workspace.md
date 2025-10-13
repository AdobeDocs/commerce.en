---
title: Setting up Live Search
description: The [!DNL Live Search] workspace is used to configure, manage, and monitor search performance.
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
---
# Setting up Live Search

The workspace is where you configure, manage, and monitor the performance of [!DNL Live Search]. The menu across the top provides access to the tools in each functional area. The available features reflect the current menu selection.

![Workspace](assets/workspace.png)

## Data collection

To ensure that each functional area on the workspace contains the correct data, you need to configure data collection based on the selected storefront implementation:

1. Luma - Data collection is available out-of-the-box.
1. Headless - Data collection must be configured manually, depending on storefront implementation.

If you are using a headless storefront, refer to the following documentation to get more information about the required events that you need to add:

- [Required events](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search) for Live Search dashboard.
- [Storefront events collector](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) that needs to be added as a prerequisite.
- [Examples](https://github.com/adobe/commerce-events/tree/main/examples) of the events structure.

### Healthcare customers

If you are a healthcare customer and you installed the [Data Services HIPAA extension](../data-connection/hipaa-readiness.md#installation), which is part of the [Data Connection](../data-connection/overview.md) extension, storefront event data that is used by [!DNL Live Search] is no longer captured. This is because storefront event data is generated client-side. To continue capturing and sending storefront event data, re-enable event collection for [!DNL Live Search]. See [general configuration](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services) to learn more.

## Set the scope

Initially the [scope](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) of all [!DNL Live Search] settings is set to `Default Store View`. If your [!DNL Commerce] installation includes multiple store views, set **Scope** to the [store view](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) where your facet settings apply.

## Menu Options

| Option | Description |
|--- |--- |
| [Performance](performance.md) | Dashboard provides insight into product search performance. | 
| [Faceting](facets.md) | High-performance filtering that uses multiple dimensions of attribute values to refine search criteria. |
| [Synonyms](synonyms.md) | Extend the reach of search to include words shoppers might use to find products that differ from those in your catalog. |
| [Search Merchandising](rules.md) | Shape the search experience with logical rules that trigger scheduled actions. Boost, bury, pin, or hide products to calibrate search results to support your business goals. |
| [Category Merchandising](category-merch.md) | Apply rules and Intelligent Merchandising on the Category level. |
| [GraphQL](graphql.md) | Developers who are logged into the Admin of your store can compose and test queries with actual catalog data. To learn more, go to [GraphQL Overview](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) in the [!DNL Live Search] developer documentation. |
| [Settings](settings.md) | Determine how price facet values are grouped by price range in the storefront and set the indexing language. |

## Set attributes as searchable

To produce highly-targeted results, review the set of [searchable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) (`searchable=true`) product attributes. To ensure relevancy, make attributes searchable only if they contain content that has a clear and concise meaning. Avoid using attributes that contain less precise, lengthy text such as `description`, which although search-enabled by default, can reduce the precision of search results. For example, if a person searches for "shorts" and there are shirts with a description that includes the term "short sleeves", then the shirts will be included in the search results.

To allow attributes to be searchable, complete the following steps:

1. In the Admin, go to **Stores** > *Attribute* > **Product**.
1. Select the attribute you want to be searchable, such as `color`.
1. Select **Storefront Properties** and set **Use in Search** to `yes`.

[!DNL Live Search] also respects the [weight](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search) of a product attribute, as set within Adobe Commerce. Attributes with a higher weight will appear higher within the search results.

The following attributes are always searchable:

- `sku`
- `name`
- `categories`

### Layered search and expansion of search types

Layered search, or search within a search, is a powerful, attribute-based filtering system that extends the traditional search functionality to include additional search parameters. These additional search parameters allow more precise and flexible product discovery.

>[!NOTE]
>
>Layered search is available in Live Search 4.6.0.

With layered search you can:

1. Perform a search within the search results.
1. Use `startsWith` and `contains` search indexation in the second layer of the layered search to further refine the results.

The advanced search capabilities are implemented through the `filter` parameter in the [`productSearch` query](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) using specific operators:

- **Layered search** - Search within another search context - With this capability, you can undertake up to two layers of search for your search queries. For example:
  
  - **Layer 1 search** - Search for "motor" on "product_attribute_1".
  - **Layer 2 search** - Search for "part number 123" on "product_attribute_2". This example searches for "part number 123" within the results for "motor".

  Layered search is available for both `startsWith` search indexation and `contains` search indexation in the second layer of the layered search, as described below:

- **startsWith search indexation** - Search using `startsWith` indexation. This new capability allows:

  - Searching for products where the attribute value starts with a particular string.
  - Configuring an "ends with" search so shoppers can search for products where the attribute value ends with a particular string. To enable an "ends with" search, the product attribute needs to be ingested in reverse and the API call should also be a reversed string.

- **contains search indexation** -Search an attribute using contains indexation. This new capability allows:

    - Searching for a query within a larger string. For example, if a shopper searches for the product number "PE-123" in the string "HAPE-123".

        - Note: This search type is different from the existing [phrase search](#phrase), which performs an autocomplete search. For example, if your product attribute value is "outdoor pants", a phrase search returns a response for "out pan", but does not return a response for "oor ants". A contains search, however, does return a response for "oor ants".

These new conditions enhance the search query filtering mechanism to refine search results. These new conditions do not affect the main search query.

#### Implementation

1. In the Admin, [set a product attribute](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) to be searchable.

    See the list of searchable [attributes](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types).

1. Specify the search capability for that attribute, such as **Contains** (default) or **Starts with**. You can specify a maximum of six attributes to be enabled for **Contains** and six attributes to be enabled for **Starts with**. 

    ![Specify search capability](./assets/search-filters-admin.png)

1. See the [developer documentation](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) for examples of how to update your [!DNL Live Search] API calls using the new `contains` and `startsWith` search capabilities.

    You can implement these new conditions on your search results page. For example, you can add a new section on the page where the shopper can further refine their search results. You can allow shoppers to select specific product attributes, such as "Manufacturer", "Part Number", and "Description". From there, they search within those attributes using the `contains` or `startsWith` conditions. 

### When to use layered search rather than facets

Layered search and facets serve different purposes in product discovery, and choosing between them depends on your specific use case:

**Use layered search when:**

- You need to search within search results using multiple criteria.
- Working with part numbers, SKUs, or technical specifications where users know partial information.
- Users need to narrow down results step-by-step with nested criteria.
- You want to reduce the number of API calls by combining multiple search criteria in a single query.
- You need to implement business-specific search patterns that go beyond standard faceted navigation.

**Use facets when:**

- Providing typical category, price, brand, and attribute filtering
- Offering intuitive filter options that users can easily understand and select
- Showing available options based on current search results
- Displaying filter counts and ranges that help users understand available options
- Working with common product characteristics like color, size, material, and so on.

**Best Practice:** Use layered search for complex, technical searches where users have specific criteria, and use facets for standard e-commerce filtering where users want to explore and narrow down options visually.

## Facets and synonyms

Facets and synonyms are another way you can enahnce the search experience for your shoppers.

[Facets](facets.md) are product attributes that are defined in [!DNL Live Search] to be filterable. You can set any filterable attribute as a facet in [!DNL Live Search], but there are [limits](boundaries-limits.md) to how many facets you can search for at one time. 

>[!NOTE]
>
>A product attribute is filterable only if the product attribute configuration has the required properties: *Use in Search = Yes*, *Use in Search Results Layered Navigation=yes*, and *Use in Layered Navigation=Filterable (with results)*. If these properties are missing, the attribute is not visible in the Facet configuration. For configuration instructions, see [Add a Facet](facets-add.md#add-a-facet).

[Synonyms](synonyms.md) are terms that you can define to help guide users to the correct product. Users looking for pants might type in "trousers" or "slacks". You can set synonyms so that these search terms will get users to the "pants" results.

## Commerce Configuration Settings

The following section describes the supported and unsupported Commerce configuration settings for [!DNL Live Search].

### Supported configuration values

>[!IMPORTANT]
>
>It is highly recommended you use the product listing widgets, enabled by default in Live Search 4.0.0. The widgets are targeted to replace adapter implementation in future releases completely. See [enable product listing widgets](install.md#enable-product-listing-widgets) to learn more.

|Commerce Configuration Setting|Description|Supported by Popover|Supported by Adapter|
|---|---|---|---|
|Stores > Configuration > Catalog > Catalog > Catalog Search > Allow All Products per Page|If set to `Yes`, includes the `ALL` option in the "Show per Page" control.| Yes. Max 500 products|Yes. Max 500 products|
|Stores > Configuration > Catalog > Catalog > Catalog Search > Minimal Query Length|The minimum number of characters allowed in a catalog search.|Yes|Yes|
|Stores > Configuration > Catalog > Catalog > Catalog Search > Products per Page on Grid Allowed Values|Determines the number of products displayed in Grid View.|Yes|Yes|
|Stores > Configuration > Catalog > Catalog > Catalog Search > Products per Page on Grid Default Value|Determines the number of products displayed per page by default in grid view.|Yes. Max 500 products|Yes. Max 500 products|
|Stores > Configuration > Catalog > Inventory > Display Out of Stock Products|Displays products that are out of stock.|Yes|Yes|
|Stores > Configuration > Currency > Default Display Currency|The primary currency used to display prices.|Yes|Yes|
|Stores > Configuration > General > Currency Setup > Currency Options > Base Currency|The primary currency used for all online payment transactions.|Yes|Yes|

Prices in the Widget Product Listing Page and Popover are converted to the Default Display Currency using the configured Currency Rates.

### Unsupported configuration values

|Commerce Configuration Setting|Description|Notes|
|---|---|---|
|Stores > Configuration > Catalog > Storefront > List Mode|Determines the format of the search results list.|Renders correctly, but events are not sent for some page interactions|
|Stores > Configuration > Catalog > Catalog > Catalog Search > Maximum Query Length|The maximum number of characters allowed in a catalog search.|Not implemented; Search Services accepts up to 255 characters|
|Configuration > Sales > Tax > Price Display Settings > Display Product Prices In Catalog|Determines if product prices published in the catalog include or exclude tax, or show two versions of the price; one with, and the other without tax||
|Stores > Configuration > Catalog > Storefront > Product Listing Sort By|Determines the sort order of the search results list.|Does not apply to the [!DNL Live Search] [Product Listing Page Widget](plp-styling.md)|

### Search terms

[!DNL Live Search] supports [search term redirects](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html) on implementations where Adobe Commerce handles the routing, such as on Luma and other php-based themes.
