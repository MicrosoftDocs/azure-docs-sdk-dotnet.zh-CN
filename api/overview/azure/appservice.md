---
title: 用于 .NET 的 Azure 应用服务库
description: 用于 .NET 的 Azure 应用服务库参考
keywords: Azure, .NET, SDK, API, web 应用, 应用服务, 移动, asp.net
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 0fee28930dff5075cdd84fe3cb88850e07bc6ccb
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065797"
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="635b1-104">用于 .NET 的 Azure 应用服务库</span><span class="sxs-lookup"><span data-stu-id="635b1-104">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="635b1-105">概述</span><span class="sxs-lookup"><span data-stu-id="635b1-105">Overview</span></span>

<span data-ttu-id="635b1-106">使用 [Azure 应用服务](/azure/app-service/app-service-value-prop-what-is)可以部署和缩放网站、Web 应用程序、服务和 REST API。</span><span class="sxs-lookup"><span data-stu-id="635b1-106">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="635b1-107">管理 API</span><span class="sxs-lookup"><span data-stu-id="635b1-107">Management API</span></span>

<span data-ttu-id="635b1-108">使用管理 API 来部署、管理和缩放 Azure 应用服务中托管的元素。</span><span class="sxs-lookup"><span data-stu-id="635b1-108">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="635b1-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="635b1-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="635b1-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="635b1-110">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="635b1-111">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="635b1-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="635b1-112">代码示例</span><span class="sxs-lookup"><span data-stu-id="635b1-112">Code Example</span></span>

<span data-ttu-id="635b1-113">创建新的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="635b1-113">Create a new web app.</span></span>

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
> [<span data-ttu-id="635b1-114">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="635b1-114">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="635b1-115">示例</span><span class="sxs-lookup"><span data-stu-id="635b1-115">Samples</span></span>

* [<span data-ttu-id="635b1-116">使用用于 Azure 的 .NET SDK 管理 Web 应用</span><span class="sxs-lookup"><span data-stu-id="635b1-116">Manage your web apps with the .NET SDK for Azure</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [<span data-ttu-id="635b1-117">Azure 应用服务的 ASP.NET 示例</span><span class="sxs-lookup"><span data-stu-id="635b1-117">ASP.NET sample for Azure App Service</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

<span data-ttu-id="635b1-118">查看 Azure 应用服务示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service)。</span><span class="sxs-lookup"><span data-stu-id="635b1-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package