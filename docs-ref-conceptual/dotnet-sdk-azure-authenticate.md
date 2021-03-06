---
title: 使用用于 .NET 的 Azure 库进行身份验证
description: 在用于 .NET 的 Azure 库中进行身份验证
ms.date: 08/22/2018
ms.openlocfilehash: d0d8db89816a887fa23490a213917a3c554ecdb4
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190852"
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a>使用用于 .NET 的 Azure 库进行身份验证

## <a name="connect-to-services-with-connection-strings"></a>使用连接字符串连接到服务

大多数 Azure 服务库要求使用连接字符串或密钥进行身份验证。 例如，SQL 数据库使用标准的 SQL 连接字符串：

```csharp
var builder = new SqlConnectionStringBuilder();
builder.DataSource = "example.database.windows.net";
builder.InitialCatalog = "MyDatabase";
builder.UserID = "sampleuser@example"; // Format user ID as "user@server"
builder.Password = password;
builder.Encrypt = true;
builder.TrustServerCertificate = true;
                
using (var conn = new SqlConnection(builder.ConnectionString))
{
    conn.Open();
    // Do things with the connection...
    // ...
}
```

Azure 存储使用存储密钥：

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

[CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db)、[Redis 缓存](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache)和[服务总线](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues)等其他 Azure 服务中使用服务连接字符串，可以使用 Azure 门户、CLI 或 PowerShell 获取这些字符串。  还可以使用用于 .NET 的 Azure 管理库来查询资源，以便在代码中生成连接字符串。 

以下代码片段使用管理库创建存储帐户连接字符串：

```csharp
// Get a storage account
var storage = azure.StorageAccounts.GetByResourceGroup("myResourceGroup", "myStorageAccount");

// Extract the keys
var storageKeys = storage.GetKeys();

// Build the connection string
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

// Connect
var account = CloudStorageAccount.Parse(storageConnectionString);

// Do things with the account here...
```

其他库要求应用程序使用[服务主体](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)运行，该服务主体授权应用程序使用授予的凭据来运行。 此配置类似于管理库的下列基于对象的身份验证步骤。

## <a name="mgmt-auth"></a>用于 .NET 的 Azure 管理库身份验证

[!include[Create service principal](includes/create-sp.md)]

创建服务主体后，可以使用两个选项对服务主体进行身份验证，以创建和管理资源。

若要使用这两个选项，需将以下 Nuget 包添加到项目。

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a>使用令牌凭据进行身份验证

第一种方法是在代码中生成令牌凭据对象。  应将凭据安全存储在配置文件、注册表或 Azure KeyVault 中。

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

使用在创建服务主体时获得的 JSON 输出中的 *clientId*、*clientSecret* 和 *tenantId* 值。

然后，创建入口点 `Azure` 对象以开始使用 API：

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="mgmt-file"></a>基于文件的身份验证

使用基于文件的身份验证可将服务主体凭据放入纯文本文件，并在文件系统中对其进行保护。

[!include[File-based authentication](includes/file-based-auth.md)]

读取该文件的内容，并创建入口点 `Azure` 对象以开始使用 API：

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
