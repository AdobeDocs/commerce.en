---
title: Types of Synonyms
description: One- and two-way [!DNL Adobe Commerce Optimizer] synonyms expand the definition of keywords.
exl-id: f5522428-c7cc-4627-a09b-d9148918c127
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

## Best practices

Keep in mind the following best practices to get the most from [!DNL Adobe Commerce Optimizer] synonyms.

### Avoid "stop words"

[!DNL Adobe Commerce Optimizer] filters out common English "stop words" from synonyms, such as:

a, an, and, are, as, at, be, but, by, for, if, in, into, is, it, no, not, of, on, or, such, that, the, their, then, there, these, they, this, to, was, will, with

Stop words do not make synonyms more meaningful, but increase the amount of data that must be processed.

### Use of singular and plural

It is not necessary to define both the singular and plural forms of a word as a synonym. If you have a mixture of singular and plural terms in your catalog, Search finds the correct set of products. For example, if you use the word "pant" in the product name and a shopper searches for "pants", the correct set of products is returned, and the singular word "pant" is offered as a suggestion. The singular term "pant" is often used in the fashion industry and sometimes in retail, although the plural form "pants" is more commonly used in some areas. (The word "pant" technically refers to the part of a garment that covers one leg, which is why you need a "pair of pants" to cover both legs.)

### Consistency

Be consistent with the way terminology is used in your catalog. Keep in mind that there might be regional differences in usage, and sometimes differences within an industry.

## Multi-word synonym behavior

For multi-word synonyms, Commerce considers the synonym as a phrase. For example, if you create a two-way synonym **dining room table** ![Two-way selector](../../assets/btn-two-way.png) **kitchen table** ![Two-way selector](../../assets/btn-two-way.png) **dining table**, then Commerce searches across all fields set to searchable for the occurrence of **dining room table** or **kitchen table** or **dining table**.

If no synonym is created and a shopper searches for **kitchen table**, Commerce looks for the terms anywhere in the searchable fields, even across different fields, for example **table** in the name field and **kitchen** in the meta keyword.

After creating a synonym, the search behavior changes to look for the exact phrase **kitchen table**. This might reduce the number of results because only products with the exact phrase will be shown.

If you want the terms to be searched separately as before, you can [create a support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). If there is enough demand, Commerce will consider adding this functionality to the product in a future release.
