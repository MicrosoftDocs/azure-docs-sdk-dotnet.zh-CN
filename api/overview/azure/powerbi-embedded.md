---
title: 用于 .NET 的 Power BI Embedded 库
description: 用于 .NET 的 Power BI Embedded 库参考
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: acb327b56e89522142e51016a6a9b279f995a674
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190370"
---
# <a name="power-bi-embedded-libraries-for-net"></a><span data-ttu-id="13d0b-103">用于 .NET 的 Power BI Embedded 库</span><span class="sxs-lookup"><span data-stu-id="13d0b-103">Power BI Embedded libraries for .NET</span></span>

<span data-ttu-id="13d0b-104">[Power BI](https://powerbi.microsoft.com/) 是基于云的业务分析服务，可提供最关键业务数据的单一视图。</span><span class="sxs-lookup"><span data-stu-id="13d0b-104">[Power BI](https://powerbi.microsoft.com/) is a cloud-based business analytics service that gives you a single view of your most critical business data.</span></span>

<span data-ttu-id="13d0b-105">若要详细了解如何在 .NET 中使用 Power BI，请参阅 [Power BI 的嵌入功能](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/)。</span><span class="sxs-lookup"><span data-stu-id="13d0b-105">To learn more about using Power BI with .NET, see [Embedding with Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span></span>

## <a name="client-library"></a><span data-ttu-id="13d0b-106">客户端库</span><span class="sxs-lookup"><span data-stu-id="13d0b-106">Client library</span></span>

<span data-ttu-id="13d0b-107">使用客户端库来连接 Power BI API，以访问数据集和报表并与其交互。</span><span class="sxs-lookup"><span data-stu-id="13d0b-107">Use the client library to connect with Power BI APIs to access and interact with data sets and reports.</span></span>

<span data-ttu-id="13d0b-108">直接从 Visual Studio [包管理器控制台][PackageManager]安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.PowerBI.Api)。</span><span class="sxs-lookup"><span data-stu-id="13d0b-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="13d0b-109">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="13d0b-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a><span data-ttu-id="13d0b-110">示例</span><span class="sxs-lookup"><span data-stu-id="13d0b-110">Example</span></span>

<span data-ttu-id="13d0b-111">以下示例检索并显示数据集和报表的列表。</span><span class="sxs-lookup"><span data-stu-id="13d0b-111">The following example retrieves and displays a list of datasets and reports.</span></span>

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
> [<span data-ttu-id="13d0b-112">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="13d0b-112">Explore the client APIs</span></span>](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a><span data-ttu-id="13d0b-113">示例</span><span class="sxs-lookup"><span data-stu-id="13d0b-113">Samples</span></span>

* [<span data-ttu-id="13d0b-114">Power BI 开发人员示例</span><span class="sxs-lookup"><span data-stu-id="13d0b-114">Power BI Developer Samples</span></span>](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [<span data-ttu-id="13d0b-115">Power BI .NET GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="13d0b-115">Power BI .NET GitHub repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)

<span data-ttu-id="13d0b-116">详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="13d0b-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
