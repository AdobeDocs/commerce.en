---
title: "[!DNL Payment Services] Release Notes"
description: Review the release notes for information about all [!DNL Payment Services] releases.
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
---

# Release Notes

These release notes describe the initial release of [!DNL Payment Services] and include:

![New](../assets/new.svg) New features
![Fixed issue](../assets/fix.svg) Fixes and improvements
![Known issue](../assets/bug.svg) Known issues

For feature changes and fixes released outside of the regular feature release version, review the _Hosted service updates_ sections.

Learn more about upcoming releases, product support, and which Adobe Commerce versions support the [!DNL Payment Services] extension, see the Adobe Commerce [Release schedule](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) and [Product Availability](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) topics.

## Hosted service updates

These release notes describe feature changes and fixes that occurred and were released outside of the regular feature releases for the hosted service.

+++Hosted service updates

_April 25, 2025_

![New issue](../assets/new.svg)<!-- Issue PAY-6051 --> Now, [!DNL Payment Services] dashboard displays both the current extension version and the dashboard version.

_August 30, 2024_

![New issue](../assets/new.svg)<!-- Issue PAY-5658 --> Now, merchants can filter transactions by the Payment Detail in the [transactions report](reporting.md#transactions-report-view) for more detailed and accurate payment methods data.

_July 15, 2024_

![New issue](../assets/new.svg)<!-- Issue PAY-5571 --> Now, merchants can filter transactions by the Commerce customer email in the [transactions report](reporting.md#transactions-report-view). Enter the customer email to filter transactions for that specific email.

_July 9, 2024_

![New issue](../assets/new.svg)<!-- Issue PAY-5488 --> Now, merchants can view the Commerce customer ID as a column in the [transactions report](reporting.md#transactions-report-view) to help identify transactions that a particular customer has placed. In addition, merchants can filter the transactions report by this Commerce customer ID for associated orders.

_March 5, 2024_

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-5252 --> Now, merchants can copy data from the dashboard grids by selecting the content of a single cell.

_October 10, 2023_

![New issue](../assets/fix.svg)<!-- Issue PAY-4888 --> Now, merchants can filter credit and debit card transactions by the last four digits of the card number in the [Transactions report](reporting.md#transactions-report-view).

_July 12, 2023_

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-4587 --> An issue introduced in the [!DNL Payment Services] 2.1.0 release that prevented authorization voids placed by previous extension versions is now resolved. Merchants using any version of [!DNL Payment Services] can void authorizations.

_June 9, 2023_

![New](../assets/new.svg)<!-- Issue PAY-4288 --> Now, merchants can [configure _only_ PayPal payment buttons](payments-options.md#use-only-paypal-payment-buttons)---and _not_ use the PayPal credit card payment option. This allows merchants to provide various payment options, including Venmo and PayPal payment buttons, and use an existing credit card provider instead of the PayPal credit card payment option.

![New](../assets/new.svg)<!-- Issue PAY-4050 --> Added a [data visualization view](/help/payment-services/payouts.md#payouts-data-visualization-view), which appears on the Payment Service Home, for the Order payment status report.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-4486--> Previously, the PayPal PayLater button did not appear in checkout for UK merchants. That issue is resolved.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-4485--> Report data visualization views are now appearing on [!DNL Payment Services] Home when[!DNL Payment Services] is disabled.

_January 25, 2023_

![Known issue](../assets/bug.svg)<!-- Issue PAY-4102 --> New installations of [!DNL Payment Services] are unable to configure Commerce Services, rendering [!DNL Payment Services] inoperable. To fix this issue, update your [!DNL Payment Services] extension to version 1.5.3.

_September 12, 2022_

![New](../assets/new.svg)<!-- Issue PAY-3705 --> The `increment_id` is now available for use in reconciling payouts in external ERP systems. It is propagated to the `custom_id` _and_ `invoice_id`, visible in both the PayPal webhook and the merchant activity detail for a payout.

_August 31, 2022_

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3629 --> When a new merchant accesses the [!DNL Payment Services] Home for the first time, the page now loads immediately to display the content instead of requiring a page refresh.

_August 9, 2021_

![New](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay is now available as a PayPal Smart Button. This [payment option](payments-options.md#apple-pay-button) enables customers to use the Touch ID feature on their iOS or macOS device to select Apple Pay. Apple Pay processes the payment using the credit and debit card payment credentials stored on the device.

_June 28, 2021_

![New](../assets/new.svg)<!-- Issue PAY-1720 --> Disputes for store orders are now available in [the Order payment status report](/help/payment-services/order-payment-status.md#view-disputes). You can address disputes by navigating directly to the PayPal Resolution Center from [!DNL Payment Services].

![New](../assets/new.svg)<!-- Issue PAY-2854 --> User experience improvements from [!DNL Payment Services] Home include the ability to modify a configuration at the current inheritance level and improvements to the display of the header and navigation.

![New](../assets/new.svg)<!-- Issue PAY-2854 --> You can now see warnings when you switch from sandbox mode to production mode and when you attempt to navigate away from a view with updates that have not been saved.

![New](../assets/new.svg)<!-- Issue PAY-2761 --> You can now customize the data that displays in the [Order payment status report](/help/payment-services/order-payment-status.md#show-and-hide-columns) and the [Payouts report](/help/payment-services/payouts.md#show-and-hide-columns) by showing or hiding columns using the Column settings control.

+++

>[!NOTE]
>
> Releases occur frequently to deliver new features and fixes as needed. The release schedule is not fixed.

## v2.13.0

_November 10, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-xxxx --> Now, [!DNL Payment Services] supports PayPal's **One-Time Checkout (OTC)** modal, featuring built-in contact and delivery information.

![New](../assets/new.svg)<!-- PAY-xxxx --> Enhanced mobile experience through **PayPal app-switch authentication**, along with improved API integration for smoother user journeys. This feature is only available for US [!DNL Payment Services] based customers.

![New](../assets/new.svg)<!-- PAY-xxxx --> Added **3D Secure (3DS)  authentication** support for Fastlane to meet **Strong Customer Authentication (SCA)** requirements. This Enables UK, and EU [!DNL Payment Services] merchants to process transactions with **3DS authentication**, enhancing fraud prevention and ensuring compliance with regional regulations.

![New](../assets/new.svg)<!-- PAY-xxxx --> Now, [!DNL Payment Services] merchants can choose between **light, and dark themes** for the Fastlane checkout component, allowing checkout pages to match their site design. If custom styles do not meet accessibility standards, the system automatically reverts to the default settings.

![Fixed issue](../assets/fix.svg)<!-- PAY-xxxx --> Fixed loader issue during **admin checkout with 3DS challenge**.

![Fixed issue](../assets/fix.svg)<!-- PAY-xxxx --> Improved **validation when storing payment configuration** via API.

## v2.12.2

_September 23, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fixed issue](../assets/fix.svg)<!-- PAY-6275 --> Declined [!DNL Fastlane] transactions in capture mode no longer create orders in Commerce.

## v2.12.1

_September 18, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fixed issue](../assets/fix.svg)<!-- PAY-6164 --> Now, [!DNL Payment Services] uses base currency for the available shipping methods in the **PayPal server-side shipping callback (SSSC)**.

![Fixed issue](../assets/fix.svg)<!-- PAY-6267 --> The **Ship To** block is hidden on the checkout page when **In-Store Pickup (ISPU)** is selected.

![Fixed issue](../assets/fix.svg)<!-- PAY-6271 --> Now, [!DNL Payment Services] displays saved credit card details from the PayPal PayFlow in the **Customer Account** > **Stored Payment Methods** section.

## v2.12.0

_August 20, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-6022 --> [Fastlane](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options) offers a faster purchase during guest checkouts.

![New](../assets/new.svg)<!-- PAY-6168 --> Added the [`addProductsToNewCart`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/) mutation to [!DNL Payment Services] to enable smoother transitions and better cart reuse.

![New](../assets/new.svg)<!-- PAY-6169 --> Added the [`setCartAsInactive`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/) mutation to [!DNL Payment Services] to improve quote lifecycle management.

![New](../assets/new.svg)<!-- PAY-6227 --> When checking out with PayPal, [!DNL Payment Services] skips the order confirmation pop-up for a quicker purchase process.

![New](../assets/new.svg)<!-- PAY-6234 --> Added a new feature for the [Pay Later](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options) payment option. Now, the BNPL messaging configurator provides more flexibility in displaying Pay Later BNPL messaging on customer checkout pages.

![Fixed issue](../assets/fix.svg)<!-- PAY-5505 --> Now, [!DNL Payment Services] sets the quote as inactive when a Google Pay or PayPal pop-up is closed within the product page.

![Fixed issue](../assets/fix.svg)<!-- PAY-5754 --> [!DNL Payment Services] no longer allows orders to be created from empty quotes.

## v2.11.1

_March 14, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fixed issue](../assets/fix.svg)<!-- PAY-5849 --> Fixed an issue that affected [Line Items](line-items.md) during checkout. Now, [!DNL Payment Services] has improved the checkout process reliability for **Line Items**. If you encounter a similar issue, contact your [!DNL Payment Services] sales representative for assistance.

## v2.11.0

_March 13, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer


![New](../assets/new.svg)<!-- PAY-5938 --> Now, [!DNL Payment Services] allows merchants to manage payment settings to maximize flexibility in their business. This version improves the ability to attach [multiple PayPal accounts](configure-admin.md#use-multiple-paypal-accounts) for the regions and brands a merchant supports. Our sales team can provide an onboarding link to set up your website and store view scopes.

![New](../assets/new.svg)<!-- PAY-5968 --> Now, [!DNL Payment Services] updates the Admin configuration with **PayPal Merchant ID** and **PayPal Merchant Status** values. These values provide merchants with better visibility into their PayPal account status.

![Fixed issue](../assets/fix.svg)<!-- PAY-5816 --> Restored normal order functionality in [!DNL Payment Services] by resolving an issue that was causing errors in all order placements with version v2.9.0.

![Fixed issue](../assets/fix.svg)<!-- PAY-5825 --> Fixed an issue where Apple Pay mini-cart used incorrect estimated totals URL for logged-in customers. Now, [!DNL Payment Services] ensures accurate total calculations.

![Fixed issue](../assets/fix.svg)<!-- PAY-5826 --> Improved order management reliability by resolving an issue that caused an HTTP 500 error when changing the quote status to `inactive`.

![Fixed issue](../assets/fix.svg)<!-- PAY-5849 --> Fixed an issue where `LineItemProvider` threw exceptions for decimal quantities below 1. Now, [!DNL Payment Services] provides better support for fractional quantities.

![Fixed issue](../assets/fix.svg)<!-- PAY-5868 --> Fixed a gift card amount error during checkout. [!DNL Payment Services] now ensures accurate values during the checkout process.

![Fixed issue](../assets/fix.svg)<!-- PAY-5911 --> Resolved errors during shipment creation for orders placed using non-[!DNL Payment Services] online payment methods, enhancing overall reliability.

![Fixed issue](../assets/fix.svg)<!-- PAY-5954 --> [!DNL Payment Services] now offers a smoother checkout experience by resolving an issue where Apple Pay failed to place an order when a different credit card was selected in the wallet.

![Fixed issue](../assets/fix.svg)<!-- PAY-5971 --> [!DNL Payment Services] no longer redirects customers to the order review page when Apple Pay fails, preventing unnecessary checkout disruptions.

## v2.10.3

_February 24, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fixed issue](../assets/fix.svg)<!-- PAY-xxxx --> Improved overall stability and performance.

![Fixed issue](../assets/fix.svg)<!-- PAY-xxxx --> General improvements and optimizations. Fixed critical bugs from v2.10.2.

## v2.10.2

_February 21, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Known issue](../assets/bug.svg)<!-- PAY-xxxx --> Contains critical bugs that can affect stability and performance. Adobe recommends upgrading to v2.10.3 instead of using  this version (v2.10.2).

## v2.10.1

_February 5, 2025_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-5813 --> Added support for Adobe Commerce 2.4.8 and PHP 8.4.

## v2.10.0

_December 13, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services] now supports GraphQL endpoints for vaulting without purchase, allowing customers to save their payment methods without completing a transaction.

![New](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services] now supports [3D Secure authentication with Google Pay](security.md#3ds), enhancing security for merchants and customers during payment transactions.

![Fix](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services] adds the ability for [customers to save cards directly in their **My Account**](vaulting.md#vaulting-without-purchase), improving convenience and simplifying future checkouts. `Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/).

![Fix](../assets/fix.svg)<!-- PAY-5762 --> Fixed an issue where coupon codes were not applied on the order review page when the order was initiated from the product detail page (PDP).

![Fix](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services] now displays descriptions and billing addresses for [vaulted cards on the checkout page](vaulting.md), giving customers more visibility into their saved payment methods.

![Fix](../assets/fix.svg)<!-- PAY-5793 --> [!DNL Payment Services] enables merchants to store the billing address for vaulted cards directly from the checkout page, ensuring accurate and complete payment information.

## v2.9.0

_November 7, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services] now supports an **upgraded SDK URL for Apple Pay**, improving the integration for merchants using Apple Pay. This feature is compatible with macOS 14 and later, devices running earlier versions of macOS will not display this functionality.

![New](../assets/new.svg)<!-- PAY-5630 --> Updated the **Checkout**, **Product**, **Cart**, and **MiniCart** pages to support the **upgraded SDK URL for Apple Pay**, enhancing the user experience for merchants who offer Apple Pay as a payment option.

![New](../assets/new.svg)<!-- PAY-5635 --> Improved shipping estimates **based on Apple Pay address**, allowing customers to view accurate shipping costs during checkout.

![Fix](../assets/fix.svg)<!-- PAY-5661 --> Fixed various **[!DNL Payment Services] issues at checkout**, improving the reliability of the payment process for merchants and shoppers.

![Fix](../assets/fix.svg)<!-- PAY-5692 --> Fixed an issue where the **customer's first and last names** were not added to the order when using **smart buttons for express checkout**.

![Fix](../assets/fix.svg)<!-- PAY-5712 --> Resolved an issue where merchants were **unable to complete checkout using the Zero Subtotal Checkout payment option** when the total amount was free.

## v2.8.1

_September 13, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg)<!-- PAY-5644 --> Fixed an issue with the cache of SDK parameters when using multiple scopes in [!DNL Payment Services]. SDK configuration is now cached separately for each scope instead of under a single key. This ensures that each scope's cache is invalidated independently, improving reliability when managing multiple scopes.

## v2.8.0

_September 13, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-5499 --> [!DNL Payment Services] now supports sending tracking number information to PayPal when a [tracking number is entered](track-shipment.md) in Adobe Commerce.

![Fix](../assets/fix.svg)<!-- PAY-5626 --> [!DNL Payment Services] has optimised the request process to the merchant registry when customers visit the Commerce checkout page. Previously, separate requests were made for each Payment Method (Hosted Fields, Google Pay, Apple Pay, and Smart Buttons). This improvement reduces the number of calls, enhancing performance and efficiency during the checkout process.

![Fix](../assets/fix.svg)<!-- PAY-5645 --> [!DNL Payment Services] now prevents the PayPal/Google Pay popup from opening if the shopper has not agreed to merchant created custom terms and conditions on the checkout page.

![Fix](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services] has addressed an issue related to the line item breakdown of tax on the PayPal portal. If the shipping cost of an order has tax associated with it, the tax will be included as part of the shipping cost, and will be visible this way in the line item details shown in the PayPal portal.

## v2.7.0

_August 2, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services] now supports [line item data at the order level](line-items.md). This feature allows merchants to see detailed information about the items in an order, such as product details, quantity, and price (including sales tax, discounts, and other relevant information).

![New](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services] improves the [Configuration in the Admin](configure-admin.md#general-configuration) experience for merchants for an easier and more intuitive onboarding process. This feature allows merchants to reset their [!DNL Payment Services] IDs.

![New](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services] includes a [Payment failure notification](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails). This feature provides near real-time notifications of payment failures to merchants, so orders can be saved by reaching out to the shopper and potentially improve issue resolution.

![Fix](../assets/fix.svg)<!-- PAY-5469 --> Fixed an issue where the **Google Pay popup was blocked by Safari**. Shoppers can now complete their Google Pay payment transactions on Safari.

![Fix](../assets/fix.svg)<!-- PAY-5492 --> Fixed an issue when a merchant adds customized terms and conditions to the checkout page. During an [express checkout](payments-options.md#standard-vs-advanced-payments-experience) a shopper now has the ability to accept these terms and conditions to complete the checkout without any issues.

![Fix](../assets/fix.svg)<!-- PAY-5532 --> Improved In-Store Pickup (ISPU) functionalities with **InstantPurchase**. **ISPU Delivery Methods** are no longer displayed when a shopper places an order with **InstantPurchase**.

![Fix](../assets/fix.svg)<!-- PAY-5606 --> Fixed an issue within the **Configuration Page** country selector that occurred when the merchant's country is set to **Germany**.

## v2.6.0

_June 4, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-4877 --> Now, [!DNL Payment Services] supports [L2/L3 pricing capabilities](/help/payment-services/levels-card-payment-transactions.md#level-2-and-level-3). This feature is only available for [!DNL Payment Services] customers with IC++ pricing enabled. If you want to use L2/L3 processing data for [!DNL Payment Services], contact your [!DNL Payment Services] account manager.

![Fix](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services] allows you to enable Apple Pay directly from the extension without downloading and hosting the [domain association file](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).

## v2.5.0

_April 23, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services] now supports [Adobe Commerce guidelines for the `--db-prefix` parameter](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line) for Adobe Commerce versions 2.4.7 and newer.

## v2.4.3

_April 16, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg)<!-- Issue PAY-5106 --> Fixed an issue that incorrectly populated the order amount totals during checkout between PayPal and Adobe Commerce. Now, Merchants can ensure that order amount totals are correct when placing an order.

## v2.4.2

_April 11, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- Issue xxx --> Added support for Adobe Commerce 2.4.7.

## v2.4.1

_April 4, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg)<!-- PAY-5322 --> Fixed a PCI compatibility issue with newer Adobe Commerce releases. Now, [!DNL Payment Services] is adapted to checkout requirements in Adobe Commerce as the payment option.

![Fix](../assets/fix.svg)<!-- PAY-5323 --> PayLater and Venmo are correctly displayed in Adobe Commerce. Fixed an error that disallowed the Admin to show PayLater and Venmo toggle options.

## v2.4.0

_March 20, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-4868 --> Merchants can successfully [configure Google Pay throughout the purchase experience](/help/payment-services/payments-options.md), similar to other payment buttons in [!DNL Payment Services] through the Admin.

![New](../assets/new.svg)<!-- PAY-4381 --> [Payment Services supports Google Pay through GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/) allowing merchants to have a headless Commerce experience with the Google Pay payment method.

![New](../assets/new.svg)<!-- PAY-4878 --> Now, the [!DNL Payment Services] basic checkout feature is bundled for Adobe Commerce and Magento Open Source merchants.[!DNL Payment Services] can now support merchants with businesses in any of 200 geographies worldwide.[!DNL Payment Services] basic checkout provides debit/credit, PayPal, Venmo (where available), and PayLater (where available) options in a self-service onboarding.

![Fix](../assets/fix.svg)<!-- PAY-5291 --> Receiving payment confirmation for some transactions may be delayed. In that case, now merchants can get an updated payment status for an order. [Payment services detects the pending status of a payment transaction](/help/payment-services/order-payment-status.md#payment-status-updates) in an order by detecting pending transactions and proactively monitoring these transactions and updating when the pending status has been captured.

## v2.3.4

_March 1, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-5244 --> Fixed async checkout compatibility.

![Fix](../assets/fix.svg)<!-- PAY-5253 --> Fixed an error where a vault token not belonging to [!DNL Payment Services] could not be deleted.

## v2.3.3

_February 14, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-5048 --> Added support for PHP 8.3

![Fix](../assets/fix.svg)<!-- PAY-5048 --> Fixed an error with the `is_deleted` flag. Now, orders do not fail due to the `Rejected` status sent from the extension.

## v2.3.2

_January 26, 2024_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg)<!-- PAY-5183 --> Fixed REST/GraphQL performance issues. Now, the credit card button renders when fetched through the API.

## v2.3.1

_December 7, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-5047 --> The credit/debit card brand or payment method type is now available from the following locations:

- the customer order page on the storefront
- the order confirmation email sent to the shopper
- from the [order details view](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order) in the Commerce Admin.

## v2.3.0

_December 1, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-4381 --> [Payment Services now supports GraphQL integration](https://developer.adobe.com/commerce/webapi/graphql/payment-services/). With GraphQL support for PayPal payment buttons, hosted fields, and Apple Pay,[!DNL Payment Services] now supports a headless Commerce setup.

## v2.2.1

_September 27, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-4870 --> Fixed an issue that incorrectly populated the new header attribute correctly in Storefront when sending the extension version with the latest release. Previously, with the `1.3.0` release of the Commerce Services connector, you could not extend the `User-Agent header` from the [!DNL Payment Services] extension.

## v2.2.0

_August 30, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- PAY-4638 --> Added an [integration with Signifyd](fraud-protection.md), which provides automated fraud protection services.

![New](../assets/new.svg)<!-- PAY-3981 --> [Promoted Apple Pay to a separate payment option](payments-options.md#apple-pay-button), outside of the PayPal payment buttons, to increase shopper visibility of the payment option and to allow merchants to control the placement and styling of Apple Pay.

![New](../assets/new.svg)<!-- PAY-4002 --> Improved the user experience of credit card fields checkout, including styling enhancements such as adding payment icons, to lower shopper cognitive load and increase conversions.

![New](../assets/new.svg)<!-- PAY-4002 --> Added functionality to allow merchants to [sort the order of their payment options](configure-admin.md#paypal-payment-buttons) to prioritize certain payment options. This functionality encourages a higher checkout conversation rate.

![New](../assets/new.svg)<!-- PAY-4035 --> Merchants can now efficiently monitor the health of their stores and identify any transaction issues using the new [Transactions report](reporting.md#transactions-report-view) available from the[!DNL Payment Services] Admin home page. The report presents data about transaction authorization rates and negative transaction trends as well.

## v2.1.0

_June 9, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- Issue xxx --> Added support for Adobe Commerce 2.4.7-beta1.

![New](../assets/new.svg)<!-- Issue xxx --> Added [availability in the following countries and associated currencies](introduction.md#availability): Australia, France, United Kingdom.

![New](../assets/new.svg)<!-- Issue PAY-4296 --> Added [expanded resources for Admin roles](configure-admin.md#configure-roles) to ensure Admin users can create and manage orders for customers and can see[!DNL Payment Services] in the Sales menu.

![New](../assets/new.svg)<!-- Issue PAY-4236 --> Added [auto-voiding for orders that incur errors during checkout](checkout.md#order-auto-voided-if-error).

![New](../assets/new.svg)<!-- Issue PAY-4183 --> Created functionality to [show the credit/debit card payment option button](payments-options.md#paypal-debit-or-credit-card-button) on the checkout page.

## v2.0.0

_March 10, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![New](../assets/new.svg)<!-- Issue PAY-4152 --> Added support for PHP 8.2 and Adobe Commerce 2.4.6. Not compatible with PHP 7.x.

## v1.6.1

_March 10, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.4 and newer

![Fix](../assets/fix.svg)<!-- Issue PAY-4226 --> Fixed an issue that prevented new [!DNL Payment Services] merchants from using checkout in the Admin.[!DNL Payment Services] was previously using the Commerce customer ID, which does not exist for new customers.

![Fix](../assets/fix.svg)<!-- Issue PAY-4205 --> Fixed an issue that caused the specified shipping address state to be replaced by the state in the default tax settings during checkout using the [PayPal option](payments-options.md#paypal-payment-buttons). Now, customers can have their orders shipped to a state other than the one configured as the default in the merchant's tax settings.

![Fix](../assets/fix.svg)<!-- Issue PAY-4202 --> Fixed an issue preventing customers from using card vaulting to complete a purchase or delete a vaulted payment method for a store [using the `Authorize and Capture` payment action](production.md#set-payment-services-as-payment-method). Previously, a "Provider Vault ID not found" error appeared when the customer attempted to use or modify their vaulted credit cards.

## v1.6.0

_February 17, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![New](../assets/new.svg)<!-- Issue PAY-3540 --> Added [PCI 3DS compliance feature for merchants transacting in the European Union (EU) and Britain](security.md#3ds). This additional layer of security, which requires buyers to authenticate with their credit card issuer, helps prevent online fraud and is required as part of European Union (EU) compliance regulations.

![New](../assets/new.svg)<!-- Issue PAY-3609 --> Added the ability to [enable card vaulting in the Admin](vaulting.md#use-vaulting-in-the-admin). This allows merchants to create an order for customers in the Admin using their vaulted payment methods.

## v1.5.4

_January 29, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-4110 --> Fixed an issue that prevented buyers from placing an order using payment buttons on the product page, mini cart, and cart. Buyers can now complete orders successfully.

## v1.5.3

_January 25, 2023_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-4102 --> Released a fix to a backward incompatible known issue. This release locks the service ID extension version to the latest stable version, which reenables new [!DNL Payment Services] installations to configure Commerce Services.

## v1.5.2

_December 22, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3992 --> Improved invoicing in [!DNL Payment Services] when a payment method is declined.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services] now correctly displays PayPal payment buttons for merchants using [Fire Checkout's](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} custom template for the checkout page. Previously, the minicart intermittently displayed the buttons.

## v1.5.1

_November 23, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![New](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services] now includes the version number in the user agent header so that requests can track, filter, or deprecate unused endpoints.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services] now correctly displays order data when an order is placed from the product page using payment buttons.

## v1.5.0

_November 18, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![New](../assets/new.svg)<!-- Issue PAY-3880 --> A shopper can now [vault (save) their credit card information during checkout](vaulting.md) to use in a later purchase for the same or another store within the same merchant account.

![New](../assets/new.svg)<!-- Issue PAY-3950 --> Merchants can now enable the [Instant Purchase Commerce feature](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) for their stores so that shoppers can (use [vaulted credit card information](vaulting.md)) to expedite checkout.

## v1.4.1

_October 14, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![Fix](../assets/fix.svg)<!-- Issue PAY-3766 --> When a customer's payment method is declined, the visible error message is more descriptive. It advises the customer to reenter payment information and try again, try another payment method, or to contact their bank about the declined the transaction.

## v1.4.0

_September 30, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![New](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services] now includes the ability to set up a merchant account to [use multiple PayPal business accounts](configure-admin.md#use-multiple-paypal-accounts). This enables the merchant to operate your stores in multiple countries using different currencies, or to use Adobe Commerce for a portion of your business.

![New](../assets/new.svg)<!-- Issue PAY-3231 --> Merchants can [add a [!UICONTROL Soft Descriptor]](configure-admin.md) to websites or individual store views configuration that show on customer transaction bank statements to delineate brands, stores, or product lines.

![New](../assets/new.svg)<!-- Issue PAY-3707 --> [Enable or disable credit card fields and PayPal payment buttons](configure-admin.md#paypal-payment-buttons) for checkout in[!DNL Payment Services] settings.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3546 --> When a customer clicks **[!UICONTROL Edit cart]**, the page redirects to the cart page and shows the updated items instead of showing an empty cart.

## v1.3.1

_September 6, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3663 --> Now, when a merchant's store is capturing an order authorized with a non-global currency, the capture process completes and no error is shown.

## v1.3.0

_August 9, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![New](../assets/new.svg)<!-- Issue PAY-XX --> General availability release---[!DNL Payment Services] is now [supported by [!DNL Adobe Commerce] and [!DNL Magento Open Source] versions 2.4.0 to 2.4.5](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-x --> Apple Pay is now compatible with the Safari browser v15.5 on mobile and desktop.

## v1.2.0

_June 29, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![Known issue](../assets/bug.svg)<!-- Issue PAY-x --> Apple Pay is incompatible with the Safari browser v15.5 on mobile and desktop. When using Safari version 15.5, you are not able to complete checkout with Apple Pay.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3264 --> Previously, when a logged-in user selected a billing/shipping address other than the default address for their account, checkout failed. Now, the selected billing/shipping address is sent (instead of the default saved address) and checkout is completed successfully.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3314 --> If you disable PayPal payment buttons for checkout, no errors are shown.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3330 --> Payments no longer fail during checkout when a guest user enters a phone number that includes dashes.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 --> When Commerce Services credentials are invalid,[!DNL Payment Services] now alerts you by displaying a credentials error from the [!DNL Payment Services] Home in the Admin.

![Known issue](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services] is incompatible with `commerce-data-export` v101.20 and higher, which renders it incompatible with the [[!DNL Channel manager] extension](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html).

## v1.1.0

_March 31, 2022_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![New](../assets/new.svg)<!-- Issue PAY-2127 --> General availability release---[!DNL Payment Services] is now [supported by [!DNL Adobe Commerce] and [!DNL Magento Open Source] versions 2.4.0 to 2.4.4](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

![New](../assets/new.svg)<!-- Issue PAY-2682 --> The [!DNL Payment Services] extension for [!DNL Adobe Commerce] and [!DNL Magento Open Source] is now available for Canadian merchants. Merchants can view payments configuration in either [French](introduction.md?lang=fr#accepted-credit-cards-and-currencies) or [English](introduction.md#accepted-credit-cards-and-currencies).

![New](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services] supports [Canadian dollars (CAD)](introduction.md#accepted-credit-cards-and-currencies) for credit cards and PayPal transactions.

![New](../assets/new.svg)<!-- Issue PAY-2680 --> Merchants can [onboard [!DNL Payment Services]](onboard.md) extension in English or French languages.

![New](../assets/new.svg)<!-- Issue PAY-2678 --> Merchants can now view financial reports, both the [Order payment status](order-payment-status.md) and [Payouts reports](payouts.md), in Canadian dollars (CAD).

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services] is now compatible with [PHP 8.1](https://www.php.net/releases/8.1/en.php).

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-3017 --> Improved Sandbox mode alert to display proper alerts with multiple stores.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-2742 --> You can now enable and disable available payment methods, such as Venmo, at the store view level. Previously, you could configure payment methods per website only.

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-2277 --> You can now selectively [enable or disable individual PayPal payment buttons](configure-admin.md#payment-buttons).

![Fixed issue](../assets/fix.svg)<!-- Issue PAY-2561 --> Previously removed products do not appear in the cart on the _Review Order_ page.

![Known issue](../assets/bug.svg)<!-- Issue PAY-2842 --> Test credit card transactions [may fail with PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html) when processing payments in a sandbox environment.

## v1.0.0

_November 29, 2021_

[!BADGE Supported]{type=Informative tooltip="Supported"} Adobe Commerce versions 2.4.0 and newer

![New](../assets/new.svg)<!-- Issue PAY-2127 --> General availability release---[[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html) is now supported by [!DNL Adobe Commerce] and [!DNL Magento Open Source] versions 2.4.0 to 2.4.3-p1.

![New](../assets/new.svg)<!-- Issue PAY-124 --> The [!DNL Payment Services] extension for [!DNL Adobe Commerce] and [!DNL Magento Open Source] can be installed either for [[!DNL Adobe Commerce] on cloud infrastructure](install.md#adobe-commerce-on-cloud-infrastructure) or [On-premises](install.md#on-premises) instances. These methods require the use of a Command Line Interface.

![New](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services] supports a [sandbox account](sandbox.md) that allows merchants to assess the extension in test mode.

![New](../assets/new.svg)<!-- Issue PAY-666 --> Merchants can [configure the Payment Services](configure-admin.md) extension with basic payment behaviors, such as utilizing [`Authorize and Capture`](production.md#set-payment-services-as-payment-method) switching between sandbox or production environments.

![New](../assets/new.svg)<!-- Issue PAY-780 --> Your shoppers can check out with [!DNL Payment Services] or via [manual order creation](create-order.md).

![New](../assets/new.svg)<!-- Issue PAY-1856 --> Comprehensive reporting, via [Order payment status](order-payment-status.md) and [Payouts reports](payouts.md), are available for [!DNL Payment Services] to give you a clear view of your store's orders and related payments.

![New](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services] supports flexible tiered pricing, based on total processing volume, adapted to any merchant.

![New](../assets/new.svg)<!-- Issue PAY-1443 --> You can easily [customize the look and feel](payments-options.md) of PayPal payment buttons and credit card fields for the [!DNL Payment Services] extension.

![Known issue](../assets/bug.svg)<!-- Issue PAY-2473 --> Using [incorrect Composer keys](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html) during installation of the extension prevents the user from [authenticating](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) with the correct `MAGEID`.

![Known issue](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services] reports [may not synchronize immediately](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html).

![Known issue](../assets/bug.svg)<!-- Issue PAY-2475 --> Your [PayPal sandbox account](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html) for [!DNL Payment Services] cannot be verified  if you create that account during onboarding.
