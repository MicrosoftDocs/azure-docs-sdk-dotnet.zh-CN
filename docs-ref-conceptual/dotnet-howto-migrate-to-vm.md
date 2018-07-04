---
title: 将 ASP.NET Web 应用程序迁移到 Azure 虚拟机
description: 了解如何将 ASP.NET Web 应用程序从本地迁移到 Azure 虚拟机。
keywords: Azure .NET, ASP.NET, VM, 虚拟机, 迁移
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-machines
ms.custom: devcenter
ms.openlocfilehash: 53e899ba3cd2ff265a2068e1b7eee5baa4520879
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065337"
---
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a><span data-ttu-id="685a6-104">将 ASP.NET Web 应用程序迁移到 Azure 虚拟机</span><span class="sxs-lookup"><span data-stu-id="685a6-104">Migrate an ASP.NET Web application to an Azure Virtual Machine</span></span>

<span data-ttu-id="685a6-105">本文档概述了解如何将 ASP.NET Web 应用程序从本地迁移到 Azure 虚拟机。</span><span class="sxs-lookup"><span data-stu-id="685a6-105">This document provides an overview of how to migrate an ASP.NET web application from on-premises to an Azure Virtual Machine.</span></span>

## <a name="quickstart"></a><span data-ttu-id="685a6-106">快速入门</span><span class="sxs-lookup"><span data-stu-id="685a6-106">Quickstart</span></span>

