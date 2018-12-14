---
title: 用于 .NET 的 Azure Cosmos DB 库
description: 用于 .NET 的 Azure Cosmos DB 库参考
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 8ff565f1cd72eec2f574b45d04ceac526b8c5eb0
ms.sourcegitcommit: 01ec3adba39a6f946015552c28da0a9a6bb57180
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53112015"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="0cf34-103">用于 .NET 的 Azure Cosmos DB 库</span><span class="sxs-lookup"><span data-stu-id="0cf34-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0cf34-104">概述</span><span class="sxs-lookup"><span data-stu-id="0cf34-104">Overview</span></span>

<span data-ttu-id="0cf34-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是一种全球分布式多模型数据库服务。</span><span class="sxs-lookup"><span data-stu-id="0cf34-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="0cf34-106">它旨在通过一个综合性 SLA 跨任意数量的地理区域以富有弹性的方式独立缩放吞吐量和存储空间。</span><span class="sxs-lookup"><span data-stu-id="0cf34-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="0cf34-107">有了 Azure Cosmos DB，可以通过使用 API 和编程模型存储和访问文档、键值、宽列和图形数据库。</span><span class="sxs-lookup"><span data-stu-id="0cf34-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="0cf34-108">[Cosmos DB 入门](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="0cf34-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="0cf34-109">客户端库</span><span class="sxs-lookup"><span data-stu-id="0cf34-109">Client library</span></span>

<span data-ttu-id="0cf34-110">使用 Azure Cosmos DB .NET 客户端库在现有 Azure Cosmos DB 数据存储中访问和存储数据。</span><span class="sxs-lookup"><span data-stu-id="0cf34-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="0cf34-111">若要自动创建新的 Azure Cosmos DB 帐户，请使用 Azure 门户、CLI 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0cf34-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="0cf34-112">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)。</span><span class="sxs-lookup"><span data-stu-id="0cf34-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

<span data-ttu-id="0cf34-113">若要安装版本 2.x，请执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="0cf34-113">To install version 2.x:</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0cf34-114">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="0cf34-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="0cf34-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="0cf34-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

<span data-ttu-id="0cf34-116">若要安装 3.0 预览版（面向 .NET Standard），请执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="0cf34-116">To install the preview of version 3.0, which targets .NET standard:</span></span> 

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0cf34-117">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="0cf34-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a><span data-ttu-id="0cf34-118">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="0cf34-118">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a><span data-ttu-id="0cf34-119">代码示例</span><span class="sxs-lookup"><span data-stu-id="0cf34-119">Code Example</span></span>

<span data-ttu-id="0cf34-120">此示例连接到现有的Azure Cosmos DB SQL API 数据库，从集合中读取文档，并将文档反序列化为 `Item` 对象。</span><span class="sxs-lookup"><span data-stu-id="0cf34-120">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span> <span data-ttu-id="0cf34-121">此示例使用 .NET SDK 的 2.x 版本。</span><span class="sxs-lookup"><span data-stu-id="0cf34-121">This example uses version 2.x of the .NET SDK.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

<span data-ttu-id="0cf34-122">此示例连接到现有 Azure Cosmos DB SQL API 数据库、创建新数据库和容器、从容器中读取某个项以及将其反序列化为 `TodoItem` 对象。</span><span class="sxs-lookup"><span data-stu-id="0cf34-122">This example connects to an existing Azure Cosmos DB SQL API database, creates a new database and container, reads an item from the container, and deserializes it to a `TodoItem` object.</span></span> <span data-ttu-id="0cf34-123">此示例使用 .NET SDK 的 3.x 版本。</span><span class="sxs-lookup"><span data-stu-id="0cf34-123">This example uses version 3.x of the .NET SDK.</span></span>   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0cf34-124">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="0cf34-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="0cf34-125">示例</span><span class="sxs-lookup"><span data-stu-id="0cf34-125">Samples</span></span>

* [<span data-ttu-id="0cf34-126">使用 Azure Cosmos DB 的 SQL API 开发 .NET 应用（版本 2.x）</span><span class="sxs-lookup"><span data-stu-id="0cf34-126">Developing a .NET app using Azure Cosmos DB's SQL API (Version 2.x)</span></span>](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [<span data-ttu-id="0cf34-127">使用 Azure Cosmos DB 的 SQL API 开发 .NET 应用（3.x 预览版）</span><span class="sxs-lookup"><span data-stu-id="0cf34-127">Developing a .NET app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [<span data-ttu-id="0cf34-128">使用 Azure Cosmos DB 的 SQL API 开发 .NET Core 应用（3.x 预览版）</span><span class="sxs-lookup"><span data-stu-id="0cf34-128">Developing a .NET Core app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

<span data-ttu-id="0cf34-129">查看 Azure Cosmos DB 示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="0cf34-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
