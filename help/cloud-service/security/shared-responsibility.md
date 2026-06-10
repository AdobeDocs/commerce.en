---
title: Shared responsibility
description: Learn about the security responsibilities of each party involved in your [!DNL Adobe Commerce as a Cloud Service] project.
feature: Cloud, Security
role: Admin, Developer, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
TQID: 'https://experienceleague.adobe.com/ZjR9eFTVz8RIrYIN1CxyEgegGoZljXJKrtWZStx-ln0'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# Shared responsibility security and operational model

[!DNL Adobe Commerce as a Cloud Service] is an on-demand service that relies on a shared responsibility security and operational model. Adobe and customers share these responsibilities, with each party bearing distinct accountability for securing and operating the Adobe Commerce application.  

>[!BEGINSHADEBOX]

The following summary tables use the RACI model to show the security responsibilities shared between Adobe and customers.

**R** — Responsible
**A** — Accountable
**C** — Consulted
**I** — Informed

>[!ENDSHADEBOX]

| Task | Adobe | Customer |
| --- | --- | --- |
| Defining backend origin WAF rules | RA | |
| Defining backend CDN WAF rules | RA | |
| Deploying and maintaining of [!DNL Adobe Developer App Builder] applications | | RA |
| Deploying backend platform WAF rules | RA | |
| Deploying backend CDN WAF rules | RA | |
| Fixing core bugs in [!DNL Adobe Commerce as a Cloud Service] | RA | I |
| Releasing [!DNL Adobe Commerce as a Cloud Service] infrastructure patches | RA | |
| Scaling (infrastructure) | RA | |
| Scaling (core application) | RA | |
| Integrating external applications | | RA |
| Installing App Builder apps | | RA |
| Testing performance of all App Builder apps | | RA |
| Theming and design of custom App Builder apps | | RA |
| Configuring backend DNS | RA | I |
| Onboarding backend CDN | RA | I |
| Supporting backend CDN | RA | I |
| Obtaining a backend DNS provider | RA | |
| Provisioning the production and sandbox environments | A | R |
| Accessing Dynamics for Adobe Commerce on cloud infrastructure | R | C |
| Resolving backend Customer security issues | RA | I |
| Resolving backend CDN security issues | RA | |
| Assisting Adobe with security research (scans/audits) | RA | |
| Performing PCI ASV scans | RA | I |
| Remediating Adobe Commerce infrastructure PCI scans | R | |
| Managing OS and platform secrets | RA | |
| Monitoring backend security logs | RA | |
| Controlling Customer support and access | A | R |
| Annual testing and documentation of Adobe DR plan and backup and restore | RA | |
| Annual testing and documentation of disaster recovery plan | RA | |
| Debugging and issue isolation | R | R |
| Timely support of debugging and issue isolation process | R | R |
| Publishing updates and patches to Adobe Commerce core | RA | I |
| Installing updates and patches to Adobe Commerce core | RA | I |
| Core Adobe Commerce Application Quality | RA | |
