---
title: 用于 .NET 的 Azure 通知中心库
description: 用于 .NET 的 Azure 通知中心库参考
keywords: Azure, .NET, SDK, API, 通知中心
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: notification-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f863bf9d5d63129e04dd31ba96b3e803bead87bc
ms.sourcegitcommit: 4c42de7e066b6aa0a5b5df02cce4d1d245aa558d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
ms.locfileid: "31447634"
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="ef73e-104">用于 .NET 的 Azure 通知中心库</span><span class="sxs-lookup"><span data-stu-id="ef73e-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="ef73e-105">Azure 通知中心提供易用的多平台扩展式推送引擎。</span><span class="sxs-lookup"><span data-stu-id="ef73e-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="ef73e-106">使用单个跨平台 API 调用，即可轻松地从任意云或本地后端向任意移动平台发送有针对性的个性化推送通知。</span><span class="sxs-lookup"><span data-stu-id="ef73e-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="ef73e-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="ef73e-107">Client library</span></span>

<span data-ttu-id="ef73e-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)。</span><span class="sxs-lookup"><span data-stu-id="ef73e-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="ef73e-109">[NuGet 包的新预览版](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1)现在支持 .NET Standard，以允许将 .NET Core 用于通知中心的后端使用</span><span class="sxs-lookup"><span data-stu-id="ef73e-109">A [new preview version of the NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ef73e-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="ef73e-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="ef73e-111">代码示例</span><span class="sxs-lookup"><span data-stu-id="ef73e-111">Code Example</span></span>

<span data-ttu-id="ef73e-112">此示例连接到通知中心，并发送 Windows 推送通知服务 (WNS) 消息。</span><span class="sxs-lookup"><span data-stu-id="ef73e-112">This example connects to a Notification Hub and sends a Windows Push Notification Service (WNS) message.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef73e-113">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="ef73e-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="ef73e-114">管理库</span><span class="sxs-lookup"><span data-stu-id="ef73e-114">Management library</span></span>

<span data-ttu-id="ef73e-115">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs)。</span><span class="sxs-lookup"><span data-stu-id="ef73e-115">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ef73e-116">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="ef73e-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef73e-117">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="ef73e-117">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="ef73e-118">示例</span><span class="sxs-lookup"><span data-stu-id="ef73e-118">Samples</span></span>

- [<span data-ttu-id="ef73e-119">Windows Universal 入门</span><span class="sxs-lookup"><span data-stu-id="ef73e-119">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
