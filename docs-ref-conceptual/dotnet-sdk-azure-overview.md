---
title: Azure .NET API
description: 用于 .NET 的 Azure API 概述
ms.date: 10/19/2017
ms.openlocfilehash: 04997caa99ed60db6ad98cabbc72b36bfbf99f4d
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190130"
---
# <a name="azure-net-apis"></a><span data-ttu-id="f82e4-103">Azure .NET API</span><span class="sxs-lookup"><span data-stu-id="f82e4-103">Azure .NET APIs</span></span>

<span data-ttu-id="f82e4-104">借助 Azure .NET API 可以通过应用程序代码使用 Azure 服务和管理 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="f82e4-104">The Azure .NET APIs let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="f82e4-105">API 以 [NuGet 包](/dotnet/api/overview/azure/)的形式提供，可在 .NET 项目中使用。</span><span class="sxs-lookup"><span data-stu-id="f82e4-105">The APIs are available as [NuGet packages](/dotnet/api/overview/azure/) for use in your .NET projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="f82e4-106">管理 Azure 资源</span><span class="sxs-lookup"><span data-stu-id="f82e4-106">Manage Azure resources</span></span>

<span data-ttu-id="f82e4-107">使用用于 .NET 的 Azure 库可以通过 .NET 应用程序创建和管理 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="f82e4-107">The Azure libraries for .NET let you create and manage Azure resources from your .NET applications.</span></span>

<span data-ttu-id="f82e4-108">用于管理 Azure 资源的许多包提供一个 [Fluent](dotnet-sdk-azure-concepts.md) 界面用于完全根据规范配置资源。</span><span class="sxs-lookup"><span data-stu-id="f82e4-108">Many of the packages for managing Azure resources have a [fluent](dotnet-sdk-azure-concepts.md) interface to configure resources exactly to your specifications.</span></span> <span data-ttu-id="f82e4-109">例如，若要创建 Windows VM，可编写以下代码：</span><span class="sxs-lookup"><span data-stu-id="f82e4-109">For example, to create a Windows VM you would write the following code:</span></span>

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

<span data-ttu-id="f82e4-110">请查看 [.NET 服务列表](/dotnet/api/overview/azure/)，立即在项目中开始使用这些库。</span><span class="sxs-lookup"><span data-stu-id="f82e4-110">Review the [.NET service list](/dotnet/api/overview/azure/) to start using the libraries immediately with your projects.</span></span> <span data-ttu-id="f82e4-111">然后阅读[入门文章](dotnet-sdk-azure-get-started.md)针对 Azure 订阅设置身份验证并运行示例代码。</span><span class="sxs-lookup"><span data-stu-id="f82e4-111">Then read the [get started article](dotnet-sdk-azure-get-started.md) to set up authentication and run sample code against your own Azure subscription.</span></span>  <span data-ttu-id="f82e4-112">[概念文章](dotnet-sdk-azure-concepts.md)深入介绍了 SDK 使用的约定，以及如何利用这些约定来简化应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="f82e4-112">The [concepts article](dotnet-sdk-azure-concepts.md) goes into the conventions the SDK uses and how to leverage them to simplify your application code.</span></span> <span data-ttu-id="f82e4-113">[发行说明](dotnet-sdk-azure-release-notes.md)中介绍了新增功能、重大更改以及有关迁移的说明。</span><span class="sxs-lookup"><span data-stu-id="f82e4-113">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

## <a name="consume-azure-services"></a><span data-ttu-id="f82e4-114">使用 Azure 服务</span><span class="sxs-lookup"><span data-stu-id="f82e4-114">Consume Azure services</span></span>

<span data-ttu-id="f82e4-115">除了使用 .NET API 在 Azure 中创建和以编程方式管理资源以外，还可以使用 .NET API 将应用程序连接到这些资源，并在运行时使用这些资源。</span><span class="sxs-lookup"><span data-stu-id="f82e4-115">In addition to using .NET APIs to create and programmatically manage resources within Azure, you can also then use .NET APIs to connect your applications to these resources and use them at runtime.</span></span>  <span data-ttu-id="f82e4-116">例如，可以连接到 SQL 数据库，或者在 Azure 存储中存储数据。</span><span class="sxs-lookup"><span data-stu-id="f82e4-116">For example, you might connect to a SQL Database or store data within Azure Storage.</span></span>  <span data-ttu-id="f82e4-117">可以通过浏览[服务 API 的完整列表](/dotnet/api/overview/azure/)，确定要对特定的 Azure 服务使用哪个 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="f82e4-117">You can identify which NuGet package to use for a particular Azure service by browsing our [full list of service APIs](/dotnet/api/overview/azure/).</span></span>  

## <a name="samples"></a><span data-ttu-id="f82e4-118">示例</span><span class="sxs-lookup"><span data-stu-id="f82e4-118">Samples</span></span>

<span data-ttu-id="f82e4-119">以下示例涵盖可以使用用于 .NET 的 Azure 库完成的常见自动化任务：</span><span class="sxs-lookup"><span data-stu-id="f82e4-119">The following samples cover common automation tasks with the Azure libraries for .NET:</span></span>

- [<span data-ttu-id="f82e4-120">虚拟机</span><span class="sxs-lookup"><span data-stu-id="f82e4-120">Virtual machines</span></span>](dotnet-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="f82e4-121">Web 应用</span><span class="sxs-lookup"><span data-stu-id="f82e4-121">Web apps</span></span>](dotnet-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="f82e4-122">SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="f82e4-122">SQL Database</span></span>](dotnet-sdk-azure-sql-database-samples.md)

<span data-ttu-id="f82e4-123">我们针对服务和管理库中的所有包提供了统一的[参考](/dotnet/api/overview/azure/?view=azure-dotnet)文档。</span><span class="sxs-lookup"><span data-stu-id="f82e4-123">A unified [reference](/dotnet/api/overview/azure/?view=azure-dotnet) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="f82e4-124">[发行说明](dotnet-sdk-azure-release-notes.md)中介绍了新增功能、重大更改以及有关迁移的说明。</span><span class="sxs-lookup"><span data-stu-id="f82e4-124">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

[!include[Contribute and community](includes/contribute.md)]