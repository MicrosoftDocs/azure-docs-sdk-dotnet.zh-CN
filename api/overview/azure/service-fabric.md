---
title: "用于 .NET 的 Azure Service Fabric 库"
description: "用于 .NET 的 Azure Service Fabric 库参考"
keywords: Azure, .NET, SDK, API, Service Fabric
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/07/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: c708ae06fa4b5165e3f615abf636b11bfd95cd3b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="a48d8-104">用于 .NET 的 Azure Service Fabric 库</span><span class="sxs-lookup"><span data-stu-id="a48d8-104">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a48d8-105">概述</span><span class="sxs-lookup"><span data-stu-id="a48d8-105">Overview</span></span>

<span data-ttu-id="a48d8-106">Azure Service Fabric 是一款分布式系统平台，可方便用户轻松打包、部署和管理可缩放的可靠微服务和容器。</span><span class="sxs-lookup"><span data-stu-id="a48d8-106">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>

## <a name="client-library"></a><span data-ttu-id="a48d8-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="a48d8-107">Client library</span></span>

<span data-ttu-id="a48d8-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.ServiceFabric)。</span><span class="sxs-lookup"><span data-stu-id="a48d8-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a48d8-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="a48d8-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-example"></a><span data-ttu-id="a48d8-110">代码示例</span><span class="sxs-lookup"><span data-stu-id="a48d8-110">Code Example</span></span>

<span data-ttu-id="a48d8-111">以下示例将应用程序包复制到映像存储区、预配应用程序类型，并创建应用程序实例。</span><span class="sxs-lookup"><span data-stu-id="a48d8-111">The following example copies an application package to the image store, provisions the application type, and creates an application instance.</span></span>

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
> [<span data-ttu-id="a48d8-112">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="a48d8-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

## <a name="samples"></a><span data-ttu-id="a48d8-113">示例</span><span class="sxs-lookup"><span data-stu-id="a48d8-113">Samples</span></span>

* [<span data-ttu-id="a48d8-114">使用 FabricClient 部署和删除应用程序</span><span class="sxs-lookup"><span data-stu-id="a48d8-114">Deploy and remove applications using FabricClient</span></span>](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
