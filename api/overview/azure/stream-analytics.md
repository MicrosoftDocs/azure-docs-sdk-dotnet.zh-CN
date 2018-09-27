---
title: 用于 .NET 的 Azure 流分析库
description: 用于 .NET 的 Azure 流分析库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: stream-analytics
ms.openlocfilehash: c04a5c8a7b1d7e0f283d4fb81bd772de24f195eb
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190450"
---
# <a name="azure-stream-analytics-libraries-for-net"></a><span data-ttu-id="98721-103">用于 .NET 的 Azure 流分析库</span><span class="sxs-lookup"><span data-stu-id="98721-103">Azure Stream Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="98721-104">概述</span><span class="sxs-lookup"><span data-stu-id="98721-104">Overview</span></span>

<span data-ttu-id="98721-105">[Azure 流分析](/azure/stream-analytics/stream-analytics-introduction)是完全托管的事件处理引擎，可以用来设置针对流式处理数据的实时分析计算。</span><span class="sxs-lookup"><span data-stu-id="98721-105">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) is a fully managed event-processing engine that lets you set up real-time analytic computations on streaming data.</span></span> <span data-ttu-id="98721-106">数据可能来自设备、传感器、网站、社交媒体源、应用程序、基础结构系统等。</span><span class="sxs-lookup"><span data-stu-id="98721-106">The data can come from devices, sensors, web sites, social media feeds, applications, infrastructure systems, and more.</span></span> 

<span data-ttu-id="98721-107">若要详细了解 Azure 流分析，请参阅 [Azure 流分析实时欺诈检测入门](/azure/stream-analytics/stream-analytics-real-time-fraud-detection)。</span><span class="sxs-lookup"><span data-stu-id="98721-107">To learn more about Azure Stream Analytics, see [Get started with Azure Stream Analytics Real-time fraud detection](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span></span>


## <a name="management-library"></a><span data-ttu-id="98721-108">管理库</span><span class="sxs-lookup"><span data-stu-id="98721-108">Management library</span></span>

<span data-ttu-id="98721-109">使用 Azure 流分析管理库可创建、启动和停止 Azure 流分析作业。</span><span class="sxs-lookup"><span data-stu-id="98721-109">Use the Azure Stream Analytics management library to create, start, and stop Azure Stream Analytics jobs.</span></span>

<span data-ttu-id="98721-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="98721-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="98721-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="98721-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a><span data-ttu-id="98721-112">代码示例</span><span class="sxs-lookup"><span data-stu-id="98721-112">Code Example</span></span>

<span data-ttu-id="98721-113">此示例实例化流分析客户端并创建流式处理作业。</span><span class="sxs-lookup"><span data-stu-id="98721-113">This example instantiates a Stream Analytics client and creates a streaming job.</span></span>

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
> [<span data-ttu-id="98721-114">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="98721-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a><span data-ttu-id="98721-115">示例</span><span class="sxs-lookup"><span data-stu-id="98721-115">Samples</span></span>

- [<span data-ttu-id="98721-116">管理 .NET SDK：使用用于 .NET 的 Azure 流分析 API 设置和运行分析作业</span><span class="sxs-lookup"><span data-stu-id="98721-116">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

<span data-ttu-id="98721-117">查看 Azure 流分析示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics)。</span><span class="sxs-lookup"><span data-stu-id="98721-117">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
