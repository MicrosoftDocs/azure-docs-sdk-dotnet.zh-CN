---
title: "使用用于 .NET 的 Azure 库进行身份验证"
description: "在用于 .NET 的 Azure 库中进行身份验证"
keywords: "Azure, .NET, SDK, API, 身份验证, active directory, 服务主体"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: c9755d7e9c20186c7677b4bfe69d4033f9852607
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a><span data-ttu-id="d9f41-104">使用用于 .NET 的 Azure 库进行身份验证</span><span class="sxs-lookup"><span data-stu-id="d9f41-104">Authenticate with the Azure Libraries for .NET</span></span>

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="d9f41-105">使用连接字符串连接到服务</span><span class="sxs-lookup"><span data-stu-id="d9f41-105">Connect to services with connection strings</span></span>

<span data-ttu-id="d9f41-106">大多数 Azure 服务库要求使用连接字符串或密钥进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="d9f41-106">Most Azure service libraries require a connection string or keys for authentication.</span></span> <span data-ttu-id="d9f41-107">例如，SQL 数据库使用标准的 SQL 连接字符串：</span><span class="sxs-lookup"><span data-stu-id="d9f41-107">For example, SQL Database uses a standard SQL connection string:</span></span>

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

<span data-ttu-id="d9f41-108">Azure 存储使用存储密钥：</span><span class="sxs-lookup"><span data-stu-id="d9f41-108">Azure Storage uses a storage key:</span></span>

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

<span data-ttu-id="d9f41-109">[CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db)、[Redis 缓存](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache)和[服务总线](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues)等其他 Azure 服务中使用服务连接字符串，可以使用 Azure 门户、CLI 或 PowerShell 获取这些字符串。</span><span class="sxs-lookup"><span data-stu-id="d9f41-109">Service connection strings are used in other Azure services like [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache), and [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) and you can get those strings using the Azure portal, CLI, or PowerShell.</span></span>  <span data-ttu-id="d9f41-110">还可以使用用于 .NET 的 Azure 管理库来查询资源，以便在代码中生成连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d9f41-110">You can also use the Azure management libraries for .NET to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="d9f41-111">以下代码片段使用管理库创建存储帐户连接字符串：</span><span class="sxs-lookup"><span data-stu-id="d9f41-111">This snippet uses the management libraries to create a storage account connection string:</span></span>

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

<span data-ttu-id="d9f41-112">其他库要求应用程序使用[服务主体](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)运行，该服务主体授权应用程序使用授予的凭据来运行。</span><span class="sxs-lookup"><span data-stu-id="d9f41-112">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="d9f41-113">此配置类似于管理库的下列基于对象的身份验证步骤。</span><span class="sxs-lookup"><span data-stu-id="d9f41-113">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

## <span data-ttu-id="d9f41-114"><a name="mgmt-auth"></a>用于 .NET 的 Azure 管理库身份验证</span><span class="sxs-lookup"><span data-stu-id="d9f41-114"><a name="mgmt-auth"></a>Azure management libraries for .NET authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

<span data-ttu-id="d9f41-115">创建服务主体后，可以使用两个选项对服务主体进行身份验证，以创建和管理资源。</span><span class="sxs-lookup"><span data-stu-id="d9f41-115">Now that the service principal is created, two options are available to authenticate to the service principal to create and manage resources.</span></span>

<span data-ttu-id="d9f41-116">若要使用这两个选项，需将以下 Nuget 包添加到项目。</span><span class="sxs-lookup"><span data-stu-id="d9f41-116">For both options you will need to add the following nuget packages to your project.</span></span>

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a><span data-ttu-id="d9f41-117">使用令牌凭据进行身份验证</span><span class="sxs-lookup"><span data-stu-id="d9f41-117">Authenticate with token credentials</span></span>

<span data-ttu-id="d9f41-118">第一种方法是在代码中生成令牌凭据对象。</span><span class="sxs-lookup"><span data-stu-id="d9f41-118">The first method is to build the token credential object in code.</span></span>  <span data-ttu-id="d9f41-119">应将凭据安全存储在配置文件、注册表或 Azure KeyVault 中。</span><span class="sxs-lookup"><span data-stu-id="d9f41-119">You should store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

- <span data-ttu-id="d9f41-120">clientId：使用服务主体输出中的 *ApplicationId* 值。</span><span class="sxs-lookup"><span data-stu-id="d9f41-120">clientId: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="d9f41-121">clientSecret：使用运行 `New-AzureRmADServicePrincipal`（不带引号）时分配的 *-Password* 参数。</span><span class="sxs-lookup"><span data-stu-id="d9f41-121">clientSecret: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="d9f41-122">tenantId：使用运行 `Login-AzureRmAccount` 后返回的 *TenantId* 值。</span><span class="sxs-lookup"><span data-stu-id="d9f41-122">tenantId: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="d9f41-123">然后，创建入口点 `Azure` 对象以开始使用 API：</span><span class="sxs-lookup"><span data-stu-id="d9f41-123">Then create the entry point `Azure` object to start working with the API:</span></span>

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <span data-ttu-id="d9f41-124"><a name="mgmt-file"></a>基于文件的身份验证</span><span class="sxs-lookup"><span data-stu-id="d9f41-124"><a name="mgmt-file"></a>File-based authentication</span></span>

<span data-ttu-id="d9f41-125">使用基于文件的身份验证可将服务主体凭据放入纯文本文件，并在文件系统中对其进行保护。</span><span class="sxs-lookup"><span data-stu-id="d9f41-125">File-based authentication allows you to put the service principal credentials in a plain text file and secure it within the file system.</span></span>

[!include[File-based authentication](includes/file-based-auth.md)]

<span data-ttu-id="d9f41-126">读取该文件的内容，并创建入口点 `Azure` 对象以开始使用 API：</span><span class="sxs-lookup"><span data-stu-id="d9f41-126">Read the contents of the file and create the entry point `Azure` object to start working with the API:</span></span>

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
