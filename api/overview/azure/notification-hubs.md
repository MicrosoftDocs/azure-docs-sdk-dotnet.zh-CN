---
title: "用于 .NET 的 Azure 通知中心库"
description: "用于 .NET 的 Azure 通知中心库参考"
keywords: "Azure, .NET, SDK, API, 通知中心"
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
ms.openlocfilehash: 9fd49ccc8d02eff09a8a53e6f1b9baa6a7a59082
ms.sourcegitcommit: 33732307162ddf6f272b0e9cc7f74eb8e6fdda1b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2017
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="0c83b-104">用于 .NET 的 Azure 通知中心库</span><span class="sxs-lookup"><span data-stu-id="0c83b-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="0c83b-105">Azure 通知中心提供易用的多平台扩展式推送引擎。</span><span class="sxs-lookup"><span data-stu-id="0c83b-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="0c83b-106">使用单个跨平台 API 调用，即可轻松地从任意云或本地后端向任意移动平台发送有针对性的个性化推送通知。</span><span class="sxs-lookup"><span data-stu-id="0c83b-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="0c83b-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="0c83b-107">Client library</span></span>

<span data-ttu-id="0c83b-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)。</span><span class="sxs-lookup"><span data-stu-id="0c83b-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="0c83b-109">[NuGet 包的新预览版](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1)现在支持 .NET Standard，以允许将 .NET Core 用于通知中心的后端使用</span><span class="sxs-lookup"><span data-stu-id="0c83b-109">A [new preview version of the NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0c83b-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="0c83b-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="0c83b-111">代码示例</span><span class="sxs-lookup"><span data-stu-id="0c83b-111">Code Example</span></span>

<span data-ttu-id="0c83b-112">此示例连接到数据库并从表中读取行。</span><span class="sxs-lookup"><span data-stu-id="0c83b-112">This example connects to a database and reads rows from a table.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0c83b-113">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="0c83b-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="0c83b-114">管理库</span><span class="sxs-lookup"><span data-stu-id="0c83b-114">Management library</span></span>

<span data-ttu-id="0c83b-115">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs)。</span><span class="sxs-lookup"><span data-stu-id="0c83b-115">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0c83b-116">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="0c83b-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0c83b-117">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="0c83b-117">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="0c83b-118">示例</span><span class="sxs-lookup"><span data-stu-id="0c83b-118">Samples</span></span>

- [<span data-ttu-id="0c83b-119">Windows Universal 入门</span><span class="sxs-lookup"><span data-stu-id="0c83b-119">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
