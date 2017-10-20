---
title: "用于 .NET 的 Azure Service Fabric 库"
description: "用于 .NET 的 Azure Service Fabric 库参考"
keywords: Azure, .NET, SDK, API, Service Fabric
author: camsoper
ms.author: casoper
manager: douge
ms.date: 10/13/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-fabric
ms.openlocfilehash: c15da57ef44663ad0463ba76ffa3b6832774240f
ms.sourcegitcommit: a235826f194e938b094be3ed03d86f7e85bb4da6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="f7a82-104">用于 .NET 的 Azure Service Fabric 库</span><span class="sxs-lookup"><span data-stu-id="f7a82-104">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="f7a82-105">概述</span><span class="sxs-lookup"><span data-stu-id="f7a82-105">Overview</span></span>

<span data-ttu-id="f7a82-106">Azure Service Fabric 是一款分布式系统平台，可方便用户轻松打包、部署和管理可缩放的可靠微服务和容器。</span><span class="sxs-lookup"><span data-stu-id="f7a82-106">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>  <span data-ttu-id="f7a82-107">有关详细信息，请参阅 [Azure Service Fabric CLI 文档](/azure/service-fabric/)。</span><span class="sxs-lookup"><span data-stu-id="f7a82-107">For more information, see the [Azure Service Fabric Documentation](/azure/service-fabric/).</span></span>

## <a name="client-library"></a><span data-ttu-id="f7a82-108">客户端库</span><span class="sxs-lookup"><span data-stu-id="f7a82-108">Client library</span></span>

<span data-ttu-id="f7a82-109">使用 Service Fabric 客户端库可与现有 Service Fabric 群集交互。</span><span class="sxs-lookup"><span data-stu-id="f7a82-109">Use the Service Fabric client library to interact with an existing Service Fabric cluster.</span></span>  <span data-ttu-id="f7a82-110">该库包含三个类别的 API：</span><span class="sxs-lookup"><span data-stu-id="f7a82-110">The library contains three categories of APIs:</span></span>

* <span data-ttu-id="f7a82-111">**客户端** API 用于管理、缩放和回收群集以及部署应用程序包。</span><span class="sxs-lookup"><span data-stu-id="f7a82-111">**Client** APIs are used to manage, scale, and recycle the cluster, as well as deploy application packages.</span></span>
* <span data-ttu-id="f7a82-112">**运行时** API 供正在运行的应用程序用来与其托管群集交互。</span><span class="sxs-lookup"><span data-stu-id="f7a82-112">**Runtime** APIs are used for the running application to interact with its hosting cluster.</span></span>
* <span data-ttu-id="f7a82-113">**公用** API 包含在**客户端** API 和**运行时** API 中使用的类型。</span><span class="sxs-lookup"><span data-stu-id="f7a82-113">**Common** APIs contain types used in both **client** and **runtime** APIs.</span></span>

<span data-ttu-id="f7a82-114">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.ServiceFabric)。</span><span class="sxs-lookup"><span data-stu-id="f7a82-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f7a82-115">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="f7a82-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a><span data-ttu-id="f7a82-116">代码示例</span><span class="sxs-lookup"><span data-stu-id="f7a82-116">Code Examples</span></span>

<span data-ttu-id="f7a82-117">以下示例使用 Service Fabric **客户端** API 将应用程序包复制到映像存储、预配应用程序类型，并创建应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="f7a82-117">The following example uses the Service Fabric **client** APIs to copy an application package to the image store, provisions the application type, and create an application instance.</span></span>

```csharp
/* Include these dependencies
using System.Fabric;
using System.Fabric.Description;
*/

// Connect to the cluster.
FabricClient fabricClient = new FabricClient(clusterConnection);

// Copy the application package to a location in the image store
fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);

// Provision the application.
fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

//  Create the application instance.
ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7a82-118">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="f7a82-118">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

<span data-ttu-id="f7a82-119">此示例从托管的应用程序中使用 Service Fabric **运行时** API 和**公用** API，以在运行时更新 [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections)。</span><span class="sxs-lookup"><span data-stu-id="f7a82-119">This example uses the Service Fabric **runtime** and **common** APIs from within a hosted application to update a [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) at runtime.</span></span>

```csharp
using System.Fabric;
using Microsoft.ServiceFabric.Data.Collections;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

/// <summary>
/// This is the main entry point for your service replica.
/// This method executes when this replica of your service becomes primary and has write status.
/// </summary>
/// <param name="cancellationToken">Canceled when Service Fabric needs to shut down this service replica.</param>
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();
        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }
        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7a82-120">浏览运行时 API</span><span class="sxs-lookup"><span data-stu-id="f7a82-120">Explore the runtime APIs</span></span>](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7a82-121">浏览公用 API</span><span class="sxs-lookup"><span data-stu-id="f7a82-121">Explore the common APIs</span></span>](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a><span data-ttu-id="f7a82-122">管理库</span><span class="sxs-lookup"><span data-stu-id="f7a82-122">Management Library</span></span>

<span data-ttu-id="f7a82-123">管理库用于创建、更新和删除 Service Fabric 群集。</span><span class="sxs-lookup"><span data-stu-id="f7a82-123">The management library is used to create, update, and delete Service Fabric clusters.</span></span>

<span data-ttu-id="f7a82-124">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric)。</span><span class="sxs-lookup"><span data-stu-id="f7a82-124">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f7a82-125">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="f7a82-125">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7a82-126">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="f7a82-126">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a><span data-ttu-id="f7a82-127">示例</span><span class="sxs-lookup"><span data-stu-id="f7a82-127">Samples</span></span>

* [<span data-ttu-id="f7a82-128">使用 FabricClient 部署和删除应用程序</span><span class="sxs-lookup"><span data-stu-id="f7a82-128">Deploy and remove applications using FabricClient</span></span>](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
