---
title: 用于 .NET 的 Azure 事件中心库
description: 用于 .NET 的 Azure 事件中心库参考
keywords: Azure, .NET, SDK, API, 事件中心
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: event-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2ec234959ffc46d2399d1c763e05f173a311b0d2
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487290"
---
# <a name="azure-event-hubs-libraries-for-net"></a><span data-ttu-id="98380-104">用于 .NET 的 Azure 事件中心库</span><span class="sxs-lookup"><span data-stu-id="98380-104">Azure Event Hubs libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="98380-105">概述</span><span class="sxs-lookup"><span data-stu-id="98380-105">Overview</span></span>

<span data-ttu-id="98380-106">Azure 事件中心是高度可缩放的数据流式处理平台和事件引入服务。</span><span class="sxs-lookup"><span data-stu-id="98380-106">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service.</span></span>

<span data-ttu-id="98380-107">若要详细了解 Azure 事件中心，请阅读[什么是事件中心？](/azure/event-hubs/event-hubs-what-is-event-hubs)一文。</span><span class="sxs-lookup"><span data-stu-id="98380-107">To learn more about Azure Event Hubs, read the article [What is Event Hubs?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>  <span data-ttu-id="98380-108">若要开始使用，请查看[事件中心编程指南](/azure/event-hubs/event-hubs-programming-guide)。</span><span class="sxs-lookup"><span data-stu-id="98380-108">To get started, check out the [Event Hubs Programming Guide](/azure/event-hubs/event-hubs-programming-guide).</span></span>

## <a name="client-library"></a><span data-ttu-id="98380-109">客户端库</span><span class="sxs-lookup"><span data-stu-id="98380-109">Client library</span></span>

<span data-ttu-id="98380-110">使用事件中心客户端可与事件中心来回发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="98380-110">Use the Event Hubs client to send and receive messages to and from Event Hubs.</span></span>

<span data-ttu-id="98380-111">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.EventHubs)。</span><span class="sxs-lookup"><span data-stu-id="98380-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="98380-112">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="98380-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a><span data-ttu-id="98380-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="98380-113">Code Example</span></span>

<span data-ttu-id="98380-114">以下代码创建事件中心客户端并将消息发送到中心。</span><span class="sxs-lookup"><span data-stu-id="98380-114">The following code creates an Event Hubs client and sends a message to the hub.</span></span>

```csharp
EventHubsConnectionStringBuilder connectionStringBuilder = new EventHubsConnectionStringBuilder(eventHubConnectionString)
{
    EntityPath = eventHubEntityPath
};

EventHubClient eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
string message = $"Message {i}";
Console.WriteLine($"Sending message: {message}");
await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="98380-115">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="98380-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a><span data-ttu-id="98380-116">管理库</span><span class="sxs-lookup"><span data-stu-id="98380-116">Management library</span></span>

<span data-ttu-id="98380-117">使用事件中心管理库可创建、更新和删除中心与使用者组。</span><span class="sxs-lookup"><span data-stu-id="98380-117">Use the Event Hubs management library to create, update, and remove hubs and consumer groups.</span></span>

<span data-ttu-id="98380-118">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub)。</span><span class="sxs-lookup"><span data-stu-id="98380-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="98380-119">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="98380-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a><span data-ttu-id="98380-120">代码示例</span><span class="sxs-lookup"><span data-stu-id="98380-120">Code Example</span></span>

<span data-ttu-id="98380-121">以下代码创建新的事件中心。</span><span class="sxs-lookup"><span data-stu-id="98380-121">The following code creates a new event hub.</span></span>

```csharp
TokenCredentials creds = new TokenCredentials(token);
EventHubManagementClient ehClient = new EventHubManagementClient(creds)
{
    SubscriptionId = subscriptionId
};

EventHubCreateOrUpdateParameters ehParams = new EventHubCreateOrUpdateParameters()
{
    Location = location
};

Console.WriteLine("Creating Event Hub...");
await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
Console.WriteLine("Created Event Hub successfully.");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="98380-122">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="98380-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a><span data-ttu-id="98380-123">教程</span><span class="sxs-lookup"><span data-stu-id="98380-123">Tutorials</span></span>

* [<span data-ttu-id="98380-124">使用 .NET Framework 将事件发送到 Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="98380-124">Send events to Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [<span data-ttu-id="98380-125">使用 .NET Framework 从 Azure 事件中心接收事件</span><span class="sxs-lookup"><span data-stu-id="98380-125">Receive events from Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a><span data-ttu-id="98380-126">示例</span><span class="sxs-lookup"><span data-stu-id="98380-126">Samples</span></span>

* [<span data-ttu-id="98380-127">Azure 事件中心示例</span><span class="sxs-lookup"><span data-stu-id="98380-127">Azure Event Hubs Samples</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="98380-128">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="98380-128">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
