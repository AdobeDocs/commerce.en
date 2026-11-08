---
title: Facet Types
description: Learn about the different types of facets in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: f4ab1f27-b393-45e0-94bf-c77d46e3f994
TQID: https://experienceleague.adobe.com/xuyEZ-CuFXUfhUi24ERf32uVNgENFTTdR5l-K22W4-M
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Types of Facets

[!DNL Adobe Commerce Optimizer] uses a variety of facets types and they appear in the *Filters* list only when relevant. The list of available facets changes according to the products returned. The following characteristics affect their presentation and behavior:

- Pinned facets  - The most commonly-used facets can be pinned to the top of the list. The remaining facets are listed in *Sort type* order after the pinned facets.
- Dynamic facets - Product attributes that [Adobe AI](https://business.adobe.com/ai.html) finds most relevant to a product set and query. The calculation takes into account the attribute metadata of the entire catalog and determines at query time the most relevant facets for the query.
- Price facets - Return products by price range. You can specify the number of selections and the price range interval on the [*Settings*](../../settings.md) workspace.

## Facet labels

You can edit facet labels from the [faceting workspace](workspace.md).

## Sort type

All facets rendered for the storefront are sorted alphabetically or by count.

| Sort type | Description |
|--- |--- |
| Alphabetic | In the storefront *Filters* list, facets are sorted alphabetically. |
| Count | Facets can also be sorted by the number of values found per facet in the current set of returned products. |
