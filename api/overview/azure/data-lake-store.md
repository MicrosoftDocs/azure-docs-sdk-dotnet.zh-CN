---
title: "用于 .NET 的 Azure Data Lake Store 库"
description: "用于 .NET 的 Azure Data Lake Store 库参考"
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e8380c4a9ebf86f03fe87fc800dffda10e48e60a
ms.sourcegitcommit: 3e904e6e4f04f1c92d729459434c85faff32e386
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="d6ddc-104">用于 .NET 的 Azure Data Lake Store 库</span><span class="sxs-lookup"><span data-stu-id="d6ddc-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d6ddc-105">概述</span><span class="sxs-lookup"><span data-stu-id="d6ddc-105">Overview</span></span>

<span data-ttu-id="d6ddc-106">Azure Data Lake Store 是一个企业范围的超大规模存储库，适用于大数据分析工作负荷。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="d6ddc-107">使用 Azure Data Lake 可以在单个位置捕获任何大小、类型和引入速度的数据进行操作和探索分析。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="d6ddc-108">有关详细信息，请参阅 [Azure Data Lake Store 概述](/azure/data-lake-store/data-lake-store-overview)。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="client-library"></a><span data-ttu-id="d6ddc-109">客户端库</span><span class="sxs-lookup"><span data-stu-id="d6ddc-109">Client library</span></span>

<span data-ttu-id="d6ddc-110">使用客户端库可在 Data Lake Store 上执行文件系统操作，如在 Data Lake Store 帐户中创建文件夹，上传文件，以及下载文件。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-110">Use the client library to perform filesystem operations on Data Lake Store, such as creating folders in a Data Lake Store account, uploading files, and downloading files.</span></span>  <span data-ttu-id="d6ddc-111">有关将 Data Lake Store 与 .NET 一起使用的完整教程，请参阅[使用 .NET SDK 在 Azure Data Lake Store 上执行的文件系统操作](/azure/data-lake-store/data-lake-store-data-operations-net-sdk)。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-111">For a full tutorial on using Data Lake Store with .NET, see [Filesystem operations on Azure Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).</span></span>

<span data-ttu-id="d6ddc-112">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d6ddc-113">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="d6ddc-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a><span data-ttu-id="d6ddc-114">身份验证</span><span class="sxs-lookup"><span data-stu-id="d6ddc-114">Authentication</span></span>

* <span data-ttu-id="d6ddc-115">有关应用程序的最终用户身份验证，请参阅[使用 .NET SDK 通过 Data Lake Store 进行最终用户身份验证](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk)。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-115">For end-user authentication for your application, see [End-user authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk).</span></span>
* <span data-ttu-id="d6ddc-116">有关应用程序的服务到服务身份验证，请参阅[使用 .NET SDK 通过 Data Lake Store 进行服务到服务身份验证](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk)。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-116">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk).</span></span>

### <a name="code-example"></a><span data-ttu-id="d6ddc-117">代码示例</span><span class="sxs-lookup"><span data-stu-id="d6ddc-117">Code Example</span></span>

<span data-ttu-id="d6ddc-118">以下代码片段创建了 Data Lake Store filesystem 客户端对象，用于向服务发出请求。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-118">The following snippet creates the Data Lake Store filesystem client object, which is used to issue requests to the service.</span></span>

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6ddc-119">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="d6ddc-119">Explore the client APIs</span></span>](/dotnet/api/overview/azure/datalakestore/client)


## <a name="management-library"></a><span data-ttu-id="d6ddc-120">管理库</span><span class="sxs-lookup"><span data-stu-id="d6ddc-120">Management library</span></span>

<span data-ttu-id="d6ddc-121">使用管理库可连接和管理大数据存储库。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-121">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="d6ddc-122">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-122">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d6ddc-123">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="d6ddc-123">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6ddc-124">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="d6ddc-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a><span data-ttu-id="d6ddc-125">示例</span><span class="sxs-lookup"><span data-stu-id="d6ddc-125">Samples</span></span>

* [<span data-ttu-id="d6ddc-126">Azure Data Lake .NET 客户端示例</span><span class="sxs-lookup"><span data-stu-id="d6ddc-126">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="d6ddc-127">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="d6ddc-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
