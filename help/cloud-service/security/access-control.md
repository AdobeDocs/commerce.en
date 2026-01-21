---
title: Identity and access management
description: Learn about the identity and access management features for Adobe Commerce as a Cloud Service.
role: Admin, Architect, Leader
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---

# Identity and access management

[!DNL Adobe Commerce as a Cloud Service] leverages Adobe's enterprise-grade identity infrastructure to ensure secure, scalable, and centralized access control across all environments. Identity and access management (IAM) in [!DNL Adobe Commerce as a Cloud Service] is designed to simplify user provisioning, enforce least-privilege access, and support compliance with global security standards.

- **[!DNL Adobe Identity Management Services (IMS)]**: [!DNL Adobe Commerce as a Cloud Service] uses IMS to authenticate users and manage entitlements. This includes support for federated identity providers and [role-based access control](../user-management.md).

- **Admin console governance**: Administrators manage access to the storefront and backend through the [!DNL Adobe Admin Console]. Permissions can be scoped to specific features and roles, ensuring least-privilege access.

## Adobe Identity Management Services (IMS)

[!DNL Adobe Commerce as a Cloud Service] uses [!DNL Adobe Identity Management Services (IMS)] to authenticate users and manage entitlements across the platform. IMS provides:

- **Federated identity support**: Integrate with enterprise identity providers (e.g., Azure AD, Okta) using SAML or OIDC.
- **Single Sign-On (SSO)**: Seamless access to [!DNL Adobe Commerce] and other [!DNL Adobe Experience Cloud] products.
- **Multi-Factor Authentication (MFA)**: Enforced at the organization level for enhanced security.
- **Global redundancy**: Identity data is stored in multi-region, load-balanced cloud infrastructure across North America, Europe, and APAC.

## Admin Console access control

The [!DNL Adobe Admin Console] is the central hub for managing user access to [!DNL Adobe Commerce as a Cloud Service]:

- **Role-Based Access Control (RBAC)**: Assign granular permissions to users based on their roles (e.g., Developer, Admin, Analyst).
- **Product Profiles**: Define access scopes for different environments (e.g., staging, production).
- **Delegated Administration**: System Admins and Product Admins can manage user access without IT involvement.

See [user management](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management) in the user guide for more information.

## API authentication & integration security

[!DNL Adobe Commerce as a Cloud Service] REST API authentication is handled through Adobe's [!DNL Identity Management System (IMS)] through standardized OAuth 2 protocols. This authentication system supports both interactive user-based workflows and automated server-to-server integrations, ensuring secure and appropriate access for different use cases.

>[!NOTE]
>
>The Admin and integration token generation methods in PaaS are not supported in SaaS environments. Instead, you must obtain an IMS admin token through OAuth authentication.

- **OAuth 2.0 support**: Secure token-based authentication for integrations and third-party services.
- **Scoped API access**: Limit API access to specific resources and operations.
- **Audit logging**: Track authentication events and access changes for compliance and troubleshooting.

See [REST authentication](https://developer.adobe.com/commerce/webapi/rest/authentication/) in the developer guide for more information.
