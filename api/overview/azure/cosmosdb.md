---
title: "用于 .NET 的 Azure CosmosDB 库"
description: "用于 .NET 的 Azure CosmosDB 库参考"
keywords: Azure, .NET, SDK, API, CosmosDB
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: babf34e98dae439a2dc3d4c63bd638335428e935
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cosmosdb-libraries-for-net"></a>用于 .NET 的 Azure CosmosDB 库

## <a name="overview"></a>概述

[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是分布式的可缩放数据存储，支持多种不同类型的数据库。

## <a name="client-library"></a>客户端库

使用 CosmosDB .NET 客户端库在 CosmosDB 数据存储中访问和存储数据。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a>代码示例

此示例连接到现有的 CosmosDB DocumentDB API 数据库，从集合中读取文档，并将文档反序列化为 `Item` 对象。

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
// "Item" is a class defined elsewhere...
Item item = client.ReadDocumentAsync<Item>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>示例

* [使用 Azure Cosmos DB 的 MongoDB API 开发 .NET 应用](https://azure.microsoft.com/en-us/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

查看 Azure Cosmos DB 示例的[完整列表](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
