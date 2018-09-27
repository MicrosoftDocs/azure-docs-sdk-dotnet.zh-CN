---
title: 将 SQL Server 数据库迁移到 Azure
description: 了解如何将 SQL Server 数据库从本地 SQL Server 迁移到 Azure。
ms.date: 11/15/2017
ms.service: sql-database
ms.openlocfilehash: 49b03632b8ebe31439b3c39629fdaf751412fd5a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190510"
---
## <a name="migrate-a-sql-server-database-to-azure"></a><span data-ttu-id="9a0c5-103">将 SQL Server 数据库迁移到 Azure</span><span class="sxs-lookup"><span data-stu-id="9a0c5-103">Migrate a SQL Server database to Azure</span></span>

<span data-ttu-id="9a0c5-104">本短文提供了用于将 SQL Server 数据库迁移到 Azure 的两个选项的简要概述。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-104">This short article provides a brief outline of two options for migrating a SQL Server database to Azure.</span></span>

<span data-ttu-id="9a0c5-105">Azure 提供两个主要选项用于迁移生产 SQL Server 数据库：</span><span class="sxs-lookup"><span data-stu-id="9a0c5-105">Azure has two primary options for migrating a production SQL Server database:</span></span>

1. <span data-ttu-id="9a0c5-106">[Azure VM 中的 SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)：在 Azure 中运行的 Windows 虚拟机上安装和托管的 SQL Server 实例，也称为基础结构即服务 (IaaS)。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-106">[SQL Server on Azure VMs](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview): A SQL Server instance installed and hosted on a Windows Virtual Machine running in Azure, also known as Infrastructure as a Service (IaaS).</span></span>
2. <span data-ttu-id="9a0c5-107">[Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)：完全托管的 SQL 数据库 Azure 服务，也称为平台即服务 (PaaS)。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-107">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview): A fully managed SQL database Azure service, also known as Platform as a Service (PaaS).</span></span>

<span data-ttu-id="9a0c5-108">两者各有利弊，在迁移之前需要进行评估。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-108">Both come with pros and cons that you will need to evaluate before migrating.</span></span>

## <a name="get-started"></a><span data-ttu-id="9a0c5-109">入门</span><span class="sxs-lookup"><span data-stu-id="9a0c5-109">Get started</span></span>

<span data-ttu-id="9a0c5-110">以下迁移指南将十分有用，具体取决于你使用哪个服务：</span><span class="sxs-lookup"><span data-stu-id="9a0c5-110">The following migration guides will be useful, depending on which service you use:</span></span>

