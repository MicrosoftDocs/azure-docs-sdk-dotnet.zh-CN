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
# <a name="azure-container-instances-libraries-for-net"></a>适用于 .NET 的 Azure 容器实例库

使用适用于 .NET 的 Microsoft Azure 容器实例库来创建和管理 Azure 容器实例。 请阅读 [Azure 容器实例概述](/azure/container-instances/container-instances-overview)了解详细信息。

## <a name="management-library"></a>管理库

使用管理库可在 Azure 中创建和管理 Azure 容器实例。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent)。

### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="examples"></a>示例

### <a name="create-container-group---single-container"></a>创建容器组 - 单个容器

此示例创建包含单个容器的容器组。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

### <a name="create-container-group---multiple-containers"></a>创建容器组 - 多个容器

此示例创建包含两个容器的容器组：应用程序容器和挎斗容器。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

### <a name="asynchronous-container-create-with-polling"></a>通过轮询进行异步容器创建

此示例使用异步创建方法创建包含单个容器的容器组。 然后，它将在 Azure 中轮询该容器组，并且会输出容器组的状态，直到其状态为“Running”。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

### <a name="create-task-based-container-group"></a>创建基于任务的容器组

此示例创建包含单个基于任务的容器的容器组。 该容器配置有[重新启动策略](/azure/container-instances/container-instances-restart-policy)“Never”以及一个[自定义命令行](/azure/container-instances/container-instances-restart-policy#command-line-override)。

如果要运行带有多个命令行参数的单个命令，例如 `echo FOO BAR`，必须以字符串数组的形式向 `WithStartingCommandLines` 方法提供这些参数。 例如：

`WithStartingCommandLines("echo", "FOO", "BAR")`

但是，如果要运行带有（可能）多个参数的多个命令，必须执行 shell，并将链接的命令作为参数传递。 例如，这样可以执行 `echo` 和 `tail` 命令：

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

### <a name="list-container-groups"></a>列出容器组

此示例列出了资源组中的容器组。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

### <a name="get-an-existing-container-group"></a>获取现有的容器组

此示例获取驻留在资源组中的特定容器组，然后打印其一些属性及属性值。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

### <a name="delete-a-container-group"></a>删除容器组

此示例将从资源组中删除容器组。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a>API 参考

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a>示例

* 可以在 GitHub 上找到前面示例的源代码：

  [Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]

* 更多 Azure 容器实例代码示例：

  [Azure 代码示例][samples]

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
