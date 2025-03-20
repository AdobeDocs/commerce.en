---
title: Shared responsibility
description: Learn about the security responsibilities of each party involved in your [!DNL Adobe Commerce as a Cloud Service] project.
role: Admin, Architect, Leader
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
---
# Shared responsibility security and operational model

{{accs-note}}

[!DNL Adobe Commerce as a Cloud Service] is an on-demand service that relies on a shared responsibility security and operational model. These responsibilities are shared between Adobe and customers. Each party bears distinct responsibility for securing and operating the Adobe Commerce application.  

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
| Applying patches to supporting services (for example, Nginx or MySQL) | RA | |
| Defining backend origin WAF rules | RA | |
| Defining backend CDN WAF rules | RA | |
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
