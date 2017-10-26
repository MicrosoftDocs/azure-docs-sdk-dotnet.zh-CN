---
title: "用于 .NET 的 Azure 媒体服务库"
description: "用于 .NET 的 Azure 媒体服务库参考"
keywords: "Azure, .NET, SDK, API, 媒体服务"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: media-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 872ed60363c0c886e9844d0cb0bef07cf41a0242
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
---
# <a name="azure-media-services-libraries-for-net"></a>用于 .NET 的 Azure 媒体服务库

## <a name="overview"></a>概述

Microsoft Azure 媒体服务是一个可扩展的基于云的平台，使开发人员能够生成可缩放的媒体管理和传送应用程序。 媒体服务基于 REST API，你可以使用这些 API 安全地上传、存储、编码和打包视频或音频内容，以供点播以及以实时流形式传送到各种客户端（例如，电视、电脑和移动设备）。 

有关详细信息，请参阅[概述](/azure/media-services/media-services-overview)和 [.NET 入门](/azure/media-services/media-services-dotnet-how-to-use)。 

## <a name="client-library"></a>客户端库

借助 Azure 媒体服务 .NET SDK 库可以使用 .NET 针对媒体服务编程。 使用 Azure 媒体服务客户端库可以针对媒体服务 API 进行连接、身份验证和开发。  

有关详细信息，请参阅[使用 .NET SDK 开始传送点播内容](/azure/media-services/media-services-dotnet-get-started)。

直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/windowsazure.mediaservices)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 包管理器

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a>代码示例

以下代码示例使用媒体服务 .NET SDK 执行下列任务：

- 创建编码作业。
- 获取对 Media Encoder Standard 编码器的引用。
- 指定使用自适应流式处理预设。
- 将一个编码任务添加到该作业。
- 指定要编码的输入资产。
- 创建一个输出资产用于接收编码的资产。
- 提交作业。


```csharp
/* Include this 'using' directive:
using Microsoft.WindowsAzure.MediaServices.Client;
*/

CloudMediaContext context = new CloudMediaContext(new Uri(mediaServiceRESTAPIEndpoint), tokenProvider);

// Get an uploaded asset.
IAsset asset = context.Assets.FirstOrDefault();

// Encode and generate the output using the "Adaptive Streaming" preset.
// Declare a new job.
IJob job = context.Jobs.Create("Media Encoder Standard Job");
// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName)
    .ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();
if (processor == null) 
{
    throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));
}

// Create a task with the encoding details, using a string preset.
// In this case "Adaptive Streaming" preset is used.
ITask task = job.Tasks.AddNew("My encoding task", processor, "Adaptive Streaming", TaskOptions.None);

// Specify the input asset to be encoded.
task.InputAssets.Add(asset);
// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);

job.Submit();
job.GetExecutionProgressTask(CancellationToken.None).Wait();
```

> [!div class="nextstepaction"]
> [了解客户端 API](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a>示例

- [流式传输受 Apple FairPlay 保护的 HLS 内容](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [使用 .NET SDK 扩展将 Blob 复制到 Azure 媒体服务资产](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)
- [使用 .NET SDK 通过 Azure 媒体服务编码和传送实时流](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)

查看 Azure 媒体服务示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services)。


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
