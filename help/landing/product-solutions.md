---
title: Commerce product solutions
description: Learn how to use badges to identify documentation that applies to different Adobe Commerce solutions (SaaS, PaaS, on-premises).
feature: Paas, Saas
recommendations: noDisplay, noCatalog
hide: yes
hidefromtoc: yes
---

# Adobe Commerce product solutions

Adobe offers several solutions to meet the requirements of your ecommerce business. The Adobe Commerce documentation on [Experience League](https://experienceleague.adobe.com/en/docs/commerce) and the [Adobe Developer](https://developer.adobe.com/commerce/docs/) site provides customers with self-service resources that support all solutions. However, navigating such a large volume of content can be challenging without guidance.

## Badges

Badges help you quickly identify whether the Commerce documentation that you find through conventional site navigation or internet search is relevant to the Commerce product solutions that you use. This is particularly important when content applies to one solution only.

If a badge is displayed, it means that the content applies to the specified solution only. If no badges are displayed, it means that the content applies to all Adobe Commerce solutions.

For example, if you're using Adobe Commerce as a Cloud Service, you should ignore content about [installing](../product-recommendations/install-configure.md#install-product-recommendations) the Product Recommendations extension and [configuring](../product-recommendations/install-configure.md#configure-product-recommendations) the Commerce Services Connnector. Adobe automatically completes these steps when you create an instance.

### Definitions

The following table defines the badges that display across Adobe Commerce documentation:

>[!BEGINSHADEBOX]

![info](../cloud-service/assets/Smock_InfoOutline_18_N.svg) The badges described here apply specifically to Adobe Commerce documentation. They do not represent how badges are used in the documentation for other Adobe Experience Cloud products.

>[!ENDSHADEBOX]

| Badge | Solution | Description |
|---------|----------|---------|
| [!BADGE SaaS only]{type=Positive tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."} | [Adobe Commerce as a Cloud Service](../cloud-service/overview.md)<br/><br/>[Adobe Commerce Optimizer](../optimizer/overview.md) | This badge identifies documentation for Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only. These projects are hosted on a cloud‑native, fully managed software-as-a-service (SaaS) solution where Adobe is responsible for most operational aspects—such as continuous updates, security monitoring, and scalability—so that customers can focus on commerce rather than infrastructure. |
| [!BADGE PaaS only]{type=Informative tooltip="Applies to Adobe Commerce on Cloud projects only (Adobe-managed PaaS infrastructure)."} | [Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) | This badge identifies documentation related to Adobe Commerce on Cloud projects only. These projects are hosted on a cloud‑native, fully managed platform-as-a-service (PaaS) solution with all Adobe Commerce's core features in a pre‑provisioned environment. |
| [!BADGE On-premises only]{type=Neutral tooltip="Applies to on-premises Adobe Commerce projects only (customer-managed hosting)."} | [Adobe Commerce on-premises](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) | This badge identifies documentation for Adobe Commerce on-premises projects only. This includes projects based on the Magento Open Source code base, even though not all Adobe Commerce features are available. Features exclusive to Adobe Commerce are marked accordingly. |
| [!BADGE PaaS & On-premises only]{type=Caution tooltip="Applies to Adobe Commerce on Cloud and on-premises Adobe Commerce projects only."} | [Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview)<br/><br/>[Adobe Commerce on-premises](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) | This badge identifies documentation for Adobe Commerce on Cloud and on-premises projects only. |

### Rules

Use these rules to understand what content applies to each Adobe Commerce solution:

- **Page-level badges**: Displayed at the top of a page (above the page title). Indicates that _all_ content on the page applies to the specified solution only.

- **Section-level badges**: Displayed immediately below all other headings on a page (except page title). Indicates that the content in that section applies to the specified solution only.

- **Inline badges**: Displayed within all non-heading page elements, such as tables, paragraphs, and lists. Indicates that the content in that element applies to the specified solution only.

>[!NOTE]
>
>Badges are intended to be mutually exclusive. That means you won't see more than one page- or section-level badge on the same page or section. However, multiple inline badges on the same page or in the same section are possible.
