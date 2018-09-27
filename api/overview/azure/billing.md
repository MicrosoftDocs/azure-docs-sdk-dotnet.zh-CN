---
title: 用于 .NET 的 Azure 计费库
description: 用于 .NET 的 Azure 计费库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 88b90c71d29eacf61e4da2099f8a054d74df4a83
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190250"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="d8a8c-103">用于 .NET 的 Azure 计费库</span><span class="sxs-lookup"><span data-stu-id="d8a8c-103">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d8a8c-104">概述</span><span class="sxs-lookup"><span data-stu-id="d8a8c-104">Overview</span></span>

<span data-ttu-id="d8a8c-105">使用 Azure 计费 API（预览）可以编程方式访问 Azure 计费信息和发票。</span><span class="sxs-lookup"><span data-stu-id="d8a8c-105">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="d8a8c-106">管理库</span><span class="sxs-lookup"><span data-stu-id="d8a8c-106">Management library</span></span>

<span data-ttu-id="d8a8c-107">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing)。</span><span class="sxs-lookup"><span data-stu-id="d8a8c-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d8a8c-108">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="d8a8c-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="d8a8c-109">代码示例</span><span class="sxs-lookup"><span data-stu-id="d8a8c-109">Code Example</span></span>

<span data-ttu-id="d8a8c-110">连接到 Azure 并获取发票列表。</span><span class="sxs-lookup"><span data-stu-id="d8a8c-110">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="d8a8c-111">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="d8a8c-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="d8a8c-112">示例</span><span class="sxs-lookup"><span data-stu-id="d8a8c-112">Samples</span></span>

* [<span data-ttu-id="d8a8c-113">使用情况 API</span><span class="sxs-lookup"><span data-stu-id="d8a8c-113">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="d8a8c-114">RateCard API</span><span class="sxs-lookup"><span data-stu-id="d8a8c-114">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="d8a8c-115">多租户 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="d8a8c-115">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
