---
title: Verify Migration Service Access
description: Learn how to verify end-to-end access to the Commerce Data Migration Service API, confirming network reachability, IMS authentication, and tenant authorization.
feature: Cloud
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Verify migration service access

{{bulk-data-early-access}}

Use this guide to verify end-to-end access to the Commerce Data Migration Service (CDMS) API from your environment. A successful call simultaneously validates network reachability from your egress IPs (IP allowlisting), IMS authentication, and tenant authorization.

Complete this guide after you finish all items in the [Customer readiness checklist](readiness-checklist.md) and before you run the migration described in the [migration guide](migration-guide.md).

## Prerequisites

- An OAuth 2.0 Server-to-Server credential (client ID and client secret) created in the [Adobe Developer Console](https://developer.adobe.com/console/).
- Your IMS organization ID, in the format `<org>@AdobeOrg`. The organization must own the target tenant.
- The target `tenantId`, a 22-character, alphanumeric IMS tenant ID.
- Your outbound egress IP addresses allowlisted for the CDMS gateway. Coordinate with the Adobe team if you are unsure.
- The region-specific service host from the [Service hosts by environment and region](#service-hosts-by-environment-and-region) table.

## Generate an IMS access token

Generate an access token using your OAuth 2.0 Server-to-Server credentials with the `client_credentials` grant. The IMS host in this step is the same for all data regions. Only the CDMS host changes per region.

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## Call the List Migrations API

The following request retrieves the list of migrations for the tenant and requires the access token from the previous step. Select the host for your region from the [Service hosts by environment and region](#service-hosts-by-environment-and-region) table. The `-i` flag prints the HTTP status line and response headers so you can confirm the result.

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## Interpret the response

| HTTP code | Meaning | Example response body |
| --- | --- | --- |
| 200 | Success. Connectivity, authentication, and tenant authorization all passed. The response body contains the list of migrations for the tenant. | `{"migrations":[...]}` |
| 401 | Missing or invalid Bearer token, rejected before reaching the service. [Regenerate the token](#generate-an-ims-access-token). | Varies (gateway-generated) |
| 403 | The authenticated user does not have migration permissions for this tenant. | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | Internal server error. | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>If the request times out or the connection is refused, and no HTTP status is returned, your egress IP is likely not allowlisted, or you are using an incorrect host. Confirm the region host in the following table and your allowlisted IPs.

## Service hosts by environment and region

| Region or environment | Host |
| --- | --- |
| Sandbox or pre-production | `https://na1-sandbox.api.commerce.adobe.com` |
| North America | `https://na1.api.commerce.adobe.com` |
| Europe | `https://eu1.api.commerce.adobe.com` |
| India | `https://in1.api.commerce.adobe.com` |
| UK | `https://uk1.api.commerce.adobe.com` |
| Australia and New Zealand | `https://au1.api.commerce.adobe.com` |

## Next steps

After you confirm access, proceed to the [migration guide](migration-guide.md) to begin environment configuration and migration execution.
