---
title: User management
description: Learn how to manage users in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
---
# User management

To enable access to [!DNL Adobe Commerce Optimizer], add users from the [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} and ensure that they have access to the Commerce product.

You can assign users to any of the following roles:

- **User**— Users have access to the [!DNL Adobe Commerce Optimizer] UI to view and manage catalog views and merchandising rules, and track performance metrics.

- [**Developer**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}— Developers have user permissions and access to the Adobe Developer Console. This means they can create projects and configure credentials to use developer tools like the [!DNL Adobe Commerce Optimizer]  APIs and SDKs along with Adobe extensibility tools like App Builder and API Mesh.

- **Admin** - There are three different types of admin roles:
    - [System admins](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - The system admin has access to all products and product profiles in the organization through the Adobe Admin Console.
    - [Product admins](#add-a-product-admin) - Product admins can [manage users, roles, and permissions for the product](#add-users-and-admins) in the [!DNL Adobe Admin Console].
    - [Product profile admins](#add-users-developers-and-product-profile-admins) - Product profile admins can manage users for the product in the [!DNL Adobe Admin Console].

## Add a product admin

1. Navigate to the [Admin console](https://adminconsole.adobe.com), and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce as a Cloud Service – Backend**] product.

    ![select product](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Select the [!UICONTROL **Admins**] tab.

1. Click [!UICONTROL **Add Admin**].

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

## Add users, developers, and product profile admins

>[!BEGINSHADEBOX "Prerequisites"]
>
The following provisioning is required for user management:

- IMS organization provisioned for [!DNL Adobe Commerce Optimizer]
- An Adobe Experience Cloud account in the same IMS organization with the system or product admin role
  
>[!ENDSHADEBOX]

Use the following instructions to add users and developers to the [!DNL Commerce Cloud Manager], where you manage your Commerce instances.

1. Navigate to [Adobe Admin Console](https://adminconsole.adobe.com) and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce as a Cloud Service – Backend**] product.

    ![select product](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Click the [!UICONTROL **Default - Cloud Manager**] product profile.

1. Select the [!UICONTROL **Users**], [!UICONTROL **Developers**], or [!UICONTROL **Admins**] tab and click [!UICONTROL **Add Users**] or [!UICONTROL **Add Developers**] or [!UICONTROL **Add Admins**].

   Admins added from this screen are assigned to the [product profile admins](#understanding-roles) group.

   ![tab select](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

## Bulk user management

You can add multiple users more efficiently with one of the following methods:

- Use the **Add Users by CSV** feature in the Adobe Admin Console to perform a [bulk CSV upload](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Add multiple users to a role by creating a [user group](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Then, add the [!UICONTROL **Adobe Commerce as a Cloud Service – Backend**] product to the user group.
