---
sidebar_position: 3
---

# How to Use

## Configuration

Navigate to the tab `Configuration`. Start the configuration by selecting a `Destination Database` where the Salesforce objects records will be saved. `Secret Name` and `External Access Integration Name` should already be there if you followed the “Grant Salesforce Access” section. If not, please go to the section and follow the procedure. Finally, select the virtual `Warehouse` where your sync will run. 

A checked box inform you that you are giving consent for Maxa to access your event table for issue resolution and improved user experience purposes. Information will be treated confidentially according to our [privacy policy](https://www.maxa.ai/legal/) and used solely to enhance your user experience. By consenting, you acknowledge and agree that Maxa is not liable for any issues arising from the use of this information. Unchecking the box will disable sharing of your event table with Maxa. In that case, we will be unable to know when an issue occurs on your app. 

### Advanced Options

All the advanced options are optional.

`Destination Table Prefix` allows to choose a prefix to apply to all tables where Salesforce objects records will be saved. The table names will have the prefix followed by the Salesforce objects name. 

`Default Replication Frequency` allows to set a default replication frequency which will be apply to all enabled Salesforce objects unless specify otherwise. The available frequency modes are:

- `Manual`: user triggers manually the replication.
- `Cron`: the user must specify a cron string for the replication. ([Documentation](https://docs.snowflake.com/en/sql-reference/sql/create-task))
- `Every 24 hours`: replication will occur in 24 hours intervals at midnight UTC.  This is the default frequency the app will use if no other mode as been specified.
- `Every 12 hours`: replication will occur in 12 hours intervals at midnight and noon UTC.

`Default Replication Mode` allows to set a default replication mode which will be applied to all enabled Salesforce objects unless specify otherwise. The available modes are: 

- `Incremental | Append + Deduped` : only the records that have been updated since the last sync will be read. New records read will replace the previous version in the destination table. If an existing row has been updated, the new row will be added to the table replacing the previous version. The firs sync of the incremental mode will act like a full refresh. This is the default mode the app will use if no other mode as been specified.
- `Incremental | Append` : only the records that have been updated since the last sync will be read. New records read will be append to the destination table. If an existing row has been updated, the new row will be added to the table and the previous version will stay in the table as well. The firs sync of the incremental mode will act like a full refresh.
- `Full Refresh | Overwrite` : the entire history of the records will be read during the sync. Existing data, if any, will be overwritten by the data read during the sync.
- `Full Refresh | Append` : the entire history of the records will be read during the sync. Existing data, if any, will stay in intact in the destination table and new data ready will be append to it. If similar data is synced, every sync will replicated existing data.

Click on `Configure` to set up and saved your configurations. Next step will be to enable Salesforce objects you would like to sync be navigating to the tab `Objects Settings`. 

## Data Sync

Navigate to the tab `Objects Settings`. If you haven’t configure the connector yet, go to the `Configuration` tab and fill-out mandatory options. Once your configuration is set up, you will see a list of all available Salesforce objects. A red circle indicated that the object has not been enable for replication yet. A green circle indicated that the object has been enable. 

### Enable Replication

If you wish to enable replication on a specific object, expand the object section by clicking on the arrow at the right of the object bar. Click on `Enable` to set replication on the object. The circle at the left of the object name will turn green indicating that the object has been enabled. To disable the replication, click on `Disable`. If a default replication schedule and mode hasn’t been configured in the advanced configuration options, the replication schedule will occur in 24 hours intervals at midnight UTC and the replication mode will be incremental. 

### Set Specific Sync Frequency

Once your Salesforce object is enabled, you can set a specific replication frequency in the `General` section. The replication frequency you choose for the object will override the default option for the specific object only. If you want to set a default replication frequency for all objects, go to the `Configuration` tab and in the `Advanced Options` section. The available frequency modes are:

- `Manual`: user triggers manually the replication.
- `Cron`: the user must specify a cron string for the replication. ([Documentation](https://docs.snowflake.com/en/sql-reference/sql/create-task))
- `Every 24 hours`: replication will occur in 24 hours intervals at midnight UTC. This is the default frequency the app will use if no other mode as been specified.
- `Every 12 hours`: replication will occur in 12 hours intervals at midnight and noon UTC.

### Set Specific Sync Mode

Once your Salesforce object is enabled, you can set a specific replication mode in the `General` section. The replication mode you choose for the object will override the default option for the specific object only. If you want to set a default replication mode for all objects, go to the `Configuration` tab and in the `Advanced Options` section. The available modes are: 

- `Incremental | Append + Deduped` : only the records that have been updated since the last sync will be read. New records read will replace the previous version in the destination table. If an existing row has been updated, the new row will be added to the table replacing the previous version. The firs sync of the incremental mode will act like a full refresh. This is the default mode the app will use if no other mode as been specified.
- `Incremental | Append` : only the records that have been updated since the last sync will be read. New records read will be append to the destination table. If an existing row has been updated, the new row will be added to the table and the previous version will stay in the table as well. The firs sync of the incremental mode will act like a full refresh.
- `Full Refresh | Overwrite` : the entire history of the records will be read during the sync. Existing data, if any, will be overwrite by the data read during the sync.
- `Full Refresh | Append` : the entire history of the records will be read during the sync. Existing data, if any, will stay in intact in the destination table and new data ready will be append to it. If similar data is synced, every sync will replicated existing data

## Sync History

Navigate to the tab `Sync History`. If you haven’t configure the connector yet, go to the `Configuration` tab and fill-out mandatory options. The `Sync History` tab allows you to see all previous replication and their respective state. It can also be used to trigger manual replication. 

### Manual Sync

If you wish to replicate all objects at once, click on `Synchronize`. If you wish to replicate only a specific object, use the search tab to select the Salesforce object to be sync and click on `Synchronize`.

## Data Preview

Navigate to the tab `Data Preview`. If you haven’t configure the connector yet, go to the `Configuration` tab and fill-out mandatory options. The `Data Preview` tab allows you to see the first 100 rows of the Salesforce objects you have enabled. Use the search bar to select the object you would like to preview.