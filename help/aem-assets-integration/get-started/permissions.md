---
title: Configure IMS user permissions for the AEM Assets Integration
description: Learn how IMS identity and Admin Console profiles enable AEM Assets delivery access, the Asset Selector, and auto-populated Commerce config fields.
feature: CMS, Media, Configuration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
---
# User permissions and IMS

**IMS** (Adobe Identity Management System) is the authentication layer.

* For Adobe Commerce as a Cloud Service, the Admin enables IMS authentication by default.
* For Adobe Commerce on cloud or on-premises, IMS is optional.

  [Enabling IMS for Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-config){target=_blank} provides an enhanced configuration UI with the Asset Selector and environment and domain dropdowns. If your configuration displays separate **Program ID** and **Environment ID** fields, you can enter those identifiers manually without IMS.

When using IMS, the AEM Assets Integration also requires specific **Adobe Admin Console product profiles**. Users who configure the integration in Commerce Admin need the **AEM Assets DM OpenAPI Users - delivery** product profile, or the **author** product profile as a fallback. This access is controlled through Admin Console product profiles in the user's IMS organization, and enables:

* **Asset Selector** allows you to select images from AEM Assets when managing category images or Page Builder content.
* **Auto-populated configuration fields**, including the **AEM Environment** and **AEM Domain Mapping** dropdowns, that pull values from the user's IMS session. See [Configure the integration](setup-synchronization.md) for environment selection and manual ID entry.

Without the correct permissions, the Asset Selector is unavailable, and these fields appear empty or require manual entry.

>[!IMPORTANT]
>
> Adobe Admin Console product profiles control user access to integration features; they do not change licensing entitlements. Assigning an author product profile does not grant AEM Assets Author API access to Product Visuals customers. See [Product Visuals limits](../../optimizer/boundaries-limits.md#product-visuals-limits) for entitlement requirements.

>[!BEGINSHADEBOX]

**How IMS and permissions interact**

Adobe IMS provides the user identity and organization context, while the Adobe Admin Console defines which **product profiles** (permissions) they have. The AEM Assets Integration uses the IMS details plus the assigned profile to determine whether it can auto-populate configuration fields and enable the Asset Selector.

>[!ENDSHADEBOX]

## Why product profiles are required

The integration can only load domains that are mapped to a profile. Therefore, users can have the following product profiles:

* **AEM delivery product profile**. Required for the Asset Selector and Configuration UI when the user has both author and delivery profiles. The integration uses the AEM delivery product profile when available.

* **Author product profile**. Required to access the AEM Assets UI. Also serves as the fallback for the Asset Selector and Configuration UI when the user does not have the AEM delivery product profile in their Admin Console.

The integration loads environments and domain mappings from the **AEM delivery product profile** when available, or falls back to the **author product profile** when the AEM delivery product profile is not in the user's Admin Console. Users need one of these profiles to:

* Populate the **AEM Environment** and **AEM Domain Mapping** dropdowns in the Commerce Admin configuration.
* Use the Asset Selector to browse and select assets from AEM Assets.

If neither profile is configured, the Asset Selector is unavailable. If your configuration displays separate **Program ID** and **Environment ID** fields, you can enter the identifiers manually.

## Grant permissions by deployment type

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE SaaS only]{type=Positive tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."}

The system enables IMS authentication by default.

Add the user to the **AEM Assets DM OpenAPI Users - delivery** product profile in the [Adobe Admin Console](https://adminconsole.adobe.com/), or to the **author** product profile as a fallback.

>[!NOTE]
>
> Users must also be added to Commerce and AEM Assets. See [Add a user to AEM Assets or Product Visuals](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} in the _User and Identity Management_ guide for the full setup.

![Admin Console product profile for AEM Assets delivery](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB Adobe Commerce on cloud or on-premises]

[!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."}

The **IMS Client ID** is required for PaaS to enable the Asset Selector. See [Configure the AEM Assets project](configure-aem.md#prerequisites) for prerequisites, including how to obtain the IMS Client ID when enabling Dynamic Media with OpenAPI.

To use the Asset Selector and the **AEM Environment** and **AEM Domain Mapping** dropdowns:

1. [Enable Adobe IMS for Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-config){target=_blank} so that Commerce Admin uses IMS authentication and can read the user's Admin Console product profiles.

1. To request a custom IMS Client ID for the Asset Selector, [Open a Support ticket](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case).

1. From the [Adobe Admin Console](https://adminconsole.adobe.com/), add the user to the **AEM Assets DM OpenAPI Users - delivery** product profile, or to the **author** product profile as a fallback.

For configurations that display separate Program ID and Environment ID fields, manual entry is available without IMS. See [Configure the integration](setup-synchronization.md).

>[!ENDTABS]

## Related documentation

* [Configure IMS user permissions for the AEM Assets Integration](setup-synchronization.md)—Connect Commerce to AEM Assets and configure matching rules.
* [Manual asset selection](../synchronize/asset-selector-integration.md)—Use the Asset Selector for category images and Page Builder.
* [Add a user to AEM Assets or Product Visuals](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank}—For [!DNL Adobe Commerce as a Cloud Service], add users to Commerce and AEM Cloud Manager (Business Owner, Deployment Manager) first. The **AEM Assets DM OpenAPI Users - delivery** profile (or **author** profile as fallback) is an additional requirement for the Asset Selector and auto-populate features.
* [Assign team members to AEM delivery layer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}. AEM documentation for delivery access.

