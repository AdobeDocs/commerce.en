---
title: AEM Assets Integration release notes
description: Review the release notes for information about all AEM Assets Integration releases.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
---
# AEM Assets Integration release notes

These release notes describe the initial release of AEM Assets Integration and include:

![New](../assets/new.svg) New features
![Fixed issue](../assets/fix.svg) Fixes and improvements
![Known issue](../assets/bug.svg) Known issues

For feature changes and fixes released outside of the regular feature release version, review the _Hosted service updates_ sections.

Learn more about upcoming releases, product support, and which Adobe Commerce versions support the AEM Assets Integration extension, see the Adobe Commerce [Release schedule](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) and [Product Availability](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) topics.

## Hosted service updates

These release notes describe feature changes and fixes that occurred and were released outside of the regular feature releases for the hosted service.

+++Hosted service updates

_September 11, 2025_

![New issue](../assets/new.svg) Updated the [custom automatic matching](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} endpoints with a new `asset_matches` attribute.

_February 11, 2025_

![New issue](../assets/new.svg) Now, merchants can synchronize images for products and categories.

+++

## v1.2.6

_October 24, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-1163 --> Resolved an issue where consecutive bulk product update requests could leave the status tracking flag stuck preventing subsequent updates from processing correctly. Now, status is reset even if an error occurs.

## v1.2.5

_October 22, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-1161 --> Fixed an issue where updating the position of an existing image mapping in the Adobe Commerce Admin resulted in a PHP type error.

## v1.2.4

_October 17, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-1155 --> Improved overall stability of custom attributes. Custom attributes now update correctly when using asynchronous APIs.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-1074 --> Now, the [product-asset synchronization](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank} does not fail when a base link URL is defined.

## v1.2.3

_October 2, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-1135 --> Fixed an issue with updating product attributes. Product attributes now update as expected, and an appropriate error is returned instead of a 200 response when updates fail.

## v1.2.2

_September 18, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-1110 --> Improved overall image stability on mini cart, cart, and checkout pages. Images on these pages now load properly.

## v1.2.0

_August 7, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![New issue](../assets/new.svg)<!-- Issue ACAP-1018 --> Now, merchants can choose the source for image and media assets by selecting a [Visualization Owner](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} when configuring the Assets integration from the Admin.

![New issue](../assets/new.svg)<!-- Issue ACAP-1078 --> Updated the [custom automatic matching](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} endpoints with a new `asset_matches` attribute. This change allows you to implement your own matching logic to return all assets associated with a specific `productSku`.

## v1.1.2

_June 11, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![New issue](../assets/new.svg)<!-- Issue ACAP-1041 --> Added support for Adobe Commerce 2.4.8 and PHP 8.4.

## v1.1.0

_April 23, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![New issue](../assets/new.svg)<!-- Issue ACAP-955 --> Now, a [Custom Domain URL](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) can be used instead of the AEM Delivery URL. If a merchant sets a **Custom Domain Name** in their AEM dashboard, it is necessary to add this **Custom Domain URL** in Commerce.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-987 --> Improved overall logs for AEM Assets synchronization processes.

## v1.0.22

_March 12, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![New issue](../assets/new.svg)<!-- Issue ACAP-xx --> Now, the [Assets selector IMS Client ID](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization) is required by the Assets Selector to enable mapping AEM Assets images with product categories and Page Builder generated content.

## v1.0.20

_February 11, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce version 2.4.5 and later releases.

![New](../assets/new.svg)<!-- Issue ACAP-xx --> General availability release.
