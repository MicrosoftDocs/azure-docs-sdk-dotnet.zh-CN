---
title: Azure .NET 和 .NET Core API 入门
description: 结合自己的 Azure 订阅开始了解用于 .NET 和 .NET Core 的 Azure 库的基本用法。
keywords: Azure, .NET, .NET Core, ASP.NET, ASP.NET Core SDK, API, 身份验证, 入门
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 08/22/2018
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: ad894e47704fcccc83f7d02acb8e418b167993f9
ms.sourcegitcommit: b2a53a3aea9de6720bd975fb7fe4e722e9d182a3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703050"
---
# <a name="get-started-with-the-azure-net-and-net-core-apis"></a><span data-ttu-id="3fa5d-104">Azure .NET 和 .NET Core API 入门</span><span class="sxs-lookup"><span data-stu-id="3fa5d-104">Get started with the Azure .NET and .NET Core APIs</span></span>

<span data-ttu-id="3fa5d-105">本教程演示多个[用于 .NET 的 Azure API](/dotnet/api/overview/azure/) 的用法。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-105">This tutorial demonstrates the usage of several [Azure APIs for .NET](/dotnet/api/overview/azure/).</span></span>  <span data-ttu-id="3fa5d-106">内容包括设置身份验证、创建和使用 Azure 存储帐户、创建和使用 Azure SQL 数据库、部署一些虚拟机，然后从 GitHub 部署一个 Azure 应用服务 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fa5d-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="3fa5d-107">Prerequisites</span></span>

- <span data-ttu-id="3fa5d-108">一个 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-108">An Azure account.</span></span> <span data-ttu-id="3fa5d-109">如果没有帐户，可[获取一个免费试用帐户](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="3fa5d-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="3fa5d-110">设置身份验证</span><span class="sxs-lookup"><span data-stu-id="3fa5d-110">Set up authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a><span data-ttu-id="3fa5d-111">创建新项目</span><span class="sxs-lookup"><span data-stu-id="3fa5d-111">Create a new project</span></span> 

<span data-ttu-id="3fa5d-112">创建新的控制台应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-112">Create a new console application project.</span></span>  <span data-ttu-id="3fa5d-113">为此，请在 Visual Studio 中依次单击“文件”、“新建”、“项目...”。在 Visual C# 模板下选择“控制台应用(.NET Core)”，为项目命名，并单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-113">In Visual Studio, do this by clicking **File**, **New**, and then clicking **Project...**.  Under the Visual C# templates, select **Console App (.NET Core)**, name your project, and then click **OK**.</span></span>

![“新建项目”对话框](media/dotnet-sdk-azure-get-started/new-project.png)

<span data-ttu-id="3fa5d-115">创建新的控制台应用后，依次单击“工具”、“NuGet 包管理器”、“包管理器控制台”打开包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-115">When the new console app is created, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>  <span data-ttu-id="3fa5d-116">在控制台中，执行以下三个命令来获取所需的包：</span><span class="sxs-lookup"><span data-stu-id="3fa5d-116">In the console, get the packages you'll need by executing the following three commands:</span></span>

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a><span data-ttu-id="3fa5d-117">指令</span><span class="sxs-lookup"><span data-stu-id="3fa5d-117">Directives</span></span>

<span data-ttu-id="3fa5d-118">编辑应用程序的 `Program.cs` 文件。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-118">Edit your application's `Program.cs` file.</span></span>  <span data-ttu-id="3fa5d-119">将顶部的 `using` 指令替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="3fa5d-119">Replace the `using` directives at the top with the following:</span></span>

