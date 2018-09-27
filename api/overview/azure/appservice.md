---
title: 用于 .NET 的 Azure 应用服务库
description: 用于 .NET 的 Azure 应用服务库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: app-service
ms.openlocfilehash: 82f8eccfafd2f7b1cf1df1ce0f40212509ccddd3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189990"
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="d4f0d-103">用于 .NET 的 Azure 应用服务库</span><span class="sxs-lookup"><span data-stu-id="d4f0d-103">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d4f0d-104">概述</span><span class="sxs-lookup"><span data-stu-id="d4f0d-104">Overview</span></span>

<span data-ttu-id="d4f0d-105">使用 [Azure 应用服务](/azure/app-service/app-service-value-prop-what-is)可以部署和缩放网站、Web 应用程序、服务和 REST API。</span><span class="sxs-lookup"><span data-stu-id="d4f0d-105">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="d4f0d-106">管理 API</span><span class="sxs-lookup"><span data-stu-id="d4f0d-106">Management API</span></span>

<span data-ttu-id="d4f0d-107">使用管理 API 来部署、管理和缩放 Azure 应用服务中托管的元素。</span><span class="sxs-lookup"><span data-stu-id="d4f0d-107">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="d4f0d-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="d4f0d-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d4f0d-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="d4f0d-109">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="d4f0d-110">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="d4f0d-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="d4f0d-111">代码示例</span><span class="sxs-lookup"><span data-stu-id="d4f0d-111">Code Example</span></span>

<span data-ttu-id="d4f0d-112">创建新的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="d4f0d-112">Create a new web app.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.AppService.Fluent;
*/

IWebApp app1 = azure.WebApps
    .Define("MyUniqueWebAddress")
    .WithRegion(Region.USWest)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewWindowsPlan(PricingTier.StandardS1)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d4f0d-113">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="d4f0d-113">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="d4f0d-114">示例</span><span class="sxs-lookup"><span data-stu-id="d4f0d-114">Samples</span></span>

* [<span data-ttu-id="d4f0d-115">使用用于 Azure 的 .NET SDK 管理 Web 应用</span><span class="sxs-lookup"><span data-stu-id="d4f0d-115">Manage your web apps with the .NET SDK for Azure</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [<span data-ttu-id="d4f0d-116">Azure 应用服务的 ASP.NET 示例</span><span class="sxs-lookup"><span data-stu-id="d4f0d-116">ASP.NET sample for Azure App Service</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

<span data-ttu-id="d4f0d-117">查看 Azure 应用服务示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service)。</span><span class="sxs-lookup"><span data-stu-id="d4f0d-117">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package