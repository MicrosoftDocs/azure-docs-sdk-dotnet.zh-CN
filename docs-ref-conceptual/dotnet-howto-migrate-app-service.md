---
title: 将 .NET Web 应用或服务迁移到 Azure 应用服务
description: 了解如何将 .NET Web 应用或服务从本地迁移到 Azure 应用服务。
keywords: Azure .NET, ASP.NET, WCF, 应用服务, Web 应用, 迁移
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 07/16/2018
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter
ms.openlocfilehash: 643d758af8f90f22791d3b7deb18ae6233067ef0
ms.sourcegitcommit: 779c1b202d3670cfa0b9428c89f830cad9ec7e9d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39135715"
---
# <a name="migrate-your-net-web-app-or-service-to-azure-app-service"></a><span data-ttu-id="e96fd-104">将 .NET Web 应用或服务迁移到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="e96fd-104">Migrate your .NET web app or service to Azure App Service</span></span> 

<span data-ttu-id="e96fd-105">[应用服务](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps)是一个完全托管的计算平台服务，非常适合用来托管可缩放的网站和 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e96fd-105">[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) is a fully-managed compute platform service that is optimized for hosting scalable websites and web applications.</span></span> <span data-ttu-id="e96fd-106">本文档提供有关如何将现有应用程序直接迁移到 Azure 应用服务、要考虑的修改，以及转移到云时所需的其他资源的信息。</span><span class="sxs-lookup"><span data-stu-id="e96fd-106">This document provides information on how to lift-and-shift an existing application to Azure App Service, modifications to consider, and additional resources for moving to the cloud.</span></span> <span data-ttu-id="e96fd-107">大多数 ASP.NET 网站（Webforms、MVC）和服务（Web API、WCF）可以直接移到 Azure 应用服务而无需进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="e96fd-107">Most ASP.NET websites (Webforms, MVC) and services (Web API, WCF) can move directly to Azure App Service with no changes.</span></span> <span data-ttu-id="e96fd-108">有些可能需要进行少量更改，而有些可能需要进行一些重构。</span><span class="sxs-lookup"><span data-stu-id="e96fd-108">Some may need minor changes while others may need some refactoring.</span></span>

