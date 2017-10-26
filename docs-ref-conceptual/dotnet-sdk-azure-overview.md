---
title: Azure .NET API
description: "用于 .NET 的 Azure API 概述"
keywords: "Azure, .NET, SDK, API, NuGet, 库, 包"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: cd0f8d6e0572fc9211af637e60d1a4f19e1ee1e8
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
---
# <a name="azure-net-apis"></a>Azure .NET API

借助 Azure .NET API 可以通过应用程序代码使用 Azure 服务和管理 Azure 资源。 API 以 [NuGet 包](/dotnet/api/overview/azure/)的形式提供，可在 .NET 项目中使用。 

## <a name="manage-azure-resources"></a>管理 Azure 资源

使用用于 .NET 的 Azure 库可以通过 .NET 应用程序创建和管理 Azure 资源。

用于管理 Azure 资源的许多包提供一个 [Fluent](dotnet-sdk-azure-concepts.md) 界面用于完全根据规范配置资源。 例如，若要创建 Windows VM，可编写以下代码：

```csharp
var windowsVM = azure.VirtualMachines.Define(windowsVmName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername(username)
    .WithAdminPassword(password)
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
 ```

请查看 [.NET 服务列表](/dotnet/api/overview/azure/)，立即在项目中开始使用这些库。 然后阅读[入门文章](dotnet-sdk-azure-get-started.md)针对 Azure 订阅设置身份验证并运行示例代码。  [概念文章](dotnet-sdk-azure-concepts.md)深入介绍了 SDK 使用的约定，以及如何利用这些约定来简化应用程序代码。 [发行说明](dotnet-sdk-azure-release-notes.md)中介绍了新增功能、重大更改以及有关迁移的说明。

## <a name="consume-azure-services"></a>使用 Azure 服务

除了使用 .NET API 在 Azure 中创建和以编程方式管理资源以外，还可以使用 .NET API 将应用程序连接到这些资源，并在运行时使用这些资源。  例如，可以连接到 SQL 数据库，或者在 Azure 存储中存储数据。  可以通过浏览[服务 API 的完整列表](/dotnet/api/overview/azure/)，确定要对特定的 Azure 服务使用哪个 NuGet 包。  

## <a name="samples"></a>示例

以下示例涵盖可以使用用于 .NET 的 Azure 库完成的常见自动化任务：

- [虚拟机](dotnet-sdk-azure-virtual-machine-samples.md)
- [Web 应用](dotnet-sdk-azure-web-apps-samples.md)
- [SQL 数据库](dotnet-sdk-azure-sql-database-samples.md)

我们针对服务和管理库中的所有包提供了统一的[参考](/dotnet/api/overview/azure/?view=azure-dotnet)文档。 [发行说明](dotnet-sdk-azure-release-notes.md)中介绍了新增功能、重大更改以及有关迁移的说明。

[!include[Contribute and community](includes/contribute.md)]