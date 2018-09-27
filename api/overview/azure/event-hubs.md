---
title: 用于 .NET 的 Azure 事件中心库
description: 用于 .NET 的 Azure 事件中心库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: event-hubs
ms.openlocfilehash: 74c533bef598b90369009d68a759d35d122a368d
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190270"
---
# <a name="azure-event-hubs-libraries-for-net"></a>用于 .NET 的 Azure 事件中心库

## <a name="overview"></a>概述

Azure 事件中心是高度可缩放的数据流式处理平台和事件引入服务。

若要详细了解 Azure 事件中心，请阅读[什么是事件中心？](/azure/event-hubs/event-hubs-what-is-event-hubs)一文。  若要开始使用，请查看[事件中心编程指南](/azure/event-hubs/event-hubs-programming-guide)。

## <a name="client-library"></a>客户端库

使用事件中心客户端可与事件中心来回发送和接收消息。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.EventHubs)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a>代码示例

以下代码创建事件中心客户端并将消息发送到中心。

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
> [了解客户端 API](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a>管理库

使用事件中心管理库可创建、更新和删除中心与使用者组。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a>代码示例

以下代码创建新的事件中心。

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
> [了解管理 API](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a>教程

* [使用 .NET Framework 将事件发送到 Azure 事件中心](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [使用 .NET Framework 从 Azure 事件中心接收事件](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a>示例

* [Azure 事件中心示例](https://github.com/Azure/azure-event-hubs/tree/master/samples)

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
