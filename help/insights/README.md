---
title: Commerce Information Center Governance
description: Learn about the internal governance model for the Commerce Information Center. Not published to Experience League—kept out of TOC.md intentionally.
---

# Commerce Documentation governance

This is an internal reference for the documentation team. It is not listed in `TOC.md`, so it is not built or published to Experience League. Keep it here so it stays close to the content it governs.

## Ownership

Commerce Insights articles are owned by the publishing author or team who is responsible for maintaining the article accuracy and currency. These articles are currently hosted in the `commerce.en` repository (see `git-repo` in `metadata.md`). The Commerce Documentation team assists with ensuring content quality and publishing the article to production.

## What belongs in Commerce Insights

- **Belongs here**: Strategic guidance and whitepapers for Commerce Solutions that covers security, implementation guidance based on real world scenarios. Include links to relevant Commerce documentation pages for support.

- **Belongs in the product repo instead**: step-by-step configuration, tutorials,reference material (API/CLI/config reference), and troubleshooting, If a post here starts accumulating that kind of detail, move it to the relevant product guide and link to it instead.

## Adding new content

Create a COMDOX JIRA ticket for the article to be published. Copy `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)` into the ticket description and fill it in—it asks the requester to identify the audience, flag whether the content is temporary (with an expiration date), and confirm the content doesn't belong in Commerce product documentation instead.

Once the ticket is scoped, start the article from a template in `templates/` (`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`—not published, copy the relevant one into the target file and delete the template's own frontmatter placeholder comments). Add a `TOC.md` entry once the content is ready to publish.

- **New top-level section** (for example, Insights > Catalog Management) requires IA review before adding, since it changes the guide's navigation shape. Loop in whoever owns Commerce IA review for the epic.

- **Add to TOC** - Add new topic to the TOC before publishing.

## Review cadence

Review article content on a when new Commerce Solutions are renamed or updated, or insights are no longer relevant.

## Relationship to help/landing/

`help/landing/` ("Adobe Commerce Services Guides") is a separate, pre-existing guide and is out of scope for this build. Its content is scoped narrowly to Catalog Service/Live Search/Product Recommendations-style services and doesn't reflect ACCS or ACO. Rescoping or consolidating it with the Information Center is a follow-up decision, not something this guide's governance model resolves.




New Guidance & Insights content type (white paper, security guidance, best practice, etc.): start from a template in templates/ (whitepaper-template.md, security-guidance-template.md—not published, copy the relevant one into the target file and delete the template's own frontmatter placeholder comments). Add a TOC.md entry once the content is ready to publish.