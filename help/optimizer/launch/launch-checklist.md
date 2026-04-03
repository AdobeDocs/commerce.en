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

B2C, 
leverage the Optimizer and EDS capabilities for the existing Adobe Commerce on Cloud instance. 
Assets are in Commerce 

### Components
- **Cloud** - Adobe Commerce on Cloud, to manage the Catalog data, Customers, and serve purchase experiences (checkout, order management, shipping, etc )
- **Optimizer** - Adobe Commerce Optimizer, to serve merchandising experiences
- **Storefront** - Adobe Commerce Storefront on Edge Delivery Services, to build UI
- **Third-Party services** to cover Payment, Shipping, Tax
- **App Builder** 🟦 TODO: add reasoning for the component
- **API Mesh** 🟦 TODO: add reasoning for the component

---

## Cloud instance is created 
- It is created 🟦 TODO: reference to the way to obtain a Cloud instance
- All testing and dummy data are removed. 
- Production data is loaded to the instance.
- GraphQL endpoint is known 🟦 TODO: reference to the way to obtain the URL 
- 🟦 TODO: reference to Cloud instance checklist if it exists

---

## Optimizer instance is created
- It is [created](../get-started.md).
- Instance is located in the correct region
- Instance type is Production
- Organization ID, Client ID, Ingestion URL, Optimizer studio URL are [known](../get-started.md).
- Limits and boundaries adjusted accordingly 🟦 TODO: reference to the way to change and double-check limits
- All testing and dummy data are removed. 🟦 TODO: reference to the way to 

---


