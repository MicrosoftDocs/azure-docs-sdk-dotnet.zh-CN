---
title: 使用 .NET Core 从命令行部署到 Azure
description: 本文介绍如何使用命令行工具将 ASP.NET Core 应用程序部署到 Azure 应用服务。
keywords: Azure.NET, SDK, Azure.NET API 参考, Azure.NET 类库
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: 8371c304681ff88cba6f1cc3ba0d1caef836d609
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2018
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a><span data-ttu-id="1a540-104">使用 .NET Core 从命令行部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="1a540-104">Deploy to Azure from the command line with .NET Core</span></span>

<span data-ttu-id="1a540-105">本教程逐步讲解如何使用 .NET Core 生成和部署 Microsoft Azure 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1a540-105">This tutorial will walk you through building and deploying a Microsoft Azure application using .NET Core.</span></span>  <span data-ttu-id="1a540-106">完成本教程后，ASP.NET MVC Core 中会生成一个基于 Web 的待办事项应用程序，该应用程序以 Azure Web 应用的形式托管，并将 Azure Cosmos DB 用于数据存储。</span><span class="sxs-lookup"><span data-stu-id="1a540-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure Cosmos DB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a540-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="1a540-107">Prerequisites</span></span>

* <span data-ttu-id="1a540-108">[Microsoft Azure 订阅](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="1a540-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="1a540-109">[.NET Core](https://www.microsoft.com/net/download/core)（可选）</span><span class="sxs-lookup"><span data-stu-id="1a540-109">[.NET Core](https://www.microsoft.com/net/download/core) (optional)</span></span>
* <span data-ttu-id="1a540-110">[Azure CLI 2.0](/cli/azure/install-az-cli2)（可选）</span><span class="sxs-lookup"><span data-stu-id="1a540-110">[Azure CLI 2.0](/cli/azure/install-az-cli2) (optional)</span></span>
* <span data-ttu-id="1a540-111">[Git](https://www.git-scm.com/) 命令行客户端（可选）</span><span class="sxs-lookup"><span data-stu-id="1a540-111">[Git](https://www.git-scm.com/) command line client (optional)</span></span>

<span data-ttu-id="1a540-112">[Azure Cloud Shell](/azure/cloud-shell/) 中预先安装了本教程所需的所有可选组件和必备组件。</span><span class="sxs-lookup"><span data-stu-id="1a540-112">The [Azure Cloud Shell](/azure/cloud-shell/) has all of the optional prerequisites for this tutorial preinstalled.</span></span>  <span data-ttu-id="1a540-113">如果想要在本地运行本教程，只需安装上述可选组件。</span><span class="sxs-lookup"><span data-stu-id="1a540-113">You only need to install the optional components above if you wish to run the tutorial locally.</span></span>  <span data-ttu-id="1a540-114">若要快速启动 Cloud Shell，只需单击下面任一代码块右上角的“试用”按钮。</span><span class="sxs-lookup"><span data-stu-id="1a540-114">To quickly launch the Cloud Shell, just click the **Try it** button in the top-right of any of the below code blocks.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="1a540-115">创建 Azure Cosmos DB 帐户</span><span class="sxs-lookup"><span data-stu-id="1a540-115">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="1a540-116">Azure Cosmos DB 在本教程中用于数据存储，因此需要创建一个帐户。</span><span class="sxs-lookup"><span data-stu-id="1a540-116">Azure Cosmos DB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="1a540-117">在本地或 Cloud Shell 中运行此脚本，以创建 Azure Cosmos DB SQL API 帐户。</span><span class="sxs-lookup"><span data-stu-id="1a540-117">Run this script locally or in the Cloud Shell to create an Azure Cosmos DB SQL API account.</span></span>

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

```

## <a name="download-and-configure-the-application"></a><span data-ttu-id="1a540-118">下载并配置应用程序</span><span class="sxs-lookup"><span data-stu-id="1a540-118">Download and configure the application</span></span>

<span data-ttu-id="1a540-119">要部署的应用程序是在 ASP.NET MVC Core 中使用 Azure Cosmos DB 客户端库编写的[简单待办事项应用](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/)。</span><span class="sxs-lookup"><span data-stu-id="1a540-119">The application you're going to deploy is a [simple to-do app](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) written using ASP.NET MVC Core using the Azure Cosmos DB client libraries.</span></span>  <span data-ttu-id="1a540-120">现在，请获取本教程的代码，并使用 Azure Cosmos DB 信息对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="1a540-120">Now you'll get the code for this tutorial and configure it with your Azure Cosmos DB information.</span></span>

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
> <span data-ttu-id="1a540-121">如果以前从未在此环境中运行过 `git commit`，系统可能会提示设置标识。</span><span class="sxs-lookup"><span data-stu-id="1a540-121">If you've never run `git commit` in this environment before, you may be prompted to set your identity.</span></span> <span data-ttu-id="1a540-122">请遵照屏幕说明操作，然后再次运行 `git commit` 命令。</span><span class="sxs-lookup"><span data-stu-id="1a540-122">Follow the on-screen instructions and then re-run the `git commit` command.</span></span>

<span data-ttu-id="1a540-123">还原 NuGet 包并生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="1a540-123">Restore the NuGet packages and build the application.</span></span>

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> <span data-ttu-id="1a540-124">如果使用自己计算机上的工具，可以通过运行 `dotnet run` 并浏览到显示的 `localhost` 地址来测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="1a540-124">If you are using the tools on your own machine, you can test the application by running `dotnet run` and browsing to the displayed `localhost` address.</span></span>  <span data-ttu-id="1a540-125">但是，不能在 Cloud Shell 中浏览到此地址。</span><span class="sxs-lookup"><span data-stu-id="1a540-125">You are not able to browse to this address in the Cloud Shell, however.</span></span>  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a><span data-ttu-id="1a540-126">配置 Azure 应用服务并部署 Web 应用</span><span class="sxs-lookup"><span data-stu-id="1a540-126">Configure Azure App Service and deploy the web app</span></span>

<span data-ttu-id="1a540-127">现已成功下载并生成 Web 应用程序，接下来可将它部署为 Azure Web 应用。</span><span class="sxs-lookup"><span data-stu-id="1a540-127">You've successfully downloaded and built the web application, and you're ready to deploy it as an Azure Web App.</span></span>  <span data-ttu-id="1a540-128">首先，请创建 Web 应用资源。</span><span class="sxs-lookup"><span data-stu-id="1a540-128">You'll start by creating the Web App resource.</span></span>

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

<span data-ttu-id="1a540-129">在部署之前，需要设置帐户级部署凭据。</span><span class="sxs-lookup"><span data-stu-id="1a540-129">Before you deploy, you need to set the account-level deployment credentials.</span></span>  <span data-ttu-id="1a540-130">使用以下脚本，同时请确保为用户名和密码使用自己的值。</span><span class="sxs-lookup"><span data-stu-id="1a540-130">Use the script below, making sure to include your own values for the user name and password.</span></span>

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

<span data-ttu-id="1a540-131">最后，将应用程序部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1a540-131">Finally, deploy the application to Azure.</span></span>  <span data-ttu-id="1a540-132">系统会提示输入前面创建的密码。</span><span class="sxs-lookup"><span data-stu-id="1a540-132">You will be prompted for the password you created above.</span></span>

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

<span data-ttu-id="1a540-133">将在远程生成并部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="1a540-133">The application will be built remotely and deployed.</span></span>  <span data-ttu-id="1a540-134">通过浏览到 `https://<web app name>.azurewebsites.net` 来测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="1a540-134">Test the application by browsing to `https://<web app name>.azurewebsites.net`.</span></span>  <span data-ttu-id="1a540-135">若要在控制台中显示地址，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="1a540-135">To display the address in the console, use the following:</span></span>

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

<span data-ttu-id="1a540-136">可以通过单击“新建”将新项添加到待办事项列表。</span><span class="sxs-lookup"><span data-stu-id="1a540-136">You can add new items to the to-do list by clicking **Create New**.</span></span>

![完成的应用](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="1a540-138">清理</span><span class="sxs-lookup"><span data-stu-id="1a540-138">Clean up</span></span>

<span data-ttu-id="1a540-139">测试完应用并检查代码和资源后，可以通过删除资源组来删除 Web 应用和 Azure Cosmos DB 帐户。</span><span class="sxs-lookup"><span data-stu-id="1a540-139">When you're done testing the app and inspecting the code and resources, you can delete the Web App and Azure Cosmos DB account by deleting the resource group.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="1a540-140">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1a540-140">Next steps</span></span>

* [<span data-ttu-id="1a540-141">在 ASP.NET Web 应用程序中使用 Azure Active Directory 进行身份验证</span><span class="sxs-lookup"><span data-stu-id="1a540-141">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="1a540-142">使用 Azure SQL 数据库生成 Azure Web 应用</span><span class="sxs-lookup"><span data-stu-id="1a540-142">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="1a540-143">结合 Azure 存储尝试运行 .NET 示例应用程序</span><span class="sxs-lookup"><span data-stu-id="1a540-143">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


