---
title: 用于 .NET 的 Azure Data Lake Analytics 库
description: 用于 .NET 的 Azure Data Lake Analytics 库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: data-lake-analytics
ms.openlocfilehash: 829f9245ae06c64c4ad9a175fd25c742533a284e
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189790"
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a><span data-ttu-id="e968f-103">用于 .NET 的 Azure Data Lake Analytics 库</span><span class="sxs-lookup"><span data-stu-id="e968f-103">Azure Data Lake Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e968f-104">概述</span><span class="sxs-lookup"><span data-stu-id="e968f-104">Overview</span></span>

<span data-ttu-id="e968f-105">Azure Data Lake Analytics 是一项按需分析作业服务，用于简化大数据分析。</span><span class="sxs-lookup"><span data-stu-id="e968f-105">Azure Data Lake Analytics is an on-demand analytics job service to simplify big data analytics.</span></span>

<span data-ttu-id="e968f-106">有关详细信息，请参阅 [Microsoft Azure Data Lake Analytics 概述](/azure/data-lake-analytics/data-lake-analytics-overview)。</span><span class="sxs-lookup"><span data-stu-id="e968f-106">To learn more, see [Overview of Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="e968f-107">管理库</span><span class="sxs-lookup"><span data-stu-id="e968f-107">Management library</span></span>

<span data-ttu-id="e968f-108">使用管理库可连接到服务和管理分析作业。</span><span class="sxs-lookup"><span data-stu-id="e968f-108">Use the management library to connect to the service and manage analytics jobs.</span></span>

<span data-ttu-id="e968f-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)。</span><span class="sxs-lookup"><span data-stu-id="e968f-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e968f-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="e968f-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a><span data-ttu-id="e968f-111">代码示例</span><span class="sxs-lookup"><span data-stu-id="e968f-111">Code Example</span></span>

<span data-ttu-id="e968f-112">此示例创建用于连接和管理分析帐户的客户端。</span><span class="sxs-lookup"><span data-stu-id="e968f-112">This example creates the clients to connect with and manage the analytics account.</span></span>

```csharp
/*
using AdlClient 
*/

// Setup authentication for this demo
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
AnalyticsAccountRef adla_account = new AnalyticsAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
AnalyticsClient adla = new AnalyticsClient(auth, adla_account);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e968f-113">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="e968f-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a><span data-ttu-id="e968f-114">示例</span><span class="sxs-lookup"><span data-stu-id="e968f-114">Samples</span></span>
* [<span data-ttu-id="e968f-115">Azure Data Lake .NET 客户端示例</span><span class="sxs-lookup"><span data-stu-id="e968f-115">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="e968f-116">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="e968f-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
