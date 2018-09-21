---
title: 用于 .NET 的 Azure 事件网格库
description: 用于 .NET 的 Azure 事件网格库参考
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/16/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: event-grid
ms.custom: devcenter
ms.openlocfilehash: 894b8a5beaf0507ab50e8eed6a5ab20d10a71ba6
ms.sourcegitcommit: 61638b504b6c4d96b357894835c80c2680a99fe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750595"
---
# <a name="azure-event-grid-libraries-for-net"></a><span data-ttu-id="fbe47-103">用于 .NET 的 Azure 事件网格库</span><span class="sxs-lookup"><span data-stu-id="fbe47-103">Azure Event Grid libraries for .NET</span></span>

<span data-ttu-id="fbe47-104">将简单的基于 HTTP 的事件处理与 Azure 事件网格配合使用，开发事件驱动型应用程序，以便侦听并响应来自 Azure 服务和自定义源的事件。</span><span class="sxs-lookup"><span data-stu-id="fbe47-104">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="fbe47-105">[详细了解](/azure/event-grid/overview) Azure 事件网格，通过 [Azure Blob 存储事件教程](/azure/storage/blobs/storage-blob-event-quickstart-powershell)来入门。</span><span class="sxs-lookup"><span data-stu-id="fbe47-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="fbe47-106">客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="fbe47-106">Client SDK</span></span>

<span data-ttu-id="fbe47-107">使用 Azure 事件网格客户端 SDK 创建事件、进行身份验证以及发布到主题。</span><span class="sxs-lookup"><span data-stu-id="fbe47-107">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="fbe47-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="fbe47-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fbe47-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="fbe47-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="fbe47-110">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="fbe47-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="publish-events"></a><span data-ttu-id="fbe47-111">发布事件</span><span class="sxs-lookup"><span data-stu-id="fbe47-111">Publish events</span></span>

<span data-ttu-id="fbe47-112">以下代码通过 Azure 进行身份验证，然后将自定义类型（在此示例中为 `Contoso.Items.ItemsReceivedEvent`）的 `EventGridEvent` 事件的 `List` 发布到某个主题。</span><span class="sxs-lookup"><span data-stu-id="fbe47-112">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceivedEvent` ) to a topic.</span></span> <span data-ttu-id="fbe47-113">在示例中使用的主题密钥和终结点地址可以从 Azure PowerShell 检索：</span><span class="sxs-lookup"><span data-stu-id="fbe47-113">The topic key and endpoint address used in the sample can be retrieved from Azure PowerShell:</span></span>

```powershell
$endpoint = (Get-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Name <topic-name>).Endpoint
$keys = Get-AzureRmEventGridTopicKey -ResourceGroupName gridResourceGroup -Name <topic-name>
```

```csharp
string topicEndpoint = "https://<topic-name>.<region>-1.eventgrid.azure.net/api/events";
string topicKey = "<topic-key>";
string topicHostname = new Uri(topicEndpoint).Host;

TopicCredentials topicCredentials = new TopicCredentials(topicKey);
EventGridClient client = new EventGridClient(topicCredentials);

client.PublishEventsAsync(topicHostname, GetEventsList()).GetAwaiter().GetResult();
Console.Write("Published events to Event Grid.");

static IList<EventGridEvent> GetEventsList()
{
    List<EventGridEvent> eventsList = new List<EventGridEvent>();
    for (int i = 0; i < 1; i++)
    {
        eventsList.Add(new EventGridEvent()
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Contoso.Items.ItemReceivedEvent",
            Data = new ContosoItemReceivedEventData()
            {
                ItemUri = "ContosoSuperItemUri"
            },

            EventTime = DateTime.Now,
            Subject = "Door1",
            DataVersion = "2.0"
        });
    }
    return eventsList;
}
```

### <a name="consume-events"></a><span data-ttu-id="fbe47-114">使用事件</span><span class="sxs-lookup"><span data-stu-id="fbe47-114">Consume events</span></span>

<span data-ttu-id="fbe47-115">此代码片段使用多种事件，包括一个自定义事件 `Contoso.Items.ItemsReceived`，以及其他 Azure 服务（例如 Blob 存储）触发的事件。</span><span class="sxs-lookup"><span data-stu-id="fbe47-115">This snippet consumes events, including a custom event `Contoso.Items.ItemsReceived` as well as events triggered from other Azure services, such as Blob Storage.</span></span>

```csharp
string response = string.Empty;
string requestContent = await req.Content.ReadAsStringAsync();

EventGridSubscriber eventGridSubscriber = new EventGridSubscriber();

// Optionally add one or more custom event type mappings
eventGridSubscriber.AddOrUpdateCustomEventMapping("Contoso.Items.ItemReceived", typeof(ContosoItemReceivedEventData));

var events = eventGridSubscriber.DeserializeEventGridEvents(requestContent);            
 
foreach (EventGridEvent receivedEvent in events)
{
    if (receivedEvent.Data is SubscriptionValidationEventData)
    {
        SubscriptionValidationEventData eventData = (SubscriptionValidationEventData)receivedEvent.Data;
        log.Info($"Got SubscriptionValidation event data, validationCode: {eventData.ValidationCode},  validationUrl: {eventData.ValidationUrl}, topic: {eventGridEvent.Topic}");
        // Handle subscription validation
    }
    else if (receivedEvent.Data is StorageBlobCreatedEventData)
    {
        StorageBlobCreatedEventData eventData = (StorageBlobCreatedEventData)receivedEvent.Data;
        log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
        // Handle StorageBlobCreatedEventData
    }
    else if (receivedEvent.Data is ContosoItemReceivedEventData)
    {
        ContosoItemReceivedEventData eventData = (ContosoItemReceivedEventData)receivedEvent.Data;
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbe47-116">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="fbe47-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="fbe47-117">管理 SDK</span><span class="sxs-lookup"><span data-stu-id="fbe47-117">Management SDK</span></span>

<span data-ttu-id="fbe47-118">使用管理 SDK 创建、更新或删除事件网格实例、主题和订阅。</span><span class="sxs-lookup"><span data-stu-id="fbe47-118">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

<span data-ttu-id="fbe47-119">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="fbe47-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fbe47-120">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="fbe47-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="fbe47-121">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="fbe47-121">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbe47-122">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="fbe47-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="fbe47-123">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="fbe47-123">Learn more</span></span>

- [<span data-ttu-id="fbe47-124">使用事件网格 SDK 接收事件</span><span class="sxs-lookup"><span data-stu-id="fbe47-124">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
