---
title: 有关保护 Azure 应用的 .NET 教程
description: 有关 Azure 上运行的 .NET 应用的应用程序安全和标识管理的教程。
ms.date: 10/19/2017
ms.openlocfilehash: 19960efa8faa762f0cde657d702f09a8dcb66e99
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190640"
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a>有关在 Azure 上运行的 .NET 应用中对用户进行身份验证的教程

下表提供了有关验证用户身份以及保护 Azure 上运行的 .NET 应用程序的深入教程的链接。

有关示例源代码，请参阅 [Azure 服务示例](https://azure.microsoft.com/resources/samples/?platform=dotnet)列表。

| | |
|---|---|
|**Active Directory**||
| [使用 Visual Studio 连接服务将 Azure Active Directory 添加到 Web 应用程序][5] | 在 Visual Studio 中将 Web 应用连接到 Azure AD |
| [使用 Azure AD 进行 Web 应用登录和注销][1] | 使用 ADAL 库在 ASP.NET 中登录和注销用户。 |
| [使用 Azure AD 进行桌面应用程序身份验证][2]| 使用 ADAL 将 Azure AD 集成到 Windows 桌面 WPF 应用中。 | 
| [使用 Azure AD 进行 Web API 身份验证][3] | 通过 Azure AD 使用持有者令牌保护 Web API。 |
|**Key Vault**||
| [使用 Visual Studio 连接服务将 Key Vault 添加到 Web 应用程序][6] | 在 Visual Studio 中将 Web 应用连接到 Azure Key Vault |
| [从 Web 应用程序使用 Azure Key Vault][4] | 访问 Azure Key Vault 中的机密，以便可以在 Web 应用程序中使用该机密。 | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application
[5]: /azure/active-directory/develop/vs-active-directory-add-connected-service
[6]: /azure/key-vault/vs-key-vault-add-connected-service