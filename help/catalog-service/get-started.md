---
title: Get Started with [!DNL Catalog Service]
description: Learn how to access the [!DNL Catalog Service] and integrate with frontend applications and third-party services.
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
TQID: https://experienceleague.adobe.com/KBdWesEoKJu-qWsY-Ny1Om-msUkyUPfUTQWftEqSg1g
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Get Started with the [!DNL Catalog Service]

After the [!DNL Catalog Service] is enabled, you can access the service and use it to retrieve catalog data, such as product and category information, from your Adobe Commerce instance. The service is available as a GraphQL API that you can access from the Commerce Admin or from any frontend application that supports GraphQL queries.

{{aco-merchandising-services}}

## Access the service

The [!DNL Catalog Service] is available as a GraphQL API that you can access from the Commerce Admin or from any frontend application that supports GraphQL queries. The service is available in both SaaS and PaaS environments.

[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}

| Environment  | Endpoint    |
| ------------ | ----------: |
| **Testing**  | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Production** | `https://catalog-service.adobe.io/graphql` |

[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."}

| Environment | Endpoint |
| ----------- | --------:|
| Testing     | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| Production (Not available yet) | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

**URL structure for SaaS endpoints**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>` is the cloud region where your instance is deployed.
- `<environment>` is the environment type, such as `sandbox`. If the environment is production, this value is omitted.
- `<tenantId>` is the unique identifier for your organization's specific instance within the Adobe Experience Cloud.

For details about using the Catalog Service GraphQL API, see the [Catalog Service for Adobe Commerce Guide](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) in the *Adobe Commerce Developer* documentation.

## Integrate with a headless storefront or third-party services

To integrate with a headless storefront, you must update the storefront configuration to enable communication between the storefront and the [!DNL Catalog Service] to retrieve product and category data.

If you are using Adobe Commerce storefront on Edge Delivery Services, add the Catalog Service endpoint to the storefront configuration. For details, see the [Edge Delivery Services documentation](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration).

For other integrations, see the project setup documentation for details on how to configure integrations between the service and backend data sources.

### Firewall configuration

To allow [!DNL Catalog Service] through a firewall, add `commerce.adobe.io` to the allowlist.

## Catalog Service and API Mesh

The [API Mesh for Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) enables developers to integrate private or third-party APIs and other interfaces with Adobe products using Adobe IO.

See the [[!DNL Catalog Service] and API Mesh](mesh.md) topic for installation and configuration details.

## Monitor and troubleshoot data export

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

Use the [Commerce CLI](../data-export/data-export-cli-commands.md) to manually resync feeds when needed. For resync options and additional troubleshooting steps, see [Manage synchronization](../data-export/data-sync-manage.md) in the _SaaS Data Export Guide_.

>[!NOTE]
>
>If the Data Feed Sync Status page is not available in the Commerce Admin for Commerce on Cloud or on premises deployments, follow the [extension installation instructions](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension).
