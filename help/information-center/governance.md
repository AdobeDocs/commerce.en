---
title: Commerce Information Center Governance
description: Learn about the internal governance model for the Commerce Information Center. Not published to Experience League.
---

# Commerce Information Center governance

This internal reference for the documentation team is not listed in `TOC.md`, so it is not published to Adobe Experience League.

## Ownership

The Adobe Commerce documentation team owns the Information Center. It is authored in `Adobe-Enterprise-Docs/commerce.en`, the repository listed as `git-repo` in `metadata.md`.

No single product team owns it because it is cross-product. Escalate product-specific corrections to the owning product team's docs contact instead of fixing them here.

## What belongs in the Information Center

| Belongs here | Belongs in the product repo |
| --- | --- |
| Content that spans more than one product or service, such as product selection guidance, cross-product implementation journeys, architecture patterns, and white papers | Single-product content, such as step-by-step configuration, API/CLI/config reference, and troubleshooting |
| Short curation pages that link to authoritative product docs | |

- If a page here accumulates single-product detail, move it to the product guide and link to it.
- The Information Center does not consolidate or migrate product documentation, and it does not document individual product features. Link to existing authoritative content before writing something new.

## Adding new content

### Articles in an existing section

1. Add the file to the folder that matches the section.
1. Add an entry to `TOC.md` under that section.

No approval is required beyond normal PR review.

| TOC section | Folder |
| --- | --- |
| Explore Commerce platforms and services | `portfolio/`, `storefronts/`, `aem-assets/`, `apis/` |
| Get started by role | `get-started/` |
| Insights and guidance | `guidance-insights/` |
| Architecture | `architecture-options/` |
| Migration and adoption | `migration-adoption/` |
| Implementation guides | `implementation-guides/` |

### Insights and guidance articles

1. Copy `whitepaper-template.md` or `security-guidance-template.md` from `templates/` into `guidance-insights/`. The templates are not published.
1. Delete the template's placeholder comments.
1. Add a `TOC.md` entry under Insights and guidance when the content is ready to publish.

### Top-level sections

A new top-level group in `TOC.md` changes the guide's navigation, so it requires IA review. Contact whoever owns Commerce IA review. Reuse an existing section first, such as Get started by role for partner or enablement content.

### Published URLs

URLs are built from the guide ID, the section IDs in `TOC.md` (for example, `{#insights-and-guidance}`), and the file name. Folder names do not appear in the URL. Give each section a unique ID, and make sure no two articles resolve to the same URL.

## Review cadence

- **Event-driven**—review the Explore Commerce platforms and services, Get started by role, Architecture, Migration and adoption, and Implementation guides sections when a Commerce product is renamed, launched, or deprecated, or its availability changes. For example, review them if Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer gain an integration. These pages become outdated first.
- **Scheduled**—to catch outdated terminology, branding, or technical inaccuracies, run an automated content audit and review every six months.

## Relationship to help/landing/

`help/landing/` ("Adobe Commerce Services Guides") is a separate guide that is not part of the Information Center. It focuses on Commerce services like Catalog Service, Live Search, Product Recommendations, and Payment Services, and the Information Center links to it for details. Rescoping or consolidating the two is a follow-up decision that this guide does not resolve.
