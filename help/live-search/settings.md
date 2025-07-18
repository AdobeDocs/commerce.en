---
title: Settings
description: Configure settings for the [!DNL Live Search] service.
exl-id: 6387a365-7e23-4023-95ac-27908164d81c
---
# Settings

Use the *Settings* workspace to configure the price facet ranges and intervals and the default language for the index. 

Price faceting specifies the number of price range groups and how price values are distributed among them.

The Language setting tells the [!DNL Live Search] service which language to expect when writing the index.

![Settings](assets/settings.png)

## Price faceting

You can specify the number of price range groups and how price values are distributed among them. Each price range overlaps the previous group by one. For example, five groups with an interval of 20 creates the following price ranges: 0-20, 20-40, 40-60, 60-80, and >80. If there are not enough products in the catalog to fill all defined ranges, the display of the available groups is adjusted accordingly. For example: 0-20, 60-80, >80.

1. In the Admin, go to **Marketing** > *SEO & Search* > **[!DNL Live Search]**.
1. On the **Settings** workspace under *Price faceting*, do the following:
   * Enter the **Number of selections**, or price groupings to be available. With [!DNL Live Search] 4.4.0, you can define up to 100 price groupings. Earlier versions allowed 50 price groupings.
   * Enter the **Interval value**, or price range for each group. The maximum value is 40,000,000.
1. Click **Save**.

   It takes about 15 minutes for the updated settings to be available in the storefront.

### Field descriptions

| Field | Description |
|--- |--- |
| Number of selections | Specifies the number of price range groupings that can be used as search filters in the storefront. Default value: 8, Maximum value: 100 (as of [!DNL Live Search] 4.4.0)|
| Interval value | Specifies the price range interval for each group. For example, five selections with an interval value of 20 creates five groupings of 0-20, 20-40, 40-60, 60-80, and >80. Default value: 5, Maximum value: 40,000,000 |

## Language

The Language setting tells [!DNL Live Search] which language to expect when reading the catalog and writing the index. 

Languages have different sets of rules for grammar: how words are separated, verb tenses and word forms, for example.
The Language setting ensures that the correct set of rules are applied to the indexing mechanism.

Set the Language setting to the primary language of the catalog. When changing the language of the index, it can take from 5 to 60 minutes to reflect the change on the storefront, depending on the size and complexity of the catalog.

|Language|Code|
|----|----|
|Arabic|ar|
|Armenian|hy|
|Basque|eu|
|Bengali|bn|
|Brazilian|pt-br|
|Bulgarian|bg|
|Catalan|ca|
|Chinese (Simplified)|zh-cn|
|Chinese (Traditional)|zh-tw|
|Czech|cs|
|Danish|da|
|Dutch|nl|
|English|en|
|Estonian|et|
|Finnish|fi|
|French|fr|
|Galician|gl|
|German|de|
|Greek|el|
|Hindi|hi|
|Hungarian|hu|
|Indonesian|id|
|Irish|ga|
|Italian|it|
|Japanese (Katakana)|ja|
|Korean|ko|
|Latvian|lv|
|Lithuanian|lt|
|Norwegian|no|
|Persian|fa|
|Portuguese|pt|
|Romanian|ro|
|Russian|ru|
|Sorani|ku|
|Spanish|es|
|Swedish|sv|
|Turkish|tr|
|Thai|th|
