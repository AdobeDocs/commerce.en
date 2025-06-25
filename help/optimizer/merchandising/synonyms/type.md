---
title: Synonym Types
description: Learn about the different types of synonyms in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: a74e48ea-e069-4ccc-a67f-2f85be251fb5
---
# Types of Synonyms

One- and two-way synonyms expand the definition of keywords. Some are interchangeable with the keyword, while others represent a subset of the keyword.

## Two-way

Two-way synonyms have the same meaning and return the same search results. In the following example, the first word shown in bold is the keyword that is used in the catalog, followed by words that have the same meaning as the original keyword. You can create a simple pair of two-way synonyms, or a chain of multiple two-way synonyms for the same keyword.

**jacket** ![Two-way selector](../../assets/btn-two-way.png) coat
**pants** ![Two-way selector](../../assets/btn-two-way.png) slacks ![Two-way selector](../../assets/btn-two-way.png) trousers

## One-way

A one-way synonym is a subset of a keyword, but with a more specific meaning. For example, capris and shorts are pants, but not all pants are capris or shorts. A search for pants includes capris and shorts. However, a search for shorts does not return capris.

**sweatshirt** ![One-way selector](../../assets/btn-one-way.png) hoodie
**pants** ![One-way selector](../../assets/btn-one-way.png) capris ![Multiple one-way selector](../../assets/btn-multiple-one-way.png) calf-length-pants ![Multiple one-way selector](../../assets/btn-multiple-one-way.png) peddle pushers

## Multi-word synonym behavior

For multi-word synonyms, [!DNL Adobe Commerce Optimizer] considers the synonym as a phrase. For example, if you create a two-way synonym **dining room table** ![Two-way selector](../../assets/btn-two-way.png) **kitchen table** ![Two-way selector](../../assets/btn-two-way.png) **dining table**, then [!DNL Adobe Commerce Optimizer] searches across all fields set to searchable for the occurrence of **dining room table** or **kitchen table** or **dining table**.

If no synonym is created and a shopper searches for **kitchen table**, [!DNL Adobe Commerce Optimizer] looks for the terms anywhere in the searchable fields, even across different fields, for example **table** in the name field and **kitchen** in the meta keyword.

After creating a synonym, the search behavior changes to look for the exact phrase **kitchen table**. This might reduce the number of results because only products with the exact phrase will be shown.

If you want the terms to be searched separately as before, you can [create a support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). If there is enough demand, [!DNL Adobe Commerce Optimizer] will consider adding this functionality to the product in a future release.
