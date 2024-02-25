## Azure Data Pipeline Project
 # Overview
This project sets up an end-to-end data pipeline using Azure services. It involves creating a Resource Group, Storage Account, Azure Data Factory, Azure Databricks, and Azure Synapse Analytics. The pipeline extracts data from a GitHub repository, transforms it using Databricks, and loads it into Azure Synapse Analytics for further analytics. Finally, the data is visualized using Power BI.

# Technologies Used
Azure Storage Account: For data storage.
Azure Data Factory: Orchestration tool for data movement.
Azure Databricks: Data transformation and processing.
Azure Synapse Analytics: Data warehousing and analytics.
Power BI: For data visualization and reporting.
# Steps to Replicate:
# 1. Create Azure Resources:
Resource Group:

Create a new Resource Group named "YourResourceGroup" in the Azure portal.
Storage Account:

Create a Storage Account named "YourStorageAccount" in the "YourResourceGroup".
Inside the Storage Account, create two containers: "raw-data" and "transformed-data".
# 2. Azure Data Factory Setup:
Data Factory:

Create an Azure Data Factory named "YourDataFactory" in the "YourResourceGroup".
Pipeline Creation:

Create a pipeline named "GitHubToDataLakePipeline" inside "YourDataFactory".
Add a Copy Data activity:
Source: GitHub repository URL.
Destination: Azure Data Lake Storage Gen2.
# 3. Data Loading to Azure Data Lake:
Data Lake Load:
Configure the Copy Data activity to load data from GitHub to the "raw-data" folder in Azure Data Lake Storage Gen2.
# 4. Azure Databricks Environment:
Databricks Workspace:

Create a Databricks workspace named "YourDatabricksWorkspace" in the Azure portal.
Cluster Setup:

Inside Databricks, create a cluster named "YourDatabricksCluster".
Mount Data Lake:

Use the following script to mount the Data Lake Storage:
python
Copy code
configs = {
  "fs.azure.account.auth.type": "OAuth",
  "fs.azure.account.oauth.provider.type": "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
  "fs.azure.account.oauth2.client.id": "<your_client_id>",
  "fs.azure.account.oauth2.client.secret": "<your_client_secret>",
  "fs.azure.account.oauth2.client.endpoint": "https://login.microsoftonline.com/<your_tenant_id>/oauth2/token"
}

dbutils.fs.mount(
  source = "abfss://tokyo-olympic-data@yourstorageaccount.dfs.core.windows.net/",
  mount_point = "/mnt/tokyoolymic",
  extra_configs = configs
)
# 5. Data Transformation:
Databricks Notebook:
Create Databricks notebooks for data transformation.
Use mounted path "/mnt/tokyoolymic/raw-data/" as the source.
# 6. Azure Synapse Analytics:
Synapse Workspace:

Create an Azure Synapse Analytics workspace named "YourSynapseWorkspace" in the Azure portal.
Data Loading:

Load transformed data from the "transformed-data" folder in Azure Data Lake to Synapse Analytics.
# 7. Power BI Integration:
Connect Power BI:
Connect Power BI to Azure Synapse Analytics for data visualization.
Create reports and dashboards based on the data in Synapse Analytics.
Additional Notes:
Ensure proper access permissions for Azure services.
Monitor pipelines and clusters for efficient data processing.
Refer to Azure documentation for detailed configurations and troubleshooting.
This README provides a quick guide to setting up the Azure Data Pipeline project. For detailed instructions, please refer to the respective Azure services in the Azure portal.

Feel free to customize the names of resources, URLs, and other parameters according to your project requirements. This README aims to provide a comprehensive yet concise overview of the project setup.# Olympic_Data_Analytics-using-AZURE_DATAFACTORY_AZURE_SYNAPSE
