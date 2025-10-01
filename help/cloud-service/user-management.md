---
title: User management
description: Learn how to manage users in [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Admin
---
# User management

If you want users to access the Admin in [!DNL Adobe Commerce as a Cloud Service], you need to add them as users in your organization and ensure they have access to the Cloud Service product in the [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

This process requires an IMS organization with access to [!DNL Adobe Commerce as a Cloud Service]. Only a System Admin or Product Admin for the organization can perform these processes.

>[!TIP]
>
>To add multiple users simultaneously, you can perform a [bulk CSV upload](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> You can also add multiple users to a role by creating a [user group](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Then you can add the [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] product to the user group.

## Understanding roles

The following roles are available for [!DNL Adobe Commerce as a Cloud Service]. To view or edit these roles, in the Commerce Admin navigate to **System** > **Permissions** > **User Roles**.

* **Users** - Users have Admin access to the Commerce Admin, but cannot manage product-level access in the Admin Console. Users can also use credits to [create instances](./getting-started.md#create-an-instance) in the [!DNL Commerce Cloud Manager].

  >[!NOTE]
  >
  >All Commerce users, including developers and admins, must also have the User role assigned to them. It is required for basic Commerce permissions.

* [**Developers**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Developers have user permissions and are added to the Commerce instance as a developer user. This means they can use the [Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [configure events](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"}, and [create webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Admins - There are three different types of admins:
    * [System admins](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - The system admin has access to all products and product profiles in the organization through the Admin Console.
    * [Product admins](#add-a-product-admin) - Product admins can [manage users, roles, and permissions for the product](#add-users) in the [!DNL Adobe Admin Console] and [manage users in the Commerce Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
    * [Product profile admins](#add-developers-and-product-profile-admins) - Product profile admins do not have access to the Adobe Commerce Admin, but can manage users for the product in the [!DNL Adobe Admin Console].

For detailed information on the permissions granted to each role inside Adobe Commerce, refer to [user permissions](#user-permissions).

## Add a product admin

>[!NOTE]
>
>Assign product admins the [User role](#add-users) before adding them as product admins. The User role is required for basic Commerce permissions.

1. Navigate to https://adminconsole.adobe.com and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] product.

    ![select product](./assets/backend.png){width="600" zoomable="yes"}

1. Select the [!UICONTROL **Admins**] tab.

1. Click [!UICONTROL **Add Admin**].

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

## Add users

The following instructions provide information on how to add users to the [!DNL Commerce Cloud Manager] and the Commerce Admin. The [!DNL Commerce Cloud Manager] interface allows you to create and manage your Commerce Instances. This process is required for all users, including developers and admins.

>[!NOTE]
>
>Only product admins and system admins can add users and developers to the Adobe Commerce as a Cloud Service product.

1. Navigate to https://adminconsole.adobe.com and sign in with your Adobe ID.

2. Select your organization.

3. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] product.

    ![select product](./assets/backend.png){width="600" zoomable="yes"}

4. Click the [!UICONTROL **Default - Cloud Manager**] product profile.

5. Select the [!UICONTROL **Users**] tab and click [!UICONTROL **Add Users**].

    ![tab select](./assets/tab-select.png){width=600 zoomable="yes"}

6. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

### Add developers and product profile admins

To add developers and product profile admins, repeat the [add users](#add-users) process, but select the [!UICONTROL **Developers**] or [!UICONTROL **Admins**] tab instead of the [!UICONTROL **Users**] tab.

>[!NOTE]
>
>Product profile admins do not have access to the Commerce Admin. Refer to [Understanding roles](#understanding-roles) for more information.
>
>Assign developers the User role before adding them as developers. The User role is required for basic Commerce permissions.

![tab select](./assets/tab-select.png){width=600 zoomable="yes"}

## Role resources

The following list describes the resources that default roles have permission to access inside of the Adobe Commerce Admin. To edit the default permissions  for each role, navigate to **System** > **Permissions** > **User Roles** in the Commerce Admin.

**Users**

* Catalog
  * Inventory
    * Products
      * Read Product Price

**Developers**

* Catalog
  * Inventory
    * Products
      * Read Product Price
* System
  * Data Transfer
    * Import History
* Adobe IO Events Configuration
  * Configuration Check
  * Create Event Provider
  * Configuration Update
  * Synchronize Events
  * Get Event Provider List
* Eventing Framework
  * Event List
  * Test Eventing Connection
  * Subscribe to an event
  * Unsubscribe from an event
  * Event Status
  * API to get event subscriptions
  * View Event Subscriptions admin UI
  * Create Event Subscriptions admin UI
  * Request New Event admin UI
* Webhooks
  * Webhooks Digital Signature
    * Webhooks Digital Signature Settings
    * Webhooks Digital Signature Generate Keys
  * Webhooks Management
    * Webhooks Grid
    * Webhooks Edit
    * Test Webhooks
    * API subscribe to webhook
    * API unsubscribe from webhook
    * Webhooks List
    * Request New Webhook
    * Webhooks Logs
    * Get list of Webhooks

**Admins**

Admins have access to all permissions.

## Add a user to AEM Assets or Product Visuals

The following setup is required for [!DNL Adobe Experience Manager Assets] and [!DNL Product Visuals powered by AEM Assets] users.

If your account has access to [Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service) and you want to allow a user to access the advanced features of [AEM Assets](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/overview){target="_blank"} along with [!DNL Adobe Commerce as a Cloud Service], use the following process:

>[!NOTE]
>
>Users without appropriate assets permissions will be unable to access advanced features of [!DNL AEM Assets], such as [AI image generation](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generative-ai-in-aem){target="_blank"}, [generated variations](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations-integrated-editor){target="_blank"} and more.

>[!TIP]
>
>To add multiple users simultaneously, you can perform a [bulk CSV upload](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
>
>You can also add multiple users to a role by creating a [user group](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Then you can add the [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] product to the user group.

1. Navigate to https://adminconsole.adobe.com and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] product.

    ![select product](./assets/backend-aem.png){width="600" zoomable="yes"}

1. Select the [!UICONTROL **Users**] tab.

1. Click [!UICONTROL **Add User**].

1. Enter the username or email address of the users you want to add.

1. Click [!UICONTROL **Add Product**].

1. Select the following product profiles, which are necessary to integrate AEM Assets with Commerce:

    * Business Owner - Required to create and manage programs.
    * Deployment Manager - Required to deploy code from your repositories to AEM.

    If you are adding a developer who does not need access to the Cloud Manager or Experience Manager interfaces, you can instead assign them the developer role.

    >[!NOTE]
    >
    >For more information on how these permissions effect your access to AEM Assets, refer to [Cloud Manager Product Profiles](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles#cloud-manager-product-profiles){target="_blank"}.

1. Click [!UICONTROL **Apply**].

1. Click [!UICONTROL **Save**].

To confirm the user has access, click on the user's name to open their profile page. In the [!UICONTROL **Products**] section, it should say [!UICONTROL **Completed**] under the [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] product. It may take a few seconds after adding the user to see the status updated on their profile. Refresh the page to see the updated status.

![product access](./assets/product-access.png){width="600" zoomable="yes"}

## Access the Experience Manager interface

After adding a user to AEM Assets, they can access the [!DNL Experience Manager] interface by navigating to [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}.

1. In the [!UICONTROL **Quick Access**] section, click [!UICONTROL **Experience Manager**] or click [!UICONTROL **View All**] if you do not see [!UICONTROL **Experience Manager**]. Then click [!UICONTROL **Cloud Manager**] or navigate directly to [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}.

1. From the [!UICONTROL **Cloud Manager**] page, click [!UICONTROL **Add Program**] to get started.

1. [Create a new program](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program){target="_blank"}.

1. [Create a new environment](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/creating-an-environment){target="_blank"}.

1. After creating the environment, return to the [Admin Console](https://adminconsole.adobe.com){target="_blank"} and select [!UICONTROL **Adobe Experience Manager as a Cloud Service**].

1. You should now see new product profiles. Select that contains `- author -`. For example, `<environment-name> - author - <program-id> - <environment-id>`.

1. [Add users to the product profile](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles){target="_blank"}.
 
* [Configure AEM Assets to support Commerce metadata](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem)
* [Integrate AEM Assets with Commerce for asset synchronization](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)
