---
title: 用于 .NET 的 Azure Key Vault 库
description: 用于 .NET 的 Azure Key Vault 库参考
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: key-vault
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 3b8bcb9135794592f493db679e60fd40116d05e6
ms.sourcegitcommit: 4114b8821f20e02f4185fcea7549d716f29b9c90
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2017
ms.locfileid: "23489181"
---
# <a name="azure-key-vault-libraries-for-net"></a>用于 .NET 的 Azure Key Vault 库

## <a name="overview"></a>概述

Azure 密钥保管库可帮助保护云应用程序和服务使用的加密密钥和机密。

依次阅读[什么是 Key Vault？](/azure/key-vault/key-vault-whatis)和 [Azure Key Vault 入门](/azure/key-vault/key-vault-get-started)，或了解如何[从 web 应用使用 Key Vault](/azure/key-vault/key-vault-use-from-web-application)。

## <a name="client-library"></a>客户端库

使用客户端库可管理密钥和相关的资产，例如证书和机密。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.KeyVault)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a>示例

以下示例检索在应用程序设置中标识的特定密钥的机密。

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a>管理库

使用管理库可创建、删除和查询 Key Vault。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a>示例

以下示例演示如何为给定的资源组和位置创建新的 Key Vault。

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
> [了解管理 API](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a>示例

* [下载 Azure Key Vault 客户端示例](https://www.microsoft.com/download/details.aspx?id=45343)
* [.NET 中的 Azure 客户端加密入门](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
