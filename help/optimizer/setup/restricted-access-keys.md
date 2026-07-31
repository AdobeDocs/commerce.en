---
title: Restricted Access Keys
description: Learn how to create, assign, and rotate restricted access keys to protect catalog views in Adobe Commerce Optimizer with signed-token authentication.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Restricted access keys

Restricted access keys let you protect a [catalog view](catalog-view.md) so that only requests carrying a valid signed token can retrieve its product and pricing data. Everyone else, including anonymous shoppers, other storefronts, or scripts probing the API, is denied.

## Restricted access key use cases

Restricted access keys are commonly used for:

- **Contract-based B2B pricing**—Show negotiated account pricing only to the buyer it applies to, without exposing it publicly.
- **Partner and reseller portals**—Limit a subset of the catalog to approved partners integrating directly with the Merchandising API.
- **Pre-release previews**—Let a trusted internal or partner system preview upcoming products before they're publicly visible.

## How restricted access keys work

A restricted access key is the public half of an RSA key pair that your client application generates and uses to prove it is authorized to read a protected catalog view:

1. Your client application generates an RSA key pair and keeps the private key.
1. You register the **public** key in [!DNL Adobe Commerce Optimizer] as a restricted access key.
1. Your client application signs a JSON Web Token (JWT) with the private key and includes it with each request to a protected catalog view.
1. [!DNL Adobe Commerce Optimizer] validates the token's signature against the registered public key and, if valid, returns the requested catalog data.

>[!IMPORTANT]
>
>Key generation, token signing, and rotation are currently managed entirely by your client application. [!DNL Adobe Commerce Optimizer] does not generate or rotate these keys on your behalf.

## Create a restricted access key

Before you begin, generate an RSA key pair using a tool such as [!DNL OpenSSL]. Keep the private key secret — only the public key is uploaded to [!DNL Adobe Commerce Optimizer].

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

The key size must be between 2048 and 8192 bits. `public-key.pem` contains the value you paste into the **Public key** field below.

1. From the left menu, go to **[!UICONTROL Store setup]**, and click **[!UICONTROL Restricted access keys]**.

   ![Restricted Access Keys list, with the Add Restricted Access Key button](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Click **[!UICONTROL Add Restricted Access Key]**.

1. Enter the key details:

    ![Add Restricted Access Key form, with Title, Expiration Date, and Public key fields](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

    - **Title**—A label to identify the key, shown in the key list and in the catalog view's key picker, for example `ACME Corp wholesale portal — Tier 1 pricing`.
    - **Expiration date**—Date and time (UTC) after which the key stops being honored, even for a token that hasn't expired yet.
    - **Public key**—The PEM-encoded RSA public key in Subject Public Key Info (SPKI) format, including the `-----BEGIN PUBLIC KEY-----` and `-----END PUBLIC KEY-----` markers. Must be unique across the environment.

1. Click **[!UICONTROL Save]**.

Keys are immutable after creation. To change any value, delete the key and create a new one. See [Rotate a key](#rotate-a-key) to do this without an access interruption.

## Assign a key to a catalog view

A restricted access key only restricts access after it's assigned to a catalog view with **[!UICONTROL Catalog Protection]** enabled. See [Protect a catalog view](private-catalog-view.md#protect-a-catalog-view) for setup steps.

## Delete a key

1. On the **[!UICONTROL Restricted access keys]** page, find the key you want to remove and click **[!UICONTROL Delete]**.

   If the key is assigned to one or more catalog views, a warning explains that clients relying on that key will lose access. The catalog views themselves remain protected—they don't become publicly accessible.

1. Confirm the deletion.

## Rotate a key

To rotate a key without an access interruption, use the fact that a catalog view can have up to three keys assigned at once:

1. Generate a new key pair and add the new public key as a new restricted access key.
1. Assign the new key to the catalog view alongside the existing key.
1. Start signing new tokens with the new private key and roll your clients over.
1. Once all clients are confirmed on the new key, remove and delete the old key.

## Limits

| Limit | Value |
| --- | --- |
| Restricted access keys per catalog view | 3 |
| RSA key size | 2048-bit minimum, 8192-bit maximum |

## More like this

- [Catalog views](catalog-view.md)—Learn how to protect a catalog view with restricted access keys.

