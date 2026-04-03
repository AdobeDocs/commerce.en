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

### Usecase

B2C, leverage the Optimizer and EDS capabilities for the existing Adobe Commerce on Cloud instance. 

### Components
- **Cloud** - Adobe Commerce on Cloud, to manage the Catalog data, Customers, and serve purchase experiences (checkout, order management, shipping, etc)
- **Optimizer** - Adobe Commerce Optimizer, to serve merchandising experiences
- **Storefront** - Adobe Commerce Storefront on Edge Delivery Services, to build UI
- **Third-Party services** to cover Payment, Shipping, Tax
- **App Builder** 
- **API Mesh**

---

## Production instances are created

~~- [ctag] [Core Configuration] **Config:** All configuration files are set and point to production services (not staging or dev)..~~
~~- [ctag] [Core Configuration] **Config:** GraphQL endpoints are configured with [!DNL Adobe Commerce Optimizer] production endpoints.~~

### Cloud
- All testing and dummy data are removed. 
- Production data is loaded to the instance.
- GraphQL endpoint is known

### Optimizer
- It is created in the correct region
- Instance type is Production
- Organization ID, Client ID, Ingestion URL, Optimizer studio URL are known, see [Get started](../get-started.md).
- Limits and boundaries adjusted accordingly 

### Storefront
- MVP steps to create the instance

---

## Cloud is connected to Optimizer

### on Cloud
~~- **Connector:** If you use a non-Adobe Commerce backend, install and configure the appropriate catalog connector (for example, the [Salesforce Commerce Connector](../developer/salesforce-connector.md) via App Builder).~~
~~- **Connector:** Uninstall conflicting extensions before you enable the [!DNL Adobe Commerce Optimizer] Connector (Live Search, Product Recommendations, and Catalog Service standalone packages).~~ should move to ^^
- ACO connector is installed and configured following [Get started with the Adobe Commerce Optimizer Connector](../../aco-connector/get-started.md) for details.
- CLI command aco:conf:show confirms connection with the production Optimizer instance. Organization ID, Client ID, Ingestion URL, Optimizer studio URL match the production instance.
- Scopes for synchronization are picked.
- Data sync is verified on the [Data sync](../setup/data-sync.md) page — expected products, prices, and attributes appear for Catalog Service, Product Discovery, and Recommendations.

### on Optimizer
- [ctag] [Core Configuration] All catalog data is received — products, category attributes, and [price books](../setup/pricebooks.md).
- Price books are auto-created from Commerce customer groups
- [Catalog views](../setup/catalog-view.md) are created. Their IDs are known.
- [Policies](../setup/policies.md) are created. Their IDs are known.
- [ctag] [Core Configuration] **Catalog:** Channels and [policies](../setup/policies.md) are configured for the production site.
- [ctag] [Core Configuration] **Merchandising:** [Facets](../merchandising/facets/overview.md), [synonyms](../merchandising/synonyms/overview.md), and [merchandising rules](../merchandising/rules/overview.md) are set up and customized (see [Merchandising](../merchandising/overview.md)). Configure [price faceting and search language](../settings.md) under Settings as needed.
- [ctag] [Core Configuration] **Merchandising:** [Product recommendations](../merchandising/recommendations/create.md) are created and validated.
- **Merchandising:** Search and recommendations data is visible in Admin — review [Search performance](../manage-results/search-performance.md) and [Recommendations performance](../manage-results/recommendation-performance.md).

---

## Storefront is connected to Cloud

### on Cloud
- Storefront compatibility packages are [installed](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/)

### on Storefront
- ensure Config.json public/default/commerce-core-endpoint mentions the GraphQL endpoint of the production Cloud instance

---

## Storefront is connected to Optimizer

### on Storefront
- ~~Switch to the Catalog Service production endpoint (`https://catalog-service.adobe.io/graphql`).~~ wrong URL
- ~~Ensure a production environment is configured in the Service Connector (will result in a new `environmentId`).~~ Moved to connector
- ~~Sync the production catalog to the new production environment.~~ Moved to connector
- ~~Create a new Commerce production API key-pair and use the public key as the `x-api-key` value.~~ unrelevant for ACO
- Verify category IDs and ensure all category pages reference the correct category.
- ~~Update `environmentId` and `x-api-key` values in the `config.json` code file.~~ unrelevant for ACO
- ~~Notify the Catalog Service team about the new production environment and launch date.~~ moved to "Launch day and post-launch support"
- **new** ensure Config.json public/default/adobe-commerce-optimizer set to "true"
- **new** ensure Config.json public/default/commerce-endpoint mentions the GraphQL endpoint of the production Optimizer instance
- **new** ensure Config.json public/default/cs/AC-view-ID mentions the correct Catalog View Id created in the production Optimizer instance

### on Optimizer
- no actions required

---

## Cloud is integrated with Third-Party services

