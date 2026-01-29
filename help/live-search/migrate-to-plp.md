---
title: Migrating from Search Adapter to PLP Widget
description: Learn how to migrate from the deprecated Search Adapter to the [!DNL Live Search] Product Listing Page Widget.
---
# Migrating from Search Adapter to PLP Widget

The Search Adapter has been [deprecated](release-notes.md#live-search-400) as of [!DNL Live Search] 4.0.0 and will only receive security updates. The [Product Listing Page (PLP) Widget](plp-styling.md) is the supported solution for all [!DNL Live Search] implementations going forward. This guide helps you understand when migration is straightforward and when additional work is required.

## Migration scenarios

### Straightforward migration (no additional work required)

You can migrate directly to the PLP widget if your implementation meets ALL of the following criteria:

**Standard Luma-based storefront:**

- Using the Luma theme or a theme that inherits from Luma with minimal customizations
- No custom modifications to product listing page layouts or templates
- No custom JavaScript extensions that interact with search results

**Standard product catalog:**

- All product attributes use standard source models (not custom source models)
- No custom product types requiring special rendering logic
- Standard facets and filtering only

**Standard integrations:**

- Not using Google Tag Manager (GTM) for analytics
- Not using third-party extensions that modify search behavior
- Using default Adobe Commerce storefront (not headless)

**Version compatibility:**

- Running Adobe Commerce 2.4.4 or newer
- Ready to upgrade to [!DNL Live Search] 4.0.0 or higher

If your implementation matches these criteria, proceed to [Standard migration steps](#standard-migration-steps).

### Migration requiring additional work

Additional work is required if your implementation has ANY of the following:

**Custom theme modifications:**

- Custom product listing page layouts that override Luma templates
- Custom CSS or JavaScript that targets search adapter-specific elements
- Custom template modifications to product listing pages or related files
- Theme does not inherit from Luma (for example, custom theme from scratch)

**Custom product attributes:**

- Product attributes with custom source models used as facets
- Custom product types with special display requirements
- Programmatic attributes with `"is_user_defined": false`

**Advanced integrations:**

- Google Tag Manager (GTM) is actively used for tracking
- Third-party analytics or personalization tools integrated with search
- Custom event tracking or data layer implementation
- Integration with external search or recommendation engines

**Headless or PWA implementations:**

- Using headless architecture (for example, PWA Studio, Vue Storefront)
- Custom frontend framework (React, Vue, Angular)
- Using GraphQL exclusively for catalog queries
- Custom storefront events implementation

**Custom widget code:**

- Previously customized the Search Adapter code
- Hosting custom versions of widgets on your own CDN
- Custom JavaScript extensions for search functionality

If your implementation has any of these scenarios, see [Complex migration scenarios](#complex-migration-scenarios).

## Prerequisites

Before starting migration:

**Technical requirements:**

- Adobe Commerce 2.4.4 or higher
- [!DNL Live Search] extension installed
- Access to the command line (CLI)
- Access to the Commerce Admin
- Staging or QA environment for testing

**Backup and preparation:**

1. Back up your database and code.
1. Document current customizations.
1. Review [Boundaries and Limits](boundaries-limits.md) to ensure that the PLP widget meets your needs.
1. Schedule migration during a low-traffic period.
1. Notify stakeholders of potential changes to storefront behavior.

**Review the current implementation:**

- Check your current [!DNL Live Search] version: `composer show magento/live-search`
- Document which facets are in use and their configuration
- Test all search functionality and document expected behaviors
- Capture screenshots of current search results presentation

## Standard migration steps

For implementations with no special customizations, follow these steps:

### Step 1: Upgrade [!DNL Live Search]

**Role**: Merchant or Partner

1. Check your current [!DNL Live Search] version:

   ```bash
   composer show magento/live-search | grep version
   ```

1. If on version 3.x or earlier, enable the AdvancedSearch module before upgrading:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

1. Update `composer.json` to require [!DNL Live Search] 4.0 or higher:

   ```json
   "require": {
      "magento/live-search": "^4.0"
   }
   ```

1. Run the upgrade:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Run setup upgrade and recompile:

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   ```

1. Deploy static content, if needed:

   ```bash
   bin/magento setup:static-content:deploy
   ```

### Step 2: Enable the PLP widget

**Role**: Merchant

The PLP widget is enabled by default for new installations of [!DNL Live Search] 4.0.0+. If upgrading from an earlier version:

1. Go to **Stores** > Settings > **Configuration**.
1. Navigate to **Live Search** > **Storefront Features**.
1. Expand the **Storefront Features** section.
1. Set **Enable Product Listing Widgets** to **Yes**.
1. Click **Save Config**.
1. Flush the cache: **System** > Tools > **Cache Management** > **Flush Magento Cache**.

### Step 3: Test on staging

**Role**: Merchant/Partner

Before deploying to production, thoroughly test the search functionality:

**Functional testing:**

- Verify that search results appear correctly
- Test all configured facets
- Verify category navigation works
- Test pagination through results
- Verify that sort options work as expected
- Test add-to-cart functionality for simple products

**Visual testing:**

- Confirm that product images display correctly
- Verify product names and prices render properly
- Test color swatches (if used)
- Check responsive behavior on mobile devices
- Verify that styling matches your brand

**Performance testing:**

- Measure page load times
- Test with realistic catalog size
- Monitor server resource usage
- Check the browser console for JavaScript errors

### Step 4: Deploy to production

**Role**: Merchant/Partner

1. Schedule deployment during the maintenance window if possible.
1. Follow your standard deployment process.
1. Enable the PLP widget in production using Step 2.
1. Monitor for any issues immediately after deployment.
1. Have a rollback plan ready if critical issues arise.

### Step 5: Validate and monitor

**Role**: Merchant

After deployment, monitor key metrics:

- Zero-results search rate
- Search-to-cart conversion rate
- Page load performance
- Customer feedback or support tickets
- JavaScript errors in browser console

## Complex migration scenarios

### Custom theme with layout modifications

In this scenario, you have custom templates or layouts that override the default product listing behavior.

**Role**: Developer/Partner

1. **Audit customizations:**
   - Document all custom layout XML files in your theme
   - Review any Custom template modifications to product listing pages or related files
   - Identify custom CSS classes used for styling
   - Document custom JavaScript interactions

1. **Migrate to CSS-based customizations:**
   - The PLP widget uses specific CSS classes (see [PLP styling guide](plp-styling.md))
   - Recreate visual customizations using PLP widget CSS classes
   - Test that custom styles apply correctly

1. **Remove conflicting customizations:**
   - Remove layout XML that modifies the product listing structure
   - Clean up JavaScript that targets search adapter-specific elements
   - Update template overrides that conflict with widget rendering

1. **Test thoroughly:**
   - Verify all visual customizations work with the PLP widget
   - Ensure no layout conflicts
   - Test across all breakpoints and devices

### Product attributes with custom source models

In this scenario, you have facets that use product attributes with custom source models that are not supported by the Search Adapter but ARE supported by the PLP widget.

**Role**: Merchant (Admin configuration)

1. **Identify affected attributes:**
   - Review product attributes used as facets
   - Identify which use custom source models
   - Document current facet configuration

1. **Upgrade and enable the PLP widget:**
   - Follow [Standard migration steps](#standard-migration-steps)
   - The PLP widget supports custom source model attributes

1. **Reconfigure facets:**
   - Go to **Marketing** > SEO & Search > **Live Search**
   - Review facet configuration for affected attributes
   - Test facets work correctly with custom source models

1. **Validate:**
   - Test filtering with custom source model facets
   - Verify that all attribute values appear correctly
   - Ensure that performance is acceptable

### Google Tag Manager (GTM) integration

In this scenario, there is a known issue where enabling the PLP widget can cause GTM to fail.

**Role**: Developer/Partner + Customer Engineering

**Option 1: Continue with Search Adapter (interim only)**

- Keep Search Adapter enabled if GTM is business-critical
- Understand you will only receive security updates
- Plan to migrate when GTM compatibility is resolved
- Contact Adobe Support for updates on GTM compatibility

**Option 2: Migrate GTM tracking to an alternative approach**

1. **Implement a custom event collection:**

   - Use the [Storefront Events SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/)
   - Capture search and product interaction events
   - Push events to the GTM data layer manually

1. **Steps:**
   - Audit current GTM tracking requirements
   - Map GTM events to Storefront Events
   - Implement custom event listeners
   - Test data flow to GTM
   - Validate analytics reports

**Option 3: Replace GTM with Adobe Analytics**

- Consider migrating to Adobe Analytics if applicable
- Contact Customer Engineering for guidance

**Who to contact:** Submit a support ticket for GTM compatibility updates or Customer Engineering assistance.

### Scenario: Headless or PWA implementation

In this scenario, you have a headless or PWA storefront that requires custom event collection and cannot use the standard PLP widget UI.

**Role**: Developer/Partner

1. **Review reference implementations:**
   - Study the [PLP widget source code](https://github.com/adobe/storefront-product-listing-page)
   - Review API documentation for [[!DNL Live Search] GraphQL](graphql.md)
   - Understand the [Catalog Service queries](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)

1. **Implement a custom UI:**
   - Use [!DNL Live Search] GraphQL API for queries
   - Build custom product listing components
   - Implement the UI for faceting
   - Handle pagination and sorting

1. **Implement event collection:**
   - Review [Storefront Events documentation](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)
   - Implement the required events:
     - `search-request-sent`
     - `search-response-received`
     - `search-results-view`
     - `product-page-view`
     - `add-to-cart`
   - Test event data flows to Adobe Commerce

1. **Configure facet sorting:**
   - For headless implementations, facets can be sorted by count
   - Configure in **Live Search** > **Facets** workspace
   - Set **Sort Type** to **Count** for better UX

1. **Test and validate:**
   - Verify search results accuracy
   - Test facet functionality
   - Confirm that events are tracked correctly
   - Monitor performance metrics
   - Validate intelligent merchandising features work

### Scenario: Custom widget code modifications

In this scenario, you have previously customized the Search Adapter or widget code and need to migrate customizations.

**Role**: Developer/Partner

1. **Document existing customizations:**
   - List all customizations made to Search Adapter
   - Identify the business requirements driving each customization
   - Determine if customizations are still needed

1. **Check if the built-in features meet your needs:**
   - Review [PLP widget features](plp-styling.md#widget-features)
   - Check if CSS-based customization is sufficient
   - Test default PLP widget behavior

1. **If custom code is still needed:**
   - Clone the [PLP widget repository](https://github.com/adobe/storefront-product-listing-page)
   - Implement your customizations
   - Host on your own CDN
   - Update Commerce configuration to use your custom widget

   >[!WARNING]
   >
   >If you customize the PLP widget using code from the repository, you are responsible for maintenance and updates. New PLP widget features from Adobe might be incompatible with your customizations.

1. **Test thoroughly:**
   - Test all custom functionality
   - Verify that Commerce updates do not break customizations
   - Document your custom implementation
   - Plan for ongoing maintenance

## Known limitations and edge cases

Be aware of these limitations when migrating:

**PLP widget limitations:**

- **Sort order direction:** When the PLP widget is enabled, the sort order direction on product listing pages cannot be changed (ascending/descending).
- **Add to cart:** Add to cart buttons are only available for simple products in the widget.
- **Tier pricing:** Not supported in the PLP widget.
- **VAT display:** Prices include VAT, but VAT cannot be displayed as a separate value.

**Feature differences from Search Adapter:**

- **Color swatches:** The `color` attribute must be spelled exactly as `color` (not "colour" or custom names) for swatches to work properly.
- **Theme styling:** Custom theme classes are not inherited by the widget; must target widget-specific CSS classes.
- **Custom product types:** Not supported in the widget.

**Performance considerations:**

- Large catalogs (50,000+ products) may experience longer initial page loads
- Multiple facets with many values can impact performance
- Mobile device performance may vary based on catalog size

**Compatibility issues:**

- Google Tag Manager compatibility issue (see [GTM scenario](#scenario-google-tag-manager-gtm-integration))
- Some third-party extensions may conflict with the PLP widget
- Custom checkout extensions may need updates

## Getting help

**Adobe Support** can assist with:

- Standard Live Search migration procedures
- PLP widget configuration issues
- Facet or attribute indexing problems
- Performance issues with default implementations
- Upgrade errors

**Development partners/systems integrators** should be contacted for:

- Custom theme modifications
- Custom widget code implementations
- Third-party extension compatibility
- Headless or PWA implementations
- Custom event tracking

To contact Adobe Support, see the [Help Center User Guide](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

## FAQ

**Q: Will the Search Adapter receive bug fixes or feature updates?**

A: No. The Search Adapter is deprecated and will only receive security updates. Bug fixes, performance improvements, and new features are only available in the PLP widget. If you encounter issues with the Search Adapter, migration to the PLP widget is the recommended solution.

**Q: Will migration disrupt my storefront?**

A: If you follow proper testing procedures in staging, migration should be seamless. Have a rollback plan ready for production deployment.

**Q: How long does migration take?**

A: For standard implementations: 1-2 hours. For custom implementations: 1-4 weeks depending on complexity.

**Q: Will my search merchandising rules still work?**

A: Yes, all search merchandising rules, synonyms, and facets configured in the [!DNL Live Search] workspace continue to work with the PLP widget.

**Q: Do I need to reconfigure my facets?**

A: Generally no, but if you were limited by custom source model attributes with the Search Adapter, you can now use them with the PLP widget.

**Q: What about my custom CSS?**

A: You need to update CSS to target the PLP widget classes. See the [CSS classes reference](plp-styling.md#css-classes).

**Q: Will this affect my search performance?**

A: The PLP widget is designed to be performant. Most merchants see equal or better performance. Large catalogs should be tested in staging.
