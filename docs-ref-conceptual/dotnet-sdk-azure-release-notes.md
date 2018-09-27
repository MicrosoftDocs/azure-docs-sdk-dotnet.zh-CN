---
title: 用于 .NET 的 Azure 管理库发行说明 | Microsoft Docs
description: 了解用于 .NET 的 Azure 管理库的新增功能，并留意其中的重大更改。
ms.date: 10/19/2017
ms.openlocfilehash: dac9dee9c25fc349dedd50d6007f25c7d15b0928
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190670"
---
# <a name="release-notes"></a><span data-ttu-id="ea1a6-103">发行说明</span><span class="sxs-lookup"><span data-stu-id="ea1a6-103">Release Notes</span></span> 

## <a name="feature-availability-and-road-map-as-of-version-100"></a><span data-ttu-id="ea1a6-104">截止版本 1.0.0 的功能可用性和路线图</span><span class="sxs-lookup"><span data-stu-id="ea1a6-104">Feature Availability and Road Map as of Version 1.0.0</span></span> ##
### <a name="april-26-2017"></a><span data-ttu-id="ea1a6-105">2017 年 4 月 26 日</span><span class="sxs-lookup"><span data-stu-id="ea1a6-105">April 26, 2017</span></span>

<table>
  <tr>
    <th align="left"><span data-ttu-id="ea1a6-106">服务 | 功能</span><span class="sxs-lookup"><span data-stu-id="ea1a6-106">Service | feature</span></span></th>
    <th align="left"><span data-ttu-id="ea1a6-107">以正式版提供</span><span class="sxs-lookup"><span data-stu-id="ea1a6-107">Available as GA</span></span></th>
    <th align="left"><span data-ttu-id="ea1a6-108">以预览版提供</span><span class="sxs-lookup"><span data-stu-id="ea1a6-108">Available as Preview</span></span></th>
    <th align="left"><span data-ttu-id="ea1a6-109">即将支持</span><span class="sxs-lookup"><span data-stu-id="ea1a6-109">Coming soon</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="ea1a6-110">计算</span><span class="sxs-lookup"><span data-stu-id="ea1a6-110">Compute</span></span></td>
    <td><span data-ttu-id="ea1a6-111">虚拟机和 VM 扩展</span><span class="sxs-lookup"><span data-stu-id="ea1a6-111">Virtual machines and VM extensions</span></span><br><span data-ttu-id="ea1a6-112">虚拟机规模集</span><span class="sxs-lookup"><span data-stu-id="ea1a6-112">Virtual machine scale sets</span></span><br><span data-ttu-id="ea1a6-113">托管磁盘</span><span class="sxs-lookup"><span data-stu-id="ea1a6-113">Managed disks</span></span></td>
    <td></td>
    <td valign="top"><span data-ttu-id="ea1a6-114">Azure 容器服务</span><span class="sxs-lookup"><span data-stu-id="ea1a6-114">Azure container services</span></span><br><span data-ttu-id="ea1a6-115">Azure 容器注册表</span><span class="sxs-lookup"><span data-stu-id="ea1a6-115">Azure container registry</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ea1a6-116">存储</span><span class="sxs-lookup"><span data-stu-id="ea1a6-116">Storage</span></span></td>
    <td><span data-ttu-id="ea1a6-117">存储帐户</span><span class="sxs-lookup"><span data-stu-id="ea1a6-117">Storage accounts</span></span></td>
    <td></td>
    <td><span data-ttu-id="ea1a6-118">加密</span><span class="sxs-lookup"><span data-stu-id="ea1a6-118">Encryption</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ea1a6-119">SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="ea1a6-119">SQL Database</span></span></td>
    <td><span data-ttu-id="ea1a6-120">数据库</span><span class="sxs-lookup"><span data-stu-id="ea1a6-120">Databases</span></span><br><span data-ttu-id="ea1a6-121">防火墙</span><span class="sxs-lookup"><span data-stu-id="ea1a6-121">Firewalls</span></span><br><span data-ttu-id="ea1a6-122">弹性池</span><span class="sxs-lookup"><span data-stu-id="ea1a6-122">Elastic pools</span></span></td>
    <td></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ea1a6-123">网络</span><span class="sxs-lookup"><span data-stu-id="ea1a6-123">Networking</span></span></td>
    <td><span data-ttu-id="ea1a6-124">虚拟网络</span><span class="sxs-lookup"><span data-stu-id="ea1a6-124">Virtual networks</span></span><br><span data-ttu-id="ea1a6-125">网络接口</span><span class="sxs-lookup"><span data-stu-id="ea1a6-125">Network interfaces</span></span><br><span data-ttu-id="ea1a6-126">IP 地址</span><span class="sxs-lookup"><span data-stu-id="ea1a6-126">IP addresses</span></span><br><span data-ttu-id="ea1a6-127">路由表</span><span class="sxs-lookup"><span data-stu-id="ea1a6-127">Routing table</span></span><br><span data-ttu-id="ea1a6-128">网络安全组</span><span class="sxs-lookup"><span data-stu-id="ea1a6-128">Network security groups</span></span><br><span data-ttu-id="ea1a6-129">DNS</span><span class="sxs-lookup"><span data-stu-id="ea1a6-129">DNS</span></span><br><span data-ttu-id="ea1a6-130">流量管理器</span><span class="sxs-lookup"><span data-stu-id="ea1a6-130">Traffic managers</span></span></td>
    <td valign="top"><span data-ttu-id="ea1a6-131">负载均衡器</span><span class="sxs-lookup"><span data-stu-id="ea1a6-131">Load balancers</span></span><br><span data-ttu-id="ea1a6-132">应用程序网关数</span><span class="sxs-lookup"><span data-stu-id="ea1a6-132">Application gateways</span></span></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ea1a6-133">其他服务</span><span class="sxs-lookup"><span data-stu-id="ea1a6-133">More services</span></span></td>
    <td><span data-ttu-id="ea1a6-134">资源管理器</span><span class="sxs-lookup"><span data-stu-id="ea1a6-134">Resource Manager</span></span><br><span data-ttu-id="ea1a6-135">Key Vault</span><span class="sxs-lookup"><span data-stu-id="ea1a6-135">Key Vault</span></span><br><span data-ttu-id="ea1a6-136">Redis</span><span class="sxs-lookup"><span data-stu-id="ea1a6-136">Redis</span></span><br><span data-ttu-id="ea1a6-137">CDN</span><span class="sxs-lookup"><span data-stu-id="ea1a6-137">CDN</span></span><br><span data-ttu-id="ea1a6-138">Batch</span><span class="sxs-lookup"><span data-stu-id="ea1a6-138">Batch</span></span></td>
    <td valign="top"><span data-ttu-id="ea1a6-139">应用服务 - Web 应用</span><span class="sxs-lookup"><span data-stu-id="ea1a6-139">App service - Web apps</span></span><br><span data-ttu-id="ea1a6-140">函数</span><span class="sxs-lookup"><span data-stu-id="ea1a6-140">Functions</span></span><br><span data-ttu-id="ea1a6-141">服务总线</span><span class="sxs-lookup"><span data-stu-id="ea1a6-141">Service bus</span></span></td>
    <td valign="top"><span data-ttu-id="ea1a6-142">监视</span><span class="sxs-lookup"><span data-stu-id="ea1a6-142">Monitor</span></span><br><span data-ttu-id="ea1a6-143">Graph RBAC</span><span class="sxs-lookup"><span data-stu-id="ea1a6-143">Graph RBAC</span></span><br><span data-ttu-id="ea1a6-144">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ea1a6-144">Azure Cosmos DB</span></span><br><span data-ttu-id="ea1a6-145">计划程序</span><span class="sxs-lookup"><span data-stu-id="ea1a6-145">Scheduler</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ea1a6-146">基本</span><span class="sxs-lookup"><span data-stu-id="ea1a6-146">Fundamentals</span></span></td>
    <td><span data-ttu-id="ea1a6-147">身份验证 - 核心身份验证</span><span class="sxs-lookup"><span data-stu-id="ea1a6-147">Authentication - core</span></span></td>
    <td><span data-ttu-id="ea1a6-148">异步方法</span><span class="sxs-lookup"><span data-stu-id="ea1a6-148">Async methods</span></span></td>
    <td valign="top"></td>
  </tr>
</table>

> [!WARNING] 
> <span data-ttu-id="ea1a6-149">*预览*功能在库中带有文档注释。</span><span class="sxs-lookup"><span data-stu-id="ea1a6-149">*Preview* features are flagged in documentation comments in libraries.</span></span> <span data-ttu-id="ea1a6-150">这些功能随时会变化。</span><span class="sxs-lookup"><span data-stu-id="ea1a6-150">These features are subject to change.</span></span> <span data-ttu-id="ea1a6-151">将来可能会以任何方式对其进行修改（甚至删除）。</span><span class="sxs-lookup"><span data-stu-id="ea1a6-151">They can be modified in any way (or even removed) in the future.</span></span>

[!include[Contribute and community](includes/contribute.md)]