- [ctag] [Integrations – Third Party Services] **Payments:** Payment gateway integration is live and tested (Stripe, PayPal, Adyen, and so on).
- [ctag] [Integrations – Third Party Services] **Shipping:** Shipping API connections are confirmed (UPS, FedEx, and so on).
- [ctag] [Integrations – Third Party Services] **Shipping:** Fulfillment platform is connected and tested (for example, ShipStation).
- [ctag] [Integrations – Third Party Services] **Tax:** Tax calculation integration is validated (Avalara, TaxJar, and so on).
- [ctag] [Integrations – Third Party Services] **Tax:** Accounting software sync is confirmed (QuickBooks, and so on).
- [ctag] [Integrations – Third Party Services] **Inventory:** PIM / ERP / inventory management integration is tested and syncing.
- [ctag] [Integrations – Third Party Services] **Architecture:** The host commerce system handles payment, shipping, tax, and inventory (not [!DNL Adobe Commerce Optimizer]).
- [ctag] [Integrations – Third Party Services] **Architecture:** API Mesh and App Builder are in sync between the host commerce system and [!DNL Adobe Commerce Optimizer].
- **Email:** Transactional email delivery is tested (order confirmation, shipping, and so on).
- **Email:** Email templates are updated to reflect brand and correct links.

---

## Cloud is integrated with App Builder and API Mesh

