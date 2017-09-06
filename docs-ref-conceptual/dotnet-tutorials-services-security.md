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
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a>有关在 Azure 上运行的 .NET 应用中对用户进行身份验证的教程

下表提供了有关验证用户身份以及保护 Azure 上运行的 .NET 应用程序的深入教程的链接。

有关示例源代码，请参阅 [Azure 服务示例](https://azure.microsoft.com/resources/samples/?platform=dotnet)列表。

| | |
|---|---|
|**Active Directory**||
| [使用 Azure AD 进行 Web 应用登录和注销][1] | 使用 ADAL 库在 ASP.NET 中登录和注销用户。
| [使用 Azure AD 进行桌面应用程序身份验证][2]| 使用 ADAL 将 Azure AD 集成到 Windows 桌面 WPF 应用中。 | 
| [使用 Azure AD 进行 Web API 身份验证][3] | 通过 Azure AD 使用持有者令牌保护 Web API。 |
|**Key Vault**||
| [从 Web 应用程序使用 Azure Key Vault][4] | 访问 Azure Key Vault 中的机密，以便可以在 Web 应用程序中使用该机密。 | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application