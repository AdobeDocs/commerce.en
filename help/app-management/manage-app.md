---
title: Manage your app
description: Associate, install, configure, upgrade, and unassociate App Builder applications with your Commerce instance.
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
---

# Manage your app

Use [!DNL App Management] to associate, install, configure, upgrade, and unassociate App Builder applications with your Commerce instance. Configuration forms are generated from each app's schema, so you can manage settings without custom Admin UI development.

![App management](assets/app-management-view.png){width="500" zoomable="yes"}

## Find an application in the Admin

Under **[!UICONTROL Apps]** > **[!UICONTROL App Management]**, each application appears as a card. The list can include every app associated with the Adobe Commerce instance for the selected Adobe IMS organization. Use the controls above the cards to narrow results:

| Control | Description |
| --- | --- |
| **[!UICONTROL Filter by app...]** | Search by application name. |
| **[!UICONTROL Status]** | Limit cards by lifecycle state. **[!UICONTROL All Statuses]** shows every app; other values include **[!UICONTROL Associated]**, **[!UICONTROL Installed]**, **[!UICONTROL Partially Installed]**, and **[!UICONTROL Unassociated]**. The status on each card matches the colored indicator in the list. |
| **[!UICONTROL Extensibility patterns]** | Limit cards by the capabilities the app uses. **[!UICONTROL All Extensibility Patterns]** shows every app; other values align with the badges on each card, such as **[!UICONTROL Business Configuration]**, **[!UICONTROL Admin UI SDK]**, **[!UICONTROL Webhooks]**, and **[!UICONTROL Events]**. |

The search field and both filters apply together. To display the full list again, clear the search field and select **[!UICONTROL All Statuses]** and **[!UICONTROL All Extensibility Patterns]**.

### Review application details

On the application's card, select **[!UICONTROL Manage]** > **[!UICONTROL Details]** to review its name, description, and version. The dialog provides two tabs:

* **[!UICONTROL Details]** lists the application's business use cases, including events and custom installation steps. Review the labels and descriptions to understand what the application adds to Commerce.
* **[!UICONTROL App config]** displays the application's configuration as JSON for inspection.

