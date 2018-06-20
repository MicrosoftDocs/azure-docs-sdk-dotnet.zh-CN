---
title: 用于 .NET 的 Azure HDInsight 库
description: 用于 .NET 的 Azure HDInsight 库参考
keywords: Azure, .NET, SDK, API, HDInsight
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: hd-insight
ms.custom: devcenter, svc-overview
ms.openlocfilehash: da9023ab4e6106754d48acb31cda58cdb358f5cb
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
ms.locfileid: "23486950"
---
# <a name="azure-hdinsight-libraries-for-net"></a>用于 .NET 的 Azure HDInsight 库

## <a name="overview"></a>概述

HDInsight 服务 .NET SDK 提供相关的类来创建、配置、提交和监视 Azure HDInsight 服务所管理的 Hadoop 作业。 此外，它还提供相应的类用于通过 HDInsight 服务管理 Azure 订阅，以及配置与 Azure 订阅所管理的 HDInsight 群集相关联的群集、存储帐户和其他资产。

## <a name="management-libraries"></a>管理库

### <a name="jobs"></a>作业

使用 Azure HDInsight 客户端 SDK 可创建、管理和监视 Hadoop 群集上的作业。 

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a>代码示例

此示例在 Hadoop 群集中运行 Hive 作业。

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

### <a name="hdinsight"></a>HDInsight

使用 Azure HDInsight 管理 SDK 可创建、管理、启动、停止和缩放 Hadoop 群集。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a>代码示例

此示例使用现有的 Azure Blob 存储创建 HDInsight 双节点 Linux Hadoop 群集。

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
> [了解管理 API](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a>示例

- [群集创建](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [群集管理](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [运行 Hive 作业](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [运行 Pig 作业](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [更多作业](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

查看 Azure SQL 数据库示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
