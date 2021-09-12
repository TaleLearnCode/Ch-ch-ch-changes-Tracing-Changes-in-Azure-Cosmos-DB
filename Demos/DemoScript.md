# Ch-ch-ch-changes: Tracing Changes in Azure Cosmos DB

1. [Basic Change Feed Demo](#basic-change-feed-demo)
2. [Archiving Data](#archiving-data)
3. Denormalizing Data
4. Replicating Containers

All of these demos assume that a Cosmos DB account has been created using the Core (SQL) API.

---

## Basic Change Feed Demo

#### Prep-Work

1. Ensure that the 'Items' container is created via the "Quick Start" blade
2. Create the demo To Do items using the data below

~~~
{
    "title": "Basic Change Feed Demo",
    "sortOrder": 1,
    "assignedTo": "Chad Green",
    "status": "Not Started",
    "partitionKey": "EventName"
}

{
    "title": "Archiving Data",
    "sortOrder": 2,
    "assignedTo": "Chad Green",
    "status": "Not Started",
    "partitionKey": "EventName"
}

{
    "title": "Denormalizing Data",
    "sortOrder": 3,
    "assignedTo": "Chad Green",
    "status": "Not Started",
    "partitionKey": "EventName"
}

{
    "title": "Replicating Containers",
    "sortOrder": 4,
    "assignedTo": "Chad Green",
    "status": "Not Started",
    "partitionKey": "EventName"
}

{
    "title": "Event-Driven Architecture",
    "sortOrder": 5,
    "assignedTo": "Chad Green",
    "status": "Not Started",
    "partitionKey": "EventName"
}

{
    "title": "Real-Time Reporting",
    "sortOrder": 6,
    "assignedTo": "Chad Green",
    "status": "Not Started",
    "partitionKey": "EventName"
}

~~~

#### Demo Steps

1. Navigate to Cosmos database
2. Open the 'Data Explorer' blade
3. Click on the ToDoList database
4. Show off the to do items in the database
5. Open a SQL Query tab
6. Execute: ~SELECT c.title, c.status  FROM c WHERE c.partitionKey = 'KCDC'~
7. In Visual Studio, create an Azure Functions project using .NET Core 3.1 adding a Cosmos triggered function
8. Add the 'CosmosConnectionString' element to the local.settings
9. Talk through the generated code.
10. While talking through the generated code, add ~CreateLeaseCollectionIfNotExists = true~
11. Change the LogInformation to LogWarning (so it shows up better during the demo)
11. Start the Azure Function project
12. From the Azure Portal, make changes and show how it gets detected by the change feed
13. Show how deletes are not detected by the change feed

---

## Archiving Data

#### Prep-Work

1. Prepare the Azure Storage Blob container to accept the archived data
* Ensure that that the container is empty

2. Prepare the Azure Cosmos DB account to accept the data
* Ensure that there is a ~moveData~ database with an empty ~archival~ container

3. Add the following settings to the local.settings.json file within the ArchiveData-Function project:
* CosmosConnectionString
* StorageAccountName
* StorageAccountKey
* BlobContainerName

4. Ensure the following settings are present in the ignored Setting class in the Demonstrator project:
* MoveDataDatabasebaseName
* ArchivalContainerName
* DataFolderPath

#### Demo Steps

1. Talk about how we are going to stimulate the questions interaction scenario
2. Talk through the code within ArchiveData function
3. Navigate to the *archival* container in the *moveData* container to show that it is empty
4. Navigate to the *data-archival* container in the Azure Storage account to show that it is empty
5. Ensure that the ArchiveData-Function and Demonstrator projects are set to start
6. Run the demonstrator project and start the Archive Data demo and talk through what's happening