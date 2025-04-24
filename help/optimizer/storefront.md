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

Before setting up your Adobe Commerce Optimizer storefront, ensure you have the following requirements in place:

* GitHub account
   * SSH keys to clone content to your local development environment

* Create a content folder and add sample content
  * [Create and share a Google Drive or Sharepoint folder](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#create-and-share-folder)
  * [Load the sample content](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content) into your folder. The sample content includes images, text, and other assets that make up your site.

* [Install the Sidekick browser extension](https://www.aem.live/docs/sidekick) to edit, preview, and publish storefront content.


  >[!TIP]
  >
  >Learn the concepts and basic workflow for creating a storefront with Adobe Edge Delivery Services by completing the [Developer Tutorial](https://www.aem.live/developer/tutorial).

## Set up your development environment

To develop and test  your Adobe Commerce Optimizer Storefront on Edge Delivery Services project locally, you need Node.js version 22.13.1 LTS.

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

   ```bash
   npm -v
   ```

>[!TIP]
>
>This initial development setup is for working with Adobe Commerce Optimizer and the Adobe Commerce Edge Delivery Service Storefront. Additional developer resources are available for extending your Adobe Commerce Optimizer solution using [App Builder for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) and [API Mesh for Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). For more information, contact your Adobe account representative.

## Create your storefront

The storefront you create for your Adobe Commerce Optimizer project is built using a customized version of the [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) boilerplate. The boilerplate is a set of files and folders that provide a starting point for building your storefront.

This storefront setup process is customized specifically for Adobe Commerce Optimizer projects. The flow is different than the flow for the standard [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) setup.

### Workflow overview

Follow these steps to set up a storefront to use with Adobe Commerce Optimizer.

1. **[Create a code repository](#step-1-create-a-code-repository-with-the-storefront-boilerplate)**–Create a GitHub repository from the Adobe Commerce + Edge Delivery Services boilerplate template. Include all branches from the source repository.
1. **[Update the storefront boilerplate](#step-2-update-the-storefront-boilerplate)**–Update the custom boilerplate template to connect your content and Adobe Commerce Optimizer data to the storefront.
1. **[Upload the updated storefront boilerplate code](#step-3-upload-the-updated-boilerplate-code)**–Overwrite the code on the `main` branch with your updates.
1. **[Add the CodeSync app](#step-4-add-the-aem-code-sync-app)**–Connect your repository to the Edge Delivery Service. Do not connect the Code Sync app until you have completed the source code customization and are ready to push the code to the `main` branch.
1. **[Preview and publish your content](#step-5-preview-and-publish-your-content)**–Use the Sidekick extension to preview and publish your content to the storefront.
1. **[Preview your site and view sample data](#step-6-preview-your-site-and-view-sample-data)**–Connect to your storefront site to view the sample content and data.
1. **[Develop the storefront in your local environment](#step-7-develop-the-storefront-in-your-local-environmentdevelop-the-storefront-in-your-local-environment)**–Install the required dependencies and start the local development server.
1. **[Manage site content](#step-8-manage-site-content)**—Learn more about updating and managing your storefront content.

### Step 1: Create a code repository with the storefront boilerplate

Create a code repository in GitHub with the boilerplate code for your storefront.

1. Log in to your GitHub account.

1. Navigate to the [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub repository, and select **Use this template**.

     ![[!DNL Create github repo from storefront boilerplate template]](assets/storefront-create-github-repo.png){width="675" zoomable="yes"}

1. Select **Create repository**.

1. Configure the new repository.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](assets/storefront-configure-github-repo.png){width="675" zoomable="yes"}

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

   If encounter errors when cloning the repository, see [Troubleshoot cloning errors](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) in the GitHub documentation.

1. Open the repository in your terminal or IDE.

1. Check out the `aco` branch

   ```bash
   git checkout aco
   ```

1. Create your configuration file by copying the `default-fstab.yaml` file to `fstab.yaml`.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. Update the storefront configuration file to point to your content URL.

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

#### Review the data connection configuration

The data connection establishes communication between Adobe Commerce Optimizer and the storefront, ensuring that catalog data seamlessly flows to the storefront. This process populates various storefront interfaces, including the Search component, Product List, and Product Details pages.

For the initial storefront setup, Adobe provides a default configuration file that connects to an Adobe Commerce Optimizer demo instance with sample data.

```json
{
  "public": {
    "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
        "cs": {
          "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
          "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
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

#### Review the default configuration file:

1. In your code repository, navigate to the root directory.

1. Open the `config.json` file.

   In this file, the following key values specify the Adobe Commerce Optimizer instance to connect to and determine the data flows to the storefront:

   * `commerce-endpoint` defines the Adobe Commerce Optimizer instance to connect to.
   * `headers` determine the data that flows to the storefront.
     * `ac-channel-id` is set to `west_coast_inc`
     * `ac-price-book-id` is set to `west_coast_inc`
     * `ac-scope-locale` is set to `en-US`
     * `ac-price-book-id` is set to `west_coast_inc`

   These values set the channel id, price book, and locale to send catalog data to a specific sales channel and filter that data based on the specified locale and price book. Later, you learn how to change the Adobe Commerce Optimizer instance and update the headers to define what data is delivered to the storefront.

1. After reviewing the file, close it and continue the tutorial.


#### Configure the Sidekick extension

Add the project configuration for the Sidekick extension that is used to edit, preview, and publish your content. This configuration ensures that you can use Sidekick to manage content both in your shared content folder and on site pages published to the staging and production environments.

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

1. In the `url` definitions, replace the variables:

   * `{ORG}` is the repository name or username for your code repository

   * `{SITE}` is the repository name

1. Save the file.

### Step 3: Upload the updated boilerplate code

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

### Step 4: Add the AEM Code Sync app

Connect your repository to the Edge Delivery Service by adding the AEM Code Sync GitHub app to your repository.

>[!IMPORTANT]
>
>Do not connect the Code Sync app until you have uploaded the updated boilerplate code to the main branch of your GitHub repository.

1. Open the [AEM Code Sync app](https://github.com/apps/aem-code-sync) configuration page.

1. Select **Configure**, then authenticate with the **organization** or **account** that contains the repository you created.

1. From the form, choose **Only select repositories** and select the repository you created.

1. Select **Install** to add the AEM Code Sync app to your repository.

   You should see a message that the app was successfully installed.

### Step 5: Preview and publish your content

To add content to your storefront, you have to preview and publish your content using the Sidekick extension.

1. Open your content folder in Google Drive or Sharepoint.

1. Turn on Sidekick by clicking the Sidekick icon in the browser toolbar.

   ![[!DNL Turn on Sidekick from browser toolbar]](assets/storefront-enable-sidekick-toolbar.png){width="675" zoomable="yes"}

1. Use the Sidekick toolbar to preview and publish your content.

   ![[Select files to preview and publish]](assets/storefront-content-preview-publish.png){width="675" zoomable="yes"}

   Select files in each folder separately, and use the Sidekick toolbar to preview and publish all files.

   * **Preview**–Uploads content to the staging environment. Storefront staging URLs end with `.aem.page`.

   * **Publish**–Uploads content to the production environment. Production URLs end with `aem.live`.

For more information, see the Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick) documentation.

### Step 6: Preview your site sample

Preview your site to verify that both the sample content and the Commerce Optimizer demo data is displaying correctly.

* **Sample content** is served from your shared content folder. It includes the page layouts, banners, and other content that you published using Sidekick.
* **Sample data** is served from the Adobe Commerce Optimizer demo instance. Data includes product data with product attributes, images, product descriptions, and prices populated based on the values specified in the storefront configuration file, `config.json`.


#### Connect to your site to view sample content and data

1. Connect to your site by navigating to `https://main--{SITE}--{ORG}.aem.live`.

   Replace `{ORG}` and `{SITE}` with the organization and name for your boilerplate repository.

   ![[!DNL ACO storefront site with boilerplate]](assets/aco-storefront-site-boilerplate.png){width="675" zoomable="yes"}

   If the page returns a 404, make sure that you have published the content using the Sidekick extension. Also, double-check the configuration in the files you updated.

1. View the sample catalog data coming from your Commerce Optimizer demo instance.

   1. Search for `tires` to see a drop-down list of available tire products.

    ![[!DNL Discover Adobe Commerce Optimizer products]](assets/storefront-site-with-aco-data.png){width="675" zoomable="yes"}

    The search component is part of the storefront boilerplate code. The search results data is populated based on the storefront configuration.

   1. Press **Enter** to view the product list page.

     ![[!DNL View product details page]](assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. View a product details page by selecting any tire product on the page.

      If you explore the storefront, notice that some of the components don't work. For example, adding a product to the shopping cart returns an error, and the account management components don't work. This is because these components have not been configured to receive data from a Commerce backend. Commerce Optimizer populates only the Search, Product list and Product details pages.

   1. After exploring the storefront, continue with the tutorial.


### Step 7: Develop the storefront in your local environment

In this section, you experiment with the storefront configuration in your local development environment by connecting the storefront to the Adobe Commerce Optimizer instance that Adobe provisioned for you.

To make the connection, you need the GraphQL endpoint for Merchandising Services that was provided in your onboarding email.

`https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql`

#### Start local development

1. In your IDE, checkout the main branch of your GitHub code repository.

   ```bash
   git checkout main
   ```

1. Install the required dependencies.

   ```bash
   npm install
   ```

1. Start the local development server.

   ```bash
   npm start
   ```

   The first page of your boilerplate storefront should be visible in your browser at `http://localhost:3000`.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](assets/aco-storefront-local-dev-env.png){width="675" zoomable="yes"}


1. Update the storefront configuration to point to the Adobe Commerce Optimizer instance that Adobe has provisioned for you.

   1. Open the `config.json` file.

   1. Update the following values using your the endpoint for your Adobe Commerce Optimizer instance:

     * Replace the **`commerce-endpoint`** value with your endpoint URL.

      `"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/XDevkG9W6UbwgQmPn995r3/graphql"`

     * Replace the **`ac-environment-id`** with the tenant ID from your endpoint URL.

       `"ac-environment-id": "XDevkG9W6UbwgQmPn995r3"`

   1. Save the file to update your local storefront configuration.

1. Check the site to see the results of the configuration change.

   1. In the browser, navigate to `http://localhost:3000` and refresh the page.

   1. In the storefront header, click the magnifying glass to search for `tires`.

      Notice that the drop-down list does not populate.

   1. Press **Enter** to display the Product list page.

      ![[!DNL Empty search results with invalid header values]](assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      The search doesn't return any results because the headers in your storefront configuration file use headers values based on the demo instance. Now that the configuration points to the Adobe Commerce Optimizer instance provisioned for you, those values are invalid.

### Next steps

To learn how to update the headers in the storefront configuration to use values from your Adobe Commerce Optimizer instance, see the [Merchandiser end-to-end use case](https://experienceleague-review.corp.adobe.com/docs/commerce/optimizer/use-case/merchandiser-use-case.html).


>[!MORELIKETHIS]
>
>If you are using Adobe Commerce Optimizer without an Adobe Commerce backend, see the [Adobe Experience Manager storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/) to learn more about updating site content and integrating with your Commerce frontend components and backend data.
>
>If you plan to use Adobe Commerce Optimizer with an Adobe Commerce backend, see the [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/) to learn how to update content and configure storefront components for account management, checkout, and other capabilities.

