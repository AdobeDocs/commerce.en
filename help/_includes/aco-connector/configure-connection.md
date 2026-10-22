# Get [!DNL Commerce Optimizer] instance details

Get the _tenant ID_ from the _[!DNL Instance Id]_ field on the [!DNL Commerce Optimizer] instance [[!DNL Instance details] page](/help/optimizer/get-started.md#manage-instances), or from the URL used to access the instance. For example, in `https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`.

1. From the Commerce Admin, select **[!UICONTROL Adobe Commerce Optimizer]** to display the configuration page with instructions.

   ![[!DNL Commerce Optimizer] configuration page](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. From the command line, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) to connect to the [!DNL Adobe Commerce] staging environment.

1. To configure the integration, run the following [!DNL Adobe Commerce] CLI command, replacing the placeholder values with the values for your [!DNL Commerce Optimizer] project:

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Verify the connection by returning to the Commerce Admin and selecting the [!UICONTROL Adobe Commerce Optimizer] option.

   When you select the option, it opens the [!DNL Commerce Optimizer] UI in a new tab.
