---
title: Get started
description: Learn how to get started with [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
hide: yes
recommendations: noCatalog
---
# Get Started

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

This guide walks you through creating and working with an [!DNL Adobe Commerce Optimizer] instance.

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/enterprise/admin-guide.html) for more information about administrator workflows.

START WITH SOURCE SVG HERE:
https://github.com/AdobeDocs/commerce.en/blob/main/help/cloud-service/assets/architecture-and-workflow-diagrams.svg

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/services/cloud/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## Provisioning

After the [!DNL Adobe Commerce Optimizer] instances are ready, the [!DNL Adobe Commerce Optimizer] provisioning team provides you with the following endpoints:

|Item|Sample URL|Purpose|
|---|---|---|
|[!DNL Adobe Commerce Optimizer] UI|`https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>`|Access Commerce Optimizer UI for managing your catalog across:<br>1. Merchandising rules (Search, Recommendations).<br>2. Catalog Management (catalog view and Policy creation).<br>3. Data Insights (View your catalog data ingestion status).|
|Storefront APIs|`https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql`|Access the APIs needed to set up your Commerce storefront powered by Edge Delivery Services.|
|Catalog data ingestion APIs|`https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>`|Access the APIs needed to ingest your catalog data.|

>[!NOTE]
>
>See the [developer documentation](https://developer-stage.adobe.com/commerce/services/composable-catalog/) to learn more about the APIs needed for storefront setup and catalog ingestion.

As an early access participant, you will receive an email with a secure link that, along with your IMS token, lets you log into [!DNL Adobe Commerce Optimizer] or make API calls.

## Set up the storefront

Now that you have an [!DNL Adobe Commerce Optimizer] instance, you are ready to proceed [setting up](./storefront.md) your Commerce Storefront powered by Edge Delivery Services.

## Available catalog data for early access participants

As an early access participant, the [!DNL Adobe Commerce Optimizer] instance contains mock catalog data based on the [Carvelo use case](./use-case/admin-use-case.md). The mock data, along with some pre-configured catalog views and policies, help you get familiar with the [!DNL Adobe Commerce Optimizer] UI.

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the catalog views and policies.-->
