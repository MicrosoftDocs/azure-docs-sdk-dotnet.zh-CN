---
title: 用于 .NET 的 Azure 服务总线中继库
description: 用于 .NET 的 Azure 服务总线中继库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus
ms.openlocfilehash: 75c481ab23e461c5194a9eeb0ca668af98f4d2d7
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189980"
---
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="1910a-103">用于 .NET 的 Azure 服务总线中继库</span><span class="sxs-lookup"><span data-stu-id="1910a-103">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="1910a-104">概述</span><span class="sxs-lookup"><span data-stu-id="1910a-104">Overview</span></span>

<span data-ttu-id="1910a-105">Azure 中继服务通过允许安全地向公有云公开位于企业网络内的服务来创建混合应用程序，无需打开防火墙连接，也无需对企业网络基础结构进行彻底更改。</span><span class="sxs-lookup"><span data-stu-id="1910a-105">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="1910a-106">中继支持各种不同的传输协议和 Web 服务标准。</span><span class="sxs-lookup"><span data-stu-id="1910a-106">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="1910a-107">[详细了解 Azure 中继](/azure/service-bus-relay/relay-what-is-it)。</span><span class="sxs-lookup"><span data-stu-id="1910a-107">Learn more about [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="1910a-108">客户端库</span><span class="sxs-lookup"><span data-stu-id="1910a-108">Client library</span></span>

<span data-ttu-id="1910a-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Relay)。</span><span class="sxs-lookup"><span data-stu-id="1910a-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="1910a-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="1910a-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1910a-111">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="1910a-111">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="1910a-112">示例</span><span class="sxs-lookup"><span data-stu-id="1910a-112">Samples</span></span>

<span data-ttu-id="1910a-113">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="1910a-113">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package