![Details tab showing the application's business use cases](assets/application-details.png){width="600" zoomable="yes"}

![App config tab displaying the application's JSON configuration](assets/app-config.png){width="600" zoomable="yes"}

## Acquire App

**[!UICONTROL Acquire App]** opens a new browser tab (or a separate browser view) to [Adobe Exchange](https://exchange.adobe.com/apps/browse/ec){target="_blank"}, where you can discover Commerce-related marketplace listings and add applications to your Adobe IMS organization. Once the app is acquired, approved, and deployed, the app appears in [!DNL App Management] for [association](#associate-an-app) and [installation](#install-an-app).

## Prerequisites

Before associating an app, ensure you have the following:

| Requirement | Description |
| --- | --- |
| **Admin access** | Commerce Admin with [!DNL App Management] permissions |
| **Deployed app** | App Builder application deployed to your organization and ready to connect |
| **Organization access** | Access to the Adobe organization where the app is deployed |

## Tutorial

Watch this video to learn how to associate an app with a Commerce instance and configure settings.

>[!VIDEO](https://video.tv.adobe.com/v/3478944)

## Associate an app

The association process imports websites, stores, and store views from Commerce and creates the link between the app and your Commerce instance.

To link your App Builder application to a Commerce instance:

1. Navigate to **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

1. Click **[!UICONTROL Associate App]**.

    ![Associate app](assets/associate-app.png){width="500" zoomable="yes"}

1. Select a **[!UICONTROL Project]** from the list.

1. Select the **[!UICONTROL Workspace]**.

1. Click **[!UICONTROL Associate]**.

    ![App details](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>If scope sync fails, association still completes. You can sync the scopes manually later from the **[!UICONTROL Manage Scopes]** view in the configuration of the associated app.

## Install an app

Association links an app to your Commerce instance. For apps that include installable components, such as events, webhooks, Admin UI extensions, or custom installation steps, installation applies those components to the instance.

1. Open the installation dialog for the associated app in [!DNL App Management].

1. Review the application's business use cases and the listed installation steps.

1. If **[!UICONTROL Pre Installation Instructions]** are displayed, complete those prerequisites before proceeding.

    ![Installation review with pre-installation instructions and business use cases](assets/installation-review.png){width="600" zoomable="yes"}

1. Click **[!UICONTROL Install]**.

1. Monitor the progress indicators for individual items until installation finishes.

    ![Installation progress for individual items](assets/installation-progress.png){width="600" zoomable="yes"}

    >[!WARNING]
    >
    >Keep the page open until installation finishes. Closing or refreshing the page might prevent installation from completing correctly.

1. Verify that **[!UICONTROL Successfully Installed]** is displayed and completed items have check marks.

    ![Successful installation with check marks for completed items](assets/installation-success.png){width="600" zoomable="yes"}

1. Complete any post-installation instructions provided by the app, then [configure its settings](#configure-settings) as needed.

## Configure settings

After associating an app in the [!DNL App Management] view, configure its settings through the form:

1. On the associated app's card, select **[!UICONTROL Manage]** > **[!UICONTROL Configure]**.

  The form displays the app's configurable settings.

1. Modify values as needed.

1. Click **[!UICONTROL Save]**.

### Scope-specific configuration

Use scope-specific configuration when different websites, stores, or store views need unique settings. For example, enable a feature only for a specific region or store view, or use different settings per brand. Settings at a lower scope override those from higher scopes.

To override global values at a specific scope level:

1. Click **[!UICONTROL Change Scope]**.

1. Select a scope from the list.

1. Modify values for this scope.

1. Click **[!UICONTROL Save]**.

## Manage scopes

Access **[!UICONTROL Manage Scopes]** from the app details screen to manage scope hierarchy for your app.

![Manage scopes](assets/manage-scopes.png){width="500" zoomable="yes"}

| Action | Description |
| --- | --- |
| **[!UICONTROL Add root scope]** | Add a scope that applies only to the app. |
| **[!UICONTROL Sync Commerce scopes]** | Refresh the list of websites, stores, and store views from Commerce after you add or change them. |
| **[!UICONTROL Import scopes]** | Import scopes in bulk from a file. |

## Upgrade an app

When your app developer deploys a new version of an installed app, [!DNL App Management] is notified that an upgrade is available. App Builder deployment and an App Management upgrade are separate operations: the upgrade applies planned changes to installed components, such as events, webhooks, and Admin UI extensions.

Ask your app developer to confirm that the app supports upgrades. For SDK prerequisites and migration requirements, see [Upgrade your app](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/){target="_blank"} in the developer documentation.

### Review and start an upgrade

In manual mode, which is the default, you review and start the upgrade in [!DNL App Management].

1. Record the installed app version and configuration, and back up application data and external resources with help from your app developer.

1. Navigate to **[!UICONTROL Apps]** > **[!UICONTROL App Management]** and open the available upgrade for the app.

1. Review the planned changes and any warnings. An upgrade can add, modify, or remove components. If a custom installation step is removed, its uninstall script does not run and resources it created are not automatically cleaned up. Confirm any required cleanup with your app developer before proceeding.

1. Start the upgrade and monitor the progress of the listed operations.

1. Review the upgrade result and check for failed operations. If the upgrade fails, follow [Upgrade fails](troubleshooting.md#upgrade-fails) before using **[!UICONTROL Retry Upgrade]**.

In manual mode, planned changes to installed Commerce components are not applied until you start the upgrade. However, deployment can update Runtime action code that the installed app already uses before the upgrade runs.

### Automatic upgrades

Your app developer controls the upgrade mode. Ask your developer to confirm whether the app uses manual or automatic upgrades.

>[!WARNING]
>
>Automatic upgrades are experimental and start after deployment without administrator review, including custom installation scripts that can modify external resources. Coordinate with your developer before automatic upgrades are enabled, including when a newly deployed version changes the mode from manual to automatic.

### Business configuration changes

Changes to the app's business configuration schema appear automatically after deployment. They are separate from installation and upgrades and do not trigger an app upgrade.

## Unassociate an app

Unassociate an app when you no longer need it connected to your Commerce instance. For example, you might need to retire an integration, switch to a different workspace, or clean up test configurations.

>[!WARNING]
>
>Unassociating removes all configuration values for this instance. This cannot be undone. Uninstallation can also remove app components and resources through custom uninstall scripts.

Before proceeding, record the installed version and configuration, back up application data, and ask your app developer which resources the app's uninstall scripts remove and which require manual cleanup. Plan for any service interruption and how to restore the app, its settings, and its data. For routine updates, [upgrade the app](#upgrade-an-app) instead of unassociating it.

To remove an app from a Commerce instance:

1. Navigate to **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

1. On the app's card, select **[!UICONTROL Manage]** > **[!UICONTROL Unassociate]**.

1. Review the listed business use cases and components affected by uninstallation, including events and custom installation steps.

    ![Unassociate confirmation listing affected business use cases](assets/unassociate-app.png){width="600" zoomable="yes"}

1. Confirm the action.

## Related documentation

* [Troubleshooting [!DNL App Management]](troubleshooting.md) - Resolve common issues with association, installation, configuration, and upgrades.
* [Upgrade your app](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/){target="_blank"} - Developer requirements for upgrade modes, migration scripts, and diagnostics.
