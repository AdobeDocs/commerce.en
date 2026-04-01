---
title: Commerce Optimizer Launch Checklist
description: "Learn how to validate configuration, storefront, SEO, CDN, integrations, security, analytics, and testing for [!DNL Adobe Commerce Optimizer] production."
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
---

# Launch checklist

Use this checklist to verify that your production [!DNL Adobe Commerce Optimizer] project is configured, tested, and ready for launch. Work through each section with your team and track completion in your own project plan or tracker. For product capabilities and UI areas referenced below, see the [[!DNL Adobe Commerce Optimizer] documentation](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview){target="_blank"}.

## 1. Core configuration

- **Config:** All configuration files are set and point to production services (not staging or dev).
- **Config:** GraphQL endpoints are configured with [!DNL Adobe Commerce Optimizer] production endpoints.
- **Catalog:** Production catalog is synced to the new environment.
- **Config:** A new Commerce API key pair is generated; the public key is set as `x-api-key`.
- **Config:** `environmentId` and `x-api-key` values are updated in `config.json`.
- **Catalog:** You have switched to the Catalog Service production endpoint (`https://catalog-service.adobe.io/graphql`).
- **Config:** Production is configured in Service Connector (a new `environmentId` is generated).
- **Config:** All testing and dummy data are removed from the production instance.

For tenant IDs, GraphQL endpoints, and instance management, see [Get started](../get-started.md).

## 2. Adobe Commerce Optimizer

- **Connector:** [!DNL Adobe Commerce Optimizer] Connector is installed and configured in your Adobe Commerce project. Install the metapackage with Composer, configure data export, obtain API credentials, enable the integration, and verify data sync. See [Get started with the Adobe Commerce Optimizer Connector](../../aco-connector/get-started.md) for details.
- **Connector:** If you use a non-Adobe Commerce backend, install and configure the appropriate catalog connector (for example, the [Salesforce Commerce Connector](../developer/salesforce-connector.md) via App Builder).
- **Connector:** Uninstall conflicting extensions before you enable the [!DNL Adobe Commerce Optimizer] Connector (Live Search, Product Recommendations, and Catalog Service standalone packages).
- **Data sync:** Data sync is verified on the [Data sync](../setup/data-sync.md) page — expected products, prices, and attributes appear for Catalog Service, Product Discovery, and Recommendations.
- **Data sync:** All catalog data is synchronized — products, category attributes, and [price books](../setup/pricebooks.md).
- **Catalog:** [Catalog views](../setup/catalog-view.md) and [policies](../setup/policies.md) are created in [!DNL Adobe Commerce Optimizer] Admin (price books are auto-created from Commerce customer groups).
- **Catalog:** Channels and [policies](../setup/policies.md) are configured for the production site.
- **Catalog:** Category IDs are verified — all category pages reference the correct categories.
- **Merchandising:** [Facets](../merchandising/facets/overview.md), [synonyms](../merchandising/synonyms/overview.md), and [merchandising rules](../merchandising/rules/overview.md) are set up and customized (see [Merchandising](../merchandising/overview.md)). Configure [price faceting and search language](../settings.md) under Settings as needed.
- **Merchandising:** [Product recommendations](../merchandising/recommendations/create.md) are created and validated.
- **Merchandising:** Search and recommendations data is visible in Admin — review [Search performance](../manage-results/search-performance.md) and [Recommendations performance](../manage-results/recommendation-performance.md).
- **Communication:** The Catalog Service team is notified about the new production environment and launch date.

## 3. Storefront, content, and authoring

