---
title: User management
description: Learn how to manage users in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# User management

>[!NOTE]
>
>This User Management documentation is for Early Access participants with onboarding instructions to manage and and provision Adobe Commerce Optimizer users within their Adobe organization. If you don’t have these instructions, contact your account representative for assistance with user management.

If you want users to access the Admin in [!DNL Adobe Commerce Optimizer], you need to add them as users in your organization and ensure they have access to the Cloud Service product in the [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

This process requires an IMS organization with access to [!DNL Adobe Commerce Optimizer]. Only a System Admin or Product Admin for the organization can perform these processes.

>[!TIP]
>
>To add multiple users simultaneously, you can perform a [bulk CSV upload](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> You can also add multiple users to a product profile by creating a [user group](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Then you can add the [!UICONTROL **Adobe Commerce as a Cloud Service – Backend**] product to the user group. 

## Understanding roles

The following roles are available for [!DNL Adobe Commerce Optimizer].

* **User** - Users have access to the Commerce Optimizer UI to view and manage Merchandising, Catalog, and Data Insight capabilities.

* [**Developers**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Developers have user permissions and access to the Adobe Developer Console. This means they can create projects and configure credentials to use developer tools like the Adobe Commerce Optimizer APIs and SDKs along with Adobe extensibility tools like App Builder and API Mesh.

* Admins - There are three different types of admins:
    * [System admins](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - The system admin has access to all products and product profiles in the organization through the Adobe Admin Console.
    * [Product admins](#add-a-product-admin) - Product admins can [manage users, roles, and permissions for the product](#add-users-and-admins) in the [!DNL Adobe Admin Console].
    * [Product profile admins](#add-users-developers-and-product-profile-admins) - Product profile admins can manage users for the product in the [!DNL Adobe Admin Console].

## Add a product admin

>[!NOTE]
>
>During the Early Access period, user provisioning for Adobe Commerce Optimizer is managed using the **Adobe Commerce as a Cloud Service – Backend** product.

1. Navigate to https://adminconsole.adobe.com and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce as a Cloud Service – Backend**] product.

    ![select product](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Select the [!UICONTROL **Admins**] tab.

1. Click [!UICONTROL **Add Admin**].

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

## Add users, developers, and product profile admins

The following instructions provide information on how to add users and developers to the [!DNL Commerce Cloud Manager]. The [!DNL Commerce Cloud Manager] interface allows you to create and manage your Commerce Instances.

>[!NOTE]
>
>Only product admins and system admins can add users and developers to the Adobe Commerce as a Cloud Service product.

1. Navigate to https://adminconsole.adobe.com and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce as a Cloud Service – Backend**] product.

    ![select product](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Click the [!UICONTROL **Default - Cloud Manager**] product profile.

1. Select the [!UICONTROL **Users**], [!UICONTROL **Developers**], or [!UICONTROL **Admins**] tab and click [!UICONTROL **Add Users**] or [!UICONTROL **Add Developers**] or [!UICONTROL **Add Admins**].

    >[!NOTE]
    >
    >Admins added from this screen are assigined to the [product profile admins](#understanding-roles) group.

    ![tab select](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"} (!!!NEED NEW SCREENSHOT SPECIFIC FOR ACO PRODUCT)

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

