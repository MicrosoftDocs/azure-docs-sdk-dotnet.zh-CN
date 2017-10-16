---
title: "有关在 Azure 上的 .NET 中使用消息传送和 IoT 的教程 | Microsoft Docs"
description: "使用 .NET 和 Azure 服务在云应用程序之间以及设备与云之间发送消息。"
author: camsoper
manager: douge
ms.assetid: 2ce6ea06-7b0b-45e6-8ca0-44e4e4030b82
ms.devlang: dotnet
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: casoper
ms.openlocfilehash: 0c3e81231ac88b2418778b83ecabcbb553608e24
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="net-tutorials-for-enterprise-messaging-and-internet-of-things-iot"></a>企业消息传送和物联网 (IoT) 的 .NET 教程

下表提供了有关使用 Azure 服务通过 .NET 代码在应用程序与设备之间发送和读取消息的深入教程的链接。

有关示例源代码，请参阅 [Azure 服务示例](https://azure.microsoft.com/resources/samples/?platform=dotnet)列表。


| | |
|---|---|
| **服务总线** | |
| [如何使用服务总线队列][1] | 创建队列、发送和接收消息，以及删除队列。 | 
| [如何使用服务总线主题和订阅][2] | 了解如何使用服务总线的发布/订阅通信模型。
| [使用 AMQP 1.0 通过 .NET 使用服务总线][3] | 了解如何在服务总线应用程序中使用 AMQP。
|**IoT 中心**|
| [将模拟设备连接到 IoT 中心][4] | 通过 IoT 中心创建设备标识、发送消息和处理遥测数据。 |   
| [处理设备到云的消息][5] | 从模拟设备发送消息并在云中处理消息。 |
|**事件中心**|
| [将事件发送到事件中心][6] | 通过控制台应用程序将事件发送到事件中心。
| [从事件中心接收事件][7] | 同时接收和处理消息。


[1]: /azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues
[2]: /azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions
[3]: /azure/service-bus-messaging/service-bus-amqp-dotnet
[4]: /azure/iot-hub/iot-hub-csharp-csharp-getstarted
[5]: /azure/iot-hub/iot-hub-csharp-csharp-process-d2c
[6]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-send
[7]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph

