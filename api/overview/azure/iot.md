---
title: "用于 .NET 的 Azure IoT 库"
description: "用于 .NET 的 Azure IoT 库参考"
keywords: Azure, .NET, SDK, API, IoT
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: iot-hub
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 0fa4121becd0d5bd646077a9644a651903c43348
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
---
# <a name="azure-iot-libraries-for-net"></a>用于 .NET 的 Azure IoT 库

## <a name="overview"></a>概述

[Azure IoT 中心](https://azure.microsoft.com/services/iot-hub/)是一个完全托管的服务，可在数百万台设备和一个解决方案后端之间实现安全可靠的双向通信。

IoT 解决方案中的设备和数据源既包括简单的联网传感器，也包括功能强大的独立计算设备。 设备的处理能力、内存、通信带宽和通信协议支持可能存在限制。 使用 IoT [设备 SDK](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) 可以实施各种设备的客户端应用程序和后端应用程序。

用于 .NET 的设备 SDK 可帮助构建运行 .NET 的、与 Azure IoT 中心相连接的设备。

用于 .NET 的服务 SDK 可帮助构建使用 .NET 的、可从云中管理和允许运行控制设备的后端应用程序。

[详细了解 Azure IoT](https://docs.microsoft.com/azure/iot-hub/)。


## <a name="client-library"></a>客户端库

使用 .NET IoT 设备客户端可以连接到 IoT 中心并向其发送消息。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a>代码示例 

此示例连接到 IoT 中心，并每秒发送一条消息。

```csharp
string deviceKey = "<deviceKey>";
string deviceId = "<deviceId>";
string iotHubHostName = "<IoTHubHostname>";
DeviceAuthenticationWithRegistrySymmetricKeyvar deviceAuthentication = new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceKey);

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
> [了解客户端 API](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a>示例

- [Web 服务到事件中心的常规方案](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

查看 Azure IoT 升频的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub)。

查看 [Azure IoT 中心开发人员指南](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide)获取更多指导。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
