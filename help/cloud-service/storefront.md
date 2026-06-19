---
title: Set up your storefront
description: Learn how to run the scaffolding tool to set up your [!DNL Adobe Commerce as a Cloud Service] storefront.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
autotag-review: '2026-06-18T16:05:19.363Z'
TQID: 'https://experienceleague.adobe.com/LoeNTJ-evBJB-TaJV0mEQpD2G2MwxHX7cYHx67kP0cA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
    internal-label: Experimentation
---
# Set up your storefront

To set up your [!DNL Adobe Commerce Storefront] powered by [!DNL Edge Delivery Services] for [!DNL Adobe Commerce as a Cloud Service] (SaaS), complete the following steps.

For a more customizable and detailed walkthrough, refer to the [storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

1. Open the [site creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Select **[!UICONTROL Create New Site (Code & Content)]**.

1. Enter the **[!UICONTROL Github Organization/Username]** where you want to create the storefront code repository.

1. Enter a **[!UICONTROL Site Name]**.

1. In the **[!UICONTROL Commerce GraphQL Endpoint (optional)]** field, enter your [!DNL Adobe Commerce as a Cloud Service] (SaaS) GraphQL endpoint, which you can access in the Commerce Cloud Manager after [creating your instance](./getting-started.md#create-an-instance).

    Alternatively, if you are using [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), enter your [!DNL API Mesh] GraphQL endpoint into the **[!UICONTROL Commerce GraphQL Endpoint (optional)]** field. See [create a mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) for more information.

1. Click **[!UICONTROL Create Site]**. Follow the on-screen instructions to authorize access to your GitHub repository.

Once the process completes, you can customize your storefront using the following methods:

* Customize your code: `https://github.com/<username or org>/<repo name>`
* Edit your content: `https://da.live/#/<username or org>/<repo name>`
* Manage your config: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Preview your storefront: `https://main--<repo name>--<username or org>.aem.page/`

## Next steps

See the following articles for more information:

* [Updating storefront content](./use-cases.md#update-storefront-content)—Manage and display content and data on the storefront.
* [Contextual experimentation](./use-cases.md#contextual-experimentation)—Create and manage experiments on your storefront.
* [Generate Variations](./use-cases.md#generate-variations)—Use Generative AI to automate high-quality content generation.
* [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/)—Get detailed information about updating site content and integrating with Commerce frontend components and backend data.
* [Configuration Service](https://www.aem.live/docs/config-service-setup)—Learn about migrating your storefront configuration from `config.json` to use the Configuration Service, which supports advanced use cases like repoless configuration and overlays. 
