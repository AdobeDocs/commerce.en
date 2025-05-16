---
title: Set up your storefront
description: Learn how to set up your [!DNL Adobe Commerce Optimizer] storefront.
role: Developer
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
---
# Set up your storefront

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

This tutorial demonstrates how to setup and use [Adobe Commerce Storefront powered by Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) to create a performant, scalable, and secure Commerce storefront powered by data from your [!DNL Adobe Commerce Optimizer] instance.


## Prerequisites

* Ensure that you have a GitHub account (github.com) that can create repositories and is configured for local development.

* Learn about the concepts and workflow to develop Commerce storefronts on Adobe Edge Delivery Services by reviewing the [Overview](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) in the Adobe Commerce Storefront documentation.
* Set up your development environment


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
>This storefront setup process is to use [!DNL Adobe Commerce Optimizer] with the Adobe Commerce Edge Delivery Service Storefront. Additional resources for extending and customizing your [!DNL Adobe Commerce Optimizer] solution are available through [App Builder for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) and [API Mesh for Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). For access and usage information, contact your Adobe account representative.

#### Install Sidekick

Install the Sidekick browser extension to edit, preview, and publish content to the storefront. See [Sidekick installation instructions](https://www.aem.live/docs/sidekick#installation).


## Create your storefront

The storefront you create for your [!DNL Adobe Commerce Optimizer] project uses a customized version of the Adobe Commerce on Edge Delivery Services Storefront boilerplate. The boilerplate is a set of files and folders that provide a starting point for storefront development. This setup process is different than the standard setup process for an [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>This tutorial uses macOS, Chrome, and Visual Studio Code as the development environment. The screen captures and instructions reflect that set up. You can use a different operating system, browser, and code editor, but the UI you see and the steps you take vary accordingly.

### Workflow overview

Follow these steps to set up a storefront to use with [!DNL Adobe Commerce Optimizer].

1. **[Create a code repository](#step-1%3A-create-site-code-repository)**–Create a GitHub repository from the Adobe Commerce + Edge Delivery Services boilerplate template. Include all branches from the source repository.
1. **[Update the storefront boilerplate](#step-2%3A-update-the-storefront-boilerplate)**–Update the custom boilerplate template on the `aco` branch to connect your content folder to the storefront.
1. **[Upload the updated storefront boilerplate code](#step-3%3A-upload-the-updated-boilerplate-code)**–Overwrite the code on the `main` branch with the updated code from the `aco` branch.
1. **[Add the CodeSync app](#step-5%3A-add-the-aem-code-sync-app)**–Connect your repository to the Edge Delivery Service. Do not connect the Code Sync app until you have completed the source code customization and are ready to push the code to the `main` branch.
1. **[Add content documents to your storefront](#step-6%3A-add-content-documents-for-your-storefront)**–Use the demo content clone tool to create and initialize your storefront content in the Document Author environment hosted on `https://da.live`.
1. **[Preview your site and view sample data](#step-7%3A-preview-your-site)**–Connect to your storefront site to view the sample content and data from the [!DNL Adobe Commerce Optimizer] demo instance.
1. **[Develop the storefront in your local environment](#step-8%3A-develop-the-storefront-in-your-local-environment)**–Install the required dependencies. Start the local development server, and update the storefront configuration to connect to the [!DNL Adobe Commerce Optimizer] instance that Adobe provisioned for you.
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

   * **Repository template**—`hlxsites/aem-boilerplate-commerce` (default).
   * **Include all branches**—Select the option to include all branches.
   * **Owner**—Your organization or account (required).
   * **Repository name**—A unique name for your new repo (required).
   * **Description**—A brief description of your repo (optional).
   * **Public or Private**—Adobe recommends public (default).

1. Select **Create repository**.

   After several minutes, your new repository opens.

   Ignore any pull request notifications displayed in the GitHub user interface.

### Step 2: Update the storefront boilerplate

You need the following information to update the storefront boilerplate code:

* **GitHub repository URL from Step 2**&mdash; `github.com/{ORG}/{SITE}`

  * `{ORG}` is the organization name or username for the repository

  * `{SITE}` is your repository name

* **Content folder URL from Step 1**&mdash; `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` is the ID of the folder that you created with the sample content data.

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

#### Review the default data connection configuration

The default configuration file (`config.json`) in the root directory of the storefront boilerplate code establishes communication between the storefront and the specified [!DNL Adobe Commerce Optimizer] instance. This connection enables catalog data to flow to the storefront and populate various storefront interfaces, including the search component, product list, and product details pages.

For your initial storefront setup, you connect to the default [!DNL Adobe Commerce Optimizer] instance with sample data.

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

In the `config.json` file, the following key values specify the [!DNL Adobe Commerce Optimizer] instance to connect to and determine the data that flows to the storefront:

* `commerce-endpoint` specifies the instance to connect to. It is set to use the default [!DNL Adobe Commerce Optimizer] instance. This endpoint is used to retrieve catalog data.
* `ac-environment-id` is the tenant ID for the [!DNL Adobe Commerce Optimizer] instance.
* `headers` determine the data that flows from the instance to the storefront.
   * `ac-channel-id` is set to `west_coast_inc`
   * `ac-price-book-id` is set to `west_coast_inc`
   * `ac-scope-locale` is set to `en-US`
   * `ac-price-book-id` is set to `west_coast_inc`

These values set the channel ID, locale, and price book ID to send catalog data to a specific sales channel and filter that data based on specified locale and price book values. Later, you update the endpoint to connect to the [!DNL Adobe Commerce Optimizer] instance that Adobe provisioned for you, and replace the header values to retrieve the data from that instance.

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

   * Replace the `{ORG}` string with the organization or username for your repository.

   * Replace the `{SITE}` string with the repository name

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

   +++

1. Save the file.

### Step 3: Upload the updated boilerplate code

To use the customized storefront boilerplate code, overwrite the code on the `main` branch with your updates.

1. From your editor or IDE, commit and save the files you updated.

   ```bash
   git add .
   ```

1. Verify that you are committing the two updated files.

   ```bash
   git status
   On branch aco
   Your branch is up to date with 'origin/aco'.

   Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   fstab1.yaml
        modified:   tools/sidekick/config.json
   ```

1. Commit the changes to the `aco` branch.

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Overwrite the boilerplate on the `main` branch with the changes on the `aco` branch.

   ```bash
   git push origin aco:main -f
   ```

### Step 5: Add the AEM Code Sync app

Connect your repository to the Edge Delivery Service by adding the AEM Code Sync GitHub app to your repository.

>[!IMPORTANT]
>
>Do not connect the Code Sync app until you have uploaded the updated boilerplate code to the main branch of your GitHub repository.

1. Open the [AEM Code Sync app](https://github.com/apps/aem-code-sync) configuration page.

1. Select **Configure**, then authenticate with the **organization** or **account** that contains the repository you created.

1. From the form, choose **Only select repositories**, and then select the repository you created.

1. Select **Install** to add the AEM Code Sync app to your repository.

   You should see a message that the app was successfully installed.

### Step 6: Add content documents for your storefront

Create and initialize your storefront content in the Document Author environment hosted on `https://da.live` using the Demo site clone tool. This tool imports the sample content into the Document Author environment and completes the content preview and publish process for all documents in the sample content. The sample content includes the page layouts, banners, labels, and other components to build your storefront.

1. Open the [demo content clone tool](https://da.live/app/hlxsites/aem-boilerplate-commerce/tools/site-creator/site-creator).

   ![[!DNL AEM demo content clone tool]](./assets/storefront-demo-content-clone-tool.png){width="700" zoomable="yes"}

1. Paste the GitHub URL for your storefront boilerplate project in the [!UICONTROL **Project GitHub URL**] field.


1. Import, preview, and publish the content to the Document Author environment, select **Create site**.

   After the site is created, you can use the links in the [!UICONTROL Edit content] section to open the Document Author environment to explore the content and the site.

   ![[!DNL AEM demo content clone tool]](./assets/storefront-document-author-environment.png){width="700" zoomable="yes"}

   The main links to your content and site follow these formats:

   * **Root content folder**&mdash;  `https://da.live/#/{ORG}/{SITE}`
   * **Site preview**&mdash;   `https://main--{SITE}--{ORG}.aem.page/`
   * **Site production:**&mdash;  `https:/main--{SITE}--{ORG}.ae.live/`

1. Open the root content folder link to view the content.

   [[!DNL Storefront Document Author environment]](./assets/storefront-document-author-environment.png){width="700" zoomable="yes"}

   >[!TIP]
   >
   >In the side navigation, use the [!UICONTROL **Learn**] and [!UICONTRL **Discover**] links to access learning resources for managing your site and site content.

### Step 7: Preview your site and view sample data

Verify that both the sample content and the data from the Adobe Commerce Optimizer demo instance are displayed correctly.

* **Sample content** is served from your shared content folder. It includes the page layouts, banners, labels for your site.
* **Sample data** is served from the [!DNL Adobe Commerce Optimizer] demo instance. Data includes product data with product attributes, images, product descriptions, and prices populated based on the header values specified in the storefront configuration file, `config.json`.


#### Connect to your site to view sample content and data

1. View your site by navigating to `https://main--{SITE}--{ORG}.aem.live`.

   Replace `{ORG}` and `{SITE}` with the organization and name for your boilerplate repository.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   If the page returns a 404, verify the following:

   * The mountpoint in your `fstab.yaml` file points to the correct content URL: `https://content.da.live/{ORG}/{SITE}/`
   * You have configured the Code Sync app to connect to your GitHub repository.
   * You have published the content to the Document Author environment using the demo content clone tool.


1. View the sample catalog data coming from the Commerce Optimizer default instance.

   1. Search for `tires` to see a drop-down list of available tire products.

     ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

    The search component is part of the storefront boilerplate code. The search results data is populated based on the storefront configuration in `config.json`.

   1. Press **Enter** to view the product list page.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. View a product details page by selecting any tire product on the page.

      If you explore the storefront, notice that some of the components don't work. For example, adding a product to the shopping cart returns an error, and the account management components don't work. These issues occur because these components have not been configured to receive data from a Commerce backend. The data from the [!DNL Adobe Commerce Optimizer] instance populates only the search result and product details pages.

   1. After exploring the storefront, continue with the tutorial.


### Step 8: Develop the storefront in your local environment

In this section, you update the storefront configuration from your local development environment.

* Update the storefront configuration to connect to the GraphQL endpoint for the [!DNL Adobe Commerce Optimizer] instance that Adobe provisioned for you.
* Update the header values to retrieve data from your instance.

#### Start local development

1. In your IDE, check out the main branch of your GitHub code repository.

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

  ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Update the storefront configuration

Update the storefront configuration file and preview the changes in your local development environment.

1. In your IDE, update the storefront configuration to connect to the [!DNL Adobe Commerce Optimizer] instance that Adobe has provisioned for you.

   1. Open the `config.json` file.

   1. Update the following values using the endpoint for your [!DNL Adobe Commerce Optimizer] instance:

      * **`commerce-endpoint`**–Replace the existing value with your endpoint URL.

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`**—Replace the existing value with the tenant ID from your endpoint URL.

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. Save the file.

      If your local preview is working correctly, the updates are applied to your local storefront. 

1. Check the site to see the results of the configuration change.

   1. In the browser, navigate to `http://localhost:3000` and refresh the page.

   1. In the storefront header, click the magnifying glass to search for `tires`.

      ![Search for tires](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

      Notice that the drop-down list does not populate.

   1. Press **Enter** to display the Product list page.

      ![Empty search results with invalid header values](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      The search doesn't return any results because the header values in your storefront configuration file are based on the default instance. Now that the configuration points to the [!DNL Adobe Commerce Optimizer] instance provisioned for you, those values are invalid.

### Next steps

See the [Storefront and Catalog Administrator end-to-end use case](./use-case/admin-use-case.md) to learn more about managing and displaying content and data in the storefront.

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/) to learn more about updating site content and integrating with your Commerce frontend components and backend data.
></br></br>
>* [Adobe Commerce Storefront documentation](https://experienceleague.adobe.com/developer/commerce/storefront/) to learn more about updating site content and integrating with Adobe Commerce frontend components and backend data.
