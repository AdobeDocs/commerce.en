---
title: Launch Checklist
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

Use this checklist to verify that your production [!DNL Adobe Commerce Optimizer] project is configured, tested, and ready for launch. Work through each section with your team and track completion in your own project plan or tracker. For product capabilities and UI areas referenced below, see the [[!DNL Adobe Commerce Optimizer] documentation](../overview.md).

## Use case and architecture {#use-case}

Use this checklist when you deliver a B2C experience that combines [!DNL Adobe Commerce Optimizer] and Edge Delivery Services (EDS) with an existing Adobe Commerce on Cloud instance.

Your solution typically includes these components:

- **Cloud**—Adobe Commerce on Cloud manages catalog data, customers, assets, and purchase flows (checkout, order management, shipping, and so on).
- **Optimizer**—[!DNL Adobe Commerce Optimizer] delivers merchandising experiences.
- **Storefront**—Adobe Commerce Storefront on Edge Delivery Services provides the UI.
- **Third-party services**—Payment, shipping, and tax providers.
- **App Builder**—Extensibility.
- **API Mesh**—Request routing.

## Verify Adobe Commerce on Cloud {#verify-cloud}

Confirm that your Adobe Commerce on Cloud environment is ready for production.

&#x25A2; The Cloud instance is [provisioned](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project).
&#x25A2; Testing and dummy data are removed from the instance.
&#x25A2; Production data is loaded on the instance.
&#x25A2; You know the [GraphQL endpoint](https://developer.adobe.com/commerce/webapi/graphql/).
&#x25A2; The instance meets [ready-for-launch](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist) requirements.

## Verify Commerce Optimizer instance {#verify-optimizer}

Confirm that your [!DNL Adobe Commerce Optimizer] production instance is set up correctly.

&#x25A2; The production instance is active. See [Get started](../get-started.md) for how you provision it.
&#x25A2; The instance is in the correct region.
&#x25A2; The environment type is Production.
&#x25A2; You know the organization ID, client ID, ingestion URL, and Commerce Optimizer URL. See [Get started](../get-started.md).
&#x25A2; Configured limits and boundaries match the values confirmed by your Adobe Customer Technical Advisor (CTA).
&#x25A2; Testing artifacts and dummy data have been removed from the instance.

## Verify storefront site {#verify-storefront-site}

Confirm that your Edge Delivery Services storefront site exists and access is restricted.

&#x25A2; The storefront site exists. See [Create a storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/).
&#x25A2; You know the site name.
&#x25A2; Only authorized people have [permission to publish](https://tools.aem.live/tools/user-admin/index.html).
&#x25A2; Only authorized people have [permission to author](https://docs.da.live/administrators/guides/permissions).

## Verify Cloud and Optimizer integration {#cloud-optimizer-integration}

Confirm that Adobe Commerce on Cloud and [!DNL Adobe Commerce Optimizer] exchange data correctly.

### On Adobe Commerce

Complete these checks in your Cloud project.

&#x25A2; The Commerce Optimizer connector is [installed and configured](../../aco-connector/get-started.md).
&#x25A2; The `aco:conf:show` CLI command confirms connection to the production Commerce Optimizer instance. The organization ID, client ID, ingestion URL, and Commerce Optimizer URL match production.
&#x25A2; Synchronization scopes in [Export configuration](../../aco-connector/get-started.md) match your requirements.
&#x25A2; [Data feed sync status](../../aco-connector/get-started.md) confirms data export from the Cloud instance.

### In Commerce Optimizer

Complete these checks in the [!DNL Adobe Commerce Optimizer] UI.

&#x25A2; The [data sync dashboard](../setup/data-sync.md) shows received data. Products, prices, and attributes appear for Catalog Service, Product Discovery, and Recommendations.
&#x25A2; [Price books](../setup/pricebooks.md) are auto-created from customer groups on Cloud.
&#x25A2; [Catalog views](../setup/catalog-view.md) exist and you know their IDs.
&#x25A2; [Policies](../setup/policies.md) exist and you know their IDs.
&#x25A2; [Facets](../merchandising/facets/overview.md) are configured.
&#x25A2; [Synonyms](../merchandising/synonyms/overview.md) are configured.
&#x25A2; [Merchandising rules](../merchandising/rules/overview.md) are configured.
&#x25A2; [Price faceting and search language](../settings.md) match your requirements when you use those features.
&#x25A2; [Product recommendations](../merchandising/recommendations/create.md) exist and behave as expected in preview.
&#x25A2; [Search performance data](../manage-results/search-performance.md) appears in the *Admin*.
&#x25A2; [Recommendations performance data](../manage-results/recommendation-performance.md) appears in the *Admin*.

