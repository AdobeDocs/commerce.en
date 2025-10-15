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

>[!BEGINTABS]

>[!NOTE]
>
>Assign product admins the [User role](#add-users) before adding them as product admins. The User role is required for basic Commerce permissions.

>[!TAB GA (Provisioned after October 13, 2025)]

1. Navigate to <https://adminconsole.adobe.com> and sign in with your Adobe ID.

1. Select your organization.

1. Select the [!UICONTROL **Users**] tab.

1. Select the [!UICONTROL **Administrators**] tab.

1. Click [!UICONTROL **Add Admin**].

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Next**].

1. Select the [!UICONTROL **Product profile administrator**] role.

1. Click **+** to add products.

1. Select the existing Commerce Optimizer instance to add the admin to. Commerce Optimizer instances use the following format: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Select the product profile.

1. Click [!UICONTROL **Apply**].

1. Click [!UICONTROL **Save**].

>[!TAB Early access (Provisioned before October 13, 2025)]

1. Navigate to <https://adminconsole.adobe.com> and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] product.

    ![select product](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Select the [!UICONTROL **Admins**] tab.

1. Click [!UICONTROL **Add Admin**].

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

>[!ENDTABS]

## Add users

The following instructions provide information on how to add users to the [!DNL Commerce Cloud Manager] and Commerce Optimizer. The [!DNL Commerce Cloud Manager] interface allows you to create and manage your Commerce Optimizer instances. This process is required for all users, including developers and admins.

>[!NOTE]
>
>Only product admins and system admins can add users and developers to the Adobe Commerce as a Cloud Service product.

>[!BEGINTABS]

>[!TAB GA (Provisioned after October 13, 2025)]

1. Navigate to <https://adminconsole.adobe.com> and sign in with your Adobe ID.

1. Select your organization.

1. Select the [!UICONTROL **Products**] tab.

1. Select the [!UICONTROL **Adobe Commerce**] product.

1. Select the Commerce Cloud Manager product if you want to add the user to the Commerce Cloud Manager interface, where they can create and manage Commerce Optimizer instances, or select the existing Commerce Optimizer instance to add the user to. Commerce Optimizer instances use the following format: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Select the [!UICONTROL **Users**] tab and click [!UICONTROL **Add Users**].

1. Enter the username or email address of the users you want to add and click [!UICONTROL **Save**].

1. Select the desired product profile.

1. Click [!UICONTROL **Apply**].

1. Click [!UICONTROL **Save**].

>[!TAB Early access (Provisioned before October 13, 2025)]

1. Navigate to <https://adminconsole.adobe.com> and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] product.

    ![select product](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. Click the [!UICONTROL **Default - Cloud Manager**] product profile.

1. Select the [!UICONTROL **Users**] tab and click [!UICONTROL **Add Users**].

    ![tab select](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Enter the username or email address of the users you want to add and click [!UICONTROL **Save**].

>[!ENDTABS]

### Add developers and product profile admins

To add developers and product profile admins, repeat the [add users](#add-users) process, but select the [!UICONTROL **Developers**] or [!UICONTROL **Admins**] tab instead of the [!UICONTROL **Users**] tab.

>[!NOTE]
>
>Assign developers the User role before adding them as developers. The User role is required for basic Commerce permissions.

![tab select](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## Bulk user management

You can add multiple users more efficiently with one of the following methods:

- Use the **Add Users by CSV** feature in the Adobe Admin Console to perform a [bulk CSV upload](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Add multiple users to a role by creating a [user group](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Then, add the [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] product to the user group.

