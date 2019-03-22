---
title: 用于 .NET 的 Azure 通知中心库
description: 用于 .NET 的 Azure 通知中心库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: notification-hubs
ms.openlocfilehash: 750a51e8dfa7323f6afb54735b4bfc517f9ec15f
ms.sourcegitcommit: 4b68c73652cb7e44cf4db36f70cb33a17dd863ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58085834"
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="d2ae3-103">用于 .NET 的 Azure 通知中心库</span><span class="sxs-lookup"><span data-stu-id="d2ae3-103">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="d2ae3-104">Azure 通知中心提供易用的多平台扩展式推送引擎。</span><span class="sxs-lookup"><span data-stu-id="d2ae3-104">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="d2ae3-105">使用单个跨平台 API 调用，即可轻松地从任意云或本地后端向任意移动平台发送有针对性的个性化推送通知。</span><span class="sxs-lookup"><span data-stu-id="d2ae3-105">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="d2ae3-106">客户端库</span><span class="sxs-lookup"><span data-stu-id="d2ae3-106">Client library</span></span>

<span data-ttu-id="d2ae3-107">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)。</span><span class="sxs-lookup"><span data-stu-id="d2ae3-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="d2ae3-108">[Azure 通知中心 NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)现在支持 .NET Standard，以允许在通知中心后端使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="d2ae3-108">The [Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d2ae3-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="d2ae3-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="d2ae3-110">代码示例</span><span class="sxs-lookup"><span data-stu-id="d2ae3-110">Code Example</span></span>

<span data-ttu-id="d2ae3-111">此示例连接到通知中心，并发送 Windows 推送通知服务 (WNS) 消息。</span><span class="sxs-lookup"><span data-stu-id="d2ae3-111">This example connects to a Notification Hub and sends a Windows Push Notification Service (WNS) message.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2ae3-112">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="d2ae3-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)

## <a name="management-library"></a><span data-ttu-id="d2ae3-113">管理库</span><span class="sxs-lookup"><span data-stu-id="d2ae3-113">Management library</span></span>

<span data-ttu-id="d2ae3-114">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs)。</span><span class="sxs-lookup"><span data-stu-id="d2ae3-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d2ae3-115">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="d2ae3-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2ae3-116">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="d2ae3-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="d2ae3-117">示例</span><span class="sxs-lookup"><span data-stu-id="d2ae3-117">Samples</span></span>

- [<span data-ttu-id="d2ae3-118">Windows Universal 入门</span><span class="sxs-lookup"><span data-stu-id="d2ae3-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
