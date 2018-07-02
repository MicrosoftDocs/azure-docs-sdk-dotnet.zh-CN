---
title: 用于 .NET 的 Azure 服务总线中继库
description: 用于 .NET 的 Azure 服务总线中继库参考
keywords: Azure, .NET, SDK, API, 服务总线中继
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e0dd9c9b0a187fe6ca81d764e60afd00cbaab654
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065947"
---
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="0679b-104">用于 .NET 的 Azure 服务总线中继库</span><span class="sxs-lookup"><span data-stu-id="0679b-104">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0679b-105">概述</span><span class="sxs-lookup"><span data-stu-id="0679b-105">Overview</span></span>

<span data-ttu-id="0679b-106">Azure 中继服务通过允许安全地向公有云公开位于企业网络内的服务来创建混合应用程序，无需打开防火墙连接，也无需对企业网络基础结构进行彻底更改。</span><span class="sxs-lookup"><span data-stu-id="0679b-106">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="0679b-107">中继支持各种不同的传输协议和 Web 服务标准。</span><span class="sxs-lookup"><span data-stu-id="0679b-107">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="0679b-108">[详细了解 Azure 中继](/azure/service-bus-relay/relay-what-is-it)。</span><span class="sxs-lookup"><span data-stu-id="0679b-108">Learn more about [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="0679b-109">客户端库</span><span class="sxs-lookup"><span data-stu-id="0679b-109">Client library</span></span>

<span data-ttu-id="0679b-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Relay)。</span><span class="sxs-lookup"><span data-stu-id="0679b-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0679b-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="0679b-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0679b-112">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="0679b-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="0679b-113">示例</span><span class="sxs-lookup"><span data-stu-id="0679b-113">Samples</span></span>

<span data-ttu-id="0679b-114">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="0679b-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package