---
title: 用于 .NET 的 Azure 数据工厂库
description: 用于 .NET 的 Azure 数据工厂库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: data-factory
ms.openlocfilehash: 9a779f223cd0e158e99afcf1ee011d121f2fe838
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190320"
---
# <a name="azure-data-factory-libraries-for-net"></a>用于 .NET 的 Azure 数据工厂库

## <a name="overview"></a>概述

Azure 数据工厂是基于云的数据集成服务。 使用它可在云中创建数据驱动的工作流，用于协调和自动化数据移动与数据转换。

有关详细信息，请参阅 [Azure 数据工厂简介](/azure/data-factory/data-factory-introduction)。

## <a name="management-library---data-factory-v2-preview"></a>管理库 - 数据工厂 V2（预览版）

使用数据工厂 V2（预览版）中的管理库可创建和计划数据驱动的工作流（管道）。  有关详细信息，请参阅[使用 .NET SDK 创建数据工厂和管道](/azure/data-factory/quickstart-create-data-factory-dot-net)。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a>代码示例

以下示例使用管理库来创建数据工厂。

```csharp
/*
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.Azure.Management.DataFactory;
using Microsoft.Azure.Management.DataFactory.Models;
*/

DataFactoryManagementClient client = new DataFactoryManagementClient(tokenCredentials) { SubscriptionId = subscriptionId };
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a>管理库 - 数据工厂 V1

使用数据工厂版本 1 中的管理库可创建和计划数据驱动的工作流（管道）。  有关详细信息，请查看[数据工厂版本 1](/azure/data-factory/v1/data-factory-introduction) 的文档。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a>代码示例

以下示例使用管理库来创建数据工厂。

```csharp
DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
client.DataFactories.CreateOrUpdate(resourceGroupName,
    new DataFactoryCreateOrUpdateParameters()
    {
        DataFactory = new DataFactory()
        {
            Name = dataFactoryName,
            Location = "westus",
            Properties = new DataFactoryProperties()
        }
    }
);
```

> [!div class="nextstepaction"]
> [了解管理 API](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a>示例

* 使用数据工厂帮助提供见解的 [MyDriving - Azure IOT 和移动应用程序示例](https://azure.microsoft.com/resources/samples/mydriving/)。

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
