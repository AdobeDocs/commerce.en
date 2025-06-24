---
title: Synonym Best Practices
description: Learn the best practices for implementing synonyms in your store.
role: Admin, Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Synonym Best Practices

The following provides a list of best practices when creating synonyms.

- [!DNL Adobe Commerce Optimizer] manages misspellings by default. You can set up synonyms to include words that shoppers might use that differ from words specified in your catalog. You do not want to lose a sale because someone is looking for a "sofa", while your product is listed as a "couch". You can capture a broad range of search terms by entering all the possible words that customers might use to find your products. You can [set synonyms as one way or two way](add.md#step-2-define-the-synonym-by-type) to improve results.

- Map brand names and abbreviations to their full names, for example "HP" to "Hewlett-Packard" and common product nicknames, for example "iPhone" to "Apple iPhone".

- Include industry-specific jargon and terms that shoppers might use interchangeably, for example "sneakers" and "running shoes".

- Regularly update the synonym list based on new search trends, product additions, and shopper behavior.

- Test the effectiveness of synonym mappings by analyzing search results and shopper feedback. Refine mappings to improve accuracy and relevance.

- Avoid using stop words as they do not make synonyms more meaningful, but increase the amount of data that must be processed. [!DNL Adobe Commerce Optimizer] filters out common English "stop words" from synonyms, such as:

    a, an, and, are, as, at, be, but, by, for, if, in, into, is, it, no, not, of, on, or, such, that, the, their, then, there, these, they, this, to, was, will, with

- It is not necessary to define both the singular and plural forms of a word as a synonym. If you have a mixture of singular and plural terms in your catalog, Search finds the correct set of products. For example, if you use the word "pant" in the product name and a shopper searches for "pants", the correct set of products is returned, and the singular word "pant" is offered as a suggestion. The singular term "pant" is often used in the fashion industry and sometimes in retail, although the plural form "pants" is more commonly used in some areas. (The word "pant" technically refers to the part of a garment that covers one leg, which is why you need a "pair of pants" to cover both legs.)

- Be consistent with the way terminology is used in your catalog. Keep in mind that there might be regional differences in usage, and sometimes differences within an industry.
