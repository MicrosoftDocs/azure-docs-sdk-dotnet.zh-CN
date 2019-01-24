---
title: 适用于 .NET 的 Azure 容器实例库
description: 适用于 .NET 的 Azure 容器实例库参考
ms.date: 06/11/2018
ms.topic: reference
ms.service: container-instances
ms.openlocfilehash: 552746b316f1ba80adce5f55bb22412749fd93bc
ms.sourcegitcommit: 4f7bc5c5cd333e41446a3ebe5639a211d8ac9b90
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2019
ms.locfileid: "54841274"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="3e385-103">适用于 .NET 的 Azure 容器实例库</span><span class="sxs-lookup"><span data-stu-id="3e385-103">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="3e385-104">使用适用于 .NET 的 Microsoft Azure 容器实例库来创建和管理 Azure 容器实例。</span><span class="sxs-lookup"><span data-stu-id="3e385-104">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="3e385-105">请阅读 [Azure 容器实例概述](/azure/container-instances/container-instances-overview)，了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="3e385-105">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="3e385-106">管理库</span><span class="sxs-lookup"><span data-stu-id="3e385-106">Management library</span></span>

<span data-ttu-id="3e385-107">使用管理库可在 Azure 中创建和管理 Azure 容器实例。</span><span class="sxs-lookup"><span data-stu-id="3e385-107">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="3e385-108">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="3e385-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="3e385-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="3e385-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a><span data-ttu-id="3e385-110">示例源</span><span class="sxs-lookup"><span data-stu-id="3e385-110">Example source</span></span>

<span data-ttu-id="3e385-111">若要在上下文中查看以下代码示例，可以在以下 GitHub 存储库中找到它们：</span><span class="sxs-lookup"><span data-stu-id="3e385-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="3e385-112">Azure-Samples/aci-docs-sample-dotnet</span><span class="sxs-lookup"><span data-stu-id="3e385-112">Azure-Samples/aci-docs-sample-dotnet</span></span>](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a><span data-ttu-id="3e385-113">身份验证</span><span class="sxs-lookup"><span data-stu-id="3e385-113">Authentication</span></span>

<span data-ttu-id="3e385-114">对 SDK 客户端进行身份验证的最简单方法之一是使用[基于文件的身份验证][sdk-auth]。</span><span class="sxs-lookup"><span data-stu-id="3e385-114">One of the easiest ways to authenticate SDK clients is with [file-based authentication][sdk-auth].</span></span> <span data-ttu-id="3e385-115">基于文件的身份验证会在实例化 [IAzure][iazure] 客户端对象时分析凭据文件，然后该对象将在向 Azure 进行身份验证时使用这些凭据。</span><span class="sxs-lookup"><span data-stu-id="3e385-115">File-based authentication parses a credentials file when instantiating the [IAzure][iazure] client object, which then uses those credentials when authenticating with Azure.</span></span> <span data-ttu-id="3e385-116">若要使用基于文件的身份验证，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3e385-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="3e385-117">使用 [Azure CLI](/cli/azure) 或 [Cloud Shell](https://shell.azure.com/) 创建凭据文件：</span><span class="sxs-lookup"><span data-stu-id="3e385-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="3e385-118">如果使用 [Cloud Shell](https://shell.azure.com/) 生成凭据文件，请将其内容复制到 .NET 应用程序能够访问的本地文件中。</span><span class="sxs-lookup"><span data-stu-id="3e385-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your .NET application can access.</span></span>

2. <span data-ttu-id="3e385-119">将 `AZURE_AUTH_LOCATION` 环境变量设置为生成的凭据文件的完整路径。</span><span class="sxs-lookup"><span data-stu-id="3e385-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="3e385-120">例如（在 Bash shell 中）：</span><span class="sxs-lookup"><span data-stu-id="3e385-120">For example (in the Bash shell):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="3e385-121">在创建凭据文件并填充`AZURE_AUTH_LOCATION`环境变量后，请使用 [Azure.Authenticate][iazure-authenticate] 方法来初始化 [IAzure][iazure] 客户端对象。</span><span class="sxs-lookup"><span data-stu-id="3e385-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the [Azure.Authenticate][iazure-authenticate] method to initialize the [IAzure][iazure] client object.</span></span> <span data-ttu-id="3e385-122">该示例项目首先获取 `AZURE_AUTH_LOCATION` 值，然后调用一个方法，该方法将返回初始化的 `IAzure` 客户端对象：</span><span class="sxs-lookup"><span data-stu-id="3e385-122">The example project first obtains the `AZURE_AUTH_LOCATION` value, then calls a method that returns an initialized `IAzure` client object:</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]

<span data-ttu-id="3e385-123">来自示例应用程序的此方法将返回初始化的 [IAzure][iazure] 实例，然后该示例将作为第一个参数传递到示例中的所有其他方法：</span><span class="sxs-lookup"><span data-stu-id="3e385-123">This method from the sample application returns the initialized [IAzure][iazure] instance, which is then passed as the first parameter to all other methods in the sample:</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]

