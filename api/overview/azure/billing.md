---
title: 用于 .NET 的 Azure 计费库
description: 用于 .NET 的 Azure 计费库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: billing
ms.openlocfilehash: 196b9b4ed5f1f5f6794d86a43d26827355800d7b
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348079"
---
# <a name="azure-billing-libraries-for-net"></a>用于 .NET 的 Azure 计费库

## <a name="overview"></a>概述

使用 Azure 计费 API（预览）可以编程方式访问 Azure 计费信息和发票。

## <a name="management-library"></a>管理库

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a>代码示例

连接到 Azure 并获取发票列表。

```csharp
/* Include these directives
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Billing;
using Microsoft.Azure.Management.Billing.Models;
*/

// Log into Azure
var serviceCreds = ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var billingClient = new BillingClient(serviceCreds);
billingClient.SubscriptionId = subscriptionId;

// Get list of invoices
billingClient.Invoices.List();
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a>示例

* [使用情况 API](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [RateCard API](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [多租户 Web 应用程序](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
