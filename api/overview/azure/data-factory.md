---
title: 用于 .NET 的 Azure 数据工厂库
description: 用于 .NET 的 Azure 数据工厂库参考
keywords: Azure, .NET, SDK, API, 数据工厂
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-factory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 20e94fa687a3008ac7112d1a6511f8cec92b544c
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487140"
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="14950-104">用于 .NET 的 Azure 数据工厂库</span><span class="sxs-lookup"><span data-stu-id="14950-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="14950-105">概述</span><span class="sxs-lookup"><span data-stu-id="14950-105">Overview</span></span>

<span data-ttu-id="14950-106">Azure 数据工厂是基于云的数据集成服务。</span><span class="sxs-lookup"><span data-stu-id="14950-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="14950-107">使用它可在云中创建数据驱动的工作流，用于协调和自动化数据移动与数据转换。</span><span class="sxs-lookup"><span data-stu-id="14950-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="14950-108">有关详细信息，请参阅 [Azure 数据工厂简介](/azure/data-factory/data-factory-introduction)。</span><span class="sxs-lookup"><span data-stu-id="14950-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library---data-factory-v2-preview"></a><span data-ttu-id="14950-109">管理库 - 数据工厂 V2（预览版）</span><span class="sxs-lookup"><span data-stu-id="14950-109">Management library - Data Factory V2 (Preview)</span></span>

<span data-ttu-id="14950-110">使用数据工厂 V2（预览版）中的管理库可创建和计划数据驱动的工作流（管道）。</span><span class="sxs-lookup"><span data-stu-id="14950-110">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory V2 (Preview).</span></span>  <span data-ttu-id="14950-111">有关详细信息，请参阅[使用 .NET SDK 创建数据工厂和管道](/azure/data-factory/quickstart-create-data-factory-dot-net)。</span><span class="sxs-lookup"><span data-stu-id="14950-111">For more information, see [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net).</span></span>

<span data-ttu-id="14950-112">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory)。</span><span class="sxs-lookup"><span data-stu-id="14950-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="14950-113">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="14950-113">Visual Studio Package Manager</span></span>

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a><span data-ttu-id="14950-114">代码示例</span><span class="sxs-lookup"><span data-stu-id="14950-114">Code Example</span></span>

<span data-ttu-id="14950-115">以下示例使用管理库来创建数据工厂。</span><span class="sxs-lookup"><span data-stu-id="14950-115">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="14950-116">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="14950-116">Explore the management APIs</span></span>](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a><span data-ttu-id="14950-117">管理库 - 数据工厂 V1</span><span class="sxs-lookup"><span data-stu-id="14950-117">Management library - Data Factory V1</span></span>

<span data-ttu-id="14950-118">使用数据工厂版本 1 中的管理库可创建和计划数据驱动的工作流（管道）。</span><span class="sxs-lookup"><span data-stu-id="14950-118">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory Version 1.</span></span>  <span data-ttu-id="14950-119">有关详细信息，请查看[数据工厂版本 1](/azure/data-factory/v1/data-factory-introduction) 的文档。</span><span class="sxs-lookup"><span data-stu-id="14950-119">For more information, review the documentation for [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span></span>

<span data-ttu-id="14950-120">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)。</span><span class="sxs-lookup"><span data-stu-id="14950-120">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="14950-121">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="14950-121">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="14950-122">代码示例</span><span class="sxs-lookup"><span data-stu-id="14950-122">Code Example</span></span>

<span data-ttu-id="14950-123">以下示例使用管理库来创建数据工厂。</span><span class="sxs-lookup"><span data-stu-id="14950-123">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="14950-124">了解管理 API</span><span class="sxs-lookup"><span data-stu-id="14950-124">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="14950-125">示例</span><span class="sxs-lookup"><span data-stu-id="14950-125">Samples</span></span>

* <span data-ttu-id="14950-126">使用数据工厂帮助提供见解的 [MyDriving - Azure IOT 和移动应用程序示例](https://azure.microsoft.com/resources/samples/mydriving/)。</span><span class="sxs-lookup"><span data-stu-id="14950-126">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="14950-127">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="14950-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
