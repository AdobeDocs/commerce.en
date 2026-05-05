---
title: Integration Limits and Boundaries
description: Learn scope limits for third-party catalogs, auto-fix coverage, crawling prerequisites, enterprise scale considerations, and restricted beta access constraints for LLM Optimizer with Commerce.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
---
# Integration limits and boundaries

>[!IMPORTANT]
>
>Access to this integration is restricted. Contact your Technical Account Manager for details.

Use this topic to set expectations for what the [!DNL Adobe Commerce] and [!DNL Adobe LLM Optimizer] integration can automate, where you remain responsible, and which constraints are still evolving.

## Third-party catalog limitations {#third-party-catalog}

When the catalog **does not** live in [!DNL Adobe Commerce]:

- LLM Optimizer can still identify issues and suggest improvements using mirrored or imported catalog data, depending on your setup.
- **Direct auto-fix** into the merchant's commerce platform is not the same as writing into the merchant's source catalog. You may need a mirror catalog, export/import, or partner automation to apply changes.

For Commerce-hosted catalogs, approved name and description updates go to the Commerce system of record. See [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Scale and technical limits {#scale-limits}

Large catalogs and high URL counts can stress crawling, analysis, and edge-deploy patterns.

## Crawling and bot readability {#crawling}

Meaningful catalog and PDP insights assume that LLM-relevant **bots can access** the URLs you care about and that pages are structured so automated analysis is reliable. Robots rules, authentication, geo-blocking, and heavy personalization can reduce coverage.

## Related topics

- [Integration overview](overview.md)
- [Connect Adobe Commerce to LLM Optimizer](get-started/connect-to-llmo.md)
- [Use LLM Optimizer with Adobe Commerce](get-started/use-llmo-with-commerce.md)
