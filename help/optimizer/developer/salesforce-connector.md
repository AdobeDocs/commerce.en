---
title: Salesforce Commerce Connector for Adobe Commerce Optimizer
description: Learn about the [!DNL Salesforce Commerce Connector] for [!DNL Adobe Commerce Optimizer] and how to integrate your Salesforce Commerce Cloud catalog data.
role: Admin, Developer
recommendations: noCatalog
---
# Salesforce Commerce Connector for [!DNL Adobe Commerce Optimizer]

The [!DNL Salesforce Commerce Connector] integrates your Salesforce Commerce Cloud B2C catalog with [!DNL Adobe Commerce Optimizer], enabling enhanced e-commerce experiences without re-platforming.

With the [!DNL Salesforce Commerce Connector], you can:

- **Synchronize catalog data** from Salesforce Commerce Cloud B2C to Adobe Commerce Optimizer without re-platforming your existing commerce infrastructure.
- **Maintain data consistency** through automated full and delta synchronization processes that keep your product information up to date.
- **Leverage existing investments** in Salesforce Commerce Cloud while gaining access to Adobe's advanced merchandising and personalization capabilities.
- **Scale your catalog** using Adobe Commerce Optimizer's high-performance storefront without migrating away from your Salesforce backend.
- **Support complex pricing structures** by synchronizing price books and locale-specific pricing from Salesforce.
- **Enable multi-locale experiences** by ingesting localized product data for different markets and languages.

## How the Salesforce Connector Works

