---
title: "使用 .NET Core 从命令行部署到 Azure"
description: "本文介绍如何使用命令行工具将 ASP.NET Core 应用程序部署到 Azure 应用服务。"
keywords: "Azure.NET, SDK, Azure.NET API 参考, Azure.NET 类库"
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.assetid: 
ms.openlocfilehash: 2ed69bfed7310c9e6b2f3f8fedb906ce33d87c3c
ms.sourcegitcommit: c630918c9e17f5e3c6d4f28fe740c041f60b1e66
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2017
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a>使用 .NET Core 从命令行部署到 Azure

本教程逐步讲解如何使用 .NET Core 生成和部署 Microsoft Azure 应用程序。  完成本教程后，ASP.NET MVC Core 中会生成一个基于 Web 的待办事项应用程序，该应用程序以 Azure Web 应用的形式托管，并使用 Azure CosmosDB 作为数据存储。

## <a name="prerequisites"></a>先决条件

* [Microsoft Azure 订阅](https://azure.microsoft.com/free/)
* [.NET Core](https://www.microsoft.com/net/download/core)（可选）
* [Azure CLI 2.0](/cli/azure/install-az-cli2)（可选）
* [Git](https://www.git-scm.com/) 命令行客户端（可选）

[Azure Cloud Shell](/azure/cloud-shell/) 中预先安装了本教程所需的所有可选组件和必备组件。  如果想要在本地运行本教程，只需安装上述可选组件。  若要快速启动 Cloud Shell，只需单击下面任一代码块右上角的“试用”按钮。

## <a name="create-a-cosmosdb-account"></a>创建 CosmosDB 帐户

CosmosDB 在本教程中用作数据存储，因此需要创建一个帐户。  在本地或 Cloud Shell 中运行此脚本，以创建 Azure CosmosDB DocumentDB API 帐户。

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the CosmosDB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)

```

## <a name="download-and-configure-the-application"></a>下载并配置应用程序

要部署的应用程序是在 ASP.NET MVC Core 中使用 CosmosDB 客户端库编写的[简单待办事项应用](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/)。  现在，请获取本教程的代码，并使用 CosmosDB 信息对其进行配置。

```azurecli-interactive
# Get the code from GitHub
git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart

# Change the working directory
cd dotnet-cosmosdb-quickstart

# Replace authKey and endpoint values in appsettings.json
sed -i "s|AUTHKEYVALUE|$cosmosAuthKey|g" appsettings.json
sed -i "s|ENDPOINTVALUE|$cosmosEndpoint|g" appsettings.json

# Now commit your changes to the local Git repository.
git commit -a -m "Modified settings"

```

> [!NOTE]
> 如果以前从未在此环境中运行过 `git commit`，系统可能会提示设置标识。 请遵照屏幕说明操作，然后再次运行 `git commit` 命令。

还原 NuGet 包并生成应用程序。

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> 如果使用自己计算机上的工具，可以通过运行 `dotnet run` 并浏览到显示的 `localhost` 地址来测试应用程序。  但是，不能在 Cloud Shell 中浏览到此地址。  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a>配置 Azure 应用服务并部署 Web 应用

现已成功下载并生成 Web 应用程序，接下来可将它部署为 Azure Web 应用。  首先，请创建 Web 应用资源。

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

在部署之前，需要设置帐户级部署凭据。  使用以下脚本，同时请确保为用户名和密码使用自己的值。

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

最后，将应用程序部署到 Azure。  系统会提示输入前面创建的密码。

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

将在远程生成并部署应用程序。  通过浏览到 `https://<web app name>.azurewebsites.net` 来测试应用程序。  若要在控制台中显示地址，请使用以下命令：

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

可以通过单击“新建”将新项添加到待办事项列表。

![完成的应用](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>清理

测试完应用并检查代码和资源后，可以通过删除资源组来删除 Web 应用和 CosmosDB 帐户。

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>后续步骤

* [在 ASP.NET Web 应用程序中使用 Azure Active Directory 进行身份验证](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [使用 Azure SQL 数据库生成 Azure Web 应用](/azure/app-service-web/web-sites-dotnet-get-started)
* [结合 Azure 存储尝试运行 .NET 示例应用程序](/azure/storage/storage-samples-dotnet)


