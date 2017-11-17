---
title: "用于 .NET 的 Azure 服务总线库"
description: "用于 .NET 的 Azure 服务总线库参考"
keywords: "Azure, .NET, SDK, API, 服务总线"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: c2019fd39f42f9bc4a39dd4e642db9f90b7a917c
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
---
# <a name="azure-service-bus-libraries-for-net"></a><span data-ttu-id="812b0-104">用于 .NET 的 Azure 服务总线库</span><span class="sxs-lookup"><span data-stu-id="812b0-104">Azure Service Bus libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="812b0-105">概述</span><span class="sxs-lookup"><span data-stu-id="812b0-105">Overview</span></span>

<span data-ttu-id="812b0-106">[Azure 服务总线](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)是位于各个应用程序之间的消息传送基础结构，允许应用程序交换消息，从而扩大规模并提高恢复能力。</span><span class="sxs-lookup"><span data-stu-id="812b0-106">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) is a messaging infrastructure that sits between applications allowing them to exchange messages for improved scale and resiliency.</span></span>

## <a name="client-library"></a><span data-ttu-id="812b0-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="812b0-107">Client library</span></span>

<span data-ttu-id="812b0-108">直接从 Visual Studio [包管理器控制台][PackageManager]安装 [NuGet 包](https://www.nuget.org/packages/WindowsAzure.ServiceBus)。</span><span class="sxs-lookup"><span data-stu-id="812b0-108">Install the [NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="812b0-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="812b0-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package WindowsAzure.ServiceBus
```

### <a name="code-example"></a><span data-ttu-id="812b0-110">代码示例</span><span class="sxs-lookup"><span data-stu-id="812b0-110">Code Example</span></span>

<span data-ttu-id="812b0-111">此示例向服务总线队列发送消息。</span><span class="sxs-lookup"><span data-stu-id="812b0-111">This example sends a message to a Service Bus queue.</span></span>

```csharp
// using Microsoft.ServiceBus.Messaging;

QueueClient client = QueueClient.CreateFromConnectionString(connectionString, queueName);
BrokeredMessage message = new BrokeredMessage("This is a test message!");
client.Send(message);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="812b0-112">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="812b0-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a><span data-ttu-id="812b0-113">管理库</span><span class="sxs-lookup"><span data-stu-id="812b0-113">Management library</span></span>

<span data-ttu-id="812b0-114">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="812b0-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="812b0-115">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="812b0-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="812b0-116">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="812b0-116">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a><span data-ttu-id="812b0-117">代码示例</span><span class="sxs-lookup"><span data-stu-id="812b0-117">Code Example</span></span>

<span data-ttu-id="812b0-118">此示例创建最大大小为 1024 MB 的服务总线队列。</span><span class="sxs-lookup"><span data-stu-id="812b0-118">This example creates a Service Bus queue with a maximum size of 1024 MB.</span></span>

```csharp
// using Microsoft.Azure.Management.ServiceBus.Fluent;
// using Microsoft.Azure.Management.ServiceBus.Fluent.Models;

using (ServiceBusManagementClient client = new ServiceBusManagementClient(credentials))
{
    client.SubscriptionId = subscriptionId;
    QueueInner parameters = new QueueInner
    {
        MaxSizeInMegabytes = 1024
    };
    await client.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, queueName, parameters);
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="812b0-119">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="812b0-119">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a><span data-ttu-id="812b0-120">示例</span><span class="sxs-lookup"><span data-stu-id="812b0-120">Samples</span></span>

- [<span data-ttu-id="812b0-121">服务总线队列基础知识 - .Net</span><span class="sxs-lookup"><span data-stu-id="812b0-121">Service Bus Queue Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [<span data-ttu-id="812b0-122">服务总线队列高级功能 - .Net</span><span class="sxs-lookup"><span data-stu-id="812b0-122">Service Bus Queue Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [<span data-ttu-id="812b0-123">服务总线发布/订阅基础知识 - .Net</span><span class="sxs-lookup"><span data-stu-id="812b0-123">Service Bus Publish/Subscribe Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [<span data-ttu-id="812b0-124">服务总线发布/订阅高级功能 - .Net</span><span class="sxs-lookup"><span data-stu-id="812b0-124">Service Bus Publish/Subscribe Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [<span data-ttu-id="812b0-125">服务总线与基于声明的授权 - .Net</span><span class="sxs-lookup"><span data-stu-id="812b0-125">Service Bus with Claims-Based Authorization - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

<span data-ttu-id="812b0-126">查看 Azure 服务总线示例的[完整列表](https://azure.microsoft.com/resources/samples/?term=service+bus)。</span><span class="sxs-lookup"><span data-stu-id="812b0-126">View the [complete list](https://azure.microsoft.com/resources/samples/?term=service+bus) of Azure Service Bus samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
