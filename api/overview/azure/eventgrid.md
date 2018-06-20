---
title: 用于 .NET 的 Azure 事件网格库
description: 用于 .NET 的 Azure 事件网格库参考
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/16/2018
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: event-grid
ms.custom: devcenter
ms.openlocfilehash: aa25f76f041e890de512c67d9380903f81216f62
ms.sourcegitcommit: 9f54e3334fc35c1066d0c591ff85b16d46416aa8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
ms.locfileid: "33802744"
---
# <a name="azure-event-grid-libraries-for-net"></a>用于 .NET 的 Azure 事件网格库

将简单的基于 HTTP 的事件处理与 Azure 事件网格配合使用，开发事件驱动型应用程序，以便侦听并响应来自 Azure 服务和自定义源的事件。

[详细了解](/azure/event-grid/overview) Azure 事件网格，通过 [Azure Blob 存储事件教程](/azure/storage/blobs/storage-blob-event-quickstart-powershell)来入门。 

## <a name="publish-sdk"></a>发布 SDK

创建事件，进行身份验证，然后使用 Azure 事件网格发布 SDK 将内容发布到主题。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="sample-usage"></a>示例用法

以下代码通过 Azure 进行身份验证，然后将自定义类型（在此示例中为 `Contoso.Items.ItemsReceivedEvent`）的 `EventGridEvent` 事件的 `List` 发布到某个主题。 在示例中使用的主题密钥和终结点地址可以从 Azure PowerShell 检索：

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

此代码片段处理在 [Azure 存储](/azure/storage/blobs/storage-blob-event-overview)中创建新 Blob 时发布的事件。

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
> [了解客户端 API](/dotnet/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>管理 SDK

使用管理 SDK 创建、更新或删除事件网格实例、主题和订阅。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)。


#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>了解详细信息

- [使用事件网格 SDK 接收事件](/azure/event-grid/receive-events)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
