---
title: "Azure .NET 存储 API"
description: "用于 .NET 的 Azure 存储库参考"
keywords: "Azure, .NET, SDK, API, 存储, blob"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 4e494952b48bfbf3b10f9af9936648634353db78
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-storage-apis-for-net"></a><span data-ttu-id="e18da-104">用于 .NET 的 Azure 存储 API</span><span class="sxs-lookup"><span data-stu-id="e18da-104">Azure Storage APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e18da-105">概述</span><span class="sxs-lookup"><span data-stu-id="e18da-105">Overview</span></span>

<span data-ttu-id="e18da-106">使用 [Azure 存储](https://review.docs.microsoft.com/en-us/azure/storage/storage-introduction)在 .NET 应用程序中读取和写入文件、Blob（对象）数据、键值对和消息。</span><span class="sxs-lookup"><span data-stu-id="e18da-106">Read and write files, blob (object) data, key-value pairs, and messages from your .NET applications with [Azure Storage](https://review.docs.microsoft.com/en-us/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="e18da-107">若要开始使用 Azure 存储，请参阅[通过 .NET 开始使用 Azure Blob 存储](/azure/storage/storage-dotnet-how-to-use-blobs)。</span><span class="sxs-lookup"><span data-stu-id="e18da-107">To get started with Azure Storage, see [Get started with Azure Blob storage using .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

## <a name="client-library"></a><span data-ttu-id="e18da-108">客户端库</span><span class="sxs-lookup"><span data-stu-id="e18da-108">Client library</span></span>

<span data-ttu-id="e18da-109">使用[连接字符串](/azure/storage/storage-create-storage-account#manage-your-storage-account)连接到 Azure 存储帐户，然后通过客户端库的类和方法来使用 Blob、表、文件或队列存储。</span><span class="sxs-lookup"><span data-stu-id="e18da-109">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span>

<span data-ttu-id="e18da-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/WindowsAzure.Storage)。</span><span class="sxs-lookup"><span data-stu-id="e18da-110">Install the [NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e18da-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="e18da-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a><span data-ttu-id="e18da-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="e18da-112">.NET Core CLI</span></span>

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a><span data-ttu-id="e18da-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="e18da-113">Code Example</span></span>

<span data-ttu-id="e18da-114">此示例为现有存储帐户中的新容器创建新的 Blob。</span><span class="sxs-lookup"><span data-stu-id="e18da-114">This example creates a new blob to a new container in an existing storage account.</span></span>

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
> [<span data-ttu-id="e18da-115">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="e18da-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a><span data-ttu-id="e18da-116">管理 API</span><span class="sxs-lookup"><span data-stu-id="e18da-116">Management APIs</span></span>

<span data-ttu-id="e18da-117">使用管理 API 创建和管理 Azure 存储帐户与连接密钥。</span><span class="sxs-lookup"><span data-stu-id="e18da-117">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="e18da-118">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="e18da-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e18da-119">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="e18da-119">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="e18da-120">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="e18da-120">.NET Core CLI</span></span>

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a><span data-ttu-id="e18da-121">代码示例</span><span class="sxs-lookup"><span data-stu-id="e18da-121">Code Example</span></span>

<span data-ttu-id="e18da-122">此示例创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="e18da-122">This example creates a storage account.</span></span>

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
> [<span data-ttu-id="e18da-123">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="e18da-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a><span data-ttu-id="e18da-124">示例</span><span class="sxs-lookup"><span data-stu-id="e18da-124">Samples</span></span>

* [<span data-ttu-id="e18da-125">在 .NET 中开始使用 Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="e18da-125">Get started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [<span data-ttu-id="e18da-126">在 .NET 中开始使用 Azure 队列存储</span><span class="sxs-lookup"><span data-stu-id="e18da-126">Get started with Azure Queue Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

<span data-ttu-id="e18da-127">查看 Azure 存储示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage)。</span><span class="sxs-lookup"><span data-stu-id="e18da-127">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) of Azure Storage samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package