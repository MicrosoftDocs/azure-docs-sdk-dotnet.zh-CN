---
title: "用于 .NET 的 Azure Redis 缓存库"
description: "用于 .NET 的 Azure Redis 缓存库参考"
keywords: "Azure, .NET, SDK, API, Redis 缓存"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: redis-cache
ms.openlocfilehash: 2316a179712b143b7e099f4592035c489d270bc3
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-redis-cache-libraries-for-net"></a>用于 .NET 的 Azure Redis 缓存库

## <a name="overview"></a>概述

Azure Redis 缓存是一个安全的数据缓存和消息传送中转站，可让应用程序以较高的吞吐量、较低的延迟访问数据。  有关详细信息，请参阅[如何使用 Redis 缓存](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache)。

## <a name="client-library"></a>客户端库

Azure Redis 缓存与任何 Redis 客户端 API（包括 `StackExchange.Redis`）兼容。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/StackExchange.Redis)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a>示例

此示例连接到 Redis 缓存数据库实例，根据名称将一些字符串添加到缓存，然后再次检索这些字符串。

```csharp
/* Include this "using" directive.
using StackExchange.Redis;
*/

ConnectionMultiplexer connection = 
    ConnectionMultiplexer.Connect("contoso.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    IDatabase cache = connection.GetDatabase();

// Perform cache operations using the cache object...
// Simple put of integral data types into the cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from the cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

## <a name="management-library"></a>管理库

使用 Redis 缓存管理库可以管理 Redis 缓存资源和访问密钥。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a>示例

此示例创建新的 Redis 缓存。

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.Redis.Fluent;
*/

IRedisCache redisCache1 = azure.RedisCaches.Define("RedisCacheName")
    .WithRegion(Region.USCentral)
    .WithNewResourceGroup("ResourceGroupName")
    .WithBasicSku()
    .Create();
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a>示例

* [Redis 入门 - 在 .NET 中管理 Redis](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
