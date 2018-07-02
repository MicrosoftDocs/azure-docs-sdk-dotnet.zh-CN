---
title: 用于 .NET 的 Azure Data Lake Store 库
description: 用于 .NET 的 Azure Data Lake Store 库参考
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f1b014c4835784ed8ecfa1e3b4bfd62a6ebf9562
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065627"
---
# <a name="azure-data-lake-store-libraries-for-net"></a>用于 .NET 的 Azure Data Lake Store 库

## <a name="overview"></a>概述

Azure Data Lake Store 是一个企业范围的超大规模存储库，适用于大数据分析工作负载。 使用 Azure Data Lake 可以在单个位置捕获任何大小、类型和引入速度的数据进行操作和探索分析。

有关详细信息，请参阅 [Azure Data Lake Store 概述](/azure/data-lake-store/data-lake-store-overview)。

## <a name="client-library"></a>客户端库

使用客户端库可在 Data Lake Store 上执行文件系统操作，如在 Data Lake Store 帐户中创建文件夹，上传文件，以及下载文件。  有关将 Data Lake Store 与 .NET 一起使用的完整教程，请参阅[使用 .NET SDK 在 Azure Data Lake Store 上执行的文件系统操作](/azure/data-lake-store/data-lake-store-data-operations-net-sdk)。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a>身份验证

* 有关应用程序的最终用户身份验证，请参阅[使用 .NET SDK 通过 Data Lake Store 进行最终用户身份验证](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk)。
* 有关应用程序的服务到服务身份验证，请参阅[使用 .NET SDK 通过 Data Lake Store 进行服务到服务身份验证](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk)。

### <a name="code-example"></a>代码示例

以下代码片段创建了 Data Lake Store filesystem 客户端对象，用于向服务发出请求。

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/datalakestore/client)


## <a name="management-library"></a>管理库

使用管理库可连接和管理大数据存储库。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a>示例

* [Azure Data Lake .NET 客户端示例](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
