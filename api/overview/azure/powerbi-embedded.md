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
# <a name="power-bi-embedded-libraries-for-net"></a>用于 .NET 的 Power BI Embedded 库

[Power BI](https://powerbi.microsoft.com/) 是基于云的业务分析服务，可提供最关键业务数据的单一视图。

若要详细了解如何在 .NET 中使用 Power BI，请参阅 [Power BI 的嵌入功能](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/)。

## <a name="client-library"></a>客户端库

使用客户端库来连接 Power BI API，以访问数据集和报表并与其交互。

直接从 Visual Studio [包管理器控制台][PackageManager]安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.PowerBI.Api)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a>示例

以下示例检索并显示数据集和报表的列表。

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
> [了解客户端 API](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a>示例

* [Power BI 开发人员示例](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [Power BI .NET GitHub 存储库](https://github.com/Microsoft/PowerBI-CSharp)

详细了解可在应用中使用的[示例 .NET 代码](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
