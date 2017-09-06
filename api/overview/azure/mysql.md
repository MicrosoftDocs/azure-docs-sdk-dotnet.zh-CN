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
# <a name="azure-database-for-mysql-libraries-for-net"></a><span data-ttu-id="bb323-104">用于 .NET 的 Azure Database for MySQL 库</span><span class="sxs-lookup"><span data-stu-id="bb323-104">Azure Database for MySQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="bb323-105">概述</span><span class="sxs-lookup"><span data-stu-id="bb323-105">Overview</span></span>

<span data-ttu-id="bb323-106">使用 [Azure Database for MySQL](/azure/mysql/overview) 中存储的数据和资源。</span><span class="sxs-lookup"><span data-stu-id="bb323-106">Work with data and resources stored in [Azure Database for MySQL](/azure/mysql/overview).</span></span>

## <a name="client-apis"></a><span data-ttu-id="bb323-107">客户端 API</span><span class="sxs-lookup"><span data-stu-id="bb323-107">Client APIs</span></span>

<span data-ttu-id="bb323-108">建议用于访问 Azure Database for MySQL 的客户端库是 MySQL 的 [Connector/Net](https://dev.mysql.com/doc/connector-net/en)。</span><span class="sxs-lookup"><span data-stu-id="bb323-108">The recommended client library for accessing Azure Database for MySQL is MySQL's [Connector/Net](https://dev.mysql.com/doc/connector-net/en).</span></span> <span data-ttu-id="bb323-109">使用包连接到数据库并直接执行 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="bb323-109">Use the package to connect to the database and execute SQL statements directly.</span></span> 

<span data-ttu-id="bb323-110">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/MySql.Data)。</span><span class="sxs-lookup"><span data-stu-id="bb323-110">Install the [NuGet package](https://www.nuget.org/packages/MySql.Data) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bb323-111">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="bb323-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a><span data-ttu-id="bb323-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="bb323-112">.NET Core CLI</span></span>

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a><span data-ttu-id="bb323-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="bb323-113">Code Example</span></span>

<span data-ttu-id="bb323-114">连接到 MySQL 数据库并执行查询：</span><span class="sxs-lookup"><span data-stu-id="bb323-114">Connect to a MySQL database and execute a query:</span></span>

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

## <a name="samples"></a><span data-ttu-id="bb323-115">示例</span><span class="sxs-lookup"><span data-stu-id="bb323-115">Samples</span></span>

- [<span data-ttu-id="bb323-116">ADO.NET 代码示例</span><span class="sxs-lookup"><span data-stu-id="bb323-116">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="bb323-117">使用 Azure CLI 设计 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="bb323-117">Design a MySQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
