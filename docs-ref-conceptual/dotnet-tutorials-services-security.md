---
title: "有关保护 Azure 应用的 .NET 教程"
description: "有关 Azure 上运行的 .NET 应用的应用程序安全和标识管理的教程。"
author: camsoper
manager: douge
ms.devlang: dotnet
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 06/09/2017
ms.author: casoper
ms.openlocfilehash: 1ac3b8168f8c2b11082536b635fc32b607354711
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a><span data-ttu-id="ea249-103">有关在 Azure 上运行的 .NET 应用中对用户进行身份验证的教程</span><span class="sxs-lookup"><span data-stu-id="ea249-103">Tutorials for authenticating users in your .NET apps running on Azure</span></span>

<span data-ttu-id="ea249-104">下表提供了有关验证用户身份以及保护 Azure 上运行的 .NET 应用程序的深入教程的链接。</span><span class="sxs-lookup"><span data-stu-id="ea249-104">The following table links to in-depth tutorials for authenticating users and securing .NET applications running on Azure.</span></span>

<span data-ttu-id="ea249-105">有关示例源代码，请参阅 [Azure 服务示例](https://azure.microsoft.com/resources/samples/?platform=dotnet)列表。</span><span class="sxs-lookup"><span data-stu-id="ea249-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>

| | |
|---|---|
|<span data-ttu-id="ea249-106">**Active Directory**</span><span class="sxs-lookup"><span data-stu-id="ea249-106">**Active Directory**</span></span>||
| <span data-ttu-id="ea249-107">[使用 Azure AD 进行 Web 应用登录和注销][1]</span><span class="sxs-lookup"><span data-stu-id="ea249-107">[Web app sign-in and sign-out with Azure AD][1]</span></span> | <span data-ttu-id="ea249-108">使用 ADAL 库在 ASP.NET 中登录和注销用户。</span><span class="sxs-lookup"><span data-stu-id="ea249-108">Sign users in and out of your ASP.NET with the ADAL library.</span></span>
| <span data-ttu-id="ea249-109">[使用 Azure AD 进行桌面应用程序身份验证][2]</span><span class="sxs-lookup"><span data-stu-id="ea249-109">[Desktop application authentication with Azure AD][2]</span></span>| <span data-ttu-id="ea249-110">使用 ADAL 将 Azure AD 集成到 Windows 桌面 WPF 应用中。</span><span class="sxs-lookup"><span data-stu-id="ea249-110">Integrate Azure AD into a Windows Desktop WPF app using ADAL.</span></span> | 
| <span data-ttu-id="ea249-111">[使用 Azure AD 进行 Web API 身份验证][3]</span><span class="sxs-lookup"><span data-stu-id="ea249-111">[Web API authentication with Azure AD][3]</span></span> | <span data-ttu-id="ea249-112">通过 Azure AD 使用持有者令牌保护 Web API。</span><span class="sxs-lookup"><span data-stu-id="ea249-112">Protect a web API using bearer tokens from Azure AD.</span></span> |
|<span data-ttu-id="ea249-113">**Key Vault**</span><span class="sxs-lookup"><span data-stu-id="ea249-113">**Key Vault**</span></span>||
| <span data-ttu-id="ea249-114">[从 Web 应用程序使用 Azure Key Vault][4]</span><span class="sxs-lookup"><span data-stu-id="ea249-114">[Use Azure Key Vault from a Web Application][4]</span></span> | <span data-ttu-id="ea249-115">访问 Azure Key Vault 中的机密，以便可以在 Web 应用程序中使用该机密。</span><span class="sxs-lookup"><span data-stu-id="ea249-115">Access a secret from an Azure Key Vault so that it can be used in your web application.</span></span> | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application