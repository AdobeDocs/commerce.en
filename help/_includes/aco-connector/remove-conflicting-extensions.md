
# Remove conflicting extensions

If you have any of the following extensions installed, uninstall them before installing the [!DNL Adobe Commerce Optimizer Connector for B2B]:

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

Data associated with these extensions is still available in the Commerce database. However, it is not exported to [!DNL Commerce Optimizer] when the connector is enabled. To implement the Adobe Commerce search and merchandising capabilities provided by these extensions after enabling the connector, configure them from the [[!DNL Commerce Optimizer] Admin UI](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Failure to remove these extensions before enabling the connector causes broken configuration screens, duplicate data in [!DNL Commerce Optimizer], and 401 or 403 authentication errors.