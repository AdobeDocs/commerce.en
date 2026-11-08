---
title: Troubleshooting [!DNL App Management]
description: Resolve common issues with app association, installation, configuration, and upgrades.
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
# Troubleshooting [!DNL App Management]

Use the following solutions to resolve common issues with app association, installation, configuration, and upgrades.

## Before contacting your app provider

Follow the steps for your issue below. If you need help from your app developer or provider, collect the following information:

* App name and installed version, if available from **[!UICONTROL Manage]** > **[!UICONTROL Details]** on the app's card.
* Affected Commerce instance and Adobe organization.
* Operation that failed, such as installation or upgrade, and the failed step.
* Displayed error message and a screenshot of the failure, if available.
* Approximate time of the failure, including the time zone.
* Any retry attempts and their results.

## App is not displayed

If the app does not appear in the list after deployment, check the following steps:

1. Verify the app is deployed and available in your organization.

1. Confirm you are signed in to the correct Adobe organization in Developer Console.

1. Ensure the app is ready to connect (your app developer or partner can confirm).

If the app still does not appear, contact your app developer or check the [Commerce Extensibility [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} documentation for technical information.

## Scope sync fails

If scope sync fails when associating an app, try the following:

1. Check that your Commerce instance is accessible and online.

1. Verify your API credentials are valid and have the correct permissions.

1. Try syncing manually from **[!UICONTROL Manage Scopes]** in the app configuration.

## Configuration not saved

If configuration changes do not save, try the following:

1. Check that all required fields are filled in and valid.

1. Ensure you have the correct permissions to modify the app configuration.

1. Try refreshing the page and saving again.

If the issue persists, check your browser console for errors or contact your app developer.

## Installation fails

Keep the installation page open without refreshing until installation finishes. Closing or refreshing it might prevent installation from completing correctly.

If installation reports a failure:

1. Note the failed item and any displayed error message.

1. Check that you completed the app's pre-installation instructions.

1. Ask your app developer to inspect the failed step and correct the cause before attempting installation again.

A failed installation can leave some changes applied. When installation is retried, custom steps recorded as successful are skipped; failed or interrupted steps can run again. Ask your developer to check for resources created by partial execution.

## Upgrade fails

A failed upgrade can leave some operations applied. Do not unassociate and reinstall the app as a routine recovery step, because unassociation removes configuration and can run destructive cleanup scripts.

1. Identify the failed step and record any displayed error message.

1. Ask your app developer to inspect the logs, check for changes already made to Commerce or external resources, and correct the cause.

1. In [!DNL App Management], select **[!UICONTROL Retry Upgrade]**. This action is available for both manual and automatic upgrade modes.

Each retry creates a new plan from the current state. Custom installation steps recorded as successful are skipped; failed or interrupted steps can run again. In automatic mode, deploying the app again also triggers another upgrade attempt.

If repeated attempts fail, ask your app developer to retain the run or attempt IDs and any execution activation ID for troubleshooting. For status commands, attempt history, and Runtime logs, see [Retry a failed upgrade](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/#retry-a-failed-upgrade){target="_blank"} in the developer documentation.

## Resources remain after an upgrade

Removing a custom installation step from an app's configuration does not run its uninstall script or remove resources it created. The upgrade plan warns that no script runs for the removed step, and the step does not appear on the progress screen or in app details after the upgrade.

Ask your app developer to confirm whether the resources are still required and provide a cleanup migration when needed. See [Upgrade an app](manage-app.md#upgrade-an-app) for the administrator workflow.

For technical troubleshooting, see [Commerce Extensibility [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} for more information.
