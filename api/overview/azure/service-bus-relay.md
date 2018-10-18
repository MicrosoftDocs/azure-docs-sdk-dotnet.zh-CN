---
title: 用于 .NET 的 Azure 服务总线中继库
description: 用于 .NET 的 Azure 服务总线中继库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus-relay
ms.openlocfilehash: 9190e8efdebe1c352b4fb2c98be189089b0975d2
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348119"
---
# <a name="azure-service-bus-relay-libraries-for-net"></a>用于 .NET 的 Azure 服务总线中继库

## <a name="overview"></a>概述

Azure 中继服务通过允许安全地向公有云公开位于企业网络内的服务来创建混合应用程序，无需打开防火墙连接，也无需对企业网络基础结构进行彻底更改。 中继支持各种不同的传输协议和 Web 服务标准。
          
[详细了解 Azure 中继](/azure/service-bus-relay/relay-what-is-it)。

## <a name="client-library"></a>客户端库

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Relay)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a>示例

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package