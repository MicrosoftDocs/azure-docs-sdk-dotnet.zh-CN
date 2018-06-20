---
title: 用于 .NET 的 Azure 计费库
description: 用于 .NET 的 Azure 计费库参考
keywords: Azure, .NET, SDK, API, 计费
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8df15d55a80991f29b694f4af06a20514bf20b32
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566078"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="3ff4a-104">用于 .NET 的 Azure 计费库</span><span class="sxs-lookup"><span data-stu-id="3ff4a-104">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3ff4a-105">概述</span><span class="sxs-lookup"><span data-stu-id="3ff4a-105">Overview</span></span>

<span data-ttu-id="3ff4a-106">使用 Azure 计费 API（预览）可以编程方式访问 Azure 计费信息和发票。</span><span class="sxs-lookup"><span data-stu-id="3ff4a-106">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="3ff4a-107">管理库</span><span class="sxs-lookup"><span data-stu-id="3ff4a-107">Management library</span></span>

<span data-ttu-id="3ff4a-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing)。</span><span class="sxs-lookup"><span data-stu-id="3ff4a-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3ff4a-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="3ff4a-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="3ff4a-110">代码示例</span><span class="sxs-lookup"><span data-stu-id="3ff4a-110">Code Example</span></span>

<span data-ttu-id="3ff4a-111">连接到 Azure 并获取发票列表。</span><span class="sxs-lookup"><span data-stu-id="3ff4a-111">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="3ff4a-112">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="3ff4a-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="3ff4a-113">示例</span><span class="sxs-lookup"><span data-stu-id="3ff4a-113">Samples</span></span>

* [<span data-ttu-id="3ff4a-114">使用情况 API</span><span class="sxs-lookup"><span data-stu-id="3ff4a-114">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="3ff4a-115">RateCard API</span><span class="sxs-lookup"><span data-stu-id="3ff4a-115">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="3ff4a-116">多租户 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="3ff4a-116">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
