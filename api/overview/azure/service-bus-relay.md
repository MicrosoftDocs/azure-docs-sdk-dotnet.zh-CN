---
title: 用于 .NET 的 Azure 服务总线中继库
description: 用于 .NET 的 Azure 服务总线中继库参考
keywords: Azure, .NET, SDK, API, 服务总线中继
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 1a869d5939e357c98ec417e6474f711b9ac8c466
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566158"
---
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="958a9-104">用于 .NET 的 Azure 服务总线中继库</span><span class="sxs-lookup"><span data-stu-id="958a9-104">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="958a9-105">概述</span><span class="sxs-lookup"><span data-stu-id="958a9-105">Overview</span></span>

<span data-ttu-id="958a9-106">Azure 中继服务通过允许安全地向公有云公开位于企业网络内的服务来创建混合应用程序，无需打开防火墙连接，也无需对企业网络基础结构进行彻底更改。</span><span class="sxs-lookup"><span data-stu-id="958a9-106">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="958a9-107">中继支持各种不同的传输协议和 Web 服务标准。</span><span class="sxs-lookup"><span data-stu-id="958a9-107">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="958a9-108">[详细了解 Azure 中继](/azure/service-bus-relay/relay-what-is-it)。</span><span class="sxs-lookup"><span data-stu-id="958a9-108">Learn more about [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="958a9-109">客户端库</span><span class="sxs-lookup"><span data-stu-id="958a9-109">Client library</span></span>

<span data-ttu-id="958a9-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Relay)。</span><span class="sxs-lookup"><span data-stu-id="958a9-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="958a9-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="958a9-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="958a9-112">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="958a9-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="958a9-113">示例</span><span class="sxs-lookup"><span data-stu-id="958a9-113">Samples</span></span>

<span data-ttu-id="958a9-114">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="958a9-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package