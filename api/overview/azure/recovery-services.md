---
title: 用于 .NET 的 Azure 恢复服务和备份库
description: 用于 .NET 的 Azure 恢复服务和备份库参考
keywords: Azure, .NET, SDK, API, 恢复服务, 备份
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: recovery-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 6186411b668d0950328b49bb826e5b05c5ee0304
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065427"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="869dd-104">用于 .NET 的 Azure 恢复服务和备份库</span><span class="sxs-lookup"><span data-stu-id="869dd-104">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="869dd-105">概述</span><span class="sxs-lookup"><span data-stu-id="869dd-105">Overview</span></span>

<span data-ttu-id="869dd-106">Azure 恢复服务是一套数据恢复服务，包括 [Azure 备份](/azure/backup/)和 [Azure Site Recovery](/azure/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="869dd-106">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="869dd-107">管理库</span><span class="sxs-lookup"><span data-stu-id="869dd-107">Management library</span></span>

<span data-ttu-id="869dd-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices)。</span><span class="sxs-lookup"><span data-stu-id="869dd-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="869dd-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="869dd-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="869dd-110">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="869dd-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="869dd-111">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="869dd-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="869dd-112">代码示例</span><span class="sxs-lookup"><span data-stu-id="869dd-112">Code Example</span></span>

<span data-ttu-id="869dd-113">以下代码示例使用管理库来触发备份。</span><span class="sxs-lookup"><span data-stu-id="869dd-113">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
