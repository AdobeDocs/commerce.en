---
title: Carvelo Use Case
description: "Learn how to use [!DNL Adobe Commerce Optimizer] to manage your catalog and create a channel and policy."
hide: yes
role: Admin, Developer
feature: Personalization, Integration
---
# Carvelo Use Case

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

In this use case, you learn about [!DNL Adobe Commerce Optimizer], its hyper performant Commerce Storefront powered by Edge Delivery Services and how Commerce Optimizer can manage your catalog data to empower you to build and grow a catalog to precisely meet your unique business goals, eliminating data redundancy. Streamline your operations by defining your catalog to mirror your retail structure and deliver the right content to the right destination – all this using a single base catalog. Here, you are empowered to seamlessly scale a catalog for multi-brand, multi-business unit and multi-market use cases.

## Let's get started

In this use case, you will be working with the following:

1. [!DNL Adobe Commerce Optimizer] UI - Set up required channels and policies to manage complex operational setup.

1. Commerce Storefront - Render the storefront as set up within [!DNL Adobe Commerce Optimizer] UI and Commerce Storefront Configs.

### ‌Key takeaways

By the end of this article, you will:

- Learn the fundamentals of [!DNL Adobe Commerce Optimizer], it's unique and performant and scalable catalog data model.
- Learn how the new catalog data model ties in seamlessly with platform agnostic storefront components built by Adobe.
- Learn how to use Commerce Storefront powered by Edge Delivery to bring a unique shopping experience to your customers.

## Business scenario – Carvelo Automobile

Carvelo Automobile is a fictitious automobile conglomerate with a complex operational set up.

![Carvelo Automobile](assets/carvelo.png)

In this diagram, you see that Carvelo sells three brands:

- Aurora (electric vehicles)
- Bolt (SUVs)
- Cruz (hybrid)

It sells these brands through three dealers:

- Arkbridge
- Kingsbluff
- Celport

These dealers belong to two different companies:

- West Coast Inc.
- East Coast Inc.

Each company has two pricebooks that are used to sell products at a specific price for different shoppers (base, VIP).

As you can see, this is a very complex business use case. Before [!DNL Adobe Commerce Optimizer], a merchant would have to duplicate their base catalog to support this use case. Now, with [!DNL Adobe Commerce Optimizer], a complex business structure can be supported using a single base catalog to syndicate data without catalog duplication, scale pricebooks (30k+ pricebooks), and deliver all of this on an Edge Delivery Service storefront.

Now that you have an overview of the business use case, it's time to access your [!DNL Adobe Commerce Optimizer] instance so you can begin playing around with the features of [!DNL Adobe Commerce Optimizer].

## Accessing the [!DNL Adobe Commerce Optimizer] instance

After you onboard to the Early Access program, you will be given a link to an [!DNL Adobe Commerce Optimizer] instance. This instance is pre-configured with everything you need to successfully complete the steps outlined in this article, including catalog data that supports the Carvelo Automobile use case.

When you launch [!DNL Adobe Commerce Optimizer], you see the following:

![[!DNL [!DNL Adobe Commerce Optimizer]] UI](assets/user-interface.png)

See the [overview](./overview.md) article to learn more about the different parts that make up the [!DNL Adobe Commerce Optimizer] UI.

## Create a new policy and channel

Let's return to our fictious business use case. Carvelo's commerce manager needs to set up a new storefront for a dealer called *Celport* that belongs to *East Coast Inc* company. Celport will be selling brakes and suspensions for the Bolt and Cruz brands.

![Celport Dealer](assets/celport-dealer.png)

Using [!DNL Adobe Commerce Optimizer], the commerce manager will:

1. Create a new policy called *Celport Part Categories* for Celport to sell only brakes and suspensions.
1. Create a new channel for Celport storefront. This channel will use your newly created policy *Celport Part Category* and the existing *East Coast Inc brands* to ensure Celport can only sell Bolt and Cruz as part of the agreement with East Coast Inc.
1. Set up Celport commerce storefront configs.

At the end of this section, Celport will be up and running ready to sell Carvelo's products.

### Create a Policy

Let's create a new policy called *Celport Part Categories* to filter the SKUs that the Celport dealer sells, which are brakes and suspension.

1. In the left navigation, expand the **[!UICONTROL Catalog]** section and click on **[!UICONTROL Policies]**.

1. Click the **[!UICONTROL Add Policy]** button.

    A new page displays for you to fill in the policy details.

1. Fill in required details:

    **Name** = *Celport Part Categories*

1. Click the **[!UICONTROL Add Filter]** button.

    A dialog displays for you to add filter details.

1. Add filter details:

    - **Attribute** = *part_category*
    - **Operator** = **IN**
    - **Value Source** = **STATIC**
    - **Value** = *brakes*, *suspension*

    >[!NOTE]
    >
    >Attribute is the name of the attribute within the catalog. Make sure it is written correctly.

    To learn more about the difference between a STATIC and TRIGGER value source, see [value source types](./policies.md#value-source-types).

1. In the **[!UICONTROL Filter details]** dialog, click the **[!UICONTROL Save]** button.

1. To enable the filter you just created, click the action dots (...) and select **Enable**.

1. Click the **[!UICONTROL Save]** blue button.

    >[!NOTE]
    >
    >If the **[!UICONTROL Save]** button is not active (blue) you might be missing the policy name. Click the pencil icon next to *New Policy* to add it.

1. Go back to the list of policies by clicking the back arrow.

    Your new *Celport Part Categories* policy appears in the list.

### Create a channel

You will now create a new channel for the *Celport* dealer and you link the following policies: *East Coast Inc brands* and *Celport Part Categories*.

1. In the left navigation, expand the **[!UICONTROL Catalog]** section and click on **[!UICONTROL Channels]**.

    You will see existing channels: *Arkbridge*, *Kingsbluff*, and *Global*.

1. Click the **[!UICONTROL Add Channel]** button.

1. Fill in channel details:

    - **Name** = *Celport*
    - **Scopes** = *en-US* (hit enter)
    - **Policies** (use dropdown) = *East Coast Inc Brands*; *Celport Part Categories*; *Brand*; *Model*                          

1. Click the **[!UICONTROL Add]** blue button, the channel will be created and listed on the list of channels page.

    >[!NOTE]
    >
    >If the **[!UICONTROL Add]** button is not blue, make sure you hit enter in the channel details for the **[!UICONTROL Scopes]** section.

With your new channel and policy created, you now configure the storefront to use the new Celport channel.

## Set up Celport commerce storefront

The final piece of this use case involves setting up the storefront for Celport.

I BELIEVE THIS SECTION WILL LINK TO OR PULL FROM MARGARET'S STOREFRONT WORK.

THIS SECTION NEEDS TO HAVE:

1. How to install the storefront.
1. Launch the storefront to see the catalog experience.
1. Update the config.json file with the new channel ID for Celport.
1. Launch the storefront to see the Celport-specific catalog experience.

## Customer specific prices

We need something here and show how a change in ACO is reflected in the storefront.

## Where to go from here

To learn how you can use Product Discovery and Recommendations to personalize the shopping experience for your buyers, see [merchandising overview](./merch-overview.md).
