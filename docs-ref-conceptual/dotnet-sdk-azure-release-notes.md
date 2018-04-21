---
title: 用于 .NET 的 Azure 管理库发行说明 | Microsoft Docs
description: 了解用于 .NET 的 Azure 管理库的新增功能，并留意其中的重大更改。
keywords: Azure, .NET, API, 参考, 说明, 更新, 弃用
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 48ff29507268f6b38acb24217801cf7b0227e444
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2018
---
# <a name="release-notes"></a><span data-ttu-id="45cb5-104">发行说明</span><span class="sxs-lookup"><span data-stu-id="45cb5-104">Release Notes</span></span> 

## <a name="feature-availability-and-road-map-as-of-version-100"></a><span data-ttu-id="45cb5-105">截止版本 1.0.0 的功能可用性和路线图</span><span class="sxs-lookup"><span data-stu-id="45cb5-105">Feature Availability and Road Map as of Version 1.0.0</span></span> ##
### <a name="april-26-2017"></a><span data-ttu-id="45cb5-106">2017 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="45cb5-106">April 26, 2017</span></span>

<table>
  <tr>
    <th align="left"><span data-ttu-id="45cb5-107">服务 | 功能</span><span class="sxs-lookup"><span data-stu-id="45cb5-107">Service | feature</span></span></th>
    <th align="left"><span data-ttu-id="45cb5-108">以正式版提供</span><span class="sxs-lookup"><span data-stu-id="45cb5-108">Available as GA</span></span></th>
    <th align="left"><span data-ttu-id="45cb5-109">以预览版提供</span><span class="sxs-lookup"><span data-stu-id="45cb5-109">Available as Preview</span></span></th>
    <th align="left"><span data-ttu-id="45cb5-110">即将支持</span><span class="sxs-lookup"><span data-stu-id="45cb5-110">Coming soon</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="45cb5-111">计算</span><span class="sxs-lookup"><span data-stu-id="45cb5-111">Compute</span></span></td>
    <td><span data-ttu-id="45cb5-112">虚拟机和 VM 扩展</span><span class="sxs-lookup"><span data-stu-id="45cb5-112">Virtual machines and VM extensions</span></span><br><span data-ttu-id="45cb5-113">虚拟机规模集</span><span class="sxs-lookup"><span data-stu-id="45cb5-113">Virtual machine scale sets</span></span><br><span data-ttu-id="45cb5-114">托管磁盘</span><span class="sxs-lookup"><span data-stu-id="45cb5-114">Managed disks</span></span></td>
    <td></td>
    <td valign="top"><span data-ttu-id="45cb5-115">Azure 容器服务</span><span class="sxs-lookup"><span data-stu-id="45cb5-115">Azure container services</span></span><br><span data-ttu-id="45cb5-116">Azure 容器注册表</span><span class="sxs-lookup"><span data-stu-id="45cb5-116">Azure container registry</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="45cb5-117">存储</span><span class="sxs-lookup"><span data-stu-id="45cb5-117">Storage</span></span></td>
    <td><span data-ttu-id="45cb5-118">存储帐户</span><span class="sxs-lookup"><span data-stu-id="45cb5-118">Storage accounts</span></span></td>
    <td></td>
    <td><span data-ttu-id="45cb5-119">加密</span><span class="sxs-lookup"><span data-stu-id="45cb5-119">Encryption</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="45cb5-120">SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="45cb5-120">SQL Database</span></span></td>
    <td><span data-ttu-id="45cb5-121">数据库</span><span class="sxs-lookup"><span data-stu-id="45cb5-121">Databases</span></span><br><span data-ttu-id="45cb5-122">防火墙</span><span class="sxs-lookup"><span data-stu-id="45cb5-122">Firewalls</span></span><br><span data-ttu-id="45cb5-123">弹性池</span><span class="sxs-lookup"><span data-stu-id="45cb5-123">Elastic pools</span></span></td>
    <td></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="45cb5-124">网络</span><span class="sxs-lookup"><span data-stu-id="45cb5-124">Networking</span></span></td>
    <td><span data-ttu-id="45cb5-125">虚拟网络</span><span class="sxs-lookup"><span data-stu-id="45cb5-125">Virtual networks</span></span><br><span data-ttu-id="45cb5-126">网络接口</span><span class="sxs-lookup"><span data-stu-id="45cb5-126">Network interfaces</span></span><br><span data-ttu-id="45cb5-127">IP 地址</span><span class="sxs-lookup"><span data-stu-id="45cb5-127">IP addresses</span></span><br><span data-ttu-id="45cb5-128">路由表</span><span class="sxs-lookup"><span data-stu-id="45cb5-128">Routing table</span></span><br><span data-ttu-id="45cb5-129">网络安全组</span><span class="sxs-lookup"><span data-stu-id="45cb5-129">Network security groups</span></span><br><span data-ttu-id="45cb5-130">DNS</span><span class="sxs-lookup"><span data-stu-id="45cb5-130">DNS</span></span><br><span data-ttu-id="45cb5-131">流量管理器</span><span class="sxs-lookup"><span data-stu-id="45cb5-131">Traffic managers</span></span></td>
    <td valign="top"><span data-ttu-id="45cb5-132">负载均衡器</span><span class="sxs-lookup"><span data-stu-id="45cb5-132">Load balancers</span></span><br><span data-ttu-id="45cb5-133">应用程序网关数</span><span class="sxs-lookup"><span data-stu-id="45cb5-133">Application gateways</span></span></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="45cb5-134">其他服务</span><span class="sxs-lookup"><span data-stu-id="45cb5-134">More services</span></span></td>
    <td><span data-ttu-id="45cb5-135">资源管理器</span><span class="sxs-lookup"><span data-stu-id="45cb5-135">Resource Manager</span></span><br><span data-ttu-id="45cb5-136">Key Vault</span><span class="sxs-lookup"><span data-stu-id="45cb5-136">Key Vault</span></span><br><span data-ttu-id="45cb5-137">Redis</span><span class="sxs-lookup"><span data-stu-id="45cb5-137">Redis</span></span><br><span data-ttu-id="45cb5-138">CDN</span><span class="sxs-lookup"><span data-stu-id="45cb5-138">CDN</span></span><br><span data-ttu-id="45cb5-139">Batch</span><span class="sxs-lookup"><span data-stu-id="45cb5-139">Batch</span></span></td>
    <td valign="top"><span data-ttu-id="45cb5-140">应用服务 - Web 应用</span><span class="sxs-lookup"><span data-stu-id="45cb5-140">App service - Web apps</span></span><br><span data-ttu-id="45cb5-141">函数</span><span class="sxs-lookup"><span data-stu-id="45cb5-141">Functions</span></span><br><span data-ttu-id="45cb5-142">服务总线</span><span class="sxs-lookup"><span data-stu-id="45cb5-142">Service bus</span></span></td>
    <td valign="top"><span data-ttu-id="45cb5-143">监视</span><span class="sxs-lookup"><span data-stu-id="45cb5-143">Monitor</span></span><br><span data-ttu-id="45cb5-144">Graph RBAC</span><span class="sxs-lookup"><span data-stu-id="45cb5-144">Graph RBAC</span></span><br><span data-ttu-id="45cb5-145">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="45cb5-145">Azure Cosmos DB</span></span><br><span data-ttu-id="45cb5-146">计划程序</span><span class="sxs-lookup"><span data-stu-id="45cb5-146">Scheduler</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="45cb5-147">基本</span><span class="sxs-lookup"><span data-stu-id="45cb5-147">Fundamentals</span></span></td>
    <td><span data-ttu-id="45cb5-148">身份验证 - 核心身份验证</span><span class="sxs-lookup"><span data-stu-id="45cb5-148">Authentication - core</span></span></td>
    <td><span data-ttu-id="45cb5-149">异步方法</span><span class="sxs-lookup"><span data-stu-id="45cb5-149">Async methods</span></span></td>
    <td valign="top"></td>
  </tr>
</table>

> [!WARNING] 
> <span data-ttu-id="45cb5-150">*预览*功能在库中带有文档注释。</span><span class="sxs-lookup"><span data-stu-id="45cb5-150">*Preview* features are flagged in documentation comments in libraries.</span></span> <span data-ttu-id="45cb5-151">这些功能随时会变化。</span><span class="sxs-lookup"><span data-stu-id="45cb5-151">These features are subject to change.</span></span> <span data-ttu-id="45cb5-152">将来可能会以任何方式对其进行修改（甚至删除）。</span><span class="sxs-lookup"><span data-stu-id="45cb5-152">They can be modified in any way (or even removed) in the future.</span></span>

[!include[Contribute and community](includes/contribute.md)]
