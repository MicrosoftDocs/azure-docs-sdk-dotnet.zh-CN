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
ms.openlocfilehash: 2b1c51575872b12a94eb44c7c082996bb879bcc9
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="d277f-104">用于 .NET 的 Azure Data Lake Store 库</span><span class="sxs-lookup"><span data-stu-id="d277f-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d277f-105">概述</span><span class="sxs-lookup"><span data-stu-id="d277f-105">Overview</span></span>

<span data-ttu-id="d277f-106">Azure Data Lake Store 是一个企业范围的超大规模存储库，适用于大数据分析工作负荷。</span><span class="sxs-lookup"><span data-stu-id="d277f-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="d277f-107">使用 Azure Data Lake 可以在单个位置捕获任何大小、类型和引入速度的数据进行操作和探索分析。</span><span class="sxs-lookup"><span data-stu-id="d277f-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="d277f-108">有关详细信息，请参阅 [Azure Data Lake Store 概述](/azure/data-lake-store/data-lake-store-overview)。</span><span class="sxs-lookup"><span data-stu-id="d277f-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="d277f-109">管理库</span><span class="sxs-lookup"><span data-stu-id="d277f-109">Management library</span></span>

<span data-ttu-id="d277f-110">使用管理库可连接和管理大数据存储库。</span><span class="sxs-lookup"><span data-stu-id="d277f-110">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="d277f-111">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)。</span><span class="sxs-lookup"><span data-stu-id="d277f-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d277f-112">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="d277f-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

### <a name="code-example"></a><span data-ttu-id="d277f-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="d277f-113">Code Example</span></span>

<span data-ttu-id="d277f-114">此示例对分析帐户和存储进行身份验证，并创建用于管理的客户端。</span><span class="sxs-lookup"><span data-stu-id="d277f-114">This example authenticates to an analytics account and store and creates the clients necessary for management.</span></span>

```csharp
/*
using AdlClient
using AdlClient.Models 
*/

// Setup authentication 
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
StoreAccountRef adls_account = new StoreAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
StoreClient adls = new StoreClient(auth, adls_account);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d277f-115">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="d277f-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="d277f-116">示例</span><span class="sxs-lookup"><span data-stu-id="d277f-116">Samples</span></span>

* [<span data-ttu-id="d277f-117">Azure Data Lake .NET 客户端示例</span><span class="sxs-lookup"><span data-stu-id="d277f-117">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="d277f-118">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="d277f-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
