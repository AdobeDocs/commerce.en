# Verify Optimizer data sync

1. **Check sync status in the Commerce Admin:**

   Go to **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Data Feed Sync Status page with feed item status reporting](/help/aco-connector/assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   When the sync is running, the feed data shows successfully sent records. Select a feed to view details or troubleshoot sync issues.

1. **Confirm data was delivered to [!DNL Commerce Optimizer]:**

   From the [!DNL Commerce Optimizer] menu, select **[!UICONTROL Data Sync]**.

   ![Data Sync page in Adobe Commerce Optimizer showing synced catalog data](/help/aco-connector/assets/data-sync.png){width="500" zoomable="yes"}

   Verify that the expected products, prices, and attributes appear.

When sync is working as expected:

- **[!UICONTROL Data Feed Sync Status]** shows successfully sent records for connector feeds, with no unresolved item-level errors.
- **[!UICONTROL Data Sync]** in [!DNL Commerce Optimizer] lists the expected catalog sources, products, prices, and attributes.

>[!TIP]
>
>If you have any issues with the data sync, see the [Troubleshooting](/help/aco-connector/troubleshooting.md) guide.
