---
title: Delivery Estimates Extension Tutorial
description: Learn how to build a delivery date estimates extension for Adobe Commerce as a Cloud Service using App Builder, Edge Delivery Services, and AI-assisted development tools.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: yes
hidefromtoc: yes
---
# Delivery estimates extension tutorial

This tutorial guides you through building a delivery date estimates extension for [!DNL Adobe Commerce as a Cloud Service] using [!DNL Adobe App Builder], [!DNL Edge Delivery Services], and AI-assisted development tools. The extension fetches shipping time and delivery date estimates from an external API and displays them across the storefront.

You build two parts:

- **App Builder extension** — A backend-for-frontend (BFF) action that wraps an external delivery estimate API, a webhook that enriches shipping methods with delivery dates at checkout, and an Admin UI configuration page for managing settings without redeployment.
- **Storefront integration** — Delivery date estimates displayed on the product detail page (PDP), cart page, and checkout page using [!DNL Edge Delivery Services] drop-in components and a shared client module.

>[!NOTE]
>
>AI agents are non-deterministic. The prompts, questions, and outputs in this tutorial are examples. Your agent may produce different questions, requirements, or architecture proposals. Use the examples in this tutorial to steer the agent toward a similar outcome.

Before you begin, complete the [prerequisites](./tutorial-prerequisites.md). This tutorial uses the **checkout starter kit**. Verify that you have already cloned it and completed the setup steps described on the prerequisites page.

## Verify prerequisites

Verify that the following prerequisites are installed:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

If any of the preceding commands do not return the expected results, refer to the [prerequisites](./tutorial-prerequisites.md) for guidance.

Additionally, verify the following:

- You have an [!DNL Adobe Commerce as a Cloud Service] instance with product data. See [Commerce Cloud Service instances](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}.
- You have a storefront project connected to your [!DNL Commerce] instance. If you do not have one, follow the steps in [Create a storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}.
- The `aem` CLI is installed:

  ```bash
  npm install -g @adobe/aem-cli
  ```

- You have a **shopper account** — a registered customer in [!DNL Commerce] with a saved default shipping address. Delivery estimates on PDP and Cart pages are only shown to logged-in shoppers. Checkout shows estimates for all shoppers regardless of authentication status.

>[!IMPORTANT]
>
>This tutorial uses the **Checkout Starter Kit** (not the Integration Starter Kit). The Checkout Starter Kit provides webhook-based extensibility for payment, shipping, taxes, and events. Make sure you bootstrap from the Checkout kit.

## Set up the mock delivery estimate API

The extension calls an external delivery estimate API to get shipping date and time estimates. For this tutorial, you use a mock API so you can run the full flow without a real carrier account. Two options are available:

- **Option A: Pipedream workflow** — Free tier, quick setup, but has monthly invocation limits.
- **Option B: App Builder Runtime action** — No external dependency, created during the backend development steps.

>[!TIP]
>
>During development, you may start with Pipedream (Option A) and switch to a Runtime action (Option B) if you hit the free-tier invocation quota. Both options implement the same API contract.

### API specification

The mock API accepts a POST request and returns delivery date estimates with carrier, transit days, cutoff time, and a best estimation.

**Request body** (all fields optional for the mock):

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**Response (200 OK):**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**Error responses:** 401 (missing/invalid API key), 400 (invalid `ship_date` format), 503 (simulated downtime).

### Set up the mock

>[!BEGINTABS]

>[!TAB Pipedream workflow]

The Pipedream option uses Bearer token authentication and accepts a POST request to the workflow trigger URL.

| Item | Description |
|------|-------------|
| Base URL | The full Pipedream workflow trigger URL (for example `https://<id>.m.pipedream.net`) |
| Auth | `Authorization: Bearer <API_KEY>` |
| Method | POST |

{style="table-layout:auto"}

**Create the workflow:**

1. Create a new workflow in [Pipedream](https://pipedream.com){target="_blank"} (**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**).

1. Add an **HTTP / Webhook** trigger configured for POST. Pipedream assigns a webhook URL.

1. Add a **Run Node.js code** step and paste the following handler code:

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];

   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;

   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }

   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }

   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }

   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }

   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }

   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. (Optional) Add a `MOCK_API_KEY` environment variable in the workflow settings to enforce Bearer token auth. If not set, any request is accepted.

