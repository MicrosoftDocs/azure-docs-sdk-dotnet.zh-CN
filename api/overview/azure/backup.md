---
title: "用于 .NET 的 Azure 备份库"
description: "用于 .NET 的 Azure 备份库参考"
keywords: "Azure, .NET, SDK, API, 备份"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/24/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 93eeaeda1860e3b7190dfb0ae917b4b85b5a3609
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-backup-libraries-for-net"></a>用于 .NET 的 Azure 备份库

## <a name="overview"></a>概述

Azure 备份是一个云服务，可用于备份、保护和还原数据。

参阅[什么是 Azure 备份？](/azure/backup/backup-introduction-to-azure-backup)了解有关 Azure 备份的详细信息。

## <a name="management-library"></a>管理库

使用备份管理库来管理备份和设置恢复服务保管库。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

以下代码示例使用管理库来触发备份。

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/backup/management)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
