---
title: Shared Responsibility
description: Learn about the security responsibilities of each party involved in your [!DNL Adobe Commerce Optimizer] project.
role: Admin, Developer, Leader
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and [!DNL Adobe Commerce Optimizer] projects only (Adobe-managed SaaS infrastructure)."
exl-id: 9e09790f-832d-43ab-b2df-6389ad52b43d
TQID: https://experienceleague.adobe.com/lOn0WJYdUi5qMX7OlRKeNAIc-TA29OFWWSqN3yQzt30
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
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
| Accessing Dynamics for [!DNL Adobe Commerce Optimizer] | R | C |
| Resolving backend Customer security issues | RA | I |
| Resolving backend CDN security issues | RA | |
| Assisting Adobe with security research (scans/audits) | RA | |
| Performing PCI ASV scans | RA | I |
| Remediating [!DNL Adobe Commerce Optimizer] infrastructure PCI scans | R | |
| Managing OS and platform secrets | RA | |
| Monitoring backend security logs | RA | |
| Controlling Customer support and access | A | R |
| Annual testing and documentation of Adobe DR plan and backup and restore | RA | |
| Annual testing and documentation of disaster recovery plan | RA | |
| Debugging and issue isolation | R | R |
| Timely support of debugging and issue isolation process | R | R |
| Installing updates and patches to [!DNL Adobe Commerce Optimizer] | RA | I |
| Core [!DNL Adobe Commerce Optimizer] Application Quality | RA | |
