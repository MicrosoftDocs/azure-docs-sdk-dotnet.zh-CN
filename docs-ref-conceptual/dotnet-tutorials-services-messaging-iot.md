---
title: 有关在 Azure 上的 .NET 中使用消息传送和 IoT 的教程 | Microsoft Docs
description: 使用 .NET 和 Azure 服务在云应用程序之间以及设备与云之间发送消息。
ms.date: 10/19/2017
ms.openlocfilehash: 92cb78b34706a453630dbf36913d53400962ff25
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190770"
---
# <a name="net-tutorials-for-enterprise-messaging-and-internet-of-things-iot"></a><span data-ttu-id="897f8-103">企业消息传送和物联网 (IoT) 的 .NET 教程</span><span class="sxs-lookup"><span data-stu-id="897f8-103">.NET tutorials for enterprise messaging and Internet of Things (IoT)</span></span>

<span data-ttu-id="897f8-104">下表提供了有关使用 Azure 服务通过 .NET 代码在应用程序与设备之间发送和读取消息的深入教程的链接。</span><span class="sxs-lookup"><span data-stu-id="897f8-104">The following table links to in-depth tutorials for sending and reading messages between applications and devices in from your .NET code using Azure services.</span></span>

<span data-ttu-id="897f8-105">有关示例源代码，请参阅 [Azure 服务示例](https://azure.microsoft.com/resources/samples/?platform=dotnet)列表。</span><span class="sxs-lookup"><span data-stu-id="897f8-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>


| | |
|---|---|
| <span data-ttu-id="897f8-106">**服务总线**</span><span class="sxs-lookup"><span data-stu-id="897f8-106">**Service Bus**</span></span> | |
| <span data-ttu-id="897f8-107">[如何使用服务总线队列][1]</span><span class="sxs-lookup"><span data-stu-id="897f8-107">[How to use Service Bus queues][1]</span></span> | <span data-ttu-id="897f8-108">创建队列、发送和接收消息，以及删除队列。</span><span class="sxs-lookup"><span data-stu-id="897f8-108">Create queues, send and receive messages, and delete queues.</span></span> | 
| <span data-ttu-id="897f8-109">[如何使用服务总线主题和订阅][2]</span><span class="sxs-lookup"><span data-stu-id="897f8-109">[How to use Service Bus topics and subscriptions][2]</span></span> | <span data-ttu-id="897f8-110">了解如何使用服务总线的发布/订阅通信模型。</span><span class="sxs-lookup"><span data-stu-id="897f8-110">Learn how to use publish/subscribe communication model with Service Bus.</span></span>
| <span data-ttu-id="897f8-111">[使用 AMQP 1.0 通过 .NET 使用服务总线][3]</span><span class="sxs-lookup"><span data-stu-id="897f8-111">[Using Service Bus from .NET with AMQP 1.0][3]</span></span> | <span data-ttu-id="897f8-112">了解如何在服务总线应用程序中使用 AMQP。</span><span class="sxs-lookup"><span data-stu-id="897f8-112">Learn how to use AMQP in you Service Bus applications.</span></span>
|<span data-ttu-id="897f8-113">**IoT 中心**</span><span class="sxs-lookup"><span data-stu-id="897f8-113">**IoT Hub**</span></span>|
| <span data-ttu-id="897f8-114">[将模拟设备连接到 IoT 中心][4]</span><span class="sxs-lookup"><span data-stu-id="897f8-114">[Connect a simulated device to your IoT Hub][4]</span></span> | <span data-ttu-id="897f8-115">通过 IoT 中心创建设备标识、发送消息和处理遥测数据。</span><span class="sxs-lookup"><span data-stu-id="897f8-115">Create a device identity, send messages, and process telemetry from your IoT Hub.</span></span> |   
| <span data-ttu-id="897f8-116">[处理设备到云的消息][5]</span><span class="sxs-lookup"><span data-stu-id="897f8-116">[Process device-to-cloud messages][5]</span></span> | <span data-ttu-id="897f8-117">从模拟设备发送消息并在云中处理消息。</span><span class="sxs-lookup"><span data-stu-id="897f8-117">Send messages from a simulated device and process them in the cloud.</span></span> |
|<span data-ttu-id="897f8-118">**事件中心**</span><span class="sxs-lookup"><span data-stu-id="897f8-118">**Event Hub**</span></span>|
| <span data-ttu-id="897f8-119">[将事件发送到事件中心][6]</span><span class="sxs-lookup"><span data-stu-id="897f8-119">[Send events to an Event Hub][6]</span></span> | <span data-ttu-id="897f8-120">通过控制台应用程序将事件发送到事件中心。</span><span class="sxs-lookup"><span data-stu-id="897f8-120">Send events to Event hub from a console application.</span></span>
| <span data-ttu-id="897f8-121">[从事件中心接收事件][7]</span><span class="sxs-lookup"><span data-stu-id="897f8-121">[Receive events from Event Hubs][7]</span></span> | <span data-ttu-id="897f8-122">同时接收和处理消息。</span><span class="sxs-lookup"><span data-stu-id="897f8-122">Receive messages and process them in parallel.</span></span>


[1]: /azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues
[2]: /azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions
[3]: /azure/service-bus-messaging/service-bus-amqp-dotnet
[4]: /azure/iot-hub/iot-hub-csharp-csharp-getstarted
[5]: /azure/iot-hub/iot-hub-csharp-csharp-process-d2c
[6]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-send
[7]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph


