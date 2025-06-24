---
title: Set up your storefront
description: Learn how to set up your [!DNL Adobe Commerce Optimizer] storefront.
role: Developer
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Set up your storefront

This tutorial demonstrates how to setup and use [Adobe Commerce Storefront powered by Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) to create a performant, scalable, and secure Commerce storefront powered by data from your [!DNL Adobe Commerce Optimizer] instance.


## Prerequisites

- Ensure that you have a GitHub account (github.com) that can create repositories and is configured for local development.

- Learn about the concepts and workflow to develop Commerce storefronts on Adobe Edge Delivery Services by reviewing the [Overview](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) in the Adobe Commerce Storefront documentation.
- Set up your development environment


### Set up your development environment

Install Node.js and the Sidekick browser extension required to develop and test your [!DNL Adobe Commerce Optimizer] storefront on Edge Delivery Services.

#### Install Node.js

Install Node Version Manager (NVM) and the required Node.js version (22.13.1 LTS).

1. Install Node Version Manager (NVM).

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
    ```

1. Install Node.js and NPM. For more information, see [Node.js](https://nodejs.org/en/).

    ```bash
    nvm install 22
    ```

    ```bash
    npm install -g npm
    ```

1. Verify the installation.

   ```bash
   npm -v
   ```

>[!TIP]
>
>Additional resources for extending and customizing your [!DNL Adobe Commerce Optimizer] solution are available through [App Builder for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) and [API Mesh for Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). For access and usage information, contact your Adobe account representative.

#### Install Sidekick

Install the Sidekick browser extension to edit, preview, and publish content to the storefront. See [Sidekick installation instructions](https://www.aem.live/docs/sidekick#installation).

## Create your storefront

The storefront you create for your [!DNL Adobe Commerce Optimizer] project uses a customized version of the Adobe Commerce on Edge Delivery Services Storefront boilerplate. The boilerplate is a set of files and folders that provide a starting point for storefront development. This setup process is different than the standard setup process for an [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>This tutorial uses macOS, Chrome, and Visual Studio Code as the development environment. The screen captures and instructions reflect that setup. You can use a different operating system, browser, and code editor, but the UI you see and the steps you take vary accordingly.

### Workflow overview

Follow these steps to set up a storefront to use with [!DNL Adobe Commerce Optimizer].

1. **[Create a code repository](#step-1-create-site-code-repository)**–Create a GitHub repository from the Adobe Commerce + Edge Delivery Services boilerplate template. Include all branches from the source repository.
1. **[Update the storefront boilerplate](#step-2-update-the-storefront-boilerplate)**–Update the custom boilerplate template on the `aco` branch to connect your content folder to the storefront.
1. **[Deploy changes](#step-3-deploy-changes)**–Overwrite the code on the `main` branch with the updated code from the `aco` branch.
1. **[Add the CodeSync app](#step-5-add-the-aem-code-sync-app)**–Connect your repository to the Edge Delivery Service. Do not connect the Code Sync app until you have completed the source code customization and have pushed the code to the `main` branch.
1. **[Add content](#step-6-add-content)**–Use the demo content clone tool to create and initialize your storefront content in the Document Author environment hosted on `https://da.live`.
1. **[Preview demo site](#step-7-preview-demo-site)**–Connect to your storefront site to view the sample content and data from the [!DNL Adobe Commerce Optimizer] demo instance.
1. **[Develop in your local environment](#step-8-develop-in-your-local-environment)**–Install the required dependencies. Start the local development server, and update the storefront configuration to connect to the [!DNL Adobe Commerce Optimizer] instance that Adobe provisioned for you.
1. **[Next steps](#next-steps)**–Learn more about managing and displaying content and data in the storefront.


### Step 1: Create site code repository

Create a GitHub repository for the site boilerplate code for your storefront using the Edge Delivery Services + Adobe Commerce Boilerplate template.

1. Log in to your GitHub account.

1. Navigate to the [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub repository.

1. Select **Use this template**, and then select **Create a new repository** from the drop-down menu.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   The repository configuration page displays.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Complete the configuration form with the following details:

   - **Repository template**—`hlxsites/aem-boilerplate-commerce` (default).
   - **Include all branches**—Select the option to include all branches.
   - **Owner**—Your organization or account (required).
   - **Repository name**—A unique name for your new repo (required).
   - **Description**—A brief description of your repo (optional).
   - **Public or Private**—Adobe recommends public (default).

1. Select **Create repository**.

   After several minutes, your new repository opens.

   Ignore any pull request notifications displayed in the GitHub user interface.

### Step 2: Update the storefront boilerplate

You need the following information to update the storefront boilerplate code:

- **GitHub repository URL from Step 2**&mdash; `github.com/{ORG}/{SITE}`
  - `{ORG}` is the organization name or username for the repository
  - `{SITE}` is your repository name
- **Content folder URL from Step 1**&mdash; `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
  - `{YOUR_FOLDER_ID}` is the ID of the folder that you created with the sample content data.

#### Link the repository to the Document Author environment

1. Clone the repository to your local machine.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   If you encounter errors when cloning the repository, see [Troubleshoot cloning errors](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) in the GitHub documentation.

1. Open the repository in your terminal or IDE.

1. Check out the `aco` branch

   ```bash
   git checkout aco
   ```

1. Create your configuration file by copying the `default-fstab.yaml` file to `fstab.yaml`.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. Update the mountpoint in the storefront configuration file to point to your content URL.

   1. Open the [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary) configuration file.

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup

      folders:
       /products/: /products/default
      ```

   1. Replace the `{ORG}` and `{SITE}` strings with the values for the GitHub repository that you created for your boilerplate code.

      For example, the updated code should look like this.

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. Save the file.

#### Configure the Sidekick extension

1. Add the project configuration for the Sidekick extension. This configuration ensures that Sidekick is available to manage content for your storefront project.

>[!NOTE]
>
>Make sure that you have installed the [Sidekick extension](https://www.aem.live/docs/sidekick#installation) in your browser.

1. Open the `tools/sidekick/config.json` file.

   +++Sidekick configuration file

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   See the [Sidekick Library documentation](https://www.aem.live/docs/sidekick-library) for more information.

   +++

1. Update the `url` key values with the values for your GitHub repository.

   - Replace the `{ORG}` string with the organization or username for your repository.

   - Replace the `{SITE}` string with the repository name

   +++Example of updated configuration file

   If your GitHub repository is named `aco-storefront` and your organization is `early-adopter`, the updated URL should look like this:

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```