1. Deploy the workflow. Your endpoint is the webhook trigger URL.

**Test the mock:**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB App Builder Runtime action]

An alternative is to deploy the mock as a Runtime action within the same [!DNL App Builder] project. This approach has no external dependency and no invocation quotas.

Prompt the agent to create the mock action:

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- add it to a separate package
- use the code in docs/pipedream as inspiration
```

The agent creates `actions/mock-delivery-api/index.js` with the same API contract as the Pipedream option. After deploying, the endpoint is:

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

Auth is validated against a `MOCK_API_KEY` environment variable in `.env`.

>[!ENDTABS]

## Extension development

This section guides you through developing the [!DNL App Builder] backend for the delivery estimates extension. The backend provides three actions:

| Action | Type | Purpose |
|--------|------|---------|
| `delivery-estimates` | Standalone web action | BFF for storefront — PDP and cart call this for delivery dates |
| `shipping-methods` | Webhook action | Enriches shipping rates with delivery dates in `additional_data` at checkout |
| `delivery-estimates-config` | Admin backend action | CRUD for configuration stored in `aio-lib-state` |

{style="table-layout:auto"}

1. Navigate to the MCP settings in your coding agent. For example, in Cursor, go to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Verify that the `commerce-extensibility` toolset is enabled without errors. If you see errors, toggle the toolset off and on.

   >[!NOTE]
   >
   >When working with AI-assisted development tools, expect natural variations in the code and responses generated by the agent.
   >If you encounter any issues with your code, you can always ask the agent to help you debug it.

1. If you have any documentation added to Cursor's context, disable it. Navigate to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** and delete any documentation listed.

### Step 1: Provide the initial prompt

Give the agent the external API specification for context and prompt it to begin. Telling the agent to stop and ask questions helps you steer the implementation early.

Enter the following prompt in the agent's chat window:

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date/time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
In order to implement this feature we will use the skills in this workspace for backend code, and a separate workspace with storefront skills. Please be only concerned about backend skills and be mindful to create an API_SPEC to hand work over to the storefront skills.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>Referencing the external API spec file (`@docs/API_SPEC.md`) in the prompt gives the agent concrete context about the third-party API contract. The agent uses this to design the BFF action, shared HTTP client, and Admin UI configuration fields. Telling the agent to STOP and ask questions triggers the guided workflow and helps you steer the implementation early.

### Step 2: Answer the agent's questions

The agent returns with a series of clarifying questions covering topics such as target environment (PaaS vs SaaS), scope (standalone BFF action, webhook enrichment, or both), origin address source, caching strategy, and testing preference. The following example shows typical questions and answers. Your agent may ask different questions, but the topics are generally the same.

**Example agent questions:**

1. **Target environment** — Are you building for PaaS (on-premise) or SaaS (Adobe Commerce as a Cloud Service)?
1. **Scope** — Should this be a standalone BFF action (storefront calls it directly), webhook enrichment (extend shipping methods at checkout), or both?
1. **Admin configurability** — Should settings like API URL, API key, and origin address be configurable via the Commerce Admin, or stored in `.env`?
1. **Origin address** — Where does the ship-from (warehouse) address come from? Should it be a static configuration or dynamically resolved?
1. **Caching** — Should delivery estimates be cached on the server side to reduce calls to the external API? If so, what TTL?

**Example answers:**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call directly the 3rd party API - or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Can we make this configurable via Adobe Commerce Admin UI. Let's use a SPA that uses Admin UI SDK to integrate with the admin, and since we are adding this config screen, let's make configurable anything else that makes sense to avoid redeployments when changing settings
```

>[!TIP]
>
>Asking the agent whether the storefront should call the third-party API directly or go through a runtime action triggers a useful architectural discussion. The agent explains the benefits of the BFF (Backend-for-Frontend) pattern: the API key stays server-side, CORS is handled, caching is centralized, and you get vendor abstraction. Asking for Admin UI configurability pushes the agent to store all settings in `aio-lib-state` instead of `.env`, eliminating redeployments when changing settings.

