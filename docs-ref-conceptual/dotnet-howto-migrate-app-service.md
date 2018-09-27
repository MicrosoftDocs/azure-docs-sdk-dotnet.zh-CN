---
title: 将 .NET Web 应用或服务迁移到 Azure 应用服务
description: 了解如何将 .NET Web 应用或服务从本地迁移到 Azure 应用服务。
ms.date: 08/11/2018
ms.service: app-service
ms.openlocfilehash: cee1745f64a575836bbf54eca435ba19b508f94c
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190730"
---
# <a name="migrate-your-net-web-app-or-service-to-azure-app-service"></a>将 .NET Web 应用或服务迁移到 Azure 应用服务 

[应用服务](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps)是一个完全托管的计算平台服务，非常适合用来托管可缩放的网站和 Web 应用程序。 本文档提供有关如何将现有应用程序直接迁移到 Azure 应用服务、要考虑的修改，以及转移到云时所需的其他资源的信息。 大多数 ASP.NET 网站（Webforms、MVC）和服务（Web API、WCF）可以直接移到 Azure 应用服务而无需进行任何更改。 有些可能需要进行少量更改，而有些可能需要进行一些重构。

已准备就绪？ [将 ASP.NET + SQL 应用程序发布到 Azure 应用服务](https://go.microsoft.com/fwlink/?linkid=863214)。

## <a name="considerations"></a>注意事项

### <a name="on-premises-resources-including-sql-server"></a>本地资源（包括 SQL Server）

验证对本地资源的访问权限，因为这些资源可能需要进行迁移或更改。 以下是用于减轻对本地资源的访问的选项：

* 使用 [Azure 虚拟网络](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet)创建将应用服务连接到本地资源的 VPN。
* 使用 [Azure 中继](https://docs.microsoft.com/azure/service-bus-relay/relay-what-is-it)，在不更改防火墙的情况下，将本地服务安全地公开给云。
* 将依赖项（如 [SQL 数据库](https://go.microsoft.com/fwlink/?linkid=863217)）迁移到 Azure。
* 在云中使用平台即服务产品/服务以减少依赖项。 例如，不要连接到本地邮件服务器，而应考虑使用 [SendGrid](https://docs.microsoft.com/azure/sendgrid-dotnet-how-to-send-email)。 

### <a name="port-bindings"></a>端口绑定

Azure 应用服务仅支持用于 HTTP 的端口 80 和用于 HTTPS 通信的端口 443。

对于 WCF，支持以下绑定：

绑定 | 说明
--------|--------
BasicHttp | 
WSHttp | 
WSDualHttpBinding | 必须启用 [Web 套接字支持](https://docs.microsoft.com/azure/app-service/web-sites-configure)。
NetHttpBinding | 必须为双工协定启用 [Web 套接字支持](https://docs.microsoft.com/azure/app-service/web-sites-configure)。
NetHttpsBinding | 必须为双工协定启用 [Web 套接字支持](https://docs.microsoft.com/azure/app-service/web-sites-configure)。
BasicHttpContextBinding |
WebHttpBinding |
WSHttpContextBinding |

### <a name="authentication"></a>身份验证

Azure 应用服务默认支持匿名身份验证，并在需要时进行表单验证。 Windows 身份验证仅可通过集成 Azure Active Directory 和 ADFS 加以使用。 [详细了解如何将本地目录与 Azure Active Directory 集成](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。

### <a name="assemblies-in-the-gac-global-assembly-cache"></a>GAC（全局程序集缓存）中的程序集 

不支持此操作。 请考虑将所需程序集复制到应用的 `\bin` 文件夹。 不能使用安装在服务器上的自定义 .MSI（例如 PDF 生成器等）。  

### <a name="iis-settings"></a>IIS 设置
以往要在应用程序中通过 applicationHost.config 配置的所有设置现在可以通过 Azure 门户进行配置。 这适用于 AppPool 位数、启用/禁用 Websocket、托管管道版本、NET Framework 版本 (2.0/4.0)，等等。若要修改[应用程序设置](https://docs.microsoft.com/azure/app-service/web-sites-configure)，请导航到 [Azure 门户](https://portal.azure.com)，打开 Web 应用的边栏选项卡，并选择“应用程序设置”选项卡。

#### <a name="iis5-compatibility-mode"></a>IIS5 兼容模式
不支持 IIS5 兼容模式。 在 Azure 应用服务中，每个 Web 应用及其下的所有应用程序都在具有一组特定[应用程序池](http://technet.microsoft.com/library/cc735247(v=WS.10).aspx)的同一工作进程中运行。

#### <a name="iis7-schema-compliance"></a>IIS7+ 架构符合性  
Azure 应用服务 IIS 架构中未定义一些元素和属性。 如果遇到问题，请考虑使用 [XDT 转换](http://azure.microsoft.com/documentation/articles/web-sites-transform-extend/)。

#### <a name="single-application-pool-per-site"></a>每个站点的单个应用程序池  
在 Azure 应用服务中，每个 Web 应用及其下的所有应用程序都在同一个应用程序池中运行。 请考虑使用通用设置建立单个应用程序池，或为每个应用程序创建单独的 Web 应用。

### <a name="com-and-com-components"></a>COM 和 COM+ 组件  
Azure 应用服务不允许在平台上注册 COM 组件。 如果你的应用使用任何 COM 组件，则需要在托管代码中重写这些组件并将其与站点或应用程序一起部署。  

### <a name="physical-directories"></a>物理目录 
Azure 应用服务不允许访问物理驱动器。 可能需要使用 [Azure 文件](https://docs.microsoft.com/azure/storage/files/storage-files-introduction)通过 SMB 访问文件。 [Azure Blob存储](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction)可以存储文件以通过 HTTPS 进行访问。  

### <a name="isapi-filters"></a>ISAPI 筛选器  
Azure 应用服务可以支持使用 ISAPI 筛选器，但是，ISAPI DLL 必须与站点一起部署并通过 web.config 注册。  

### <a name="https-bindings-and-ssl"></a>HTTPS 绑定和 SSL 
将不会迁移 HTTPS 绑定，也不会迁移与网站关联的 SSL 证书。 但是，在完成站点迁移后，[可以手动上传 SSL证书](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl)。  

### <a name="sharepoint-and-frontpage"></a>SharePoint 和 FrontPage 
不支持 SharePoint 和 FrontPage 服务器扩展 (FPSE)。

### <a name="web-site-size"></a>网站大小  
免费站点的内容大小限制为 1 GB。 如果你的站点大于 1 GB，则必须升级到付费 SKU。 请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/windows/)。 

### <a name="database-size"></a>数据库大小  
对于 SQL Server 数据库，请检查当前 [SQL 数据库定价](http://azure.microsoft.com/pricing/details/sql-database)。  

### <a name="azure-active-directory-aad-integration"></a>Azure Active Directory (AAD) 集成  
AAD 不适用于免费应用。 若要使用 AAD，必须升级应用 SKU。 请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/windows/)。

### <a name="monitoring-and-diagnostics"></a>监视和诊断
当前用于监视和诊断的本地解决方案不太可能在云中工作。 但是，Azure 提供了日志记录、监视和诊断工具，用于识别和调试 Web 应用的问题。 可以轻松地在 Web 应用的配置中为其启用诊断，并可以在 Azure Application Insights 中查看记录的日志。 [详细了解如何为 Web 应用启用诊断日志记录](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log)。

### <a name="connection-strings-and-application-settings"></a>连接字符串和应用程序设置
请考虑使用 [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/)，这是一个可安全存储应用程序中使用的敏感信息的服务。 或者，可将此数据存储为应用服务设置。

### <a name="dns"></a>DNS
可能需要根据应用程序的要求更新 DNS 配置。 可在应用服务的[自定义域设置](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain)中配置这些 DNS 设置。 

## <a name="azure-app-service-with-windows-containers"></a>使用 Windows 容器的 Azure 应用服务
如果你的应用无法直接迁移到应用服务，请考虑使用 Windows 容器的应用服务，这样可以使用 GAC、COM 组件、MSI，完全访问.NET FX API、DirectX 等。

## <a name="additional-reading"></a>其他阅读材料

* [如何确定应用是否符合应用服务的条件](https://azure.microsoft.com/downloads/migration-assistant/)
* [将数据库转移到云中](https://go.microsoft.com/fwlink/?linkid=863217)
* [Azure Web 应用沙盒的详细信息和限制](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [从 Visual Studio 部署应用](https://docs.microsoft.com/visualstudio/deployment/quickstart-deploy-to-azure?view=vs-2017)
