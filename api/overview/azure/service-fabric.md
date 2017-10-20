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
# <a name="azure-service-fabric-libraries-for-net"></a>用于 .NET 的 Azure Service Fabric 库

## <a name="overview"></a>概述

Azure Service Fabric 是一款分布式系统平台，可方便用户轻松打包、部署和管理可缩放的可靠微服务和容器。  有关详细信息，请参阅 [Azure Service Fabric CLI 文档](/azure/service-fabric/)。

## <a name="client-library"></a>客户端库

使用 Service Fabric 客户端库可与现有 Service Fabric 群集交互。  该库包含三个类别的 API：

* **客户端** API 用于管理、缩放和回收群集以及部署应用程序包。
* **运行时** API 供正在运行的应用程序用来与其托管群集交互。
* **公用** API 包含在**客户端** API 和**运行时** API 中使用的类型。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.ServiceFabric)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a>代码示例

以下示例使用 Service Fabric **客户端** API 将应用程序包复制到映像存储、预配应用程序类型，并创建应用程序实例。

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
> [了解客户端 API](/dotnet/api/overview/azure/servicefabric/client)

此示例从托管的应用程序中使用 Service Fabric **运行时** API 和**公用** API，以在运行时更新 [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections)。

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
> [浏览运行时 API](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [浏览公用 API](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a>管理库

管理库用于创建、更新和删除 Service Fabric 群集。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a>示例

* [使用 FabricClient 部署和删除应用程序](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