>[!NOTE]
>
>Your agent may ask different questions. Use these answers as guidance for steering the agent toward the same functional outcome: a BFF action for storefront calls, a shipping-methods webhook for checkout enrichment, and an Admin UI config page that stores settings in `aio-lib-state`.

### Step 3: Review requirements and architecture

The agent generates requirements and architecture documents for you to review. Verify that the requirements match the answers you provided and that the architecture covers:

- A **BFF action** (`delivery-estimates`) — A standalone web action that the storefront calls from PDP and cart pages. It reads configuration from `aio-lib-state`, calls the external delivery estimate API, and returns formatted estimates.
- A **webhook action** (`shipping-methods`) — Enriches shipping rates with delivery dates in `additional_data` during checkout. Uses the `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` webhook method.
- An **Admin config action** (`delivery-estimates-config`) — CRUD for configuration (API URL, API key, origin address, carriers, cache TTL) stored in `aio-lib-state`.
- **Shared libraries** — An HTTP client for the external API and a config module for reading/writing `aio-lib-state`.

>[!NOTE]
>
>AI agents are non-deterministic and their behaviors differ depending on the model and IDE. You may get a different set of questions that produce a different set of requirements and architecture. If so, try to steer the agent in a direction such that the implementation closely matches what is presented in this tutorial before proceeding.

### Step 4: Select an implementation plan

The agent gives you the option of creating a detailed implementation plan or doing a direct implementation.

- If you want a reviewable plan that you can execute in phases with more control, select the first option.
- If you want the agent to do the full implementation with minimal intervention, select the second option.

### Step 5: Clean up and deploy

Once the agent completes the implementation, it proceeds to cleanup. Since only the Shipping domain is in use, the agent removes unused scaffolding:

- Payment actions and config (`validate-payment/`, `filter-payment/`, `payment-methods.yaml`)
- Tax actions and config (`collect-taxes/`, `collect-adjustment-taxes/`, `tax-integrations.yaml`)
- Events actions and config (`commerce-events/`, `3rd-party-events/`, `events.config.yaml`)
- Generic scaffolding (`generic/`)
- Admin UI SPA components from other domains (for example, tax-related pages and hooks)
- Unused scripts, test files, and environment variables

>[!TIP]
>
>Ask the agent to also check the Admin UI SPA for leftovers from other domains. The Tax Classes page and its hooks may still be present from the starter kit scaffolding and need to be removed.

After cleanup, deploy using these steps **in this order**:

```bash
# 1. Copy env template and fill in credentials
cp env.dist .env

# 2. Select your App Builder workspace
aio app use --merge

# 3. Sync OAuth credentials from workspace
npm run sync-oauth-credentials

# 4. Deploy the extension
aio app deploy

# 5. Register shipping carriers in Commerce
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>The order matters. Steps 1–3 are prerequisites to deployment — `aio app deploy` fails without credentials configured. Do not skip or reorder them.

### Step 6: Configure webhook and Admin UI

After deploying, configure the shipping webhook. The agent can create a script to subscribe programmatically:

```bash
npm run subscribe-webhook
```

This subscribes the webhook with the following settings:

| Field | Value |
|-------|-------|
| Webhook Method | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Webhook Type | `after` |
| Required | Optional (allows fallback to default shipping) |
| Timeout | 5000ms |

{style="table-layout:auto"}

>[!NOTE]
>
>For SaaS, the webhook method name drops `magento.` from the path. PaaS uses `plugin.magento.out_of_process_shipping_methods...` while SaaS uses `plugin.out_of_process_shipping_methods...`.

Next, configure the Admin UI:

1. Enable the **Admin UI SDK** (**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**).

1. Configure extensions — select your [!DNL App Builder] workspace and extension.

1. Click **[!UICONTROL Refresh registrations]**.

1. Navigate to **[!UICONTROL Apps]** > **[!UICONTROL Delivery Estimates]** in the [!DNL Admin] sidebar.

1. Fill in the configuration: enable the feature, set the API URL, API key, origin address, default carriers, cache TTL, and carrier code mapping.

   ![Delivery Estimates configuration page in Commerce Admin](../assets/delivery-estimates-admin-config.png){width="600" zoomable="yes"}

### Step 7: Test the extension

Test the delivery estimates BFF action directly:

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

The response should look similar to:

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

![Runtime action logs in Adobe Developer Console showing successful BFF invocation](../assets/delivery-estimates-bff-logs.png){width="600" zoomable="yes"}

### Create the service contract

Now that the backend is complete, ask the agent to create a service contract for the storefront work:

```shell-session
Can you produce a spec, let's call it STOREFRONT_API_SPEC so I can use it in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

