---
title: 用于 .NET 的 Azure 资源管理器库
description: 用于 .NET 的 Azure 资源管理器库参考
keywords: Azure, .NET, SDK, API, 资源管理器
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f9fe96fcdc94d3d27445f462c5220def9f2966da
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566368"
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="3610d-104">用于 .NET 的 Azure 资源管理器库</span><span class="sxs-lookup"><span data-stu-id="3610d-104">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3610d-105">概述</span><span class="sxs-lookup"><span data-stu-id="3610d-105">Overview</span></span>

<span data-ttu-id="3610d-106">那么，可以使用 Azure Resource Manager 以组的方式处理解决方案中的资源。</span><span class="sxs-lookup"><span data-stu-id="3610d-106">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="3610d-107">有关资源管理器的详细信息，请参阅 [Azure 资源管理器概述](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。</span><span class="sxs-lookup"><span data-stu-id="3610d-107">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="3610d-108">管理库</span><span class="sxs-lookup"><span data-stu-id="3610d-108">Management library</span></span>

<span data-ttu-id="3610d-109">使用用于 .NET 的 Azure 资源管理器库可创建、更新、删除和列出资源与资源组。</span><span class="sxs-lookup"><span data-stu-id="3610d-109">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="3610d-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="3610d-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3610d-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="3610d-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="3610d-112">示例</span><span class="sxs-lookup"><span data-stu-id="3610d-112">Example</span></span>

<span data-ttu-id="3610d-113">此示例创建新的资源组。</span><span class="sxs-lookup"><span data-stu-id="3610d-113">This example creates a new resource group.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IResourceGroup resourceGroup = azure.ResourceGroups
    .Define("ResourceGroupName")
    .WithRegion(Region.USWest)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3610d-114">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="3610d-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="3610d-115">示例</span><span class="sxs-lookup"><span data-stu-id="3610d-115">Samples</span></span>

* [<span data-ttu-id="3610d-116">管理资源组</span><span class="sxs-lookup"><span data-stu-id="3610d-116">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="3610d-117">管理资源</span><span class="sxs-lookup"><span data-stu-id="3610d-117">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="3610d-118">使用 ARM 模板部署资源</span><span class="sxs-lookup"><span data-stu-id="3610d-118">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="3610d-119">使用 ARM 模板部署资源（显示进度）</span><span class="sxs-lookup"><span data-stu-id="3610d-119">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
