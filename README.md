# Databricksinitsandbox
Creating Databricks cluster in Azure and installing agent via init script

## Prerequisite: 
Have access to your [Microsoft Azure account] (https://portal.azure.com/)

## Objective:
1. Create Databricks workspace
2. Setup Cluster within Databricks specifying Spark Config and envvars DD_API_KEY, DD_SITE, and DD_ENV
3. Add init script to Workspace and point to init script in cluster
4. install databricks integration tile


## Create Databricks Workspace
1. Login to microsoft azure account with onmicrosoft.com account
2. search for databricks in services
3. create databricks workspace (add tags creator, myteam, and ticketspec)
4. might see error for resource group issues


## Setup Cluster in Databricks Workspace
1. Navigate to the +'new' Icon and choose cluster
2. Toggle to single node - Leave default configurations - navigate to 'Advanced options' dropdown arrow and in the spark tab specify the following:
   1. Spark config: spark.databricks.delta.preview.enabled true
   2. Environment Variables: DD_SITE=https://app.datadoghq.com, DD_ ENV-prod, DD API KEY-<yourkey>
3. Click 'Create Cluster' 

## Add init script to Workspace
1. Navigate to the +'new' Icon and choose notebook
2. Paste the init script mentioned in our [Databricks Driver Only](https://docs.datadoghq.com/integrations/databricks/?tab=driveronly#standard-cluster) docs
3. change or create folder by specifying one in the 1st line of code: `dbutils.fs.put("dbfs:/<init-script-folder>/datadog-install-driver-only.sh","""` -> `dbutils.fs.put("dbfs:/ISFolder/datadog-install-driver-only.sh","""`
4. Click run to create the init script
5. Copy the path (for example: `dbfs:/ISFolder/datadog-install-driver-only.sh`) 
6. Navigate to 'Compute' and click on your cluster > edit
7. Drop down to advanced options and click the init scipts tab - specify DBFS as Type - paste the path (for example: `dbfs:/ISFolder/datadog-install-driver-only.sh`) and click add
8. click 'confirm and restart'


## Helpful Links
[Databricks Driver Only](https://docs.datadoghq.com/integrations/databricks/?tab=driveronly#standard-cluster) doc
[Databricks Driver Only Internal](https://datadoghq.atlassian.net/wiki/spaces/~6387b6f3f6c85b343c0ba799/pages/2830664472/Databrick+Integration+with+Datadog) doc
[Databricks Worker And Driver Internal]([https://docs.datadoghq.com/integrations/databricks/?tab=driveronly#standard-cluster](https://datadoghq.atlassian.net/wiki/spaces/TS/pages/1391626126/Databricks+Datadog+Integration+for+Driver+Workers)https://datadoghq.atlassian.net/wiki/spaces/TS/pages/1391626126/Databricks+Datadog+Integration+for+Driver+Workers) doc


  
