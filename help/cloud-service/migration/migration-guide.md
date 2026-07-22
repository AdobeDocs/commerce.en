---
title: Run a Bulk Data Migration
description: Learn how to configure and run a bulk data migration from an Adobe Commerce PaaS or on-premises instance to Adobe Commerce as a Cloud Service with the CLI.
feature: Cloud
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
---
# Run a bulk data migration

{{bulk-data-early-access}}

This guide is a step-by-step operational reference for running a data migration from an [!DNL Adobe Commerce] PaaS or on-premises installation to [!DNL Adobe Commerce as a Cloud Service] using the bulk data migration tool. The steps cover the typical migration workflow. Actual configuration values and environment-specific details vary depending on your setup.

Before you begin, confirm that you have completed every item in the [Customer readiness checklist](readiness-checklist.md) and verified API access with the [Migration service access guide](cdms-access.md).

>[!NOTE]
>
>Comprehensive technical documentation covering the tool's architecture, internal design, data transformation framework, and integrity testing framework is provided as part of the tool distribution package.

## Prerequisites

- **[!DNL Docker]** and **[!DNL Docker Compose]** must be installed on the machine where you run the migration.
- The user running the migration must have permission to execute `docker` and `docker compose` (or the legacy `docker-compose`) commands. On [!DNL Linux], the user must be in the `docker` group. On [!DNL macOS] and [!DNL Windows], [!DNL Docker Desktop] must be running and accessible. The migration CLI invokes [!DNL Docker] repeatedly, and permission errors here block the run.
- Core configuration must be consistent between source and target before you run the migration. Core configuration data, such as store settings and system configuration, is not migrated by this tool. Set it up on the target independently and align it with the source before migration.

## Set up the tool package