## Verify storefront and Cloud integration {#storefront-cloud-integration}

Confirm that the storefront reads from the correct Adobe Commerce GraphQL endpoint.

### On Adobe Commerce

&#x25A2; Storefront compatibility packages are [installed](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/).

### On the storefront

&#x25A2; The storefront `commerce-core-endpoint` setting points to your [Cloud GraphQL endpoint](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
&#x25A2; If you use API Mesh as a proxy for Cloud GraphQL, `commerce-core-endpoint` points to the API Mesh endpoint instead of the Cloud GraphQL endpoint.

## Verify storefront and Optimizer integration {#storefront-optimizer-integration}

Confirm Commerce Optimizer settings in the storefront configuration.

&#x25A2; Your storefront uses the correct [Commerce Optimizer settings](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
&#x25A2; `adobe-commerce-optimizer` is `true`.
&#x25A2; `commerce-endpoint` points to the production Commerce Optimizer GraphQL endpoint, or to the API Mesh endpoint when you use API Mesh.
&#x25A2; `headers.cs.AC-view-ID` holds the catalog view ID from your production Commerce Optimizer instance.

## Verify third-party services on Cloud {#third-party-services}

Confirm integrations that run on your host commerce system (not in [!DNL Adobe Commerce Optimizer]).

&#x25A2; **Payments:** Payment gateway is live and tested (Stripe, PayPal, Adyen, and so on).
&#x25A2; **Shipping:** Shipping API connections work (UPS, FedEx, and so on).
&#x25A2; **Shipping:** Fulfillment platform is connected and tested (for example, ShipStation).
&#x25A2; **Tax:** Tax calculation integration is validated (Avalara, TaxJar, and so on).
&#x25A2; **Tax:** Accounting software sync works (QuickBooks, and so on).
&#x25A2; **Inventory:** PIM, ERP, or inventory management integration is tested and syncing.
&#x25A2; **Architecture:** The host commerce system handles payment, shipping, tax, and inventory (not [!DNL Adobe Commerce Optimizer]).
&#x25A2; **Architecture:** API Mesh and App Builder stay in sync between the host commerce system and [!DNL Adobe Commerce Optimizer].
&#x25A2; **Email:** Transactional email delivery works (order confirmation, shipping, and so on).
&#x25A2; **Email:** Email templates match your brand and use correct links.

## Verify App Builder and API Mesh {#app-builder-mesh}

Confirm extensibility configuration for production.

### App Builder

&#x25A2; The production workspace includes all required configurations and services.
&#x25A2; The production app passes testing across build scenarios.
&#x25A2; Product limits and boundaries have been reviewed and confirmed based on the [Adobe Developer App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} and [App Builder system settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
&#x25A2; The production app uses App Builder production endpoints.
&#x25A2; Custom *Admin* panel extensions are deployed to the production workspace.

### API Mesh

&#x25A2; Configurations and sources are ready for production.

### Events

&#x25A2; Adobe I/O Events are configured and subscriptions are verified.

## Finalize storefront experience {#finalize-storefront}

Polish content, SEO, performance, security, and CDN behavior before launch.

### Content and authoring

Confirm authoring workflow and storefront components.

&#x25A2; The [AEM/EDS go-live checklist](https://www.aem.live/docs/go-live-checklist) review is complete.
&#x25A2; The authoring source is document-based or Universal Editor (and configured).
&#x25A2; Content is published using the preview → publish cycle.
&#x25A2; Content and design QA is complete on the `.aem.live` domain.
&#x25A2; A favicon is configured and served correctly by the site.
&#x25A2; da.live and product visuals use [configured](https://docs.da.live/administrators/guides/permissions) dedicated credentials.
&#x25A2; Drop-ins (cart, checkout, PDP, PLP, auth, account) are [customized](../storefront.md) and tested.
&#x25A2; Storefront branding reflects CSS design tokens, typography, and colors.

