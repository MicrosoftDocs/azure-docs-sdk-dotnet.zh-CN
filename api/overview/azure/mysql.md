---
title: 用于 .NET 的 Azure Database for MySQL 库
description: 用于 Azure Database for MySQL 的 .NET 客户端库的参考文档
ms.date: 10/19/2017
ms.topic: reference
ms.service: mysql
ms.openlocfilehash: 34550c7089a2ec05164f7a16f24bfc8b18391f8a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190150"
---
# <a name="azure-database-for-mysql-libraries-for-net"></a>用于 .NET 的 Azure Database for MySQL 库

## <a name="overview"></a>概述

使用 [Azure Database for MySQL](/azure/mysql/overview) 中存储的数据和资源。

## <a name="client-apis"></a>客户端 API

建议用于访问 Azure Database for MySQL 的客户端库是 MySQL 的 [Connector/Net](https://dev.mysql.com/doc/connector-net/en)。 使用包连接到数据库并直接执行 SQL 语句。 

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/MySql.Data)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a>代码示例

连接到 MySQL 数据库并执行查询：

```csharp
/* Include this "using" directive...
using MySql.Data.MySqlClient;
*/

string connectionString = "Server=[servername].mysql.database.azure.com; " +
    "Database=myDataBase; Uid=[userid]@[servername]; Pwd=myPassword;";

// Best practice is to scope the MySqlConnection to a "using" block
using (MySqlConnection conn = new MySqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    MySqlCommand selectCommand = new MySqlCommand("SELECT * FROM MyTable", conn);
    MySqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

## <a name="samples"></a>示例

- [ADO.NET 代码示例](/dotnet/framework/data/adonet/ado-net-code-examples)
- [使用 Azure CLI 设计 MySQL 数据库](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