```csharp
using System;
using System.Linq;
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Data.SqlClient;
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="3fa5d-120">创建虚拟机</span><span class="sxs-lookup"><span data-stu-id="3fa5d-120">Create a virtual machine</span></span>

<span data-ttu-id="3fa5d-121">此示例部署虚拟机。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-121">This example deploys a virtual machine.</span></span> 

<span data-ttu-id="3fa5d-122">将 `Main` 方法替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-122">Replace the `Main` method with the following.</span></span>  <span data-ttu-id="3fa5d-123">请务必为虚拟机提供实际的 `username` 和 `password`。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-123">Be sure to provide an actual `username` and `password` for the virtual machine.</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string username = "MY_USERNAME";
    string password = "MY_PASSWORD";
    string rgName = "sampleResourceGroup";
    string windowsVmName = "sampleWindowsVM";
    string publicIpDnsLabel = "samplePublicIP" + (new Random().Next(0,100000)).ToString();

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the VM
    Console.WriteLine("Creating VM...");
    var windowsVM = azure.VirtualMachines.Define(windowsVmName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewPrimaryNetwork("10.0.0.0/28")
        .WithPrimaryPrivateIPAddressDynamic()
        .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
        .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
        .WithAdminUsername(username)
        .WithAdminPassword(password)
        .WithSize(VirtualMachineSizeTypes.StandardD2V2)
        .Create();

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="3fa5d-124">按 **F5** 运行示例。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-124">Press **F5** to run the sample.</span></span>

<span data-ttu-id="3fa5d-125">几分钟后，程序将会完成，并提示按 Enter 键。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-125">After several minutes, the program will finish, prompting you to press enter.</span></span> <span data-ttu-id="3fa5d-126">按 Enter 键后，请使用 Cloud Shell 验证订阅中的虚拟机：</span><span class="sxs-lookup"><span data-stu-id="3fa5d-126">After pressing enter, verify the virtual machine in your subscription with the Cloud Shell:</span></span>

```azurecli-interactive
az vm list
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="3fa5d-127">从 GitHub 存储库部署 Web 应用</span><span class="sxs-lookup"><span data-stu-id="3fa5d-127">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="3fa5d-128">现在请修改代码，以便从现有的 GitHub 存储库创建并部署新的 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-128">Now you'll modify your code to create a deploy a new web app from an existing GitHub repository.</span></span> <span data-ttu-id="3fa5d-129">将 `Main`方法替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3fa5d-129">Replace the `Main` method with the following code:</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string appName = SdkContext.RandomResourceName("WebApp", 20);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the web app
    Console.WriteLine("Creating Web App...");
    var app = azure.WebApps.Define(appName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewFreeAppServicePlan()
        .DefineSourceControl()
        .WithPublicGitRepository("https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
        .WithBranch("master")
        .Attach()
        .Create();
    Console.WriteLine("Your web app is live at: https://{0}", app.HostNames.First());

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="3fa5d-130">如前所述按 **F5** 运行代码。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-130">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="3fa5d-131">通过打开浏览器并导航到控制台中显示的 URL 来验证部署。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-131">Verify the deployment by opening a browser and navigating to URL displayed in the console.</span></span>

## <a name="connect-to-a-sql-database"></a><span data-ttu-id="3fa5d-132">连接到 SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="3fa5d-132">Connect to a SQL database</span></span>

<span data-ttu-id="3fa5d-133">此示例创建新的 Azure SQL 数据库并执行一些 SQL 操作。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-133">This example creates a new Azure SQL Database and performs a few SQL operations.</span></span>

<span data-ttu-id="3fa5d-134">将 `Main` 方法替换为以下内容，并确保为 `dbPassword` 分配强密码：</span><span class="sxs-lookup"><span data-stu-id="3fa5d-134">Replace the `Main` method with the following, making sure to assign a strong password for `dbPassword`:</span></span>

```csharp
 static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string adminUser = SdkContext.RandomResourceName("db", 8);
    string sqlServerName = SdkContext.RandomResourceName("sql", 10);
    string sqlDbName = SdkContext.RandomResourceName("dbname", 8);
    string dbPassword = "YOUR_PASSWORD_HERE";

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the SQL server and database
    Console.WriteLine("Creating server...");
    var sqlServer = azure.SqlServers.Define(sqlServerName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithAdministratorLogin(adminUser)
        .WithAdministratorPassword(dbPassword)
        .WithNewFirewallRule("0.0.0.0", "255.255.255.255")
        .Create();

    Console.WriteLine("Creating database...");
    var sqlDb = sqlServer.Databases.Define(sqlDbName).Create();

    // Display information for connecting later...
    Console.WriteLine("Created database {0} in server {1}.", sqlDbName, sqlServer.FullyQualifiedDomainName);
    Console.WriteLine("Your user name is {0}.", adminUser + "@" + sqlServer.Name);

    // Build the connection string
    var builder = new SqlConnectionStringBuilder();
    builder.DataSource = sqlServer.FullyQualifiedDomainName;
    builder.InitialCatalog = sqlDbName;
    builder.UserID = adminUser + "@" + sqlServer.Name; // Format user ID as "user@server"
    builder.Password = dbPassword;
    builder.Encrypt = true;
    builder.TrustServerCertificate = true;

    // connect to the database, create a table and insert an entry into it
    using (var conn = new SqlConnection(builder.ConnectionString))
    {
        conn.Open();

        Console.WriteLine("Populating database...");
        var createCommand = new SqlCommand("CREATE TABLE CLOUD (name varchar(255), code int);", conn);
        createCommand.ExecuteNonQuery();

        var insertCommand = new SqlCommand("INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);", conn);
        insertCommand.ExecuteNonQuery();

        Console.WriteLine("Reading from database...");
        var selectCommand = new SqlCommand("SELECT * FROM CLOUD", conn);
        var results = selectCommand.ExecuteReader();
        while(results.Read())
        {
            Console.WriteLine("Name: {0} Code: {1}", results[0], results[1]);
        }
    }

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="3fa5d-135">如前所述按 **F5** 运行代码。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-135">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="3fa5d-136">控制台输出应会验证服务器是否已创建并按预期工作，但如果需要，你可以使用 SQL Server Management Studio 等工具直接连接到该服务器。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-136">The console output should validate that the server was created and works as expected, but you can connect to it directly with a tool like SQL Server Management Studio if you like.</span></span>

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="3fa5d-137">将 Blob 写入新存储帐户</span><span class="sxs-lookup"><span data-stu-id="3fa5d-137">Write a blob into a new storage account</span></span>

<span data-ttu-id="3fa5d-138">此示例创建存储帐户并上传 Blob。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-138">This example creates a storage account and upload a blob.</span></span>  

<span data-ttu-id="3fa5d-139">将 `Main` 方法替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-139">Replace the `Main` method with the following.</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string storageAccountName = SdkContext.RandomResourceName("st", 10);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the storage account
    Console.WriteLine("Creating storage account...");
    var storage = azure.StorageAccounts.Define(storageAccountName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .Create();

    var storageKeys = storage.GetKeys();
    string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

    var account = CloudStorageAccount.Parse(storageConnectionString);
    var serviceClient = account.CreateCloudBlobClient();

    // Create container. Name must be lower case.
    Console.WriteLine("Creating container...");
    var container = serviceClient.GetContainerReference("helloazure");
    container.CreateIfNotExistsAsync().Wait();

    // Make the container public
    var containerPermissions = new BlobContainerPermissions()
        { PublicAccess = BlobContainerPublicAccessType.Container };
    container.SetPermissionsAsync(containerPermissions).Wait();

    // write a blob to the container
    Console.WriteLine("Uploading blob...");
    var blob = container.GetBlockBlobReference("helloazure.txt");
    blob.UploadTextAsync("Hello, Azure!").Wait();
    Console.WriteLine("Your blob is located at {0}", blob.StorageUri.PrimaryUri);

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="3fa5d-140">按 **F5** 运行示例。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-140">Press **F5** to run the sample.</span></span>

<span data-ttu-id="3fa5d-141">几分钟后，程序将会完成。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-141">After several minutes, the program finishes.</span></span> <span data-ttu-id="3fa5d-142">通过浏览到控制台中显示的 URL 来验证是否已上传 Blob。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-142">Verify the blob was uploaded by browsing to the URL displayed in the console.</span></span>  <span data-ttu-id="3fa5d-143">文本“Hello, Azure!”应会显示</span><span class="sxs-lookup"><span data-stu-id="3fa5d-143">You should see the text "Hello, Azure!"</span></span> <span data-ttu-id="3fa5d-144">在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-144">in your browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="3fa5d-145">清理</span><span class="sxs-lookup"><span data-stu-id="3fa5d-145">Clean up</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fa5d-146">如果不清理本教程创建的资源，这些资源会继续产生费用。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-146">If you don't clean up your resources from this tutorial, you will continue to be charged for them.</span></span>  <span data-ttu-id="3fa5d-147">请务必执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-147">Be sure to do this step.</span></span>

<span data-ttu-id="3fa5d-148">在 Cloud Shell 中输入以下命令来删除创建的所有资源：</span><span class="sxs-lookup"><span data-stu-id="3fa5d-148">Delete all the resources you created by entering the following in the Cloud Shell:</span></span>

```azurecli-interactive
az group delete --name sampleResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="3fa5d-149">学习更多示例</span><span class="sxs-lookup"><span data-stu-id="3fa5d-149">Explore more samples</span></span>

<span data-ttu-id="3fa5d-150">若要详细了解如何使用用于 .NET 的 Azure 库来管理资源和自动执行任务，请参阅针对[虚拟机](dotnet-sdk-azure-virtual-machine-samples.md)、[Web 应用](dotnet-sdk-azure-web-apps-samples.md)和 [SQL 数据库](dotnet-sdk-azure-sql-database-samples.md)的示例代码。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-150">To learn more about how to use the Azure libraries for .NET to manage resources and automate tasks, see our sample code for [virtual machines](dotnet-sdk-azure-virtual-machine-samples.md), [web apps](dotnet-sdk-azure-web-apps-samples.md) and [SQL database](dotnet-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference"></a><span data-ttu-id="3fa5d-151">引用</span><span class="sxs-lookup"><span data-stu-id="3fa5d-151">Reference</span></span>

<span data-ttu-id="3fa5d-152">我们为所有包提供了[参考](http://docs.microsoft.com/dotnet/api)文档。</span><span class="sxs-lookup"><span data-stu-id="3fa5d-152">A [reference](http://docs.microsoft.com/dotnet/api) is available for all packages.</span></span>

[!include[Contribute and community](includes/contribute.md)]
