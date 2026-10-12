---
title: Commerce Information Center Governance
description: Learn about the internal governance model for the Commerce Information Center. Not published to Experience League—kept out of TOC.md intentionally.
---

# Commerce Information Center governance

This is an internal reference for the documentation team. It is not listed in `TOC.md`, so it is not built or published to Experience League. Keep it here so it stays close to the content it governs.

## Ownership

The Commerce Information Center is owned by the Adobe Commerce documentation team. It is currently hosted in the `commerce.en` repository (see `git-repo` in `metadata.md`). There is no dedicated owning product team, since the Information Center is explicitly cross-product—escalate product-specific corrections to the owning team's docs contact instead of fixing them here.

## What belongs in the Information Center vs. a product repo

- **Belongs here**: content that spans more than one Commerce product or service (product selection guidance, cross-product implementation journeys, architecture patterns, strategic guidance/white papers), and short curation pages that point to authoritative product docs.
- **Belongs in the product repo instead**: step-by-step configuration, reference material (API/CLI/config reference), troubleshooting, and anything else scoped to a single product. If a page here starts accumulating that kind of detail, move it to the relevant product guide and link to it instead.
- Per COMDOX-1756 Phase 1 scope: this guide does not consolidate or migrate existing product documentation, and does not introduce new feature documentation. New sections should default to linking to existing authoritative content before authoring something new.

## Adding new content

- **New Implementation guide or Architecture center page**: add the file under the relevant subdirectory and add an entry to `TOC.md`. No approval gate beyond normal PR review.
- **New Guidance & Insights content type** (white paper, security guidance, best practice, etc.): start from a template in `templates/` (`whitepaper-template.md`, `security-guidance-template.md`—not published, copy the relevant one into the target file and delete the template's own frontmatter placeholder comments). Add a `TOC.md` entry once the content is ready to publish.
- **New top-level section** (e.g. Partner Resources, Learning Center, Support & Resources from the full COMDOX-1756 IA): requires IA review before adding, since it changes the guide's navigation shape. Loop in whoever owns Commerce IA review for the epic.

## Review cadence

Review the Products and Get Started sections whenever a Commerce product is renamed, launched, or deprecated (for example, the ACCS/ACO launches that originally prompted this epic)—these pages are the most likely to go stale first. There's no fixed recurring review scheduled yet; add one here once a cadence is agreed with the docs team lead.

## Relationship to help/landing/

`help/landing/` ("Adobe Commerce Services Guides") is a separate, pre-existing guide and is out of scope for this build. Its content is scoped narrowly to Catalog Service/Live Search/Product Recommendations-style services and doesn't reflect ACCS or ACO. Rescoping or consolidating it with the Information Center is a follow-up decision, not something this guide's governance model resolves.
