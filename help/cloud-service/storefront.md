---
title: Set up your storefront
description: Learn how to run the scaffolding tool to setup your [!DNL Adobe Commerce as a Cloud Service] storefront.
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Set up your storefront

Set up your Adobe Commerce Storefront powered by Edge Delivery Services using the instructions in [set up your storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started).

When you get to the [adding content](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-content) step and access the [site creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator), enter your Adobe Commerce as a Cloud Service (SaaS) GraphQL endpoint into the **Commerce GraphQL Endpoint (Optional)** field, which you can access in the Commerce Cloud Manager after [creating your instance](./getting-started.md#create-an-instance).

Alternatively, if you are using [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), as an orchestration layer to combine multiple data sources into a single GraphQL endpoint, enter your API Mesh GraphQL endpoint into the **Commerce GraphQL Endpoint (Optional)** field. See [create a mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) for more information.

Once the process completes, you can customize your storefront using the following methods:

* Customize your code: `https://github.com/<username or org>/<repo name>`
* Edit your content: `https://da.live/#/<username or org>/<repo name>`
* Manage your config: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Preview your storefront: `https://main--<repo name>--<username or org>.aem.page/`

To customize your storefront, refer to the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/).

For additional information, refer to the following:

* [Commerce Storefront powered by Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) - A performant, scalable, and secure storefront that is powered by Adobe's Edge Delivery Services.
* [Use cases](./use-cases.md) - Learn how to use the manage data, set up contextual experimentation, and use generative AI in your storefront.
* [API Mesh for Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/mesh/) - an API platform that allows developers to combine multiple data sources into a single GraphQL endpoint. API Mesh orchestrates third-party API with Adobe API through a single gateway. One query to the single GraphQL endpoint can return results from multiple sources.
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) - A collection of developer tools with access to APIs, events, runtime functions, and plugins, whic you can use to build projects for Adobe applications.
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) - A serverless engine for deploying custom code that responds to events and executes functions in the cloud.