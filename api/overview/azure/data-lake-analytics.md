---
title: 用于 .NET 的 Azure Data Lake Analytics 库
description: 用于 .NET 的 Azure Data Lake Analytics 库参考
keywords: Azure, .NET, SDK, API, Data Lake Analytics
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: data-lake-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: a4340844906d7ccf2612ce17dae13e1fce257da0
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065677"
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a>用于 .NET 的 Azure Data Lake Analytics 库

## <a name="overview"></a>概述

Azure Data Lake Analytics 是一项按需分析作业服务，用于简化大数据分析。

有关详细信息，请参阅 [Microsoft Azure Data Lake Analytics 概述](/azure/data-lake-analytics/data-lake-analytics-overview)。

## <a name="management-library"></a>管理库

使用管理库可连接到服务和管理分析作业。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a>代码示例

此示例创建用于连接和管理分析帐户的客户端。

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
> [了解管理 API](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>示例
* [Azure Data Lake .NET 客户端示例](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