<span data-ttu-id="685a6-107">了解如何创建虚拟机并将应用发布到其中：[发布到 Azure VM](https://tutorials.visualstudio.com/aspnet-vm/intro)</span><span class="sxs-lookup"><span data-stu-id="685a6-107">Learn how to create a virtual machine and publish your app to it: [Publish to an Azure VM](https://tutorials.visualstudio.com/aspnet-vm/intro)</span></span>

## <a name="get-started"></a><span data-ttu-id="685a6-108">入门</span><span class="sxs-lookup"><span data-stu-id="685a6-108">Get Started</span></span>

<span data-ttu-id="685a6-109">这些教程演示了创建（或迁移）虚拟机、将 Web 应用程序发布到该虚拟机的步骤，以及在 Azure 中支持应用程序所要执行的其他任务。</span><span class="sxs-lookup"><span data-stu-id="685a6-109">These tutorials demonstrate the steps to create (or migrate) a virtual machine, publish your web application to it, and other tasks that may be required to support your application in Azure.</span></span>

- <span data-ttu-id="685a6-110">使用以下两个选项之一在 Azure 中为 ASP.NET 应用程序创建虚拟机：</span><span class="sxs-lookup"><span data-stu-id="685a6-110">Create a virtual machine for your ASP.NET application in Azure using one of the following two options:</span></span>
    - [<span data-ttu-id="685a6-111">为 ASP.NET 应用程序创建新的虚拟机</span><span class="sxs-lookup"><span data-stu-id="685a6-111">Create a new virtual machine for ASP.NET Applications</span></span>](https://go.microsoft.com/fwlink/?linkid=863237)
    - [<span data-ttu-id="685a6-112">迁移现有的本地虚拟机</span><span class="sxs-lookup"><span data-stu-id="685a6-112">Migrate an existing on-premises virtual machine</span></span>](https://docs.microsoft.com/azure/site-recovery/tutorial-migrate-on-premises-to-azure)
- [<span data-ttu-id="685a6-113">使用 Visual Studio 发布应用</span><span class="sxs-lookup"><span data-stu-id="685a6-113">Publish your app using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?linkid=863240)
- [<span data-ttu-id="685a6-114">为 VM 创建安全虚拟网络</span><span class="sxs-lookup"><span data-stu-id="685a6-114">Create a secure virtual network for your VMs</span></span>](https://docs.microsoft.com/azure/virtual-network/virtual-network-get-started-vnet-subnet)
- [<span data-ttu-id="685a6-115">为应用程序创建 CI/CD 管道</span><span class="sxs-lookup"><span data-stu-id="685a6-115">Create a CI/CD pipeline for your application</span></span>](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups)
- [<span data-ttu-id="685a6-116">转移到 VM 规模集以实现高可用性和可伸缩性</span><span class="sxs-lookup"><span data-stu-id="685a6-116">Move to a VM scale set for high availability and scalability</span></span>](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)

## <a name="considerations"></a><span data-ttu-id="685a6-117">注意事项</span><span class="sxs-lookup"><span data-stu-id="685a6-117">Considerations</span></span>

### <a name="benefits"></a><span data-ttu-id="685a6-118">优点</span><span class="sxs-lookup"><span data-stu-id="685a6-118">Benefits</span></span>

<span data-ttu-id="685a6-119">虚拟机提供将应用程序从本地迁移到云的最简单路径。</span><span class="sxs-lookup"><span data-stu-id="685a6-119">Virtual machines offer the easiest path to migrate an application from on-premises to the cloud.</span></span>  <span data-ttu-id="685a6-120">这样就可以复制应用程序在本地使用的相同环境，同时无需维护自己的数据中心。</span><span class="sxs-lookup"><span data-stu-id="685a6-120">They enable you to replicate the same environment your application uses on-premises, while removing the need to maintain your own data centers.</span></span>  <span data-ttu-id="685a6-121">虚拟机规模集为虚拟机中运行的应用程序提供高可用性和可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="685a6-121">Virtual Machine Scale Sets provide high availability and scalability for applications running in Virtual Machines.</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="685a6-122">虚拟机大小</span><span class="sxs-lookup"><span data-stu-id="685a6-122">Virtual Machine Size</span></span>

<span data-ttu-id="685a6-123">选择最大程度地针对工作负荷进行优化的虚拟机大小和类型。</span><span class="sxs-lookup"><span data-stu-id="685a6-123">Choose the virtual machine size and type that is best optimized for your workload.</span></span>  <span data-ttu-id="685a6-124">有关详细信息，请参阅 [Azure 中的 Windows 虚拟机大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)。</span><span class="sxs-lookup"><span data-stu-id="685a6-124">See [sizes for Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) for more information.</span></span>

### <a name="maintenance"></a><span data-ttu-id="685a6-125">维护</span><span class="sxs-lookup"><span data-stu-id="685a6-125">Maintenance</span></span>

<span data-ttu-id="685a6-126">就像在本地计算机上一样，你需要负责维护和更新虚拟机 <sup>&#42;</sup>。</span><span class="sxs-lookup"><span data-stu-id="685a6-126">Just like an on-premises machine, you are responsible for maintaining and updating the virtual machine<sup>&#42;</sup>.</span></span>  <span data-ttu-id="685a6-127">如果应用程序可以在 [Azure 应用服务](https://docs.microsoft.com/azure/app-service/)等平台即服务 (PaaS) 环境或者在[容器](https://docs.microsoft.com/azure/app-service/containers/)中运行，则不需要执行维护和更新。</span><span class="sxs-lookup"><span data-stu-id="685a6-127">If your application can run in a Platform as a Service (PaaS) environment such as [Azure App Service](https://docs.microsoft.com/azure/app-service/) or in a [container](https://docs.microsoft.com/azure/app-service/containers/), that will remove this need.</span></span>

<span data-ttu-id="685a6-128">*<sup>&#42;</sup>[虚拟机规模集的自动 OS 升级](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade)目前以预览服务提供。*</span><span class="sxs-lookup"><span data-stu-id="685a6-128">*<sup>&#42;</sup>[Automatic OS upgrades for virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) is currently available as a Preview service.*</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="685a6-129">虚拟网络</span><span class="sxs-lookup"><span data-stu-id="685a6-129">Virtual Networks</span></span>

<span data-ttu-id="685a6-130">使用 Azure 虚拟网络可以：</span><span class="sxs-lookup"><span data-stu-id="685a6-130">Azure Virtual Networks enable you to:</span></span>
- <span data-ttu-id="685a6-131">构建可控的混合基础结构</span><span class="sxs-lookup"><span data-stu-id="685a6-131">Build a hybrid infrastructure that you control</span></span>
- <span data-ttu-id="685a6-132">自带 IP 地址和 DNS 服务器</span><span class="sxs-lookup"><span data-stu-id="685a6-132">Bring your own IP addresses and DNS servers</span></span>
- <span data-ttu-id="685a6-133">为应用程序创建独立且高度安全的环境</span><span class="sxs-lookup"><span data-stu-id="685a6-133">Create an isolated and highly-secure environment for your applications</span></span>
- <span data-ttu-id="685a6-134">使用多个[连接选项](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)之一将 VM 连接到本地网络</span><span class="sxs-lookup"><span data-stu-id="685a6-134">Connect your VM to your on-premises network using one of several [connectivity options](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)</span></span>
- <span data-ttu-id="685a6-135">使用 [ExpressRoute](https://azure.microsoft.com/services/expressroute/) 将虚拟机集成到本地网络</span><span class="sxs-lookup"><span data-stu-id="685a6-135">Integrate your virtual machine into your on-premises network using [ExpressRoute](https://azure.microsoft.com/services/expressroute/)</span></span>

<span data-ttu-id="685a6-136">若要开始，请参阅[虚拟网络文档](https://docs.microsoft.com/azure/virtual-network/)</span><span class="sxs-lookup"><span data-stu-id="685a6-136">To get started, see the [Virtual Network documentation](https://docs.microsoft.com/azure/virtual-network/)</span></span>

### <a name="active-directory"></a><span data-ttu-id="685a6-137">Active Directory</span><span class="sxs-lookup"><span data-stu-id="685a6-137">Active Directory</span></span>
<span data-ttu-id="685a6-138">许多应用程序使用 Active Directory 进行身份验证和标识管理。</span><span class="sxs-lookup"><span data-stu-id="685a6-138">Many applications use Active Directory for authentication and identity management.</span></span>  
- <span data-ttu-id="685a6-139">使用 Azure AD Connect 可将本地目录与 Azure Active Directory 集成。</span><span class="sxs-lookup"><span data-stu-id="685a6-139">Azure AD Connect enables you to integrate your on-premises directories with Azure Active Directory.</span></span>  <span data-ttu-id="685a6-140">若要开始集成，请参阅[将本地目录与 Azure Active Directory 集成](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</span><span class="sxs-lookup"><span data-stu-id="685a6-140">To get started, see [Integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>  
- <span data-ttu-id="685a6-141">或者，可以让应用程序使用 [ExpressRoute](https://azure.microsoft.com/services/expressroute/) 访问本地 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="685a6-141">Alternatively, [ExpressRoute](https://azure.microsoft.com/services/expressroute/) enables your application to access your on-premises Active Directory.</span></span>

### <a name="sql-databases"></a><span data-ttu-id="685a6-142">SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="685a6-142">SQL Databases</span></span>

<span data-ttu-id="685a6-143">如果应用程序使用本地数据库，默认情况下，应用无法与该数据库通信。</span><span class="sxs-lookup"><span data-stu-id="685a6-143">If your application is using an on-premises database, your app will not be able to talk to it by default.</span></span> <span data-ttu-id="685a6-144">可以：</span><span class="sxs-lookup"><span data-stu-id="685a6-144">You can either:</span></span>
- <span data-ttu-id="685a6-145">配置一个混合网络来让应用程序访问本地运行的数据库。</span><span class="sxs-lookup"><span data-stu-id="685a6-145">Configure a hybrid network that enables your application to access your database running on-premises.</span></span>  
- <span data-ttu-id="685a6-146">将数据库迁移到 Azure</span><span class="sxs-lookup"><span data-stu-id="685a6-146">Migrate your database to the Azure.</span></span>  <span data-ttu-id="685a6-147">有关详细信息，请参阅[将 SQL Server 数据库迁移到 Azure](dotnet-howto-migrate-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="685a6-147">See [Migrate your SQL Server database to Azure](dotnet-howto-migrate-sql.md) for more information.</span></span>

### <a name="high-availability-and-scalability"></a><span data-ttu-id="685a6-148">高可用性和可伸缩性</span><span class="sxs-lookup"><span data-stu-id="685a6-148">High Availability and Scalability</span></span>

#### <a name="virtual-machine-scale-sets"></a><span data-ttu-id="685a6-149">虚拟机规模集</span><span class="sxs-lookup"><span data-stu-id="685a6-149">Virtual Machine Scale Sets</span></span>
<span data-ttu-id="685a6-150">如果想要确保应用程序具有高可用性并可缩放，可将 VM 映像迁移到 Azure 虚拟机规模集，以提高应用程序的可用性和可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="685a6-150">You want to make sure that your application is highly available and can scale, migrate your VM image to an Azure Virtual Machine Scale Set to improve the availability and scalability of your application.</span></span>  <span data-ttu-id="685a6-151">借助 VM 规模集，可以使用已配置的现有 VM 或设置一个生成管道来生成包含应用程序的映像。</span><span class="sxs-lookup"><span data-stu-id="685a6-151">VM Scale Sets provide the ability to use an existing VM you’ve already configured or set up a build pipeline to build an image with your application.</span></span>  

<span data-ttu-id="685a6-152">若要开始，请参阅[在虚拟机规模集上部署应用程序](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)。</span><span class="sxs-lookup"><span data-stu-id="685a6-152">To get started, see [Deploy your application on virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).</span></span>

#### <a name="centralized-logging"></a><span data-ttu-id="685a6-153">集中式日志记录</span><span class="sxs-lookup"><span data-stu-id="685a6-153">Centralized Logging</span></span>
<span data-ttu-id="685a6-154">跨多个实例运行应用程序时，请考虑将日志存储在某个中心位置，例如 [Azure 存储](https://docs.microsoft.com/azure/storage/)。</span><span class="sxs-lookup"><span data-stu-id="685a6-154">When running your application across multiple instances, consider storing your logs in a centralized location such as [Azure Storage](https://docs.microsoft.com/azure/storage/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="685a6-155">后续步骤</span><span class="sxs-lookup"><span data-stu-id="685a6-155">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="685a6-156">将 SQL Server 数据库迁移到 Azure</span><span class="sxs-lookup"><span data-stu-id="685a6-156">Migrate a SQL Server database to Azure</span></span>](dotnet-howto-migrate-sql.md)