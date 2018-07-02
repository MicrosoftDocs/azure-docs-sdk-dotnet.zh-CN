---
title: 用于 .NET 的 Azure Batch 库
description: 用于 .NET 的 Azure Batch 库参考
keywords: Azure, .NET, SDK, API, Batch
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: batch
ms.custom: devcenter, svc-overview
ms.openlocfilehash: b6053e19d26247dd36ed7e38fc33030f96aecca8
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065553"
---
# <a name="azure-batch-libraries-for-net"></a><span data-ttu-id="f4c02-104">用于 .NET 的 Azure Batch 库</span><span class="sxs-lookup"><span data-stu-id="f4c02-104">Azure Batch libraries for .NET</span></span>

<span data-ttu-id="f4c02-105">Azure Batch 是一项平台服务，适用于在云中有效运行大规模并行和高性能计算 (HPC) 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f4c02-105">Azure Batch is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="f4c02-106">Azure Batch 可以计划要在托管的虚拟机集合上运行的计算密集型工作，并且可以缩放计算资源，使之符合作业的需求。</span><span class="sxs-lookup"><span data-stu-id="f4c02-106">Azure Batch schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="f4c02-107">使用 Azure Batch 时，可以轻松定义用于大规模并行执行应用程序的 Azure 计算资源。</span><span class="sxs-lookup"><span data-stu-id="f4c02-107">With Azure Batch, you can easily define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="f4c02-108">不需要手动创建、配置和管理 HPC 群集、各个虚拟机、虚拟网络或复杂的作业和任务计划基础结构。</span><span class="sxs-lookup"><span data-stu-id="f4c02-108">There's no need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span> <span data-ttu-id="f4c02-109">Azure Batch 自动执行这些任务，或者为用户简化这些任务。</span><span class="sxs-lookup"><span data-stu-id="f4c02-109">Azure Batch automates or simplifies these tasks for you.</span></span>

