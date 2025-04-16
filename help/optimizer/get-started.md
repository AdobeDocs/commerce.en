---
title: 'Get Started with [!DNL Adobe Commerce Optimizer]'
description: 'Learn how to get started with [!DNL Adobe Commerce Optimizer].'
hide: yes
recommendations: noCatalog
---
# Get Started

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

[!DNL Adobe Commerce Optimizer] provides most configuration out of the box. After completing a few basic setup processes, your store will be up and running in no time. This guide walks you through creating and working with an instance.

Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/services/cloud/) for more information.

NEED DIAGRAM

>[!ENDTABS]

## Provisioning

>[!IMPORTANT]
>
>This section contains information that is only applicable for early access participants.

[!DNL Adobe Commerce Optimizer] services are a subset of the services provisioned for [!DNL Adobe Commerce Cloud Service]. When the Adobe provisioning team gives you access to an [!DNL Adobe Commerce Cloud Service] instance, you effectively gain access to [!DNL Adobe Commerce Optimizer] functionality (services, APIs, UI) without needing a dedicated [!DNL Adobe Commerce Optimizer] SKU. Access includes entitlements to EDS and App Builder.

After the [!DNL Adobe Commerce Optimizer] instances are ready, the [!DNL Adobe Commerce Optimizer] provisioning team provides you with the following endpoints:

|Item|Sample URL|Purpose|
|---|---|---|
|[!DNL Adobe Commerce Optimizer] UI|`https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant={tenantId}`|Access Commerce Optimizer UI for managing your catalog across:<br>1. Merchandising rules (Product Discovery, Product Recommendations).<br>2. Catalog Management (Channel and Policy creation).<br>3. Data Insights (View your catalog data ingestion status).|
|Storefront APIs|`/{tenantId}/graphql`|Access the APIs needed to set up your Commerce storefront powered by Edge Delivery Services.|
|Catalog data ingestion APIs|`/{tenantId}/v1/catalog`|Access the APIs needed to ingest your catalog data.|

As an early access participant, you will receive an email with a secure link that, along with your IMS token, lets you log into [!DNL Adobe Commerce Optimizer] or make API calls.

## Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.

## Set up the storefront

Now that you have created an instance, you are ready to proceed [setting up](storefront.md) your Commerce Storefront powered by Edge Delivery Services.
