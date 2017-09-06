---
title: "用于 .NET 的 Azure 服务总线库"
description: "用于 .NET 的 Azure 服务总线库参考"
keywords: "Azure, .NET, SDK, API, 服务总线"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/01/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: d4d3ac982794fc7533b97fe8c053730b4b39ff58
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-bus-libraries-for-net"></a>用于 .NET 的 Azure 服务总线库

## <a name="overview"></a>概述

[Azure 服务总线](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)是位于各个应用程序之间的消息传送基础结构，允许应用程序交换消息，从而扩大规模并提高恢复能力。

## <a name="client-library"></a>客户端库

直接从 Visual Studio [包管理器控制台][PackageManager]安装 [NuGet 包](https://www.nuget.org/packages/WindowsAzure.ServiceBus)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package WindowsAzure.ServiceBus
```

### <a name="code-example"></a>代码示例

此示例向服务总线队列发送消息。

```csharp
// using Microsoft.ServiceBus.Messaging;

QueueClient client = QueueClient.CreateFromConnectionString(connectionString, queueName);
BrokeredMessage message = new BrokeredMessage("This is a test message!");
client.Send(message);
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a>管理库

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a>代码示例

此示例创建最大大小为 1024 MB 的服务总线队列。

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
> [了解管理 API](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a>示例

- [服务总线队列基础知识 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [服务总线队列高级功能 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [服务总线发布/订阅基础知识 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [服务总线发布/订阅高级功能 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [服务总线与基于声明的授权 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

查看 Azure 服务总线示例的[完整列表](https://azure.microsoft.com/resources/samples/?term=service+bus)。


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
