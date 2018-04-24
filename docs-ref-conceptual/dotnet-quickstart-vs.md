---
title: 从 Visual Studio 部署到 Azure
description: 本教程逐步讲解如何使用 Visual Studio 和 .NET 来生成及部署 Microsoft Azure 应用程序。
keywords: Azure.NET, SDK, Azure.NET API 参考, Azure.NET 类库
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: 87f65d8b8b1b1a5184b9d71770c08be472c7e498
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2018
---
# <a name="deploy-to-azure-from-visual-studio"></a>从 Visual Studio 部署到 Azure

本教程逐步讲解如何使用 Visual Studio 和 .NET 来生成及部署 Microsoft Azure 应用程序。  完成本教程后，ASP.NET MVC Core 中会生成一个基于 Web 的待办事项应用程序，该应用程序以 Azure Web 应用的形式托管，并将 Azure Cosmos DB 用于数据存储。

## <a name="prerequisites"></a>先决条件

* [Visual Studio 2017](https://www.visualstudio.com/downloads/)
* [Microsoft Azure 订阅](https://azure.microsoft.com/free/)

## <a name="create-an-azure-cosmos-db-account"></a>创建 Azure Cosmos DB 帐户

Azure Cosmos DB 在本教程中用于数据存储，因此需要创建一个帐户。  在本地或 Cloud Shell 中运行此脚本，以创建 Azure Cosmos DB SQL API 帐户。  在以下代码块上单击“试用”按钮，启动 [Azure Cloud Shell](/azure/cloud-shell/) 并将脚本块复制/粘贴到 shell 中。

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the Azure Cosmos DB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)
printf "\n\nauthKey: $cosmosAuthKey\nendpoint: $cosmosEndpoint\n\n"

# Done!

```

记下显示的 **authKey** 和 **endpoint** 值 

## <a name="downloading-and-running-the-application"></a>下载并运行应用程序

让我们获取用于本演练的示例代码，并将其挂接到 Azure Cosmos DB 帐户。

1. 下载示例代码。  可以[从 GitHub 获取示例代码](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/)；如果已安装 [git 命令行客户端](https://git-scm.com/)，请使用以下命令将其克隆到本地计算机：

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. 在 Visual Studio 中打开 **todo.csproj**。

3. 打开 Web 项目中的 **appsettings.json**。  查找以下行：

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    将 **AUTHKEYVALUE** 和 **ENDPOINTVALUE** 替换为前面记下的值。

4. 按 **F5** 还原项目的 NuGet 包，生成项目，并在本地运行项目。

Web 应用程序应在浏览器中本地运行。  可以通过单击“新建”将新项添加到待办事项列表。  可以看到，在应用程序中输入的数据正存储到 Azure Cosmos DB 帐户中。  可以通过从左侧菜单中选择 Azure Cosmos DB，选择帐户，然后选择“数据资源管理器”，在 [Azure 门户](https://portal.azure.com)中查看数据。

## <a name="deploying-the-application-as-an-azure-web-app"></a>将应用程序部署为 Azure Web 应用

现在已成功生成一个使用 Azure Cosmos DB 等 Azure 服务的应用程序。  接下来，将 Web 应用程序部署到云中。

> [!IMPORTANT]
> 请务必使用与 Azure 订阅关联的同一帐户登录到 Visual Studio。

1. 在 Visual Studio 的解决方案资源管理器中，右键单击项目名称并选择“发布...”。

2. 在“发布”对话框下，依次选择“Microsoft Azure 应用服务”和“新建”，并单击“发布”。

3. 按如下所示完成“创建应用服务”对话框中的操作：

    * 输入唯一的 **Web 应用名称**。  此名称会包含在应用的 URL 中。
    * 选择要部署到的 Azure **订阅**。  使用前面登录到 Cloud Shell 时所用的同一订阅。
    * 选择“DotNetAzureTutorial”作为 Web 应用程序的**资源组**。
    * 选择或创建一个**应用服务计划**用于确定应用程序的定价。  此处提供了[有关应用服务计划的详细信息](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)。

4. 单击“创建”部署应用程序。  部署完成后，会打开一个浏览器，其中包含部署的应用程序。

![完成的应用](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>清理

测试完应用并检查代码和资源后，可以通过在 Cloud Shell 中删除资源组来删除 Web 应用和 Azure Cosmos DB 帐户。

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>后续步骤

* [在 ASP.NET Web 应用程序中使用 Azure Active Directory 进行身份验证](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [使用 Azure SQL 数据库生成 Azure Web 应用](/azure/app-service-web/web-sites-dotnet-get-started)
* [结合 Azure 存储尝试运行 .NET 示例应用程序](/azure/storage/storage-samples-dotnet)