>[!VIDEO](https://video.tv.adobe.com/v/3496121)

1. Extract the contents of `ccsaas-migration-tools.tar.gz`.

1. Run all commands from the extracted `ccsaas-migration-tools` folder, where `bin/console` lives.

1. Ensure the folder is writable for logs, cache, [!DNL Composer], and generated files.

   Change ownership of all files and subfolders under that directory to the operating system user who runs the migration, so the tool can read and write consistently. For example, on [!DNL Linux]: `chown -R <user>:<group> <project-root>`.

1. Create the `.env` and `.my.cnf` files in the project root by copying the example files (`.example.env` to `.env` and `.my.cnf.example` to `.my.cnf`), and then fill in the values described in the following sections.

### Example configuration files

The `.example.env` and `.my.cnf.example` files in the repository root are the starting point for your configuration. Copy each file to its working name and fill in the required values.

| Example file | Copy to | What it covers |
| --- | --- | --- |
| `.example.env` | `.env` | Annotated list of all supported environment variables: performance (threads, chunks, `MEMORY_LIMIT_PER_THREAD`, timeouts), CDMS, IMS, target SaaS, source URLs and OAuth, tests, logging, S3, migration strategy, and optional PaaS values (`MAGENTO_CLOUD_CLI_TOKEN` when `id=` is set in `.my.cnf`). |
| `.my.cnf.example` | `.my.cnf` | Reference `[section]` layouts for on-premises [!DNL MySQL] and PaaS (`id=project:environment`). The `[section]` name must match `SOURCE_CONNECTION_NAME` in `.env`. Fields include `user`, `password`, `host`, `port`, `database`, and `id=` for PaaS. |

## Configure the environment file

The `.env` file in the project root is the migration and extraction configuration. It drives the CLI pipeline, including source and target URLs, OAuth, the remote CDMS connection, SaaS and IMS authentication, and other switches.

>[!NOTE]
>
>Do not include trailing slashes in URLs. For example, use `https://example.com` instead of `https://example.com/`.

Edit the `.env` file and set at least the following values correctly. For the full list of supported variables, refer to the inline annotations in `.example.env`.

### Configure source OAuth credentials

>[!VIDEO](https://video.tv.adobe.com/v/3496142)

These four values sign requests from the migration tool to the source store APIs. To obtain them, open the source [!UICONTROL Admin] and go to [!UICONTROL System] > [!UICONTROL Extensions] > [!UICONTROL Integrations]. Create or open an integration, and then copy the values into `.env`:

```text
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Set the Magento Cloud CLI token

>[!NOTE]
>
>This applies to PaaS source instances only. The tool detects the source type automatically from `.my.cnf`. If the `SOURCE_CONNECTION_NAME` section contains an `id=` line (for example, `id=project:production`), the source is PaaS and `MAGENTO_CLOUD_CLI_TOKEN` is required. For on-premises sources with no `id=`, this token is not needed and tunnel setup is skipped.

1. Go to `https://accounts.magento.cloud` and sign in.

1. Select your avatar, and then select [!UICONTROL Account Settings].

1. Go to the [!UICONTROL API Tokens] section.

1. Select [!UICONTROL Create an API token], give it a descriptive name, and copy the generated token.

1. Set the token in `.env`:

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>If this is your first time using the [!DNL Magento Cloud] CLI, you must also add your SSH public key to your [!DNL Adobe Commerce] Cloud account. See the [Secure connections guide](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) for instructions.

### Align Commerce Admin settings

Before migration, ensure the following settings are consistent between source and target.

1. For B2B-enabled stores only, go to [!UICONTROL Stores] > [!UICONTROL Configuration] > [!UICONTROL General] > [!UICONTROL B2B Features] and set each option as shown.

   The exact [!UICONTROL Admin] path can differ by [!DNL Magento] version. Use configuration search for **B2B** if the menus do not match.

   | Option | Value |
   | --- | --- |
   | Enable Company | Yes |
   | Enable Shared Catalog | Yes |
   | Enable B2B Quote | No |
   | Enable Shared Catalog direct products price assigning | No |
   | Enable Quick Order | Yes |
   | Enable Requisition List | Yes |

1. Go to [!UICONTROL Stores] > [!UICONTROL Configuration] > [!UICONTROL Sales] > [!UICONTROL Sales] > [!UICONTROL Orders, Invoices, Shipments, Credit Memos Archive] and set [!UICONTROL Enable archiving] to [!UICONTROL Yes].

### Configure target SaaS and IMS credentials

>[!VIDEO](https://video.tv.adobe.com/v/3496167)

These are the [!DNL Adobe Commerce as a Cloud Service] IMS and API settings for the target. You need the tenant ID, organization ID, IMS OAuth Server-to-Server credentials, and the correct IMS host for your environment. Coordinate with your Adobe team for organization, tenant, and profile access. Do not attempt to infer or estimate sensitive values.

#### Generate IMS credentials

Use the [Adobe Developer Console](https://developer.adobe.com/console/). You need [!UICONTROL Developer] or [!UICONTROL Admin] access on the Adobe organization to create projects. A basic user login is not enough to add APIs.

1. Create a project, or open an existing one, and then select [!UICONTROL Add API].

1. Choose [!UICONTROL Adobe Commerce as a Cloud Service] and continue.

1. Select [!UICONTROL OAuth Server-to-Server] as the authentication type and continue.

1. Select the product profile that your Adobe team expects for this tenant, and then select [!UICONTROL Save configured API].

1. In the project sidebar, open [!UICONTROL OAuth Server-to-Server] (or [!UICONTROL Credentials]), and then copy the client ID and client secret into `.env` as `ADOBE_IMS_CLIENT_ID` and `ADOBE_IMS_CLIENT_SECRET`.

The IMS token endpoint (`ADOBE_IMS_URL`) must match the credential's environment.

| Tier | Typical `ADOBE_IMS_URL` |
| --- | --- |
| QA or staging-style | `https://ims-na1-stg1.adobelogin.com` |
| Pre-production or production | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>`na1` in these URLs represents the region where your target instance is provisioned. Replace it with the appropriate region identifier if your instance is provisioned in a different region.

`ADOBE_IMS_META_SCOPES` must match the scopes provisioned on that credential. The `.example.env` file includes the full comma-separated scope string as a reference. Change it only if Adobe instructs you to.

#### Map Adobe I/O credentials to the environment file

In [!DNL Developer Console], the OAuth Server-to-Server values are presented as a client ID and a client secret, corresponding to the following JSON structure:

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

Map them into `.env` (example placeholders):

```text
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

The SaaS API hosts differ between pre-production and production. `TARGET_INSTANCE_REST_URL` and `TARGET_INSTANCE_GRAPHQL_URL` must use the same Commerce API environment as your migration, either pre-production or production. Do not mix one tier with the other tier's CDMS or tenant.

| Environment | Typical host in `TARGET_INSTANCE_*_URL` |
| --- | --- |
| Pre-production or sandbox | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| Production | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>`na1` in these URLs represents the region where your target instance is provisioned. Replace it with the appropriate region identifier if your instance is provisioned in a different region.

```text
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

For production SaaS hosts, replace `na1-sandbox` with `na1` in both `TARGET_INSTANCE_*` URLs. Use the matching `ADOBE_IMS_URL` for that tier, as shown in the previous table.

### Set the CDMS endpoint

Point the migration tool at the CDMS API host that matches the environment you are migrating to. Set `CDMS_HOST` (and typically `CDMS_PORT=443`) in `.env`. Use one host, either pre-production or production, not both.

| Environment | When to use | `CDMS_HOST` |
| --- | --- | --- |
| Pre-production | Pre-production or sandbox-style runs, non-production CDMS | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| Production | Live production migration or cutover | `https://commerce-data-migration-service-prod-external.adobe.io` |

Set or uncomment the block that matches your run:

```text
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://commerce-data-migration-service-prod-external.adobe.io
# CDMS_PORT=443
```

### Set the store code

`STORE_CODE` is the store view code used by the migration tool for source instance REST API calls, synthetic test customer creation, and data cleanup. It is also sent as the `x-store-code` header during the loading phase.

`STORE_CODE` defaults to `default` in `.example.env`. Verify that this matches your source instance's default store view code. To check, in the source [!UICONTROL Admin] go to [!UICONTROL Stores] > [!UICONTROL All Stores] and look at the [!UICONTROL Code] column for the store view that should be used. If the code shown there is not `default`, update `STORE_CODE` in `.env` to match.

## Configure the database connection file

>[!VIDEO](https://video.tv.adobe.com/v/3496152)

The `.my.cnf` file supplies [!DNL MySQL] connection settings for the extraction side of the migration tool. Create it by copying `.my.cnf.example` to `.my.cnf` in the project root. The section name must match `SOURCE_CONNECTION_NAME` in `.env`.

For an on-premises or self-hosted source:

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>The machine running the migration tool must have direct network access to the source database. The tool does not establish or verify on-premises connectivity automatically. Confirm that the host, port, and credentials are reachable from the migration machine before you run any migration command.

For a PaaS source ([!DNL Adobe Commerce] Cloud):

```ini
[<connection-name>]
id=<project_id>:<environment>
```

The `id=` field tells the tool that the source is PaaS and triggers tunnel setup using `MAGENTO_CLOUD_CLI_TOKEN`. The `project_id` and `environment` values are available in the [!DNL Magento Cloud] Console or through the `magento-cloud project:list` and `magento-cloud environment:list` commands.

## Prepare the network and instances

### Source

HTTP Basic Auth in front of the store can block API and tool traffic. Ensure it is disabled for the source URL used by the migration, or that the tool's paths are permitted, so REST and GraphQL requests can reach the store.

### Maintain source database stability during extraction

While the tool extracts data from the source database, no other processes should write to it. Concurrent writes can result in an inconsistent snapshot.

- Stop [!DNL Magento] cron on the source, and any operating-system schedulers that run `bin/magento` or other writers, for the extraction window, or ensure they cannot run during extraction.
- Review other integrations, such as ERP, OMS, PIM, custom jobs, and third-party APIs that write to the same database. Pause or block writes for the extraction window so nothing mutates tables while extraction runs.
- This complements maintenance mode and tunnel or database access. Together they reduce storefront and API traffic. Cron and integrations are separate sources of writes that you must control explicitly.

### Target

If the target catalog must be cleared before migration, delete products in [!UICONTROL Admin] in small batches, for example 200 at a time, to avoid duplicate catalog conflicts and bulk-delete timeouts.

## Build and run the migration

Work from the extracted project directory with write access.

### Keep the session alive over SSH

If you connect over SSH, a dropped network can kill your shell and interrupt a long migration. GNU `screen` keeps the session alive on the server:

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

You can also use `tmux` if it is available on the server.

### Build the Docker image

Build the [!DNL Docker] image used by `bin/console`, which contains PHP, the CLI, and dependencies. Run this before the first run, or after Dockerfile or base image changes.

```bash
./bin/console build
```

### Start the backing services

Start the [!DNL Docker Compose] backing services for the tool, such as the local test database and, when enabled in `.env`, optional local services. The exact services depend on your configuration. Run this after a successful build and before the shell, migration, or phased commands.

```bash
./bin/console start
```

### Initialize the CLI container

Start the CLI container once so the entrypoint can finish setup, such as a [!DNL Composer] install if needed, against your mounted project. Run this once before the first migration run in a fresh environment.

```bash
./bin/console shell
exit
```

### Run the migration

The tool supports two migration approaches. Choose the one that fits your use case.

#### Option A: single-phase migration

No maintenance mode is required on the source instance. Run the full migration pipeline with a single command:

```bash
./bin/console migration
```

The command runs all pipeline steps automatically, end to end, in the following order.

| Step | What happens |
| --- | --- |
| 1 | **Configuration check** — validates environment variables and tool setup. |
| 2 | **Environment initialization** — starts [!DNL Docker] services, opens PaaS cloud tunnels (if applicable), and runs unit tests. |
| 3 | **Integration tests and CDMS initialization** — runs integration tests and initializes the CDMS API connection. |
| 4 | **Create migration** — registers the migration with CDMS and waits for target schema analysis. The migration ID is saved to `.migration_id`. |
| 5 | **Functional tests and test data generation** — runs functional tests and generates synthetic test data on the source for integrity verification (if enabled). |
| 6 | **Data extraction** — extracts data from the source instance. |
| 7 | **Load to target** — loads extracted data into the target [!DNL Adobe Commerce as a Cloud Service] instance. Staging views are cleaned up on the source and source test data is removed through REST in parallel with the load. |
| 8 | **Data integrity verification** — triggers checksum verification and runs local API verification tests. Results are logged, and failures do not stop the pipeline. |
| 9 | **Test data cleanup on target** — removes synthetic test data from the target instance. |
| 10 | **Process results** — generates a migration summary and optionally downloads artifacts from storage. |

Use this option when no maintenance window is required, which is typical for end-to-end dry runs, dev or sandbox environments, or any migration where the source can remain live during extraction.

>[!WARNING]
>
>Do not use this option when a frozen source is required, for example any production migration where new orders or data changes must not occur during extraction. Use Option B instead. Do not use this command as a step inside the phased maintenance workflow.

#### Option B: multi-phase migration with maintenance mode

Maintenance mode is required on the source instance to ensure data consistency during extraction. The migration is split into distinct phases that you must run in order.

>[!NOTE]
>
>Two different CLIs are involved. The `./bin/console` commands run from the migration tool project root (this package). The `bin/magento maintenance:*` commands run on the source [!DNL Adobe Commerce] application server, through SSH to the install root, or through the [!UICONTROL Admin]. The tool does not issue [!DNL Magento] maintenance commands on your behalf.

| Phase | Who runs it | Source state |
| --- | --- | --- |
| 1. `migration:before-maintenance` | Tool | Live — do not enable maintenance yet |
| 2. Enable maintenance mode | Manual | Transition to frozen |
| 3. `migration:during-maintenance` | Tool | Frozen — do not disable maintenance during this phase |
| 4. Disable maintenance mode | Manual (conditional) | Transition source instance back to live |
| 5. `migration:cleanup` (optional) | Tool | Live — must be out of maintenance |

**Phase 1 — Before maintenance (source is live)**

Run while the source instance is live and accepting traffic. REST and GraphQL to the source must be fully available. Do not enable maintenance mode before this phase completes.

```bash
./bin/console migration:before-maintenance
```

| Step | What happens |
| --- | --- |
| 1 | **Configuration check** — validates environment variables and tool setup. |
| 2 | **Environment initialization** — starts [!DNL Docker] services, opens PaaS cloud tunnels (if applicable), and runs unit tests. |
| 3 | **Integration tests and CDMS initialization** — runs integration tests and initializes the CDMS API connection. |
| 4 | **Create migration** — registers the migration with CDMS and waits for target schema analysis. The migration ID is saved to `.migration_id`. |
| 5 | **Functional tests** — runs functional tests against the live source. |
| 6 | **Test data generation** — creates synthetic test customers and orders on the source for integrity verification (if enabled). |

When this completes, proceed to Phase 2.

**Phase 2 — Enable maintenance mode (manual)**

Before you run Phase 3, enable maintenance mode on the source and pause all activities that write to or impact the database, including scheduled jobs, third-party integrations, order processing, and media asset synchronization.

On the source Commerce server (install root):

```bash
bin/magento maintenance:enable
```

After maintenance mode is active and all database-impacting activities are paused, proceed to Phase 3.

**Phase 3 — During maintenance (source is frozen)**

Run with the source instance in maintenance mode. The source must remain frozen for the entire duration of this phase. Do not disable maintenance mode until Phase 3 completes successfully.

```bash
./bin/console migration:during-maintenance
```

| Step | What happens |
| --- | --- |
| 1 | **PaaS cloud tunnel setup** — for PaaS source instances, reopens cloud tunnels and verifies database connectivity. Skipped automatically for on-premises instances. |
| 2 | **Data extraction** — extracts data from the frozen source instance. |
| 3 | **Staging view cleanup** — removes staging views from the source using a direct database connection (safe under maintenance mode). |
| 4 | **Load to target** — loads extracted data into the target [!DNL Adobe Commerce as a Cloud Service] instance and waits for completion. |
| 5 | **Data integrity verification** — triggers CDMS checksum verification and runs local API verification tests. Results are logged, and failures do not stop the pipeline. |
| 6 | **Test data cleanup on target** — removes synthetic test data from the target instance. |
| 7 | **Process results** — generates a migration summary and optionally downloads artifacts from storage. |

When this completes, proceed to Phase 4.

**Phase 4 — Disable maintenance mode (manual, conditional)**

Disable maintenance mode after Phase 3 succeeds if traffic to the source instance needs to be re-enabled. This step is also required before you run Phase 5 (cleanup), because cleanup communicates with the source through REST and fails with HTTP 503 if maintenance mode is still active.

On the source Commerce server:

```bash
bin/magento maintenance:disable
```

**Phase 5 — Cleanup (optional, source must be live)**

Remove the synthetic test customers and orders created in Phase 1 from the source instance through REST. This phase can run only after maintenance mode is disabled.

>[!NOTE]
>
>Skip this phase if `SKIP_TEST_DATA_CREATION=true` is set in `.env`, because no test data was created.

```bash
./bin/console migration:cleanup
```

| Step | What happens |
| --- | --- |
| 1 | **Database connection setup** — for PaaS source instances, reopens cloud tunnels. For on-premises instances, establishes and verifies direct database connectivity. |
| 2 | **Source REST cleanup** — removes synthetic test customers and orders from the source through the REST API. |

## Resume or re-run a migration

The migration tool tracks progress using a `.migration_id` file in the project root. This file is created automatically when a new migration starts and records the current migration identifier.

### Resume after a failure

If a migration run fails or is interrupted, re-run the same command to resume from the last successful step (extraction, loading, or verification) rather than restarting from scratch. Already-completed steps are skipped automatically.

>[!IMPORTANT]
>
>When you resume the `migration:during-maintenance` phase, the source must remain in maintenance mode throughout. If the source was taken out of maintenance or data changed between runs, the resumed migration can produce inconsistent results.

### Start a fresh migration

To discard a previous run and start a completely new migration, delete the `.migration_id` file before you start your next migration:

```bash
rm .migration_id
```

If `.migration_id` exists and the previous migration already completed, the tool prints a message saying the migration is already done and advises you to delete the file.

## Review logs and debug

All migration logs are written to the `logs/` directory in the project root, organized into timestamped subdirectories:

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log` is the main pipeline orchestration log. If a step failed, it shows which script exited with a non-zero code and why.
- Per-step logs, such as `09b_run_load.log` and `11_verify_data_integrity_local.log`, contain detailed output for each phase.
