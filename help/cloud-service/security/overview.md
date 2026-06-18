---
title: Security overview
description: Learn about the security features for Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
autotag-review: '2026-06-18T16:18:52.695Z'
TQID: 'https://experienceleague.adobe.com/AmkzZgLeOa9zJkPE8kWM6lFcFNtBAAOmJeULI-y4gOw'
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
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: adedf3b3-e153-47a3-ae73-b5d65067b544
    internal-label: Build system
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---

# Security overview

[!DNL Adobe Commerce as a Cloud Service] is engineered with security at its core—offering a modern, SaaS-native commerce platform that delivers enterprise-grade protection, operational resilience, and peace of mind for businesses of all sizes.

Unlike traditional PaaS models, the SaaS model eliminates the burden of manual patching, infrastructure maintenance, and upgrade cycles. Security is embedded into every layer of the platform—from Adobe-managed infrastructure and automated deployment pipelines to identity and access management through [!DNL Adobe IMS].

[!DNL Adobe Commerce as a Cloud Service] leverages Adobe's global security and compliance framework, ensuring alignment with industry standards such as ISO 27001, SOC 2, and GDPR. Customers benefit from a [shared responsibility model](./shared-responsibility.md) that clearly delineates Adobe's role in securing the platform and the customer's role in managing data and access.

With built-in protections like Web Application Firewall (WAF), DDoS mitigation, secure provisioning, and continuous vulnerability scanning, [!DNL Adobe Commerce as a Cloud Service] enables businesses to innovate faster without compromising on security.

This document outlines the security architecture, operational safeguards, and compliance posture of [!DNL Adobe Commerce as a Cloud Service]—empowering customers to make informed decisions and confidently scale their digital commerce operations.

## Content delivery network (CDN) & Web application firewall (WAF)

### Storefront CDN

Merchants can opt to deploy an Adobe-managed CDN or purchase their own CDN solution to protect their Commerce-powered storefront.

>[!IMPORTANT]
>
>If customers choose to deploy Adobe-managed CDN, they cannot configure CDN rules. Custom caching rules or WAF rules can be configured by the customers when they bring their own CDN to protect their Storefronts.

### [!DNL API Mesh for Adobe Developer App Builder] CDN

[!DNL API Mesh]'s CDN layer terminates TLS, runs the GraphQL gateway as Workers, provides global edge caching and automatic DDoS/WAF, and exposes `edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io` as the public mesh endpoints; customers can add their own CDN in front, but [!DNL API Mesh]'s CDN is fixed and managed by Adobe and customers cannot configure their own WAF rules.

For more information on [!DNL API Mesh]'s security features, refer to the [API Mesh documentation](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}.

### Backend CDN

A built-in CDN protects [!DNL Adobe Commerce as a Cloud Service].

Due to the [!DNL Adobe Commerce as a Cloud Service] architecture, when a merchant provisions an instance in a composite cell, such as `na1`, `eu1`, `au1`, or other geographic regions, three public surfaces are exposed:

| Surface | Example URL pattern |
| --- | --- |
| Admin UI | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| REST API | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| GraphQL API | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service] uses a combined WAF and CDN:

- **WAF** – Web Application Firewall protection for all [!DNL Adobe Commerce as a Cloud Service] public surfaces.
- **CDN** – Edge caching for static assets and cacheable GraphQL responses.

WAF and CDN are managed by the [!DNL Adobe Commerce as a Cloud Service] platform and are not configurable by the customers.

### DDoS protection

The built-in CDN and WAF provides both network‑layer and HTTP‑layer DDoS protection. [!DNL Adobe Commerce as a Cloud Service] does not expose those WAF or DDoS logs directly to merchants.

## Data storage and encryption

If data is being stored in [!DNL App Builder], then a merchant can refer to the [!DNL App Builder] [storage options](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/). [!DNL App Builder] enforces tenant isolation and access to data stored in these services is restricted to the runtime namespace in which the action is executed. There is no encryption of data in storage.

When using [!DNL API Mesh], secrets should be stored in the `secrets.yaml` file in your mesh configuration. [!DNL API Mesh] encrypts these secrets using AES-256 encryption ([https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/)).

Any data stored in [!DNL Adobe Commerce as a Cloud Service] is encrypted at rest using AES 256-bit encryption and all data is encrypted over HTTPS using TLS 1.2 or greater in transit.
