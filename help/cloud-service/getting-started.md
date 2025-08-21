---
title: 'Getting started with [!DNL Adobe Commerce as a Cloud Service]'
description: Learn how to get started with [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Getting started

[!DNL Adobe Commerce as a Cloud Service] provides most configuration out of the box. After completing a few basic setup processes, your store will be up and running in no time. This guide walks you through creating and working with an instance.

Click the tabs below to see high-level workflow overviews for the following user types:

* Administrators
* Merchants
* Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce as a Cloud Service] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/enterprise/admin-guide.html) for more information about administrator workflows.

![[!DNL Adobe Commerce as a Cloud Service] merchant flow diagram](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce as a Cloud Service] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/webapi/rest/) for more information.

![[!DNL Adobe Commerce as a Cloud Service] developer flow diagram](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## Create an instance

>[!NOTE]
>
>Before you can create an instance, your organization's product admin or system admin must add you as a user of the [!DNL Adobe Commerce as a Cloud Service] product. See [Add users and admins](./user-management.md#add-users-and-admins) for more information.

[!DNL Adobe Commerce as a Cloud Service] instances use a credit-based system. You can create multiple instances, but each instance requires a relative amount of credits. The amount of credits you have initially depends on your subscription.

1. Log in to your [Adobe Experience Cloud](https://experience.adobe.com/) account.

1. Under [!UICONTROL Quick access], click [!UICONTROL **Commerce**] to open the [!UICONTROL Commerce Cloud Manager]. 

   The [!UICONTROL Commerce Cloud Manager] displays a list of [!DNL Adobe Commerce as a Cloud Service] instances that are available in your Adobe IMS organization.

1. Click [!UICONTROL **Add Instance**] in the top-right corner of the screen.

    ![Create Instance](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Select [!UICONTROL **Commerce as a Cloud Service**].

1. Enter a **Name** and **Description** for your instance.
 
1. Choose the [!UICONTROL **Environment Type**] for your instance. You can choose between the following options:

   * [!UICONTROL **Sandbox**] - Ideal for design and testing purposes. You should begin your [!DNL Adobe Commerce as a Cloud Service] journey by using the sandbox environment.
   * [!UICONTROL **Production**] - For live stores and customer-facing sites.

   >[!NOTE]
   >
   >* Sandbox instances are limited to the North America region.
   >* The option to install sample data is currently unavailable.

1. Select the region where you want your instance hosted.

   >[!NOTE]
   >
   >Once you have created your instance, you will not be able to modify the region.

1. Click [!UICONTROL **Add Instance**].

## Access an instance

After you create an instance, you can access it from the [!UICONTROL Commerce Cloud Manager].

1. Log in to your [Adobe Experience Cloud](https://experience.adobe.com/) account.

1. Under [!UICONTROL Quick access], click [!UICONTROL **Commerce**] to open the [!UICONTROL Commerce Cloud Manager]. 

   The [!UICONTROL Commerce Cloud Manager] displays a list of instances that are available in your Adobe IMS organization.

1. To open the [!UICONTROL Commerce Admin] for an instance, click the instance name.

>[!TIP]
>
>To see information about your instance, including the REST and GraphQL endpoints and the Admin URL, click the information icon next to the instance name.

## Import your catalog

By default, [!DNL Adobe Commerce as a Cloud Service] instances do not include any product data. You have an option to include sample product data when you create an instance for testing and learning purposes before importing your own catalog.

There are two ways to import your catalog into [!DNL Adobe Commerce as a Cloud Service]:

* [**Commerce Admin**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) - A user-friendly interface that allows you to import your catalog data in a few clicks.
* [**Import JSON API**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - A REST API that allows you to import your catalog data programmatically.

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## Set up the storefront

Now that you have created an instance, you are ready to proceed [setting up](storefront.md) your Commerce Storefront powered by Edge Delivery Services.
