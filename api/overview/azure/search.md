---
title: 用于 .NET 的 Azure 搜索库
description: 用于 .NET 的 Azure 搜索库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: search
ms.openlocfilehash: cf622ccb59f10a5270c02fa76d7396345fbb1a9b
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190240"
---
# <a name="azure-search-libraries-for-net"></a>用于 .NET 的 Azure 搜索库

## <a name="overview"></a>概述

[Azure 搜索](https://docs.microsoft.com/azure/search/search-what-is-azure-search)是一个完全托管的云搜索服务，可基于 Web、移动和企业应用程序中的数据提供丰富的搜索体验。

## <a name="client-library"></a>客户端库

使用 Azure 搜索客户端库可访问搜索服务、索引、文档或其他对象并对其执行索引和搜索操作。 有关分步介绍，请参阅[如何通过 .NET 应用程序使用 Azure 搜索](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Search)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a>代码示例

```csharp
/* Include these 'using' directives:
   using Microsoft.Azure.Search;
   using Microsoft.Azure.Search.Models;
*/

// A service endpoint and an api-key are required on a connection.
// Set them in a config file (not shown) and then connect to the client.
IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
IConfigurationRoot configuration = builder.Build();

SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

// Create an index named hotels
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a>管理库

使用 Azure 搜索管理库可预配服务、管理 API 密钥，以及调整资源。 服务管理依赖于使用 Azure 资源管理器来识别订阅方和租户。 通常，若要支持工作流，还需要在 Azure Active Directory 中完成身份验证和应用程序注册。 有关 Azure 搜索服务预配的简介，请参阅[如何使用管理 REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api)。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Search)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a>示例

 + [Azure 示例 / search-dotnet-getting-started](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [Azure 示例 / search-dotnet-management-api](https://github.com/Azure-Samples/search-dotnet-management-api)

在 Github 上的 [Azure 示例存储库](https://github.com/Azure-Samples/)中查找更多的搜索示例。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
