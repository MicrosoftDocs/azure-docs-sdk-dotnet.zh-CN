---
title: 用于 .NET 的 Azure Key Vault 库
description: 用于 .NET 的 Azure Key Vault 库参考
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: key-vault
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 037b80f60616a37665eddb0b7b212d15180700ba
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065447"
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="acd34-104">用于 .NET 的 Azure Key Vault 库</span><span class="sxs-lookup"><span data-stu-id="acd34-104">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="acd34-105">概述</span><span class="sxs-lookup"><span data-stu-id="acd34-105">Overview</span></span>

<span data-ttu-id="acd34-106">Azure 密钥保管库可帮助保护云应用程序和服务使用的加密密钥和机密。</span><span class="sxs-lookup"><span data-stu-id="acd34-106">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="acd34-107">依次阅读[什么是 Key Vault？](/azure/key-vault/key-vault-whatis)和 [Azure Key Vault 入门](/azure/key-vault/key-vault-get-started)，或了解如何[从 web 应用使用 Key Vault](/azure/key-vault/key-vault-use-from-web-application)。</span><span class="sxs-lookup"><span data-stu-id="acd34-107">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="acd34-108">客户端库</span><span class="sxs-lookup"><span data-stu-id="acd34-108">Client library</span></span>

<span data-ttu-id="acd34-109">使用客户端库可管理密钥和相关的资产，例如证书和机密。</span><span class="sxs-lookup"><span data-stu-id="acd34-109">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="acd34-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.KeyVault)。</span><span class="sxs-lookup"><span data-stu-id="acd34-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="acd34-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="acd34-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="acd34-112">示例</span><span class="sxs-lookup"><span data-stu-id="acd34-112">Example</span></span>

<span data-ttu-id="acd34-113">以下示例检索在应用程序设置中标识的特定密钥的机密。</span><span class="sxs-lookup"><span data-stu-id="acd34-113">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="acd34-114">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="acd34-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="acd34-115">管理库</span><span class="sxs-lookup"><span data-stu-id="acd34-115">Management library</span></span>

<span data-ttu-id="acd34-116">使用管理库可创建、删除和查询 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="acd34-116">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="acd34-117">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="acd34-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="acd34-118">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="acd34-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="acd34-119">示例</span><span class="sxs-lookup"><span data-stu-id="acd34-119">Example</span></span>

<span data-ttu-id="acd34-120">以下示例演示如何为给定的资源组和位置创建新的 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="acd34-120">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

```csharp
using (KeyVaultManagementClient client = new KeyVaultManagementClient(
    new TokenCloudCredentials(subscriptionId, accessToken)))
{
    client.Vaults.CreateOrUpdate(resourceGroupName, "myKeyVault", new VaultCreateOrUpdateParameters
    {
        Properties = new VaultProperties
        {
            EnabledForDeployment = true,
            EnabledForDiskEncryption = true,
            EnabledForTemplateDeployment = true,
            Location = resourceGroupLocation,
            // SKU level, access policies, tenants, etc.
        }
    });
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="acd34-121">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="acd34-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="acd34-122">示例</span><span class="sxs-lookup"><span data-stu-id="acd34-122">Samples</span></span>

* [<span data-ttu-id="acd34-123">下载 Azure Key Vault 客户端示例</span><span class="sxs-lookup"><span data-stu-id="acd34-123">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* [<span data-ttu-id="acd34-124">.NET 中的 Azure 客户端加密入门</span><span class="sxs-lookup"><span data-stu-id="acd34-124">Getting Started with Azure Client Side Encryption in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


<span data-ttu-id="acd34-125">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="acd34-125">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
