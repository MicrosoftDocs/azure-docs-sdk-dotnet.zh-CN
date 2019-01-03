---
title: 用于 .NET 的 Azure IoT 库
description: 用于 .NET 的 Azure IoT 库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: iot-hub
ms.openlocfilehash: 667663c5f5e3452fcc5ec0c4f3ded997370c5852
ms.sourcegitcommit: 7f1a1bf275d8489f8df266b746baa33d66fcb2c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2018
ms.locfileid: "53737072"
---
# <a name="azure-iot-libraries-for-net"></a><span data-ttu-id="d4897-103">用于 .NET 的 Azure IoT 库</span><span class="sxs-lookup"><span data-stu-id="d4897-103">Azure IoT libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d4897-104">概述</span><span class="sxs-lookup"><span data-stu-id="d4897-104">Overview</span></span>

<span data-ttu-id="d4897-105">[Azure IoT 中心](https://azure.microsoft.com/services/iot-hub/)是一个完全托管的服务，可在数百万台设备和一个解决方案后端之间实现安全可靠的双向通信。</span><span class="sxs-lookup"><span data-stu-id="d4897-105">[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="d4897-106">IoT 解决方案中的设备和数据源既包括简单的联网传感器，也包括功能强大的独立计算设备。</span><span class="sxs-lookup"><span data-stu-id="d4897-106">Devices and data sources in an IoT solution can range from a simple network-connected sensor to a powerful, standalone computing device.</span></span> <span data-ttu-id="d4897-107">设备的处理能力、内存、通信带宽和通信协议支持可能存在限制。</span><span class="sxs-lookup"><span data-stu-id="d4897-107">Devices may have limited processing capability, memory, communication bandwidth, and communication protocol support.</span></span> <span data-ttu-id="d4897-108">使用 IoT [设备 SDK](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) 可以实施各种设备的客户端应用程序和后端应用程序。</span><span class="sxs-lookup"><span data-stu-id="d4897-108">The IoT [device SDKs](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) enable you to implement client applications for a wide variety of devices and back-end applications.</span></span>

<span data-ttu-id="d4897-109">用于 .NET 的设备 SDK 可帮助构建运行 .NET 的、与 Azure IoT 中心相连接的设备。</span><span class="sxs-lookup"><span data-stu-id="d4897-109">The device SDK for .NET facilitates building devices running .NET that connect to Azure IoT Hub.</span></span>

<span data-ttu-id="d4897-110">用于 .NET 的服务 SDK 可帮助构建使用 .NET 的、可从云中管理和允许运行控制设备的后端应用程序。</span><span class="sxs-lookup"><span data-stu-id="d4897-110">The service SDK for .NET facilitates building back-end applications using .NET that manage and allow controlling devices from the Cloud.</span></span>

<span data-ttu-id="d4897-111">[详细了解 Azure IoT](https://docs.microsoft.com/azure/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="d4897-111">[Learn more about Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span></span>


## <a name="client-library"></a><span data-ttu-id="d4897-112">客户端库</span><span class="sxs-lookup"><span data-stu-id="d4897-112">Client library</span></span>

<span data-ttu-id="d4897-113">使用 .NET IoT 设备客户端可以连接到 IoT 中心并向其发送消息。</span><span class="sxs-lookup"><span data-stu-id="d4897-113">Use the .NET IoT devices client to connect and send messages to your IoT Hub.</span></span>

<span data-ttu-id="d4897-114">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client)。</span><span class="sxs-lookup"><span data-stu-id="d4897-114">Install the [NuGet package]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d4897-115">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="d4897-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a><span data-ttu-id="d4897-116">代码示例</span><span class="sxs-lookup"><span data-stu-id="d4897-116">Code Examples</span></span> 

<span data-ttu-id="d4897-117">此示例连接到 IoT 中心，并每秒发送一条消息。</span><span class="sxs-lookup"><span data-stu-id="d4897-117">This example connects to the IoT Hub and sends one message per second.</span></span>

```csharp
string deviceKey = "<deviceKey>";
string deviceId = "<deviceId>";
string iotHubHostName = "<IoTHubHostname>";
var deviceAuthentication = new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceKey);

DeviceClient deviceClient = DeviceClient.Create(iotHubHostName, deviceAuthentication, TransportType.Mqtt);

while (true)
{
    double currentTemperature = 20 + Rand.NextDouble() * 15;
    double currentHumidity = 60 + Rand.NextDouble() * 20;

    var telemetryDataPoint = new
    {
        messageId = _messageId++,
        deviceId = deviceId,
        temperature = currentTemperature,
        humidity = currentHumidity
    };
    string messageString = JsonConvert.SerializeObject(telemetryDataPoint);
    Message message = new Message(Encoding.ASCII.GetBytes(messageString));
    message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

    await deviceClient.SendEventAsync(message);
    Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

    await Task.Delay(1000);
}
```


> [!div class="nextstepaction"]
> [<span data-ttu-id="d4897-118">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="d4897-118">Explore the client APIs</span></span>](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a><span data-ttu-id="d4897-119">示例</span><span class="sxs-lookup"><span data-stu-id="d4897-119">Samples</span></span>

- [<span data-ttu-id="d4897-120">Web 服务到事件中心的常规方案</span><span class="sxs-lookup"><span data-stu-id="d4897-120">Generic Web Service to Event Hub scenario</span></span>](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

<span data-ttu-id="d4897-121">查看 Azure IoT 升频的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub)。</span><span class="sxs-lookup"><span data-stu-id="d4897-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) of Azure IoT Upsamples.</span></span>

<span data-ttu-id="d4897-122">查看 [Azure IoT 中心开发人员指南](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide)获取更多指导。</span><span class="sxs-lookup"><span data-stu-id="d4897-122">View the [Azure IoT Hub developer guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) for more guidance.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
