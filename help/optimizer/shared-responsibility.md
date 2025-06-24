---
title: Shared Responsibility
description: Learn about the security responsibilities of each party involved in your [!DNL Adobe Commerce Optimizer] project.
role: Admin, Architect, Leader
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Shared responsibility security and operational model

>[!BEGINSHADEBOX]

The following summary tables use the RACI model to show the security responsibilities shared between Adobe and customers.

**R** — Responsible
**A** — Accountable
**C** — Consulted
**I** — Informed

>[!ENDSHADEBOX]

| Task | Adobe | Customer |
| --- | --- | --- |
| Applying Adobe Commerce infrastructure patches | RA | |
| Applying patches to supporting services | RA | |
| Defining backend origin WAF rules | RA | |
| Defining backend CDN WAF rules | RA | |
| Deploying backend platform WAF rules | RA | |
| Deploying backend CDN WAF rules | RA | |
| Fixing bugs in [!DNL Adobe Commerce Optimizer]| RA | I |
| Releasing [!DNL Adobe Commerce Optimizer]infrastructure patches | RA | |
| Scaling (infrastructure) | RA | I |
| Integrating external applications | | RA |
| Installing App Builder apps | | RA |
| Testing performance of all App Builder apps | | RA |
| Theming and design of custom App Builder apps | | RA |
| Configuring backend DNS | RA |  |
| Onboarding backend CDN | RA |  |
| Supporting backend CDN | RA |  |
| Obtaining a backend DNS provider | RA | |
| Provisioning the production and sandbox environments | A | R |
| Accessing Dynamics for Adobe Commerce Optimizer | R | C |
| Resolving backend Customer security issues | RA | I |
| Resolving backend CDN security issues | RA | |
| Assisting Adobe with security research (scans/audits) | RA | |
| Performing PCI ASV scans | RA | I |
| Remediating Adobe Commerce Optimizer infrastructure PCI scans | R | |
| Managing OS and platform secrets | RA | |
| Monitoring backend security logs | RA | |
| Controlling Customer support and access | A | R |
| Annual testing and documentation of Adobe DR plan and backup and restore | RA | |
| Annual testing and documentation of disaster recovery plan | RA | |
| Debugging and issue isolation | R | R |
| Timely support of debugging and issue isolation process | R | R |
| Installing updates and patches to Adobe Commerce Optimizer | RA | I |
| Core Adobe Commerce Optimizer Application Quality | RA | |
