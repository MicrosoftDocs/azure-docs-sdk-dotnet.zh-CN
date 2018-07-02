---
title: 用于 .NET 的 Azure 流量管理器库
description: 用于 .NET 的 Azure 流量管理器库参考
keywords: Azure, .NET, SDK, API, 流量管理器
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: traffic-manager
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 05856cbe48a5cf5f0c9ebf43609a029928f490f9
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065867"
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="6ad2f-104">用于 .NET 的 Azure 流量管理器库</span><span class="sxs-lookup"><span data-stu-id="6ad2f-104">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6ad2f-105">概述</span><span class="sxs-lookup"><span data-stu-id="6ad2f-105">Overview</span></span>

<span data-ttu-id="6ad2f-106">使用 Microsoft Azure 流量管理器，可以控制用户流量在不同数据中心内的服务终结点上的分布。</span><span class="sxs-lookup"><span data-stu-id="6ad2f-106">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="6ad2f-107">流量管理器支持的服务终结点包括 Azure VM、Web 应用和云服务。</span><span class="sxs-lookup"><span data-stu-id="6ad2f-107">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="6ad2f-108">也可将流量管理器用于外部的非 Azure 终结点。</span><span class="sxs-lookup"><span data-stu-id="6ad2f-108">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="6ad2f-109">详细了解 [Azure 流量管理器](/azure/traffic-manager/traffic-manager-overview)。</span><span class="sxs-lookup"><span data-stu-id="6ad2f-109">Learn more about [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="6ad2f-110">管理库</span><span class="sxs-lookup"><span data-stu-id="6ad2f-110">Management library</span></span>

<span data-ttu-id="6ad2f-111">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="6ad2f-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6ad2f-112">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="6ad2f-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ad2f-113">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="6ad2f-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="6ad2f-114">示例</span><span class="sxs-lookup"><span data-stu-id="6ad2f-114">Samples</span></span>

<span data-ttu-id="6ad2f-115">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="6ad2f-115">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package