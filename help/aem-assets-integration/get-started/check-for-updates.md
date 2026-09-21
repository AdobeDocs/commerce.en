---
title: Check for Extension Updates
description: Learn how Adobe Commerce checks for and notifies administrators about new AEM Assets Integration extension versions, including the manual CLI check.
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
---
# Check for extension updates

As of AEM Assets Integration extension version 1.4.6, Adobe Commerce can automatically check if a newer version of the extension is available and notify administrators in the Admin. This check runs asynchronously as part of scheduled processing and does not block Admin page rendering.

## How the update check works

* The checker compares your installed `aem-assets-integration` package version against the highest compatible version available from [repo.magento.com](https://repo.magento.com/admin/dashboard).
* Results are cached. Loading an Admin page reads the most recent cached result rather than triggering a live network request.
* If `repo.magento.com` is unavailable, or the returned metadata is invalid, Commerce keeps the last successful cached result and does not block the Admin.

>[!NOTE]
>
>_[Cloud Service availability TBD]_ — The update checker is intended for Adobe Commerce on Cloud and on-premises deployments. Whether it is available or suppressed on Adobe Commerce as a Cloud Service is not yet confirmed.

## View update notifications

Administrators can see an available update notification in either location:

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* The Admin notification dropdown

Each notification displays:

* The installed version
* The available version
* The release classification
* A link to the release notes

Select **[!UICONTROL Remind me later]** to snooze the notification for this Commerce instance, or opt out of update notifications entirely.

## Run a manual update check

To check for an available update immediately, run the following command from the Commerce root directory:

```bash
bin/magento aem:assets:check-update
```

This command only checks for and reports an available update. It does not modify Composer files or deploy an update. To install an update, follow the Composer instructions in [Install Adobe Commerce packages](configure-commerce.md).

## Release metadata for extension packages

The update checker reads release metadata from the `extra` section of the installed package's `composer.json` file:

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## Next step

* [Install Adobe Commerce packages](configure-commerce.md)