- **EDS:** The [AEM/EDS Go-Live Checklist](https://aem.live/docs/go-live-checklist) is reviewed. Align with [Set up your storefront](../storefront.md) in the [!DNL Adobe Commerce Optimizer] guide.
- **Content:** Content authoring source is selected and configured (document-based or Universal Editor).
- **Content:** All content is published through the preview → publish cycle.
- **Content:** Content and design QA is completed on the `.aem.live` domain.
- **Performance:** Pre-rendering is enabled for key pages, for example product detail (PDP) and product listing (PLP) pages.
- **Performance:** All URLs are verified as lowercase to support pre-rendering.
- **Performance:** HTML source is validated for metadata and enriched body content.
- **Content:** Page translations are verified for all locales and languages.
- **Content:** A favicon is added to the site.
- **Security:** Authentication is configured for authors (DA.live permissions and EDS sites).
- **Content:** SharePoint / Google Drive access is configured with dedicated credentials.
- **Content:** [Product visuals](../setup/product-visuals.md) (AEM Assets) integration is provisioned.
- **Content:** Password reset links are updated to match the EDS implementation in Admin.
- **Dropins:** Drop-ins (Cart, Checkout, PDP, PLP, Auth, Account) are customized and tested. See [Set up your storefront](../storefront.md) (and storefront resources linked from that topic).
- **Content:** Storefront branding is applied — CSS design tokens, typography, and colors.

## 4. SEO and indexing

- **Indexing:** `robots.txt` is in place with a sitemap reference and rules that block unwanted content (for example, `/drafts`).
- **Indexing:** A sitemap is generated for site and catalog pages.
- **Indexing:** The sitemap is submitted to Google Search Console.
- **Metadata:** Metadata and structured data (LD-JSON) are added to all PDPs.
- **Metadata:** Document title metadata is added for key pages (PDPs, PLPs).
- **URLs:** URL formats are standardized for products (for example, `domain/product-name`).
- **URLs:** Redirects are configured for all legacy and vanity URLs to preserve SEO value.
- **URLs:** Canonical URLs return 2xx status (not 3xx or 4xx).
- **Indexing:** `hreflang` tags are added to the sitemap for multilingual sites.
- **Indexing:** The Google Search Console coverage report is reviewed.
- **URLs:** Vanity URLs redirect to canonical URLs.

## 5. CDN, caching, and DNS

- **CDN:** CDN is configured with the production GraphQL endpoint (`yourproject.com/graphql`).
- **CDN:** CDN configuration is tested in staging before production cutover.
- **CDN:** Push invalidation is set up and tested (publish a change, then verify on the production domain).
- **CDN:** A CDN purge token is requested for Commerce production (`authToken` and `serviceId` are updated in `.helix/config.xlsx`).
- **Caching:** Cache invalidation is validated — content updates propagate correctly.
- **Caching:** A store-specific cache buster is added for multi-store setups.
- **DNS:** DNS TTL is reduced to the minimum before cutover.
- **DNS:** DNS A/CNAME records are updated for all domains and hostnames.
- **DNS:** SSL/TLS certificate is provisioned and verified for the production domain.
- **DNS:** `www` ↔ apex redirects work correctly.
- **CDN:** Sidekick extensions and scripts use the production GraphQL endpoint.

## 6. Integrations — third-party services

- **Payments:** Payment gateway integration is live and tested (Stripe, PayPal, Adyen, and so on).
- **Shipping:** Shipping API connections are confirmed (UPS, FedEx, and so on).
- **Shipping:** Fulfillment platform is connected and tested (for example, ShipStation).
- **Tax:** Tax calculation integration is validated (Avalara, TaxJar, and so on).
- **Tax:** Accounting software sync is confirmed (QuickBooks, and so on).
- **Inventory:** PIM / ERP / inventory management integration is tested and syncing.
- **Architecture:** The host commerce system handles payment, shipping, tax, and inventory (not [!DNL Adobe Commerce Optimizer]).
- **Architecture:** API Mesh and App Builder are in sync between the host commerce system and [!DNL Adobe Commerce Optimizer].
- **Payments:** Production keys are configured for all integration and payment providers.
- **Architecture:** New domains and subdomains are allowlisted; backend webhooks are confirmed working.
- **Email:** Transactional email delivery is tested (order confirmation, shipping, and so on).
- **Email:** Email templates are updated to reflect brand and correct links.

## 7. Integrations — App Builder and extensibility

- **App Builder:** All configurations and services are applied to the production workspace.
- **App Builder:** The App Builder production app is tested across all build scenarios.
- **API Mesh:** API Mesh configs and sources are ready for the production environment.
- **App Builder:** App Builder product limitations are reviewed — see the [Adobe Developer App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} and [App Builder system settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
- **App Builder:** The production application is configured with App Builder production endpoints.
- **Events:** Adobe I/O Events are configured and event subscriptions are verified.
- **App Builder:** Custom admin panel extensions are deployed to the production workspace.

## 8. Security and compliance

- **SSL:** SSL/TLS security certificate is installed (100% signed and trusted).
- **SSL:** HTTPS is enforced across the entire site.
- **Access:** Admin password is changed from defaults; a strong password policy is enforced. Manage [!DNL Adobe Commerce Optimizer] users and roles using [User and identity management](../user-management.md).
- **Access:** Admin URL is changed from the default.
- **Access:** Two-factor authentication is enabled for all admin users.
- **Access:** Unused admin users are removed from the project.
- **Firewall:** Web Application Firewall (WAF) is configured and verified.
- **PCI:** Security penetration testing is completed on production (PCI compliance).
- **Scanning:** Adobe Security Scan Tool is registered and an initial scan is completed.
- **Access:** CORS configuration is reviewed and restricted to allowed origins.
- **Compliance:** The [shared responsibility model](../shared-responsibility.md) for [!DNL Adobe Commerce Optimizer] is reviewed (Adobe vs. customer responsibilities).
- **Compliance:** Privacy policy, cookie consent, and GDPR/CCPA compliance are verified.

## 9. Analytics and monitoring

- **Config:** Analytics config `environment` parameter is set to `Production`.
- **Analytics:** Google Analytics / Google Tag Manager is configured (optional).
- **Events:** Storefront events implementation is validated (Snowplow debugger).
- **RUM:** Real Use Monitoring (RUM) is instrumented for before/after launch comparison.
- **Analytics:** Adobe Experience Platform data collection is configured (if applicable).
- **Analytics:** Martech stack tags fire correctly on the production hostname.
- **Analytics:** Analytics baselines are documented — expect metric shifts post-launch (pageviews, bounce rate, and so on).
- **Events:** Conversion tracking is verified end-to-end (add-to-cart → checkout → confirmation).

## 10. Testing

- **Functional:** All user flows are tested: browse → search → filter → add to cart → checkout → account creation.
- **Functional:** Payment gateways are tested with real and test transactions.
- **Functional:** Order placement, confirmation emails, and order tracking are verified.
- **Functional:** Shipping options and tax calculations are accurate.
- **Functional:** Coupon codes, discounts, and loyalty programs work.
- **UAT:** User Acceptance Testing (UAT) is completed on staging and production.
- **Performance:** Load and stress testing is completed; results are shared with Adobe CTA/CSE.
- **Performance:** Page load speed is validated — under 3 seconds on desktop and mobile.
- **Performance:** Lighthouse score is green (target 100) on all key pages via PageSpeed Insights.
- **Performance:** Images, scripts, and assets are optimized for performance.
- **Compatibility:** Cross-browser testing is completed (Chrome, Firefox, Safari, Edge).
- **Compatibility:** Responsive design is verified on all device sizes (mobile, tablet, desktop).
- **Compatibility:** Performance is tested under different network conditions (3G, 4G, Wi-Fi).
- **Accessibility:** An accessibility audit is completed (WCAG compliance, screen reader, keyboard navigation).
- **Functional:** A 404 error monitoring plan is in place for post-launch.
- **UAT:** A rollback plan is documented and tested in case of launch issues.

## 11. Launch day and post-launch support

- **Communication:** Adobe is notified of the planned launch date (early notice for team availability).
- **Communication:** The Edge Delivery Services team is notified — email [aemgolives@adobe.com](mailto:aemgolives@adobe.com) with URLs, domain, date, contact, and Slack or Teams channel.
- **Support:** P1 hotline number is recorded: US (+1) 800 497 0335 — press 6 for Commerce.
- **Support:** Support ticket process is understood — file a ticket **first**, then call the P1 hotline.
- **Updates:** Latest boilerplate changes are applied to the project.
- **Validation:** Post-launch: verify Lighthouse score on the production domain.
- **Validation:** Post-launch: monitor Google Search Console for indexing and crawl errors.
- **Validation:** Post-launch: monitor the 404 report and add redirects for high-traffic legacy URLs.
- **Validation:** Post-launch: martech and analytics data are flowing correctly on production.
- **Validation:** Post-launch: notify CTA/CSE/AM to activate High SLA monitoring.
- **Support:** Disaster recovery plan is documented and tested.
