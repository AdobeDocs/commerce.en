---
title: Carvelo Use Case
description: "Learn how to use [!DNL Adobe Commerce Optimizer] to manage your catalog using channels and policies and how to set up your storefront based on your catalog configuration."
hide: yes
role: Admin, Developer
feature: Personalization, Integration
---
# Carvelo Use Case

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

The following use case demonstrates how you can use [!DNL Adobe Commerce Optimizer] to organize your catalog to match retail operations using a single base catalog. It also demonstrates how to set up a storefront powered by Edge Delivery Services.

## Prerequisite

Before you go through this use case, make sure you have [set up your storefront](./storefront.md).

## Let's get started

In this use case, you will be working with the following:

1. [!DNL Adobe Commerce Optimizer] UI - Set up required channels and policies to manage complex catalog operational setup.

1. Commerce Storefront - Render the storefront with the catalog data set up within [!DNL Adobe Commerce Optimizer] UI and the Commerce Storefront configuration files, `fstab.yaml` and `config.json`.

### ‌Key takeaways

By the end of this article, you will:

- Learn the fundamentals of [!DNL Adobe Commerce Optimizer] with it's unique performant and scalable catalog data model.
- Learn how the catalog data model seamlessly ties in with platform agnostic storefront components built by Adobe.
- Learn how to use Adobe Commerce Optimizer channels and policies to create custom catalog views and data access filters, and send the data to an Adobe Commerce storefront powered by Edge Delivery.

## Business scenario – Carvelo Automobile

Carvelo Automobile is a fictitious automobile conglomerate with a complex operational setup.

![Carvelo Automobile](assets/carvelo.png)

In this diagram, you see that Carvelo sells automobile products of three brands. Each brand is a different child company:

- Aurora (electric vehicles)
- Bolt (SUVs)
- Cruz (hybrid)

It sells these brands through three dealers:

- Arkbridge
- Kingsbluff
- Celport

These dealers belong to two different parent dealership companies:

- West Coast Inc. (Arkbridge)
- East Coast Inc. (Kingsbluff, Celport)

Each company has two pricebooks that are used to sell products at a specific price for different shoppers (base, VIP).

- `west_coast_inc` and `vip_west_coast_inc`
- `east_coast_inc` and `vip_east_coast_inc`

As you can see, this is a very complex business use case. With [!DNL Adobe Commerce Optimizer], a merchant can support a complex business structure using a single base catalog to syndicate data without catalog duplication, scale pricebooks (30k+ pricebooks), and deliver all of this data to an Edge Delivery Services storefront.

Now that you have an overview of the business use case, here is your objective as you work through this tutorial:

>[!BEGINSHADEBOX]

Carvelo wants to sell parts across its three brands (Aurora, Bolt, and Cruz) through the different dealerships (Akbridge, Kingsbluff, and Celport). Carvelo wants to ensure that the dealerships have access to only the correct parts and prices per their respective licensing agreements.

Ultimately, Carvelo has two major goals:

1. Maintain a "global" website, which has all SKUs across all three brands.
1. Provide a path for dealerships to set up their own storefronts based on unique SKU visibility and prices for each SKU for each dealership.

>[!ENDSHADEBOX]

Now, access your [!DNL Adobe Commerce Optimizer] instance.

## 1. Access the [!DNL Adobe Commerce Optimizer] instance

After you onboard to the Early Access program, Adobe sends an email that provides the URL to access the l[!DNL Adobe Commerce Optimizer] instance provisioned for you. This instance is pre-configured with everything that you need to successfully complete the steps outlined in this tutorial, including catalog data that supports the Carvelo Automobile use case.

When you launch [!DNL Adobe Commerce Optimizer], you see the following:

![[!DNL Adobe Commerce Optimizer] UI](assets/user-interface.png)

>[!NOTE]
>
>See the [overview](./overview.md) article to learn more about the different parts that make up the [!DNL Adobe Commerce Optimizer] UI.

