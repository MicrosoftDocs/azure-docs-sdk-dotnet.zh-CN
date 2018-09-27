---
title: 用于 .NET 的 Azure Database for PostgreSQL 库
description: 用于 Azure Database for PostgreSQL 的 .NET 客户端库的参考文档
ms.date: 10/19/2017
ms.topic: reference
ms.service: postgresql
ms.openlocfilehash: 4137e024eadba93c9cb3e94c1e7478d0816f8370
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190740"
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="b1a09-103">用于 .NET 的 Azure Database for PostgreSQL 库</span><span class="sxs-lookup"><span data-stu-id="b1a09-103">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="b1a09-104">概述</span><span class="sxs-lookup"><span data-stu-id="b1a09-104">Overview</span></span>

<span data-ttu-id="b1a09-105">使用 [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/) 中存储的数据和资源。</span><span class="sxs-lookup"><span data-stu-id="b1a09-105">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="b1a09-106">客户端 API</span><span class="sxs-lookup"><span data-stu-id="b1a09-106">Client API</span></span>

<span data-ttu-id="b1a09-107">建议用于访问 Azure Database for PostgreSQL 的客户端库是开源 [Npgsql ADO.NET 数据提供程序](http://www.npgsql.org/)。</span><span class="sxs-lookup"><span data-stu-id="b1a09-107">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="b1a09-108">使用 ADO.NET 提供程序可以借助 Npgsql 的 [Entity Framework 6](http://www.npgsql.org/ef6/index.html) 或 [Entity Framework Core](http://www.npgsql.org/efcore/index.html) 提供程序连接到数据库，并直接或通过 Entity Framework 执行 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="b1a09-108">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="b1a09-109">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Npgsql)。</span><span class="sxs-lookup"><span data-stu-id="b1a09-109">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b1a09-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="b1a09-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="b1a09-111">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="b1a09-111">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="b1a09-112">代码示例</span><span class="sxs-lookup"><span data-stu-id="b1a09-112">Code Example</span></span>

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

### <a name="samples"></a><span data-ttu-id="b1a09-113">示例</span><span class="sxs-lookup"><span data-stu-id="b1a09-113">Samples</span></span>

- [<span data-ttu-id="b1a09-114">ADO.NET 代码示例</span><span class="sxs-lookup"><span data-stu-id="b1a09-114">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="b1a09-115">使用 Azure CLI 设计 PostgreSQL 数据库</span><span class="sxs-lookup"><span data-stu-id="b1a09-115">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
