---
title: 适用于 .NET 的 Azure Monitor 库
description: 适用于 .NET 的 Azure Monitor 库参考
keywords: Azure, .NET, SDK, API, Monitor
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/27/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8055b8861f6991e021ff1ea3bfa87cf96f554fa2
ms.sourcegitcommit: 64c9e16e42894e8db8ed088487e55c5e0edd6861
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2017
ms.locfileid: "23639635"
---
# <a name="azure-monitor-libraries-for-net"></a>适用于 .NET 的 Azure Monitor 库

## <a name="overview"></a>概述

借助 Azure Monitor 可以跟踪性能、保持安全性和确定趋势。

详细了解 [Azure Monitor](/azure/monitoring-and-diagnostics/)。   

## <a name="management-library"></a>管理库

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Monitor.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Monitor.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Monitor.Fluent
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/monitor/management)

## <a name="samples"></a>示例

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package