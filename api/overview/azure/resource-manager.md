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
# <a name="azure-resource-manager-libraries-for-net"></a>用于 .NET 的 Azure 资源管理器库

## <a name="overview"></a>概述

那么，可以使用 Azure 资源管理器以组的方式处理解决方案中的资源。  有关资源管理器的详细信息，请参阅 [Azure 资源管理器概述](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。

## <a name="management-library"></a>管理库

使用用于 .NET 的 Azure 资源管理器库可创建、更新、删除和列出资源与资源组。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a>示例

此示例创建新的资源组。

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
> [了解管理 API](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a>示例

* [管理资源组](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [管理资源](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [使用 ARM 模板部署资源](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [使用 ARM 模板部署资源（显示进度）](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
