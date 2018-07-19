---
title: 用于 .NET 的 Azure SQL 数据库 API
description: 用于 .NET 的 Azure SQL 数据库库参考
keywords: Azure, .NET, SDK, API, SQL, SQL 数据库
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: sql-database
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8096e66be1263bc50648ef5b9b16f3fc2bd08ac8
ms.sourcegitcommit: 512e031ead61a578ac96835c8ea01829842740bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39116673"
---
# <a name="azure-sql-database-apis-for-net"></a>用于 .NET 的 Azure SQL 数据库 API

## <a name="overview"></a>概述

[Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)是使用 Microsoft SQL Server 引擎的数据库服务，支持关系型数据、表数据、JSON 数据、空间数据和 XML 数据。 

若要详细了解如何在 .NET 中使用 SQL 数据库，请参阅[使用 .NET 和 Visual Studio 来连接和查询 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio)。

## <a name="client-library"></a>客户端库

使用 .NET SQL 客户端库可以连接到数据库并在其中进行身份验证，以及执行即席 T-SQL 语句和存储过程。

直接从 Visual Studio [包管理器控制台](https://docs.microsoft.com/nuget/tools/package-manager-console)或使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package) 安装 [NuGet 包]( https://www.nuget.org/packages/System.Data.SqlClient)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a>代码示例

此示例连接到数据库并从表中读取行。

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
> [了解客户端 API](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a>管理库

使用 Azure SQL 数据库管理库可创建、管理和缩放 Azure SQL 数据库服务器实例。

直接从 Visual Studio [包管理器控制台](https://docs.microsoft.com/nuget/tools/package-manager-console)或使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package) 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a>.NET Core 命令行

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a>代码示例

此示例创建新的 SQL 数据库服务器实例，然后在该实例上创建新数据库。

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
> [了解管理 API](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a>示例

- [ADO.NET 代码示例](/dotnet/framework/data/adonet/ado-net-code-examples)
- [用于 .NET 的 Azure 管理库的 SQL 数据库示例](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

查看 Azure SQL 数据库示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database)。

