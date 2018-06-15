---
title: 将 ASP.NET Web 应用程序迁移到 Azure 应用服务
description: 了解如何将 ASP.NET Web 应用程序从本地迁移到 Azure 应用服务。
keywords: Azure .NET, ASP.NET, 应用服务, Web 应用, 迁移
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter
ms.openlocfilehash: 050782871c3fe4ccb0d15bf9933c3b11c88ce661
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
ms.locfileid: "29728418"
---
# <a name="migrate-an-aspnet-web-application-to-azure-app-service"></a>将 ASP.NET Web 应用程序迁移到 Azure 应用服务

[应用服务](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps)是一个完全托管的计算平台服务，非常适合用来托管可缩放的网站和 Web 应用程序。 本文档提供有关如何将现有应用程序直接迁移到 Azure 应用服务、要考虑的修改，以及转移到云时所需的其他资源的信息。

已准备就绪？ [将 ASP.NET + SQL 应用程序发布到 Azure 应用服务](https://go.microsoft.com/fwlink/?linkid=863214)。

# <a name="preparation"></a>准备工作   
* [如何确定应用是否符合应用服务的条件](https://azure.microsoft.com/downloads/migration-assistant/)
* [将数据库转移到云中](https://go.microsoft.com/fwlink/?linkid=863217)

# <a name="considerations"></a>注意事项
在迁移应用程序之前，必须考虑几个因素。 下面是可能需要对应用程序做出的修改列表，以及如何开始进行这些修改。

## <a name="sql-database-configuration"></a>SQL 数据库配置
如果应用程序使用本地数据库，则可对 Web 应用使用多个选项。 [详细了解如何将 SQL 数据库迁移到 Azure](https://go.microsoft.com/fwlink/?linkid=863217)。

## <a name="iis"></a>IIS
以往要在应用程序中通过 applicationHost.config 配置的所有设置现在可以通过 Azure 门户进行配置。 这适用于 AppPool 位数、启用/禁用 Websocket、托管管道版本、NET Framework 版本 (2.0/4.0)，等等。若要修改[应用程序设置](https://docs.microsoft.com/azure/app-service/web-sites-configure)，请导航到 [Azure 门户](https://portal.azure.com)，打开 Web 应用的边栏选项卡，并选择“应用程序设置”选项卡。

## <a name="authentication"></a>身份验证
如果应用程序随时要对用户进行身份验证，则你需要修改此功能，以便在 Azure Web 应用中部署应用程序后此功能可正常工作。 一种可行的方法是使用 Azure AD Connect 将本地目录与 Azure Active Directory 集成。 [详细了解如何将本地目录与 Azure Active Directory 集成](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。

## <a name="virtual-network-modification"></a>虚拟网络修改
如果使用多个 Azure 服务，可以考虑使用虚拟网络在这些服务之间安全通信。 可以使用 VPN 或 ExpressRoute 配置从本地网络到 [Azure 虚拟网络](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet)的连接。

## <a name="monitoring-and-diagnostics"></a>监视和诊断
当前用于监视和诊断的本地解决方案不太可能在云中工作。 但是，Azure 提供了日志记录、监视和诊断工具，用于识别和调试 Web 应用的问题。 可以轻松地在 Web 应用的配置中为其启用诊断，并可以在 Azure Application Insights 中查看记录的日志。 [详细了解如何为 Web 应用启用诊断日志记录](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log)。

## <a name="connection-strings-and-application-settings"></a>连接字符串和应用程序设置
确保信息安全的方法之一是使用 [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/)，这是一个可以安全存储应用程序中所用敏感信息的服务。 或者，可将此数据存储为应用服务设置。

## <a name="dns"></a>DNS
可能需要根据应用程序的要求更新 DNS 配置。 可在应用服务的[自定义域设置](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain)中配置这些 DNS 设置。 要考虑的另一个因素是[绑定现有的自定义 SSL 证书](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl)。

## <a name="file-system-and-storage"></a>文件系统和存储
如果应用程序持久保存数据，则需要将其更新为改用 Azure 存储。 Azure 存储是提供文件共享的服务，可通过 SMB 协议、Blob 存储、简单队列和非关系表共享信息。 [详细了解 Azure 存储文件共享](https://docs.microsoft.com/azure/storage/files/storage-files-introduction)。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [将 ASP.NET Web 应用程序迁移到 Azure 应用服务](https://aka.ms/azure-webapp-migrate)
