---
title: 有关保护 Azure 应用的 .NET 教程
description: 有关 Azure 上运行的 .NET 应用的应用程序安全和标识管理的教程。
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 88ecfc69fbd57becf1adf1163a063c0d2bb086a8
ms.sourcegitcommit: 61638b504b6c4d96b357894835c80c2680a99fe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750585"
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a><span data-ttu-id="2e017-103">有关在 Azure 上运行的 .NET 应用中对用户进行身份验证的教程</span><span class="sxs-lookup"><span data-stu-id="2e017-103">Tutorials for authenticating users in your .NET apps running on Azure</span></span>

<span data-ttu-id="2e017-104">下表提供了有关验证用户身份以及保护 Azure 上运行的 .NET 应用程序的深入教程的链接。</span><span class="sxs-lookup"><span data-stu-id="2e017-104">The following table links to in-depth tutorials for authenticating users and securing .NET applications running on Azure.</span></span>

<span data-ttu-id="2e017-105">有关示例源代码，请参阅 [Azure 服务示例](https://azure.microsoft.com/resources/samples/?platform=dotnet)列表。</span><span class="sxs-lookup"><span data-stu-id="2e017-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>

| | |
|---|---|
|<span data-ttu-id="2e017-106">**Active Directory**</span><span class="sxs-lookup"><span data-stu-id="2e017-106">**Active Directory**</span></span>||
| <span data-ttu-id="2e017-107">[使用 Visual Studio 连接服务将 Azure Active Directory 添加到 Web 应用程序][5]</span><span class="sxs-lookup"><span data-stu-id="2e017-107">[Add Azure Active Directory to your web application by using Visual Studio Connected Services][5]</span></span> | <span data-ttu-id="2e017-108">在 Visual Studio 中将 Web 应用连接到 Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e017-108">Connect a web app to Azure AD in Visual Studio</span></span> |
| <span data-ttu-id="2e017-109">[使用 Azure AD 进行 Web 应用登录和注销][1]</span><span class="sxs-lookup"><span data-stu-id="2e017-109">[Web app sign-in and sign-out with Azure AD][1]</span></span> | <span data-ttu-id="2e017-110">使用 ADAL 库在 ASP.NET 中登录和注销用户。</span><span class="sxs-lookup"><span data-stu-id="2e017-110">Sign users in and out of your ASP.NET with the ADAL library.</span></span> |
| <span data-ttu-id="2e017-111">[使用 Azure AD 进行桌面应用程序身份验证][2]</span><span class="sxs-lookup"><span data-stu-id="2e017-111">[Desktop application authentication with Azure AD][2]</span></span>| <span data-ttu-id="2e017-112">使用 ADAL 将 Azure AD 集成到 Windows 桌面 WPF 应用中。</span><span class="sxs-lookup"><span data-stu-id="2e017-112">Integrate Azure AD into a Windows Desktop WPF app using ADAL.</span></span> | 
| <span data-ttu-id="2e017-113">[使用 Azure AD 进行 Web API 身份验证][3]</span><span class="sxs-lookup"><span data-stu-id="2e017-113">[Web API authentication with Azure AD][3]</span></span> | <span data-ttu-id="2e017-114">通过 Azure AD 使用持有者令牌保护 Web API。</span><span class="sxs-lookup"><span data-stu-id="2e017-114">Protect a web API using bearer tokens from Azure AD.</span></span> |
|<span data-ttu-id="2e017-115">**Key Vault**</span><span class="sxs-lookup"><span data-stu-id="2e017-115">**Key Vault**</span></span>||
| <span data-ttu-id="2e017-116">[使用 Visual Studio 连接服务将 Key Vault 添加到 Web 应用程序][6]</span><span class="sxs-lookup"><span data-stu-id="2e017-116">[Add Key Vault to your web application by using Visual Studio Connected Services][6]</span></span> | <span data-ttu-id="2e017-117">在 Visual Studio 中将 Web 应用连接到 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="2e017-117">Connect a web app to Azure Key Vault in Visual Studio</span></span> |
| <span data-ttu-id="2e017-118">[从 Web 应用程序使用 Azure Key Vault][4]</span><span class="sxs-lookup"><span data-stu-id="2e017-118">[Use Azure Key Vault from a Web Application][4]</span></span> | <span data-ttu-id="2e017-119">访问 Azure Key Vault 中的机密，以便可以在 Web 应用程序中使用该机密。</span><span class="sxs-lookup"><span data-stu-id="2e017-119">Access a secret from an Azure Key Vault so that it can be used in your web application.</span></span> | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application
[5]: /azure/active-directory/develop/vs-active-directory-add-connected-service
[6]: /azure/key-vault/vs-key-vault-add-connected-service