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
---
# <a name="migrate-an-aspnet-web-application-to-azure-app-service"></a><span data-ttu-id="f256c-104">将 ASP.NET Web 应用程序迁移到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="f256c-104">Migrate an ASP.NET web application to Azure App Service</span></span>

<span data-ttu-id="f256c-105">[应用服务](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps)是一个完全托管的计算平台服务，非常适合用来托管可缩放的网站和 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f256c-105">[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) is a fully-managed compute platform service that is optimized for hosting scalable websites and web applications.</span></span> <span data-ttu-id="f256c-106">本文档提供有关如何将现有应用程序直接迁移到 Azure 应用服务、要考虑的修改，以及转移到云时所需的其他资源的信息。</span><span class="sxs-lookup"><span data-stu-id="f256c-106">This document provides information on how to lift-and-shift an existing application to Azure App Service, modifications to consider, and additional resources for moving to the cloud.</span></span>

<span data-ttu-id="f256c-107">已准备就绪？</span><span class="sxs-lookup"><span data-stu-id="f256c-107">Ready to get started?</span></span> <span data-ttu-id="f256c-108">[将 ASP.NET + SQL 应用程序发布到 Azure 应用服务](https://go.microsoft.com/fwlink/?linkid=863214)。</span><span class="sxs-lookup"><span data-stu-id="f256c-108">[Publish your ASP.NET + SQL application to Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214).</span></span>

# <a name="preparation"></a><span data-ttu-id="f256c-109">准备工作</span><span class="sxs-lookup"><span data-stu-id="f256c-109">Preparation</span></span>   
* [<span data-ttu-id="f256c-110">如何确定应用是否符合应用服务的条件</span><span class="sxs-lookup"><span data-stu-id="f256c-110">How to determine if your app qualifies for App Service</span></span>](https://azure.microsoft.com/downloads/migration-assistant/)
* [<span data-ttu-id="f256c-111">将数据库转移到云中</span><span class="sxs-lookup"><span data-stu-id="f256c-111">Moving your database to the cloud</span></span>](https://go.microsoft.com/fwlink/?linkid=863217)

# <a name="considerations"></a><span data-ttu-id="f256c-112">注意事项</span><span class="sxs-lookup"><span data-stu-id="f256c-112">Considerations</span></span>
<span data-ttu-id="f256c-113">在迁移应用程序之前，必须考虑几个因素。</span><span class="sxs-lookup"><span data-stu-id="f256c-113">There are several factors you must consider before migrating your application.</span></span> <span data-ttu-id="f256c-114">下面是可能需要对应用程序做出的修改列表，以及如何开始进行这些修改。</span><span class="sxs-lookup"><span data-stu-id="f256c-114">Below is a list of potential modifications you might have to make to your application, and how to go about doing them.</span></span>

## <a name="sql-database-configuration"></a><span data-ttu-id="f256c-115">SQL 数据库配置</span><span class="sxs-lookup"><span data-stu-id="f256c-115">SQL Database configuration</span></span>
<span data-ttu-id="f256c-116">如果应用程序使用本地数据库，则可对 Web 应用使用多个选项。</span><span class="sxs-lookup"><span data-stu-id="f256c-116">If your application is using an on-premises database, you have several options for your web app.</span></span> <span data-ttu-id="f256c-117">[详细了解如何将 SQL 数据库迁移到 Azure](https://go.microsoft.com/fwlink/?linkid=863217)。</span><span class="sxs-lookup"><span data-stu-id="f256c-117">[Read more about migrating SQL databases to Azure](https://go.microsoft.com/fwlink/?linkid=863217).</span></span>

## <a name="iis"></a><span data-ttu-id="f256c-118">IIS</span><span class="sxs-lookup"><span data-stu-id="f256c-118">IIS</span></span>
<span data-ttu-id="f256c-119">以往要在应用程序中通过 applicationHost.config 配置的所有设置现在可以通过 Azure 门户进行配置。</span><span class="sxs-lookup"><span data-stu-id="f256c-119">Everything traditionally configured via applicationHost.config in your application can now be configured through the Azure portal.</span></span> <span data-ttu-id="f256c-120">这适用于 AppPool 位数、启用/禁用 Websocket、托管管道版本、NET Framework 版本 (2.0/4.0)，等等。若要修改[应用程序设置](https://docs.microsoft.com/azure/app-service/web-sites-configure)，请导航到 [Azure 门户](https://portal.azure.com)，打开 Web 应用的边栏选项卡，并选择“应用程序设置”选项卡。</span><span class="sxs-lookup"><span data-stu-id="f256c-120">This applies to AppPool bitness, enable/disable websockets, managed pipeline version, .NET Framework version (2.0/4.0), etc. To modify your [application settings](https://docs.microsoft.com/azure/app-service/web-sites-configure), navigate to the [Azure portal](https://portal.azure.com), open the blade for your web app, and then select the **Application Settings** tab.</span></span>

## <a name="authentication"></a><span data-ttu-id="f256c-121">身份验证</span><span class="sxs-lookup"><span data-stu-id="f256c-121">Authentication</span></span>
<span data-ttu-id="f256c-122">如果应用程序随时要对用户进行身份验证，则你需要修改此功能，以便在 Azure Web 应用中部署应用程序后此功能可正常工作。</span><span class="sxs-lookup"><span data-stu-id="f256c-122">If your application authenticates users at any point, you will have to modify this functionality to work once the application deployed on Azure Web Apps.</span></span> <span data-ttu-id="f256c-123">一种可行的方法是使用 Azure AD Connect 将本地目录与 Azure Active Directory 集成。</span><span class="sxs-lookup"><span data-stu-id="f256c-123">One possibility is to use Azure AD Connect to integrate your on-premises directories with Azure Active Directory.</span></span> <span data-ttu-id="f256c-124">[详细了解如何将本地目录与 Azure Active Directory 集成](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</span><span class="sxs-lookup"><span data-stu-id="f256c-124">[Learn more about how to integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>

## <a name="virtual-network-modification"></a><span data-ttu-id="f256c-125">虚拟网络修改</span><span class="sxs-lookup"><span data-stu-id="f256c-125">Virtual Network Modification</span></span>
<span data-ttu-id="f256c-126">如果使用多个 Azure 服务，可以考虑使用虚拟网络在这些服务之间安全通信。</span><span class="sxs-lookup"><span data-stu-id="f256c-126">If you use more than one Azure service you may consider using a virtual network to securely communicate between these services.</span></span> <span data-ttu-id="f256c-127">可以使用 VPN 或 ExpressRoute 配置从本地网络到 [Azure 虚拟网络](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet)的连接。</span><span class="sxs-lookup"><span data-stu-id="f256c-127">You can configure a connection from your on-premises network to an [Azure Virtual Network](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet) using VPN or ExpressRoute.</span></span>

## <a name="monitoring-and-diagnostics"></a><span data-ttu-id="f256c-128">监视和诊断</span><span class="sxs-lookup"><span data-stu-id="f256c-128">Monitoring and Diagnostics</span></span>
<span data-ttu-id="f256c-129">当前用于监视和诊断的本地解决方案不太可能在云中工作。</span><span class="sxs-lookup"><span data-stu-id="f256c-129">Your current on-premises solutions for monitoring and diagnostics are unlikely to work in the cloud.</span></span> <span data-ttu-id="f256c-130">但是，Azure 提供了日志记录、监视和诊断工具，用于识别和调试 Web 应用的问题。</span><span class="sxs-lookup"><span data-stu-id="f256c-130">However, Azure provides tools for logging, monitoring, and diagnostics so that you can identify and debug issues with web apps.</span></span> <span data-ttu-id="f256c-131">可以轻松地在 Web 应用的配置中为其启用诊断，并可以在 Azure Application Insights 中查看记录的日志。</span><span class="sxs-lookup"><span data-stu-id="f256c-131">You can easily enable diagnostics for your web app in its configuration, and you can view the logs recorded in Azure Application Insights.</span></span> <span data-ttu-id="f256c-132">[详细了解如何为 Web 应用启用诊断日志记录](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log)。</span><span class="sxs-lookup"><span data-stu-id="f256c-132">[Learn more about enabling diagnostics logging for web apps](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).</span></span>

## <a name="connection-strings-and-application-settings"></a><span data-ttu-id="f256c-133">连接字符串和应用程序设置</span><span class="sxs-lookup"><span data-stu-id="f256c-133">Connection Strings and application settings</span></span>
<span data-ttu-id="f256c-134">确保信息安全的方法之一是使用 [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/)，这是一个可以安全存储应用程序中所用敏感信息的服务。</span><span class="sxs-lookup"><span data-stu-id="f256c-134">One option for keeping information safe is to use [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), a service that securely stores sensitive information used in your application.</span></span> <span data-ttu-id="f256c-135">或者，可将此数据存储为应用服务设置。</span><span class="sxs-lookup"><span data-stu-id="f256c-135">Alternatively, you can store this data as an App Service setting.</span></span>

## <a name="dns"></a><span data-ttu-id="f256c-136">DNS</span><span class="sxs-lookup"><span data-stu-id="f256c-136">DNS</span></span>
<span data-ttu-id="f256c-137">可能需要根据应用程序的要求更新 DNS 配置。</span><span class="sxs-lookup"><span data-stu-id="f256c-137">You may need to update DNS configurations based on the requirements of your application.</span></span> <span data-ttu-id="f256c-138">可在应用服务的[自定义域设置](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain)中配置这些 DNS 设置。</span><span class="sxs-lookup"><span data-stu-id="f256c-138">These DNS settings can be configured in the App Service [custom domain settings](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain).</span></span> <span data-ttu-id="f256c-139">要考虑的另一个因素是[绑定现有的自定义 SSL 证书](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl)。</span><span class="sxs-lookup"><span data-stu-id="f256c-139">Another factor to consider is [binding an existing custom SSL certificate](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl).</span></span>

## <a name="file-system-and-storage"></a><span data-ttu-id="f256c-140">文件系统和存储</span><span class="sxs-lookup"><span data-stu-id="f256c-140">File system and Storage</span></span>
<span data-ttu-id="f256c-141">如果应用程序持久保存数据，则需要将其更新为改用 Azure 存储。</span><span class="sxs-lookup"><span data-stu-id="f256c-141">If your application persists data, you will need to update it to use Azure Storage instead.</span></span> <span data-ttu-id="f256c-142">Azure 存储是提供文件共享的服务，可通过 SMB 协议、Blob 存储、简单队列和非关系表共享信息。</span><span class="sxs-lookup"><span data-stu-id="f256c-142">Azure Storage is a service that provides file shares for sharing via SMB protocol, blob storage, simple queues, and non-relational tables.</span></span> <span data-ttu-id="f256c-143">[详细了解 Azure 存储文件共享](https://docs.microsoft.com/azure/storage/files/storage-files-introduction)。</span><span class="sxs-lookup"><span data-stu-id="f256c-143">[Learn more about Azure Storage file shares](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f256c-144">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f256c-144">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f256c-145">将 ASP.NET Web 应用程序迁移到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="f256c-145">Migrate an ASP.NET Web application to Azure App Service</span></span>](https://aka.ms/azure-webapp-migrate)
