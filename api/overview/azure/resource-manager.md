---
title: 用于 .NET 的 Azure 资源管理器库
description: 用于 .NET 的 Azure 资源管理器库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 6d3a27c5f7ba94f5579723cc4f798826c8bdefd6
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190832"
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="abeaa-103">用于 .NET 的 Azure 资源管理器库</span><span class="sxs-lookup"><span data-stu-id="abeaa-103">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="abeaa-104">概述</span><span class="sxs-lookup"><span data-stu-id="abeaa-104">Overview</span></span>

<span data-ttu-id="abeaa-105">那么，可以使用 Azure 资源管理器以组的方式处理解决方案中的资源。</span><span class="sxs-lookup"><span data-stu-id="abeaa-105">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="abeaa-106">有关资源管理器的详细信息，请参阅 [Azure 资源管理器概述](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。</span><span class="sxs-lookup"><span data-stu-id="abeaa-106">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="abeaa-107">管理库</span><span class="sxs-lookup"><span data-stu-id="abeaa-107">Management library</span></span>

<span data-ttu-id="abeaa-108">使用用于 .NET 的 Azure 资源管理器库可创建、更新、删除和列出资源与资源组。</span><span class="sxs-lookup"><span data-stu-id="abeaa-108">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="abeaa-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="abeaa-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="abeaa-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="abeaa-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="abeaa-111">示例</span><span class="sxs-lookup"><span data-stu-id="abeaa-111">Example</span></span>

<span data-ttu-id="abeaa-112">此示例创建新的资源组。</span><span class="sxs-lookup"><span data-stu-id="abeaa-112">This example creates a new resource group.</span></span>

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
> [<span data-ttu-id="abeaa-113">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="abeaa-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="abeaa-114">示例</span><span class="sxs-lookup"><span data-stu-id="abeaa-114">Samples</span></span>

* [<span data-ttu-id="abeaa-115">管理资源组</span><span class="sxs-lookup"><span data-stu-id="abeaa-115">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="abeaa-116">管理资源</span><span class="sxs-lookup"><span data-stu-id="abeaa-116">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="abeaa-117">使用 ARM 模板部署资源</span><span class="sxs-lookup"><span data-stu-id="abeaa-117">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="abeaa-118">使用 ARM 模板部署资源（显示进度）</span><span class="sxs-lookup"><span data-stu-id="abeaa-118">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
