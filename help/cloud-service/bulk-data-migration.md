---
title: 'Bulk data migration tool overview'
description: Learn about the bulk data migration tool for migrating data from Adobe Commerce PaaS to Adobe Commerce as a Cloud Service.
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
---
# Bulk data migration tool overview

{{accs-early-access}}

The bulk data migration tool is designed to provide the best onboarding experience and time-to-value possible when migrating from Adobe Commerce PaaS to [!DNL Adobe Commerce as a Cloud Service]. This tool handles the comprehensive transfer of core data sets while accounting for the architectural differences between PaaS and SaaS platforms.

## What is the bulk data migration tool?

The bulk data migration tool is a custom CLI application that facilitates the migration of first-party data from Adobe Commerce PaaS instances to [!DNL Adobe Commerce as a Cloud Service]. It provides a mechanism to transfer essential commerce data while handling the transformation required for the new cloud-native architecture.

## Key capabilities

The bulk data migration tool supports migration of the following data sets:

### Core data sets

* **Product data** - Product details including titles, descriptions, prices, SKUs, attributes, images, and metadata
* **Customer data** - Customer information including names, contact details, shipping addresses, preferences, and account data
* **Order history** - Historical order data including shipping details, order status, payment history, and order metadata
* **Inventory data** - Stock levels, inventory tracking, and warehouse information
* **Content data** - CMS pages, blocks, and static content
* **Category data** - Category structure, hierarchy, and metadata
* **Configuration data** - Store configuration, system settings, and administrative data

### Technical features

* **High-performance extraction** - Uses direct SQL queries to source databases for optimal performance
* **Data transformation** - Converts data from PaaS schema to [!DNL Adobe Commerce as a Cloud Service] schema during extraction
* **Resume capability** - Ability to restart migration from the point of failure for enhanced reliability
* **Progress monitoring** - Real-time visibility into migration status and completion progress
* **Error handling** - Comprehensive error reporting and logging for troubleshooting

## Architecture overview

The bulk data migration tool uses a two-part architecture:

1. **Data extraction tool** - A custom CLI application that extracts data from the source PaaS environment
2. **Data loading tool** - A service that loads transformed data into the target [!DNL Adobe Commerce as a Cloud Service] environment

### Data flow

1. **Extract** - Data is extracted from the PaaS database using direct SQL queries
2. **Transform** - Data is transformed from PaaS schema to [!DNL Adobe Commerce as a Cloud Service] schema
3. **Load** - Transformed data is loaded into the target [!DNL Adobe Commerce as a Cloud Service] database

## Prerequisites

Before using the bulk data migration tool, ensure you have:

* Access to the source Adobe Commerce PaaS environment
* Access to the target [!DNL Adobe Commerce as a Cloud Service] environment
* Appropriate database credentials and permissions
* CLI access to both environments
* Sufficient storage space for data dumps (if required)

## Supported migration scenarios

The tool supports the following migration scenarios:

* **Full migration** - Complete data transfer from PaaS to [!DNL Adobe Commerce as a Cloud Service]
* **Selective migration** - Migration of specific data sets or tables
* **Fresh start migration** - Migration of essential data only, excluding historical data

## How to run the bulk data migration tool

Follow these steps to execute the bulk data migration tool for your [!DNL Adobe Commerce as a Cloud Service] migration.

### Step 1: Prepare the source environment

1. **Access your PaaS environment**

   ```bash
   ssh user@your-paas-environment.com
   ```

1. **Verify database connectivity**

   ```bash
   mysql -u username -p -h database_host
   ```

1. **Check available disk space**

   ```bash
   df -h
   ```

### Step 2: Set up the migration tool

1. **Download the migration tool**

   ```bash
   wget https://repo.adobe.com/migration-tools/bulk-data-migration-tool.tar.gz
   tar -xzf bulk-data-migration-tool.tar.gz
   cd bulk-data-migration-tool
   ```

1. **Configure the tool**

   ```bash
   cp config.sample.php config.php
   ```

