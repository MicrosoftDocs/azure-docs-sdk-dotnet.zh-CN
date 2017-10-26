---
title: "用于 .NET 的 Azure 应用服务库"
description: "用于 .NET 的 Azure 应用服务库参考"
keywords: "Azure, .NET, SDK, API, web 应用, 应用服务, 移动, asp.net"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 9f54fb6aca934f07c6ae23a4ae40dc29fa48ec8b
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
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

* [使用用于 Azure 的 .NET SDK 管理 Web 应用](https://azure.microsoft.com/en-us/resources/samples/app-service-web-dotnet-manage/)
* [Azure 应用服务的 ASP.NET 示例](https://azure.microsoft.com/en-us/resources/samples/app-service-web-dotnet-get-started/)

查看 Azure 应用服务示例的[完整列表](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=app%20service)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package