---
title: Azure .NET API
description: "用于 .NET 的 Azure API 概述"
keywords: "Azure, .NET, SDK, API, NuGet, 库, 包"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 27956b5c351314b2302109d81d015cc77effea15
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-net-apis"></a><span data-ttu-id="49931-104">Azure .NET API</span><span class="sxs-lookup"><span data-stu-id="49931-104">Azure .NET APIs</span></span>

<span data-ttu-id="49931-105">借助 Azure .NET API 可以通过应用程序代码使用 Azure 服务和管理 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="49931-105">The Azure .NET APIs let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="49931-106">API 以 [NuGet 包](/dotnet/api/overview/azure/)的形式提供，可在 .NET 项目中使用。</span><span class="sxs-lookup"><span data-stu-id="49931-106">The APIs are available as [NuGet packages](/dotnet/api/overview/azure/) for use in your .NET projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="49931-107">管理 Azure 资源</span><span class="sxs-lookup"><span data-stu-id="49931-107">Manage Azure resources</span></span>

<span data-ttu-id="49931-108">使用用于 .NET 的 Azure 库可以通过 .NET 应用程序创建和管理 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="49931-108">The Azure libraries for .NET let you create and manage Azure resources from your .NET applications.</span></span>

<span data-ttu-id="49931-109">用于管理 Azure 资源的许多包提供一个 [Fluent](dotnet-sdk-azure-concepts.md) 界面用于完全根据规范配置资源。</span><span class="sxs-lookup"><span data-stu-id="49931-109">Many of the packages for managing Azure resources have a [fluent](dotnet-sdk-azure-concepts.md) interface to configure resources exactly to your specifications.</span></span> <span data-ttu-id="49931-110">例如，若要创建 Windows VM，可编写以下代码：</span><span class="sxs-lookup"><span data-stu-id="49931-110">For example, to create a Windows VM you would write the following code:</span></span>

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

<span data-ttu-id="49931-111">请查看 [.NET 服务列表](/dotnet/api/overview/azure/)，立即在项目中开始使用这些库。</span><span class="sxs-lookup"><span data-stu-id="49931-111">Review the [.NET service list](/dotnet/api/overview/azure/) to start using the libraries immediately with your projects.</span></span> <span data-ttu-id="49931-112">然后阅读[入门文章](dotnet-sdk-azure-get-started.md)针对 Azure 订阅设置身份验证并运行示例代码。</span><span class="sxs-lookup"><span data-stu-id="49931-112">Then read the [get started article](dotnet-sdk-azure-get-started.md) to set up authentication and run sample code against your own Azure subscription.</span></span>  <span data-ttu-id="49931-113">[概念文章](dotnet-sdk-azure-concepts.md)深入介绍了 SDK 使用的约定，以及如何利用这些约定来简化应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="49931-113">The [concepts article](dotnet-sdk-azure-concepts.md) goes into the conventions the SDK uses and how to leverage them to simplify your application code.</span></span> <span data-ttu-id="49931-114">[发行说明](dotnet-sdk-azure-release-notes.md)中介绍了新增功能、重大更改以及有关迁移的说明。</span><span class="sxs-lookup"><span data-stu-id="49931-114">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

## <a name="consume-azure-services"></a><span data-ttu-id="49931-115">使用 Azure 服务</span><span class="sxs-lookup"><span data-stu-id="49931-115">Consume Azure services</span></span>

<span data-ttu-id="49931-116">除了使用 .NET API 在 Azure 中创建和以编程方式管理资源以外，还可以使用 .NET API 将应用程序连接到这些资源，并在运行时使用这些资源。</span><span class="sxs-lookup"><span data-stu-id="49931-116">In addition to using .NET APIs to create and programmatically manage resources within Azure, you can also then use .NET APIs to connect your applications to these resources and use them at runtime.</span></span>  <span data-ttu-id="49931-117">例如，可以连接到 SQL 数据库，或者在 Azure 存储中存储数据。</span><span class="sxs-lookup"><span data-stu-id="49931-117">For example, you might connect to a SQL Database or store data within Azure Storage.</span></span>  <span data-ttu-id="49931-118">可以通过浏览[服务 API 的完整列表](/dotnet/api/overview/azure/)，确定要对特定的 Azure 服务使用哪个 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="49931-118">You can identify which NuGet package to use for a particular Azure service by browsing our [full list of service APIs](/dotnet/api/overview/azure/).</span></span>  

## <a name="samples"></a><span data-ttu-id="49931-119">示例</span><span class="sxs-lookup"><span data-stu-id="49931-119">Samples</span></span>

<span data-ttu-id="49931-120">以下示例涵盖可以使用用于 .NET 的 Azure 库完成的常见自动化任务：</span><span class="sxs-lookup"><span data-stu-id="49931-120">The following samples cover common automation tasks with the Azure libraries for .NET:</span></span>

- [<span data-ttu-id="49931-121">虚拟机</span><span class="sxs-lookup"><span data-stu-id="49931-121">Virtual machines</span></span>](dotnet-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="49931-122">Web 应用</span><span class="sxs-lookup"><span data-stu-id="49931-122">Web apps</span></span>](dotnet-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="49931-123">SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="49931-123">SQL Database</span></span>](dotnet-sdk-azure-sql-database-samples.md)

<span data-ttu-id="49931-124">我们针对服务和管理库中的所有包提供了统一的[参考](/dotnet/api/overview/azure/?view=azure-dotnet)文档。</span><span class="sxs-lookup"><span data-stu-id="49931-124">A unified [reference](/dotnet/api/overview/azure/?view=azure-dotnet) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="49931-125">[发行说明](dotnet-sdk-azure-release-notes.md)中介绍了新增功能、重大更改以及有关迁移的说明。</span><span class="sxs-lookup"><span data-stu-id="49931-125">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

[!include[Contribute and community](includes/contribute.md)]