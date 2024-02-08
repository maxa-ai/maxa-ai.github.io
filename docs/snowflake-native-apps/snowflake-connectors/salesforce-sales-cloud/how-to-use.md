---
sidebar_position: 2
---

# How to Install

## Step-by-Step Guide to Running the App

### 1. Prerequisites

You will need a Salesforce Sales Cloud account with permission to access data from resources you want to sync. The following information will be needed after installing the app to allow Snowflake to get Salesforce access: 

- `salesforce_client_id` , `salesforce_client_secret` and `salesforce_refresh_token` : this information can be obtained from Salesforce following the procedure described [here](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_refresh_token_flow.htm&type=5).
- `salesforce_domain` : Your custom domain is the part between **https://** and **.my.salesforce.com** in your custom Salesforce URL. More info can be obtained from Salesforce following the procedure [here](https://help.salesforce.com/s/articleView?id=sf.domain_name_overview.htm&type=5).

Please have this information ready to use, it will be needed after installing the app in the section “Grant Salesforce Access”.

### 2. Installation
1. Log into your Snowflake account. 
2. Navigate to the `Marketplace` and locate the Salesforce Connector app by Maxa.
3. Click on `Get` to initiate the installation process.
4. Follow the prompts and grant necessary permissions to complete the installation.
5. Click `Apps` on the left sidebar under the `Installed Apps` section, you should see the `Salesforce Connector` by Maxa.

### 3. Grant Salesforce Access

`salesforce_client_id` , `salesforce_client_secret` , `salesforce_refresh_token` and `salesforce_domain` are needed for this step. Please refer to the “Prerequisite” section for explanation on how to get this information. 

Before opening the app, you will need to run the following script adjusted with your information in a Snowflake worksheet. This script allows you to stock your Snowflake credential in a confidential place and grant access for the app to access it. 

Copy the following script in a Snowflake worksheet and replace <salesforce_domain> by `salesforce_domain` , <salesforce_client_id> by `salesforce_client_id` , <salesforce_client_secret> by `salesforce_client_secret` and <salesforce_refresh_token> by `salesforce_refresh_token` and run the script. 

```sql
SET APP_NAME = '<INSTALLED_APPLICATION_NAME>';
SET WAREHOUSE = '<WAREHOUSE_NAME>';
SET APP_INSTANCE_NAME = $APP_NAME || '_INSTANCE';
SET INTEGRATION_NAME = $APP_NAME || '_INTEGRATION';
SET SECRETS_DB = $APP_NAME || '_SECRETS';
SET SECRETS_SCHEMA = $SECRETS_DB || '.PUBLIC';
SET SECRET_NAME = $SECRETS_DB || '.PUBLIC.{{ config.installation.secret }}';

USE ROLE ACCOUNTADMIN;

CREATE OR REPLACE DATABASE IDENTIFIER($SECRETS_DB);
USE DATABASE IDENTIFIER($SECRETS_DB);

CREATE OR REPLACE NETWORK RULE SALESFORCE_RULE
MODE = EGRESS
TYPE = HOST_PORT
VALUE_LIST = ('login.salesforce.com:443', '<salesforce_domain>.my.salesforce.com:443');

CREATE OR REPLACE SECRET IDENTIFIER($SECRET_NAME)
TYPE=GENERIC_STRING
SECRET_STRING='{
    "client_id": "<salesforce_client_id>",
    "client_secret": "<salesforce_client_secret>",
    "refresh_token": "<salesforce_refresh_token>"
}';

SET CREATE_INTEGRATION = 'CREATE OR REPLACE EXTERNAL ACCESS INTEGRATION
IDENTIFIER($INTEGRATION_NAME)
ALLOWED_NETWORK_RULES = (SALESFORCE_RULE)
ALLOWED_AUTHENTICATION_SECRETS = (''' || $SECRET_NAME || ''')
ENABLED = TRUE';

SELECT $CREATE_INTEGRATION;
EXECUTE IMMEDIATE $CREATE_INTEGRATION;

GRANT USAGE ON INTEGRATION IDENTIFIER($INTEGRATION_NAME) TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);

GRANT USAGE ON DATABASE IDENTIFIER($SECRETS_DB) TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);
GRANT USAGE ON SCHEMA IDENTIFIER($SECRETS_SCHEMA)  TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);
GRANT READ ON SECRET IDENTIFIER($SECRET_NAME) TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);

GRANT CREATE DATABASE ON ACCOUNT TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);
GRANT EXECUTE TASK ON ACCOUNT TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);

CREATE DATABASE IF NOT EXISTS LOGS;
CREATE EVENT TABLE IF NOT EXISTS LOGS.PUBLIC.EVENT_TABLE;

GRANT USAGE ON DATABASE LOGS TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);
GRANT USAGE ON SCHEMA LOGS.PUBLIC TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);
GRANT SELECT ON TABLE LOGS.PUBLIC.EVENT_TABLE TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);

GRANT USAGE ON WAREHOUSE IDENTIFIER($WAREHOUSE) TO APPLICATION IDENTIFIER($APP_INSTANCE_NAME);
```

### Grant Privileges

Once you open the `Salesforce Connector` app, you will need to grant the application privileges necessary to extract data into Snowflake. Click on the security logo situated in the top right corner. Under `Account level privileges`, click `Review` , enable `Create Database` , `Create Warahouse` and `Execute Task` and click on `Update Privileges`. 

# App Functionality

Note: All tabs except "Configuration" will show a warning message until the connector is configured.