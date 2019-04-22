---
title: 用于 .NET 的 Azure HDInsight SDK
description: 用于 .NET 的 Azure HDInsight SDK 参考
ms.date: 04/10/2019
ms.topic: reference
ms.service: hdinsight
ms.openlocfilehash: 2282a302b269a52c71ed88c26e021344cdca4382
ms.sourcegitcommit: 4328168172ac1b1a448e16988f75199262bc5c2d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59700255"
---
# <a name="azure-hdinsight-sdk-for-net"></a>用于 .NET 的 Azure HDInsight SDK

Azure HDInsight 提供了用于 .NET 的管理和作业 SDK，这些 SDK 提供用于管理 HDInsight 群集以及提交和监视 Hadoop 作业的类。

## <a name="management"></a>管理

用于 .NET 的 HDInsight 管理 SDK 提供用于管理 HDInsight 群集的类和方法。 该 SDK 包含用于创建、删除、更新、列出、调整大小、执行脚本操作，以及监视、获取 HDInsight 群集属性等操作。

## <a name="prerequisites"></a>先决条件

* 一个 Azure 帐户。 如果没有帐户，可[获取一个免费试用帐户](https://azure.microsoft.com/free/)。
* [Visual Studio](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a>SDK 安装

在 Visual Studio 项目中，依次单击“工具”、“NuGet 包管理器”、“包管理器控制台”打开包管理器控制台。

在包管理器控制台中执行以下命令：

```
  Install-Package Microsoft.Azure.Management.HDInsight
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a>Authentication

首先需要使用 Azure 订阅对该 SDK 进行身份验证。  请遵循以下示例创建服务主体，然后使用该服务主体进行身份验证。 完成此操作后，将会获得 `HDInsightManagementClient` 的实例，其中包含可用于执行管理操作的多个方法（以下部分将概述这些方法）。

> [!NOTE]
> 除了以下示例中所示的方法以外，还有其他一些身份验证方法可能更符合你的需要。 此处概述了所有方法：[使用用于 .NET 的 Azure 库进行身份验证](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)

### <a name="authentication-example-using-a-service-principal"></a>使用服务主体的身份验证示例

首先登录到 [Azure Cloud Shell](https://shell.azure.com/bash)。 验证当前使用的是要在其中创建服务主体的订阅。 

```azurecli-interactive
az account show
```

订阅信息将显示为 JSON。

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

如果尚未登录到正确的订阅，请运行以下命令选择正确的订阅： 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> 如果尚未通过其他方法（例如，通过 Azure 门户创建 HDInsight 群集）注册 HDInsight 资源提供程序，则需要先执行此操作一次，然后才能进行身份验证。 可以在 [Azure Cloud Shell](https://shell.azure.com/bash) 中运行以下命令来完成此操作：
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

接下来，选择服务主体的名称，然后使用以下命令创建服务主体：

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

服务主体信息将以 JSON 格式显示。

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
复制以下代码片段，并在 `TENANT_ID`、`CLIENT_ID`、`CLIENT_SECRET` 和 `SUBSCRIPTION_ID` 中填写运行创建服务主体的命令后返回的 JSON 中的字符串。

```csharp
using Microsoft.Azure.Management.HDInsight;
using Microsoft.Azure.Management.HDInsight.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent;

namespace HDI_SDK_Test
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tenant ID for your Azure Subscription
            var TENANT_ID = "";
            // Your Service Principal App Client ID
            var CLIENT_ID = "";
            // Your Service Principal Client Secret
            var CLIENT_SECRET = "";
            // Azure Subscription ID
            var SUBSCRIPTION_ID = "";

            var credentials = SdkContext.AzureCredentialsFactory
                .FromServicePrincipal(
                CLIENT_ID,
                CLIENT_SECRET,
                TENANT_ID,
                AzureEnvironment.AzureGlobalCloud);

            var client = new HDInsightManagementClient(credentials);
            client.SubscriptionId = SUBSCRIPTION_ID;
        }
    }
}
```

## <a name="cluster-management"></a>群集管理

> [!NOTE]
> 本部分假设你已完成身份验证，已构造 `HDInsightManagementClient` 实例并已将其存储在名为 `client` 的变量中。 在前面的“身份验证”部分可以找到有关身份验证和获取 `HDInsightManagementClient` 的说明。

### <a name="create-a-cluster"></a>创建群集

可以通过调用 `client.Clusters.Create()` 来创建新群集。

#### <a name="samples"></a>示例

用于创建几个常见类型的 HDInsight 群集的代码示例可供使用：[HDInsight .NET 示例](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples)。

#### <a name="example"></a>示例

本示例演示如何创建包含 2 个头节点和 1 个工作节点的 Spark 群集。

> [!NOTE]
> 首先需要创建一个资源组和存储帐户，下面将予以介绍。 如果已创建资源组和存储帐户，则可以跳过这些步骤。

##### <a name="creating-a-resource-group"></a>创建资源组

可以在 [Azure Cloud Shell](https://shell.azure.com/bash) 中运行以下命令来创建资源组
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>创建存储帐户

可以在 [Azure Cloud Shell](https://shell.azure.com/bash) 中运行以下命令来创建存储帐户
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
现在，运行以下命令获取存储帐户的密钥（创建群集时需要用到）：
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
以下 .NET 代码片段创建包含 2 个头节点和 1 个工作节点的 Spark 群集。 按照注释中所述填写空白变量，并根据具体的需要任意更改其他参数。

```csharp
// The name for the cluster you are creating
var clusterName = "";
// The name of your existing Resource Group
var resourceGroupName = "";
// Choose a username
var username = "";
// Choose a password
var password = "";
// Replace <> with the name of your storage account
var storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
var storageAccountKey = "";
// Choose a region
var location = "";
var container = "default";

