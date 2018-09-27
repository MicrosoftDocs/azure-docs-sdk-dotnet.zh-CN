---
title: 用于 .NET 的 Azure Application Insights 库
description: 用于 .NET 的 Azure Application Insights 库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: application-insights
ms.openlocfilehash: 10b65f536c6461959b0be9b8f9bd3ec56a307bea
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190831"
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="773ef-103">用于 .NET 的 Azure Application Insights 库</span><span class="sxs-lookup"><span data-stu-id="773ef-103">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="773ef-104">概述</span><span class="sxs-lookup"><span data-stu-id="773ef-104">Overview</span></span>

<span data-ttu-id="773ef-105">Application Insights 是面向 Web 开发人员的可扩展监视和诊断服务，具有强大的即席分析功能。</span><span class="sxs-lookup"><span data-stu-id="773ef-105">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="773ef-106">可以使用 ApplicationInsights 命名空间中的类来配置遥测数据的收集，并发送想要监视的应用程序所发出的任何自定义遥测数据。</span><span class="sxs-lookup"><span data-stu-id="773ef-106">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="773ef-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="773ef-107">Client library</span></span>

<span data-ttu-id="773ef-108">使用用于 .NET 的 Application Insights 客户端 SDK 可将事件、聚合数据、异常、依赖项和指标记录到 Azure 供将来分析。</span><span class="sxs-lookup"><span data-stu-id="773ef-108">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="773ef-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.ApplicationInsights )。</span><span class="sxs-lookup"><span data-stu-id="773ef-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="773ef-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="773ef-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="773ef-111">示例</span><span class="sxs-lookup"><span data-stu-id="773ef-111">Example</span></span>

<span data-ttu-id="773ef-112">此示例在 Application Insights 中跟踪自定义事件。</span><span class="sxs-lookup"><span data-stu-id="773ef-112">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="773ef-113">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="773ef-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="773ef-114">示例</span><span class="sxs-lookup"><span data-stu-id="773ef-114">Samples</span></span>

- [<span data-ttu-id="773ef-115">将 Application Insights Analytics 与 OpenSchema 配合使用</span><span class="sxs-lookup"><span data-stu-id="773ef-115">Application Insights Analytics with OpenSchema</span></span>](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

<span data-ttu-id="773ef-116">查看 Azure Application Insights 示例的[完整列表](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="773ef-116">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
