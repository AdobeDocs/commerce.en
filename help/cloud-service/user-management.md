---
title: 'User management'
description: Learn how to manage users in [!DNL Adobe Commerce as a Cloud Service].
---
# User management

{{accs-early-access}}

If you want users to access the Admin in [!DNL Adobe Commerce as a Cloud Service], you need to add them as users in your organization and ensure they have access to the Cloud Service product in the [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

This process requires an IMS organization with access to [!DNL Adobe Commerce as a Cloud Service]. Only a System Admin for the organization can perform these processes

>[!TIP]
>
>To add multiple users simultaneously, you can perform a [bulk CSV upload](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.

## Add users and admins

The following instructions provide information on how to add users and admins to the [!UICONTROL Commerce Cloud Manager]. This user interface allows you to create and manage your Commerce Instances. To manage users inside Adobe Commerce instead, refer to [manage user accounts](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.

>[!NOTE]
>
>Only product admins can add users and admins to the Adobe Commerce as a Cloud Service product.

1. Navigate to https://adminconsole.adobe.com and sign in with your Adobe ID.

1. Select your organization.

1. On the [!UICONTROL **Products**] tab, under [!UICONTROL **Products and Services**], select the [!UICONTROL **Adobe Commerce as a Cloud Service – Backend**] product.

    ![select product](./assets/backend.png){width="600" zoomable="yes"}

1. Click the [!UICONTROL **Default**] product profile.

1. Select the [!UICONTROL **Users**] or [!UICONTROL **Admins**] tab and click [!UICONTROL **Add Users**], [!UICONTROL **Add Admins**], or [!UICONTROL **Add Developers**].

    ![tab select](./assets/tab-select.png){width=600 zoomable="yes"}

1. Enter the username or email address of the users you want to add as admins and click [!UICONTROL **Save**].

You can also add multiple users to a role by creating a [user group](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}.

## Understanding roles

* **Users** - Users have Admin access to the Commerce Admin, and can manage users inside Commerce, but cannot manage product-level access. Users can also use credits to [create instances](./getting-started#create-an-instance) in the [!UICONTROL Commerce Cloud Manager].

* [**Admins**](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - In addition to user permissions, admins can [Manage users, roles, and permissions for the product](#add-users-and-admins)

>[!NOTE]
>
>The Developer and API Credential roles are not currently supported.

For more information, refer to [Administrative roles](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"}.