var parameters = new ClusterCreateParametersExtended
{
    Location = location,
    Tags = new Dictionary<string, string>(),
    Properties = new ClusterCreateProperties
    {
        ClusterVersion = "3.6",
        OsType = OSType.Linux,
        ClusterDefinition = new ClusterDefinition
        {
            Kind = "Hadoop",            
            Configurations = new Dictionary<string, Dictionary<string, string>>()
            {                
                { "gateway", new Dictionary<string, string>
                    {
                        { "restAuthCredential.isEnabled", "true" },
                        { "restAuthCredential.username", username},
                        { "restAuthCredential.password", password}
                    }
                }
            }
        },
        Tier = Tier.Standard,
        ComputeProfile = new ComputeProfile
        {
            Roles = new List<Role>{
                new Role
                {
                    Name = "headnode",
                    TargetInstanceCount = 2,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
                new Role
                {
                    Name = "workernode",
                    TargetInstanceCount = 1,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
            }
        },
        StorageProfile = new StorageProfile
        {
            Storageaccounts = new[]
            {
                new StorageAccount
                {
                    Name = storageAccount,
                    Key = storageAccountKey,
                    Container = container,
                    IsDefault = true
                }
            }
        }
    }
};
client.Clusters.Create(
    resourceGroupName,
    clusterName,
    parameters
);
```

### <a name="get-cluster-details"></a>获取群集详细信息

获取给定群集的属性：

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>示例

可以使用 `get` 来确认已成功创建群集。

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

输出应如下所示：

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> 存储在变量 `myCluster` 中的 `get` 返回值的类型为 `Microsoft.Azure.Management.HDInsight.ModelsCluster`。 可在[此处](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview)找到此对象的属性的完整列表。


### <a name="list-clusters"></a>列出群集

#### <a name="list-clusters-under-the-subscription"></a>列出订阅下的群集

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a>按资源组列出群集

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> `List()` 和 `ListByResourceGroup()` 都返回 `IPage<Cluster>` 对象。 若要获取下一个页面，可以调用 `client.Clusters.ListNext("Next Page Link")`。 可以反复执行此调用，直到 `NextPageLink` 为 `null`，如以下示例中所示。

#### <a name="example"></a>示例
以下示例列显当前订阅的所有群集的属性：

```csharp
var clustersPaged = client.Clusters.List();
while (true)
{
  foreach (var cluster in clustersPaged)
  {
    Debug.WriteLine(cluster.Name);
  
}  if (clustersPaged.NextPageLink == null)
  {
    break;
  }
  clustersPaged = client.Clusters.ListNext(clustersPaged.NextPageLink);
}
```

### <a name="delete-a-cluster"></a>删除群集

删除群集：

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>更新群集标记

可按如下所示更新给定群集的标记：

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a>示例

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a>调整群集大小

可以通过指定新大小来调整给定群集的工作节点数，如下所示：

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>群集监视

使用 HDInsight 管理 SDK 还可以通过 Operations Management Suite (OMS) 来管理群集的监视。

### <a name="enable-oms-monitoring"></a>启用 OMS 监视

> [!NOTE]
> 若要启用 OMS 监视，必须已有一个 Log Analytics 工作区。 如果尚未创建工作区，可在此了解创建方法：[在 Azure 门户中创建 Log Analytics 工作区](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace)。

在群集上启用 OMS 监视：

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>查看 OMS 监视状态

获取群集上的 OMS 状态：

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>禁用 OMS 监视

在群集上禁用 OMS：

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>脚本操作

HDInsight 提供一个称为“脚本操作”的配置方法，该方法可调用用于自定义群集的自定义脚本。
> [!NOTE]
> 有关如何使用脚本操作的详细信息见此处：[使用脚本操作自定义基于 Linux 的 HDInsight 群集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>执行脚本操作

可按如下所示在给定的群集上执行脚本操作：

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>删除脚本操作

删除给定群集上指定的持久化脚本操作：

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>列出持久化脚本操作

> [!NOTE]
> `ListPersistedScripts()` 和 `List()` 返回 `IPage<RuntimeScriptActionDetail>` 对象。 若要获取下一个页面，可以调用 `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` 或 `client.ScriptExecutionHistory.ListNext("Next Page Link")`。 可以反复执行此调用，直到 `NextPageLink` 为 `null`，如以下示例中所示。

列出指定群集的所有持久化脚本操作：
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>示例

```csharp
var scriptsPaged = client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.
    }
    if (scriptsPaged.NextPageLink == null)
    {
        break;
    }
    scriptsPaged = client.ScriptActions.ListPersistedScriptsNext(scriptsPaged.NextPageLink);
}
```

### <a name="list-all-scripts-execution-history"></a>列出所有脚本的执行历史记录

列出指定群集的所有脚本的执行历史记录：

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>示例

此示例列显以往所有脚本执行活动的所有详细信息。

```csharp
var scriptExecutionsPaged = client.ScriptExecutionHistory.List("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptExecutionsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.

    }
    if (scriptExecutionsPaged.NextPageLink == null)
    {
        break;
    }
    scriptExecutionsPaged = client.ScriptExecutionHistory.ListNext(scriptExecutionsPaged.NextPageLink);
}
```

## <a name="jobs"></a>作业

使用用于 .NET 的 Azure HDInsight 作业 SDK 可创建、管理和监视 Hadoop 群集上的作业。

### <a name="sdk-installation"></a>SDK 安装

直接从 Visual Studio [包管理器控制台][PackageManager] 或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

### <a name="code-example"></a>代码示例

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

### <a name="samples"></a>示例

- [运行 Hive 作业](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [运行 Pig 作业](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [更多作业](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)
