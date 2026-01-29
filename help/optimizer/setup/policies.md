---
title: Policies
description: Learn how to create and manage policies in [!DNL Adobe Commerce Optimizer].
recommendations: noCatalog
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: 77f524f6-e283-44d2-9c79-9d40f686a7bf
---
# Policies

Policies are data access filters contained within catalog views that further refine the data delivered to each catalog view. Policies ensure that the right content is sent to the right destination. For example, point of sale physical stores, marketplaces, advertisement pipelines (Google, Facebook, Instagram).

Policies are based on product attributes, such as brand, model, or part category, and are used to tailor the catalog data to meet specific business requirements. ​

## Filters

Filters are the mechanism within a policy that enforce catalog segmentation. Filters allow businesses to tailor storefronts and catalog views to specific product sets based on operational needs. You use criteria such as product attributes, operators, and values to define a rule or condition that indicates which products are included or excluded in a catalog view or storefront.

### Parts of a filter

A filter is composed of the following parts:

|Part|Description|Example|
|---|---|---|
|**Attribute**|The product attribute used for filtering.|`part_category`|
|**Operator**|The condition applied to the attribute.|`IN`, `EQUALS`, `CONTAINS`|
|**Value source**|Specifies whether the values are `STATIC` or `TRIGGER`.|`STATIC` [Learn more](#value-source-types)|
|**Value**|The specific values that meet the condition.|`brakes, suspension`|

### Example

A filter with the attribute `part_category`, an operator of `IN`, and values `brakes, suspension` ensures that only products with an attribute `part_category` which has a value of `brake` or `suspension` is filtered and displayed by the policy.

### Value source types

There are two types of value sources: **STATIC** and **TRIGGER**.

Policies with a **Value source** of **STATIC** are considered universal policies. Universal policies define the experience of a website as a whole. This means that the catalog view will always execute that policy. In other words, the execution of that policy is not based on any user interaction on the storefront.

Policies with a **Value source** of **TRIGGER** are referred to as exclusive policies. This means that the catalog view will execute that policy only when the trigger is specified in the header of the API call. On the storefront, this means information is displayed based on what the shopper selects. For example, in the following image, there are two drop-down menus: **Brand** and **Model**.

![Trigger value source on storefront](../assets/policy-trigger.png)

**Brand** and **Model** are defined triggers:

- `AC-Policy-Brand`
- `AC-Policy-Model`

If the shopper clicks the **Brand** drop-down, the header of the API call contains `AC-Policy-Brand`, which is configured to only show products specific to the `AC-Policy-Brand` policy.

## Create policy

In this section, you create a new policy. The policy can be either **STATIC** or **TRIGGER**.

### Create a STATIC policy

1. On the left menu, open the **[!UICONTROL Catalog]** section and click on **[!UICONTROL Policies]**.

1. Click the **[!UICONTROL Add Policy]** button.

    A new page opens for you to fill in the policy details. ​

1. Enter the name of the policy, for example "Celport Part Categories".

1. Click the **[!UICONTROL Add Filter]** button.

    A dialog opens for you to add filter details.

1. Add the filter details. For example:

    1. **Attribute** - Enter an attribute from your catalog. For example, "part_category". This name must exactly match the name of the attribute in your catalog.
    1. **Operator** - Choose the operator. For example, **IN**. ​
    1. **Value Source** - Select **STATIC**. ​
    1. **Value** - Enter a value from the attribute definition that you previously specified. For example, enter "brakes" to create a filter for brake parts.
    1. To save the value, press **Enter**.

       If the policy is designed to filter by multiple values, enter each value separately.

1. Click the **[!UICONTROL Save]** button in the filter details dialog. ​
    
1. Click the action dots (...) next to the filter you created and select **Enable**. From here, you can also **Edit**, **Disable**, or **Delete** the filter.

    The **Status** column shows a green icon and the word "Enabled".

1. Click the **[!UICONTROL Save]** button to save the new policy.​ If the button is not active, ensure that the policy name is added by clicking the pencil icon next to **New Policy**.

1. To verify your new policy, go back to the list of policies by clicking the back arrow. ​You will see your new policy listed.

### Create a TRIGGER policy

1. On the left menu, open the **[!UICONTROL Catalog]** section and click on **[!UICONTROL Policies]**.

1. Click the **[!UICONTROL Add Policy]** button.

    A new page opens for you to fill in the policy details. ​

1. Enter the name of the policy, for example "Celport Part Categories".

1. Click the **[!UICONTROL Add Trigger]** button.

    The **Trigger details** dialog appears.

1. Enter a name for the trigger, such as **AC-Policy-Brand**.

1. Select the **Transport type**. **HTTP_HEADER** is currently the only type supported.

1. Click the **[!UICONTROL Save]** button to save the trigger.

1. Click the **[!UICONTROL Add Filter]** button.

    A dialog opens for you to add filter details.

1. Add the filter details. For example:

    1. **Attribute** - Enter an attribute from your catalog. For example, "part_category". This name must exactly match the name of the attribute in your catalog.
    1. **Operator** - Choose the operator. For example, **IN**. ​
    1. **Value Source** - Select **TRIGGER**. ​
    1. **Value** - Enter the trigger name you created previously (**AC-Policy-Brand**).

1. Click the **[!UICONTROL Save]** button in the filter details dialog. ​
    
1. Click the action dots (...) next to the filter you created and select **Enable**. From here, you can also **Edit**, **Disable**, or **Delete** the filter.

    The **Status** column shows a green icon and the word "Enabled".

1. Click the **[!UICONTROL Save]** button to save the new policy.​ If the button is not active, ensure that the policy name is added by clicking the pencil icon next to **New Policy**.

1. To verify your new policy, go back to the list of policies by clicking the back arrow. ​You will see your new policy listed.

By following these steps, the policy will be created and ready to be linked to a catalog view to control product visibility.
