---
title: 用于 .NET 的 Azure Redis 缓存库
description: 用于 .NET 的 Azure Redis 缓存库参考
keywords: Azure, .NET, SDK, API, Redis 缓存
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: redis-cache
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 64bb5a43cec8c82412b3dc7b60fea1e8566ab399
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566338"
---
# <a name="azure-redis-cache-libraries-for-net"></a><span data-ttu-id="7d192-104">用于 .NET 的 Azure Redis 缓存库</span><span class="sxs-lookup"><span data-stu-id="7d192-104">Azure Redis Cache libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7d192-105">概述</span><span class="sxs-lookup"><span data-stu-id="7d192-105">Overview</span></span>

<span data-ttu-id="7d192-106">Azure Redis 缓存是一个安全的数据缓存和消息传送中转站，可让应用程序以较高的吞吐量、较低的延迟访问数据。</span><span class="sxs-lookup"><span data-stu-id="7d192-106">Azure Redis Cache is a secure data cache and messaging broker that provides high throughput and low-latency access to data for applications.</span></span>  <span data-ttu-id="7d192-107">有关详细信息，请参阅[如何使用 Redis 缓存](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache)。</span><span class="sxs-lookup"><span data-stu-id="7d192-107">For more information, see [How to Use Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span></span>

## <a name="client-library"></a><span data-ttu-id="7d192-108">客户端库</span><span class="sxs-lookup"><span data-stu-id="7d192-108">Client library</span></span>

<span data-ttu-id="7d192-109">Azure Redis 缓存与任何 Redis 客户端 API（包括 `StackExchange.Redis`）兼容。</span><span class="sxs-lookup"><span data-stu-id="7d192-109">Azure Redis Cache is compatible with any Redis client API, including `StackExchange.Redis`.</span></span>

<span data-ttu-id="7d192-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/StackExchange.Redis)。</span><span class="sxs-lookup"><span data-stu-id="7d192-110">Install the [NuGet package](https://www.nuget.org/packages/StackExchange.Redis) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7d192-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="7d192-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a><span data-ttu-id="7d192-112">示例</span><span class="sxs-lookup"><span data-stu-id="7d192-112">Example</span></span>

<span data-ttu-id="7d192-113">此示例连接到 Redis 缓存数据库实例，根据名称将一些字符串添加到缓存，然后再次检索这些字符串。</span><span class="sxs-lookup"><span data-stu-id="7d192-113">This example connects to a Redis Cache database instance, adds some strings to the cache by name, and then retrieves them again.</span></span>

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

## <a name="management-library"></a><span data-ttu-id="7d192-114">管理库</span><span class="sxs-lookup"><span data-stu-id="7d192-114">Management library</span></span>

<span data-ttu-id="7d192-115">使用 Redis 缓存管理库可以管理 Redis 缓存资源和访问密钥。</span><span class="sxs-lookup"><span data-stu-id="7d192-115">The Redis Cache management library allows you to manage Redis Cache resources and access keys.</span></span>

<span data-ttu-id="7d192-116">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="7d192-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7d192-117">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="7d192-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a><span data-ttu-id="7d192-118">示例</span><span class="sxs-lookup"><span data-stu-id="7d192-118">Example</span></span>

<span data-ttu-id="7d192-119">此示例创建新的 Redis 缓存。</span><span class="sxs-lookup"><span data-stu-id="7d192-119">This example creates a new Redis Cache.</span></span>

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
> [<span data-ttu-id="7d192-120">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="7d192-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a><span data-ttu-id="7d192-121">示例</span><span class="sxs-lookup"><span data-stu-id="7d192-121">Samples</span></span>

* [<span data-ttu-id="7d192-122">Redis 入门 - 在 .NET 中管理 Redis</span><span class="sxs-lookup"><span data-stu-id="7d192-122">Getting Started with Redis - Manage Redis - in .NET</span></span>](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
