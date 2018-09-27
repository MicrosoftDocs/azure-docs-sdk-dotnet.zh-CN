---
title: 用于 .NET 的 Azure 计算库
description: 用于 .NET 的 Azure 计算库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: virtual-machines
ms.openlocfilehash: ee481e0f2448a874629bec36a719e7682407d320
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190690"
---
# <a name="azure-virtual-machine-libraries-for-net"></a><span data-ttu-id="7ddda-103">用于 .NET 的 Azure 虚拟机库</span><span class="sxs-lookup"><span data-stu-id="7ddda-103">Azure virtual machine libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7ddda-104">概述</span><span class="sxs-lookup"><span data-stu-id="7ddda-104">Overview</span></span>

<span data-ttu-id="7ddda-105">运行 Linux 或 Windows 的按需可缩放计算资源。</span><span class="sxs-lookup"><span data-stu-id="7ddda-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="7ddda-106">若要开始使用 Azure 虚拟机，请参阅[使用 Azure 门户创建 Linux 虚拟机](https://review.docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal)。</span><span class="sxs-lookup"><span data-stu-id="7ddda-106">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](https://review.docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="7ddda-107">管理 API</span><span class="sxs-lookup"><span data-stu-id="7ddda-107">Management APIs</span></span>

<span data-ttu-id="7ddda-108">使用管理 API 通过代码在 Azure 中创建、配置和横向扩展 Windows 与 Linux 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="7ddda-108">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="7ddda-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="7ddda-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7ddda-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="7ddda-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="7ddda-111">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="7ddda-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a><span data-ttu-id="7ddda-112">代码示例</span><span class="sxs-lookup"><span data-stu-id="7ddda-112">Code Example</span></span>

<span data-ttu-id="7ddda-113">创建 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="7ddda-113">Create a Windows VM.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IVirtualMachine windowsVM = azure.VirtualMachines.Define("MyVirtualMachine")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress("MyIPAddressLabel")
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername("UserName")
    .WithAdminPassword("Password")
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ddda-114">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="7ddda-114">Explore the management APIs</span></span>](https://docs.microsoft.com/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a><span data-ttu-id="7ddda-115">示例</span><span class="sxs-lookup"><span data-stu-id="7ddda-115">Samples</span></span>

* [<span data-ttu-id="7ddda-116">创建和管理虚拟机</span><span class="sxs-lookup"><span data-stu-id="7ddda-116">Create and manage virtual machines</span></span>](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [<span data-ttu-id="7ddda-117">在 .NET 中使用模板部署启用 SSH 的 VM</span><span class="sxs-lookup"><span data-stu-id="7ddda-117">Deploy an SSH-enabled VM with a Template with .NET</span></span>](https://azure.microsoft.com/resources/samples/resource-manager-dotnet-template-deployment/)

<span data-ttu-id="7ddda-118">查看虚拟机示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=VM)。</span><span class="sxs-lookup"><span data-stu-id="7ddda-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=VM) of virtual machine samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
