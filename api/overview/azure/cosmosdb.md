---
title: 用于 .NET 的 Azure Cosmos DB 库
description: 用于 .NET 的 Azure Cosmos DB 库参考
keywords: Azure, .NET, SDK, API, Cosmos DB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 11/17/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: fa9bc7497ac189f18ee0ba14d72d4cdb23a05f0b
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2018
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="450fb-104">用于 .NET 的 Azure Cosmos DB 库</span><span class="sxs-lookup"><span data-stu-id="450fb-104">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="450fb-105">概述</span><span class="sxs-lookup"><span data-stu-id="450fb-105">Overview</span></span>

<span data-ttu-id="450fb-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是分布式的可缩放数据存储，支持多种不同类型的数据库。</span><span class="sxs-lookup"><span data-stu-id="450fb-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

<span data-ttu-id="450fb-107">[Cosmos DB 入门](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="450fb-107">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="450fb-108">客户端库</span><span class="sxs-lookup"><span data-stu-id="450fb-108">Client library</span></span>

<span data-ttu-id="450fb-109">使用 Azure Cosmos DB .NET 客户端库在现有 Azure Cosmos DB 数据存储中访问和存储数据。</span><span class="sxs-lookup"><span data-stu-id="450fb-109">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span>  <span data-ttu-id="450fb-110">若要自动创建新的 Azure Cosmos DB 帐户，请使用 Azure 门户、CLI 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="450fb-110">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="450fb-111">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)。</span><span class="sxs-lookup"><span data-stu-id="450fb-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="450fb-112">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="450fb-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="450fb-113">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="450fb-113">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="450fb-114">代码示例</span><span class="sxs-lookup"><span data-stu-id="450fb-114">Code Example</span></span>

<span data-ttu-id="450fb-115">此示例连接到现有的Azure Cosmos DB SQL API 数据库，从集合中读取文档，并将文档反序列化为 `Item` 对象。</span><span class="sxs-lookup"><span data-stu-id="450fb-115">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="450fb-116">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="450fb-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="450fb-117">示例</span><span class="sxs-lookup"><span data-stu-id="450fb-117">Samples</span></span>

* [<span data-ttu-id="450fb-118">使用 Azure Cosmos DB 的 MongoDB API 开发 .NET 应用</span><span class="sxs-lookup"><span data-stu-id="450fb-118">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="450fb-119">查看 Azure Cosmos DB 示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="450fb-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
