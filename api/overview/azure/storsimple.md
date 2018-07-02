---
title: 适用于 .NET 的 Azure StorSimple 库
description: 适用于 .NET 的 Azure StorSimple 存储库参考
keywords: Azure, .NET, SDK, API, StorSimple
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/27/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: storsimple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 818c48a0f45812841eb0e8c3928b59f6681892cf
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065897"
---
# <a name="azure-storsimple-libraries-for-net"></a><span data-ttu-id="4b6ca-104">适用于 .NET 的 Azure StorSimple 库</span><span class="sxs-lookup"><span data-stu-id="4b6ca-104">Azure StorSimple libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="4b6ca-105">概述</span><span class="sxs-lookup"><span data-stu-id="4b6ca-105">Overview</span></span>

<span data-ttu-id="4b6ca-106">Microsoft Azure StorSimple 是一种企业存储解决方案，它提供与基于云的存储的物理 iSCSI 或 SMB 接口。</span><span class="sxs-lookup"><span data-stu-id="4b6ca-106">Microsoft Azure StorSimple is an enterprise storage solution that provides physical iSCSI or SMB interfaces to cloud-based storage.</span></span> 

<span data-ttu-id="4b6ca-107">了解有关 [Azure StorSimple](/azure/storsimple/) 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="4b6ca-107">Learn more about [Azure StorSimple](/azure/storsimple/).</span></span>    

## <a name="management-library"></a><span data-ttu-id="4b6ca-108">管理库</span><span class="sxs-lookup"><span data-stu-id="4b6ca-108">Management library</span></span>

<span data-ttu-id="4b6ca-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.StorSimple.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="4b6ca-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StorSimple.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="4b6ca-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="4b6ca-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StorSimple.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.StorSimple.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b6ca-111">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="4b6ca-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/monitor/management)

## <a name="samples"></a><span data-ttu-id="4b6ca-112">示例</span><span class="sxs-lookup"><span data-stu-id="4b6ca-112">Samples</span></span>

<span data-ttu-id="4b6ca-113">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="4b6ca-113">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package