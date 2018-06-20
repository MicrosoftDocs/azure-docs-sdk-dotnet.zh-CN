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
ms.locfileid: "31005804"
---
# <a name="azure-cosmos-db-libraries-for-net"></a>用于 .NET 的 Azure Cosmos DB 库

## <a name="overview"></a>概述

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) 是分布式的可缩放数据存储，支持多种不同类型的数据库。

[Cosmos DB 入门](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。

## <a name="client-library"></a>客户端库

使用 Azure Cosmos DB .NET 客户端库在现有 Azure Cosmos DB 数据存储中访问和存储数据。  若要自动创建新的 Azure Cosmos DB 帐户，请使用 Azure 门户、CLI 或 PowerShell。

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

此示例连接到现有的Azure Cosmos DB SQL API 数据库，从集合中读取文档，并将文档反序列化为 `Item` 对象。   

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

* [使用 Azure Cosmos DB 的 MongoDB API 开发 .NET 应用](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

查看 Azure Cosmos DB 示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
