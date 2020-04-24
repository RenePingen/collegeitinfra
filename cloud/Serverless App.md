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

Set the access level to the blob to "Anonymous read access for containers and blob"

## Creating the database
Use the Azure portal to create an Azure cosmos DB with the following characteristics:
- API: Core (SQL)
- Geo redundancy: disable
- Multi region writes: disable

## Creating the API (Azure function)
Use the Azure portal to create a Function App with the following characteristics:
- publish: code
- runtime stack: .net core
- hosting plan: consumption (serverless)

### Create the upload function
This function will be used to upload data to the database.

1. Go to the Azure function, and click "New Function".
2. Template: HTTP Trigger, Name  uploadData
3. Click on the function-> "Integrate". We will add a binding to the cosmos DB so that the function can access the database.
4. Add an "Output" to the function, Azure cosmos DB, with the following values:
   - DocumentParameter name: outputDocument
   - Azure Cosmos DB account connection: Click on new and select your cosmos database account
   - Database name: userdata
   - Click Save
5. Insert the code for the function:
```csharp
#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;

public static async Task<IActionResult> Run(HttpRequest req, IAsyncCollector<object> outputDocument, ILogger log)
{

    log.LogInformation("C# HTTP trigger function processed a request.");

    var doc =  new DBDocument();  

    string name = req.Query["name"];   
    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    dynamic data = JsonConvert.DeserializeObject(requestBody);
    name = name ?? data?.name;

    if (name!=null)
    {
        doc.userName=name;
        await outputDocument.AddAsync(doc);
        return (ActionResult)new OkObjectResult($"Hello, {name}");
    }
    else
    {
        return new BadRequestObjectResult("Please pass a name on the query string or in the request body");
    }

}

public class DBDocument{
  public string userName {get;set;}
}
```


