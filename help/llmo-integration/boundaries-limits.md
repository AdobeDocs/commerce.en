---
title: Integration Limits and Boundaries
description: Learn scope limits for third-party catalogs, auto-fix coverage, crawling prerequisites, enterprise scale considerations, and beta or early-access constraints for LLMO with Commerce.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Integration limits and boundaries

Use this topic to set expectations for what the [!DNL Adobe Commerce] and [!DNL Adobe LLM Optimizer] integration can automate, where merchants remain responsible, and which constraints are still evolving.

## Third-party catalog limitations

When the catalog **does not** live in [!DNL Adobe Commerce]:

- LLMO can still **identify** issues and **suggest** improvements using mirrored or imported catalog data, depending on your setup.
- **Direct auto-fix** into the merchant's commerce platform is not the same as writing into Commerce core tables; you may need a **mirror catalog**, export/import, or partner automation to apply changes.

For Commerce-hosted catalogs, deploy of approved **name** and **description** updates targets the Commerce system of record. See [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Auto-fix scope and exclusions

- **Product Catalog Enrichment** focuses on shopper-visible fields such as **product name** and **product description** (exact field mapping follows your LLMO release).
- Recommendations for **additional structured or agent-oriented metadata** (hidden attributes, semantic tags, relationships) may be proposed separately and can depend on attribute and agent capabilities described in LLMO product documentation.
- Not every LLMO opportunity type results in a **one-click deploy** into Commerce; some improvements are guidance-only or require implementation in the storefront or CMS.

## Scale and technical limits

Large catalogs and high URL counts can stress crawling, analysis, and edge-deploy patterns. Adobe continues to document **enterprise-scale** limits—for example, very large PDP and PLP footprints—for specific integration paths (including workarounds that use extensibility projects). **Numeric limits may change** between releases; confirm current thresholds with release notes, field readiness materials, or your Adobe contact.

## Crawling and bot readability

Meaningful catalog and PDP insights assume that LLM-relevant **bots can access** the URLs you care about and that pages are structured so automated analysis is reliable. Robots rules, authentication, geo-blocking, and heavy personalization can reduce coverage.

## Beta and early-access constraints

Features described in the integration guides may ship in **beta** or **controlled availability** phases. UI labels, opportunity types, and deploy surfaces can differ by tenant. Your entitlement and onboarding email supersede generic documentation when they conflict.

## Related topics

- [Integration overview](overview.md)
- [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md)
- [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md)
