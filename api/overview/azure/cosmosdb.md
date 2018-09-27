---
title: 用于 .NET 的 Azure Cosmos DB 库
description: 用于 .NET 的 Azure Cosmos DB 库参考
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 21a2f2168259528a0d27103783e34aa532d7e17a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190784"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="11146-103">用于 .NET 的 Azure Cosmos DB 库</span><span class="sxs-lookup"><span data-stu-id="11146-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="11146-104">概述</span><span class="sxs-lookup"><span data-stu-id="11146-104">Overview</span></span>

<span data-ttu-id="11146-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是一种全球分布式多模型数据库服务。</span><span class="sxs-lookup"><span data-stu-id="11146-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="11146-106">它旨在通过一个综合性 SLA 跨任意数量的地理区域以富有弹性的方式独立缩放吞吐量和存储空间。</span><span class="sxs-lookup"><span data-stu-id="11146-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="11146-107">有了 Azure Cosmos DB，可以通过使用 API 和编程模型存储和访问文档、键值、宽列和图形数据库。</span><span class="sxs-lookup"><span data-stu-id="11146-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="11146-108">[Cosmos DB 入门](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="11146-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="11146-109">客户端库</span><span class="sxs-lookup"><span data-stu-id="11146-109">Client library</span></span>

<span data-ttu-id="11146-110">使用 Azure Cosmos DB .NET 客户端库在现有 Azure Cosmos DB 数据存储中访问和存储数据。</span><span class="sxs-lookup"><span data-stu-id="11146-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="11146-111">若要自动创建新的 Azure Cosmos DB 帐户，请使用 Azure 门户、CLI 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="11146-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="11146-112">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)。</span><span class="sxs-lookup"><span data-stu-id="11146-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="11146-113">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="11146-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="11146-114">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="11146-114">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="11146-115">代码示例</span><span class="sxs-lookup"><span data-stu-id="11146-115">Code Example</span></span>

<span data-ttu-id="11146-116">此示例连接到现有的Azure Cosmos DB SQL API 数据库，从集合中读取文档，并将文档反序列化为 `Item` 对象。</span><span class="sxs-lookup"><span data-stu-id="11146-116">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="11146-117">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="11146-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="11146-118">示例</span><span class="sxs-lookup"><span data-stu-id="11146-118">Samples</span></span>

* [<span data-ttu-id="11146-119">使用 Azure Cosmos DB 的 MongoDB API 开发 .NET 应用</span><span class="sxs-lookup"><span data-stu-id="11146-119">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="11146-120">查看 Azure Cosmos DB 示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。</span><span class="sxs-lookup"><span data-stu-id="11146-120">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