The agent produces `docs/STOREFRONT_API_SPEC.md` with the full BFF endpoint contract (request/response format, example payloads, error handling) and a ready-to-use prompt for the storefront workspace. Copy this file into your storefront project before starting the storefront dev steps.

>[!TIP]
>
>Having the agent generate both a service contract **and** a prompt for the other workspace ensures a clean handoff between the backend and storefront teams (or agents). The storefront agent can start working immediately without needing to ask questions about the API.

## Connect to the storefront

This section guides you through implementing the storefront portion of the delivery estimates extension using [!DNL Edge Delivery Services] and AI-assisted development tools. You add delivery date estimates to the PDP, cart page, and checkout page.

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Storefront prerequisites

Before starting the storefront integration, verify you have the following:

- A storefront project connected to your [!DNL Commerce] instance
- Commerce storefront AI tools [installed using the CLI](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- The `STOREFRONT_API_SPEC.md` file copied into your storefront project's `docs/` folder

### Step 1: Validate the environment

Open your `config.json` file and verify that the values for `commerce-core-endpoint` and `commerce-endpoint` point to your [!DNL Adobe Commerce as a Cloud Service] GraphQL endpoint.

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Step 2: Provide the initial prompt

With the service contract already in your project, prompt the agent to implement the storefront integration. Use **Plan** mode if available in your agent, to prevent the agent from proceeding without a plan.

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services / storefront dropins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in docs/STOREFRONT_API_SPEC.md — please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's additional_data by a webhook. No API call needed — just read additional_data from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>The prompt is detailed because the full API contract is already available from the backend agent. By referencing `@docs/STOREFRONT_API_SPEC.md`, the agent knows the exact endpoint URL, request/response format, and error handling. The explicit requirements list prevents the agent from inventing scope. Specifically requesting plan mode triggers the phased workflow that helps you steer the implementation early.

### Step 3: Answer clarifying questions

The agent returns with questions about authentication scope, checkout approach, and styling. The following example shows typical questions and answers.

**Example agent questions:**

1. **Anonymous vs logged-in users** — Should PDP/Cart estimates show for all shoppers or only authenticated ones?
1. **Checkout approach** — The ShippingMethods drop-in container does not expose `additional_data`, so the agent proposes two options:
   - **Option A:** Call the BFF at checkout and DOM-inject delivery dates (simpler, consistent with PDP/Cart)
   - **Option B:** Extend the checkout GraphQL fragment via `overrideGQLOperations` to include `additional_data`
1. **Styling** — Emojis vs existing design tokens

**Example answers:**

```shell-session
1 & 2. Is it possible to implement only for users logged in? Does it make sense?
3. Let's do A if feasible
4. Use anything that matches the current styling
```

>[!TIP]
>
>Showing estimates only for logged-in shoppers is a pragmatic choice — the agent can use the shopper's default shipping address automatically (via GraphQL), so no zip code input is needed. Anonymous shoppers on PDP and Cart would require entering a postal code, which adds friction. At checkout, all shoppers see delivery dates because the shipping address has already been entered.

>[!NOTE]
>
>Your agent may ask different questions. Use these answers as guidance:
>
>- PDP and Cart estimates should show only for logged-in shoppers (no zip code input needed).
>- For checkout, use Option A (BFF call + DOM injection) for simplicity.
>- Use existing design tokens for styling.

### Step 4: Review requirements and architecture

The agent designs a shared module architecture. Verify that it covers:

| Component | Purpose |
|-----------|---------|
| `scripts/delivery-estimates.js` | Shared module — BFF client, caching (sessionStorage, 30-min TTL), date formatting, countdown logic, customer address lookup, carrier mapping |
| PDP integration | Shows "Get it by [date]" with optional countdown between price and description |
| Cart integration | Shows date range ("Thu, Mar 12 – Fri, Mar 13") in right column above order summary |
| Checkout integration | Calls BFF when shipping step is active, DOM-injects delivery dates via `MutationObserver` |

{style="table-layout:auto"}

Key design decisions to verify:

- All BFF calls are non-blocking — pages render first, estimates appear asynchronously.
- All failures are silent — `console.debug` only, no shopper-facing errors.
- `CARRIER_MAP` maps Commerce carrier codes (DPS, Fedex) to BFF carrier codes (standard, express).
- Dynamic `import()` keeps the delivery module out of the critical rendering path.

>[!NOTE]
>
>AI agents are non-deterministic and their behaviors differ depending on the model and IDE. You may get a different set of questions that produce a different set of requirements and architecture. If so, try to steer the agent in a direction such that the implementation closely matches what is presented in this tutorial before proceeding.

### Step 5: Select an implementation plan

The agent gives you the option of creating a detailed implementation plan or doing a direct implementation.

- If you want a reviewable plan that you can execute in phases with more control, select the first option.
- If you want the agent to do the full implementation with minimal intervention, select the second option.

During implementation, the agent creates and modifies the following files:

**New file:**

- `scripts/delivery-estimates.js` — Shared module with `fetchDeliveryEstimates()`, `getCustomerShippingAddress()`, `formatDeliveryDate()`, `buildCountdownText()`, `findEstimateForCarrier()`

**Modified files:**

- `blocks/product-details/product-details.js` + `.css` — Delivery estimate div in the right column, async fetch after main render
- `blocks/commerce-cart/commerce-cart.js` + `.css` — Delivery estimate div above order summary
- `blocks/commerce-checkout/commerce-checkout.js`, `containers.js`, `.css` — `MutationObserver`-based DOM injection for shipping method labels

Watch the code being generated and ask questions or redirect the agent as needed.

### Step 6: Start the server and test

After the agent completes the implementation, start the development server and test the delivery estimates.

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, log in to your shopper account. Delivery estimates on PDP and Cart require an authenticated session with a saved default shipping address.

1. Navigate to a product page. Verify the following results:

   | Page | Expected result | Auth required |
   |------|-----------------|---------------|
   | PDP | "Get it by Thursday, March 12" with optional countdown | Yes (logged-in only) |
   | Cart | "Estimated delivery: Thu, Mar 12 – Fri, Mar 13" | Yes (logged-in only) |
   | Checkout | "Estimated delivery: Thursday, March 12" per shipping method | No (address entered at checkout) |

   {style="table-layout:auto"}

   ![Product detail page showing delivery estimate below the add to cart button](../assets/delivery-estimates-pdp.png){width="600" zoomable="yes"}

   ![Cart page showing delivery date range above order summary](../assets/delivery-estimates-cart.png){width="600" zoomable="yes"}

   ![Checkout page showing delivery dates next to each shipping method](../assets/delivery-estimates-checkout.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Shipping methods without a matching carrier (for example, Flat Rate) show no estimate. This is by design — only carriers mapped in `CARRIER_MAP` get delivery dates.

You can do manual testing or ask the agent to use its browser capabilities to test for you:

```shell-session
run through browser testing. use the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### Step 7: Clean up

If you want to skip testing or after finishing testing, the agent asks if you want to proceed to cleanup. After you agree or tell the agent to clean up, the agent archives any documentation artifacts produced during implementation.

## Troubleshooting

Use the following tips if you encounter issues during the tutorial.

### Backend (App Builder)

| Symptom | Cause | Fix |
|---------|-------|-----|
| Admin UI config action returns `400 Bad Request` with "Request defines parameters that are not allowed (reserved properties)" | The frontend hook is sending `__ow_method` in the request body. Properties prefixed with `__ow_` are reserved by OpenWhisk and rejected when the action has `final: true`. | Send a custom `method` property instead of `__ow_method`. The backend action reads `params.method` first, then falls back to `params.__ow_method` (which Runtime provides automatically). |
| `aio app deploy` fails with "maxVersion is required in productDependencies" | The CLI validation requires both `minVersion` and `maxVersion` in `app.config.yaml` product dependencies. | Add a `maxVersion` value to each `productDependencies` entry in `app.config.yaml`. |
| Deployment command fails | Credentials not configured before deploy. `.env`, workspace selection, and OAuth sync must happen first. | Follow the correct order: `cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`. |

{style="table-layout:auto"}

### Storefront (Edge Delivery Services)

| Symptom | Cause | Fix |
|---------|-------|-----|
| PDP delivery estimate not appearing for logged-in shoppers | The PDP block does not initialize the `account` drop-in, so `getCustomerAddress()` fails silently and no estimate is fetched. | Use `CORE_FETCH_GRAPHQL.fetchGraphQl()` directly to query shopper addresses instead of relying on the account drop-in API. This works on any page. |
| PDP still not showing after GraphQL fix | Typo in method name: `CORE_FETCH_GRAPHQL.fetch()` was used instead of `CORE_FETCH_GRAPHQL.fetchGraphQl()`. | Use the correct method name: `fetchGraphQl` (capital Q, lowercase l). |
| Checkout delivery dates not appearing on first load | The `checkout/updated` event listener was registered after `checkout/initialized` had already fired, so the initial data was missed. | Add a `checkout/initialized` listener with `{ eager: true }` to catch events emitted before registration. Keep the `checkout/updated` listener for subsequent changes. |
| Cart delivery estimate not appearing | `block.appendChild(fragment)` moves all children out of the fragment, so `fragment.querySelector('.cart__delivery-estimate')` returns null. | Query from `block` instead of `fragment` after the append operation. |
| Flat Rate shipping shows no delivery date at checkout | By design — `CARRIER_MAP` only maps DPS to standard and Fedex to express. Flat Rate has no corresponding carrier in the external API. | Not a bug. To add estimates for other carriers, extend the `CARRIER_MAP` in `scripts/delivery-estimates.js` and configure the carrier in the backend extension. |

{style="table-layout:auto"}

### Commerce SaaS sandbox

| Symptom | Cause | Fix |
|---------|-------|-----|
| Webhook returns `429 Too Many Requests` | [!DNL App Builder] workspace is in debug mode, which has strict per-minute rate limits. [!DNL Commerce] recalculates shipping rates frequently during checkout, exhausting the quota. | Deploy to a Production workspace (`aio app use` to switch, then `aio app deploy`). Production workspaces do not have debug rate limits. |
| Webhook soft timeout warning (>1000ms) | The shipping-methods webhook action took longer than the [!DNL Commerce] 1000ms soft timeout. | Enable server-side caching in `aio-lib-state` more aggressively, or increase the webhook timeout in [!DNL Commerce Admin] (Commerce Webhooks configuration). |

{style="table-layout:auto"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

- **Mock API setup:** Creating a mock delivery estimate API using Pipedream or an [!DNL App Builder] Runtime action.
- **BFF pattern:** Building a backend-for-frontend action that wraps the external API, keeps credentials server-side, and centralizes caching.
- **Webhook enrichment:** Extending the shipping-methods webhook to inject delivery dates into each shipping option at checkout.
- **Admin UI configurability:** Adding a configuration page using the [!DNL Admin UI SDK] so merchants can manage API settings, origin address, and carrier mappings without redeployment.
- **Service contracts:** Creating API contracts that bridge backend extensions and storefront implementations.
- **Storefront integration:** Displaying delivery estimates on PDP ("Get it by"), cart (date range), and checkout (per shipping method) using a shared client module.
- **Non-blocking UX:** Ensuring delivery estimates never block the purchase flow — pages render first and estimates appear asynchronously.

## Next steps

Use the following suggestions to extend your delivery estimates service:

- **Connect a real carrier API:** Replace the mock with a live shipping API such as UPS, FedEx, or USPS by changing the Service URL and API key in the [!DNL Admin UI].
- **Support anonymous shoppers:** Add a postal code input on PDP and cart pages so shoppers who are not logged in can also see delivery estimates.
- **Extend carrier mappings:** Add more carrier codes to `CARRIER_MAP` to display delivery dates for additional shipping methods.
- **Add server-side caching:** Implement `aio-lib-state` caching in the BFF action to reduce calls to the external API for repeated origin/destination pairs.
- **Show estimates in order confirmation:** Display the estimated delivery date on the order confirmation page and in transactional emails.
