---
title: View and manage logs
description: Learn where to find and manage logs for the AEM Assets Integration for Commerce.
feature: CMS, Media, Integration
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
---
# View and manage logs

The AEM Assets integration provides the following log files in your Commerce instance:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Ask your System Administrator to check the log file rotation schedule for these logs to prevent them from growing too large. In some environments, logs rotate automatically; in others, you must configure log rotation manually.  For details, see the following topics:

- For Adobe Commerce on-premises installations, ask your System Administrator to set up [log rotation](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings).
- For Adobe Commerce on cloud infrastructure projects, see [View and manage logs](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html).
