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
# <a name="azure-hdinsight-sdk-for-net"></a><span data-ttu-id="bad44-103">用于 .NET 的 Azure HDInsight SDK</span><span class="sxs-lookup"><span data-stu-id="bad44-103">Azure HDInsight SDK for .NET</span></span>

<span data-ttu-id="bad44-104">Azure HDInsight 提供了用于 .NET 的管理和作业 SDK，这些 SDK 提供用于管理 HDInsight 群集以及提交和监视 Hadoop 作业的类。</span><span class="sxs-lookup"><span data-stu-id="bad44-104">Azure HDInsight offers management and job SDKs for .NET that provide classes for managing your HDInsight cluster and submitting and monitoring Hadoop jobs.</span></span>

## <a name="management"></a><span data-ttu-id="bad44-105">管理</span><span class="sxs-lookup"><span data-stu-id="bad44-105">Management</span></span>

<span data-ttu-id="bad44-106">用于 .NET 的 HDInsight 管理 SDK 提供用于管理 HDInsight 群集的类和方法。</span><span class="sxs-lookup"><span data-stu-id="bad44-106">The HDInsight management SDK for .NET provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="bad44-107">该 SDK 包含用于创建、删除、更新、列出、调整大小、执行脚本操作，以及监视、获取 HDInsight 群集属性等操作。</span><span class="sxs-lookup"><span data-stu-id="bad44-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bad44-108">先决条件</span><span class="sxs-lookup"><span data-stu-id="bad44-108">Prerequisites</span></span>