### SEO and indexing

Confirm metadata, URLs, and crawl behavior.

&#x25A2; Document title metadata is present for key pages (especially PDPs and PLPs). See [SEO metadata](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
&#x25A2; PDPs include [metadata and structured data](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} (for example, JSON-LD).
&#x25A2; Product URL formats are consistent (for example, `domain/product-name`).
&#x25A2; Vanity URLs redirect to canonical URLs.
&#x25A2; The project includes `robots.txt` that allows indexing where appropriate, references sitemaps, and blocks paths you do not want indexed (for example, `/drafts`).
&#x25A2; [Redirect](https://www.aem.live/docs/redirects) files cover URL changes from migration (for example, after removing `.html`).
&#x25A2; Sitemap exists and is submitted to Google Search Console as needed.
&#x25A2; Canonical URLs return `2xx` status (not `3xx` or `4xx`).
&#x25A2; Multilingual sites include `hreflang` tags in the sitemap.
&#x25A2; The Google Search Console coverage report is current.

### Pre-rendering

Confirm server-side rendering where you enable it.

&#x25A2; Pre-rendering is on for key pages. See [Pre-rendering for AEM](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
&#x25A2; URLs use lowercase so pre-rendering does not break links.
&#x25A2; HTML source includes metadata and body content that confirm pre-rendering works.
&#x25A2; Locales show the correct translated pages where applicable.
&#x25A2; Additional HTML markup is [configured](https://www.aem.live/docs/redirects) as needed.

### Performance and monitoring

Confirm performance baselines and analytics wiring.

&#x25A2; Your storefront follows [performance best practices](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
&#x25A2; (Optional) Google Analytics and Google Tag Manager are configured.
&#x25A2; [Storefront events](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger) implementation is valid and data appears in your [!DNL Live Search] and [!DNL Product Recommendations] dashboards in the Adobe Commerce *Admin*.
&#x25A2; The `environment` analytics parameter in [Commerce configuration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"} is `"Testing"` during development and `"Production"` at go-live. See [Analytics instrumentation](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}.
&#x25A2; Lighthouse scores meet your targets (for example, `100` on key pages) given the guidance in this topic.

### Security and access

Confirm permissions and secrets.

&#x25A2; Appropriate permissions are configured for DA content and EDS sites. See [DA.live permissions](https://da.live/docs/administration/permissions) and [Authentication setup for authoring](https://www.aem.live/docs/authentication-setup-authoring).
&#x25A2; The product visuals integration is provisioned. See [AEM Cloud Service access overview](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#).
&#x25A2; Password reset links in email templates match your Edge Delivery Services setup. See the storefront FAQ: [What should I do if my email template links are broken after migrating to Edge Delivery Services or Helix?](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}.
&#x25A2; Production keys for integrations and payment providers are in place.
&#x25A2; Domains are allowlisted and backend webhooks work.

### CDN and caching

Confirm CDN, DNS, and cache behavior.

&#x25A2; The CDN configuration uses the production GraphQL endpoint (`yourproject.com/graphql`) for Sidekick extensions and scripts (for example, sitemap generation and the image importer).
&#x25A2; When you use Adobe Commerce Fastly, a CDN purge token is available and [site configuration](https://tools.aem.live/tools/cdn-setup/index.html) includes `authToken` and `serviceId`.
&#x25A2; [CDN configuration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"} validates caching and invalidation.
&#x25A2; For [multi-store setups](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}, Catalog Service and [!DNL Live Search] requests include a store-specific cache buster (for example, a query parameter or CDN rule).
&#x25A2; Push invalidation works end to end (publish a change, then verify on the production domain).
&#x25A2; DNS TTL is low enough before cutover.
&#x25A2; DNS A and CNAME records are correct for all domains and hostnames.
&#x25A2; The SSL/TLS certificate is provisioned and verified for the production domain.
&#x25A2; `www` and apex redirects behave correctly.

## Security and compliance {#security-compliance}

Confirm security posture and compliance tasks.