* [<span data-ttu-id="9a0c5-111">将 SQL Server 数据库迁移到 Azure VM 中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="9a0c5-111">Migrate a SQL Server database to SQL Server in an Azure VM</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)
* [<span data-ttu-id="9a0c5-112">将 SQL Server 数据库迁移至 Azure SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="9a0c5-112">Migrate your SQL Server database to Azure SQL Database</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

<span data-ttu-id="9a0c5-113">此外，以下概念性内容的链接将帮助你更好地理解 VM：</span><span class="sxs-lookup"><span data-stu-id="9a0c5-113">Additionally, the following links to conceptual content will help you understand VMs better:</span></span>

* [<span data-ttu-id="9a0c5-114">Azure 虚拟机中 SQL Server 的高可用性和灾难恢复</span><span class="sxs-lookup"><span data-stu-id="9a0c5-114">High availability and disaster recovery for SQL Server in Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)
* [<span data-ttu-id="9a0c5-115">Azure 虚拟机中 SQL Server 的性能最佳实践</span><span class="sxs-lookup"><span data-stu-id="9a0c5-115">Performance best practices for SQL Server in Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)
* [<span data-ttu-id="9a0c5-116">Azure 虚拟机中的 SQL Server 的应用程序模式和开发策略</span><span class="sxs-lookup"><span data-stu-id="9a0c5-116">Application Patterns and Development Strategies for SQL Server in Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-app-patterns-dev-strategies)

<span data-ttu-id="9a0c5-117">以下链接有助于更好地了解 Azure SQL 数据库：</span><span class="sxs-lookup"><span data-stu-id="9a0c5-117">And the following links will help you understand Azure SQL Database better:</span></span>

* [<span data-ttu-id="9a0c5-118">创建和管理 Azure SQL 数据库服务器与数据库</span><span class="sxs-lookup"><span data-stu-id="9a0c5-118">Create and manage Azure SQL Database servers and databases</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases)
* [<span data-ttu-id="9a0c5-119">数据库事务单位 (DTU) 和弹性数据库事务单位 (eDTU)</span><span class="sxs-lookup"><span data-stu-id="9a0c5-119">Database Transaction Units (DTUs) and elastic Database Transaction Units (eDTUs)</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)
* [<span data-ttu-id="9a0c5-120">Azure SQL 数据库资源限制</span><span class="sxs-lookup"><span data-stu-id="9a0c5-120">Azure SQL Database resource limits</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits)

## <a name="choosing-iaas-or-paas"></a><span data-ttu-id="9a0c5-121">选择 IaaS 或 PaaS</span><span class="sxs-lookup"><span data-stu-id="9a0c5-121">Choosing IaaS or PaaS</span></span>

<span data-ttu-id="9a0c5-122">当评估数据库要迁移到的位置时，应确定是 IaaS 还是 PaaS 更适合你。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-122">When evaluating where to migrate your database, you should determine if IaaS or PaaS is more appropriate for you.</span></span>

<span data-ttu-id="9a0c5-123">**对于以下情况，应选择 Azure VM 中的 SQL Server：**</span><span class="sxs-lookup"><span data-stu-id="9a0c5-123">**You should choose SQL Server in Azure VMs if:**</span></span>

* <span data-ttu-id="9a0c5-124">希望在进行少量的更改甚至无需更改的情况下，“直接迁移”数据库和应用程序。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-124">You are looking to "lift and shift" your database and applications with minimal to no changes.</span></span>
* <span data-ttu-id="9a0c5-125">希望完全控制数据库服务器及其运行所在的 VM。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-125">You prefer having full control over your database server and the VM it runs on.</span></span>
* <span data-ttu-id="9a0c5-126">已获得想要使用的 SQL Server 和 Windows Server 许可证。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-126">You already have SQL Server and Windows Server licenses that you intend to use.</span></span>

<span data-ttu-id="9a0c5-127">**对于以下情况，应选择 Azure SQL 数据库：**</span><span class="sxs-lookup"><span data-stu-id="9a0c5-127">**You should choose Azure SQL Database if:**</span></span>

* <span data-ttu-id="9a0c5-128">想要将应用程序现代化并进行迁移，以使用 Azure 中的其他 PaaS 服务。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-128">You are looking to modernize your applications and are migrating to use other PaaS services in Azure.</span></span>
* <span data-ttu-id="9a0c5-129">不希望管理数据库服务器及其运行所在的 VM。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-129">You do not wish to manage your database server and the VM it runs on.</span></span>
* <span data-ttu-id="9a0c5-130">未获得 SQL Server 或 Windows Server 许可证，或打算让现有的许可证过期。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-130">You do not have SQL Server or Windows Server licenses, or you intend to let licenses you have expire.</span></span>

<span data-ttu-id="9a0c5-131">下表根据一组情景描述了不同服务之间的差异。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-131">The following table describes differences between each service based on a set of scenarios.</span></span>

| <span data-ttu-id="9a0c5-132">场景</span><span class="sxs-lookup"><span data-stu-id="9a0c5-132">Scenario</span></span> | <span data-ttu-id="9a0c5-133">Azure VM 中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="9a0c5-133">SQL Server in Azure VMs</span></span> | <span data-ttu-id="9a0c5-134">Azure SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="9a0c5-134">Azure SQL Database</span></span> |
|----------|-------------------------|--------------------|
| <span data-ttu-id="9a0c5-135">迁移</span><span class="sxs-lookup"><span data-stu-id="9a0c5-135">Migration</span></span> | <span data-ttu-id="9a0c5-136">需要对数据库进行少量的更改。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-136">Requires minimal changes to your database.</span></span> | <span data-ttu-id="9a0c5-137">如果使用 Azure SQL 中不可用的功能（哪些功能可用由[数据迁移助手](https://www.microsoft.com/download/details.aspx?id=53595)确定），或者存在其他依赖项（例如本地安装的可执行文件），则可能需要对数据库进行更改。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-137">May require changes to your database if you use features unavailable in Azure SQL, as determined by the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595), or if you have other dependencies such as locally installed executables.</span></span>|
| <span data-ttu-id="9a0c5-138">管理可用性、恢复和升级</span><span class="sxs-lookup"><span data-stu-id="9a0c5-138">Managing availability, recovery, and upgrades</span></span> | <span data-ttu-id="9a0c5-139">手动配置可用性和恢复。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-139">Availability and recovery is configured manually.</span></span> <span data-ttu-id="9a0c5-140">可以使用 [VM 规模集](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade)自动升级。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-140">Upgrades can be automated with [VM Scale Sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade).</span></span> | <span data-ttu-id="9a0c5-141">由系统自动管理。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-141">Automatically managed for you.</span></span> |
| <span data-ttu-id="9a0c5-142">基础 OS 配置</span><span class="sxs-lookup"><span data-stu-id="9a0c5-142">Underlying OS configuration</span></span> | <span data-ttu-id="9a0c5-143">手动配置。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-143">Manual configuration.</span></span> | <span data-ttu-id="9a0c5-144">由系统自动管理。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-144">Automatically managed for you.</span></span> |
| <span data-ttu-id="9a0c5-145">管理数据库大小</span><span class="sxs-lookup"><span data-stu-id="9a0c5-145">Managing database size</span></span> | <span data-ttu-id="9a0c5-146">支持为每个 SQL Server 实例最多配置 64TB 存储。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-146">Supports up to 64TB of storage per SQL Server instance.</span></span> | <span data-ttu-id="9a0c5-147">支持 4TB 存储，超过此限制后，需要横向分区。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-147">Supports 4TB of storage before needing a horizontal partition.</span></span> |
| <span data-ttu-id="9a0c5-148">管理成本</span><span class="sxs-lookup"><span data-stu-id="9a0c5-148">Managing costs</span></span> | <span data-ttu-id="9a0c5-149">必须管理 SQL Server 许可成本、Windows Server 许可成本和 VM 成本（基于核心数、RAM 和存储）。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-149">You must manage SQL Server license costs, Windows Server license costs, and VM costs (based on cores, RAM, and storage).</span></span> | <span data-ttu-id="9a0c5-150">必须管理服务成本（基于 [eDTU 或 DTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)、存储，以及数据库数目（如果使用弹性池））。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-150">You must manage service costs (based on [eDTUs or DTUs](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu), storage, and number of databases if using an elastic pool).</span></span>  <span data-ttu-id="9a0c5-151">此外，必须管理任何 SLA 的成本。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-151">You must also manage the cost of any SLA.</span></span> |

