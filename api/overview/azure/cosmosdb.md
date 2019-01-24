---
title: 用于 .NET 的 Azure Cosmos DB 库
description: 用于 .NET 的 Azure Cosmos DB 库参考
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 95fcd8468c3d472cfcadeaae3b56ae789c3b1e7a
ms.sourcegitcommit: 55ee51501678d1575e5159f0ac0e475b5bf9daf3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2019
ms.locfileid: "54453991"
---
# <a name="azure-cosmos-db-libraries-for-net"></a>用于 .NET 的 Azure Cosmos DB 库

## <a name="overview"></a>概述

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是一种全球分布式多模型数据库服务。 它旨在通过一个综合性 SLA 跨任意数量的地理区域以富有弹性的方式独立缩放吞吐量和存储空间。 有了 Azure Cosmos DB，可以通过使用 API 和编程模型存储和访问文档、键值、宽列和图形数据库。 

[Cosmos DB 入门](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。

## <a name="client-library"></a>客户端库

使用 Azure Cosmos DB .NET 客户端库在现有 Azure Cosmos DB 数据存储中访问和存储数据。 若要自动创建新的 Azure Cosmos DB 帐户，请使用 Azure 门户、CLI 或 PowerShell。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)。

若要安装版本 2.x，请执行以下命令：

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

若要安装 3.0 预览版（面向 .NET Standard），请执行以下命令： 

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a>代码示例

此示例连接到现有的Azure Cosmos DB SQL API 数据库，从集合中读取文档，并将文档反序列化为 `TodoItem` 对象。 此示例使用 .NET SDK 的 2.x 版本。   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
var todoItem = client.ReadDocumentAsync<TodoItem>(documentUri);
```

此示例连接到现有 Azure Cosmos DB SQL API 数据库、创建新数据库和容器、从容器中读取某个项以及将其反序列化为 `TodoItem` 对象。 此示例使用 .NET SDK 的 3.x 版本。   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>示例

* [使用 Azure Cosmos DB 的 SQL API 开发 .NET 应用（版本 2.x）](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [使用 Azure Cosmos DB 的 SQL API 开发 .NET 应用（3.x 预览版）](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [使用 Azure Cosmos DB 的 SQL API 开发 .NET Core 应用（3.x 预览版）](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

查看 Azure Cosmos DB 示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