<span data-ttu-id="3e385-124">若要更详细地了解用于 Azure 的 .NET 管理库中提供的身份验证方法，请参阅[用于 .NET 的 Azure 管理库中的身份验证][sdk-auth]。</span><span class="sxs-lookup"><span data-stu-id="3e385-124">For more details about the available authentication methods in the .NET management libraries for Azure, see [Authentication in Azure Management Libraries for .NET][sdk-auth].</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="3e385-125">创建容器组 - 单个容器</span><span class="sxs-lookup"><span data-stu-id="3e385-125">Create container group - single container</span></span>

<span data-ttu-id="3e385-126">此示例创建包含单个容器的容器组。</span><span class="sxs-lookup"><span data-stu-id="3e385-126">This example creates a container group with a single container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="3e385-127">创建容器组 - 多个容器</span><span class="sxs-lookup"><span data-stu-id="3e385-127">Create container group - multiple containers</span></span>

<span data-ttu-id="3e385-128">此示例创建包含两个容器的容器组：应用程序容器和挎斗容器。</span><span class="sxs-lookup"><span data-stu-id="3e385-128">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

## <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="3e385-129">通过轮询进行异步容器创建</span><span class="sxs-lookup"><span data-stu-id="3e385-129">Asynchronous container create with polling</span></span>

<span data-ttu-id="3e385-130">此示例使用异步创建方法创建包含单个容器的容器组。</span><span class="sxs-lookup"><span data-stu-id="3e385-130">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="3e385-131">然后，它将在 Azure 中轮询该容器组，并且会输出容器组的状态，直到其状态为“Running”。</span><span class="sxs-lookup"><span data-stu-id="3e385-131">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

## <a name="create-task-based-container-group"></a><span data-ttu-id="3e385-132">创建基于任务的容器组</span><span class="sxs-lookup"><span data-stu-id="3e385-132">Create task-based container group</span></span>

<span data-ttu-id="3e385-133">此示例创建包含单个基于任务的容器的容器组。</span><span class="sxs-lookup"><span data-stu-id="3e385-133">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="3e385-134">该容器配置有[重新启动策略](/azure/container-instances/container-instances-restart-policy)“Never”以及一个[自定义命令行](/azure/container-instances/container-instances-restart-policy#command-line-override)。</span><span class="sxs-lookup"><span data-stu-id="3e385-134">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="3e385-135">如果要运行带有多个命令行参数的单个命令，例如 `echo FOO BAR`，必须以字符串数组的形式向 `WithStartingCommandLines` 方法提供这些参数。</span><span class="sxs-lookup"><span data-stu-id="3e385-135">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="3e385-136">例如：</span><span class="sxs-lookup"><span data-stu-id="3e385-136">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="3e385-137">但是，如果要运行带有（可能）多个参数的多个命令，必须执行 shell，并将链接的命令作为参数传递。</span><span class="sxs-lookup"><span data-stu-id="3e385-137">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="3e385-138">例如，这样可以执行 `echo` 和 `tail` 命令：</span><span class="sxs-lookup"><span data-stu-id="3e385-138">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

## <a name="list-container-groups"></a><span data-ttu-id="3e385-139">列出容器组</span><span class="sxs-lookup"><span data-stu-id="3e385-139">List container groups</span></span>

<span data-ttu-id="3e385-140">此示例列出了资源组中的容器组。</span><span class="sxs-lookup"><span data-stu-id="3e385-140">This example lists the container groups in a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

## <a name="get-an-existing-container-group"></a><span data-ttu-id="3e385-141">获取现有的容器组</span><span class="sxs-lookup"><span data-stu-id="3e385-141">Get an existing container group</span></span>

<span data-ttu-id="3e385-142">此示例获取驻留在资源组中的特定容器组，然后打印其一些属性及属性值。</span><span class="sxs-lookup"><span data-stu-id="3e385-142">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

## <a name="delete-a-container-group"></a><span data-ttu-id="3e385-143">删除容器组</span><span class="sxs-lookup"><span data-stu-id="3e385-143">Delete a container group</span></span>

<span data-ttu-id="3e385-144">此示例将从资源组中删除容器组。</span><span class="sxs-lookup"><span data-stu-id="3e385-144">This example deletes a container group from a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a><span data-ttu-id="3e385-145">API 参考</span><span class="sxs-lookup"><span data-stu-id="3e385-145">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e385-146">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="3e385-146">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="3e385-147">示例</span><span class="sxs-lookup"><span data-stu-id="3e385-147">Samples</span></span>

* <span data-ttu-id="3e385-148">可以在 GitHub 上找到前述示例的源代码：</span><span class="sxs-lookup"><span data-stu-id="3e385-148">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="3e385-149">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="3e385-149">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="3e385-150">更多 Azure 容器实例代码示例：</span><span class="sxs-lookup"><span data-stu-id="3e385-150">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="3e385-151">[Azure 代码示例][samples]</span><span class="sxs-lookup"><span data-stu-id="3e385-151">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="3e385-152">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="3e385-152">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