<span data-ttu-id="9a0c5-152">若要了解有关两者之间的差异的详细信息，请阅读“选择云 SQL Server 选项：[Azure SQL 数据库或 Azure VM 上的 SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas)”。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-152">To learn more about the differences between the two, read Choose a cloud SQL Server option: [Azure SQL Database or SQL Server on Azure VMs](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas).</span></span>

## <a name="faq"></a><span data-ttu-id="9a0c5-153">常见问题解答</span><span class="sxs-lookup"><span data-stu-id="9a0c5-153">FAQ</span></span>

* <span data-ttu-id="9a0c5-154">**是否仍可对 Azure VM 中的 SQL Server 或 Azure SQL 数据库使用 SQL Server Management Studio 和 SQL Server Reporting Services (SSRS) 等工具？**</span><span class="sxs-lookup"><span data-stu-id="9a0c5-154">**Can I still use tools such as SQL Server Management Studio and SQL Server Reporting Services (SSRS) with SQL Server in Azure VMs or Azure SQL Database?**</span></span>

    <span data-ttu-id="9a0c5-155">能！</span><span class="sxs-lookup"><span data-stu-id="9a0c5-155">Yes!</span></span> <span data-ttu-id="9a0c5-156">所有 Microsoft SQL 工具都适用于这两个服务。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-156">All Microsoft SQL tooling works with both services.</span></span> <span data-ttu-id="9a0c5-157">不过，SSRS 不是 Azure SQL 数据库的一部分，我们建议在 Azure VM 中运行它，然后将它指向数据库实例。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-157">SSRS is not part of Azure SQL Database, though, and it's recommended that you run it in an Azure VM and then point it to your database instance.</span></span>
    
* <span data-ttu-id="9a0c5-158">**我想要改用 PaaS，但我不确定数据库是否兼容。是否可以借助某些工具？**</span><span class="sxs-lookup"><span data-stu-id="9a0c5-158">**I want to go PaaS but I'm not sure if my database is compatible. Are there tools to help?**</span></span>

    <span data-ttu-id="9a0c5-159">是的。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-159">Yes.</span></span> <span data-ttu-id="9a0c5-160">在迁移到 Azure SQL 数据库过程中，可以使用[数据迁移助手](https://www.microsoft.com/download/details.aspx?id=53595)工具。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-160">The [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) is a tool that is used as a part of migrating to Azure SQL Database.</span></span>  <span data-ttu-id="9a0c5-161">[Azure 数据库迁移服务](https://azure.microsoft.com/campaigns/database-migration/)是可用于 IaaS 或 PaaS 的预览服务。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-161">The [Azure Database Migration Service](https://azure.microsoft.com/campaigns/database-migration/) is a preview service which you can use for either IaaS or PaaS.</span></span>

* <span data-ttu-id="9a0c5-162">**是否可以估算成本？**</span><span class="sxs-lookup"><span data-stu-id="9a0c5-162">**Can I estimate costs?**</span></span>

    <span data-ttu-id="9a0c5-163">是的。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-163">Yes.</span></span>  <span data-ttu-id="9a0c5-164">可以使用 [Azure 定价计算器](https://azure.microsoft.com/pricing/calculator/)估算所有 Azure 服务（包括 VM 和数据库服务）的成本。</span><span class="sxs-lookup"><span data-stu-id="9a0c5-164">The [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) can be used for estimating costs for all Azure services, including VMs and database services.</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="9a0c5-165">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9a0c5-165">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a0c5-166">选择适当的 Azure 托管选项</span><span class="sxs-lookup"><span data-stu-id="9a0c5-166">Choose the right Azure hosting option</span></span>](dotnet-howto-choose-migration.md)