## Storefront instance is created
- A dedicated production instance is [created](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/)
- The name of the production instance is known
- Just authorized personnel have [permissions](https://docs.da.live/administrators/guides/permissions) to publish

---

## Cloud is integrated with Optimizer

### on Cloud
- ACO connector is installed and configured following [Get started with the Adobe Commerce Optimizer Connector](../../aco-connector/get-started.md) for details.
- CLI command aco:conf:show confirms connection with the production Optimizer instance. Organization ID, Client ID, Ingestion URL, Optimizer studio URL match the production instance. 
- Scopes for synchronization are picked. 🟦 TODO: add reference to do the configuration
- Data is synced 🟦 TODO: add reference to data sync board introduced in MDEE  

### on Optimizer
- Data sync is verified on the [Data sync](../setup/data-sync.md) page — expected products, prices, and attributes appear for Catalog Service, Product Discovery, and Recommendations.
- [Price books](../setup/pricebooks.md) are auto-created from customer groups on Cloud. 
- [Catalog views](../setup/catalog-view.md) are created by Admin. Their IDs are known.
- [Policies](../setup/policies.md) are created by Admin. Their IDs are known.
- [Facets](../merchandising/facets/overview.md) are set up by Admin
- [Synonyms](../merchandising/synonyms/overview.md) are set up by Admin
- [Merchandising rules](../merchandising/rules/overview.md) are set up by Admin 
- [Price faceting and search language](../settings.md) are configured if required.
- [Product recommendations](../merchandising/recommendations/create.md) are created and validated.
- [Search data](../manage-results/search-performance.md) is visible in Admin
- [Recommendations data](../manage-results/recommendation-performance.md) is visible in Admin

---

## Storefront is integrated with Cloud

### on Cloud
- Storefront compatibility packages are [installed](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/) 🟦 TODO: should be reviewed and updated by a storefront expert

### on Storefront
- ensure Config.json public/default/commerce-core-endpoint mentions the GraphQL endpoint of the production Cloud instance  
-- 🟦 TODO: should be reviewed and updated by a storefront expert
-- 🟦 TODO: Steven review all config lines to ensure we have the required configuration in place
-- 🟦 TODO: if APi Mesh is used, shouldn't we create the API mesh endpoint and mention its endpoint instead?

---

## Storefront is integrated with Optimizer

### on Storefront  🟦 TODO: should be reviewed and updated by a storefront expert
- Ensure Config.json public/default/adobe-commerce-optimizer set to "true"
- Ensure Config.json public/default/commerce-endpoint mentions the GraphQL endpoint of the production Optimizer instance
- Ensure Config.json public/default/cs/AC-view-ID mentions the correct Catalog View Id created in the production Optimizer instance
- Category IDs and all category pages reference the correct category.  🟦 TODO: refer to steps to check, should we configure   Config.json plugins/picker/rootCategory": "2"
  for categories?

### on Optimizer
- no actions required

---

## Cloud is integrated with Third-Party services

- **Payments:** Payment gateway integration is live and tested (Stripe, PayPal, Adyen, and so on). ℹ️ctag Integrations – Third Party Services
- **Shipping:** Shipping API connections are confirmed (UPS, FedEx, and so on). ℹ️ctag Integrations – Third Party Services
- **Shipping:** Fulfillment platform is connected and tested (for example, ShipStation). ℹ️ctag Integrations – Third Party Services
- **Tax:** Tax calculation integration is validated (Avalara, TaxJar, and so on). ℹ️ctag Integrations – Third Party Services
- **Tax:** Accounting software sync is confirmed (QuickBooks, and so on). ℹ️ctag Integrations – Third Party Services
- **Inventory:** PIM / ERP / inventory management integration is tested and syncing. ℹ️ctag Integrations – Third Party Services
- **Architecture:** The host commerce system handles payment, shipping, tax, and inventory (not [!DNL Adobe Commerce Optimizer]). ℹ️ctag Integrations – Third Party Services
- **Architecture:** API Mesh and App Builder are in sync between the host commerce system and [!DNL Adobe Commerce Optimizer]. ℹ️ctag Integrations – Third Party Services
- **Email:** Transactional email delivery is tested (order confirmation, shipping, and so on).
- **Email:** Email templates are updated to reflect brand and correct links.

---

## Cloud is integrated with App Builder and API Mesh

- **App Builder:** All configurations and services are applied to the production workspace. ℹ️ctag Integrations – App Builder
- **App Builder:** The App Builder production app is tested across all build scenarios. ℹ️ctag Integrations – App Builder
- **API Mesh:** API Mesh configs and sources are ready for the production environment. ℹ️ctag Integrations – App Builder
- **App Builder:** App Builder product limitations are reviewed — see the [Adobe Developer App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} and [App Builder system settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}. ℹ️ctag Integrations – App Builder
- **App Builder:** The production application is configured with App Builder production endpoints. ℹ️ctag Integrations – App Builder
- **Events:** Adobe I/O Events are configured and event subscriptions are verified.
- **App Builder:** Custom admin panel extensions are deployed to the production workspace.

---

## Storefront is finetuned

### Content and authoring

- The [AEM/EDS Go-Live Checklist](https://aem.live/docs/go-live-checklist) is reviewed. 
- Content authoring source is selected and configured (document-based or Universal Editor). ℹ️ctag
- All content is published through the preview → publish cycle. ℹ️ctag
- Content and design QA is completed on the `.aem.live` domain.
- A favicon is added to the site.
- da.live and product visuals are [configured](https://docs.da.live/administrators/guides/permissions) with dedicated credentials. 
- Drop-ins (Cart, Checkout, PDP, PLP, Auth, Account) are [customized](../storefront.md) and tested.
- Storefront branding is applied — CSS design tokens, typography, and colors.

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
- Canonical URLs return 2xx status (not 3xx or 4xx). ℹ️ new
- `hreflang` tags are added to the sitemap for multilingual sites. ℹ️ new
- The Google Search Console coverage report is reviewed. ℹ️ new

### Enable pre-rendering

- Add pre-rendering for key pages. See the [pre-rendering documentation](/setup/configuration/aem-prerender/) for details.
- Verify that all URLs are lowercase to support pre-rendering without breaking any links.
- Validate HTML source for metadata and enriched body content (to ensure pre-rendering is working).
- Check the availability of page translations for locales with different languages.
- Additional HTML markup is configured [configured](https://www.aem.live/docs/redirects)  

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
- Push invalidation is set up and tested (publish a change, then verify on the production domain). ℹ️ new
- DNS TTL is reduced to the minimum before cutover. ℹ️ new
- DNS A/CNAME records are updated for all domains and hostnames. ℹ️ new
- SSL/TLS certificate is provisioned and verified for the production domain. ℹ️ new
- `www` ↔ apex redirects work correctly. ℹ️ new

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

- **Functional:** All user flows are tested: browse → search → filter → add to cart → checkout → account creation. ℹ️ctag Testing
- **Functional:** Payment gateways are tested with real and test transactions. ℹ️ctag Testing
- **Functional:** Order placement, confirmation emails, and order tracking are verified. ℹ️ctag Testing
- **Functional:** Shipping options and tax calculations are accurate. ℹ️ctag Testing
- **Functional:** Coupon codes, discounts, and loyalty programs work. ℹ️ctag Testing
- **UAT:** User Acceptance Testing (UAT) is completed on staging and production.
- **Performance:** Load and stress testing is completed; results are shared with Adobe CTA/CSE. ℹ️ctag Testing
- **Performance:** Page load speed is validated — under 3 seconds on desktop and mobile. ℹ️ctag Testing
- **Performance:** Images, scripts, and assets are optimized for performance. ℹ️ctag Testing
- **Compatibility:** Cross-browser testing is completed (Chrome, Firefox, Safari, Edge). ℹ️ctag Testing
- **Compatibility:** Responsive design is verified on all device sizes (mobile, tablet, desktop). ℹ️ctag Testing
- **Compatibility:** Performance is tested under different network conditions (3G, 4G, Wi-Fi). ℹ️ctag Testing
- **Accessibility:** An accessibility audit is completed (WCAG compliance, screen reader, keyboard navigation).
- **Functional:** A 404 error monitoring plan is in place for post-launch.
- **UAT:** A rollback plan is documented and tested in case of launch issues.

---

## Launch day and post-launch support

- ~~The Edge Delivery Services~~ CTAG team is notified — email ~~[aemgolives@adobe.com](mailto:aemgolives@adobe.com)~~ 🟦 TODO: Contact point is required here with URLs, domain, date, contact, and Slack or Teams channel.
- **Support:** P1 hotline number is recorded: US (+1) 800 497 0335 — press 6 for Commerce. ℹ️ctag Launch Support
- **Support:** Support ticket process is understood — file a ticket **first**, then call the P1 hotline. ℹ️ctag Launch Support
- Post-launch: verify Lighthouse score on the production domain.
- Post-launch: monitor Google Search Console for indexing and crawl errors.
- Post-launch: monitor the 404 report and add redirects for high-traffic legacy URLs.
- Post-launch: martech and analytics data are flowing correctly on production.
- Post-launch: notify CTA/CSE/AM to activate High SLA monitoring.
- Disaster recovery plan is documented and tested.
- Track and update to the latest boilerplate and extension packages versions
