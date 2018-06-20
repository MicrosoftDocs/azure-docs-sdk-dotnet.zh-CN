---
title: 用于 .NET 的 Azure 虚拟网络库
description: 用于 .NET 的 Azure 虚拟网络库参考
keywords: Azure, .NET, SDK, API, 虚拟网络
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-network
ms.custom: devcenter, svc-overview
ms.openlocfilehash: b67415344ef9cbf8af598a1fd43b6b47023bb071
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487000"
---
# <a name="azure-virtual-network-libraries-for-net"></a>用于 .NET 的 Azure 虚拟网络库

## <a name="overview"></a>概述
使用 [Azure 虚拟网络](/azure/virtual-network/virtual-networks-overview)服务，可以通过虚拟网络 (VNet) 来安全地相互连接 Azure 资源。 VNet 是自己的网络在云中的表示形式。 还可将 VNet 相互连接到一起，使连接到任一 VNet 的资源可以相互通信。 

## <a name="management-library"></a>管理库

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a>代码示例
此示例演示如何创建虚拟网络。

```csharp
/* 
  Include these "using" directives...
  
  using Microsoft.Azure.Management.Network.Fluent;
  using Microsoft.Azure.Management.Network.Fluent.Models;
*/
using (NetworkManagementClient client = new NetworkManagementClient(credentials))
{
    // Define VNet
    VirtualNetworkInner vnet = new VirtualNetworkInner()
    {
        Location = "West US",
        AddressSpace = new AddressSpace()
        {
            AddressPrefixes = new List<string>() { "0.0.0.0/16" }
        },

        DhcpOptions = new DhcpOptions()
        {
            DnsServers = new List<string>() { "1.1.1.1", "1.1.2.4" }
        },

        Subnets = new List<Subnet>()
        {
            new Subnet()
            {
                Name = subnet1Name,
                AddressPrefix = "1.0.1.0/24",
            },
            new Subnet()
            {
                Name = subnet2Name,
               AddressPrefix = "1.0.2.0/24",
            }
        }
    };
    
    await client.VirtualNetworks.CreateOrUpdateAsync(resourceGroupName, vNetName, vnet);
}

```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a>示例
- [管理包含子网的虚拟网络](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

详细了解可在应用中使用的 [.NET 示例代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

