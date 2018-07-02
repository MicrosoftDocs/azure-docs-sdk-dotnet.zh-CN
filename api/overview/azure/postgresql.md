---
title: 用于 .NET 的 Azure Database for PostgreSQL 库
description: 用于 Azure Database for PostgreSQL 的 .NET 客户端库的参考文档
keywords: Azure, .NET ODBC, SDK, API, SQL, ADO.NET, 数据库, PostGres, PostgreSQL
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: postgresql
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 40ef1d5ffd41b45523fbeb2c29095fd423b749bd
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065407"
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="e7481-104">用于 .NET 的 Azure Database for PostgreSQL 库</span><span class="sxs-lookup"><span data-stu-id="e7481-104">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e7481-105">概述</span><span class="sxs-lookup"><span data-stu-id="e7481-105">Overview</span></span>

<span data-ttu-id="e7481-106">使用 [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/) 中存储的数据和资源。</span><span class="sxs-lookup"><span data-stu-id="e7481-106">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="e7481-107">客户端 API</span><span class="sxs-lookup"><span data-stu-id="e7481-107">Client API</span></span>

<span data-ttu-id="e7481-108">建议用于访问 Azure Database for PostgreSQL 的客户端库是开源 [Npgsql ADO.NET 数据提供程序](http://www.npgsql.org/)。</span><span class="sxs-lookup"><span data-stu-id="e7481-108">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="e7481-109">使用 ADO.NET 提供程序可以借助 Npgsql 的 [Entity Framework 6](http://www.npgsql.org/ef6/index.html) 或 [Entity Framework Core](http://www.npgsql.org/efcore/index.html) 提供程序连接到数据库，并直接或通过 Entity Framework 执行 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="e7481-109">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="e7481-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Npgsql)。</span><span class="sxs-lookup"><span data-stu-id="e7481-110">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e7481-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="e7481-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="e7481-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="e7481-112">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="e7481-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="e7481-113">Code Example</span></span>

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

### <a name="samples"></a><span data-ttu-id="e7481-114">示例</span><span class="sxs-lookup"><span data-stu-id="e7481-114">Samples</span></span>

- [<span data-ttu-id="e7481-115">ADO.NET 代码示例</span><span class="sxs-lookup"><span data-stu-id="e7481-115">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="e7481-116">使用 Azure CLI 设计 PostgreSQL 数据库</span><span class="sxs-lookup"><span data-stu-id="e7481-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