In the left navigation, expand the **[!UICONTROL Catalog]** section and click **[!UICONTROL Channels]**. Notice that the Arkbridge and Kingsbluff dealerships already have channels created:

![Preconfigured Channels](assets/existing-channels-list.png)

>[!NOTE]
>
>You can ignore the **Global** channel for now.

Click the info icon to review channel details.

Arkbridge has the following policies:

- Brand
- Model
- West Coast Inc brands
- Arkbridge part categories

Kingsbluff has the following policies:

- Brand
- Model
- East Coast Inc brands
- Kingsbluff part categories

In the next section, you will create a channel and policies for the Celport dealership.

## 2. Create a policy and channel

Carvelo's commerce manager needs to set up a new storefront for a dealer called *Celport* that belongs to the *East Coast Inc* company. Celport will sell brakes and suspensions for the Bolt and Cruz brands.

![Celport Dealer](assets/celport-dealer.png)

Using [!DNL Adobe Commerce Optimizer], the commerce manager will:

1. Create a new policy called *Celport part categories* for Celport to sell only brake and suspension parts.
1. Create a new channel for the Celport storefront.

   This channel uses your newly created policy *Celport part categories* and the existing *East Coast Inc Brands* to ensure that Celport can sell only the Bolt and Cruz brands as part of the agreement with East Coast Inc. The Celport channel will use the `east_coast_inc` price book to support product pricing schedules that align with brand licensing agreements. 
1. Update the commerce storefront configuration to use data from the Celport channel that you created.

At the end of this section, Celport will be up and running ready to sell Carvelo's products.

### Create a Policy

Let's create a new policy called *Celport part categories* to filter the SKUs that the Celport dealer sells, which include brake and suspension parts.

1. In the left navigation, expand the **[!UICONTROL Catalog]** section and click on **[!UICONTROL Policies]**.

1. Click **[!UICONTROL Add Policy]**.

    A new page displays to add the policy details.

1. Add the required details:

    **Name** = *Celport Part Categories*

1. Click **[!UICONTROL Add Filter]**.

    A dialog displays to add filter details.

