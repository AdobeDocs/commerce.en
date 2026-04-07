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

**Usecase**

B2C, leverage the Commerce Optimizer and EDS capabilities for the existing Adobe Commerce on Cloud instance. 

**Components**

- **Cloud** - Adobe Commerce on Cloud, to manage the Catalog data, Customers, assets, and serve purchase experiences (checkout, order management, shipping, etc )
- **Optimizer** - Adobe Commerce Optimizer, to serve merchandising experiences
- **Storefront** - Adobe Commerce Storefront on Edge Delivery Services, to build UI
- **Third-Party services** to cover Payment, Shipping, Tax
- **App Builder** to implement extensibility
- **API Mesh** to implement request routing

## Cloud instance is created

- It is [provisioned](https://experienceleague.corp.adobe.com/docs/commerce-on-cloud/start/new-project.html?lang=en)
- All testing and dummy data are removed. 
- Production data is loaded to the instance.
- GraphQL endpoint is [known](https://developer.adobe.com/commerce/webapi/graphql/)
- It is [ready for launch](https://experienceleague.corp.adobe.com/docs/commerce-on-cloud/user-guide/launch/checklist.html?lang=en)

## Commerce Optimizer instance is created

- It is [created](../get-started.md).
- Instance is located in the correct region
- Instance type is Production
- Organization ID, Client ID, Ingestion URL, Commerce Optimizer URL are [known](../get-started.md).
- Limits and boundaries adjusted accordingly. Confirmed by Adobe CTA.
- All testing and dummy data are removed.  

## Storefront site is created

- A site is [created](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/)
- The name of the site is known
- Just authorized personnel have [permissions](https://tools.aem.live/tools/user-admin/index.html) to publish
- Just authorized personnel have [permissions](https://docs.da.live/administrators/guides/permissions) to author

## Cloud is integrated with Commerce Optimizer

### on Cloud

- ACO connector is installed and configured following [Get started with the Adobe Commerce Optimizer Connector](../../aco-connector/get-started.md) for details.
- CLI command aco:conf:show confirms connection with the production Commerce Optimizer instance. Organization ID, Client ID, Ingestion URL, Commerce Optimizer URL match the production instance. 
- Scopes for synchronization are picked in [Export Configuration](../../aco-connector/get-started.md)
- [Data Feed Sync Status](../../aco-connector/get-started.md) confirm that data departed the Cloud instance.
  
### on Commerce Optimizer

- [Data sync dashboard ](../setup/data-sync.md) confirms that data is received. Products, prices, and attributes appear for Catalog Service, Product Discovery, and Recommendations.
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

## Storefront is integrated with Cloud

### on Cloud

- Storefront compatibility packages are [installed](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/)

### on Storefront

- Ensure the storefront configuration's commerce-core-endpoint points to your Cloud GraphQL endpoint value. [See](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/)
- If API Mesh is used as a proxy for your Cloud GraphQL, use the API mesh endpoint instead of the Cloud GraphQL endpoint for the commerce-core-endpoint property.

## Storefront is integrated with Commerce Optimizer

- Ensure your storefront configuration has the proper ACO settings: https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/
- `adobe-commerce-optimizer` set to "true"
- `commerce-endpoint` has the GraphQL endpoint of the production Commerce Optimizer instance, or in the case of API Mesh, the API mesh endpoint.
- `headers.cs.AC-view-ID` has the correct Catalog View Id created in the production Commerce Optimizer instance

## Cloud is integrated with Third-Party services

- Payments: Payment gateway integration is live and tested (Stripe, PayPal, Adyen, and so on).
- Shipping: Shipping API connections are confirmed (UPS, FedEx, and so on).
- Shipping: Fulfillment platform is connected and tested (for example, ShipStation).
- Tax: Tax calculation integration is validated (Avalara, TaxJar, and so on).
- Tax: Accounting software sync is confirmed (QuickBooks, and so on).
- Inventory: PIM / ERP / inventory management integration is tested and syncing.
- Architecture: The host commerce system handles payment, shipping, tax, and inventory (not [!DNL Adobe Commerce Optimizer]).
- Architecture: API Mesh and App Builder are in sync between the host commerce system and [!DNL Adobe Commerce Optimizer].
- Email: Transactional email delivery is tested (order confirmation, shipping, and so on).
- Email: Email templates are updated to reflect brand and correct links.

## Cloud is integrated with App Builder and API Mesh

- App Builder: All configurations and services are applied to the production workspace.
- App Builder: The App Builder production app is tested across all build scenarios.
- API Mesh: API Mesh configs and sources are ready for the production environment.
- App Builder: App Builder product limitations are reviewed — see the [Adobe Developer App Builder product description](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} and [App Builder system settings and limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
- App Builder: The production application is configured with App Builder production endpoints.
- Events: Adobe I/O Events are configured and event subscriptions are verified.
- App Builder: Custom admin panel extensions are deployed to the production workspace.

## Storefront is finetuned

### Content and authoring

- The [AEM/EDS Go-Live Checklist](https://aem.live/docs/go-live-checklist) is reviewed. 
- Content authoring source is selected and configured (document-based or Universal Editor).
- All content is published through the preview → publish cycle.
- Content and design QA is completed on the `.aem.live` domain.
- A favicon is added to the site.
- da.live and product visuals are [configured](https://docs.da.live/administrators/guides/permissions) with dedicated credentials. 
- Drop-ins (Cart, Checkout, PDP, PLP, Auth, Account) are [customized](../storefront.md) and tested.
- Storefront branding is applied — CSS design tokens, typography, and colors.

### SEO and indexing

- Add document title metadata for key pages (especially PDPs and PLPs). See [SEO metadata](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
- Ensure that your PDPs have [metadata and structured data](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} (for example, JSON-LD is configured).
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
- Canonical URLs return 2xx status (not 3xx or 4xx).
- `hreflang` tags are added to the sitemap for multilingual sites.
- The Google Search Console coverage report is reviewed.

### Enable pre-rendering

- Add pre-rendering for key pages. See [Pre-rendering for AEM](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
- Verify that all URLs are lowercase to support pre-rendering without breaking any links.
- Validate HTML source for metadata and enriched body content (to ensure pre-rendering is working).
- Check the availability of page translations for locales with different languages.
- Additional HTML markup is [configured](https://www.aem.live/docs/redirects) as needed.

### Performance and monitoring

- Ensure you have followed all [Performance best practices](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} in the _Adobe Commerce Storefront_ documentation.
- (Optional) Configure Google Analytics and Google Tag Manager.
- Validate your [storefront events](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger)
  implementation and ensure that data is displayed in your Live Search and Product
  Recommendation dashboards in the Adobe Commerce Admin.
- Ensure that the `environment` analytics config parameter is set appropriately in your [Commerce configuration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"}. It should be set to `"Testing"` when you are developing your storefront, and `"Production"` when you are ready to deploy your storefront. See [Analytics instrumentation](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"} for more information.
- Ensure that the site's Lighthouse score is green; targeting `100` on every page (taking into
  account previous considerations mentioned in this document).

### Security and access

- Verify that you have configured permissions for DA content and EDS sites. See [DA.live permissions](https://da.live/docs/administration/permissions) and [authentication setup for authoring](https://www.aem.live/docs/authentication-setup-authoring).
- Ensure that the product visuals integration has been provisioned. See [AEM Cloud Service access overview](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#).
- Verify/update password reset links. Match the Edge Delivery Services implementation in the Adobe Commerce Admin. See [What should I do if my email template links are broken after migrating to Edge Delivery Services or Helix?](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"} in the storefront FAQ.
- Provide and configure production keys for integrations and payment providers.
- Verify that the new domains/subdomains are `allowlisted` and potential backend webhooks are working.

### CDN and caching

- Update your CDN configuration with your production GraphQL endpoint (`yourproject.com/graphql`). Use that endpoint for all Sidekick extensions and scripts (for example, sitemap generation and the image importer).
- Request a new CDN purge token for the Adobe Commerce production environment when you use Adobe Commerce Fastly. Update your [site configuration](https://tools.aem.live/tools/cdn-setup/index.html) with the `authToken` and `serviceId` values.
- Validate your [CDN configuration](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"} and ensure that caching
  and cache invalidation work as expected.
- Add a store-specific cache buster to the Catalog Service and Live Search requests for [multi-store setups](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"} (for example, a query parameter or proxy through your CDN configuration).
- Push invalidation is set up and tested (publish a change, then verify on the production domain).
- DNS TTL is reduced to the minimum before cutover.
- DNS A/CNAME records are updated for all domains and hostnames.
- SSL/TLS certificate is provisioned and verified for the production domain.
- `www` ↔ apex redirects work correctly.

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

## Analytics and monitoring

- **RUM:** Real Use Monitoring (RUM) is instrumented for before/after launch comparison.
- **Analytics:** Adobe Experience Platform data collection is configured (if applicable).
- **Analytics:** Martech stack tags fire correctly on the production hostname.
- **Analytics:** Analytics baselines are documented — expect metric shifts post-launch (pageviews, bounce rate, and so on).
- **Events:** Conversion tracking is verified end-to-end (add-to-cart → checkout → confirmation).

## Testing

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

## Launch day and post-launch support

-  Adobe has been informed of the launch day. Mail is sent to Adobe CTA.
- Support: P1 hotline number is recorded: US (+1) 800 497 0335 — press 6 for Commerce.
- Support: Support ticket process is understood — file a ticket **first**, then call the P1 hotline.
- Post-launch: verify Lighthouse score on the production domain.
- Post-launch: monitor Google Search Console for indexing and crawl errors.
- Post-launch: monitor the 404 report and add redirects for high-traffic legacy URLs.
- Post-launch: martech and analytics data are flowing correctly on production.
- Post-launch: notify CTA/CSE/AM to activate High SLA monitoring.
- Disaster recovery plan is documented and tested.
- Track and update to the latest boilerplate and extension packages versions
