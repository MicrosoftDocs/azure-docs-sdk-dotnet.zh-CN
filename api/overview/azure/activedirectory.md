---
title: 用于 .NET 的 Azure Active Directory 库
description: 用于 .NET 的 Azure Active Directory 库参考
keywords: Azure, .NET, SDK, API, AAD, Active Directory
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: active-directory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: a5a228fcde29dbef6a6e8d0482121ee710b002a4
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065857"
---
# <a name="azure-active-directory-libraries-for-net"></a><span data-ttu-id="144c3-104">用于 .NET 的 Azure Active Directory 库</span><span class="sxs-lookup"><span data-stu-id="144c3-104">Azure Active Directory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="144c3-105">概述</span><span class="sxs-lookup"><span data-stu-id="144c3-105">Overview</span></span>

<span data-ttu-id="144c3-106">使用 Azure Active Directory 将用户登录并管理对应用程序和 API 的访问。</span><span class="sxs-lookup"><span data-stu-id="144c3-106">Sign-on users and manage access to applications and APIs with Azure Active Directory.</span></span>

<span data-ttu-id="144c3-107">若要开始使用 Azure Active Directory，请参阅[使用 Azure AD 进行 ASP.NET Web 应用登录和注销](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="144c3-107">To get started with Azure Active Directory, see [ASP.NET web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="144c3-108">客户端库</span><span class="sxs-lookup"><span data-stu-id="144c3-108">Client library</span></span>

<span data-ttu-id="144c3-109">通过 OAuth2、OpenID Connect、Active Directory 图形 API 身份验证或 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 连接用户或应用程序并对其进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="144c3-109">Connect and authenticate users or applications over OAuth2, OpenID Connect, Active Directory Graph API authentication or [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span></span>

<span data-ttu-id="144c3-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="144c3-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="144c3-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="144c3-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a><span data-ttu-id="144c3-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="144c3-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a><span data-ttu-id="144c3-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="144c3-113">Code Example</span></span>

<span data-ttu-id="144c3-114">检索桌面应用程序的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="144c3-114">Retrieve an access token for a desktop application.</span></span>

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
> [<span data-ttu-id="144c3-115">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="144c3-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a><span data-ttu-id="144c3-116">示例</span><span class="sxs-lookup"><span data-stu-id="144c3-116">Samples</span></span>

* [<span data-ttu-id="144c3-117">通过 Azure AD 租户使用 OpenID Connect 对用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="144c3-117">Use OpenID Connect to authenticate users from an Azure AD tenant</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [<span data-ttu-id="144c3-118">使用 Oauth2 调用具有应用程序权限的 Web API</span><span class="sxs-lookup"><span data-stu-id="144c3-118">Use Oauth2 to call a web API with application permissions</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [<span data-ttu-id="144c3-119">在应用程序中使用基于角色的访问控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="144c3-119">Use role-based access control (RBAC) in an application</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

<span data-ttu-id="144c3-120">浏览 [Azure Active Directory 代码示例](/azure/active-directory/develop/active-directory-code-samples)的完整集合。</span><span class="sxs-lookup"><span data-stu-id="144c3-120">Explore the full collection of [Azure Active Directory code samples](/azure/active-directory/develop/active-directory-code-samples).</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
