---
title: Restricted Access Keys
description: "Learn how to create, assign, and rotate restricted access keys to protect catalog views in [!DNL Adobe Commerce Optimizer] with signed-token authentication."
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
nudge: true
---
# Restricted access keys

Restricted access keys let authorized client applications access a private [catalog view](catalog-view.md)—only requests carrying a valid signed token from an assigned key can retrieve catalog data. All other requests are denied, including those from anonymous shoppers, shoppers who haven't been explicitly given access to this catalog view, and scripts probing the API.

## Restricted access key use cases

In [!DNL Adobe Commerce Optimizer], **[!UICONTROL Price Book ID]** determines which prices a request sees—it scopes pricing, not who can make the request. Any client that knows a catalog view's ID and price book ID can retrieve that data through the Merchandising API. Restricted access keys add a separate, complementary control: they scope who can access a catalog view at all, independent of which price book applies.

Restricted access keys are commonly used for:

- **Contract-based B2B pricing**—Restrict a catalog view linked to a negotiated price book so only the buyer it applies to can query it. Other buying organizations and the public cannot.
- **Partner and reseller portals**—Limit a subset of the catalog to approved partners integrating directly with the Merchandising API.
- **Pre-release previews**—Let a trusted internal or partner system preview upcoming products before they're publicly visible.

>[!IMPORTANT]
>
>Key generation, token signing, and rotation are currently managed entirely by the backend client application that authenticates shoppers. [!DNL Adobe Commerce Optimizer] does not generate or rotate these keys on your behalf.

## How restricted access keys work

A restricted access key is the public component of an RSA key pair. Your client application generates and uses this key to prove it is authorized to read a private catalog view. In this context, "client application" means the backend system that authenticates shoppers—for example, custom logic on [!DNL Adobe Commerce] or a third-party backend—never the storefront frontend itself.

The following steps describe how a key pair and signed token move from creation to validation:

1. Your client application generates an RSA key pair and keeps the private key.
1. You register the **public** key in [!DNL Commerce Optimizer] as a restricted access key.
1. Your client application signs a JSON Web Token (JWT) with the private key and includes it with each request to a private catalog view.
1. [!DNL Commerce Optimizer] validates the token's signature against the registered public key and, if valid, returns the requested catalog data.

## Create a restricted access key

For initial testing of private catalog views, generate a key pair using a tool such as [!DNL OpenSSL]. Keep the private key secret — only the public key is uploaded to [!DNL Commerce Optimizer].

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

The key size must be between 2048 and 8192 bits. `public-key.pem` contains the value you paste into the **[!UICONTROL Public key]** field below.

## Add a restricted access key to [!DNL Commerce Optimizer]

1. From the left menu in [!DNL Adobe Commerce Optimizer Studio], go to **[!UICONTROL Store setup]**, and click **[!UICONTROL Restricted access keys]**.

   ![Restricted Access Keys list, with the Add Restricted Access Key button](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Click **[!UICONTROL Add Restricted Access Key]**.

1. Enter the key details:

    ![Add restricted access key form, with Title, Expiration date, and Public key fields](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

    - **[!UICONTROL Title]**—A label to identify the key, shown in the key list and the catalog view key picker, for example `ACME Corp wholesale portal — Tier 1 pricing`.
    - **[!UICONTROL Expiration date]**—Date and time (UTC) after which the key stops being honored, even for a token that hasn't expired yet.
    - **[!UICONTROL Public key]**—The PEM-encoded RSA public key in Subject Public Key Info (SPKI) format, including the `-----BEGIN PUBLIC KEY-----` and `-----END PUBLIC KEY-----` markers. Must be unique across the environment.

1. Click **[!UICONTROL Save]**.

Keys are immutable after creation. To change any value, delete the key and create a new one. See [Rotate a key](#rotate-a-key) to do this without an access interruption.

## Assign a key to a catalog view

A restricted access key only restricts access after it's assigned to a catalog view with **[!UICONTROL Catalog Protection]** enabled. See [Protect a catalog view](private-catalog-view.md#protect-a-catalog-view) for setup steps.

## Delete a key

1. On the **[!UICONTROL Restricted access keys]** page, find the key you want to remove and click **[!UICONTROL Delete]**.

   If the key is assigned to one or more catalog views, a warning explains that client applications relying on that key lose access. The catalog views themselves remain protected—they don't become publicly accessible.

1. Confirm the deletion.

## Rotate a key

To rotate a key without an access interruption, note that a catalog view can have up to three keys assigned at once:

1. Generate a new key pair and add the new public key as a new restricted access key.
1. Assign the new key to the catalog view alongside the existing key.
1. Start signing new tokens with the new private key to complete the key rollover.
1. Once all client applications are confirmed on the new key, remove and delete the old key.

## Limits

See [Catalog views and policy limits](boundaries-limits.md).

## More like this

- [Private catalog views](private-catalog-view.md)—Learn how to protect a catalog view with restricted access keys.

