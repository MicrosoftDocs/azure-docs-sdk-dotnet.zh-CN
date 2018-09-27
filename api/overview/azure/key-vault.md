---
title: 用于 .NET 的 Azure Key Vault 库
description: 用于 .NET 的 Azure Key Vault 库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: key-vault
ms.openlocfilehash: a42eb9684bcfb8e8d2209235f61bbf6962cf5e9e
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190550"
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="bb4f0-103">用于 .NET 的 Azure Key Vault 库</span><span class="sxs-lookup"><span data-stu-id="bb4f0-103">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="bb4f0-104">概述</span><span class="sxs-lookup"><span data-stu-id="bb4f0-104">Overview</span></span>

<span data-ttu-id="bb4f0-105">Azure 密钥保管库可帮助保护云应用程序和服务使用的加密密钥和机密。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-105">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="bb4f0-106">依次阅读[什么是 Key Vault？](/azure/key-vault/key-vault-whatis)和 [Azure Key Vault 入门](/azure/key-vault/key-vault-get-started)，或了解如何[从 web 应用使用 Key Vault](/azure/key-vault/key-vault-use-from-web-application)。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-106">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="bb4f0-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="bb4f0-107">Client library</span></span>

<span data-ttu-id="bb4f0-108">使用客户端库可管理密钥和相关的资产，例如证书和机密。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-108">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="bb4f0-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.KeyVault)。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bb4f0-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="bb4f0-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="bb4f0-111">示例</span><span class="sxs-lookup"><span data-stu-id="bb4f0-111">Example</span></span>

<span data-ttu-id="bb4f0-112">以下示例检索在应用程序设置中标识的特定密钥的机密。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-112">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb4f0-113">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="bb4f0-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="bb4f0-114">管理库</span><span class="sxs-lookup"><span data-stu-id="bb4f0-114">Management library</span></span>

<span data-ttu-id="bb4f0-115">使用管理库可创建、删除和查询 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-115">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="bb4f0-116">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bb4f0-117">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="bb4f0-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="bb4f0-118">示例</span><span class="sxs-lookup"><span data-stu-id="bb4f0-118">Example</span></span>

<span data-ttu-id="bb4f0-119">以下示例演示如何为给定的资源组和位置创建新的 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-119">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

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
> [<span data-ttu-id="bb4f0-120">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="bb4f0-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="bb4f0-121">示例</span><span class="sxs-lookup"><span data-stu-id="bb4f0-121">Samples</span></span>

* [<span data-ttu-id="bb4f0-122">下载 Azure Key Vault 客户端示例</span><span class="sxs-lookup"><span data-stu-id="bb4f0-122">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* [<span data-ttu-id="bb4f0-123">.NET 中的 Azure 客户端加密入门</span><span class="sxs-lookup"><span data-stu-id="bb4f0-123">Getting Started with Azure Client Side Encryption in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


<span data-ttu-id="bb4f0-124">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="bb4f0-124">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
