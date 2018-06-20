---
title: 适用于 .NET 的 Azure StorSimple 库
description: 适用于 .NET 的 Azure StorSimple 存储库参考
keywords: Azure, .NET, SDK, API, StorSimple
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/27/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: storsimple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: dcb6732bf1eded6852a3185546a09c96cfe84eca
ms.sourcegitcommit: 64c9e16e42894e8db8ed088487e55c5e0edd6861
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2017
ms.locfileid: "23639645"
---
# <a name="azure-storsimple-libraries-for-net"></a>适用于 .NET 的 Azure StorSimple 库

## <a name="overview"></a>概述

Microsoft Azure StorSimple 是一种企业存储解决方案，它提供与基于云的存储的物理 iSCSI 或 SMB 接口。 

了解有关 [Azure StorSimple](/azure/storsimple/) 的详细信息。    

## <a name="management-library"></a>管理库

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.StorSimple.Fluent)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.StorSimple.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.StorSimple.Fluent
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/monitor/management)

## <a name="samples"></a>示例

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package