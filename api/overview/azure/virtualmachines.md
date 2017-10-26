---
title: "用于 .NET 的 Azure 计算库"
description: "用于 .NET 的 Azure 计算库参考"
keywords: "Azure, .NET, SDK, API, VM, 虚拟机, 计算"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-machines
ms.custom: devcenter, svc-overview
ms.openlocfilehash: b8caa9a46b858c2ea1f14e83880bd69d83f6a5e9
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
---
# <a name="azure-virtual-machine-libraries-for-net"></a>用于 .NET 的 Azure 虚拟机库

## <a name="overview"></a>概述

运行 Linux 或 Windows 的按需可缩放计算资源。

若要开始使用 Azure 虚拟机，请参阅[使用 Azure 门户创建 Linux 虚拟机](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)。

## <a name="management-apis"></a>管理 API

使用管理 API 通过代码在 Azure 中创建、配置和横向扩展 Windows 与 Linux 虚拟机。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a>代码示例

创建 Windows VM。

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
> [了解管理 API](https://review.docs.microsoft.com/en-us/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a>示例

* [创建和管理虚拟机](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [在 .NET 中使用模板部署启用 SSH 的 VM](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/)

查看虚拟机示例的[完整列表](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
