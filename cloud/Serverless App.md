Work in progress
# Introduction
In this short tutorial you will build a serverless application in Azure using the following components:
1. Static website on storage account to host the page
2. Serverless API functions using Azure Functions
3. Database using Azure Cosmos DB

## Creating an Azure Storage account
Use the Azure portal to create an Azure storage account with the following characteristics:
- general purpose v2
- Local redundant storage (LRS)

Upload the index.html file to the storage account using this tutorial:
https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal

Set the access level to the blob
