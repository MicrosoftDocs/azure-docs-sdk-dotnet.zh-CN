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
# <a name="azure-application-insights-libraries-for-net"></a>用于 .NET 的 Azure Application Insights 库

## <a name="overview"></a>概述

Application Insights 是面向 Web 开发人员的可扩展监视和诊断服务，具有强大的即席分析功能。 可以使用 ApplicationInsights 命名空间中的类来配置遥测数据的收集，并发送想要监视的应用程序所发出的任何自定义遥测数据。

## <a name="client-library"></a>客户端库

使用用于 .NET 的 Application Insights 客户端 SDK 可将事件、聚合数据、异常、依赖项和指标记录到 Azure 供将来分析。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.ApplicationInsights )。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a>示例

此示例在 Application Insights 中跟踪自定义事件。

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a>示例

- [将 Application Insights Analytics 与 OpenSchema 配合使用](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

查看 Azure Application Insights 示例的[完整列表](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
