---
title: 用于 .NET 的 Azure 流分析库
description: 用于 .NET 的 Azure 流分析库参考
keywords: Azure, .NET, SDK, API, 流分析
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: stream-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4fc8c5700122a82a5e31df870787a67dad277542
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065927"
---
# <a name="azure-stream-analytics-libraries-for-net"></a>用于 .NET 的 Azure 流分析库

## <a name="overview"></a>概述

[Azure 流分析](/azure/stream-analytics/stream-analytics-introduction)是完全托管的事件处理引擎，可以用来设置针对流式处理数据的实时分析计算。 数据可能来自设备、传感器、网站、社交媒体源、应用程序、基础结构系统等。 

若要详细了解 Azure 流分析，请参阅 [Azure 流分析实时欺诈检测入门](/azure/stream-analytics/stream-analytics-real-time-fraud-detection)。


## <a name="management-library"></a>管理库

使用 Azure 流分析管理库可创建、启动和停止 Azure 流分析作业。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a>代码示例

此示例实例化流分析客户端并创建流式处理作业。

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
> [了解管理 API](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a>示例

- [管理 .NET SDK：使用用于 .NET 的 Azure 流分析 API 设置和运行分析作业](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

查看 Azure 流分析示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
