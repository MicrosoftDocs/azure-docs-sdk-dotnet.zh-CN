---
title: 用于 .NET 的 Azure CDN 库
description: 用于 .NET 的 Azure CDN 库参考
keywords: Azure, .NET, SDK, API, CDN
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cdn
ms.custom: devcenter, svc-overview
ms.openlocfilehash: afc63f943fcac3afd9afb7d85f6e699079829244
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566328"
---
# <a name="azure-cdn-libraries-for-net"></a><span data-ttu-id="88f74-104">用于 .NET 的 Azure CDN 库</span><span class="sxs-lookup"><span data-stu-id="88f74-104">Azure CDN libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="88f74-105">概述</span><span class="sxs-lookup"><span data-stu-id="88f74-105">Overview</span></span>

<span data-ttu-id="88f74-106">Azure 内容交付网络 (CDN) 将静态 Web 内容缓存在按特定策略布置好的位置，以便提供最大的吞吐量，方便将内容交付给用户。</span><span class="sxs-lookup"><span data-stu-id="88f74-106">The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="88f74-107">CDN 为开发人员提供了一个全局解决方案，通过在世界各地的物理节点缓存内容来交付高带宽内容。</span><span class="sxs-lookup"><span data-stu-id="88f74-107">The CDN offers developers a global solution for delivering high-bandwidth content by caching the content at physical nodes across the world.</span></span>

<span data-ttu-id="88f74-108">若要详细了解 Azure CDN，请参阅 [Azure 内容交付网络概述](https://docs.microsoft.com/azure/cdn/cdn-overview)。</span><span class="sxs-lookup"><span data-stu-id="88f74-108">To learn more about Azure CDN, see [Overview of the Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn/cdn-overview).</span></span>


## <a name="management-library"></a><span data-ttu-id="88f74-109">管理库</span><span class="sxs-lookup"><span data-stu-id="88f74-109">Management library</span></span>

<span data-ttu-id="88f74-110">可以使用用于 .NET 的 Azure CDN 库来自动创建和管理 CDN 配置文件与终结点。</span><span class="sxs-lookup"><span data-stu-id="88f74-110">You can use the Azure CDN Library for .NET to automate creation and management of CDN profiles and endpoints.</span></span> 

<span data-ttu-id="88f74-111">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="88f74-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="88f74-112">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="88f74-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a><span data-ttu-id="88f74-113">示例</span><span class="sxs-lookup"><span data-stu-id="88f74-113">Example</span></span>

<span data-ttu-id="88f74-114">此示例创建一个新的 CDN 配置文件，其中包含指向 `www.contoso.com` 的新终结点。</span><span class="sxs-lookup"><span data-stu-id="88f74-114">This example creates a new CDN profile with a new endpoint pointed to `www.contoso.com`.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.Cdn.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

ICdnProfile profileDefinition = azure.CdnProfiles.Define("CdnProfileName")
    .WithRegion(Region.USCentral)
    .WithExistingResourceGroup("ResourceGroupName")
    .WithStandardVerizonSku()
    .WithNewEndpoint("www.contoso.com")
    .Create();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="88f74-115">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="88f74-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a><span data-ttu-id="88f74-116">示例</span><span class="sxs-lookup"><span data-stu-id="88f74-116">Samples</span></span>

* [<span data-ttu-id="88f74-117">CDN 入门 - 在 .NET 中管理 CDN</span><span class="sxs-lookup"><span data-stu-id="88f74-117">Getting started with CDN - Manage CDN - in .NET</span></span>](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
