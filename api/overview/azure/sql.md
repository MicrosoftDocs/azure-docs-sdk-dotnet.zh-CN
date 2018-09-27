---
title: 用于 .NET 的 Azure SQL 数据库 API
description: 用于 .NET 的 Azure SQL 数据库库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: sql-database
ms.openlocfilehash: e4c1620ddf488952c6720b9bedf2521c6512b9a3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190630"
---
# <a name="azure-sql-database-apis-for-net"></a><span data-ttu-id="8cd36-103">用于 .NET 的 Azure SQL 数据库 API</span><span class="sxs-lookup"><span data-stu-id="8cd36-103">Azure SQL Database APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="8cd36-104">概述</span><span class="sxs-lookup"><span data-stu-id="8cd36-104">Overview</span></span>

<span data-ttu-id="8cd36-105">[Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)是使用 Microsoft SQL Server 引擎的数据库服务，支持关系型数据、表数据、JSON 数据、空间数据和 XML 数据。</span><span class="sxs-lookup"><span data-stu-id="8cd36-105">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) is a database service using the Microsoft SQL Server engine that supports relational, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="8cd36-106">若要详细了解如何在 .NET 中使用 SQL 数据库，请参阅[使用 .NET 和 Visual Studio 来连接和查询 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="8cd36-106">To learn more about the using SQL Database with .NET, see [Use .NET with Visual Studio to connect and query an Azure SQL database](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span></span>

## <a name="client-library"></a><span data-ttu-id="8cd36-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="8cd36-107">Client library</span></span>

<span data-ttu-id="8cd36-108">使用 .NET SQL 客户端库可以连接到数据库并在其中进行身份验证，以及执行即席 T-SQL 语句和存储过程。</span><span class="sxs-lookup"><span data-stu-id="8cd36-108">Use the .NET SQL client library to connect and authenticate with your database and execute ad-hoc T-SQL statements and stored procedures.</span></span>

<span data-ttu-id="8cd36-109">直接从 Visual Studio [包管理器控制台](https://docs.microsoft.com/nuget/tools/package-manager-console)或使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package) 安装 [NuGet 包]( https://www.nuget.org/packages/System.Data.SqlClient)。</span><span class="sxs-lookup"><span data-stu-id="8cd36-109">Install the [NuGet package]( https://www.nuget.org/packages/System.Data.SqlClient) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8cd36-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="8cd36-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a><span data-ttu-id="8cd36-111">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="8cd36-111">.NET Core CLI</span></span>

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a><span data-ttu-id="8cd36-112">代码示例</span><span class="sxs-lookup"><span data-stu-id="8cd36-112">Code Example</span></span>

<span data-ttu-id="8cd36-113">此示例连接到数据库并从表中读取行。</span><span class="sxs-lookup"><span data-stu-id="8cd36-113">This example connects to a database and reads rows from a table.</span></span>

```csharp
/* Include this 'using' directive...
using System.Data.SqlClient;
*/

// Always store connection strings securely. 
string connectionString = "Server=tcp:[serverName].database.windows.net;" 
    + "Database=myDataBase;User ID=[loginname]@[serverName];Password=myPassword;"
    + "Trusted_Connection=False;Encrypt=True;";

// Best practice is to scope the SqlConnection to a "using" block
using (SqlConnection conn = new SqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    SqlCommand selectCommand = new SqlCommand("SELECT * FROM MyTable", conn);
    SqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8cd36-114">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="8cd36-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a><span data-ttu-id="8cd36-115">管理库</span><span class="sxs-lookup"><span data-stu-id="8cd36-115">Management library</span></span>

<span data-ttu-id="8cd36-116">使用 Azure SQL 数据库管理库可创建、管理和缩放 Azure SQL 数据库服务器实例。</span><span class="sxs-lookup"><span data-stu-id="8cd36-116">Use the Azure SQL Database management library to create, manage, and scale Azure SQL Database server instances.</span></span>

<span data-ttu-id="8cd36-117">直接从 Visual Studio [包管理器控制台](https://docs.microsoft.com/nuget/tools/package-manager-console)或使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package) 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/)。</span><span class="sxs-lookup"><span data-stu-id="8cd36-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8cd36-118">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="8cd36-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a><span data-ttu-id="8cd36-119">.NET Core 命令行</span><span class="sxs-lookup"><span data-stu-id="8cd36-119">.NET Core command line</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a><span data-ttu-id="8cd36-120">代码示例</span><span class="sxs-lookup"><span data-stu-id="8cd36-120">Code Example</span></span>

<span data-ttu-id="8cd36-121">此示例创建新的 SQL 数据库服务器实例，然后在该实例上创建新数据库。</span><span class="sxs-lookup"><span data-stu-id="8cd36-121">This example creates a new SQL Database server instance and then creates a new database on that instance.</span></span>

```csharp
/* Include these 'using' directives...
using Microsoft.Azure.Management.Sql.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

string startAddress = "0.0.0.0";
string endAddress = "255.255.255.255";

// Create the SQL server instance
ISqlServer sqlServer = azure.SqlServers.Define("UniqueServerName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("ResourceGroupName")
    .WithAdministratorLogin("UserName")
    .WithAdministratorPassword("Password")
    .WithNewFirewallRule(startAddress, endAddress)
    .Create();

// Create the database
ISqlDatabase sqlDb = sqlServer.Databases.Define("DatabaseName").Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8cd36-122">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="8cd36-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a><span data-ttu-id="8cd36-123">示例</span><span class="sxs-lookup"><span data-stu-id="8cd36-123">Samples</span></span>

- [<span data-ttu-id="8cd36-124">ADO.NET 代码示例</span><span class="sxs-lookup"><span data-stu-id="8cd36-124">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="8cd36-125">用于 .NET 的 Azure 管理库的 SQL 数据库示例</span><span class="sxs-lookup"><span data-stu-id="8cd36-125">Azure management libraries for .NET samples for SQL Database</span></span>](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

<span data-ttu-id="8cd36-126">查看 Azure SQL 数据库示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database)。</span><span class="sxs-lookup"><span data-stu-id="8cd36-126">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database) of Azure SQL Database samples.</span></span>