<span data-ttu-id="f4c02-110">详细了解如何[使用 Batch 运行固有并行的工作负荷](/azure/batch/batch-technical-overview)。</span><span class="sxs-lookup"><span data-stu-id="f4c02-110">Read more about how to [run intrinsically parallel workloads with Batch](/azure/batch/batch-technical-overview).</span></span> <span data-ttu-id="f4c02-111">此外，还可以详细如何[使用用于 .NET 的 Batch 客户端库开始构建解决方案](/azure/batch/batch-dotnet-get-started)。</span><span class="sxs-lookup"><span data-stu-id="f4c02-111">You can also learn how to [get started building solutions with the Batch client library for .NET](/azure/batch/batch-dotnet-get-started).</span></span> <span data-ttu-id="f4c02-112">了解如何[使用用于 .NET 的 Batch 管理库来管理 Batch 帐户和配额](/azure/batch/batch-management-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="f4c02-112">Discover how to [manage Batch accounts and quotas with the Batch Management library for .NET](/azure/batch/batch-management-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="f4c02-113">客户端库</span><span class="sxs-lookup"><span data-stu-id="f4c02-113">Client library</span></span>

<span data-ttu-id="f4c02-114">在 Batch 中使用客户端库运行并行工作负荷。</span><span class="sxs-lookup"><span data-stu-id="f4c02-114">Use the client library to run parallel workloads with Batch.</span></span>

<span data-ttu-id="f4c02-115">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Azure.Batch)。</span><span class="sxs-lookup"><span data-stu-id="f4c02-115">Install the [NuGet package](https://www.nuget.org/packages/Azure.Batch) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f4c02-116">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="f4c02-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a><span data-ttu-id="f4c02-117">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="f4c02-117">.NET Core CLI</span></span>

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a><span data-ttu-id="f4c02-118">示例</span><span class="sxs-lookup"><span data-stu-id="f4c02-118">Example</span></span>

<span data-ttu-id="f4c02-119">以下示例使用客户端 SDK 创建在 Azure Batch 中运行的作业。</span><span class="sxs-lookup"><span data-stu-id="f4c02-119">The following example uses the client SDK to create a job to run in Azure Batch.</span></span>

```csharp
/*
using Microsoft.Azure.Batch.Auth;
using Microsoft.Azure.Batch;
*/
BatchSharedKeyCredentials credentials = new BatchSharedKeyCredentials(batchUrl, accountName, accountKey);
using (BatchClient batchClient = await BatchClient.OpenAsync(credentials))
{
    //set up pool specification and information along with resource files here
    JobManagerTask jobManagerTask = new JobManagerTask()
    {
        ResourceFiles = jobManagerResourceFiles,
        CommandLine = Constants.JobManagerExecutable,

        //Determines if the job should terminate when the job manager process exits.
        KillJobOnCompletion = true,
        Id = jobManagerTaskId
    };

    string jobId = Environment.GetEnvironmentVariable("USERNAME") + DateTime.UtcNow.ToString("yyyyMMdd-HHmmss");

    CloudJob unboundJob = batchClient.JobOperations.CreateJob(jobId, poolInformation);
    unboundJob.JobManagerTask = jobManagerTask;

    // now interact with the job ...
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4c02-120">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="f4c02-120">Explore the client APIs</span></span>](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a><span data-ttu-id="f4c02-121">管理库</span><span class="sxs-lookup"><span data-stu-id="f4c02-121">Management library</span></span>

<span data-ttu-id="f4c02-122">使用管理库可通过编程方式管理 Batch 帐户、配额和应用程序包。</span><span class="sxs-lookup"><span data-stu-id="f4c02-122">Use the management library to programmatically manage Batch accounts, quotas, and application packages.</span></span>

<span data-ttu-id="f4c02-123">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch)。</span><span class="sxs-lookup"><span data-stu-id="f4c02-123">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f4c02-124">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="f4c02-124">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a><span data-ttu-id="f4c02-125">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="f4c02-125">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a><span data-ttu-id="f4c02-126">示例</span><span class="sxs-lookup"><span data-stu-id="f4c02-126">Example</span></span>

<span data-ttu-id="f4c02-127">以下示例检索订阅的配额、创建帐户，并重新生成主帐户密钥。</span><span class="sxs-lookup"><span data-stu-id="f4c02-127">The following example retrieves the quota for the subscription, creates an account, and regenerates the primary account key.</span></span>

```csharp
/*
using Microsoft.Azure.Management.Batch;
using Microsoft.Azure.Management.Batch.Models;
using Microsoft.Rest;
*/
using (BatchManagementClient batchManagementClient = new BatchManagementClient(new TokenCredentials(accessToken)))
{
    batchManagementClient.SubscriptionId = subscriptionId;

    // Get the account quota for the subscription
    BatchLocationQuota quotaResponse = await batchManagementClient.Location.GetQuotasAsync(location);
    Console.WriteLine("Your subscription can create {0} account(s) in the {1} region.", quotaResponse.AccountQuota, location);

    // Create account
    await batchManagementClient.BatchAccount.CreateAsync(ResourceGroupName, accountName, 
        new BatchAccountCreateParameters() { Location = location });

    // Regenerate primary account key
    BatchAccountKeys newKeys = await batchManagementClient.BatchAccount.RegenerateKeyAsync(
        ResourceGroupName, account.Name, AccountKeyType.Primary);
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4c02-128">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="f4c02-128">Explore the management APIs</span></span>](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a><span data-ttu-id="f4c02-129">示例</span><span class="sxs-lookup"><span data-stu-id="f4c02-129">Samples</span></span>

* [<span data-ttu-id="f4c02-130">用于 .NET 的 Azure Batch 客户端和管理 SDK 示例</span><span class="sxs-lookup"><span data-stu-id="f4c02-130">Azure Batch Client and Management SDK for .NET Samples</span></span>](https://github.com/Azure/azure-batch-samples/tree/master/CSharp)

<span data-ttu-id="f4c02-131">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="f4c02-131">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
