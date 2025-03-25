---
title: 'User management'
description: Learn how to manage users in [!DNL Adobe Commerce as a Cloud Service].
---
# User management

{{accs-early-access}}

If you want users to access the Admin in [!DNL Adobe Commerce as a Cloud Service], you need to add them as users in your organization and ensure they have access to the Cloud Service product in the [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

This process requires an IMS organization with access to [!DNL Adobe Commerce as a Cloud Service]. Only a System Admin for the organization can perform these processes

>[!TIP] To add multiple users simultaneously, you can perform a [bulk CSV upload](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.

## Add users, admins, and developers

1. Navigate to https://adminconsole.adobe.com and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce as a Cloud Service – Backend**] product.

    ![select product](./assets/backend.png){width="600" zoomable="yes"}

1. Click the [!UICONTROL **Default**] product profile.

1. Select the [!UICONTROL **Users**], [!UICONTROL **Admins**], or [!UICONTROL **Developers**] tab and click [!UICONTROL **Add Users**], [!UICONTROL **Add Admins**], or [!UICONTROL **Add Developers**].

    ![tab select](./assets/tab-select.png){width=600 zoomable="yes"}

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

You can also add multiple users to a role by creating a [user group](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}.

## Understanding roles

* **Users** - Users have access to the Commerce Admin.
* [**Developers**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Developers have user permissions and can create and use API credentials on Adobe I/O. 
* [**Admins**](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - Admins have user and developer permissions and can manage users, roles, and permissions for the product.

For more information, refer to the following Adobe Admin Console documentation:

* [Administrative roles](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"}
* [Manage developers](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}
