---
title: "用于 .NET 的 Azure 数据工厂库"
description: "用于 .NET 的 Azure 数据工厂库参考"
keywords: "Azure, .NET, SDK, API, 数据工厂"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: e0b85d7d3988febca6dce7f4038825d74e4b8d2e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-factory-libraries-for-net"></a>用于 .NET 的 Azure 数据工厂库

## <a name="overview"></a>概述

Azure 数据工厂是基于云的数据集成服务。 使用它可在云中创建数据驱动的工作流，用于协调和自动化数据移动与数据转换。

有关详细信息，请参阅 [Azure 数据工厂简介](/azure/data-factory/data-factory-introduction)。

## <a name="management-library"></a>管理库

使用管理库可创建和计划数据驱动的工作流（管道）。

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
