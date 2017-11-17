---
title: "用于 .NET 的 Azure Application Insights 库"
description: "用于 .NET 的 Azure Application Insights 库参考"
keywords: Azure, .NET, SDK, API, Application AppInsights
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: application-insights
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 081143eafaeea2954703c337609a67fd5a7941c6
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="e6767-104">用于 .NET 的 Azure Application Insights 库</span><span class="sxs-lookup"><span data-stu-id="e6767-104">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e6767-105">概述</span><span class="sxs-lookup"><span data-stu-id="e6767-105">Overview</span></span>

<span data-ttu-id="e6767-106">Application Insights 是面向 Web 开发人员的可扩展监视和诊断服务，具有强大的即席分析功能。</span><span class="sxs-lookup"><span data-stu-id="e6767-106">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="e6767-107">可以使用 ApplicationInsights 命名空间中的类来配置遥测数据的收集，并发送想要监视的应用程序所发出的任何自定义遥测数据。</span><span class="sxs-lookup"><span data-stu-id="e6767-107">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="e6767-108">客户端库</span><span class="sxs-lookup"><span data-stu-id="e6767-108">Client library</span></span>

<span data-ttu-id="e6767-109">使用用于 .NET 的 Application Insights 客户端 SDK 可将事件、聚合数据、异常、依赖项和指标记录到 Azure 供将来分析。</span><span class="sxs-lookup"><span data-stu-id="e6767-109">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="e6767-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.ApplicationInsights )。</span><span class="sxs-lookup"><span data-stu-id="e6767-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e6767-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="e6767-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="e6767-112">示例</span><span class="sxs-lookup"><span data-stu-id="e6767-112">Example</span></span>

<span data-ttu-id="e6767-113">此示例在 Application Insights 中跟踪自定义事件。</span><span class="sxs-lookup"><span data-stu-id="e6767-113">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e6767-114">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="e6767-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="e6767-115">示例</span><span class="sxs-lookup"><span data-stu-id="e6767-115">Samples</span></span>

- [<span data-ttu-id="e6767-116">将 Application Insights Analytics 与 OpenSchema 配合使用</span><span class="sxs-lookup"><span data-stu-id="e6767-116">Application Insights Analytics with OpenSchema</span></span>](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

<span data-ttu-id="e6767-117">查看 Azure Application Insights 示例的[完整列表](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="e6767-117">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
