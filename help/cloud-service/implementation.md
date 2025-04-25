---
title: Implementation
description:
role: Developer
---

# Comparison: SaaS vs PaaS

| Feature | SaaS model | PaaS model |
|---------|------------|------------|
| Customizable Admin theme | Not supported (Admin UI theming not available) | Supported (via extensible admin theming framework) |
| Extensible core Admin screens | Limited control / extension points (e.g., preset filters, visibility controls) | Full control over layout and functionality |
| Extensible new Admin screens | Supported via external app injection (Admin UI SDK) | Supported via standard admin UI |
| In-process execution customization | Out-of-process only (App Builder, microservices-based) | Supported (native extensibility framework) |
| B2B functionality | Supported (pre-installed with core B2B features)* | Supported |
| Data model extensibility | Supported via custom attributes for core and B2B entities** | Full control of data model |
| Search index customizations | Not supported (requires 3rd party) | Supported |
| Custom (new use case) email types | Not supported | Supported |
| Custom data storage | Limited (state-lib, file only, App Builder storage limitations***) | Supported (DB, file, cache, queue) |
| Primary technologies | CSS, HTML, JS, Node, CLI | PHP, XML, HTML, CSS, JS, CLI |
| Extensible web APIs | Limited (API Mesh with custom resolvers can extend functionality****) | Supported (native REST/GraphQL extensibility) |

\* Note: Core B2B features like company management and quoting are available out-of-the-box in SaaS. However, industry-specific customizations may require additional implementation considerations.

\** Note: Data model extensibility in SaaS supports extending core entities beyond just product and customer, including B2B entities. However, industry-specific data models (e.g., dealer-specific attributes) may require additional architectural considerations.

\*** Note: For SaaS model's App Builder storage limitations, Adobe is actively working on solutions including Document DB integration to address persistent storage needs. Currently, implementations requiring long-term data storage may need to provision and maintain additional infrastructure.

\**** Note: While direct extension of REST and GraphQL APIs is limited in SaaS, API Mesh can be used to modify schemas and add custom resolvers to augment the out-of-box APIs.

For future readiness when considering SaaS migration, it's recommended to:

1. Move suitable functionality to out-of-process implementations where possible
2. Reduce the surface area that would need transition
3. Consider API Mesh for extending API functionality
4. Monitor Adobe's ongoing platform evolution and new capability releases
5. Evaluate industry-specific data model requirements against available extensibility options

