---
title: Azure .NET 存储 API
description: 用于 .NET 的 Azure 存储库参考
keywords: Azure, .NET, SDK, API, 存储, blob
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: storage
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 273e7ffc8794ef531e2bd35858b8ad1299755882
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065527"
---
# <a name="azure-storage-apis-for-net"></a>用于 .NET 的 Azure 存储 API

## <a name="overview"></a>概述

使用 [Azure 存储](https://review.docs.microsoft.com/azure/storage/storage-introduction)在 .NET 应用程序中读取和写入文件、Blob（对象）数据、键值对和消息。

若要开始使用 Azure 存储，请参阅[通过 .NET 开始使用 Azure Blob 存储](/azure/storage/storage-dotnet-how-to-use-blobs)。

## <a name="client-library"></a>客户端库

使用[连接字符串](/azure/storage/storage-create-storage-account#manage-your-storage-account)连接到 Azure 存储帐户，然后通过客户端库的类和方法来使用 Blob、表、文件或队列存储。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/WindowsAzure.Storage)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a>代码示例

此示例为现有存储帐户中的新容器创建新的 Blob。

```csharp
/* Include these "using" directives...
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
*/

string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=[Storage Account Name]"
    + ";AccountKey=[Storage Account Key]"
    + ";EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);
CloudBlobClient serviceClient = account.CreateCloudBlobClient();

// Create container. Name must be lower case.
Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("mycontainer");
container.CreateIfNotExistsAsync().Wait();

// write a blob to the container
CloudBlockBlob blob = container.GetBlockBlobReference("helloworld.txt");
blob.UploadTextAsync("Hello, World!").Wait();
```

> [!div class="nextstepactions"]
> [了解客户端 API](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a>管理 API

使用管理 API 创建和管理 Azure 存储帐户与连接密钥。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a>代码示例

此示例创建存储帐户。

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Management.Storage.Fluent
*/

IStorageAccount storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .Create();
```

> [!div class="nextstepactions"]
> [了解管理 API](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a>示例

* [在 .NET 中开始使用 Azure Blob 存储](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [在 .NET 中开始使用 Azure 队列存储](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

查看 Azure 存储示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package