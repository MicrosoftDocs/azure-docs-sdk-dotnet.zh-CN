---
title: 用于 .NET 的 Azure 服务总线库
description: 用于 .NET 的 Azure 服务总线库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus
ms.openlocfilehash: 506be9a669a2418f2437271d128a963e351442e7
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190870"
---
# <a name="azure-service-bus-libraries-for-net"></a><span data-ttu-id="ae05e-103">用于 .NET 的 Azure 服务总线库</span><span class="sxs-lookup"><span data-stu-id="ae05e-103">Azure Service Bus libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="ae05e-104">概述</span><span class="sxs-lookup"><span data-stu-id="ae05e-104">Overview</span></span>

<span data-ttu-id="ae05e-105">[Azure 服务总线](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)是位于各个应用程序之间的消息传送基础结构，允许应用程序交换消息，从而扩大规模并提高恢复能力。</span><span class="sxs-lookup"><span data-stu-id="ae05e-105">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) is a messaging infrastructure that sits between applications allowing them to exchange messages for improved scale and resiliency.</span></span>

## <a name="client-library"></a><span data-ttu-id="ae05e-106">客户端库</span><span class="sxs-lookup"><span data-stu-id="ae05e-106">Client library</span></span>

<span data-ttu-id="ae05e-107">直接从 Visual Studio [包管理器控制台][PackageManager]安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus)。</span><span class="sxs-lookup"><span data-stu-id="ae05e-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ae05e-108">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="ae05e-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.ServiceBus
```

### <a name="code-example"></a><span data-ttu-id="ae05e-109">代码示例</span><span class="sxs-lookup"><span data-stu-id="ae05e-109">Code Example</span></span>

<span data-ttu-id="ae05e-110">此示例向服务总线队列发送消息。</span><span class="sxs-lookup"><span data-stu-id="ae05e-110">This example sends a message to a Service Bus queue.</span></span>

```csharp
// using Microsoft.Azure.ServiceBus;
// Microsoft.Azure.ServiceBus 2.0.0 (stable)

byte[] messageBody = System.Text.Encoding.Unicode.GetBytes("Hello, world!");
ServiceBusConnectionStringBuilder builder = new ServiceBusConnectionStringBuilder(connectionString);
QueueClient client = new QueueClient(builder, ReceiveMode.PeekLock);
client.SendAsync(new Message(messageBody));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae05e-111">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="ae05e-111">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a><span data-ttu-id="ae05e-112">管理库</span><span class="sxs-lookup"><span data-stu-id="ae05e-112">Management library</span></span>

<span data-ttu-id="ae05e-113">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="ae05e-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ae05e-114">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="ae05e-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="ae05e-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="ae05e-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a><span data-ttu-id="ae05e-116">代码示例</span><span class="sxs-lookup"><span data-stu-id="ae05e-116">Code Example</span></span>

<span data-ttu-id="ae05e-117">此示例创建最大大小为 1024 MB 的服务总线队列。</span><span class="sxs-lookup"><span data-stu-id="ae05e-117">This example creates a Service Bus queue with a maximum size of 1024 MB.</span></span>

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
> [<span data-ttu-id="ae05e-118">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="ae05e-118">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a><span data-ttu-id="ae05e-119">示例</span><span class="sxs-lookup"><span data-stu-id="ae05e-119">Samples</span></span>

- [<span data-ttu-id="ae05e-120">服务总线队列基础知识 - .Net</span><span class="sxs-lookup"><span data-stu-id="ae05e-120">Service Bus Queue Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [<span data-ttu-id="ae05e-121">服务总线队列高级功能 - .Net</span><span class="sxs-lookup"><span data-stu-id="ae05e-121">Service Bus Queue Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [<span data-ttu-id="ae05e-122">服务总线发布/订阅基础知识 - .Net</span><span class="sxs-lookup"><span data-stu-id="ae05e-122">Service Bus Publish/Subscribe Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [<span data-ttu-id="ae05e-123">服务总线发布/订阅高级功能 - .Net</span><span class="sxs-lookup"><span data-stu-id="ae05e-123">Service Bus Publish/Subscribe Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [<span data-ttu-id="ae05e-124">服务总线与基于声明的授权 - .Net</span><span class="sxs-lookup"><span data-stu-id="ae05e-124">Service Bus with Claims-Based Authorization - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

<span data-ttu-id="ae05e-125">查看 Azure 服务总线示例的[完整列表](https://azure.microsoft.com/resources/samples/?term=service+bus)。</span><span class="sxs-lookup"><span data-stu-id="ae05e-125">View the [complete list](https://azure.microsoft.com/resources/samples/?term=service+bus) of Azure Service Bus samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
