---
title: 用于 .NET 的 Azure 自动化库
description: 用于 .NET 的 Azure 自动化库参考
keywords: Azure, .NET, SDK, API, 自动化
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: automation
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e45db49fa71e5ad16ab1e4f26d76cd9b0146ac5f
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065757"
---
# <a name="azure-automation-libraries-for-net"></a>用于 .NET 的 Azure 自动化库

## <a name="overview"></a>概述

借助 Microsoft Azure 自动化，用户可以自动完成通常要在云环境和企业环境中执行的任务。 

请阅读 [Azure 自动化概述](/azure/automation/automation-intro)了解详细信息。

## <a name="management-library"></a>管理库

使用管理库可以管理 Runbook 和作业，以及管理 Desired State Configuration 设置。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a>代码示例

以下示例演示如何基于现有的 Runbook 启动新作业。

```csharp
/*
  using Microsoft.Azure.Management.Automation;
*/
AutomationManagementClient client =
    new AutomationManagementClient(new CertificateCloudCredentials(subscriptionId, cert));

// Create job create parameters
JobCreateParameters jcParam = new JobCreateParameters
{
    Properties = new JobCreateProperties
    {
        Runbook = new RunbookAssociationProperty
        {
            Name = runbookName
        },
        Parameters = null // optional parameters here
    }
};

// create runbook job. This gives back the Job
Job job = automationManagementClient.Jobs.Create(automationAccountName, jcParam).Job;
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a>示例

* [AzureBot](https://github.com/Microsoft/AzureBot) 在 Azure 中结合 [Bot Framework](https://docs.microsoft.com/bot-framework/) 和[认知服务](/cognitive-services)使用自动化库来提高开发人员的工作效率

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