<span data-ttu-id="e96fd-109">已准备就绪？</span><span class="sxs-lookup"><span data-stu-id="e96fd-109">Ready to get started?</span></span> <span data-ttu-id="e96fd-110">[将 ASP.NET + SQL 应用程序发布到 Azure 应用服务](https://go.microsoft.com/fwlink/?linkid=863214)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-110">[Publish your ASP.NET + SQL application to Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214).</span></span>

## <a name="considerations"></a><span data-ttu-id="e96fd-111">注意事项</span><span class="sxs-lookup"><span data-stu-id="e96fd-111">Considerations</span></span>

### <a name="on-premises-resources-including-sql-server"></a><span data-ttu-id="e96fd-112">本地资源（包括 SQL Server）</span><span class="sxs-lookup"><span data-stu-id="e96fd-112">On-premises resources (including SQL Server)</span></span>

<span data-ttu-id="e96fd-113">验证对本地资源的访问权限，因为这些资源可能需要进行迁移或更改。</span><span class="sxs-lookup"><span data-stu-id="e96fd-113">Verify access to on-premises resources as these may need to be migrated or changed.</span></span> <span data-ttu-id="e96fd-114">以下是用于减轻对本地资源的访问的选项：</span><span class="sxs-lookup"><span data-stu-id="e96fd-114">The following are options for mitigating access to on-premises resources:</span></span>

* <span data-ttu-id="e96fd-115">使用 [Azure 虚拟网络](https://docs.microsoft.com/en-us/azure/app-service/web-sites-integrate-with-vnet)创建将应用服务连接到本地资源的 VPN。</span><span class="sxs-lookup"><span data-stu-id="e96fd-115">Create a VPN connecting App Service to on-premises resources using [Azure Virtual Networks](https://docs.microsoft.com/en-us/azure/app-service/web-sites-integrate-with-vnet).</span></span>
* <span data-ttu-id="e96fd-116">使用 [Azure 中继](https://docs.microsoft.com/en-us/azure/service-bus-relay/relay-what-is-it)，在不更改防火墙的情况下，将本地服务安全地公开给云。</span><span class="sxs-lookup"><span data-stu-id="e96fd-116">Securely expose on-premises services to the cloud without firewall changes using [Azure Relay](https://docs.microsoft.com/en-us/azure/service-bus-relay/relay-what-is-it).</span></span>
* <span data-ttu-id="e96fd-117">将依赖项（如 [SQL 数据库](https://go.microsoft.com/fwlink/?linkid=863217)）迁移到 Azure。</span><span class="sxs-lookup"><span data-stu-id="e96fd-117">Migrate dependencies such as a [SQL database](https://go.microsoft.com/fwlink/?linkid=863217) to Azure.</span></span>
* <span data-ttu-id="e96fd-118">在云中使用平台即服务产品/服务以减少依赖项。</span><span class="sxs-lookup"><span data-stu-id="e96fd-118">Use platform-as-a-service offerings in the cloud to reduce dependecies.</span></span> <span data-ttu-id="e96fd-119">例如，不要连接到本地邮件服务器，而应考虑使用 [SendGrid](https://docs.microsoft.com/en-us/azure/sendgrid-dotnet-how-to-send-email)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-119">For example, rather than connect to an on-premises mail server, consider using [SendGrid](https://docs.microsoft.com/en-us/azure/sendgrid-dotnet-how-to-send-email).</span></span> 

### <a name="port-bindings"></a><span data-ttu-id="e96fd-120">端口绑定</span><span class="sxs-lookup"><span data-stu-id="e96fd-120">Port Bindings</span></span>

<span data-ttu-id="e96fd-121">Azure 应用服务仅支持用于 HTTP 的端口 80 和用于 HTTPS 通信的端口 443。</span><span class="sxs-lookup"><span data-stu-id="e96fd-121">Azure App Service supports port 80 for HTTP and port 443 for HTTPS traffic.</span></span>

<span data-ttu-id="e96fd-122">对于 WCF，支持以下绑定：</span><span class="sxs-lookup"><span data-stu-id="e96fd-122">For WCF, the following bindings are supported:</span></span>

<span data-ttu-id="e96fd-123">绑定</span><span class="sxs-lookup"><span data-stu-id="e96fd-123">Binding</span></span> | <span data-ttu-id="e96fd-124">说明</span><span class="sxs-lookup"><span data-stu-id="e96fd-124">Notes</span></span>
--------|--------
<span data-ttu-id="e96fd-125">BasicHttp</span><span class="sxs-lookup"><span data-stu-id="e96fd-125">BasicHttp</span></span> | 
<span data-ttu-id="e96fd-126">WSHttp</span><span class="sxs-lookup"><span data-stu-id="e96fd-126">WSHttp</span></span> | 
<span data-ttu-id="e96fd-127">WSDualHttpBinding</span><span class="sxs-lookup"><span data-stu-id="e96fd-127">WSDualHttpBinding</span></span> | <span data-ttu-id="e96fd-128">必须启用 [Web 套接字支持](https://docs.microsoft.com/azure/app-service/web-sites-configure)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-128">[Web socket support](https://docs.microsoft.com/azure/app-service/web-sites-configure) must be enabled.</span></span>
<span data-ttu-id="e96fd-129">NetHttpBinding</span><span class="sxs-lookup"><span data-stu-id="e96fd-129">NetHttpBinding</span></span> | <span data-ttu-id="e96fd-130">必须为双工协定启用 [Web 套接字支持](https://docs.microsoft.com/azure/app-service/web-sites-configure)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-130">[Web socket support](https://docs.microsoft.com/azure/app-service/web-sites-configure) must be enabled for duplex contracts.</span></span>
<span data-ttu-id="e96fd-131">NetHttpsBinding</span><span class="sxs-lookup"><span data-stu-id="e96fd-131">NetHttpsBinding</span></span> | <span data-ttu-id="e96fd-132">必须为双工协定启用 [Web 套接字支持](https://docs.microsoft.com/azure/app-service/web-sites-configure)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-132">[Web socket support](https://docs.microsoft.com/azure/app-service/web-sites-configure) must be enabled for duplex contracts.</span></span>
<span data-ttu-id="e96fd-133">BasicHttpContextBinding</span><span class="sxs-lookup"><span data-stu-id="e96fd-133">BasicHttpContextBinding</span></span> |
<span data-ttu-id="e96fd-134">WebHttpBinding</span><span class="sxs-lookup"><span data-stu-id="e96fd-134">WebHttpBinding</span></span> |
<span data-ttu-id="e96fd-135">WSHttpContextBinding</span><span class="sxs-lookup"><span data-stu-id="e96fd-135">WSHttpContextBinding</span></span> |

### <a name="authentication"></a><span data-ttu-id="e96fd-136">身份验证</span><span class="sxs-lookup"><span data-stu-id="e96fd-136">Authentication</span></span>

<span data-ttu-id="e96fd-137">Azure 应用服务默认支持匿名身份验证，并在需要时进行表单验证。</span><span class="sxs-lookup"><span data-stu-id="e96fd-137">Azure App Service supports anonymous authentication by default and Forms authentication when intended.</span></span> <span data-ttu-id="e96fd-138">Windows 身份验证仅可通过集成 Azure Active Directory 和 ADFS 加以使用。</span><span class="sxs-lookup"><span data-stu-id="e96fd-138">Windows authentication can be used by integrating with Azure Active Directory and ADFS only.</span></span> <span data-ttu-id="e96fd-139">[详细了解如何将本地目录与 Azure Active Directory 集成](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-139">[Learn more about how to integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>

### <a name="assemblies-in-the-gac-global-assembly-cache"></a><span data-ttu-id="e96fd-140">GAC（全局程序集缓存）中的程序集</span><span class="sxs-lookup"><span data-stu-id="e96fd-140">Assemblies in the GAC (Global Assembly Cache)</span></span> 

<span data-ttu-id="e96fd-141">不支持此操作。</span><span class="sxs-lookup"><span data-stu-id="e96fd-141">This isn't supported.</span></span> <span data-ttu-id="e96fd-142">请考虑将所需程序集复制到应用的 `\bin` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e96fd-142">Consider copying required assemblies to the app's `\bin` folder.</span></span> <span data-ttu-id="e96fd-143">不能使用安装在服务器上的自定义 .MSI（例如 PDF 生成器等）。</span><span class="sxs-lookup"><span data-stu-id="e96fd-143">Custom .MSIs installed on the server (e.g. PDF generators, etc.) cannot be used.</span></span>  

### <a name="iis-settings"></a><span data-ttu-id="e96fd-144">IIS 设置</span><span class="sxs-lookup"><span data-stu-id="e96fd-144">IIS settings</span></span>
<span data-ttu-id="e96fd-145">以往要在应用程序中通过 applicationHost.config 配置的所有设置现在可以通过 Azure 门户进行配置。</span><span class="sxs-lookup"><span data-stu-id="e96fd-145">Everything traditionally configured via applicationHost.config in your application can now be configured through the Azure portal.</span></span> <span data-ttu-id="e96fd-146">这适用于 AppPool 位数、启用/禁用 Websocket、托管管道版本、NET Framework 版本 (2.0/4.0)，等等。若要修改[应用程序设置](https://docs.microsoft.com/azure/app-service/web-sites-configure)，请导航到 [Azure 门户](https://portal.azure.com)，打开 Web 应用的边栏选项卡，并选择“应用程序设置”选项卡。</span><span class="sxs-lookup"><span data-stu-id="e96fd-146">This applies to AppPool bitness, enable/disable websockets, managed pipeline version, .NET Framework version (2.0/4.0), etc. To modify your [application settings](https://docs.microsoft.com/azure/app-service/web-sites-configure), navigate to the [Azure portal](https://portal.azure.com), open the blade for your web app, and then select the **Application Settings** tab.</span></span>

#### <a name="iis5-compatibility-mode"></a><span data-ttu-id="e96fd-147">IIS5 兼容模式</span><span class="sxs-lookup"><span data-stu-id="e96fd-147">IIS5 Compatibility Mode</span></span>
<span data-ttu-id="e96fd-148">不支持 IIS5 兼容模式。</span><span class="sxs-lookup"><span data-stu-id="e96fd-148">IIS5 Compatibility Mode is not supported.</span></span> <span data-ttu-id="e96fd-149">在 Azure 应用服务中，每个 Web 应用及其下的所有应用程序都在具有一组特定[应用程序池](http://technet.microsoft.com/en-us/library/cc735247(v=WS.10).aspx)的同一工作进程中运行。</span><span class="sxs-lookup"><span data-stu-id="e96fd-149">In Azure App Service each Web App and all of the applications under it run in the same worker process with a specific set of [application pool](http://technet.microsoft.com/en-us/library/cc735247(v=WS.10).aspx).</span></span>

#### <a name="iis7-schema-compliance"></a><span data-ttu-id="e96fd-150">IIS7+ 架构符合性</span><span class="sxs-lookup"><span data-stu-id="e96fd-150">IIS7+ schema compliance</span></span>  
<span data-ttu-id="e96fd-151">Azure 应用服务 IIS 架构中未定义一些元素和属性。</span><span class="sxs-lookup"><span data-stu-id="e96fd-151">Some elements and attributes are not defined in the Azure App Service IIS schema.</span></span> <span data-ttu-id="e96fd-152">如果遇到问题，请考虑使用 [XDT 转换](http://azure.microsoft.com/documentation/articles/web-sites-transform-extend/)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-152">If you encounter issues, consider using [XDT transforms](http://azure.microsoft.com/documentation/articles/web-sites-transform-extend/).</span></span>

#### <a name="single-application-pool-per-site"></a><span data-ttu-id="e96fd-153">每个站点的单个应用程序池</span><span class="sxs-lookup"><span data-stu-id="e96fd-153">Single application pool per site</span></span>  
<span data-ttu-id="e96fd-154">在 Azure 应用服务中，每个 Web 应用及其下的所有应用程序都在同一个应用程序池中运行。</span><span class="sxs-lookup"><span data-stu-id="e96fd-154">In Azure App Service each Web App and all of the applications under it run in the same application pool.</span></span> <span data-ttu-id="e96fd-155">请考虑使用通用设置建立单个应用程序池，或为每个应用程序创建单独的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="e96fd-155">Consider establishing a single application pool with common settings or creating a separate Web App for each application.</span></span>

### <a name="com-and-com-components"></a><span data-ttu-id="e96fd-156">COM 和 COM+ 组件</span><span class="sxs-lookup"><span data-stu-id="e96fd-156">COM and COM+ components</span></span>  
<span data-ttu-id="e96fd-157">Azure 应用服务不允许在平台上注册 COM 组件。</span><span class="sxs-lookup"><span data-stu-id="e96fd-157">Azure App Service does not allow the registration of COM components on the platform.</span></span> <span data-ttu-id="e96fd-158">如果你的应用使用任何 COM 组件，则需要在托管代码中重写这些组件并将其与站点或应用程序一起部署。</span><span class="sxs-lookup"><span data-stu-id="e96fd-158">If your app makes use of any COM components, these would need to be rewritten in managed code and deployed with the site or application.</span></span>  

### <a name="physical-directories"></a><span data-ttu-id="e96fd-159">物理目录</span><span class="sxs-lookup"><span data-stu-id="e96fd-159">Physical directories</span></span> 
<span data-ttu-id="e96fd-160">Azure 应用服务不允许访问物理驱动器。</span><span class="sxs-lookup"><span data-stu-id="e96fd-160">Azure App Service does not allow physical drive access.</span></span> <span data-ttu-id="e96fd-161">可能需要使用 [Azure 文件](https://docs.microsoft.com/azure/storage/files/storage-files-introduction)通过 SMB 访问文件。</span><span class="sxs-lookup"><span data-stu-id="e96fd-161">You may need to use a [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) to access files via SMB.</span></span> <span data-ttu-id="e96fd-162">[Azure Blob存储](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction)可以存储文件以通过 HTTPS 进行访问。</span><span class="sxs-lookup"><span data-stu-id="e96fd-162">[Azure Blob Storage](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction) can store files for access via HTTPS.</span></span>  

### <a name="isapi-filters"></a><span data-ttu-id="e96fd-163">ISAPI 筛选器</span><span class="sxs-lookup"><span data-stu-id="e96fd-163">ISAPI Filters</span></span>  
<span data-ttu-id="e96fd-164">Azure 应用服务可以支持使用 ISAPI 筛选器，但是，ISAPI DLL 必须与站点一起部署并通过 web.config 注册。</span><span class="sxs-lookup"><span data-stu-id="e96fd-164">Azure App Service can support the use of ISAPI Filters, however, the ISAPI DLL must be deployed with your site and registered via web.config.</span></span>  

### <a name="https-bindings-and-ssl"></a><span data-ttu-id="e96fd-165">HTTPS 绑定和 SSL</span><span class="sxs-lookup"><span data-stu-id="e96fd-165">HTTPS bindings and SSL</span></span> 
<span data-ttu-id="e96fd-166">将不会迁移 HTTPS 绑定，也不会迁移与网站关联的 SSL 证书。</span><span class="sxs-lookup"><span data-stu-id="e96fd-166">HTTPS bindings will not be migrated, nor will the SSL certificates associated with your web sites.</span></span> <span data-ttu-id="e96fd-167">但是，在完成站点迁移后，[可以手动上传 SSL证书](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-167">[SSL certificates can be manually uploaded](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl) after site migration is completed, however.</span></span>  

### <a name="sharepoint-and-frontpage"></a><span data-ttu-id="e96fd-168">SharePoint 和 FrontPage</span><span class="sxs-lookup"><span data-stu-id="e96fd-168">SharePoint and FrontPage</span></span> 
<span data-ttu-id="e96fd-169">不支持 SharePoint 和 FrontPage 服务器扩展 (FPSE)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-169">SharePoint and FrontPage Server Extensions (FPSE) are not supported.</span></span>

### <a name="web-site-size"></a><span data-ttu-id="e96fd-170">网站大小</span><span class="sxs-lookup"><span data-stu-id="e96fd-170">Web site size</span></span>  
<span data-ttu-id="e96fd-171">免费站点的内容大小限制为 1 GB。</span><span class="sxs-lookup"><span data-stu-id="e96fd-171">Free sites have a size limit of 1 GB of content.</span></span> <span data-ttu-id="e96fd-172">如果你的站点大于 1 GB，则必须升级到付费 SKU。</span><span class="sxs-lookup"><span data-stu-id="e96fd-172">If your site is greater than 1 GB, you must upgrade to a paid SKU.</span></span> <span data-ttu-id="e96fd-173">请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/windows/)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-173">See [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/windows/).</span></span> 

### <a name="database-size"></a><span data-ttu-id="e96fd-174">数据库大小</span><span class="sxs-lookup"><span data-stu-id="e96fd-174">Database size</span></span>  
<span data-ttu-id="e96fd-175">对于 SQL Server 数据库，请检查当前 [SQL 数据库定价](http://azure.microsoft.com/pricing/details/sql-database)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-175">For SQL Server databases, please check the current [SQL Database pricing](http://azure.microsoft.com/pricing/details/sql-database).</span></span>  

### <a name="azure-active-directory-aad-integration"></a><span data-ttu-id="e96fd-176">Azure Active Directory (AAD) 集成</span><span class="sxs-lookup"><span data-stu-id="e96fd-176">Azure Active Directory (AAD) integration</span></span>  
<span data-ttu-id="e96fd-177">AAD 不适用于免费应用。</span><span class="sxs-lookup"><span data-stu-id="e96fd-177">AAD does not work with free apps.</span></span> <span data-ttu-id="e96fd-178">若要使用 AAD，必须升级应用 SKU。</span><span class="sxs-lookup"><span data-stu-id="e96fd-178">To use AAD, you must upgrade the app SKU.</span></span> <span data-ttu-id="e96fd-179">请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/windows/)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-179">See [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/windows/).</span></span>

### <a name="monitoring-and-diagnostics"></a><span data-ttu-id="e96fd-180">监视和诊断</span><span class="sxs-lookup"><span data-stu-id="e96fd-180">Monitoring and Diagnostics</span></span>
<span data-ttu-id="e96fd-181">当前用于监视和诊断的本地解决方案不太可能在云中工作。</span><span class="sxs-lookup"><span data-stu-id="e96fd-181">Your current on-premises solutions for monitoring and diagnostics are unlikely to work in the cloud.</span></span> <span data-ttu-id="e96fd-182">但是，Azure 提供了日志记录、监视和诊断工具，用于识别和调试 Web 应用的问题。</span><span class="sxs-lookup"><span data-stu-id="e96fd-182">However, Azure provides tools for logging, monitoring, and diagnostics so that you can identify and debug issues with web apps.</span></span> <span data-ttu-id="e96fd-183">可以轻松地在 Web 应用的配置中为其启用诊断，并可以在 Azure Application Insights 中查看记录的日志。</span><span class="sxs-lookup"><span data-stu-id="e96fd-183">You can easily enable diagnostics for your web app in its configuration, and you can view the logs recorded in Azure Application Insights.</span></span> <span data-ttu-id="e96fd-184">[详细了解如何为 Web 应用启用诊断日志记录](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log)。</span><span class="sxs-lookup"><span data-stu-id="e96fd-184">[Learn more about enabling diagnostics logging for web apps](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).</span></span>

### <a name="connection-strings-and-application-settings"></a><span data-ttu-id="e96fd-185">连接字符串和应用程序设置</span><span class="sxs-lookup"><span data-stu-id="e96fd-185">Connection Strings and application settings</span></span>
<span data-ttu-id="e96fd-186">请考虑使用 [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/)，这是一个可安全存储应用程序中使用的敏感信息的服务。</span><span class="sxs-lookup"><span data-stu-id="e96fd-186">Consider using [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), a service that securely stores sensitive information used in your application.</span></span> <span data-ttu-id="e96fd-187">或者，可将此数据存储为应用服务设置。</span><span class="sxs-lookup"><span data-stu-id="e96fd-187">Alternatively, you can store this data as an App Service setting.</span></span>

### <a name="dns"></a><span data-ttu-id="e96fd-188">DNS</span><span class="sxs-lookup"><span data-stu-id="e96fd-188">DNS</span></span>
<span data-ttu-id="e96fd-189">可能需要根据应用程序的要求更新 DNS 配置。</span><span class="sxs-lookup"><span data-stu-id="e96fd-189">You may need to update DNS configurations based on the requirements of your application.</span></span> <span data-ttu-id="e96fd-190">可在应用服务的[自定义域设置](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain)中配置这些 DNS 设置。</span><span class="sxs-lookup"><span data-stu-id="e96fd-190">These DNS settings can be configured in the App Service [custom domain settings](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain).</span></span> 

## <a name="azure-app-service-with-windows-containers"></a><span data-ttu-id="e96fd-191">使用 Windows 容器的 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="e96fd-191">Azure App Service with Windows Containers</span></span>
<span data-ttu-id="e96fd-192">如果你的应用无法直接迁移到应用服务，请考虑使用 Windows 容器的应用服务，这样可以使用 GAC、COM 组件、MSI，完全访问.NET FX API、DirectX 等。</span><span class="sxs-lookup"><span data-stu-id="e96fd-192">If your app cannot be migrated directly to App Service, consider App Service using Windows Containers, which enables usage of the GAC, COM components, MSIs, full access to .NET FX APIs, DirectX, and more.</span></span>

## <a name="additional-reading"></a><span data-ttu-id="e96fd-193">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="e96fd-193">Additional Reading</span></span>

* [<span data-ttu-id="e96fd-194">如何确定应用是否符合应用服务的条件</span><span class="sxs-lookup"><span data-stu-id="e96fd-194">How to determine if your app qualifies for App Service</span></span>](https://azure.microsoft.com/downloads/migration-assistant/)
* [<span data-ttu-id="e96fd-195">将数据库转移到云中</span><span class="sxs-lookup"><span data-stu-id="e96fd-195">Moving your database to the cloud</span></span>](https://go.microsoft.com/fwlink/?linkid=863217)
* [<span data-ttu-id="e96fd-196">Azure Web 应用沙盒的详细信息和限制</span><span class="sxs-lookup"><span data-stu-id="e96fd-196">Azure Web App sandbox details and restrictions</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)

## <a name="next-steps"></a><span data-ttu-id="e96fd-197">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e96fd-197">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e96fd-198">将 ASP.NET Web 应用程序迁移到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="e96fd-198">Migrate an ASP.NET Web application to Azure App Service</span></span>](https://aka.ms/azure-webapp-migrate)
