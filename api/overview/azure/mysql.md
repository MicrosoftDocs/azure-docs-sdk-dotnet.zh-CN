---
title: "用于 .NET 的 Azure Database for MySQL 库"
description: "用于 Azure Database for MySQL 的 .NET 客户端库的参考文档"
keywords: "Azure, .NET, SDK, API, SQL, 数据库, MySQL"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: mysql
ms.openlocfilehash: 1bc373d63b0172fd554277a6ef30fa09772a395b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
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
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
