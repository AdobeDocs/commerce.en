---
title: Merchandising Rules
description: '[!DNL Adobe Commerce Optimizer] merchandising rules combine logic with actions to shape the shopping experience.'
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
exl-id: f2a9b5e8-d23d-4855-b424-ca6b40e057df
---
# Merchandising Rules

Merchandising rules refers to a set of rules that combine logic with actions to shape a shopper's search experience in your store. You can use merchandising rules to boost, bury, pin, or hide products to calibrate search results in real time to support your business goals.

Each rule has three main components:

- Conditions – The conditions that trigger an action.
- Events – The actions that take place when the conditions are met.
- Details – The name of the rule, and optional time frame and description.

You can combine multiple conditions and actions, and schedule a rule to be active for a period. You can also set a default rule that is applied even when no search term is set.

## Requirements

A simple search rule can have a single condition and a single event, while a complex rule can have up to ten conditions that trigger up to 25 events.
Rules can have:

- Up to ten conditions
- Up to 25 events

Query text can contain:

- Alphanumeric characters (letters and numbers)
- Either upper or lowercase characters. Capitalization is ignored.

## Logical Operators

The logical operators `AND` and `OR` join two conditions and return different results. All logical operators used in a rule with multiple conditions are the same. It is not possible to use both `AND` and `OR` in the same rule.

### Match Operators

The Match operators `All` and `Any` determine the logical operator that is used to join multiple conditions in the rule, and can be used to change the existing operator.

- `All` - Uses the `AND` logical operator to join multiple conditions. A rule that uses the `All` Match operator can have only one `Search query is` condition.
- `Any` - Uses the `OR` logical operator to join multiple conditions.

When composing a complex rule, it can help to write it out with indentation to describe the conditions, associated events, and product names or SKUs that are needed to return the results you want to achieve. Then, build the rule and test the result.

## Default rule

You can set a default rule that is applied when no search term is provided, or no other search rule can be applied. If you set the default rule to "Most Purchased", then all queries will default to that ranking type, unless super-ceded by a more specific search term. No search term can be set for the default rule.

## Order of precedence with multiple rules

Only one search rule is applied to a search term at any one time.
If multiple rules are found to be applicable to a search phrase, then all these rules are applied. If there is a collision between two rules---`rule 1` that boosts sku1 but `rule 2` hides the same SKU---then the most recently applied rule (`rule 2`) takes precedence.

- Rules are ordered by the "Last Modified" timestamp. The most recently modified rule is applied first, and older rules after that, in timestamp order.
- The `query is` condition takes precedence over other conditions. If a newer rule contains a `query contains` condition, but an older rule has a `query is` condition, the `query is` rule is applied.

### Storefront requests

If an active rule containing a `query is` condition matches the search phrase, it is applied. If there are multiple matching rules with a `query is` condition, the most recently updated active rule is applied.
Otherwise, the most recently updated active rule is applied.

### Preview requests

Request made in [!DNL Adobe Commerce Optimizer] work slightly differently. When previewing [!DNL Adobe Commerce Optimizer], all rules are applied, including those expired and scheduled.

- If rule being previewed has a `query is` condition, it is applied.
- If rule being previewed does not have a `query is` condition, and a subsequent active, matching rule with a `query is` condition is found, the `query is` rule is applied.
- If rule being previewed does not have a `query is` condition, and no other rule with a `query is` condition is found, then the rule being previewed is applied.
