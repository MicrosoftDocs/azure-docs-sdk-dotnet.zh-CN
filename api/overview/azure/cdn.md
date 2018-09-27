---
title: 用于 .NET 的 Azure CDN 库
description: 用于 .NET 的 Azure CDN 库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: cdn
ms.openlocfilehash: 6475edbe4fa0d01739de5cff76038aa6e7fd2cf9
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190120"
---
# <a name="azure-cdn-libraries-for-net"></a><span data-ttu-id="819c9-103">用于 .NET 的 Azure CDN 库</span><span class="sxs-lookup"><span data-stu-id="819c9-103">Azure CDN libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="819c9-104">概述</span><span class="sxs-lookup"><span data-stu-id="819c9-104">Overview</span></span>

<span data-ttu-id="819c9-105">Azure 内容分发网络 (CDN) 将静态 Web 内容缓存在按特定策略布置好的位置，以便提供最大的吞吐量，方便将内容分发给用户。</span><span class="sxs-lookup"><span data-stu-id="819c9-105">The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="819c9-106">CDN 将内容缓存在世界各地的物理节点，从而为开发人员提供交付高带宽内容的全球解决方案。</span><span class="sxs-lookup"><span data-stu-id="819c9-106">The CDN offers developers a global solution for delivering high-bandwidth content by caching the content at physical nodes across the world.</span></span>

<span data-ttu-id="819c9-107">若要详细了解 Azure CDN，请参阅 [Azure 内容分发网络概述](https://docs.microsoft.com/azure/cdn/cdn-overview)。</span><span class="sxs-lookup"><span data-stu-id="819c9-107">To learn more about Azure CDN, see [Overview of the Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn/cdn-overview).</span></span>


## <a name="management-library"></a><span data-ttu-id="819c9-108">管理库</span><span class="sxs-lookup"><span data-stu-id="819c9-108">Management library</span></span>

<span data-ttu-id="819c9-109">可以使用用于 .NET 的 Azure CDN 库来自动创建和管理 CDN 配置文件与终结点。</span><span class="sxs-lookup"><span data-stu-id="819c9-109">You can use the Azure CDN Library for .NET to automate creation and management of CDN profiles and endpoints.</span></span> 

<span data-ttu-id="819c9-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="819c9-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="819c9-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="819c9-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a><span data-ttu-id="819c9-112">示例</span><span class="sxs-lookup"><span data-stu-id="819c9-112">Example</span></span>

<span data-ttu-id="819c9-113">此示例创建一个新的 CDN 配置文件，其中包含指向 `www.contoso.com` 的新终结点。</span><span class="sxs-lookup"><span data-stu-id="819c9-113">This example creates a new CDN profile with a new endpoint pointed to `www.contoso.com`.</span></span>

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
> [<span data-ttu-id="819c9-114">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="819c9-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a><span data-ttu-id="819c9-115">示例</span><span class="sxs-lookup"><span data-stu-id="819c9-115">Samples</span></span>

* [<span data-ttu-id="819c9-116">CDN 入门 - 在 .NET 中管理 CDN</span><span class="sxs-lookup"><span data-stu-id="819c9-116">Getting started with CDN - Manage CDN - in .NET</span></span>](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
