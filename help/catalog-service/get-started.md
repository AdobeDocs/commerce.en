---
title: Get Started with [!DNL Catalog Service]
description: Learn how to access the [!DNL Catalog Service] and integrate with frontend applications and third-party services.
role: Admin, Developer
---

# Get Started with the [!DNL Catalog Service]

After the [!DNL Catalog Service] is enabled, you can access the service and use it to retrieve catalog data, such as product and category information, from your Adobe Commerce instance. The service is available as a GraphQL API that you can access from the Commerce Admin or from any frontend application that supports GraphQL queries.

## Access the service

The [!DNL Catalog Service] is available as a GraphQL API that you can access from the Commerce Admin or from any frontend application that supports GraphQL queries. The service is available in both SaaS and PaaS environments.


[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."}

| Environment | Endpoint    |
|------------ | ----------: |
| **Testing**    | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Production** | `https://catalog-service.adobe.io/graphql` |

[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."}

|  Environment | Endpoint |
| ------------ | --------:|
| Testing | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
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

If you are using Adobe Commerce storefront on Edge Delivery Services, you add the Catalog Service endpoint to the storefront configuration. For details, see the [Edge Delivery Services documentation](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration).

For other integrations, see the project setup documentation for details on how to configure integrations between the service and backend data sources.


### Firewall configuration

To allow [!DNL Catalog Service] through a firewall, add `commerce.adobe.io` to the allowlist.

## Catalog Service and API Mesh

The [API Mesh for Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) enables developers to integrate private or third-party APIs and other interfaces with Adobe products using Adobe IO.

See the [[!DNL Catalog Service] and API Mesh](mesh.md) topic for installation and configuration details.

## Use the Data Management Dashboard

Use the [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) to monitor data synchronization between the [!DNL Catalog Service] and your Adobe Commerce instance. The dashboard provides insights into the data transfer process, including the status of data exports and a list of synced products.
