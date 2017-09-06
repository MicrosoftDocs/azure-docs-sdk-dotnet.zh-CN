---
title: "用于 .NET 的 Power BI Embedded 库"
description: "用于 .NET 的 Power BI Embedded 库参考"
keywords: Azure, .NET, SDK, API, Power BI Embedded
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: f9a6aac8dbb3c284948e9140ad87aff5e415d9fb
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="power-bi-embedded-libraries-for-net"></a><span data-ttu-id="fe533-104">用于 .NET 的 Power BI Embedded 库</span><span class="sxs-lookup"><span data-stu-id="fe533-104">Power BI Embedded libraries for .NET</span></span>

<span data-ttu-id="fe533-105">[Power BI](https://powerbi.microsoft.com/) 是基于云的业务分析服务，可提供最关键业务数据的单一视图。</span><span class="sxs-lookup"><span data-stu-id="fe533-105">[Power BI](https://powerbi.microsoft.com/) is a cloud-based business analytics service that gives you a single view of your most critical business data.</span></span>

<span data-ttu-id="fe533-106">若要详细了解如何在 .NET 中使用 Power BI，请参阅 [Power BI 的嵌入功能](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/)。</span><span class="sxs-lookup"><span data-stu-id="fe533-106">To learn more about using Power BI with .NET, see [Embedding with Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span></span>

## <a name="client-library"></a><span data-ttu-id="fe533-107">客户端库</span><span class="sxs-lookup"><span data-stu-id="fe533-107">Client library</span></span>

<span data-ttu-id="fe533-108">使用客户端库来连接 Power BI API，以访问数据集和报表并与其交互。</span><span class="sxs-lookup"><span data-stu-id="fe533-108">Use the client library to connect with Power BI APIs to access and interact with data sets and reports.</span></span>

<span data-ttu-id="fe533-109">直接从 Visual Studio [包管理器控制台][PackageManager]安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.PowerBI.Api)。</span><span class="sxs-lookup"><span data-stu-id="fe533-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fe533-110">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="fe533-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a><span data-ttu-id="fe533-111">示例</span><span class="sxs-lookup"><span data-stu-id="fe533-111">Example</span></span>

<span data-ttu-id="fe533-112">以下示例检索并显示数据集和报表的列表。</span><span class="sxs-lookup"><span data-stu-id="fe533-112">The following example retrieves and displays a list of datasets and reports.</span></span>

```csharp
/* Include these'using' directive:
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;
*/
using (PowerBIClient client = new PowerBIClient(new Uri(apiUrl), tokenCredentials))
{

    Console.WriteLine("\r*** DATASETS ***\r");

    // List of datasets in a group/app workspace
    ODataResponseListDataset datasetList = client.Datasets.GetDatasetsInGroup(groupId);

    foreach(Dataset ds in datasetList.Value)
    {
        Console.WriteLine(ds.Id + " | " + ds.Name);
    }

    Console.WriteLine("\r*** REPORTS ***\r");

    // List of reports in a group/app workspace
    ODataResponseListReport reportList = client.Reports.GetReportsInGroup(groupId);

    foreach (Report rpt in reportList.Value)
    {
        Console.WriteLine(rpt.Id + " | " + rpt.Name +  " | DatasetID = " + rpt.DatasetId);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe533-113">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="fe533-113">Explore the client APIs</span></span>](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a><span data-ttu-id="fe533-114">示例</span><span class="sxs-lookup"><span data-stu-id="fe533-114">Samples</span></span>

* [<span data-ttu-id="fe533-115">Power BI 开发人员示例</span><span class="sxs-lookup"><span data-stu-id="fe533-115">Power BI Developer Samples</span></span>](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [<span data-ttu-id="fe533-116">Power BI .NET GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="fe533-116">Power BI .NET GitHub repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)

<span data-ttu-id="fe533-117">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="fe533-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
