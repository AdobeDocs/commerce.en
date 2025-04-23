---
title: Set up your storefront
description: Learn how to set up your [!DNL Adobe Commerce Optimizer] storefront.
role: Developer
---
# Set up your storefront

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

This tutorial demonstrates how to set up a local development environment and create a performant, scalable, and secure storefront that is powered by [Adobe Commerce Storefront powered by Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

## Prerequisites

Gather required information and that required tools and accounts as needed.

* Get the Commerce Optimizer instance details from your system administrator, or client onboarding email.
    * GraphQL API URL: `https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql`
    * tenant ID: {tenantId}

* Set up content folder and install the Sidekick extension
  * [Create and share a Google Drive or Sharepoint folder and load sample content data.](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content).
  * [Install the Sidekick browser extension](https://www.aem.live/docs/sidekick) to edit, preview, and publish storefront content.

  * Log in to your GitHub account.

  >[!TIP]
  >
  >Learn the concepts and basic workflow for creating a storefront with Adobe Edge Delivery Services by completing the [Developer Tutorial](https://www.aem.live/developer/tutorial) to learn site development and management basics.

## Set up your development environment

To develop and test your Adobe Commerce Storefront on Edge Delivery Services project locally, you need Node.js version 22.13.1 LTS.

If needed, complete the following steps to install Node Version Manager (NVM) and the required Node.js version.

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

  ```npm -v```

>[!TIP]
>
>This initial development setup is for working with Adobe Commerce Optimizer and the Adobe Commerce Edge Delivery Service Storefront. Additional developer resources are available for extending your Adobe Commerce Optimizer solution using [App Builder for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) and [API Mesh for Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). For more information, contact your Adobe account representative.

## Create your storefront

The storefront you create for your Adobe Commerce Optimizer project is built using a customized version of the [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) boilerplate. The boilerplate is a set of files and folders that provide a starting point for building your storefront.

The storefront setup process is a customized specifically for Adobe Commerce Optimizer projects, which differs from the standard [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) setup process.

### Workflow overview

Follow these steps to set up a storefront to use with Adobe Commerce Optimizer.

1. [Create a code repository](#step-1-create-a-code-repository-with-the-storefront-boilerplate)–Create a GitHub repository from the Adobe Commerce + Edge Delivery Services boilerplate template. Include all branches from the source repository.
1. [Update the storefront boilerplate](#step-2-update-the-storefront-boilerplate))–Update the custom boilerplate template to connect your content and Adobe Commerce Optimizer data to the storefront.
1. [Add the CodeSync app](#step-3-add-the-aem-code-sync-app)–Connect your repository to the Edge Delivery Service. Do not connect the Code Sync app until you have completed the source code customization and are ready to push the code to the `main` branch.
1. [Upload the updated storefront boilerplate code](#step-4-upload-the-updated-boilerplate)–Overwrite the code on the `main` branch with your updates.
1. [Preview and publish your content](#step-5-preview-and-publish-your-content)–Use the Sidekick extension to preview and publish your content to the storefront.
1. [Preview your site and view sample data](#step-6-preview-your-site-and-view-sample-data)–Connect to your storefront site to view the sample content and data.
1. [Develop the storefront in your local environment](#develop-the-storefront-in-your-local-environment)–Install the required dependencies and start the local development server.
1. [Manage site content](#step-8-manage-site-content)



### Step 1: Create a code repository with the storefront boilerplate

Create a code repository in GitHub with the boilerplate code for your storefront.

1. Log in to your GitHub account.

1. Navigate to the [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub repository, and select **Use this template**.

     ![[!DNL Create github repo from storefront boilerplate template]](assets/storefront-create-github-repo.png){width="600" zoomable="yes"}

1. Select **Create a new repository**.

1. Configure the new repository.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](assets/storefront-configure-github-repo.png){width="600" zoomable="yes"}

   Complete the form with the following details:

   * **Repository template**—`hlxsites/aem-boilerplate-commerce` (default).
   * **Include all branches**—Select the option to include all branches.
   * **Owner**—Your organization or account (required).
   * **Repository name**—A unique name for your new repo (required).
   * **Description**—A brief description of your repo (optional).
   * **Public or Private**—Adobe recommends public (default).

### Step 2: Update the storefront boilerplate

Update the custom boilerplate template on the `aco` branch to connect your content and data for Commerce Optimizer projects.

#### Gather data

Gather the following data to complete the storefront setup process:

| Required data | Definition and Example |
|------|------------------------|
| **GitHub repository URL** | `github.com/{ORG}/{SITE}`<br><br>`{ORG}` is the organization name or username for the repository<br>`{SITE}` is your repository name<br><br>**Example:** `github.com/myorg/mywebsite` |
| **Content folder URL** | `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`<br><br>`{YOUR_FOLDER_ID}` is the ID of the folder that you created with the sample content data.<br><br>**Example:** `https://drive.google.com/drive/folders/1a2b3c4d5e6f7g8h9i0j` |
| **API endpoint for Adobe Commerce Optimizer** | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql`<br><br>`{tenantId}` is the tenant ID for your Adobe Commerce Optimizer instance.<br><br>**Example:** `https://na1-sandbox.api.commerce.adobe.com/XDevkG9W6UbwgQmPn995r3/graphql` |


#### Configure the content connection

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

   1. Open the [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary) configuration file.

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}

      folders:
       /products/: /products/default
      ```

   1. Replace `{YOUR_MOUNTPOINT_URL}` with the URL of your content management system.

      For example, if you are using Google Drive, the updated code should look like this.

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}
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

      Notice the `ac-channel-id`, `ac-price-book-id`, and `ac-scope-locale` values in the headers section. These values control catalog configuration and data access filters. Later, you can learn how these headers help you create and manage catalog, price, and product data that displays in your storefront.
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

   * `{ORG}` is the repository name or username for the repository

   * `{SITE}` is the name of your repository

1. Save the file.


### Step 3: Add the AEM Code Sync app

Connect your repository to the Edge Delivery Service by adding the [AEM Code Sync GitHub app](https://github.com/apps/aem-code-sync) to your repository.

>[!IMPORTANT]
>
>Do not connect the Code Sync app until you have completed the source code customization.

1. On the AEM Code Sync** page, select **Configure**, then authenticate with the **organization** or **account** that contains the repository you created.

1. From the form, choose **Only select repositories** and select the repository you created.

1. Select **Install** to add the AEM Code Sync app to your repository.

   You should see a message that the app was successfully installed.


### Step 4: Upload the updated boilerplate code

To use the customized storefront boilerplate code, you must overwrite the code on the `main` branch with your updates.

1. From your editor or IDE, commit and save the files you updated.

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

   ![[!DNL Turn on Sidekick from browser toolbar]](assets/storefront-enable-sidekick-toolbar.png){width="675" zoomable="yes"}

1. Use the Sidekick toolbar to preview and publish your content.

   ![[Select files to preview and publish]](assets/storefront-content-preview-publish.png){width="600" zoomable="yes"}

   Select files in each folder separately, and use the Sidekick toolbar to preview and publish all files.

   * **Preview**–Uploads content to the staging environment. Storefront staging URLs end with `.aem.page`.

   * **Publish**–Uploads content to the production environment. Production URLs end with `aem.live`.

For more information, see the Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick) documentation.

### Step 6: Preview your site and view sample data

Preview your site and view the sample data by using the storefront search feature and the product details page.

#### Connect to your site to view sample content and data

1. Connect to your site by navigating to `https://main--{SITE}--{ORG}.aem.live`.

   Replace `{ORG}` and `{SITE}` with the organization and name for your boilerplate repository.

   ![[!DNL ACO storefront site with boilerplate]](assets/aco-storefront-site-boilerplate.png){width="600" zoomable="yes"}

   If the page returns a 404, make sure that you have published the content using the Sidekick extension. Also, double-check the configuration in the files you updated.

1. View the sample catalog data coming from your Commerce Optimizer instance.

   1. Search for `tires` to see a drop-down list of available tire products.

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

## STEP 7: Develop the storefront in your local environment

1. In the directory where you cloned your storefront repository, install the required dependencies.

   ```bash
   npm install
   ```

1. After running this command,
1. Start the local development server.

## STEP 8: Manage site content

* If you plan to use Adobe Commerce Optimizer with an Adobe Commerce backend, see the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/).

* If you are using Adobe Commerce Optimizer without an Adobe Commerce backend, see the [Adobe Experience Manager storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/).
