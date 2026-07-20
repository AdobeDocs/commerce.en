# Verify Commerce service data sync

To verify that the data sync is working, confirm that data exported successfully from [!DNL Adobe Commerce] and that the data was successfully delivered to the connected Commerce service. Use the dashboards for your deployment to check both steps.

Start with export, then confirm delivery.

1. Check the sync status in the Commerce Admin.

   Go to **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Data Feed Sync Status page with feed item status reporting](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   When the sync is running, the feed data shows successfully sent records. Select a feed to view details or troubleshoot sync issues.

1. Confirm the data was delivered to connected Commerce Services.

   From the Commerce Admin, go to **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**.

   ![Data Management dashboard showing synced catalog data in connected Commerce Services](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   Verify that the expected products, prices, and attributes appear.

>[!TIP]
>
>If you have any additional issues with the data sync, see [Review logs and troubleshoot](/help/data-export/troubleshooting/logging.md).