* <span data-ttu-id="bad44-109">一个 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="bad44-109">An Azure account.</span></span> <span data-ttu-id="bad44-110">如果没有帐户，可[获取一个免费试用帐户](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="bad44-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="bad44-111">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bad44-111">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a><span data-ttu-id="bad44-112">SDK 安装</span><span class="sxs-lookup"><span data-stu-id="bad44-112">SDK Installation</span></span>

<span data-ttu-id="bad44-113">在 Visual Studio 项目中，依次单击“工具”、“NuGet 包管理器”、“包管理器控制台”打开包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="bad44-113">From your Visual Studio project, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>

<span data-ttu-id="bad44-114">在包管理器控制台中执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="bad44-114">In the Package Manager Console, execute the following commands:</span></span>

```
  Install-Package Microsoft.Azure.Management.HDInsight
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a><span data-ttu-id="bad44-115">Authentication</span><span class="sxs-lookup"><span data-stu-id="bad44-115">Authentication</span></span>

<span data-ttu-id="bad44-116">首先需要使用 Azure 订阅对该 SDK 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="bad44-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="bad44-117">请遵循以下示例创建服务主体，然后使用该服务主体进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="bad44-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="bad44-118">完成此操作后，将会获得 `HDInsightManagementClient` 的实例，其中包含可用于执行管理操作的多个方法（以下部分将概述这些方法）。</span><span class="sxs-lookup"><span data-stu-id="bad44-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="bad44-119">除了以下示例中所示的方法以外，还有其他一些身份验证方法可能更符合你的需要。</span><span class="sxs-lookup"><span data-stu-id="bad44-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="bad44-120">此处概述了所有方法：[使用用于 .NET 的 Azure 库进行身份验证](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="bad44-120">All methods are outlined here: [Authenticate with the Azure Libraries for .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="bad44-121">使用服务主体的身份验证示例</span><span class="sxs-lookup"><span data-stu-id="bad44-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="bad44-122">首先登录到 [Azure Cloud Shell](https://shell.azure.com/bash)。</span><span class="sxs-lookup"><span data-stu-id="bad44-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="bad44-123">验证当前使用的是要在其中创建服务主体的订阅。</span><span class="sxs-lookup"><span data-stu-id="bad44-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="bad44-124">订阅信息将显示为 JSON。</span><span class="sxs-lookup"><span data-stu-id="bad44-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="bad44-125">如果尚未登录到正确的订阅，请运行以下命令选择正确的订阅：</span><span class="sxs-lookup"><span data-stu-id="bad44-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="bad44-126">如果尚未通过其他方法（例如，通过 Azure 门户创建 HDInsight 群集）注册 HDInsight 资源提供程序，则需要先执行此操作一次，然后才能进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="bad44-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="bad44-127">可以在 [Azure Cloud Shell](https://shell.azure.com/bash) 中运行以下命令来完成此操作：</span><span class="sxs-lookup"><span data-stu-id="bad44-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="bad44-128">接下来，选择服务主体的名称，然后使用以下命令创建服务主体：</span><span class="sxs-lookup"><span data-stu-id="bad44-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="bad44-129">服务主体信息将以 JSON 格式显示。</span><span class="sxs-lookup"><span data-stu-id="bad44-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="bad44-130">复制以下代码片段，并在 `TENANT_ID`、`CLIENT_ID`、`CLIENT_SECRET` 和 `SUBSCRIPTION_ID` 中填写运行创建服务主体的命令后返回的 JSON 中的字符串。</span><span class="sxs-lookup"><span data-stu-id="bad44-130">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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

## <a name="cluster-management"></a><span data-ttu-id="bad44-131">群集管理</span><span class="sxs-lookup"><span data-stu-id="bad44-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="bad44-132">本部分假设你已完成身份验证，已构造 `HDInsightManagementClient` 实例并已将其存储在名为 `client` 的变量中。</span><span class="sxs-lookup"><span data-stu-id="bad44-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="bad44-133">在前面的“身份验证”部分可以找到有关身份验证和获取 `HDInsightManagementClient` 的说明。</span><span class="sxs-lookup"><span data-stu-id="bad44-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="bad44-134">创建群集</span><span class="sxs-lookup"><span data-stu-id="bad44-134">Create a Cluster</span></span>

<span data-ttu-id="bad44-135">可以通过调用 `client.Clusters.Create()` 来创建新群集。</span><span class="sxs-lookup"><span data-stu-id="bad44-135">A new cluster can be created by calling `client.Clusters.Create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="bad44-136">示例</span><span class="sxs-lookup"><span data-stu-id="bad44-136">Samples</span></span>

<span data-ttu-id="bad44-137">用于创建几个常见类型的 HDInsight 群集的代码示例可供使用：[HDInsight .NET 示例](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples)。</span><span class="sxs-lookup"><span data-stu-id="bad44-137">Code samples for creating several common types of HDInsight clusters are available: [HDInsight .NET Samples](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="bad44-138">示例</span><span class="sxs-lookup"><span data-stu-id="bad44-138">Example</span></span>

<span data-ttu-id="bad44-139">本示例演示如何创建包含 2 个头节点和 1 个工作节点的 Spark 群集。</span><span class="sxs-lookup"><span data-stu-id="bad44-139">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="bad44-140">首先需要创建一个资源组和存储帐户，下面将予以介绍。</span><span class="sxs-lookup"><span data-stu-id="bad44-140">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="bad44-141">如果已创建资源组和存储帐户，则可以跳过这些步骤。</span><span class="sxs-lookup"><span data-stu-id="bad44-141">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="bad44-142">创建资源组</span><span class="sxs-lookup"><span data-stu-id="bad44-142">Creating a Resource Group</span></span>

<span data-ttu-id="bad44-143">可以在 [Azure Cloud Shell](https://shell.azure.com/bash) 中运行以下命令来创建资源组</span><span class="sxs-lookup"><span data-stu-id="bad44-143">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="bad44-144">创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="bad44-144">Creating a Storage Account</span></span>

<span data-ttu-id="bad44-145">可以在 [Azure Cloud Shell](https://shell.azure.com/bash) 中运行以下命令来创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="bad44-145">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="bad44-146">现在，运行以下命令获取存储帐户的密钥（创建群集时需要用到）：</span><span class="sxs-lookup"><span data-stu-id="bad44-146">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="bad44-147">以下 .NET 代码片段创建包含 2 个头节点和 1 个工作节点的 Spark 群集。</span><span class="sxs-lookup"><span data-stu-id="bad44-147">The below .NET snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="bad44-148">按照注释中所述填写空白变量，并根据具体的需要任意更改其他参数。</span><span class="sxs-lookup"><span data-stu-id="bad44-148">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="bad44-149">获取群集详细信息</span><span class="sxs-lookup"><span data-stu-id="bad44-149">Get Cluster Details</span></span>

<span data-ttu-id="bad44-150">获取给定群集的属性：</span><span class="sxs-lookup"><span data-stu-id="bad44-150">To get properties for a given cluster:</span></span>

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="bad44-151">示例</span><span class="sxs-lookup"><span data-stu-id="bad44-151">Example</span></span>

<span data-ttu-id="bad44-152">可以使用 `get` 来确认已成功创建群集。</span><span class="sxs-lookup"><span data-stu-id="bad44-152">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

<span data-ttu-id="bad44-153">输出应如下所示：</span><span class="sxs-lookup"><span data-stu-id="bad44-153">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> <span data-ttu-id="bad44-154">存储在变量 `myCluster` 中的 `get` 返回值的类型为 `Microsoft.Azure.Management.HDInsight.ModelsCluster`。</span><span class="sxs-lookup"><span data-stu-id="bad44-154">The return value of `get`, stored in variable `myCluster`, is of type `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span></span> <span data-ttu-id="bad44-155">可在[此处](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview)找到此对象的属性的完整列表。</span><span class="sxs-lookup"><span data-stu-id="bad44-155">A full list of this object's properties can be found [here](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span></span>


### <a name="list-clusters"></a><span data-ttu-id="bad44-156">列出群集</span><span class="sxs-lookup"><span data-stu-id="bad44-156">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="bad44-157">列出订阅下的群集</span><span class="sxs-lookup"><span data-stu-id="bad44-157">List Clusters Under The Subscription</span></span>

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="bad44-158">按资源组列出群集</span><span class="sxs-lookup"><span data-stu-id="bad44-158">List Clusters By Resource Group</span></span>

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="bad44-159">`List()` 和 `ListByResourceGroup()` 都返回 `IPage<Cluster>` 对象。</span><span class="sxs-lookup"><span data-stu-id="bad44-159">Both `List()` and `ListByResourceGroup()` return an `IPage<Cluster>` object.</span></span> <span data-ttu-id="bad44-160">若要获取下一个页面，可以调用 `client.Clusters.ListNext("Next Page Link")`。</span><span class="sxs-lookup"><span data-stu-id="bad44-160">To get the next page, you can call `client.Clusters.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="bad44-161">可以反复执行此调用，直到 `NextPageLink` 为 `null`，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="bad44-161">This can be repeated until `NextPageLink` is `null`, as shown in the example below.</span></span>

#### <a name="example"></a><span data-ttu-id="bad44-162">示例</span><span class="sxs-lookup"><span data-stu-id="bad44-162">Example</span></span>
<span data-ttu-id="bad44-163">以下示例列显当前订阅的所有群集的属性：</span><span class="sxs-lookup"><span data-stu-id="bad44-163">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="bad44-164">删除群集</span><span class="sxs-lookup"><span data-stu-id="bad44-164">Delete a Cluster</span></span>

<span data-ttu-id="bad44-165">删除群集：</span><span class="sxs-lookup"><span data-stu-id="bad44-165">To delete a cluster:</span></span>

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="bad44-166">更新群集标记</span><span class="sxs-lookup"><span data-stu-id="bad44-166">Update Cluster Tags</span></span>

<span data-ttu-id="bad44-167">可按如下所示更新给定群集的标记：</span><span class="sxs-lookup"><span data-stu-id="bad44-167">You can update the tags of a given cluster like so:</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a><span data-ttu-id="bad44-168">示例</span><span class="sxs-lookup"><span data-stu-id="bad44-168">Example</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a><span data-ttu-id="bad44-169">调整群集大小</span><span class="sxs-lookup"><span data-stu-id="bad44-169">Resize Cluster</span></span>

<span data-ttu-id="bad44-170">可以通过指定新大小来调整给定群集的工作节点数，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bad44-170">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="bad44-171">群集监视</span><span class="sxs-lookup"><span data-stu-id="bad44-171">Cluster Monitoring</span></span>

<span data-ttu-id="bad44-172">使用 HDInsight 管理 SDK 还可以通过 Operations Management Suite (OMS) 来管理群集的监视。</span><span class="sxs-lookup"><span data-stu-id="bad44-172">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="bad44-173">启用 OMS 监视</span><span class="sxs-lookup"><span data-stu-id="bad44-173">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="bad44-174">若要启用 OMS 监视，必须已有一个 Log Analytics 工作区。</span><span class="sxs-lookup"><span data-stu-id="bad44-174">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="bad44-175">如果尚未创建工作区，可在此了解创建方法：[在 Azure 门户中创建 Log Analytics 工作区](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace)。</span><span class="sxs-lookup"><span data-stu-id="bad44-175">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="bad44-176">在群集上启用 OMS 监视：</span><span class="sxs-lookup"><span data-stu-id="bad44-176">To enable OMS Monitoring on your cluster:</span></span>

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="bad44-177">查看 OMS 监视状态</span><span class="sxs-lookup"><span data-stu-id="bad44-177">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="bad44-178">获取群集上的 OMS 状态：</span><span class="sxs-lookup"><span data-stu-id="bad44-178">To get the status of OMS on your cluster:</span></span>

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="bad44-179">禁用 OMS 监视</span><span class="sxs-lookup"><span data-stu-id="bad44-179">Disable OMS Monitoring</span></span>

<span data-ttu-id="bad44-180">在群集上禁用 OMS：</span><span class="sxs-lookup"><span data-stu-id="bad44-180">To disable OMS on your cluster:</span></span>

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="bad44-181">脚本操作</span><span class="sxs-lookup"><span data-stu-id="bad44-181">Script Actions</span></span>

<span data-ttu-id="bad44-182">HDInsight 提供一个称为“脚本操作”的配置方法，该方法可调用用于自定义群集的自定义脚本。</span><span class="sxs-lookup"><span data-stu-id="bad44-182">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="bad44-183">有关如何使用脚本操作的详细信息见此处：[使用脚本操作自定义基于 Linux 的 HDInsight 群集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="bad44-183">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="bad44-184">执行脚本操作</span><span class="sxs-lookup"><span data-stu-id="bad44-184">Execute Script Actions</span></span>

<span data-ttu-id="bad44-185">可按如下所示在给定的群集上执行脚本操作：</span><span class="sxs-lookup"><span data-stu-id="bad44-185">You can execute script actions on a given cluster like so:</span></span>

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="bad44-186">删除脚本操作</span><span class="sxs-lookup"><span data-stu-id="bad44-186">Delete Script Action</span></span>

<span data-ttu-id="bad44-187">删除给定群集上指定的持久化脚本操作：</span><span class="sxs-lookup"><span data-stu-id="bad44-187">To delete a specified persisted script action on a given cluster:</span></span>

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="bad44-188">列出持久化脚本操作</span><span class="sxs-lookup"><span data-stu-id="bad44-188">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="bad44-189">`ListPersistedScripts()` 和 `List()` 返回 `IPage<RuntimeScriptActionDetail>` 对象。</span><span class="sxs-lookup"><span data-stu-id="bad44-189">`ListPersistedScripts()` and `List()` return an `IPage<RuntimeScriptActionDetail>` object.</span></span> <span data-ttu-id="bad44-190">若要获取下一个页面，可以调用 `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` 或 `client.ScriptExecutionHistory.ListNext("Next Page Link")`。</span><span class="sxs-lookup"><span data-stu-id="bad44-190">To get the next page, you can call `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` or `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="bad44-191">可以反复执行此调用，直到 `NextPageLink` 为 `null`，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="bad44-191">This can be repeated until `NextPageLink` is `null`, as shown in the examples below.</span></span>

<span data-ttu-id="bad44-192">列出指定群集的所有持久化脚本操作：</span><span class="sxs-lookup"><span data-stu-id="bad44-192">To list all persisted script actions for the specified cluster:</span></span>
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="bad44-193">示例</span><span class="sxs-lookup"><span data-stu-id="bad44-193">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="bad44-194">列出所有脚本的执行历史记录</span><span class="sxs-lookup"><span data-stu-id="bad44-194">List All Scripts' Execution History</span></span>

<span data-ttu-id="bad44-195">列出指定群集的所有脚本的执行历史记录：</span><span class="sxs-lookup"><span data-stu-id="bad44-195">To list all scripts' execution history for the specified cluster:</span></span>

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="bad44-196">示例</span><span class="sxs-lookup"><span data-stu-id="bad44-196">Example</span></span>

<span data-ttu-id="bad44-197">此示例列显以往所有脚本执行活动的所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="bad44-197">This example prints all the details for all past script executions.</span></span>

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

## <a name="jobs"></a><span data-ttu-id="bad44-198">作业</span><span class="sxs-lookup"><span data-stu-id="bad44-198">Jobs</span></span>

<span data-ttu-id="bad44-199">使用用于 .NET 的 Azure HDInsight 作业 SDK 可创建、管理和监视 Hadoop 群集上的作业。</span><span class="sxs-lookup"><span data-stu-id="bad44-199">Use the Azure HDInsight job SDK for .NET to create, manage, and monitor jobs on a Hadoop cluster.</span></span>

### <a name="sdk-installation"></a><span data-ttu-id="bad44-200">SDK 安装</span><span class="sxs-lookup"><span data-stu-id="bad44-200">SDK Installation</span></span>

<span data-ttu-id="bad44-201">直接从 Visual Studio [包管理器控制台][PackageManager] 或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job)。</span><span class="sxs-lookup"><span data-stu-id="bad44-201">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bad44-202">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="bad44-202">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

### <a name="code-example"></a><span data-ttu-id="bad44-203">代码示例</span><span class="sxs-lookup"><span data-stu-id="bad44-203">Code Example</span></span>

<span data-ttu-id="bad44-204">此示例在 Hadoop 群集中运行 Hive 作业。</span><span class="sxs-lookup"><span data-stu-id="bad44-204">This example runs a Hive job in a Hadoop cluster.</span></span>

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

### <a name="samples"></a><span data-ttu-id="bad44-205">示例</span><span class="sxs-lookup"><span data-stu-id="bad44-205">Samples</span></span>

- [<span data-ttu-id="bad44-206">运行 Hive 作业</span><span class="sxs-lookup"><span data-stu-id="bad44-206">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="bad44-207">运行 Pig 作业</span><span class="sxs-lookup"><span data-stu-id="bad44-207">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="bad44-208">更多作业</span><span class="sxs-lookup"><span data-stu-id="bad44-208">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)
