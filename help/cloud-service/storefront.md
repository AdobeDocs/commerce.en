---
title: Set up your storefront
description: Learn how to run the scaffolding tool to set up your [!DNL Adobe Commerce as a Cloud Service] storefront.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Set up your storefront

To set up your [!DNL Adobe Commerce Storefront] powered by [!DNL Edge Delivery Services] for [!DNL Adobe Commerce as a Cloud Service] (SaaS), complete the following steps.

For a more customizable and detailed walkthrough, refer to the [storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

1. Open the [site creator tool](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Select **[!UICONTROL Create New Site (Code & Content)]**.

1. Enter the **[!UICONTROL Github Organization/Username]** where you want to create the storefront code repository.

1. Enter a **[!UICONTROL Site Name]**.

1. In the **[!UICONTROL Commerce GraphQL Endpoint (optional)]** field, enter your [!DNL Adobe Commerce as a Cloud Service] (SaaS) GraphQL endpoint, which you can access in the Commerce Cloud Manager after [creating your instance](./getting-started.md#create-an-instance).

    Alternatively, if you are using [!DNL API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), enter your [!DNL API Mesh] GraphQL endpoint into the **[!UICONTROL Commerce GraphQL Endpoint (optional)]** field. See [create a mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) for more information.

1. Click **[!UICONTROL Create Site]**. Follow the on-screen instructions to authorize access to your GitHub repository.

Once the process completes, you can customize your storefront using the following methods:

* Customize your code: `https://github.com/<username or org>/<repo name>`
* Edit your content: `https://da.live/#/<username or org>/<repo name>`
* Manage your config: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Preview your storefront: `https://main--<repo name>--<username or org>.aem.page/`

## Next steps

Refer to the following articles for more information:

* To learn more about managing and displaying content and data in the storefront, see [updating storefront content](./use-cases.md#update-storefront-content).
* For more information on contextual experimentation features, see [contextual experimentation](./use-cases.md#contextual-experimentation).
* For more information on using Generative AI to automate high-quality content generation, see [Generate Variations](./use-cases.md#generate-variations).
* To learn more about updating site content and integrating with Commerce frontend components and backend data, see the [!DNL Adobe Commerce Storefront] [documentation](https://experienceleague.adobe.com/developer/commerce/storefront/).
