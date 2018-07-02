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
ms.openlocfilehash: 922e1a49a2b864d8cd408a8383d7cda27c7f89c2
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065297"
---
# <a name="azure-event-grid-libraries-for-net"></a><span data-ttu-id="6ff61-103">用于 .NET 的 Azure 事件网格库</span><span class="sxs-lookup"><span data-stu-id="6ff61-103">Azure Event Grid libraries for .NET</span></span>

<span data-ttu-id="6ff61-104">将简单的基于 HTTP 的事件处理与 Azure 事件网格配合使用，开发事件驱动型应用程序，以便侦听并响应来自 Azure 服务和自定义源的事件。</span><span class="sxs-lookup"><span data-stu-id="6ff61-104">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="6ff61-105">[详细了解](/azure/event-grid/overview) Azure 事件网格，通过 [Azure Blob 存储事件教程](/azure/storage/blobs/storage-blob-event-quickstart-powershell)来入门。</span><span class="sxs-lookup"><span data-stu-id="6ff61-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="6ff61-106">发布 SDK</span><span class="sxs-lookup"><span data-stu-id="6ff61-106">Publish SDK</span></span>

<span data-ttu-id="6ff61-107">创建事件，进行身份验证，然后使用 Azure 事件网格发布 SDK 将内容发布到主题。</span><span class="sxs-lookup"><span data-stu-id="6ff61-107">Create events, authenticate, and post to topics using the Azure Event Grid publish SDK.</span></span>

<span data-ttu-id="6ff61-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="6ff61-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6ff61-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="6ff61-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="6ff61-110">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6ff61-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="sample-usage"></a><span data-ttu-id="6ff61-111">示例用法</span><span class="sxs-lookup"><span data-stu-id="6ff61-111">Sample usage</span></span>

<span data-ttu-id="6ff61-112">以下代码通过 Azure 进行身份验证，然后将自定义类型（在此示例中为 `Contoso.Items.ItemsReceivedEvent`）的 `EventGridEvent` 事件的 `List` 发布到某个主题。</span><span class="sxs-lookup"><span data-stu-id="6ff61-112">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceivedEvent` ) to a topic.</span></span> <span data-ttu-id="6ff61-113">在示例中使用的主题密钥和终结点地址可以从 Azure PowerShell 检索：</span><span class="sxs-lookup"><span data-stu-id="6ff61-113">The topic key and endpoint address used in the sample can be retrieved from Azure PowerShell:</span></span>

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

<span data-ttu-id="6ff61-114">此代码片段处理在 [Azure 存储](/azure/storage/blobs/storage-blob-event-overview)中创建新 Blob 时发布的事件。</span><span class="sxs-lookup"><span data-stu-id="6ff61-114">This snippet handles events published when creating a new blob in [Azure Storage](/azure/storage/blobs/storage-blob-event-overview).</span></span>

```csharp
string response = string.Empty;
const string SubscriptionValidationEvent = "Microsoft.EventGrid.SubscriptionValidationEvent";
const string StorageBlobCreatedEvent = "Microsoft.Storage.BlobCreated";

string requestContent = await req.Content.ReadAsStringAsync();
EventGridEvent[] eventGridEvents = JsonConvert.DeserializeObject<EventGridEvent[]>(requestContent);

foreach (EventGridEvent eventGridEvent in eventGridEvents)
{
    JObject dataObject = eventGridEvent.Data as JObject;

    // Deserialize the event data into the appropriate type based on event type 
    if (string.Equals(eventGridEvent.EventType, SubscriptionValidationEvent, StringComparison.OrdinalIgnoreCase))
    {
        var eventData = dataObject.ToObject<SubscriptionValidationEventData>();
        log.Info($"Got SubscriptionValidation event data, validation code: {eventData.ValidationCode}, topic: {eventGridEvent.Topic}");

        // Do any additional validation (as required) and then return back the below response
        var responseData = new SubscriptionValidationResponseData();
        responseData.ValidationResponse = eventData.ValidationCode;
        return req.CreateResponse(HttpStatusCode.OK, responseData);
    }

    else if (string.Equals(eventGridEvent.EventType, StorageBlobCreatedEvent, StringComparison.OrdinalIgnoreCase))
    {
        var eventData = dataObject.ToObject<StorageBlobCreatedEventData>();
        log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ff61-115">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="6ff61-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="6ff61-116">管理 SDK</span><span class="sxs-lookup"><span data-stu-id="6ff61-116">Management SDK</span></span>

<span data-ttu-id="6ff61-117">使用管理 SDK 创建、更新或删除事件网格实例、主题和订阅。</span><span class="sxs-lookup"><span data-stu-id="6ff61-117">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

<span data-ttu-id="6ff61-118">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="6ff61-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6ff61-119">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="6ff61-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="6ff61-120">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6ff61-120">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ff61-121">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="6ff61-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="6ff61-122">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="6ff61-122">Learn more</span></span>

- [<span data-ttu-id="6ff61-123">使用事件网格 SDK 接收事件</span><span class="sxs-lookup"><span data-stu-id="6ff61-123">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
