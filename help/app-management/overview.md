---
title: '[!DNL App Management] overview'
description: Manage App Builder applications associated with your Adobe Commerce instance through a unified Admin UI.
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
# [!DNL App Management] overview

[!DNL App Management] in Adobe Commerce simplifies how applications are discovered, installed, configured, and operated across the commerce environment. It provides a unified framework that enables organizations to adopt extensibility safely and efficiently while reducing operational friction.

![App Management](assets/app-management-view.png){width="500" zoomable="yes"}

For **App Managers**, [!DNL App Management] delivers a centralized view of all installed applications, enabling easier governance, lifecycle management, and operational oversight. Through simplified installation flows, automated configuration steps, and clear visibility into app status and permissions, business and technical operators can manage integrations with confidence—without requiring deep engineering involvement.

For **App Developers**, [!DNL App Management] introduces a standardized way to package and distribute applications using a declarative app manifest. Developers can define configuration, event subscriptions, permissions, and post-installation steps in a single place, allowing applications to install and configure automatically within a merchant environment. This reduces integration effort, improves deployment reliability, and enables developers to focus on delivering business value rather than managing installation complexity.

Together, these capabilities create a scalable extensibility model that empowers merchants to adopt new functionality more quickly while providing developers with a predictable, streamlined application lifecycle.

## What [!DNL App Management] delivers

* **One place for all your apps**. Associate, configure, and manage apps from **[!UICONTROL Apps]** > **[!UICONTROL App Management]**. [Search, filter, and acquire apps](manage-app.md) from the same view.
* **Settings that match your business**. Apply different configurations per website, store, or store view for multi-region or multi-brand setups.
* **Automatic store sync**. Websites, stores, and store views from Commerce are imported when you associate an app.
* **Native Admin experience**. Work with apps from Adobe Exchange or custom deployments without leaving Commerce.

## Who uses [!DNL App Management]?

| Role | Use case |
|------|----------|
| **App managers** | Associate apps, configure settings, and manage apps across your Commerce instance. |
| **Commerce administrators** | Oversee app configurations and permissions across the organization. |
| **Technical architects** | Ensure apps are correctly configured for multi-store or multi-region deployments. |

## What you can do

* **Associate an app**. Link an App Builder application to your Commerce instance by selecting the project and workspace.
* **Configure settings**. Adjust app settings through the auto-generated form; override values per store or region when needed.
* **Manage scopes**. Keep your store hierarchy in sync with your apps and apply settings at the right level.
* **Unassociate an app**. Remove an app when retiring an integration or cleaning up test configurations.

## Next steps

* [Install](install.md). Ensure prerequisites are met and access [!DNL App Management].
* [Manage your app](manage-app.md). Associate, configure, and unassociate apps.

## For developers

If you are building App Builder applications for Adobe Commerce, see the [Commerce Extensibility [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} documentation for configuration schema, runtime actions, and developer setup.
