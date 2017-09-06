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
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="6cc70-104">用于 .NET 的 Azure 数据工厂库</span><span class="sxs-lookup"><span data-stu-id="6cc70-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6cc70-105">概述</span><span class="sxs-lookup"><span data-stu-id="6cc70-105">Overview</span></span>

<span data-ttu-id="6cc70-106">Azure 数据工厂是基于云的数据集成服务。</span><span class="sxs-lookup"><span data-stu-id="6cc70-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="6cc70-107">使用它可在云中创建数据驱动的工作流，用于协调和自动化数据移动与数据转换。</span><span class="sxs-lookup"><span data-stu-id="6cc70-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="6cc70-108">有关详细信息，请参阅 [Azure 数据工厂简介](/azure/data-factory/data-factory-introduction)。</span><span class="sxs-lookup"><span data-stu-id="6cc70-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library"></a><span data-ttu-id="6cc70-109">管理库</span><span class="sxs-lookup"><span data-stu-id="6cc70-109">Management library</span></span>

<span data-ttu-id="6cc70-110">使用管理库可创建和计划数据驱动的工作流（管道）。</span><span class="sxs-lookup"><span data-stu-id="6cc70-110">Use the management library to create and schedule data-driven workflows (pipelines).</span></span>

<span data-ttu-id="6cc70-111">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)。</span><span class="sxs-lookup"><span data-stu-id="6cc70-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6cc70-112">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="6cc70-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="6cc70-113">代码示例</span><span class="sxs-lookup"><span data-stu-id="6cc70-113">Code Example</span></span>

<span data-ttu-id="6cc70-114">以下示例使用管理库来创建数据工厂。</span><span class="sxs-lookup"><span data-stu-id="6cc70-114">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="6cc70-115">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="6cc70-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="6cc70-116">示例</span><span class="sxs-lookup"><span data-stu-id="6cc70-116">Samples</span></span>

* <span data-ttu-id="6cc70-117">使用数据工厂帮助提供见解的 [MyDriving - Azure IOT 和移动应用程序示例](https://azure.microsoft.com/resources/samples/mydriving/)。</span><span class="sxs-lookup"><span data-stu-id="6cc70-117">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="6cc70-118">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="6cc70-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
