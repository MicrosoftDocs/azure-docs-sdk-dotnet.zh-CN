---
title: "用于 .NET 的 Azure CosmosDB 库"
description: "用于 .NET 的 Azure CosmosDB 库参考"
keywords: Azure, .NET, SDK, API, CosmosDB
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
ms.openlocfilehash: 9f29e53e7f202e48ade12e28f08487bbacd2833c
ms.sourcegitcommit: 9cc5f8da9e9a15ba07fd67fe8b9a2d4ee6b57c73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="azure-cosmosdb-libraries-for-net"></a>用于 .NET 的 Azure CosmosDB 库

## <a name="overview"></a>概述

[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是分布式的可缩放数据存储，支持多种不同类型的数据库。

[CosmosDB 入门](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet)。

## <a name="client-library"></a>客户端库

使用 CosmosDB .NET 客户端库在现有 CosmosDB 数据存储中访问和存储数据。  若要自动创建新的 CosmosDB 帐户，请使用 Azure 门户、CLI 或 PowerShell。

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
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>示例

* [使用 Azure Cosmos DB 的 MongoDB API 开发 .NET 应用](https://azure.microsoft.com/en-us/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

查看 Azure Cosmos DB 示例的[完整列表](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