1. **Edit the configuration file**

   ```php
   <?php
   return [
       'source' => [
           'host' => 'source-db-host',
           'username' => 'source-db-user',
           'password' => 'source-db-password',
           'database' => 'source-db-name',
           'port' => 3306
       ],
       'target' => [
           'host' => 'target-db-host',
           'username' => 'target-db-user', 
           'password' => 'target-db-password',
           'database' => 'target-db-name',
           'port' => 3306
       ],
       'migration' => [
           'batch_size' => 1000,
           'log_level' => 'info',
           'temp_directory' => '/tmp/migration'
       ]
   ];
   ```

### Step 3: Validate the migration setup

1. **Run pre-migration checks**

   ```bash
   php bin/migration-tool validate --config=config.php
   ```

1. **Verify data connectivity**

   ```bash
   php bin/migration-tool test-connection --config=config.php
   ```

1. **Generate migration plan**

   ```bash
   php bin/migration-tool plan --config=config.php --output=migration-plan.json
   ```

### Step 4: Execute the data migration

1. **Start the migration process**

   ```bash
   php bin/migration-tool migrate --config=config.php --plan=migration-plan.json
   ```

1. **Monitor progress**

   ```bash
   # In a separate terminal
   tail -f logs/migration.log
   ```

1. **Check migration status**

   ```bash
   php bin/migration-tool status --config=config.php
   ```

### Step 5: Handle migration stages

The migration process includes several stages that execute sequentially:

1. **Data extraction stage**

   ```bash
   # Monitor extraction progress
   php bin/migration-tool status --stage=extract
   ```

1. **Data transformation stage**

   ```bash
   # Monitor transformation progress  
   php bin/migration-tool status --stage=transform
   ```

1. **Data loading stage**

   ```bash
   # Monitor loading progress
   php bin/migration-tool status --stage=load
   ```

### Step 6: Resume interrupted migrations

If the migration is interrupted, you can resume from the last successful point:

1. **Check last successful checkpoint**

   ```bash
   php bin/migration-tool checkpoint --config=config.php
   ```

1. **Resume migration**

   ```bash
   php bin/migration-tool resume --config=config.php --from-checkpoint
   ```

### Step 7: Verify migration completion

1. **Run post-migration validation**

   ```bash
   php bin/migration-tool verify --config=config.php
   ```

1. **Generate migration report**

   ```bash
   php bin/migration-tool report --config=config.php --output=migration-report.html
   ```

1. **Check data integrity**

   ```bash
   php bin/migration-tool integrity-check --config=config.php
   ```

## Troubleshooting

### Common issues and solutions

**Connection timeouts**

```bash
# Increase timeout values in config.php
'connection_timeout' => 300,
'query_timeout' => 600
```

**Memory limitations**

```bash
# Reduce batch size in config.php
'batch_size' => 500
```

**Disk space issues**

```bash
# Clean up temporary files
php bin/migration-tool cleanup --config=config.php
```

### Monitoring and logging

* **View detailed logs**: `tail -f logs/migration-detailed.log`
* **Check error logs**: `cat logs/migration-errors.log`
* **Monitor system resources**: `htop` or `top`

## Best practices

1. **Test on staging first** - Always run a test migration on a staging environment before production
1. **Backup source data** - Create a backup of your source database before starting migration
1. **Monitor system resources** - Ensure adequate CPU, memory, and disk space during migration
1. **Schedule during low traffic** - Plan migrations during maintenance windows or low-traffic periods
1. **Validate data post-migration** - Thoroughly test your [!DNL Adobe Commerce as a Cloud Service] instance after migration

## Next steps

After completing the bulk data migration:

1. **Verify storefront functionality** - Test critical user flows and commerce operations
1. **Configure [!DNL Adobe Commerce as a Cloud Service] specific features** - Set up cloud-native capabilities
1. **Update integrations** - Reconfigure third-party integrations for the new environment
1. **Performance optimization** - Implement performance tuning for the cloud environment
1. **Go-live planning** - Coordinate DNS cutover and traffic routing to the new platform

For additional support or questions about the bulk data migration tool, contact Adobe Commerce Support or consult the [migration guide](migration.md) for comprehensive migration planning.
