---
title: 适用于 .NET 的 Azure 容器实例库
description: 适用于 .NET 的 Azure 容器实例库参考
ms.date: 06/11/2018
ms.topic: reference
ms.service: dcontainer-instances
ms.openlocfilehash: 93f537058e0ed11f51cc6cb6cece01da80559822
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190720"
---
# <a name="azure-container-instances-libraries-for-net"></a>适用于 .NET 的 Azure 容器实例库

使用适用于 .NET 的 Microsoft Azure 容器实例库来创建和管理 Azure 容器实例。 请阅读 [Azure 容器实例概述](/azure/container-instances/container-instances-overview)，了解详细信息。

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

## <a name="example-source"></a>示例源

若要在上下文中查看以下代码示例，可以在以下 GitHub 存储库中找到它们：

[Azure-Samples/aci-docs-sample-dotnet](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a>身份验证

对 SDK 客户端进行身份验证的最简单方法之一是使用[基于文件的身份验证][sdk-auth]。 基于文件的身份验证会在实例化 [IAzure][iazure] 客户端对象时分析凭据文件，然后该对象将在向 Azure 进行身份验证时使用这些凭据。 若要使用基于文件的身份验证，请执行以下操作：

1. 使用 [Azure CLI](/cli/azure) 或 [Cloud Shell](https://shell.azure.com/) 创建凭据文件：

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   如果使用 [Cloud Shell](https://shell.azure.com/) 生成凭据文件，请将其内容复制到 .NET 应用程序能够访问的本地文件中。

2. 将 `AZURE_AUTH_LOCATION` 环境变量设置为生成的凭据文件的完整路径。 例如（在 Bash shell 中）：

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

在创建凭据文件并填充`AZURE_AUTH_LOCATION`环境变量后，请使用 [Azure.Authenticate][iazure-authenticate] 方法来初始化 [IAzure][iazure] 客户端对象。 该示例项目首先获取 `AZURE_AUTH_LOCATION` 值，然后调用一个方法，该方法将返回初始化的 `IAzure` 客户端对象：

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]

来自示例应用程序的此方法将返回初始化的 [IAzure][iazure] 实例，然后该示例将作为第一个参数传递到示例中的所有其他方法：

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]

若要更详细地了解用于 Azure 的 .NET 管理库中提供的身份验证方法，请参阅[用于 .NET 的 Azure 管理库中的身份验证][sdk-auth]。

## <a name="create-container-group---single-container"></a>创建容器组 - 单个容器

此示例创建包含单个容器的容器组。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>创建容器组 - 多个容器

此示例创建的容器组包含两个容器：应用程序容器和挎斗容器。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

## <a name="asynchronous-container-create-with-polling"></a>通过轮询进行异步容器创建

此示例使用异步创建方法创建包含单个容器的容器组。 然后，它将在 Azure 中轮询该容器组，并且会输出容器组的状态，直到其状态为“Running”。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

## <a name="create-task-based-container-group"></a>创建基于任务的容器组

此示例创建包含单个基于任务的容器的容器组。 该容器配置有[重新启动策略](/azure/container-instances/container-instances-restart-policy)“Never”以及一个[自定义命令行](/azure/container-instances/container-instances-restart-policy#command-line-override)。

如果要运行带有多个命令行参数的单个命令，例如 `echo FOO BAR`，必须以字符串数组的形式向 `WithStartingCommandLines` 方法提供这些参数。 例如：

`WithStartingCommandLines("echo", "FOO", "BAR")`

但是，如果要运行带有（可能）多个参数的多个命令，必须执行 shell，并将链接的命令作为参数传递。 例如，这样可以执行 `echo` 和 `tail` 命令：

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

## <a name="list-container-groups"></a>列出容器组

此示例列出了资源组中的容器组。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

## <a name="get-an-existing-container-group"></a>获取现有的容器组

此示例获取驻留在资源组中的特定容器组，然后打印其一些属性及属性值。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

## <a name="delete-a-container-group"></a>删除容器组

此示例将从资源组中删除容器组。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a>API 参考

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a>示例

* 可以在 GitHub 上找到前述示例的源代码：

  [Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]

* 更多 Azure 容器实例代码示例：

  [Azure 代码示例][samples]

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
