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
# <a name="azure-app-service-libraries-for-net"></a>用于 .NET 的 Azure 应用服务库

## <a name="overview"></a>概述

使用 [Azure 应用服务](/azure/app-service/app-service-value-prop-what-is)可以部署和缩放网站、Web 应用程序、服务和 REST API。

## <a name="management-api"></a>管理 API

使用管理 API 来部署、管理和缩放 Azure 应用服务中托管的元素。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)。


#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a>代码示例

创建新的 Web 应用。

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
> [了解管理 API](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a>示例

* [使用用于 Azure 的 .NET SDK 管理 Web 应用](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [Azure 应用服务的 ASP.NET 示例](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

查看 Azure 应用服务示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package