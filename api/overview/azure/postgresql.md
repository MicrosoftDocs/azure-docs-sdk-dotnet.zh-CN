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
# <a name="azure-database-for-postgresql-libraries-for-net"></a>用于 .NET 的 Azure Database for PostgreSQL 库

## <a name="overview"></a>概述

使用 [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/) 中存储的数据和资源。

## <a name="client-api"></a>客户端 API

建议用于访问 Azure Database for PostgreSQL 的客户端库是开源 [Npgsql ADO.NET 数据提供程序](http://www.npgsql.org/)。 使用 ADO.NET 提供程序可以借助 Npgsql 的 [Entity Framework 6](http://www.npgsql.org/ef6/index.html) 或 [Entity Framework Core](http://www.npgsql.org/efcore/index.html) 提供程序连接到数据库，并直接或通过 Entity Framework 执行 SQL 语句。

直接从 Visual Studio [包管理器控制台][PackageManager] 或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Npgsql)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a>代码示例

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

### <a name="samples"></a>示例

- [ADO.NET 代码示例](/dotnet/framework/data/adonet/ado-net-code-examples)
- [使用 Azure CLI 设计 PostgreSQL 数据库](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) [PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console [DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package