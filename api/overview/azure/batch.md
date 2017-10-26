---
title: "用于 .NET 的 Azure Batch 库"
description: "用于 .NET 的 Azure Batch 库参考"
keywords: Azure, .NET, SDK, API, Batch
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: batch
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 79ca70e5d0f3d5555c8a691da6dbcc1e6a55ab0b
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
---
# <a name="azure-batch-libraries-for-net"></a>用于 .NET 的 Azure Batch 库

Azure Batch 是一项平台服务，适用于在云中有效运行大规模并行和高性能计算 (HPC) 应用程序。 Azure Batch 可以计划要在托管的虚拟机集合上运行的计算密集型工作，并且可以缩放计算资源，使之符合作业的需求。

使用 Azure Batch 时，可以轻松定义用于大规模并行执行应用程序的 Azure 计算资源。 不需要手动创建、配置和管理 HPC 群集、各个虚拟机、虚拟网络或复杂的作业和任务计划基础结构。 Azure Batch 自动执行这些任务，或者为用户简化这些任务。

详细了解如何[使用 Batch 运行固有并行的工作负荷](/azure/batch/batch-technical-overview)。 此外，还可以详细如何[使用用于 .NET 的 Batch 客户端库开始构建解决方案](/azure/batch/batch-dotnet-get-started)。 了解如何[使用用于 .NET 的 Batch 管理库来管理 Batch 帐户和配额](/azure/batch/batch-management-dotnet)。

## <a name="client-library"></a>客户端库

在 Batch 中使用客户端库运行并行工作负荷。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Azure.Batch)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a>示例

以下示例使用客户端 SDK 创建在 Azure Batch 中运行的作业。

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
> [了解客户端 API](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a>管理库

使用管理库可通过编程方式管理 Batch 帐户、配额和应用程序包。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a>示例

以下示例检索订阅的配额、创建帐户，并重新生成主帐户密钥。

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
> [了解管理 API](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a>示例

* [用于 .NET 的 Azure Batch 客户端和管理 SDK 示例](https://github.com/Azure/azure-batch-samples/tree/master/CSharp)

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