1. Add the filter details:

    - **Attribute** = *part_category*
    - **Operator** = **IN**
    - **Value Source** = **STATIC**
    - **Value** = *brakes*, *suspension*

    >[!IMPORTANT]
    >
    >Make sure the attribute name that you specify exactly matches the SKU attribute name in the catalog.

    To learn more about the difference between a STATIC and TRIGGER value source, see [value source types](./policies.md#value-source-types).

1. In the **[!UICONTROL Filter details]** dialog, click **[!UICONTROL Save]**.

1. To enable the filter you just created, click the action dots (...) and select **Enable**.

1. Click **[!UICONTROL Save]**.

    >[!NOTE]
    >
    >If the **[!UICONTROL Save]** button is not active (blue), you might be missing the policy name. Click the pencil icon next to *New Policy* to add it.

1. Go back to the list of policies by clicking the back arrow.

    Your new *Celport part categories* policy appears in the list.

### Create a channel

Create a new channel for the *Celport* dealer and link the following policies: *East Coast Inc brands* and *Celport Part Categories*.

1. In the left navigation, expand the **[!UICONTROL Catalog]** section and click **[!UICONTROL Channels]**.

    ![Channels](assets/channels.png)

    Notice the existing channels: *Arkbridge*, *Kingsbluff*, and *Global*.

    ![Existing Channels Page](assets/existing-channels-list.png)

1. Click **[!UICONTROL Add Channel]**.

1. Fill in channel details:

    - **Name** = *Celport*
    - **Scopes** = *en-US* (hit enter)
    - **Policies** (use dropdown) = *East Coast Inc Brands*; *Celport part categories*; *Brand*; *Model*                          

1. Click **[!UICONTROL Add]** to create the channel.

    The Channels page updates to display the new channel.

    ![Updated Channels List](assets/updated-channels-list.png)

    >[!NOTE]
    >
    >If the **[!UICONTROL Add]** button is not blue, ensure that the scope is selected by placing your cursor in the **[!UICONTROL Scopes]** section and pressing **enter**.

1. Get the Celport channel ID.

    Click the information icon for the Celport channel on the **Channels** page.

    ![Celport Channel ID](assets/celport-channel-id.png)

    Copy and save the channel ID. You need this ID when you update the storefront configuration to deliver data to your new Celport catalog. 

After you create the Celport channel and associated policies, the next step is to configure the storefront to create your new Celport catalog.

## 3. Update your storefront

The final piece of this tutorial involves updating the storefront that [you already created](#prerequisite) to deliver data to the new Celport catalog. In this section, you replace the channel ID in your storefront configuration file with the channel ID for Celport.

1. In your local development environment, open the folder where you cloned the GitHub repository with your storefront boilerplate configuration files.

1. In the root directory of the folder, open the `config.json` file.

   +++config.json code

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

   Notice that the channel header contains the following lines:

   - `ac-channel-id`:`"9ced53d7-35a6-40c5-830e-8288c00985ad"`
   - `ac-environment-id`: `"Fwus6kdpvYCmeEdcCX7PZg"`
   - `ac-price-book-id`: `"west_coast_inc"`

   +++

1. Replace the `ac-channel-id` value with Celport channel ID that you copied previously.
1. If needed, replace the `ac-environment-id` value with the tenant ID for your [!DNL Adobe Commerce Optimizer] instance. You can find the ID in the onboarding email for the Early Access program, or by contacting your Adobe account representative.

   Make sure that the `commerce-endpoint` value matches the GraphQL endpoint for your  [!DNL Adobe Commerce Optimizer] instance.

1. Replace the `ac-price-book-id` value with `"east_coast_inc"`.
1. Save the file.

When you save the changes, you update the catalog configuration to use the Carvelo channel which has been configured to sell only brake and suspension parts.

1. Launch the storefront to view the Celport-specific catalog experience created by your storefront configuration.

    1. From the terminal window in your IDE, start your local storefront preview.
   
        ```shell
        npm start
        ```

    The browser opens to the local development preview at `http://localhost:3000`.
    
    ![Storefront preview in local development environment](assets/storefront-preview-local-development.png){width="675" zoomable="yes"}

     If the command fails or the browser does not open, review the [instructions for local development](storefront.md) in the Storefront setup topic.

    1. In the browser, search for `brakes`, and press **Enter**. 
    
       The storefront updates to display the product list page showing the brake parts.
  
    ![Brakes Product Listing Page](assets/brakes-listing-page.png)

    Click a brake part image to view the product details with price information and note the product price information.

1. Now search for `tires`, which is another part category available in the use case data on your [!DNL Adobe Commerce Optimizer] instance.

   ![Storefront Configuration with Incorrect Headers](assets/storefront-configuration-with-incorrect-headers.png)

   Notice that no results are returned. This is because the Celport channel has been configured to sell only brake and suspension parts.
 
1. Experiment with updating your storefront configuration file (`config.json`).
    
    1. Change the `ac-channel-id` and `ac-price-book` values.
   
       For example, you can change the channel ID to the Kingsbluff channel, and the price book ID to  `east_coast_inc`. You can see the parts categories available for Kingsbluff by reviewing the *Kingsbluff part categories* policy.

    1. Save the file.
   
       When you save the file, the local storefront preview updates automatically.
      
    1. Preview the changes in the browser by using the the Search feature to find tire parts .
       
       Notice the different part types available and notice the prices assigned to the Kingsbluff channel.
       
       By changing header values in the storefront configuration file and exploring the updated storefront, you can see how easy it is to update the catalog view and data filters to customize the storefront experience.

## That's it!

In this tutorial, you learned how [!DNL Adobe Commerce Optimizer] can help you organize your catalog to match your retail operations using a single base catalog. You also learned how to set up a storefront powered by Edge Delivery Services.

## Where to go from here

To learn how you can use Product Discovery and Recommendations to personalize the shopping experience for your customers, see the [merchandising overview](./merch-overview.md).
