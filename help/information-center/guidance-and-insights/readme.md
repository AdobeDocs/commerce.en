---
title: Insights and Guidance Governance
description: Learn about the internal governance model for Insights and guidance. Not published to Experience League.
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
---

# Insights and guidance governance

This is an internal reference for the documentation team. It is not listed in `TOC.md`, so it is not built or published to Experience League. Keep it here so it stays close to the content it governs. For the governance of the Information Center as a whole, see [governance.md](../governance.md).

## Ownership

Insights and guidance articles are owned by the publishing author or team who is responsible for maintaining the article accuracy and currency. These articles are currently hosted in the `commerce.en` repository. The Commerce Documentation team assists with ensuring content quality and publishing the article to production.

## What belongs in Insights and guidance

- **Belongs here**—Strategic guidance and whitepapers for Commerce Solutions that cover implementation guidance based on real world scenarios. Include links to relevant Commerce documentation pages for support.

- **Belongs in the product repo instead**—step-by-step configuration, tutorials, reference material (API/CLI/config reference), and troubleshooting. If a post here starts accumulating that kind of detail, move it to the relevant product guide and link to it instead.

## Adding new content

Create a COMDOX JIRA ticket for the article to be published. Copy `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)` into the ticket description and fill it in—it asks the requester to identify the audience, flag whether the content is temporary (with an expiration date), and confirm that it belongs in Insights and guidance, and not in the Commerce product documentation.

Once the ticket is scoped, start the article from a template in `templates/` (`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`—not published, copy the relevant one into the target file and delete the template's own frontmatter placeholder comments). Add an entry to `help/information-center/TOC.md` under Insights and guidance once the content is ready to publish.

- **New top-level section** (for example, Insights > Catalog Management) requires IA review before adding, since it changes the guide's navigation shape. Loop in whoever owns Commerce IA review for the story or task.

- **Add to TOC**—Add the new topic to the TOC before publishing. If needed, use hide metadata to publish a hidden article accessible only to people who have the link. See [Hiding content](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files) in the ExL Author's Guide.

## Review cadence

Review article content when new Commerce Solutions are renamed or updated, or insights are no longer relevant.
