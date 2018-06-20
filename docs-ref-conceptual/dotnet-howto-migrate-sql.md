---
title: 将 SQL Server 数据库迁移到 Azure
description: 了解如何将 SQL Server 数据库从本地 SQL Server 迁移到 Azure。
keywords: Azure .NET, ASP.NET, SQL, SQL Server, SQL 数据库, 迁移
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: sql-database
ms.custom: devcenter
ms.openlocfilehash: d118d39e2168686c851f0daa6cb611f0a0c9d2fc
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
ms.locfileid: "29728488"
---
## <a name="migrate-a-sql-server-database-to-azure"></a>将 SQL Server 数据库迁移到 Azure

本短文提供了用于将 SQL Server 数据库迁移到 Azure 的两个选项的简要概述。

Azure 提供两个主要选项用于迁移生产 SQL Server 数据库：

1. [Azure VM 中的 SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)：在 Azure 中运行的 Windows 虚拟机上安装和托管的 SQL Server 实例，也称为基础结构即服务 (IaaS)。
2. [Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)：完全托管的 SQL 数据库 Azure 服务，也称为平台即服务 (PaaS)。

两者各有利弊，在迁移之前需要进行评估。

## <a name="get-started"></a>入门

以下迁移指南将十分有用，具体取决于你使用哪个服务：

* [将 SQL Server 数据库迁移到 Azure VM 中的 SQL Server](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)
* [将 SQL Server 数据库迁移至 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

此外，以下概念性内容的链接将帮助你更好地理解 VM：

* [Azure 虚拟机中 SQL Server 的高可用性和灾难恢复](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)
* [Azure 虚拟机中 SQL Server 的性能最佳实践](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)
* [Azure 虚拟机中的 SQL Server 的应用程序模式和开发策略](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-app-patterns-dev-strategies)

以下链接有助于更好地了解 Azure SQL 数据库：

* [创建和管理 Azure SQL 数据库服务器与数据库](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases)
* [数据库事务单位 (DTU) 和弹性数据库事务单位 (eDTU)](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)
* [Azure SQL 数据库资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits)

## <a name="choosing-iaas-or-paas"></a>选择 IaaS 或 PaaS

当评估数据库要迁移到的位置时，应确定是 IaaS 还是 PaaS 更适合你。

**对于以下情况，应选择 Azure VM 中的 SQL Server：**

* 希望在进行少量的更改甚至无需更改的情况下，“直接迁移”数据库和应用程序。
* 希望完全控制数据库服务器及其运行所在的 VM。
* 已获得想要使用的 SQL Server 和 Windows Server 许可证。

**对于以下情况，应选择 Azure SQL 数据库：**

* 想要将应用程序现代化并进行迁移，以使用 Azure 中的其他 PaaS 服务。
* 不希望管理数据库服务器及其运行所在的 VM。
* 未获得 SQL Server 或 Windows Server 许可证，或打算让现有的许可证过期。

下表根据一组情景描述了不同服务之间的差异。

| 方案 | Azure VM 中的 SQL Server | Azure SQL 数据库 |
|----------|-------------------------|--------------------|
| 迁移 | 需要对数据库进行少量的更改。 | 如果使用 Azure SQL 中不可用的功能（哪些功能可用由[数据迁移助手](https://www.microsoft.com/download/details.aspx?id=53595)确定），或者存在其他依赖项（例如本地安装的可执行文件），则可能需要对数据库进行更改。|
| 管理可用性、恢复和升级 | 手动配置可用性和恢复。 可以使用 [VM 规模集](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade)自动升级。 | 由系统自动管理。 |
| 基础 OS 配置 | 手动配置。 | 由系统自动管理。 |
| 管理数据库大小 | 支持为每个 SQL Server 实例最多配置 64TB 存储。 | 支持 4TB 存储，超过此限制后，需要横向分区。 |
| 管理成本 | 必须管理 SQL Server 许可成本、Windows Server 许可成本和 VM 成本（基于核心数、RAM 和存储）。 | 必须管理服务成本（基于 [eDTU 或 DTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)、存储，以及数据库数目（如果使用弹性池））。  此外，必须管理任何 SLA 的成本。 |

若要了解有关两者之间的差异的详细信息，请阅读“选择云 SQL Server 选项：[Azure SQL 数据库或 Azure VM 上的 SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas)”。

## <a name="faq"></a>常见问题

* **是否仍可对 Azure VM 中的 SQL Server 或 Azure SQL 数据库使用 SQL Server Management Studio 和 SQL Server Reporting Services (SSRS) 等工具？**

    能！ 所有 Microsoft SQL 工具都适用于这两个服务。 不过，SSRS 不是 Azure SQL 数据库的一部分，我们建议在 Azure VM 中运行它，然后将它指向数据库实例。
    
* **我想要改用 PaaS，但我不确定数据库是否兼容。是否可以借助某些工具？**

    是的。 在迁移到 Azure SQL 数据库过程中，可以使用[数据迁移助手](https://www.microsoft.com/download/details.aspx?id=53595)工具。  [Azure 数据库迁移服务](https://azure.microsoft.com/campaigns/database-migration/)是可用于 IaaS 或 PaaS 的预览服务。

* **是否可以估算成本？**

    是的。  可以使用 [Azure 定价计算器](https://azure.microsoft.com/pricing/calculator/)估算所有 Azure 服务（包括 VM 和数据库服务）的成本。
    
## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [选择适当的 Azure 托管选项](dotnet-howto-choose-migration.md)
