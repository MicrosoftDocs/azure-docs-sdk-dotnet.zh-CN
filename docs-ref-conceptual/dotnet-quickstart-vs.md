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
ms.locfileid: "31005884"
---
# <a name="deploy-to-azure-from-visual-studio"></a><span data-ttu-id="ea6b8-104">从 Visual Studio 部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="ea6b8-104">Deploy to Azure from Visual Studio</span></span>

<span data-ttu-id="ea6b8-105">本教程逐步讲解如何使用 Visual Studio 和 .NET 来生成及部署 Microsoft Azure 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-105">This tutorial will walk you through building and deploying a Microsoft Azure application using Visual Studio and .NET.</span></span>  <span data-ttu-id="ea6b8-106">完成本教程后，ASP.NET MVC Core 中会生成一个基于 Web 的待办事项应用程序，该应用程序以 Azure Web 应用的形式托管，并将 Azure Cosmos DB 用于数据存储。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure Cosmos DB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea6b8-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="ea6b8-107">Prerequisites</span></span>

* [<span data-ttu-id="ea6b8-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ea6b8-108">Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="ea6b8-109">[Microsoft Azure 订阅](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="ea6b8-109">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="ea6b8-110">创建 Azure Cosmos DB 帐户</span><span class="sxs-lookup"><span data-stu-id="ea6b8-110">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="ea6b8-111">Azure Cosmos DB 在本教程中用于数据存储，因此需要创建一个帐户。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-111">Azure Cosmos DB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="ea6b8-112">在本地或 Cloud Shell 中运行此脚本，以创建 Azure Cosmos DB SQL API 帐户。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-112">Run this script locally or in the Cloud Shell to create an Azure Cosmos DB SQL API account.</span></span>  <span data-ttu-id="ea6b8-113">在以下代码块上单击“试用”按钮，启动 [Azure Cloud Shell](/azure/cloud-shell/) 并将脚本块复制/粘贴到 shell 中。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-113">Click the **Try it** button on the code block below to launch the [Azure Cloud Shell](/azure/cloud-shell/) and copy/paste the script block into the shell.</span></span>

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

<span data-ttu-id="ea6b8-114">记下显示的 **authKey** 和 **endpoint** 值</span><span class="sxs-lookup"><span data-stu-id="ea6b8-114">Make a note of the displayed **authKey** and **endpoint**</span></span> 

## <a name="downloading-and-running-the-application"></a><span data-ttu-id="ea6b8-115">下载并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="ea6b8-115">Downloading and running the application</span></span>

<span data-ttu-id="ea6b8-116">让我们获取用于本演练的示例代码，并将其挂接到 Azure Cosmos DB 帐户。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-116">Let's get the sample code for this walkthrough and hook it up to your Azure Cosmos DB account.</span></span>

1. <span data-ttu-id="ea6b8-117">下载示例代码。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-117">Download the sample code.</span></span>  <span data-ttu-id="ea6b8-118">可以[从 GitHub 获取示例代码](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/)；如果已安装 [git 命令行客户端](https://git-scm.com/)，请使用以下命令将其克隆到本地计算机：</span><span class="sxs-lookup"><span data-stu-id="ea6b8-118">You can [get it from GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/), or if you have the [git command line client](https://git-scm.com/), clone it to your local machine with the following command:</span></span>

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. <span data-ttu-id="ea6b8-119">在 Visual Studio 中打开 **todo.csproj**。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-119">Open **todo.csproj** in Visual Studio.</span></span>

3. <span data-ttu-id="ea6b8-120">打开 Web 项目中的 **appsettings.json**。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-120">Open **appsettings.json** in the web project.</span></span>  <span data-ttu-id="ea6b8-121">查找以下行：</span><span class="sxs-lookup"><span data-stu-id="ea6b8-121">Look for the following lines:</span></span>

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    <span data-ttu-id="ea6b8-122">将 **AUTHKEYVALUE** 和 **ENDPOINTVALUE** 替换为前面记下的值。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-122">Replace **AUTHKEYVALUE** and **ENDPOINTVALUE** with the values you noted earlier.</span></span>

4. <span data-ttu-id="ea6b8-123">按 **F5** 还原项目的 NuGet 包，生成项目，并在本地运行项目。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-123">Press **F5** to restore the project's NuGet packages, build the project, and run it locally.</span></span>

<span data-ttu-id="ea6b8-124">Web 应用程序应在浏览器中本地运行。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-124">The web application should run locally in your browser.</span></span>  <span data-ttu-id="ea6b8-125">可以通过单击“新建”将新项添加到待办事项列表。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-125">You can add new items to the to-do list by clicking **Create New**.</span></span>  <span data-ttu-id="ea6b8-126">可以看到，在应用程序中输入的数据正存储到 Azure Cosmos DB 帐户中。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-126">Note the data you enter in the application is being stored in your Azure Cosmos DB account.</span></span>  <span data-ttu-id="ea6b8-127">可以通过从左侧菜单中选择 Azure Cosmos DB，选择帐户，然后选择“数据资源管理器”，在 [Azure 门户](https://portal.azure.com)中查看数据。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-127">You can view your data in the [Azure portal](https://portal.azure.com) by selecting Azure Cosmos DB from the left menu, selecting your account, and then selecting **Data Explorer**.</span></span>

## <a name="deploying-the-application-as-an-azure-web-app"></a><span data-ttu-id="ea6b8-128">将应用程序部署为 Azure Web 应用</span><span class="sxs-lookup"><span data-stu-id="ea6b8-128">Deploying the application as an Azure Web App</span></span>

<span data-ttu-id="ea6b8-129">现在已成功生成一个使用 Azure Cosmos DB 等 Azure 服务的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-129">You've successfully built an application that uses Azure services like Azure Cosmos DB.</span></span>  <span data-ttu-id="ea6b8-130">接下来，将 Web 应用程序部署到云中。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-130">Next, we'll deploy our web application to the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea6b8-131">请务必使用与 Azure 订阅关联的同一帐户登录到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-131">Be sure you're signed into Visual Studio with the same account your Azure subscription is associated with.</span></span>

1. <span data-ttu-id="ea6b8-132">在 Visual Studio 的解决方案资源管理器中，右键单击项目名称并选择“发布...”。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-132">In Visual Studio Solution Explorer, right-click on the project name and select **Publish...**</span></span>

2. <span data-ttu-id="ea6b8-133">在“发布”对话框下，依次选择“Microsoft Azure 应用服务”和“新建”，并单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-133">Using the Publish dialog, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**</span></span>

3. <span data-ttu-id="ea6b8-134">按如下所示完成“创建应用服务”对话框中的操作：</span><span class="sxs-lookup"><span data-stu-id="ea6b8-134">Complete the Create App Service dialog as follows:</span></span>

    * <span data-ttu-id="ea6b8-135">输入唯一的 **Web 应用名称**。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-135">Enter a unique **Web App Name**.</span></span>  <span data-ttu-id="ea6b8-136">此名称会包含在应用的 URL 中。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-136">This will be part of the URL for your app.</span></span>
    * <span data-ttu-id="ea6b8-137">选择要部署到的 Azure **订阅**。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-137">Select the Azure **Subscription** you're deploying to.</span></span>  <span data-ttu-id="ea6b8-138">使用前面登录到 Cloud Shell 时所用的同一订阅。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-138">Use same subscription with which you were logged into Cloud Shell earlier.</span></span>
    * <span data-ttu-id="ea6b8-139">选择“DotNetAzureTutorial”作为 Web 应用程序的**资源组**。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-139">Select *DotNetAzureTutorial* for the **Resource Group** for your web application.</span></span>
    * <span data-ttu-id="ea6b8-140">选择或创建一个**应用服务计划**用于确定应用程序的定价。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-140">Select or create an **App Service Plan** to determine the pricing your your application.</span></span>  <span data-ttu-id="ea6b8-141">此处提供了[有关应用服务计划的详细信息](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-141">Here's [more information about App Service Plans](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

4. <span data-ttu-id="ea6b8-142">单击“创建”部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-142">Click **Create** to deploy the application.</span></span>  <span data-ttu-id="ea6b8-143">部署完成后，会打开一个浏览器，其中包含部署的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-143">When deployment is complete, a browser will open with your deployed application.</span></span>

![完成的应用](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="ea6b8-145">清理</span><span class="sxs-lookup"><span data-stu-id="ea6b8-145">Clean up</span></span>

<span data-ttu-id="ea6b8-146">测试完应用并检查代码和资源后，可以通过在 Cloud Shell 中删除资源组来删除 Web 应用和 Azure Cosmos DB 帐户。</span><span class="sxs-lookup"><span data-stu-id="ea6b8-146">When you're done testing the app and inspecting the code and resources, you can delete the Web App and Azure Cosmos DB account by deleting the resource group in the Cloud Shell.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="ea6b8-147">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ea6b8-147">Next steps</span></span>

* [<span data-ttu-id="ea6b8-148">在 ASP.NET Web 应用程序中使用 Azure Active Directory 进行身份验证</span><span class="sxs-lookup"><span data-stu-id="ea6b8-148">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="ea6b8-149">使用 Azure SQL 数据库生成 Azure Web 应用</span><span class="sxs-lookup"><span data-stu-id="ea6b8-149">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="ea6b8-150">结合 Azure 存储尝试运行 .NET 示例应用程序</span><span class="sxs-lookup"><span data-stu-id="ea6b8-150">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


