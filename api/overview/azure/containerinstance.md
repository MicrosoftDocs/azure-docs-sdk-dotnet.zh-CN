---
title: 适用于 .NET 的 Azure 容器实例库
description: 适用于 .NET 的 Azure 容器实例库参考
keywords: Azure, .NET, SDK, API, 容器实例, ACI
author: mmacy
ms.author: marsma
manager: jeconnoc
ms.date: 05/25/2018
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: dcontainer-instances
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 033f67a989b0ed6cfcb67a6212c0d5c46c485afa
ms.sourcegitcommit: 4ae9f77a9300a4fe54d0179055ae61191078f207
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34567177"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="52d59-104">适用于 .NET 的 Azure 容器实例库</span><span class="sxs-lookup"><span data-stu-id="52d59-104">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="52d59-105">使用适用于 .NET 的 Microsoft Azure 容器实例库来创建和管理 Azure 容器实例。</span><span class="sxs-lookup"><span data-stu-id="52d59-105">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="52d59-106">请阅读 [Azure 容器实例概述](/azure/container-instances/container-instances-overview)了解详细信息。</span><span class="sxs-lookup"><span data-stu-id="52d59-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="52d59-107">管理库</span><span class="sxs-lookup"><span data-stu-id="52d59-107">Management library</span></span>

<span data-ttu-id="52d59-108">使用管理库可在 Azure 中创建和管理 Azure 容器实例。</span><span class="sxs-lookup"><span data-stu-id="52d59-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="52d59-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent)。</span><span class="sxs-lookup"><span data-stu-id="52d59-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="52d59-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="52d59-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="examples"></a><span data-ttu-id="52d59-111">示例</span><span class="sxs-lookup"><span data-stu-id="52d59-111">Examples</span></span>

### <a name="create-container-group---single-container"></a><span data-ttu-id="52d59-112">创建容器组 - 单个容器</span><span class="sxs-lookup"><span data-stu-id="52d59-112">Create container group - single container</span></span>

<span data-ttu-id="52d59-113">此示例创建包含单个容器的容器组。</span><span class="sxs-lookup"><span data-stu-id="52d59-113">This example creates a container group with a single container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

### <a name="create-container-group---multiple-containers"></a><span data-ttu-id="52d59-114">创建容器组 - 多个容器</span><span class="sxs-lookup"><span data-stu-id="52d59-114">Create container group - multiple containers</span></span>

<span data-ttu-id="52d59-115">此示例创建包含两个容器的容器组：应用程序容器和挎斗容器。</span><span class="sxs-lookup"><span data-stu-id="52d59-115">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

### <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="52d59-116">通过轮询进行异步容器创建</span><span class="sxs-lookup"><span data-stu-id="52d59-116">Asynchronous container create with polling</span></span>

<span data-ttu-id="52d59-117">此示例使用异步创建方法创建包含单个容器的容器组。</span><span class="sxs-lookup"><span data-stu-id="52d59-117">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="52d59-118">然后，它将在 Azure 中轮询该容器组，并且会输出容器组的状态，直到其状态为“Running”。</span><span class="sxs-lookup"><span data-stu-id="52d59-118">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

### <a name="create-task-based-container-group"></a><span data-ttu-id="52d59-119">创建基于任务的容器组</span><span class="sxs-lookup"><span data-stu-id="52d59-119">Create task-based container group</span></span>

<span data-ttu-id="52d59-120">此示例创建包含单个基于任务的容器的容器组。</span><span class="sxs-lookup"><span data-stu-id="52d59-120">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="52d59-121">该容器配置有[重新启动策略](/azure/container-instances/container-instances-restart-policy)“Never”以及一个[自定义命令行](/azure/container-instances/container-instances-restart-policy#command-line-override)。</span><span class="sxs-lookup"><span data-stu-id="52d59-121">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="52d59-122">如果要运行带有多个命令行参数的单个命令，例如 `echo FOO BAR`，必须以字符串数组的形式向 `WithStartingCommandLines` 方法提供这些参数。</span><span class="sxs-lookup"><span data-stu-id="52d59-122">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="52d59-123">例如：</span><span class="sxs-lookup"><span data-stu-id="52d59-123">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="52d59-124">但是，如果要运行带有（可能）多个参数的多个命令，必须执行 shell，并将链接的命令作为参数传递。</span><span class="sxs-lookup"><span data-stu-id="52d59-124">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="52d59-125">例如，这样可以执行 `echo` 和 `tail` 命令：</span><span class="sxs-lookup"><span data-stu-id="52d59-125">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

### <a name="list-container-groups"></a><span data-ttu-id="52d59-126">列出容器组</span><span class="sxs-lookup"><span data-stu-id="52d59-126">List container groups</span></span>

<span data-ttu-id="52d59-127">此示例列出了资源组中的容器组。</span><span class="sxs-lookup"><span data-stu-id="52d59-127">This example lists the container groups in a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

### <a name="get-an-existing-container-group"></a><span data-ttu-id="52d59-128">获取现有的容器组</span><span class="sxs-lookup"><span data-stu-id="52d59-128">Get an existing container group</span></span>

<span data-ttu-id="52d59-129">此示例获取驻留在资源组中的特定容器组，然后打印其一些属性及属性值。</span><span class="sxs-lookup"><span data-stu-id="52d59-129">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

### <a name="delete-a-container-group"></a><span data-ttu-id="52d59-130">删除容器组</span><span class="sxs-lookup"><span data-stu-id="52d59-130">Delete a container group</span></span>

<span data-ttu-id="52d59-131">此示例将从资源组中删除容器组。</span><span class="sxs-lookup"><span data-stu-id="52d59-131">This example deletes a container group from a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a><span data-ttu-id="52d59-132">API 参考</span><span class="sxs-lookup"><span data-stu-id="52d59-132">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52d59-133">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="52d59-133">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="52d59-134">示例</span><span class="sxs-lookup"><span data-stu-id="52d59-134">Samples</span></span>

* <span data-ttu-id="52d59-135">可以在 GitHub 上找到前面示例的源代码：</span><span class="sxs-lookup"><span data-stu-id="52d59-135">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="52d59-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="52d59-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="52d59-137">更多 Azure 容器实例代码示例：</span><span class="sxs-lookup"><span data-stu-id="52d59-137">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="52d59-138">[Azure 代码示例][samples]</span><span class="sxs-lookup"><span data-stu-id="52d59-138">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="52d59-139">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="52d59-139">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
