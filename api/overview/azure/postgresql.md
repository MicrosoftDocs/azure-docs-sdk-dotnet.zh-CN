---
title: "用于 .NET 的 Azure Database for PostgreSQL 库"
description: "用于 Azure Database for PostgreSQL 的 .NET 客户端库的参考文档"
keywords: "Azure, .NET ODBC, SDK, API, SQL, ADO.NET, 数据库, PostGres, PostgreSQL"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: postgresql
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e3153a35845a2d7660aded64e5dbc3787c62afb6
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2017
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="ce777-104">用于 .NET 的 Azure Database for PostgreSQL 库</span><span class="sxs-lookup"><span data-stu-id="ce777-104">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="ce777-105">概述</span><span class="sxs-lookup"><span data-stu-id="ce777-105">Overview</span></span>

<span data-ttu-id="ce777-106">使用 [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/) 中存储的数据和资源。</span><span class="sxs-lookup"><span data-stu-id="ce777-106">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="ce777-107">客户端 API</span><span class="sxs-lookup"><span data-stu-id="ce777-107">Client API</span></span>

<span data-ttu-id="ce777-108">建议用于访问 Azure Database for PostgreSQL 的客户端库是开源 [Npgsql ADO.NET 数据提供程序](http://www.npgsql.org/)。</span><span class="sxs-lookup"><span data-stu-id="ce777-108">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="ce777-109">使用 ADO.NET 提供程序可以借助 Npgsql 的 [Entity Framework 6](http://www.npgsql.org/ef6/index.html) 或 [Entity Framework Core](http://www.npgsql.org/efcore/index.html) 提供程序连接到数据库，并直接或通过 Entity Framework 执行 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="ce777-109">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="ce777-110">直接从 Visual Studio [包管理器控制台][PackageManager] 或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Npgsql)。</span><span class="sxs-lookup"><span data-stu-id="ce777-110">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ce777-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="ce777-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="ce777-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="ce777-112">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="ce777-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="ce777-113">Code Example</span></span>

```csharp
/* Include this 'using' directive...
using Npgsql;
*/

// Always store connection strings securely. 
string connectionString = "Server=[servername].postgres.database.azure.com; " +
    "Port=5432; Database=myDataBase; User Id=[userid]@[servername]; Password=password;";

// Best practice is to scope the NpgsqlConnection to a "using" block
using (NpgsqlConnection conn = new NpgsqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    NpgsqlCommand selectCommand = new NpgsqlCommand("SELECT * FROM MyTable", conn);
    NpgsqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

### <a name="samples"></a><span data-ttu-id="ce777-114">示例</span><span class="sxs-lookup"><span data-stu-id="ce777-114">Samples</span></span>

- [<span data-ttu-id="ce777-115">ADO.NET 代码示例</span><span class="sxs-lookup"><span data-stu-id="ce777-115">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- <span data-ttu-id="ce777-116">[使用 Azure CLI 设计 PostgreSQL 数据库](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) [PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console [DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package</span><span class="sxs-lookup"><span data-stu-id="ce777-116">[Design a PostgreSQL database using the Azure CLI](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) [PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console [DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package</span></span>