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
# <a name="azure-search-libraries-for-net"></a><span data-ttu-id="ecc22-103">用于 .NET 的 Azure 搜索库</span><span class="sxs-lookup"><span data-stu-id="ecc22-103">Azure Search libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="ecc22-104">概述</span><span class="sxs-lookup"><span data-stu-id="ecc22-104">Overview</span></span>

<span data-ttu-id="ecc22-105">[Azure 搜索](https://docs.microsoft.com/azure/search/search-what-is-azure-search)是一个完全托管的云搜索服务，可基于 Web、移动和企业应用程序中的数据提供丰富的搜索体验。</span><span class="sxs-lookup"><span data-stu-id="ecc22-105">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) is a fully managed cloud search service that provides a rich search experience over data in web, mobile, and enterprise applications.</span></span>

## <a name="client-library"></a><span data-ttu-id="ecc22-106">客户端库</span><span class="sxs-lookup"><span data-stu-id="ecc22-106">Client library</span></span>

<span data-ttu-id="ecc22-107">使用 Azure 搜索客户端库可访问搜索服务、索引、文档或其他对象并对其执行索引和搜索操作。</span><span class="sxs-lookup"><span data-stu-id="ecc22-107">Use the Azure Search client library to access and execute indexing and search operations on a search service, index, documents, or other object.</span></span> <span data-ttu-id="ecc22-108">有关分步介绍，请参阅[如何通过 .NET 应用程序使用 Azure 搜索](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)。</span><span class="sxs-lookup"><span data-stu-id="ecc22-108">For a step-by-step introduction, see [How to use Azure Search from a .NET application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

<span data-ttu-id="ecc22-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Search)。</span><span class="sxs-lookup"><span data-stu-id="ecc22-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ecc22-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="ecc22-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a><span data-ttu-id="ecc22-111">代码示例</span><span class="sxs-lookup"><span data-stu-id="ecc22-111">Code Example</span></span>

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
> [<span data-ttu-id="ecc22-112">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="ecc22-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a><span data-ttu-id="ecc22-113">管理库</span><span class="sxs-lookup"><span data-stu-id="ecc22-113">Management library</span></span>

<span data-ttu-id="ecc22-114">使用 Azure 搜索管理库可预配服务、管理 API 密钥，以及调整资源。</span><span class="sxs-lookup"><span data-stu-id="ecc22-114">Use the Azure Search management library to provision a service, manage api-keys, and adjust resources.</span></span> <span data-ttu-id="ecc22-115">服务管理依赖于使用 Azure 资源管理器来识别订阅方和租户。</span><span class="sxs-lookup"><span data-stu-id="ecc22-115">Service management has a dependency on Azure Resource Manager for subscriber and tenant identification.</span></span> <span data-ttu-id="ecc22-116">通常，若要支持工作流，还需要在 Azure Active Directory 中完成身份验证和应用程序注册。</span><span class="sxs-lookup"><span data-stu-id="ecc22-116">Typically, authentication and application registration with Azure Active Directory is also necessary to support the workflow.</span></span> <span data-ttu-id="ecc22-117">有关 Azure 搜索服务预配的简介，请参阅[如何使用管理 REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api)。</span><span class="sxs-lookup"><span data-stu-id="ecc22-117">For an introduction to Azure Search service provisioning, see [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span></span>

<span data-ttu-id="ecc22-118">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Search)。</span><span class="sxs-lookup"><span data-stu-id="ecc22-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ecc22-119">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="ecc22-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ecc22-120">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="ecc22-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a><span data-ttu-id="ecc22-121">示例</span><span class="sxs-lookup"><span data-stu-id="ecc22-121">Samples</span></span>

 + [<span data-ttu-id="ecc22-122">Azure 示例 / search-dotnet-getting-started</span><span class="sxs-lookup"><span data-stu-id="ecc22-122">Azure Samples / search-dotnet-getting-started</span></span>](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [<span data-ttu-id="ecc22-123">Azure 示例 / search-dotnet-management-api</span><span class="sxs-lookup"><span data-stu-id="ecc22-123">Azure Samples / search-dotnet-management-api</span></span>](https://github.com/Azure-Samples/search-dotnet-management-api)

<span data-ttu-id="ecc22-124">在 Github 上的 [Azure 示例存储库](https://github.com/Azure-Samples/)中查找更多的搜索示例。</span><span class="sxs-lookup"><span data-stu-id="ecc22-124">Find more search samples in the [Azure samples repository](https://github.com/Azure-Samples/) on Github.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
