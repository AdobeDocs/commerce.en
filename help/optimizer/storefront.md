---
title: Set up your storefront
description: Learn how to run the scaffolding tool to setup your [!DNL Adobe Commerce Optimizer] storefront.
role: Developer
---
# Set up your storefront

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

The following steps demonstrate how to set up a local development environment and your Adobe Commerce Storefront powered by Edge Delivery. The [Commerce Storefront powered by Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) is a performant, scalable, and secure storefront that is powered by Adobe's Edge Delivery Services.

## Prerequisites

Before you set up the storefront, set up required tools and accounts as needed.

* GitHub account
* Get the Commerce Optimizer instance details from your system administrator, or client onboarding email.
    * GraphQL API URL: `https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql`
    * tenant ID: {tenantId}
* Get started with Adobe Edge Delivery Services by completing the [Developer Tutorial](https://www.aem.live/developer/tutorial) to learn site development and management basics.
* [Set up a Google Drive or Sharepoint account to store your content, and upload the sample content](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content).
* Install the [Sidekick extension](https://www.aem.live/docs/sidekick) in your browser.
  This extension provides content authors with a toolbar offering context-aware options so that you can edit, preview, and publish your content directly from the pages of your website.

## Set up your development environment

To develop and test your Adobe Commerce Storefront on Edge Delivery Services project locally, you need to set up an environment with Node.js version 22.13.1 LTS. Follow these steps to install Node Version Manager (NVM) and the required Node.js version:

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

>[!TIP]
>
>This initial development setup is for working with Adobe Commerce Optimizer and Adobe Commerce Edge Delivery Service Storefront. Additional developer resources are available for extending your Adobe Commerce Optimizer solution using [App Builder for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) and [API Mesh for Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). For more information, contact your Adobe account representative.

## Create your storefront

The storefront you create for your Adobe Commerce Optimizer project is built using a customized version of the [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) boilerplate. The boilerplate is a set of files and folders that provide a starting point for building your storefront.

### Workflow overview

This workflow is a high-level overview of the steps to set up your storefront. This is a customized setup process for Adobe Commerce Optimizer projects, and is slightly different from the standard [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) setup process.

1. [Create a code repository](#create-a-code-repository)–Create a GitHub repository from the Adobe Commerce + Edge Delivery Services boilerplate template, include all branches from the source repository.
1. [Update storefront boilerplate](#update-storefront-boilerplate)–Update the custom boilerplate template to connect your content and data your data and content for Commerce Optimizer projects.
1. [Install the CodeSync app](#install-codesync-app)–Install the AEM Code Sync GitHub app to connect your repository to the Edge Delivery Service code bus. do not connect the Code Sync app until you have completed source code customization.
1. [Apply customizations to the storefront boiler code](#apply-customizations-to-the-storefront-boiler-code)–Overwrite the code on the `main` branch with your updates.
1. [Preview and publish your content](#preview-and-publish-your-content)–Use the Sidekick extension to preview and publish your content.
1. [Connect to your site](#connect-to-your-site)–Connect to the staging version of your site to view the sample content and data.
1. [Develop the storefront in your local environment](#develop-the-storefront-in-your-local-environment)–Install the required dependencies and start the local development server.



### Step 1: Create a code repository with the storefront boilerplate

In the Adobe Commerce storefront documentation, follow the instructions to create a code repository in GitHub with the boilerplate code for your storefront.

1. Navigate to [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce), select **Use this template**, then select **Create a new repository** option to open the form.

     ![[!DNL Create github repo from storefront boilerplate template]](assets/storefront-create-github-repo.png){width="600" zoomable="yes"}

   If you don't see the **Use this template** button, log in to your GitHub account and navigate to the repository again.

1. Complete the form, and select the **include all branches** option.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](assets/storefront-configure-github-repo.png){width="600" zoomable="yes"}

   After a minute or two, you should be redirected to the home page of your new repository.

### Step 2: Update storefront boilerplate

Update the custom boilerplate template on the `aco` branch to connect your content and data for Commerce Optimizer projects.

Before starting this process, make sure you have the following:

* The URL for the GitHub repository you created from the template.
  You need two values from the repository to complete the setup

  * `{ORG}` - Replace this variable with the organization name or username for the repository
  * `{SITE}` - Replace this variable with your repository name

* The URL to the content folder where [you uploaded the sample data](#prerequisites)

#### Configure the content connection

>[!NOTE]
>
>Make sure that you have [created a content folder in Google Drive or Sharepoint](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#create-and-share-folder) and added the [sample storefront content](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content) to the folder.

1. Clone the repository to your local machine.

   ```bash
   git clone https://github.com/<organization>/<repository>.git

   ```

1. Open the repository in your terminal or IDE.

1. Check out the `aco` branch

   ```bash
   git checkout aco
   ```

1. Update the storefront configuration file to point to your content URL.

   1. Create your configuration file by copying the `default-fstab.yaml` file to `fstab.yaml`.

      ```bash
      cp default-fstab.yaml fstab.yaml
      ```

   1. Open the `[fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary)` configuration file.

      ```json
      mountpoints:
       /: {YOUR_MOUNTAINY_URL}

      folders:
       /products/: /products/default
      ```

   1. Replace `{YOUR_MOUNTPOINT_URL}` with the URL of your content management system. For example, if you are using Google Drive, the updated code should look like this.


      ```json
      mountpoints:
       /: https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}

      folders:
       /products/: /products/default
      ```

   1. Save the file.

#### Configure the data connection

1. In the root directory of the repository, open the `config.json` file.

   +++config.json code

      ```json
      {
       "public": {
         "default": {
           "commerce-core-endpoint": "https://www.aemshop.net/graphql",
           "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/XDevkG9W6UbwgQmPn995r3/graphql",
           "headers": {
              "cs": {
                "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
                "ac-environment-id": "",
                "ac-price-book-id": "west_coast_inc",
                "ac-scope-locale": "en-US"
             }
         },
           "analytics": {
              "base-currency-code": "USD",
              "environment": "Production",
              "store-id": 1,
              "store-name": "ACO Demo",
              "store-url": "https://www.aemshop.net",
              "store-view-id": 1,
              "store-view-name": "Default Store View",
              "website-id": 1,
              "website-name": "Main Website"
             }
           }
         }
      }

      ```

      Notice the `ac-channel-id`, `ac-price-book-id`, and `ac-scope-locale` values in the headers section. These values control catalog configuration and data access filters. Later, you will learn how these headers help you create and manage catalog, price, and product data that displays in your storefront.
      +++

1. Update `commerce-endpoint` with your ACO tenant API url.

1. Update `ac-environment-id` with the tenant ID.

1. Notice that the headers for  `ac-scope-locale` and `ac-price-book-id` are set:

   *`ac-scope-locale` is set to `en-US`
   *`ac-price-book-id` is set to `west_coast_inc`

   These values are used to set the locale and price book for the storefront. Later, you can change these values and add additional headers to set up and manage catalogs and catalog data for different.

#### Configure the Sidekick extension

Add the project configuration for the Sidekick extension used to edit, preview, and publish your content.

>[!NOTE]
>
>Make sure you have the [Sidekick extension installed](https://www.aem.live/docs/sidekick#installation) in your browser.

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

1. In the `url` definitions, replace the variables:

   * `{ORG}`is the repository name or username for the repository

   * `{SITE}` is the name of your repository

1. Save the file.


### Step 3: Add the AEM Code Sync app

Connect your repository to the Edge Delivery Service code bus by adding the [AEM Code Sync GitHub app](https://github.com/apps/aem-code-sync) to your repository.

>[!IMPORTANT]
>
>Do not connect the Code Sync app until you have completed the source code customization.

1. On the  **AEM Code Sync** page, select **Configure**, then authenticate with the **organization** or **account** that contains the repository you created.

1. From the form, choose **Only select repositories** and select the repository you created.

1. Select **Install** to add the AEM Code Sync app to your repository.

   You should see a message that the app was successfully installed.


### Step 4: Apply customizations to the storefront boiler code

To use the customized storefront boilerplate code, you must overwrite the code on the `main` branch with your updates.

1. From you editor or IDE, commit and save the files you updated.

   ```bash
   git add .
   ```

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Push the changes on the `aco` branch and overwrite the `main` branch:

   ```bash
   git push origin aco:main -f
   ```

### Step 5: Preview and publish your content

To add content to your storefront, you have to preview and publish your content using the Sidekick extension.

1. Open your content folder in Google Drive or Sharepoint.

1. Turn on Sidekick by clicking the Sidekick icon in the browser toolbar.

   ![[!DNL Turn on Sidekick from browser toolbar]](assets/storefront-enable-sidekick-toolbar.png){width="600" zoomable="yes"}

1. Use the Sidekick toolbar to preview and publish your content.

   ![[Select files to preview and publish]](assets/storefront-content-preview-publish.png){width="600" zoomable="yes"}

   You must select files in each folder separately, and use the Sidekick toolbar to preview and publish all files.

   * **Preview**–Uploads content to the staging environment. Storefront staging URLs end with `.aem.page`.

   * **Publish**–Uploads content to the production environment. Production URLs end with `aem.live`.

For more information, see the Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick) documentation.

### Preview your site and view sample data

Preview your site and view the sample data by using the storefront search feature and the product details page.

#### Connect to your site to view sample content and data

1. Connect to your site by navigating to `https://main--{SITE}--{ORG}.aem.live`.

   Replace `{ORG}` and `{SITE}` with the organization and repository name you created.

   ![[!DNL ACO storefront site with boilerplate]](assets/aco-storefront-site-boilerplate.png){width="600" zoomable="yes"}

   If the page returns a 404, make sure that you have published the content using the Sidekick extension. Also, double-check the configuration in the files you updated.

1. View the sample catalog data coming from your Commerce Optimizer instance.

   1. Search for `tires` to see a drop down list of available tire products.

    ![[!DNL Discover Adobe Commerce Optimizer products]](assets/storefront-site-with-aco-data.png){width="600" zoomable="yes"}

   1. Press **Enter** to view the product details page.

     ![[!DNL View product details page]](assets/storefront-with-aco-pdp-page.png){width="600" zoomable="yes"}


>[!BEGINSHADEBOX]

**Sample data**

The sample data from your Adobe Commerce Optimizer instance includes a set of product images, product descriptions, and product details. This data is used to populate product search results, product details, and price information based on the headers configured in the storefront `config.json` file.

```json
"ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
"ac-environment-id": "",
"ac-price-book-id": "west_coast_inc",
"ac-scope-locale": "en-US"
```

See the [Use Case](merchandiser-use-case.md) topic to learn more about these headers and how to use them to deliver catalog, product, and price data to the storefront.

>[!ENDSHADEBOX]

## Develop the storefront in your local environment

1. In the directory where you cloned your storefront repository, install the required dependencies.

   ```bash
   npm install
   ```

1. After running this command, 
1. Start the local development server.

## Manage site content

* If you plan to use Adobe Commerce Optimizer with an Adobe Commerce backend, see the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/).

* If you are using Adobe Commerce Optimizer without an Adobe Commerce backend, see the [Adobe Experience Manager storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/).
