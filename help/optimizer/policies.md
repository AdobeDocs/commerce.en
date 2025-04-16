---
title: Policies
description: Learn how to use policies to filter data within a channel to ensure that data is sent to the right destination.
hide: yes
recommendations: noCatalog
---
# Policies

>[!NOTE]
>
>This documentation describes a product in early-access development and does not reflect all functionality intended for general availability.

Policies are data access filters that are housed within channels. Policies help to ensure that the right content is sent to the right destination. For example, point of sale physical stores, marketplaces, advertisement pipelines (Google, Facebook, Instagram).

Policies are based on product attributes, such as brand, model, or part category, and are used to tailor the catalog data to meet specific business requirements. ​

## Filters

Filters are the mechanism within a policy that enforce catalog segmentation. Filters allow businesses to tailor storefronts and channels to specific product sets based on operational needs. You use criteria such as product attributes, operators, and values to define a rule or condition that indicates which products are included or excluded in a channel or storefront.

### Parts of a filter

A filter is composed of the following parts:

|Part|Description|Example|
|---|---|---|
|**Attribute**|The product attribute used for filtering.|`part_category`|
|**Operator**|The condition applied to the attribute.|`IN`, `EQUALS`, `CONTAINS`|
|**Value source**|Specifies whether the values are `STATIC` or `TRIGGER`.|`STATIC`|
|**Value**|The specific values that meet the condition.|`brakes, suspension`|

### Example

A filter with the attribute `part_category`, an operator of `IN`, and values `brakes, suspension` ensures that only products categorized as brakes and suspension are included in the policy.

### Value source types

There are two types of value sources: **STATIC** and **TRIGGER**.

Policies with a **Value source** of **STATIC** are considered universal policies. Universal policies define the experience of a website as a whole. This means the channel will always execute that policy. In other words, the execution of that policy is not based on any user interaction on the storefront.

Policies with a **Value source** of **TRIGGER** are referred to as exclusive policies. This means the channel will execute that policy only when the trigger is specified in the header of the API call. On the storefront, this means information is displayed based on what the shopper selects. For example, in the following image, there are two drop-down menus: **Brand** and **Model**.

![Trigger value source on storefront](./assets/policy-trigger.png)

**Brand** and **Model** are defined triggers:

- `AC-Policy-Brand`
- `AC-Policy-Model`

If the shopper clicks the **Brand** drop-down, the header of the API call contains `AC-Policy-Brand`, which is configured to only show products specific to the `AC-Policy-Brand` policy.

## Create policy

In this section, you create a new policy. The policy can be either **STATIC** or **TRIGGER**.

### Create STATIC policy

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
    1. **Value** - Enter the value(s) within the attribute you previously specified. For example, "brakes, suspension". ​These names must exactly match the names of the values for the attribute you previously specified.

1. Click the **[!UICONTROL Save]** button in the filter details dialog. ​
    
1. Click the action dots (...) next to the filter you created and select **Enable**. From here, you can also **Edit**, **Disable**, or **Delete** the filter.

    The **Status** column shows a green icon and the word "Enabled".

1. Click the **[!UICONTROL Save]** button to save the new policy.​ If the button is not active, ensure the policy name is added by clicking the pencil icon next to **New Policy**.

1. To verify your new policy, go back to the list of policies by clicking the back arrow. ​You will see your new policy listed.

### Create TRIGGER policy

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

1. Click the **[!UICONTROL Save]** button to save the new policy.​ If the button is not active, ensure the policy name is added by clicking the pencil icon next to **New Policy**.

1. To verify your new policy, go back to the list of policies by clicking the back arrow. ​You will see your new policy listed.

By following these steps, the policy will be created and ready to be linked to a channel to control product visibility.
