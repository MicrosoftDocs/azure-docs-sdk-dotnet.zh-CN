---
title: "用于 .NET 的 Azure 虚拟网络库"
description: "用于 .NET 的 Azure 虚拟网络库参考"
keywords: "Azure, .NET, SDK, API, 虚拟网络"
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
---
# <a name="azure-virtual-network-libraries-for-net"></a><span data-ttu-id="838e8-104">用于 .NET 的 Azure 虚拟网络库</span><span class="sxs-lookup"><span data-stu-id="838e8-104">Azure Virtual Network libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="838e8-105">概述</span><span class="sxs-lookup"><span data-stu-id="838e8-105">Overview</span></span>
<span data-ttu-id="838e8-106">使用 [Azure 虚拟网络](/azure/virtual-network/virtual-networks-overview)服务，可以通过虚拟网络 (VNet) 来安全地相互连接 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="838e8-106">The [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) service enables you to securely connect Azure resources to each other with virtual networks (VNets).</span></span> <span data-ttu-id="838e8-107">VNet 是自己的网络在云中的表示形式。</span><span class="sxs-lookup"><span data-stu-id="838e8-107">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="838e8-108">还可将 VNet 相互连接到一起，使连接到任一 VNet 的资源可以相互通信。</span><span class="sxs-lookup"><span data-stu-id="838e8-108">You can also connect VNets to each other, enabling resources connected to either VNet to communicate with each other.</span></span> 

## <a name="management-library"></a><span data-ttu-id="838e8-109">管理库</span><span class="sxs-lookup"><span data-stu-id="838e8-109">Management library</span></span>

<span data-ttu-id="838e8-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="838e8-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="838e8-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="838e8-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="838e8-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="838e8-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a><span data-ttu-id="838e8-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="838e8-113">Code Example</span></span>
<span data-ttu-id="838e8-114">此示例演示如何创建虚拟网络。</span><span class="sxs-lookup"><span data-stu-id="838e8-114">This example shows how you can create a virtual network.</span></span>

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
> [<span data-ttu-id="838e8-115">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="838e8-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a><span data-ttu-id="838e8-116">示例</span><span class="sxs-lookup"><span data-stu-id="838e8-116">Samples</span></span>
- [<span data-ttu-id="838e8-117">管理包含子网的虚拟网络</span><span class="sxs-lookup"><span data-stu-id="838e8-117">Managing Virtual Networks with subnets</span></span>](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

<span data-ttu-id="838e8-118">详细了解可在应用中使用的 [.NET 示例代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="838e8-118">Explore more [.NET sample code](https://azure.microsoft.com/resources/samples/?platform=dotnet) that you can use in your apps.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

