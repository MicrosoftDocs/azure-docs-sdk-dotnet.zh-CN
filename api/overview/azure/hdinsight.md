---
title: 用于 .NET 的 Azure HDInsight 库
description: 用于 .NET 的 Azure HDInsight 库参考
keywords: Azure, .NET, SDK, API, HDInsight
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: hd-insight
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2cdb080b4d224a77a36318cefd13ebfae2e3e2e1
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065807"
---
# <a name="azure-hdinsight-libraries-for-net"></a><span data-ttu-id="b2d9d-104">用于 .NET 的 Azure HDInsight 库</span><span class="sxs-lookup"><span data-stu-id="b2d9d-104">Azure HDInsight libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="b2d9d-105">概述</span><span class="sxs-lookup"><span data-stu-id="b2d9d-105">Overview</span></span>

<span data-ttu-id="b2d9d-106">HDInsight 服务 .NET SDK 提供相关的类来创建、配置、提交和监视 Azure HDInsight 服务所管理的 Hadoop 作业。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-106">The HDInsight Service .NET SDK provides classes that relate to the creation, configuration, submission, and monitoring of Hadoop jobs managed by an Azure HDInsight Service.</span></span> <span data-ttu-id="b2d9d-107">此外，它还提供相应的类用于通过 HDInsight 服务管理 Azure 订阅，以及配置与 Azure 订阅所管理的 HDInsight 群集相关联的群集、存储帐户和其他资产。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-107">In addition, it provides classes to manage Azure subscriptions using the HDInsight Service and to configure the clusters, storage accounts, and other assets associated with the HDInsight clusters that are managed by an Azure subscription.</span></span>

## <a name="management-libraries"></a><span data-ttu-id="b2d9d-108">管理库</span><span class="sxs-lookup"><span data-stu-id="b2d9d-108">Management libraries</span></span>

### <a name="jobs"></a><span data-ttu-id="b2d9d-109">作业</span><span class="sxs-lookup"><span data-stu-id="b2d9d-109">Jobs</span></span>

<span data-ttu-id="b2d9d-110">使用 Azure HDInsight 客户端 SDK 可创建、管理和监视 Hadoop 群集上的作业。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-110">Use the Azure HDInsight client SDK to create, manage, and monitor jobs on a Hadoop cluster.</span></span> 

<span data-ttu-id="b2d9d-111">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job)。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b2d9d-112">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="b2d9d-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a><span data-ttu-id="b2d9d-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="b2d9d-113">Code Example</span></span>

<span data-ttu-id="b2d9d-114">此示例在 Hadoop 群集中运行 Hive 作业。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-114">This example runs a Hive job in a Hadoop cluster.</span></span>

```csharp
HDInsightJobManagementClient managementClient = new HDInsightJobManagementClient(clusterUri, credentials);

Dictionary<string, string> defines = new Dictionary<string, string> {
    { "hive.execution.engine", "tez" },
    { "hive.exec.reducers.max", "1" }
};
List<string> arguments = new List<string> { { "argA" }, { "argB" } };
HiveJobSubmissionParameters parameters = new HiveJobSubmissionParameters
{
    Query = "SHOW TABLES",
    Defines = defines,
    Arguments = arguments
};

JobSubmissionResponse jobResponse = managementClient.JobManagement.SubmitHiveJob(parameters);
```

### <a name="hdinsight"></a><span data-ttu-id="b2d9d-115">HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2d9d-115">HDInsight</span></span>

<span data-ttu-id="b2d9d-116">使用 Azure HDInsight 管理 SDK 可创建、管理、启动、停止和缩放 Hadoop 群集。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-116">Use the Azure HDInsight management SDK to create, manage, start, stop, and scale Hadoop clusters.</span></span>

<span data-ttu-id="b2d9d-117">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight)。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b2d9d-118">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="b2d9d-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a><span data-ttu-id="b2d9d-119">代码示例</span><span class="sxs-lookup"><span data-stu-id="b2d9d-119">Code Example</span></span>

<span data-ttu-id="b2d9d-120">此示例使用现有的 Azure Blob 存储创建 HDInsight 双节点 Linux Hadoop 群集。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-120">This example creates an HDInsight two node Linux Hadoop cluster with an existing Azure Blob Storage.</span></span>

```csharp
HDInsightManagementClient managementClient = new HDInsightManagementClient(authToken);
// Set parameters for the new cluster
ClusterCreateParameters parameters = new ClusterCreateParameters
{
    ClusterSizeInNodes = 2,
    UserName = "admin",
    Password = "<Enter HTTP User Password>",
    ClusterType = "Hadoop",
    OSType = OSType.Linux,
    Version = "3.5",
    // Use an Azure storage account as the default storage
    DefaultStorageInfo = new AzureStorageInfo("<StorageAccount>", "<StorageKey>", "<BlobContainerName>"),
    Location = "EAST US 2",
    SshUserName = "sshuser",
    SshPassword = "<Enter SSH User Password>",
};

// Create the cluster
managementClient.Clusters.Create("<ExistingResourceGroupName>", "<NewClusterName>", parameters);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2d9d-121">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="b2d9d-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a><span data-ttu-id="b2d9d-122">示例</span><span class="sxs-lookup"><span data-stu-id="b2d9d-122">Samples</span></span>

- [<span data-ttu-id="b2d9d-123">群集创建</span><span class="sxs-lookup"><span data-stu-id="b2d9d-123">Cluster creation</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [<span data-ttu-id="b2d9d-124">群集管理</span><span class="sxs-lookup"><span data-stu-id="b2d9d-124">Cluster management</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [<span data-ttu-id="b2d9d-125">运行 Hive 作业</span><span class="sxs-lookup"><span data-stu-id="b2d9d-125">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="b2d9d-126">运行 Pig 作业</span><span class="sxs-lookup"><span data-stu-id="b2d9d-126">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="b2d9d-127">更多作业</span><span class="sxs-lookup"><span data-stu-id="b2d9d-127">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

<span data-ttu-id="b2d9d-128">查看 Azure SQL 数据库示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight)。</span><span class="sxs-lookup"><span data-stu-id="b2d9d-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) of Azure SQL Database samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
