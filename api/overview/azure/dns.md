---
title: 用于 .NET 的 Azure DNS 库
description: 用于 .NET 的 Azure DNS 库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: dns
ms.openlocfilehash: b9ab6359aaa1e4e9b6e99e7a7b007928d18f3453
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190190"
---
# <a name="azure-dns-libraries-for-net"></a><span data-ttu-id="e61bb-103">用于 .NET 的 Azure DNS 库</span><span class="sxs-lookup"><span data-stu-id="e61bb-103">Azure DNS libraries for .NET</span></span>

<span data-ttu-id="e61bb-104">使用用于 .NET 的 Microsoft Azure DNS 库可创建和修改 Azure 中托管的 DNS 区域与记录。</span><span class="sxs-lookup"><span data-stu-id="e61bb-104">Use the Microsoft Azure DNS libraries for .NET to create and modify DNS zones and records hosted within Azure.</span></span> <span data-ttu-id="e61bb-105">区域和记录以 Azure 资源的形式进行管理。</span><span class="sxs-lookup"><span data-stu-id="e61bb-105">Zones and records are managed as Azure Resources.</span></span> <span data-ttu-id="e61bb-106">请阅读 [Azure DNS 概述](/azure/dns/dns-overview)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="e61bb-106">Learn more by reading the [Azure DNS overview](/azure/dns/dns-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="e61bb-107">管理库</span><span class="sxs-lookup"><span data-stu-id="e61bb-107">Management library</span></span>

<span data-ttu-id="e61bb-108">使用管理库可创建和修改 Azure 中托管的 DNS 区域与记录。</span><span class="sxs-lookup"><span data-stu-id="e61bb-108">Use the management library to create and modify DNS zones and records that are hosted in Azure.</span></span>

<span data-ttu-id="e61bb-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns)。</span><span class="sxs-lookup"><span data-stu-id="e61bb-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e61bb-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="e61bb-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a><span data-ttu-id="e61bb-111">示例</span><span class="sxs-lookup"><span data-stu-id="e61bb-111">Example</span></span>

<span data-ttu-id="e61bb-112">以下示例创建新的 DNS 区域。</span><span class="sxs-lookup"><span data-stu-id="e61bb-112">The following example creates a new DNS zone.</span></span>

```csharp
/*
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
*/
Microsoft.Rest.ServiceClientCredentials serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
DnsManagementClient dnsClient = new DnsManagementClient(serviceCreds);            
Zone dnsZoneParams = new Zone("global");
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");
Zone dnsZone =
    await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e61bb-113">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="e61bb-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="e61bb-114">示例</span><span class="sxs-lookup"><span data-stu-id="e61bb-114">Samples</span></span>

* [<span data-ttu-id="e61bb-115">Azure DNS .NET SDK 示例项目</span><span class="sxs-lookup"><span data-stu-id="e61bb-115">Azure DNS .NET SDK Sample Project</span></span>](https://www.microsoft.com/download/details.aspx?id=47268)

<span data-ttu-id="e61bb-116">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="e61bb-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
