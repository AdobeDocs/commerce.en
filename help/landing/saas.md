---
title: Commerce Services Connector
description: Learn how to integrate your Adobe Commerce or Magento Open Source instance to services using production and sandbox API keys.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# [!DNL Commerce Services Connector]

Some Adobe Commerce and Magento Open Source features are powered by [!DNL Commerce Services] and deployed as SaaS (software as a service). To use these services, you must connect your [!DNL Commerce] instance using production and sandbox API keys, and specify the data space in the [configuration](#saas-configuration). You only need to configure the connection one time for each instance.

Only the [!DNL Commerce] license owner can generate these API keys. If you are not the license owner, request the keys from the person or team that owns the Commerce license for your store.

## Available services {#availableservices}

The following lists the [!DNL Commerce] features you can access through the [!DNL Commerce Services Connector]:

| Service | Availability |
| --- | --- |
|[[!DNL Product Recommendations]](/help/product-recommendations/overview.md) powered by Adobe AI| Adobe Commerce|
|[[!DNL Live Search]](/help/live-search/overview.md) powered by Adobe AI | Adobe Commerce|
|[[!DNL Payment Services]](/help/payment-services/guide-overview.md) | Adobe Commerce and Magento Open Source|
|[[!DNL Catalog Service]](/help/catalog-service/overview.md)|Adobe Commerce|
|[[!DNL Data Connection]](/help/data-connection/overview.md)|Adobe Commerce|

## Architecture

At a high level, the [!DNL Commerce Services Connector] is made up of the following core elements:

![Commerce Services Connector Architecture](assets/saas-config-sync-workflow.png)

The following sections discuss each of these elements in more detail.

## Credentials {#apikey}

The production and sandbox API keys are generated from the [!DNL Commerce] account of the [license owner](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding). The Commerce account is identified by a unique [!DNL Commerce] ID (MageID). The license owner for the merchant's organization can generate API keys for services like Product Recommendations or Live Search, as long as the account is in good standing.

The keys can be shared on a "need-to-know" basis with the systems integrator or development team that manages projects and environments on behalf of the license holder. Developers who have been granted [!DNL Shared Access] by the license owner cannot generate the keys on the license owner's behalf even if the merchant's organization is present in the [!DNL Switch Accounts] dropdown on their account.

Additionally, solution integrators are entitled to use [!DNL Commerce Services]. If you are a solution integrator, the signer of the [!DNL Commerce] partner contract should generate the API keys.

The key identifiers *Production* and *Sandbox* refer to SaaS data space environments where [!DNL Commerce Services] store data (not to your Adobe Commerce environments). You can use the same set of API keys across your local, development, staging, and production Adobe Commerce environments—what matters is that you paste the correct key pair for the data space you configure.

The license owner is typically the Primary Contact on the Adobe Commerce account and is not always the same as the Project Owner of the Adobe Commerce on cloud infrastructure project.

### Generate the production and sandbox API keys {#genapikey}

1. Log in to your [!DNL Commerce] account at [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. Under the **Magento** tab, select **API Portal** on the sidebar.

1. From the _Environment_ menu, select **Production** or **Sandbox**. 

1. Enter a name in the _API Keys_ section, and click **Add New** to open the dialog to download the new key.

   ![Download private key](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > You can copy or download the private key only once. Store it securely.

1. Click **Download** to save the private key, then close the dialog.

1. Repeat the above steps for each environment (production and sandbox).

   The **API Keys** section now displays your API (Public) keys. You need all four keys (both the production and sandbox keys, Public+Private) when you [select or create a SaaS project](#createsaasenv) in any of the environments or installations associated with the license.

## SaaS configuration {#saasenv}

[!DNL Commerce] instances must be configured with a SaaS project and a SaaS data space so that [!DNL Commerce Services] can send data to the right location. A SaaS project groups all SaaS data spaces. The SaaS data spaces are used to collect and store data that enables [!DNL Commerce Services] to work. Some of this data may be exported from the [!DNL Commerce] instance and some may be collected from shopper behavior on the storefront. That data is then persisted to secure cloud storage.

For [!DNL Product Recommendations], the SaaS data space contains catalog and behavioral data. You can point a [!DNL Commerce] instance to a SaaS data space by [selecting it](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) in the [!DNL Commerce] configuration.

>[!WARNING]
>
> Use your **production SaaS data space** only with your production [!DNL Commerce] installation. Using it in non-production environments can mix testing and live data (for example, staging URLs or test catalog data). If this happens, [submit a Support request](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) to request data cleanup.

If you cannot find Live Search configuration fields in the Admin, verify that you entered the correct API key pair for the data space you selected (production data spaces use production keys; testing data spaces use sandbox keys). If you configure incorrect keys, SaaS services such as Live Search are not available in that Adobe Commerce environment.

### Delete an API key {#delapikey}

>[!WARNING]
>
>Deleting a key that is still in active use immediately disrupts connected services.

Before deleting an API key, generate and securely store a replacement key. Update all integrations to use the new key, and confirm that dependent services are working as expected.

On the API key to remove, click **[!UICONTROL Delete]**. When prompted,  confirm the operation to permanently remove the key.

### SaaS data space provisioning

All Adobe Commerce merchants can access one production data space and two testing data spaces per SaaS project.

You can use the testing data spaces in non-production environments, but avoid using the same data space in multiple environments at the same time. If you want to move a testing data space to a different environment, perform a data cleanup before selecting and configuring it in the new environment.

For Adobe Commerce Cloud Pro projects with multiple staging environments, you can request additional testing data spaces for each staging environment by [submitting a Support request](https://experienceleague.adobe.com/home?support-tab=home#support). However, if you only have one staging environment and require additional testing data spaces, you have the following options:

- Contact the Customer Success team or your appointed Customer Success Manager to request an additional staging environment.

- [Submit a Support request](https://experienceleague.adobe.com/home?support-tab=home#support) to request the additional testing data space and indicate the business justification for the extra data space. This request is subject to approval.

Magento Open Source customers using Adobe Payment Services may also request an additional data space. Contact the Payments team for prior approval of the additional data spaces before submitting a [Support request](https://experienceleague.adobe.com/home?support-tab=home#support) to request the testing data space.

Customers who own multiple Cloud projects or on-premises (live/production) installations can also request additional production and testing data spaces for each project or instance by [submitting a Support request](https://experienceleague.adobe.com/home?support-tab=home#support).

### Select or create a SaaS project {#createsaasenv}

To select or create a SaaS project, request the [!DNL Commerce] API keys from the [!DNL Commerce] license owner for your store:

1. On the _Admin_ sidebar, go to **System** > Services > **Commerce Services Connector**.

   If you do not see the **[!UICONTROL Commerce Services Connector]** section, install the [!DNL Commerce] modules for your desired [[!DNL Commerce] service](#availableservices) and make sure that the `magento/module-services-id` package is installed.

1. In the _[!UICONTROL Sandbox API Keys]_ and _[!UICONTROL Production API Keys]_ sections, paste your key values.

   - Private keys must include `-----BEGIN PRIVATE KEY-----` at the beginning of the key and `-----END PRIVATE KEY-----` at the end of the key.
   - If you do not have a copy of the actual keys, ask the license owner for them, then plug the values into the configuration.

   Do not paste key values copied from a database backup or snapshot. When the configuration is saved, an additional layer of encryption is applied and the keys will not work.

1. Click **Save**.

   Any SaaS projects that are associated with your keys appear in the **Project** field in the **SaaS Identifier** section.

1. If no SaaS projects exist, click **Create Project**. Then in the **Project** field, enter a name for your SaaS project.

   To avoid confusion, do not use a specific Commerce Service as the name for your project (for example, *Live Search*, *Product Recommendations*, or *Data Connection*). Unless your license has been provisioned for multiple SaaS projects, you can use the same SaaS project for multiple services.

1. Select the **Data Space** to use for the current configuration of your [!DNL Commerce] store.

   If you have separate instances to integrate with Commerce Services, [submit a Support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) to request a new SaaS project for each additional instance. After Support creates the SaaS project, configure the integration for the instance using the same API keys and selecting the new SaaS project for the data space.

  >[!WARNING]
  >
  > If you generate new keys in the API Portal, immediately update the API keys in the Admin configuration. If the Admin is still using old keys, your SaaS extensions stop working and data collection is interrupted.

To change the names of your SaaS project or data space, click **Rename** next to either one. Changing the name does not affect your service because the name is only a label to help you identify and differentiate between projects and data spaces.

## IMS Organization (optional) {#organizationid}

To connect your Adobe Commerce instance to the Adobe Experience Platform, sign in to your Adobe account using your Adobe ID. After you sign in, the IMS organization associated with your Adobe account is displayed in this section.

## SaaS data export

When your [!DNL Commerce] instance successfully connects to [!DNL Commerce Services], the SaaS data export process exports Commerce data from your [!DNL Commerce] server to [!DNL Commerce SaaS Services] so it can be synchronized to connected Commerce Services. In the Admin, you can check synchronization status using the [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). For details, see the [SaaS Data Export Guide](../data-export/overview.md).
