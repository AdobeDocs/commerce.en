---
title: Email templating
description: Learn how to configure transactional email sender addresses for your [!DNL Adobe Commerce as a Cloud Service] instance.
role: Admin
level: Beginner
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Email templating

{{accs-sandbox-experimental}}

[!DNL Adobe Commerce as a Cloud Service] has a new REST API endpoint, [`POST /V1/custom-email/send`](https://adobe-commerce-saas.redoc.ly/tag/custom-emailsend/), that allows you to trigger transactional emails on demand by specifying an email template ID, recipient email, and template variables. The API supports nested arrays as template variables for complex email content.

>[!IMPORTANT]
>
>The email templating feature is currently in development and will be expanded in future releases.

## Configure email sender addresses

Similar to how you [configure your email in the Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/store-email-addresses), you can configure email sender addresses through the API to override the default settings. The following configuration paths control the sender email address for each identity:

|Sender identity|Configuration path|
|---|---|
|General Contact|`trans_email/ident_general/email`|
|Sales Representative|`trans_email/ident_sales/email`|
|Customer Support|`trans_email/ident_support/email`|

>[!NOTE]
>
>Instance-specific email sender configurations take precedence over any default settings.

### Set configuration using the API

To set email sender addresses programmatically, first obtain an access token from [!DNL Adobe Identity Management Service] (IMS), then send a configuration request with the desired email settings.

**Step 1: Obtain an access token**

```bash
curl --request POST \
  --url https://ims-na1.adobelogin.com/ims/token \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data grant_type=authorization_code \
  --data client_id=<client_id> \
  --data client_secret=<client_secret> \
  --data code=<authorization_code>
```

**Step 2: Set sender email configuration**

Using the access token from the previous step, send a request to the provisioner endpoint with the instance ID and configuration values:

```bash
curl --request POST \
  --url <provisioner_base_url>/provisioner/set-config/ \
  --header 'Authorization: Bearer <access_token>' \
  --header 'Content-Type: application/json' \
  --data '{
  "tenant_id": "<instance_id>",
  "config": [
    {"path": "trans_email/ident_general/email", "value": "info@your-store.com"},
    {"path": "trans_email/ident_sales/email", "value": "sales@your-store.com"},
    {"path": "trans_email/ident_support/email", "value": "support@your-store.com"}
  ]
}'
```

**Response (200 OK):**

```json
{
  "data": {
    "success": true,
    "message": "Configuration batch set successfully for tenant: <instance_id>"
  }
}
```
