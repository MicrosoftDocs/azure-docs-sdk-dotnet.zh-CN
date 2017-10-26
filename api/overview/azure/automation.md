---
title: "用于 .NET 的 Azure 自动化库"
description: "用于 .NET 的 Azure 自动化库参考"
keywords: "Azure, .NET, SDK, API, 自动化"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: automation
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2055a5e24d445468763c049c34a5055cea108688
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
---
# <a name="azure-automation-libraries-for-net"></a><span data-ttu-id="a6518-104">用于 .NET 的 Azure 自动化库</span><span class="sxs-lookup"><span data-stu-id="a6518-104">Azure Automation libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a6518-105">概述</span><span class="sxs-lookup"><span data-stu-id="a6518-105">Overview</span></span>

<span data-ttu-id="a6518-106">借助 Microsoft Azure 自动化，用户可以自动完成通常要在云环境和企业环境中执行的任务。</span><span class="sxs-lookup"><span data-stu-id="a6518-106">Microsoft Azure Automation provides a way for users to automate the tasks that are commonly performed in a cloud and enterprise environment.</span></span> 

<span data-ttu-id="a6518-107">请阅读 [Azure 自动化概述](/azure/automation/automation-intro)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="a6518-107">Learn more by reading the [Azure Automation Overview](/azure/automation/automation-intro).</span></span>

## <a name="management-library"></a><span data-ttu-id="a6518-108">管理库</span><span class="sxs-lookup"><span data-stu-id="a6518-108">Management library</span></span>

<span data-ttu-id="a6518-109">使用管理库可以管理 Runbook 和作业，以及管理 Desired State Configuration 设置。</span><span class="sxs-lookup"><span data-stu-id="a6518-109">Using the management library to manage runbooks and jobs and manage Desired State Configuration settings.</span></span>

<span data-ttu-id="a6518-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation)。</span><span class="sxs-lookup"><span data-stu-id="a6518-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a6518-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="a6518-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a><span data-ttu-id="a6518-112">代码示例</span><span class="sxs-lookup"><span data-stu-id="a6518-112">Code Example</span></span>

<span data-ttu-id="a6518-113">以下示例演示如何基于现有的 Runbook 启动新作业。</span><span class="sxs-lookup"><span data-stu-id="a6518-113">The following example illustrates how to start a new job based on an existing runbook.</span></span>

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
> [<span data-ttu-id="a6518-114">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="a6518-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a><span data-ttu-id="a6518-115">示例</span><span class="sxs-lookup"><span data-stu-id="a6518-115">Samples</span></span>

* <span data-ttu-id="a6518-116">[AzureBot](https://github.com/Microsoft/AzureBot) 在 Azure 中结合 [Bot Framework](https://docs.microsoft.com/bot-framework/) 和[认知服务](/cognitive-services)使用自动化库来提高开发人员的工作效率</span><span class="sxs-lookup"><span data-stu-id="a6518-116">[AzureBot](https://github.com/Microsoft/AzureBot) uses the automation library with the [Bot Framework](https://docs.microsoft.com/bot-framework/) and [Cognitive Services](/cognitive-services) to improve developer productivity on Azure</span></span>

<span data-ttu-id="a6518-117">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="a6518-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