The Salesforce Commerce Connector is built on [Adobe App Builder](https://developer.adobe.com/app-builder/) and provides a robust integration layer between your SFCC instance and Adobe Commerce Optimizer. The connector operates through a series of synchronization actions that transfer your catalog data, price books, and product information.

### Key Components

The connector consists of several key components:

<!-- To do: Add correct architecture diagram here -->

- **App Builder Runtime Actions** - Serverless functions that handle data synchronization between SFCC and Adobe Commerce Optimizer.
- **Custom SFCC Cartridge** - Required cartridge that extends your SFCC instance with APIs needed for data extraction.
- **Synchronization Engine** - Automated processes for full and delta data synchronization.
- **Management UI** - Web interface for monitoring sync status and managing connector operations.

### Synchronization Process

The connector supports multiple synchronization modes:

#### Full Site Sync

Performs a comprehensive synchronization of all products, price books, and prices for your configured Salesforce Commerce Cloud site and locales. This data includes:

- Product metadata and attributes
- Catalog structure and categories
- Price books and pricing information
- Multi-locale product data

#### Delta Sync

Retrieves and synchronizes only the changes made in Salesforce product and price data since the last synchronization, ensuring efficient and timely updates. Delta sync runs automatically on a scheduled basis (default: hourly) to maintain data freshness.

#### Targeted Sync Options

- **Price Book Sync** - Synchronizes price book information only.
- **Metadata Sync** - Updates product metadata and attribute definitions.
- **Specific Product Sync** - Synchronizes individual products by SKU.

## Who Benefits from the Salesforce Connector?

The [!DNL Salesforce Commerce Connector] is ideal for:

- **Existing Salesforce Commerce Cloud B2C customers** who want to enhance their storefront capabilities without migrating their entire commerce platform.
- **Multi-brand organizations** using Salesforce that require advanced merchandising and personalization features across multiple storefronts.
- **Businesses seeking performance improvements** who want to leverage Adobe's Edge Delivery Services for faster storefront experiences while maintaining their Salesforce commerce catalog management.
- **Companies with complex pricing structures** that need to synchronize sophisticated price books and locale-specific pricing from Salesforce Commerce.
- **AEM customers** seeking a simple way to manage their product catalog from Salesforce Commerce while using AEM for content management and storefront delivery.
- **Retailers with multi-locale requirements** who need to synchronize localized product information across different markets and languages.

## Use Cases

The connector supports several key use cases:

### Catalog Data Ingestion and Storefront Display

This primary use case demonstrates the complete data flow from Salesforce Commerce Cloud to the Adobe Commerce storefront:

1. **Initial catalog ingestion**—Perform a bulk load of your entire Salesforce commerce catalog, including simple products with variants, price books, and pricing information.
1. **Automated delta updates**—Automatically synchronize product changes made in the Salesforce Commerce catalog management UI to Adobe Commerce Optimizer.
1. **Storefront integration**—Display synchronized catalog data on your AEM storefront using Adobe Commerce Optimizer's storefront APIs.
1. **Real-time updates**—View updated product information (names, prices, descriptions) immediately on your storefront after making changes in Salesforce.

### Multi-Locale Product Management

Leverage the Salesforce Commerce Cloud localization capabilities:

- Synchronize localized versions of product text fields (names, descriptions) from Salesforce Commerce Cloud for different locales.
- Map Salesforce locale concepts 1:1 with Adobe Commerce Optimizer locales.
- Support multiple product ingestion cycles for different localizations.
- Maintain consistency across global product catalogs.

## Getting Started

To begin using the Salesforce Commerce Connector:

### Prerequisites

Before implementing the connector, ensure you have:

1. **Active Adobe Commerce Optimizer instance** with appropriate permissions and SaaS Catalog Services enabled.
2. **Salesforce Commerce Cloud B2C instance** with administrative access and API client credentials.
3. **Adobe Developer Console project** with the following API services enabled:
   - Adobe Commerce Optimizer Ingestion API
   - I/O Events
   - I/O Management API
4. **Node.js and npm** installed for local development.
5. **Adobe I/O CLI** installed globally for App Builder deployment.

>[!NOTE]
>
>The connector is specifically designed for Salesforce Commerce Cloud B2C. It does not support Salesforce B2B or D2C products, which are built on different technology stacks.

### Installation Overview

The implementation process involves:

1. **Installing the required SFCC cartridge** in your Salesforce Commerce Cloud instance.
2. **Configuring the Adobe App Builder project** with necessary API services and credentials.
3. **Deploying the connector application** to your App Builder runtime environment.
4. **Configuring synchronization settings** for your specific Salesforce Commerce Cloud site and locales.

For detailed installation instructions, see the [ACO SFCC Starter Kit repository](https://github.com/adobe-commerce/aco-sfcc-starter-kit).

### Required SFCC Cartridge

>[!IMPORTANT]
>
>Installation of the custom ACO SFCC Cartridge is required for the connector to function properly. The cartridge provides the necessary API endpoints for data extraction from your SFCC instance.

Download and install the required cartridge from the [ACO SFCC Cartridges repository](https://github.com/adobe-commerce/aco-sfcc-cartridges).

## Important Considerations

When planning your implementation, consider these key factors:

### Data Mapping and Attributes

- **Searchable attributes** - Salesforce Commerce Cloud sets searchable attributes through the UI, which are not exposed via API. You need to manually configure these searchable attributes in Adobe Commerce Optimizer using the metadata APIs.
- **Attribute mapping** - Plan the mapping of Salesforce Commerce product attributes to Adobe Commerce Optimizer metadata based on your specific business requirements.
- **Default searchable fields** - The connector automatically makes core attributes (name, description, ID) searchable by default.

### Synchronization Scope

- **Site selection**—Salesforce Commerce Cloud has a concept of sites that catalogs attach to. During full sync, you select which Salesforce site to synchronize.
- **Locale management**—Each Salesforce Commerce locale results in a separate product ingestion cycle in Adobe Commerce Optimizer.
- **Data volume**—Consider your catalog size and sync frequency when planning implementation.

## Monitoring and Management

The connector provides comprehensive monitoring and management capabilities:

<!-- To do: Add correct management UI screenshot here -->

- **Sync Status Tracking** - Monitor the status and timestamps of all synchronization operations.
- **Connectivity Validation** - Test connections to both Salesforce Commerce Cloud and Adobe Commerce Optimizer.
- **Product Data Validation** - Verify that synchronized product data appears correctly in your storefront.
- **Error Logging and Troubleshooting** - Access detailed logs for diagnosing and resolving sync issues.
- **State Management** - Track sync progress and prevent conflicts with built-in state management.

## Architecture and Data Flow

The Salesforce Commerce Connector follows a secure, scalable architecture that ensures reliable data synchronization:

![Adobe Commerce Optimizer Architecture](../assets/architecture.png){zoomable="yes"}

1. **Data Extraction**—The connector authenticates with your Salesforce Commerce instance and extracts catalog data using the custom cartridge APIs.
1. **Data Transformation**—Product data is transformed to match Adobe Commerce Optimizer's data model and schema requirements.
1. **Data Ingestion**—Transformed data is securely transmitted to Adobe Commerce Optimizer using the ACO TypeScript SDK.
1. **Storefront Integration**—Synchronized data becomes available through Adobe Commerce Optimizer's APIs for use in your storefront experiences.

The following diagram illustrates the high-level workflow for the integration:

<!-- To do: Add the correct data flow diagram here -->

## Source Code and Development Resources

The Salesforce Commerce Connector is open source and available for customization:

- **[ACO SFCC Starter Kit](https://github.com/adobe-commerce/aco-sfcc-starter-kit)** - Main connector application and documentation.
- **[ACO SFCC Cartridges](https://github.com/adobe-commerce/aco-sfcc-cartridges)** - Required SFCC cartridge for API integration.
- **[ACO TypeScript SDK](https://github.com/adobe-commerce/aco-ts-sdk)** - SDK for Adobe Commerce Optimizer integration.

These repositories provide complete source code, detailed documentation, and examples for implementing and customizing the connector to meet your specific business requirements.

## Next Steps

Ready to integrate your Salesforce Commerce Cloud data with Adobe Commerce Optimizer? Start by reviewing the detailed implementation guide in the [ACO SFCC Starter Kit repository](https://github.com/adobe-commerce/aco-sfcc-starter-kit) and ensure you have the necessary prerequisites in place.
