---
title: "用于 .NET 的 Azure 搜索库"
description: "用于 .NET 的 Azure 搜索库参考"
keywords: "Azure, .NET, SDK, API, 搜索"
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 5330e0642bc27c97c4acc0857d4b92e6fc2a027c
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-search-libraries-for-net"></a><span data-ttu-id="3142a-104">用于 .NET 的 Azure 搜索库</span><span class="sxs-lookup"><span data-stu-id="3142a-104">Azure Search libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3142a-105">概述</span><span class="sxs-lookup"><span data-stu-id="3142a-105">Overview</span></span>

<span data-ttu-id="3142a-106">[Azure 搜索](https://docs.microsoft.com/azure/search/search-what-is-azure-search)是一个完全托管的云搜索服务，可基于 Web、移动和企业应用程序中的数据提供丰富的搜索体验。</span><span class="sxs-lookup"><span data-stu-id="3142a-106">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) is a fully managed cloud search service that provides a rich search experience over data in web, mobile, and enterprise applications.</span></span>

## <a name="client-library"></a><span data-ttu-id="3142a-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="3142a-107">Client library</span></span>

<span data-ttu-id="3142a-108">使用 Azure 搜索客户端库可访问搜索服务、索引、文档或其他对象并对其执行索引和搜索操作。</span><span class="sxs-lookup"><span data-stu-id="3142a-108">Use the Azure Search client library to access and execute indexing and search operations on a search service, index, documents, or other object.</span></span> <span data-ttu-id="3142a-109">有关分步介绍，请参阅[如何通过 .NET 应用程序使用 Azure 搜索](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)。</span><span class="sxs-lookup"><span data-stu-id="3142a-109">For a step-by-step introduction, see [How to use Azure Search from a .NET application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

<span data-ttu-id="3142a-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Search)。</span><span class="sxs-lookup"><span data-stu-id="3142a-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3142a-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="3142a-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a><span data-ttu-id="3142a-112">代码示例</span><span class="sxs-lookup"><span data-stu-id="3142a-112">Code Example</span></span>

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
> [<span data-ttu-id="3142a-113">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="3142a-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a><span data-ttu-id="3142a-114">管理库</span><span class="sxs-lookup"><span data-stu-id="3142a-114">Management library</span></span>

<span data-ttu-id="3142a-115">使用 Azure 搜索管理库可预配服务、管理 API 密钥，以及调整资源。</span><span class="sxs-lookup"><span data-stu-id="3142a-115">Use the Azure Search management library to provision a service, manage api-keys, and adjust resources.</span></span> <span data-ttu-id="3142a-116">服务管理依赖于使用 Azure 资源管理器来识别订阅方和租户。</span><span class="sxs-lookup"><span data-stu-id="3142a-116">Service management has a dependency on Azure Resource Manager for subscriber and tenant identification.</span></span> <span data-ttu-id="3142a-117">通常，若要支持工作流，还需要在 Azure Active Directory 中完成身份验证和应用程序注册。</span><span class="sxs-lookup"><span data-stu-id="3142a-117">Typically, authentication and application registration with Azure Active Directory is also necessary to support the workflow.</span></span> <span data-ttu-id="3142a-118">有关 Azure 搜索服务预配的简介，请参阅[如何使用管理 REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api)。</span><span class="sxs-lookup"><span data-stu-id="3142a-118">For an introduction to Azure Search service provisioning, see [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span></span>

<span data-ttu-id="3142a-119">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Search)。</span><span class="sxs-lookup"><span data-stu-id="3142a-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3142a-120">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="3142a-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3142a-121">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="3142a-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a><span data-ttu-id="3142a-122">示例</span><span class="sxs-lookup"><span data-stu-id="3142a-122">Samples</span></span>

 + [<span data-ttu-id="3142a-123">Azure 示例 / search-dotnet-getting-started</span><span class="sxs-lookup"><span data-stu-id="3142a-123">Azure Samples / search-dotnet-getting-started</span></span>](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [<span data-ttu-id="3142a-124">Azure 示例 / search-dotnet-management-api</span><span class="sxs-lookup"><span data-stu-id="3142a-124">Azure Samples / search-dotnet-management-api</span></span>](https://github.com/Azure-Samples/search-dotnet-management-api)

<span data-ttu-id="3142a-125">在 Github 上的 [Azure 示例存储库](https://github.com/Azure-Samples/)中查找更多的搜索示例。</span><span class="sxs-lookup"><span data-stu-id="3142a-125">Find more search samples in the [Azure samples repository](https://github.com/Azure-Samples/) on Github.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
