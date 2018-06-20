---
title: 用于 .NET 的 Azure 流分析库
description: 用于 .NET 的 Azure 流分析库参考
keywords: Azure, .NET, SDK, API, 流分析
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: stream-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2a5e8b8481548d6cfebc5104eb459f8772f51462
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487130"
---
# <a name="azure-stream-analytics-libraries-for-net"></a><span data-ttu-id="eb2b5-104">用于 .NET 的 Azure 流分析库</span><span class="sxs-lookup"><span data-stu-id="eb2b5-104">Azure Stream Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="eb2b5-105">概述</span><span class="sxs-lookup"><span data-stu-id="eb2b5-105">Overview</span></span>

<span data-ttu-id="eb2b5-106">[Azure 流分析](/azure/stream-analytics/stream-analytics-introduction)是完全托管的事件处理引擎，可以用来设置针对流式处理数据的实时分析计算。</span><span class="sxs-lookup"><span data-stu-id="eb2b5-106">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) is a fully managed event-processing engine that lets you set up real-time analytic computations on streaming data.</span></span> <span data-ttu-id="eb2b5-107">数据可能来自设备、传感器、网站、社交媒体源、应用程序、基础结构系统等。</span><span class="sxs-lookup"><span data-stu-id="eb2b5-107">The data can come from devices, sensors, web sites, social media feeds, applications, infrastructure systems, and more.</span></span> 

<span data-ttu-id="eb2b5-108">若要详细了解 Azure 流分析，请参阅 [Azure 流分析实时欺诈检测入门](/azure/stream-analytics/stream-analytics-real-time-fraud-detection)。</span><span class="sxs-lookup"><span data-stu-id="eb2b5-108">To learn more about Azure Stream Analytics, see [Get started with Azure Stream Analytics Real-time fraud detection](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span></span>


## <a name="management-library"></a><span data-ttu-id="eb2b5-109">管理库</span><span class="sxs-lookup"><span data-stu-id="eb2b5-109">Management library</span></span>

<span data-ttu-id="eb2b5-110">使用 Azure 流分析管理库可创建、启动和停止 Azure 流分析作业。</span><span class="sxs-lookup"><span data-stu-id="eb2b5-110">Use the Azure Stream Analytics management library to create, start, and stop Azure Stream Analytics jobs.</span></span>

<span data-ttu-id="eb2b5-111">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="eb2b5-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="eb2b5-112">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="eb2b5-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a><span data-ttu-id="eb2b5-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="eb2b5-113">Code Example</span></span>

<span data-ttu-id="eb2b5-114">此示例实例化流分析客户端并创建流式处理作业。</span><span class="sxs-lookup"><span data-stu-id="eb2b5-114">This example instantiates a Stream Analytics client and creates a streaming job.</span></span>

```csharp
/* Include these 'using' directives:
using Microsoft.Azure.Management.StreamAnalytics;
*/
SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

// Get credentials
ServiceClientCredentials credentials = GetCredentials().Result;

// Create Stream Analytics management client
StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
{
    SubscriptionId = subscriptionId
};

// Create a streaming job
StreamingJob streamingJob = new StreamingJob()
{
    Tags = new Dictionary<string, string>()
    {
        { "Origin", ".NET SDK" },
        { "ReasonCreated", "Getting started tutorial" }
    },
    Location = "West US",
    EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
    EventsOutOfOrderMaxDelayInSeconds = 5,
    EventsLateArrivalMaxDelayInSeconds = 16,
    OutputErrorPolicy = OutputErrorPolicy.Drop,
    DataLocale = "en-US",
    CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
    Sku = new Sku()
    {
        Name = SkuName.Standard
    }
};
StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb2b5-115">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="eb2b5-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a><span data-ttu-id="eb2b5-116">示例</span><span class="sxs-lookup"><span data-stu-id="eb2b5-116">Samples</span></span>

- [<span data-ttu-id="eb2b5-117">管理 .NET SDK：使用用于 .NET 的 Azure 流分析 API 设置和运行分析作业</span><span class="sxs-lookup"><span data-stu-id="eb2b5-117">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

<span data-ttu-id="eb2b5-118">查看 Azure 流分析示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics)。</span><span class="sxs-lookup"><span data-stu-id="eb2b5-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
