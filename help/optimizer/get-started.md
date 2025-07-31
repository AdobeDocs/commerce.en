---
title: Get started
description: Learn how to get started with [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
---
# Get Started

This guide walks you through setting up [!DNL Adobe Commerce Optimizer] from start to finish. While this guide covers all roles, see the [developer documentation](https://developer.adobe.com/commerce/services/optimizer/) for detailed developer-specific content.

## Prerequisites

Before you begin, ensure you have:

- **Adobe Experience Cloud account** with [!DNL Adobe Commerce Optimizer] entitlements
- **Organization admin access** to create instances and manage users
- **GitHub account** (for loading sample data and storefront development)
- **Basic understanding** of e-commerce concepts

## Quick Start guide

Follow these essential steps to get your [!DNL Adobe Commerce Optimizer] environment running:

### Step 1. Create an instance

1. Log in to [Adobe Experience Cloud](https://experience.adobe.com/).
1. Navigate to **Commerce** > **Commerce Cloud Manager**.
1. Click **Add Instance** > **Commerce Optimizer**.

   ![Create Instance](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Configure instance settings:
   - **Name**: Descriptive name (for example, "My Company Sandbox")
   - **Description**: Brief description of purpose
   - **Region**: Select your preferred region
   - **Environment Type**: Start with a **Sandbox** environment for testing

1. Click **Add Instance**.

   The Cloud Manager updates to include your new instance. For details on accessing and managing it, see [Manage an instance](#manage-an-instance).

>[!NOTE]
>
>Sandbox instances are limited to the North America region. You cannot change the region after creation.

### Step 2. Set up your environment

After creating your instance:

1. [Manage your instance](#manage-an-instance) from Commerce Cloud Manager.
1. Configure user access using the [User Management guide](./user-management.md).

### Step 3. Add sample data (Optional)

For testing and learning, follow the [Load Sample Data](#add-sample-data) instructions.

## Role-Based workflows

[!DNL Adobe Commerce Optimizer] setup and management rely on three key roles. Each role has specific tasks and responsibilities:

![High-Level Workflow](./assets/high-level-workflow.png){zoomable="yes"}

### Administrator tasks

Administrators manage instances, users, and organizational settings.

|Task|Description|Link|
|---|---|---|
|**Manage Users**|Add users, developers, and admins|[User Management](./user-management.md)|
|**Create Instances**|Set up sandbox and production environments|[Create Instance](#create-an-instance)|
|**Configure Access**|Set up catalog views and policies|[Catalog Views](./setup/catalog-view.md)|

### Developer tasks

Developers handle technical implementation and data integration, including platform architecture tasks.

|Task|Description|Link|
|---|---|---|
|**Access Developer Console**|Create projects and generate credentials|[Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started)|
|**Ingest Catalog Data**|Import product data from existing systems|[Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)|
|**Set Up Storefront**|Configure Edge Delivery Services storefront|[Storefront Setup](./storefront.md)|

### Merchandiser tasks

Merchandisers optimize and personalize the shopping experience through product discovery and recommendations. They also use shopper data and analytics to make strategic decisions about product placement, pricing, and promotions on the storefront.

|Task|Description|Link|
|---|---|---|
|**Product Discovery**|Configure search and filtering|[Merchandising Overview](./merchandising/overview.md)|
|**Recommendations**|Set up AI-powered product recommendations|[Product Recommendations](./merchandising/recommendations/overview.md)|
|**Performance Tracking**|Monitor success metrics|[Success Metrics](./manage-results/success-metrics.md)|

## Manage an instance

1. Log in to [Adobe Experience Cloud](https://experience.adobe.com/).

1. Open Commerce Cloud Manager:
   - Under **Quick access**, click **Commerce**.
   - View your available instances.

1. Access your instance:

   Click the instance name to open the [!DNL Adobe Commerce Optimizer] application. Within the application, you can switch between different [!DNL Adobe Commerce Optimizer] instances using the drop-down at the top of the page:

   ![Instance Switcher](./assets/context-switcher.png){zoomable="yes"}

   All instances displayed belong to the same organization. You can switch between instances to view data and settings for each one, such as between sandbox and production environments.

1. Get instance details:
   - Click the information icon next to your instance name.
   - Note the GraphQL endpoint, the Catalog Service endpoint for data ingestion, and the Instance ID (also known as the `tenant ID`).

   ![Instance Details](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

   The endpoint and instance ID (tenant ID) details are required to integrate with frontend applications and backend systems. The URL to access the [!DNL Adobe Commerce Optimizer] application is also provided here.

   Not all Adobe Commerce Optimizer users have access to Cloud Manager and the instance details. Access depends on the role and permissions assigned to the user account. If you do not have access, contact your organization administrator to get the instance details.

1. Edit instance name and description:
   - Click the **Edit** icon next to an instance name.
   - Update the name and description as needed.
   - Click **Save**.

   You can also use the search and filter options to find specific instances quickly.

## Add sample data

Adobe provides a GitHub repository with sample data and tools to help you learn and test [!DNL Adobe Commerce Optimizer] features.
The sample data is based on the [Carvelo business scenario](./use-case/admin-use-case.md) and includes:

- Product catalog with automotive parts
- Multiple price books and pricing scenarios
- Catalog views and policies for different dealers
- Complete end-to-end workflow examples

**Load the sample data:**

1. Access the [Sample Catalog Data Ingestion](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion) GitHub repository.

1. Follow the setup instructions in the repository's README file to complete the following tasks:

   - Set up your environment
   - Complete the data ingestion process
   - Create catalog views and policies using the sample data 
   - Verify the data ingestion by checking the Catalog Service data on the [Data Sync](./setup/data-sync.md) page

## Next Steps

After completing the setup:

1. Set up your storefront:
   - Configure [Edge Delivery Services storefront](./storefront.md)
   - Connect to your catalog data

1. Explore the Carvelo use case:
   - Follow the [end-to-end workflow](./use-case/admin-use-case.md)
   - Practice with real scenarios

1. Configure merchandising:
   - Set up [product discovery](./merchandising/overview.md)
   - Create [recommendations](./merchandising/recommendations/overview.md)

1. Monitor performance:
   - Track [success metrics](./manage-results/success-metrics.md)
   - Analyze [search performance](./manage-results/search-performance.md)

## Troubleshooting

### Common issues

|Issue|Solution|
|---|---|
|**Cannot create an instance**|Verify that you have [!DNL Adobe Commerce Optimizer] entitlements and admin permissions.|
|**Instance not appearing**|Check your Adobe IMS organization and refresh the page.|
|**Cannot access instance**|Ensure that you're added as a user in the Admin Console.|
|**Sample data not loading**|Verify your instance credentials and API endpoints.|

### Get help

- **Developer Resources**: [Developer Documentation](https://developer.adobe.com/commerce/services/optimizer/)
- **Storefront Resources**: [Commerce Storefront Documentation](https://experienceleague.adobe.com/developer/commerce/storefront/)
- **Support**: [Adobe Commerce Support resources](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)
