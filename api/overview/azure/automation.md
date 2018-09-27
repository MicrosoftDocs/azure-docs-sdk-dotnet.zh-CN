---
title: 用于 .NET 的 Azure 自动化库
description: 用于 .NET 的 Azure 自动化库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: automation
ms.openlocfilehash: 4890faab86d1319fe802a30e3735419ac65e8d64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190280"
---
# <a name="azure-automation-libraries-for-net"></a><span data-ttu-id="9e0f1-103">用于 .NET 的 Azure 自动化库</span><span class="sxs-lookup"><span data-stu-id="9e0f1-103">Azure Automation libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="9e0f1-104">概述</span><span class="sxs-lookup"><span data-stu-id="9e0f1-104">Overview</span></span>

<span data-ttu-id="9e0f1-105">借助 Microsoft Azure 自动化，用户可以自动完成通常要在云环境和企业环境中执行的任务。</span><span class="sxs-lookup"><span data-stu-id="9e0f1-105">Microsoft Azure Automation provides a way for users to automate the tasks that are commonly performed in a cloud and enterprise environment.</span></span> 

<span data-ttu-id="9e0f1-106">请阅读 [Azure 自动化概述](/azure/automation/automation-intro)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="9e0f1-106">Learn more by reading the [Azure Automation Overview](/azure/automation/automation-intro).</span></span>

## <a name="management-library"></a><span data-ttu-id="9e0f1-107">管理库</span><span class="sxs-lookup"><span data-stu-id="9e0f1-107">Management library</span></span>

<span data-ttu-id="9e0f1-108">使用管理库可以管理 Runbook 和作业，以及管理 Desired State Configuration 设置。</span><span class="sxs-lookup"><span data-stu-id="9e0f1-108">Using the management library to manage runbooks and jobs and manage Desired State Configuration settings.</span></span>

<span data-ttu-id="9e0f1-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation)。</span><span class="sxs-lookup"><span data-stu-id="9e0f1-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9e0f1-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="9e0f1-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a><span data-ttu-id="9e0f1-111">代码示例</span><span class="sxs-lookup"><span data-stu-id="9e0f1-111">Code Example</span></span>

<span data-ttu-id="9e0f1-112">以下示例演示如何基于现有的 Runbook 启动新作业。</span><span class="sxs-lookup"><span data-stu-id="9e0f1-112">The following example illustrates how to start a new job based on an existing runbook.</span></span>

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
> [<span data-ttu-id="9e0f1-113">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="9e0f1-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a><span data-ttu-id="9e0f1-114">示例</span><span class="sxs-lookup"><span data-stu-id="9e0f1-114">Samples</span></span>

* <span data-ttu-id="9e0f1-115">[AzureBot](https://github.com/Microsoft/AzureBot) 在 Azure 中结合 [Bot Framework](https://docs.microsoft.com/bot-framework/) 和[认知服务](/cognitive-services)使用自动化库来提高开发人员的工作效率</span><span class="sxs-lookup"><span data-stu-id="9e0f1-115">[AzureBot](https://github.com/Microsoft/AzureBot) uses the automation library with the [Bot Framework](https://docs.microsoft.com/bot-framework/) and [Cognitive Services](/cognitive-services) to improve developer productivity on Azure</span></span>

<span data-ttu-id="9e0f1-116">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="9e0f1-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