- [ctag] [Integrations – App Builder] **App Builder:** All configurations and services are applied to the production workspace.
- [ctag] [Integrations – App Builder] **App Builder:** The App Builder production app is tested across all build scenarios.
- [ctag] [Integrations – App Builder] **API Mesh:** API Mesh configs and sources are ready for the production environment.
- [ctag] [Integrations – App Builder] **App Builder:** App Builder product limitations are reviewed — see the [Adobe Developer App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} and [App Builder system settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
- [ctag] [Integrations – App Builder] **App Builder:** The production application is configured with App Builder production endpoints.
- **Events:** Adobe I/O Events are configured and event subscriptions are verified.
- **App Builder:** Custom admin panel extensions are deployed to the production workspace.

---

## Storefront is finetuned

### **new** Content and authoring

- [ctag] **new** The [AEM/EDS Go-Live Checklist](https://aem.live/docs/go-live-checklist) is reviewed. Align with [Set up your storefront](../storefront.md) in the [!DNL Adobe Commerce Optimizer] guide.
- [ctag] **new** Content authoring source is selected and configured (document-based or Universal Editor).
- [ctag] **new** All content is published through the preview → publish cycle.
- **new** Content and design QA is completed on the `.aem.live` domain.
- **new** A favicon is added to the site.
- **new** SharePoint / Google Drive access is configured with dedicated credentials.
- **new** Drop-ins (Cart, Checkout, PDP, PLP, Auth, Account) are customized and tested. See [Set up your storefront](../storefront.md) (and storefront resources linked from that topic).
- **new** Storefront branding is applied — CSS design tokens, typography, and colors.

### SEO and indexing

- Add document title metadata for key pages (especially PDPs and PLPs). See the [SEO metadata](/setup/seo/metadata/) documentation for details.
- Ensure that your PDPs have [metadata and structured data](/setup/seo/metadata/) (for example, JSON-LD is configured).
- Standardize URL formats for products (example: `domain/product-name`).
- Redirect all vanity URLs to canonical URLs.
- Add a `robots.txt` file to your project, which allows your site to be indexed by search
  engines. Ensure that your sitemaps are referenced and that you add rules to block indexing
  of any content that you do not want to be indexed (for example, the `/drafts` folder).
- Add one or multiple [redirect](https://www.aem.live/docs/redirects) files to ensure that
  URLs that were changed as part of the migration still work (for example, when you remove the
  `.html` file extension).
- Generate a sitemap for your site and catalog. To speed up the indexing process, Adobe
  recommends adding the sitemap to Google Search Console.
- **new** Canonical URLs return 2xx status (not 3xx or 4xx).
- **new** `hreflang` tags are added to the sitemap for multilingual sites.
- **new** The Google Search Console coverage report is reviewed.

### Enable pre-rendering

- Add pre-rendering for key pages. See the [pre-rendering documentation](/setup/configuration/aem-prerender/) for details.
- Verify that all URLs are lowercase to support pre-rendering without breaking any links.
- Validate HTML source for metadata and enriched body content (to ensure pre-rendering is working).
- Check availability of page translations for locales with different languages.

### Performance and monitoring

- Ensure you have followed all [Performance best practices](/get-started/performance/).
- (Optional) Configure Google Analytics and Google Tag Manager.
- Validate your [storefront
  events](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger)
  implementation and ensure that data is displayed in your Live Search and Product
  Recommendation dashboards in the Adobe Commerce Admin.
- Ensure that the `environment` analytics config parameter is set appropriately in your [Commerce configuration](/setup/configuration/commerce-configuration). It should be set to `"Testing"` when you are developing your storefront, and `"Production"` when you are ready to deploy your storefront. See the [Instrumentation](/setup/analytics/instrumentation/) documentation for more information.
- Ensure that the site's Lighthouse score is green; targeting `100` on every page (taking into
  account previous considerations mentioned in this document).

### Security and access

- Verify that you have configured permissions for DA content and EDS sites. See [DA.live permissions](https://da.live/docs/administration/permissions) and [authentication setup for authoring](https://www.aem.live/docs/authentication-setup-authoring).
- Ensure that the product visuals integration has been provisioned. See [AEM Cloud Service access overview](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#).
- Verify/update password reset links. Match the Edge Delivery Services implementation in the Adobe Commerce Admin. See the [FAQ](/troubleshooting/faq#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix) for details.
- Provide and configure production keys for integrations and payment providers.
- Verify that the new domains/subdomains are `allowlisted` and potential backend webhooks are working.

### CDN and caching

- Update your CDN configuration with your production GraphQL endpoint (`yourproject.com/graphql`). Use that endpoint for all Sidekick extensions and scripts (for example, sitemap generation and the image importer).
- Request a new CDN purge token for the Adobe Commerce production environment when you use Adobe Commerce Fastly. Update the `.helix/config.xlsx` file in SharePoint with the `authToken` and `serviceId` values.
- Validate your [CDN configuration](/setup/configuration/content-delivery-network/) and ensure that caching
  and cache invalidation work as expected.
- Add a store-specific cache buster to the Catalog Service and Live Search requests for [multi-store setups](/setup/seo/indexing/#multi-store-setups) (for example, a query parameter or proxy through your CDN configuration).
- **new** Push invalidation is set up and tested (publish a change, then verify on the production domain).
- **new** DNS TTL is reduced to the minimum before cutover.
- **new** DNS A/CNAME records are updated for all domains and hostnames.
- **new** SSL/TLS certificate is provisioned and verified for the production domain.
- **new** `www` ↔ apex redirects work correctly.

### ~~Catalog service~~ moved to "Storefront is connected to Optimizer"

### ~~Project management and updates~~ moved to ""Launch day and post-launch support.""

- ~~Notify Adobe early about your planned launch date to ensure that the Adobe Commerce team is
  available to support you during the launch.~~ 
- ~~Check for the latest boilerplate changes and update your project accordingly.~~ 

---

## Security and compliance

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

---

## Analytics and monitoring

- **RUM:** Real Use Monitoring (RUM) is instrumented for before/after launch comparison.
- **Analytics:** Adobe Experience Platform data collection is configured (if applicable).
- **Analytics:** Martech stack tags fire correctly on the production hostname.
- **Analytics:** Analytics baselines are documented — expect metric shifts post-launch (pageviews, bounce rate, and so on).
- **Events:** Conversion tracking is verified end-to-end (add-to-cart → checkout → confirmation).

---

## Testing

- [ctag] [Testing] **Functional:** All user flows are tested: browse → search → filter → add to cart → checkout → account creation.
- [ctag] [Testing] **Functional:** Payment gateways are tested with real and test transactions.
- [ctag] [Testing] **Functional:** Order placement, confirmation emails, and order tracking are verified.
- [ctag] [Testing] **Functional:** Shipping options and tax calculations are accurate.
- [ctag] [Testing] **Functional:** Coupon codes, discounts, and loyalty programs work.
- **UAT:** User Acceptance Testing (UAT) is completed on staging and production.
- [ctag] [Testing] **Performance:** Load and stress testing is completed; results are shared with Adobe CTA/CSE.
- [ctag] [Testing] **Performance:** Page load speed is validated — under 3 seconds on desktop and mobile.
- [ctag] [Testing] **Performance:** Images, scripts, and assets are optimized for performance.
- [ctag] [Testing] **Compatibility:** Cross-browser testing is completed (Chrome, Firefox, Safari, Edge).
- [ctag] [Testing] **Compatibility:** Responsive design is verified on all device sizes (mobile, tablet, desktop).
- [ctag] [Testing] **Compatibility:** Performance is tested under different network conditions (3G, 4G, Wi-Fi).
- **Accessibility:** An accessibility audit is completed (WCAG compliance, screen reader, keyboard navigation).
- **Functional:** A 404 error monitoring plan is in place for post-launch.
- **UAT:** A rollback plan is documented and tested in case of launch issues.

---

## Launch day and post-launch support

- ~~The Edge Delivery Services~~ CTAG team is notified — email ~~[aemgolives@adobe.com](mailto:aemgolives@adobe.com)~~ Contact point is required here with URLs, domain, date, contact, and Slack or Teams channel.
- [ctag] [Launch Support] **Support:** P1 hotline number is recorded: US (+1) 800 497 0335 — press 6 for Commerce.
- [ctag] [Launch Support] **Support:** Support ticket process is understood — file a ticket **first**, then call the P1 hotline.
- Post-launch: verify Lighthouse score on the production domain.
- Post-launch: monitor Google Search Console for indexing and crawl errors.
- Post-launch: monitor the 404 report and add redirects for high-traffic legacy URLs.
- Post-launch: martech and analytics data are flowing correctly on production.
- Post-launch: notify CTA/CSE/AM to activate High SLA monitoring.
- Disaster recovery plan is documented and tested.
- Track and update to the latest boilerplate and extension packages versions
