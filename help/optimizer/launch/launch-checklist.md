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

- You [provisioned](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project) the instance.
- You removed all testing and dummy data.
- You loaded production data on the instance.
- You know the [GraphQL endpoint](https://developer.adobe.com/commerce/webapi/graphql/).
- The instance is [ready for launch](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist).

## Verify Commerce Optimizer instance {#verify-optimizer}

Confirm that your [!DNL Adobe Commerce Optimizer] production instance is set up correctly.

- You [created](../get-started.md) the instance.
- The instance is in the correct region.
- The environment type is Production.
- You know the organization ID, client ID, ingestion URL, and Commerce Optimizer URL. See [Get started](../get-started.md).
- You adjusted limits and boundaries with your Adobe CTA and received confirmation.
- You removed all testing and dummy data.

## Verify storefront site {#verify-storefront-site}

Confirm that your Edge Delivery Services storefront site exists and access is restricted.

- You [created](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/) the site.
- You know the site name.
- Only authorized people have [permission to publish](https://tools.aem.live/tools/user-admin/index.html).
- Only authorized people have [permission to author](https://docs.da.live/administrators/guides/permissions).

## Verify Cloud and Optimizer integration {#cloud-optimizer-integration}

Confirm that Adobe Commerce on Cloud and [!DNL Adobe Commerce Optimizer] exchange data correctly.

### On Adobe Commerce

Complete these checks in your Cloud project.

- You [installed and configured](../../aco-connector/get-started.md) the Commerce Optimizer connector.
- The `aco:conf:show` CLI command confirms connection to the production Commerce Optimizer instance. The organization ID, client ID, ingestion URL, and Commerce Optimizer URL match production.
- You selected synchronization scopes in [Export configuration](../../aco-connector/get-started.md).
- [Data feed sync status](../../aco-connector/get-started.md) shows that data left the Cloud instance.

### In Commerce Optimizer

Complete these checks in the [!DNL Adobe Commerce Optimizer] UI.

- The [data sync dashboard](../setup/data-sync.md) shows received data. Products, prices, and attributes appear for Catalog Service, Product Discovery, and Recommendations.
- [Price books](../setup/pricebooks.md) are auto-created from customer groups on Cloud.
- An administrator created [catalog views](../setup/catalog-view.md) and you know their IDs.
- An administrator created [policies](../setup/policies.md) and you know their IDs.
- An administrator set up [facets](../merchandising/facets/overview.md).
- An administrator set up [synonyms](../merchandising/synonyms/overview.md).
- An administrator set up [merchandising rules](../merchandising/rules/overview.md).
- You configured [price faceting and search language](../settings.md) if required.
- You created and validated [product recommendations](../merchandising/recommendations/create.md).
- [Search performance data](../manage-results/search-performance.md) appears in the *Admin*.
- [Recommendations performance data](../manage-results/recommendation-performance.md) appears in the *Admin*.

## Verify storefront and Cloud integration {#storefront-cloud-integration}

Confirm that the storefront reads from the correct Adobe Commerce GraphQL endpoint.

### On Adobe Commerce

- You [installed](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/) storefront compatibility packages.

### On the storefront

- The storefront `commerce-core-endpoint` setting points to your [Cloud GraphQL endpoint](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
- If you use API Mesh as a proxy for Cloud GraphQL, you set `commerce-core-endpoint` to the API Mesh endpoint instead of the Cloud GraphQL endpoint.

## Verify storefront and Optimizer integration {#storefront-optimizer-integration}

Confirm Commerce Optimizer settings in storefront configuration.

- Your storefront uses the correct [Commerce Optimizer settings](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
- You set `adobe-commerce-optimizer` to `true`.
- You set `commerce-endpoint` to the production Commerce Optimizer GraphQL endpoint, or to the API Mesh endpoint when you use API Mesh.
- You set `headers.cs.AC-view-ID` to the catalog view ID from your production Commerce Optimizer instance.

## Verify third-party services on Cloud {#third-party-services}

Confirm integrations that run on your host commerce system (not in [!DNL Adobe Commerce Optimizer]).

- **Payments:** Payment gateway is live and tested (Stripe, PayPal, Adyen, and so on).
- **Shipping:** Shipping API connections work (UPS, FedEx, and so on).
- **Shipping:** Fulfillment platform is connected and tested (for example, ShipStation).
- **Tax:** Tax calculation integration is validated (Avalara, TaxJar, and so on).
- **Tax:** Accounting software sync works (QuickBooks, and so on).
- **Inventory:** PIM, ERP, or inventory management integration is tested and syncing.
- **Architecture:** The host commerce system handles payment, shipping, tax, and inventory (not [!DNL Adobe Commerce Optimizer]).
- **Architecture:** API Mesh and App Builder stay in sync between the host commerce system and [!DNL Adobe Commerce Optimizer].
- **Email:** Transactional email delivery works (order confirmation, shipping, and so on).
- **Email:** Email templates match your brand and use correct links.

## Verify App Builder and API Mesh {#app-builder-mesh}

Confirm extensibility configuration for production.

- **App Builder:** You applied all configurations and services to the production workspace.
- **App Builder:** You tested the production app across build scenarios.
- **API Mesh:** Configurations and sources are ready for production.
- **App Builder:** You reviewed product limits—see the [Adobe Developer App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} and [App Builder system settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
- **App Builder:** The production app uses App Builder production endpoints.
- **Events:** Adobe I/O Events are configured and subscriptions are verified.
- **App Builder:** You deployed custom *Admin* panel extensions to the production workspace.

## Finalize storefront experience {#finalize-storefront}

Polish content, SEO, performance, security, and CDN behavior before launch.

### Content and authoring

Confirm authoring workflow and storefront components.

- You reviewed the [AEM/EDS go-live checklist](https://www.aem.live/docs/go-live-checklist).
- You selected and configured the authoring source (document-based or Universal Editor).
- You publish content through the preview → publish cycle.
- You completed content and design QA on the `.aem.live` domain.
- You added a favicon.
- You [configured](https://docs.da.live/administrators/guides/permissions) da.live and product visuals with dedicated credentials.
- You [customized](../storefront.md) and tested drop-ins (cart, checkout, PDP, PLP, auth, account).
- You applied storefront branding (CSS design tokens, typography, and colors).

### SEO and indexing

Confirm metadata, URLs, and crawl behavior.

- You added document title metadata for key pages (especially PDPs and PLPs). See [SEO metadata](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
- PDPs include [metadata and structured data](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} (for example, JSON-LD).
- Product URL formats are consistent (for example, `domain/product-name`).
- Vanity URLs redirect to canonical URLs.
- Your project includes `robots.txt` that allows indexing where appropriate, references sitemaps, and blocks paths you do not want indexed (for example, `/drafts`).
- You added [redirect](https://www.aem.live/docs/redirects) files so changed URLs (for example, after removing `.html`) still resolve.
- You generated a sitemap and, where helpful, submitted it in Google Search Console.
- Canonical URLs return `2xx` status (not `3xx` or `4xx`).
- Multilingual sites include `hreflang` tags in the sitemap.
- You reviewed the Google Search Console coverage report.

### Pre-rendering

Confirm server-side rendering where you enable it.

- You enabled pre-rendering for key pages. See [Pre-rendering for AEM](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
- URLs use lowercase so pre-rendering does not break links.
- HTML source includes metadata and body content that confirm pre-rendering works.
- Locales show the correct translated pages where applicable.
- You [configured](https://www.aem.live/docs/redirects) additional HTML markup as needed.

### Performance and monitoring

Confirm performance baselines and analytics wiring.

- You followed [performance best practices](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
- (Optional) You configured Google Analytics and Google Tag Manager.
- You validated [storefront events](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger) implementation and see data in your [!DNL Live Search] and [!DNL Product Recommendations] dashboards in the Adobe Commerce *Admin*.
- You set the `environment` analytics parameter in [Commerce configuration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"} to `"Testing"` during development and `"Production"` at go-live. See [Analytics instrumentation](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}.
- Lighthouse scores meet your targets (for example, `100` on key pages) given the guidance in this topic.

### Security and access

Confirm permissions and secrets.

- You configured permissions for DA content and EDS sites. See [DA.live permissions](https://da.live/docs/administration/permissions) and [Authentication setup for authoring](https://www.aem.live/docs/authentication-setup-authoring).
- You provisioned the product visuals integration. See [AEM Cloud Service access overview](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#).
- Password reset links in email templates match your Edge Delivery Services setup. See the storefront FAQ: [What should I do if my email template links are broken after migrating to Edge Delivery Services or Helix?](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}.
- You provided and configured production keys for integrations and payment providers.
- You allowlisted new domains or subdomains and verified backend webhooks.

### CDN and caching

Confirm CDN, DNS, and cache behavior.

- Your CDN uses the production GraphQL endpoint (`yourproject.com/graphql`) for Sidekick extensions and scripts (for example, sitemap generation and the image importer).
- When you use Adobe Commerce Fastly, you requested a CDN purge token and updated [site configuration](https://tools.aem.live/tools/cdn-setup/index.html) with `authToken` and `serviceId`.
- [CDN configuration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"} validates caching and invalidation.
- For [multi-store setups](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}, Catalog Service and [!DNL Live Search] requests include a store-specific cache buster (for example, a query parameter or CDN rule).
- Push invalidation works end to end (publish a change, then verify on the production domain).
- You lowered DNS TTL before cutover.
- You updated DNS A and CNAME records for all domains and hostnames.
- The SSL/TLS certificate is provisioned and verified for the production domain.
- `www` and apex redirects behave correctly.

## Security and compliance {#security-compliance}

Confirm security posture and compliance tasks.

- **SSL:** You installed a trusted SSL/TLS certificate.
- **SSL:** HTTPS is enforced site-wide.
- **Access:** You changed default *Admin* passwords and enforce a strong password policy. Manage [!DNL Adobe Commerce Optimizer] users in [User and identity management](../user-management.md).
- **Access:** You changed the *Admin* URL from the default.
- **Access:** Two-factor authentication is enabled for all *Admin* users.
- **Access:** You removed unused *Admin* users from the project.
- **Firewall:** Web Application Firewall (WAF) is configured and verified.
- **PCI:** You completed security penetration testing on production (PCI scope).
- **Scanning:** You registered the Adobe Security Scan Tool and completed an initial scan.
- **Access:** CORS allows only approved origins.
- **Compliance:** You reviewed the [shared responsibility model](../shared-responsibility.md) for [!DNL Adobe Commerce Optimizer] (Adobe compared with customer responsibilities).
- **Compliance:** Privacy policy, cookie consent, and GDPR or CCPA requirements are verified.

## Analytics and monitoring {#analytics-monitoring}

Confirm measurement and baselines.

- **RUM:** Real User Monitoring (RUM) is instrumented for before-and-after comparison.
- **Analytics:** Adobe Experience Platform data collection is configured (if applicable).
- **Analytics:** Martech tags fire on the production hostname.
- **Analytics:** You documented analytics baselines and expect shifts after launch (pageviews, bounce rate, and so on).
- **Events:** Conversion tracking works end to end (add to cart → checkout → confirmation).

## Testing {#testing}

Confirm quality before and after launch.

- **Functional:** You tested browse → search → filter → add to cart → checkout → account creation.
- **Functional:** You tested payment gateways with real and test transactions.
- **Functional:** Order placement, confirmation email, and order tracking work.
- **Functional:** Shipping options and tax calculations are accurate.
- **Functional:** Coupons, discounts, and loyalty programs behave as expected.
- **UAT:** You completed user acceptance testing on staging and production.
- **Performance:** You completed load and stress testing and shared results with Adobe CTA or CSE.
- **Performance:** Page load time is under three seconds on desktop and mobile.
- **Performance:** Lighthouse scores meet targets on key pages (for example, via PageSpeed Insights).
- **Performance:** Images, scripts, and assets are optimized.
- **Compatibility:** You tested Chrome, Firefox, Safari, and Edge.
- **Compatibility:** Responsive layouts work on mobile, tablet, and desktop.
- **Compatibility:** You tested performance on 3G, 4G, and Wi-Fi.
- **Accessibility:** You completed an accessibility audit (WCAG, screen reader, keyboard navigation).
- **Functional:** You have a 404 monitoring plan for after launch.
- **UAT:** You documented and tested a rollback plan if launch issues occur.

## Launch day and post-launch {#launch-post-launch}

Confirm communication, support, and follow-up tasks.

- You notified Adobe of the launch date (email your CTA).
- **Support:** You recorded the P1 hotline: US (+1) 800-497-0335, then press 6 for Commerce.
- **Support:** Your team knows to open a support ticket **first**, then call the P1 hotline.
- **After launch:** Verify Lighthouse scores on the production domain.
- **After launch:** Monitor Google Search Console for indexing and crawl errors.
- **After launch:** Monitor 404 reports and add redirects for high-traffic legacy URLs.
- **After launch:** Confirm martech and analytics data on production.
- **After launch:** Ask your CTA, CSE, or AM to enable high-SLA monitoring.
- You documented and tested a disaster recovery plan.
- You track and upgrade boilerplate and extension packages to current versions.
