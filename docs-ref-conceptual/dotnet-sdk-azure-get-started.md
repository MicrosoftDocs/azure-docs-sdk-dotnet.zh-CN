---
title: Azure .NET API 入门
description: 结合自己的 Azure 订阅开始了解用于 .NET 的 Azure 库的基本用法。
keywords: Azure, .NET, SDK, API, 身份验证, 入门
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a3733898f948dbb2ec07da20aa61724e07f23e73
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2018
---
# <a name="get-started-with-the-azure-net-apis"></a>Azure .NET API 入门

本教程演示多个[用于 .NET 的 Azure API](/dotnet/api/overview/azure/) 的用法。  内容包括设置身份验证、创建和使用 Azure 存储帐户、创建和使用 Azure SQL 数据库、部署一些虚拟机，然后从 GitHub 部署一个 Azure 应用服务 Web 应用。

## <a name="prerequisites"></a>先决条件

- 一个 Azure 帐户。 如果没有帐户，可[获取一个免费试用帐户](https://azure.microsoft.com/free/)
- [Azure PowerShell](/powershell/azure/install-azurerm-ps)

## <a name="set-up-authentication"></a>设置身份验证

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a>创建新项目 

创建新的控制台应用程序项目。  为此，请在 Visual Studio 中依次单击“文件”、“新建”、“项目...”。在 Visual C# 模板下选择“控制台应用(.NET Core)”，为项目命名，并单击“确定”。

![“新建项目”对话框](media/dotnet-sdk-azure-get-started/new-project.png)

创建新的控制台应用后，依次单击“工具”、“NuGet 包管理器”、“包管理器控制台”打开包管理器控制台。  在控制台中，执行以下三个命令来获取所需的包：

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a>指令

编辑应用程序的 `Program.cs` 文件。  将顶部的 `using` 指令替换为以下内容：

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

## <a name="create-a-virtual-machine"></a>创建虚拟机

此示例部署虚拟机。 

将 `Main` 方法替换为以下内容。  请务必为虚拟机提供实际的 `username` 和 `password`。

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string username = "MY_USERNAME";
    string password = "MY_PASSWORD";
    string rgName = "sampleResourceGroup";
    string windowsVmName = "sampleWindowsVM";
    string publicIpDnsLabel = "samplePublicIP";

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

按 **F5** 运行示例。

几分钟后，程序将会完成，并提示按 Enter 键。 按 Enter 键后，请使用 PowerShell 验证订阅中的虚拟机：

```powershell
Get-AzureRmVm -ResourceGroupName sampleResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>从 GitHub 存储库部署 Web 应用

现在请修改代码，以便从现有的 GitHub 存储库创建并部署新的 Web 应用。 将 `Main`方法替换为以下代码：

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

如前所述按 **F5** 运行代码。  通过打开浏览器并导航到控制台中显示的 URL 来验证部署。

## <a name="connect-to-a-sql-database"></a>连接到 SQL 数据库

此示例创建新的 Azure SQL 数据库并执行一些 SQL 操作。

将 `Main` 方法替换为以下内容，并确保为 `dbPassword` 分配强密码：

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
如前所述按 **F5** 运行代码。  控制台输出应会验证服务器是否已创建并按预期工作，但如果需要，你可以使用 SQL Server Management Studio 等工具直接连接到该服务器。

## <a name="write-a-blob-into-a-new-storage-account"></a>将 Blob 写入新存储帐户

此示例创建存储帐户并上传 Blob。  

将 `Main` 方法替换为以下内容。

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

按 **F5** 运行示例。

几分钟后，程序将会完成。 通过浏览到控制台中显示的 URL 来验证是否已上传 Blob。  文本“Hello, Azure!”应会显示 在浏览器中。

## <a name="clean-up"></a>清理

> [!IMPORTANT]
> 如果不清理本教程创建的资源，这些资源会继续产生费用。  请务必执行此步骤。

在 PowerShell 中输入以下命令，删除创建的所有资源：

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName sampleResourceGroup
```
## <a name="explore-more-samples"></a>学习更多示例

若要详细了解如何使用用于 .NET 的 Azure 库来管理资源和自动执行任务，请参阅针对[虚拟机](dotnet-sdk-azure-virtual-machine-samples.md)、[Web 应用](dotnet-sdk-azure-web-apps-samples.md)和 [SQL 数据库](dotnet-sdk-azure-sql-database-samples.md)的示例代码。

## <a name="reference"></a>引用

我们为所有包提供了[参考](http://docs.microsoft.com/dotnet/api)文档。

[!include[Contribute and community](includes/contribute.md)]
