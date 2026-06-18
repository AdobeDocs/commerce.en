---
title: Identity and Access Management
description: Learn about the identity and access management features for Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
autotag-review: '2026-06-18T16:14:06.699Z'
TQID: 'https://experienceleague.adobe.com/lbI3nsLtafel6GtquXnkZmXD2Z3b-rRGPOyr8EqzrjE'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
role_v2:
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---

# Identity and access management

[!DNL Adobe Commerce as a Cloud Service] leverages Adobe's enterprise-grade identity infrastructure to ensure secure, scalable, and centralized access control across all environments. Identity and access management (IAM) in [!DNL Adobe Commerce as a Cloud Service] is designed to simplify user provisioning, enforce least-privilege access, and support compliance with global security standards.

- **[!DNL Adobe Identity Management Services (IMS)]**: [!DNL Adobe Commerce as a Cloud Service] uses [Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview) to authenticate users and manage entitlements. This includes support for federated identity providers and [role-based access control](../user-management.md).

- **Admin console governance**: Administrators manage access to the storefront and backend through the [!DNL Adobe Admin Console]. Permissions can be scoped to specific features and roles, ensuring least-privilege access.

## Adobe Identity Management Services (IMS)

[!DNL Adobe Commerce as a Cloud Service] uses [!DNL Adobe Identity Management Services (IMS)] to authenticate users and manage entitlements across the platform. IMS provides:

- **Federated identity support**: Integrate with enterprise identity providers, such as Azure AD and Okta, using SAML or OIDC.
- **Single Sign-On (SSO)**: Seamless access to [!DNL Adobe Commerce] and other [!DNL Adobe Experience Cloud] products.
- **Multi-Factor Authentication (MFA)**: Enforced at the organization level for enhanced security.
- **Global redundancy**: Identity data is stored in multi-region, load-balanced cloud infrastructure.

## Admin Console access control

The [!DNL Adobe Admin Console] is the central hub for managing user access to [!DNL Adobe Commerce as a Cloud Service]:

- **Role-Based Access Control (RBAC)**: Assign granular permissions to users based on their roles, such as Developer, Admin, and Analyst.
- **Product profiles**: Define access scopes for different environments, such as staging and production.
- **Delegated administration**: System Admins and Product Admins can manage user access without IT involvement.

See [user management](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management) for more information.

## API authentication and integration security

[!DNL Adobe Commerce as a Cloud Service]'s REST API authentication is handled through Adobe's [!DNL Adobe Identity Management Services (IMS)] using standardized OAuth 2 protocols. This authentication system supports both interactive user-based workflows and automated server-to-server integrations, ensuring secure and appropriate access for different use cases.

>[!NOTE]
>
>The Admin and integration token generation methods in PaaS versions of [!DNL Adobe Commerce] are not supported in SaaS environments. Instead, you must obtain an IMS admin token through OAuth authentication.

- **OAuth 2.0 support**: Secure token-based authentication for integrations and third-party services.
- **Scoped API access**: Limit API access to specific resources and operations.
- **Audit logging**: Track authentication events and access changes for compliance and troubleshooting.

See [REST authentication](https://developer.adobe.com/commerce/webapi/rest/authentication/) for more information.
