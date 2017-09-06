---
title: "用于 .NET 的 Azure CDN 库"
description: "用于 .NET 的 Azure CDN 库参考"
keywords: Azure, .NET, SDK, API, CDN
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cdn
ms.openlocfilehash: 1582f85c6e25a973fdf0294afb4393e6622e92a0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cdn-libraries-for-net"></a>用于 .NET 的 Azure CDN 库

## <a name="overview"></a>概述

Azure 内容交付网络 (CDN) 将静态 Web 内容缓存在按特定策略布置好的位置，以便提供最大的吞吐量，方便将内容交付给用户。 CDN 为开发人员提供了一个全局解决方案，通过在世界各地的物理节点缓存内容来交付高带宽内容。

若要详细了解 Azure CDN，请参阅 [Azure 内容交付网络概述](https://docs.microsoft.com/azure/cdn/cdn-overview)。


## <a name="management-library"></a>管理库

可以使用用于 .NET 的 Azure CDN 库来自动创建和管理 CDN 配置文件与终结点。 

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a>示例

此示例创建一个新的 CDN 配置文件，其中包含指向 `www.contoso.com` 的新终结点。

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
> [了解管理 API](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a>示例

* [CDN 入门 - 在 .NET 中管理 CDN](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