&#x25A2; **SSL:** A trusted SSL/TLS certificate is installed.
&#x25A2; **SSL:** HTTPS is enforced site-wide.
&#x25A2; **Access:** Default *Admin* passwords are changed and a strong password policy is in place. See [!DNL Adobe Commerce Optimizer] [User and identity management](../user-management.md).
&#x25A2; **Access:** The *Admin* URL is not the default.
&#x25A2; **Access:** Two-factor authentication is enabled for all *Admin* users.
&#x25A2; **Access:** No inactive or unused Admin users are associated with the project.
&#x25A2; **Firewall:** Web Application Firewall (WAF) is configured and verified.
&#x25A2; **PCI:** Security penetration testing on production (PCI scope) is complete.
&#x25A2; **Scanning:** The Adobe Security Scan Tool is registered and an initial scan is complete.
&#x25A2; **Access:** CORS allows only approved origins.
&#x25A2; **Compliance:** The  [shared responsibility model](../shared-responsibility.md) for [!DNL Adobe Commerce Optimizer] is up to date and clearly defines Adobe versus customer responsibilities.
&#x25A2; **Compliance:** Privacy policy, cookie consent, and GDPR or CCPA requirements are verified.

## Analytics and monitoring {#analytics-monitoring}

Confirm measurement and baselines.

&#x25A2; **RUM:** Real User Monitoring (RUM) is instrumented for before-and-after comparison.
&#x25A2; **Analytics:** Adobe Experience Platform data collection is configured (if applicable).
&#x25A2; **Analytics:** Verified that MarTech tags fire on the production hostname.
&#x25A2; **Analytics:** Baseline analytics are documented; post‑launch fluctuations (page views, bounce rate, and so on) are expected.
&#x25A2; **Events:** Conversion tracking works end to end (add to cart → checkout → confirmation).

## Testing {#testing}

Confirm quality before and after launch.

&#x25A2; **Functional:** Core flows work end to end: browse → search → filter → add to cart → checkout → account creation.
&#x25A2; **Functional:** Payment gateways accept real and test transactions.
&#x25A2; **Functional:** Order placement, confirmation email, and order tracking work.
&#x25A2; **Functional:** Shipping options and tax calculations are accurate.
&#x25A2; **Functional:** Coupons, discounts, and loyalty programs behave as expected.
&#x25A2; **UAT:** User acceptance testing is complete on staging and production.
&#x25A2; **Performance:** Load and stress testing is complete and Adobe CTA or CSE has the results.
&#x25A2; **Performance:** Page load time is under three seconds on desktop and mobile.
&#x25A2; **Performance:** Lighthouse scores meet targets on key pages (for example, via PageSpeed Insights).
&#x25A2; **Performance:** Images, scripts, and assets are optimized.
&#x25A2; **Compatibility:** Chrome, Firefox, Safari, and Edge behave as expected.
&#x25A2; **Compatibility:** Responsive layouts work on mobile, tablet, and desktop.
&#x25A2; **Compatibility:** Performance is acceptable on 3G, 4G, and Wi-Fi.
&#x25A2; **Accessibility:** An accessibility audit is complete (WCAG, screen reader, keyboard navigation).
&#x25A2; **Functional:** A post‑launch 404 monitoring plan is in place.
&#x25A2; **UAT:** A rollback plan exists and passes testing if launch issues occur.

## Launch day and post-launch {#launch-post-launch}

Confirm communication, support, and follow-up tasks.

&#x25A2; **Launch coordination:** Adobe has your confirmed launch date; the CTA has been notified by email.
&#x25A2; **Support:** The P1 hotline number is recorded: US (+1) 800-497-0335, then press 6 for Commerce.
&#x25A2; **Support:** Your team is trained to open a support ticket **before** calling the P1 hotline.
&#x25A2; **Post launch:** Verify Lighthouse scores on the production domain.
&#x25A2; **Post launch:** Monitor Google Search Console for indexing and crawl errors.
&#x25A2; **Post launch:** Monitor 404 reports and add redirects for high-traffic legacy URLs.
&#x25A2; **Post launch:** Confirm MarTech and analytics data on production.
&#x25A2; **Post launch:** Ask your CTA, CSE, or AM to enable high-SLA monitoring.
&#x25A2; A disaster recovery plan exists and passes testing.
&#x25A2; A process is in place to track and upgrade boilerplate and extension packages to current versions.
