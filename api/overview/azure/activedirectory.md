---
title: "用于 .NET 的 Azure Active Directory 库"
description: "用于 .NET 的 Azure Active Directory 库参考"
keywords: Azure, .NET, SDK, API, AAD, Active Directory
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: active-directory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: aa20715fb62b1d4b714245c404f1a7c142caf586
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
---
# <a name="azure-active-directory-libraries-for-net"></a>用于 .NET 的 Azure Active Directory 库

## <a name="overview"></a>概述

使用 Azure Active Directory 将用户登录并管理对应用程序和 API 的访问。

若要开始使用 Azure Active Directory，请参阅[使用 Azure AD 进行 ASP.NET Web 应用登录和注销](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)。

## <a name="client-library"></a>客户端库

通过 OAuth2、OpenID Connect、Active Directory 图形 API 身份验证或 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 连接用户或应用程序并对其进行身份验证。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a>代码示例

检索桌面应用程序的访问令牌。

```csharp
/* Include this "using" directive...
using Microsoft.IdentityModel.Clients.ActiveDirectory;
*/

AuthenticationResult result = null;
AuthenticationContext authContext = new AuthenticationContext("https://someauthority.com");
try
{
    result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
}
catch (AdalException ex)
{
    // An unexpected error occurred, or user canceled the sign in.
    if (ex.ErrorCode != "access_denied")
        MessageBox.Show(ex.Message);

    return;
}
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a>示例

* [通过 Azure AD 租户使用 OpenID Connect 对用户进行身份验证](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [使用 Oauth2 调用具有应用程序权限的 Web API](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [在应用程序中使用基于角色的访问控制 (RBAC)](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

浏览 [Azure Active Directory 代码示例](/azure/active-directory/develop/active-directory-code-samples)的完整集合。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
