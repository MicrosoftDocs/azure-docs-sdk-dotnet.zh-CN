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
# <a name="azure-dns-libraries-for-net"></a>用于 .NET 的 Azure DNS 库

使用用于 .NET 的 Microsoft Azure DNS 库可创建和修改 Azure 中托管的 DNS 区域与记录。 区域和记录以 Azure 资源的形式进行管理。 请阅读 [Azure DNS 概述](/azure/dns/dns-overview)了解详细信息。

## <a name="management-library"></a>管理库

使用管理库可创建和修改 Azure 中托管的 DNS 区域与记录。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a>示例

以下示例创建新的 DNS 区域。

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
> [了解管理 API](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a>示例

* [Azure DNS .NET SDK 示例项目](https://www.microsoft.com/download/details.aspx?id=47268)

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
