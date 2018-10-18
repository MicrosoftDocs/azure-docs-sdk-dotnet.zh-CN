---
title: 用于 .NET 的 Azure 恢复服务和备份库
description: 用于 .NET 的 Azure 恢复服务和备份库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: backup
ms.openlocfilehash: c2faef5c83f28cb35158609b92f0334671161d1d
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348169"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="86c8f-103">用于 .NET 的 Azure 恢复服务和备份库</span><span class="sxs-lookup"><span data-stu-id="86c8f-103">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="86c8f-104">概述</span><span class="sxs-lookup"><span data-stu-id="86c8f-104">Overview</span></span>

<span data-ttu-id="86c8f-105">Azure 恢复服务是一套数据恢复服务，包括 [Azure 备份](/azure/backup/)和 [Azure Site Recovery](/azure/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="86c8f-105">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="86c8f-106">管理库</span><span class="sxs-lookup"><span data-stu-id="86c8f-106">Management library</span></span>

<span data-ttu-id="86c8f-107">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices)。</span><span class="sxs-lookup"><span data-stu-id="86c8f-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="86c8f-108">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="86c8f-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="86c8f-109">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="86c8f-109">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="86c8f-110">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="86c8f-110">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="86c8f-111">代码示例</span><span class="sxs-lookup"><span data-stu-id="86c8f-111">Code Example</span></span>

<span data-ttu-id="86c8f-112">以下代码示例使用管理库来触发备份。</span><span class="sxs-lookup"><span data-stu-id="86c8f-112">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
