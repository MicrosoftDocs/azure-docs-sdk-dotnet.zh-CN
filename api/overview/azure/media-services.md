---
title: 用于 .NET 的 Azure 媒体服务库
description: 用于 .NET 的 Azure 媒体服务库参考
keywords: Azure, .NET, SDK, API, 媒体服务
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
ms.locfileid: "23487440"
---
# <a name="azure-media-services-libraries-for-net"></a><span data-ttu-id="5d6fe-104">用于 .NET 的 Azure 媒体服务库</span><span class="sxs-lookup"><span data-stu-id="5d6fe-104">Azure Media Services libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="5d6fe-105">概述</span><span class="sxs-lookup"><span data-stu-id="5d6fe-105">Overview</span></span>

<span data-ttu-id="5d6fe-106">Microsoft Azure 媒体服务是一个可扩展的基于云的平台，使开发人员能够生成可缩放的媒体管理和传送应用程序。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-106">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="5d6fe-107">媒体服务基于 REST API，你可以使用这些 API 安全地上传、存储、编码和打包视频或音频内容，以供点播以及以实时流形式传送到各种客户端（例如，电视、电脑和移动设备）。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-107">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span> 

<span data-ttu-id="5d6fe-108">有关详细信息，请参阅[概述](/azure/media-services/media-services-overview)和 [.NET 入门](/azure/media-services/media-services-dotnet-how-to-use)。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-108">To learn more, see [Overview](/azure/media-services/media-services-overview) and [Getting started with .NET](/azure/media-services/media-services-dotnet-how-to-use).</span></span> 

## <a name="client-library"></a><span data-ttu-id="5d6fe-109">客户端库</span><span class="sxs-lookup"><span data-stu-id="5d6fe-109">Client library</span></span>

<span data-ttu-id="5d6fe-110">借助 Azure 媒体服务 .NET SDK 库可以使用 .NET 针对媒体服务编程。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-110">The Azure Media Services .NET SDK library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="5d6fe-111">使用 Azure 媒体服务客户端库可以针对媒体服务 API 进行连接、身份验证和开发。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-111">Use the Azure Media Services client library to connect, authenticate, and develop against Media Services APIs.</span></span>  

<span data-ttu-id="5d6fe-112">有关详细信息，请参阅[使用 .NET SDK 开始传送点播内容](/azure/media-services/media-services-dotnet-get-started)。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-112">For more information, see [Get started with delivering content on demand using .NET SDK](/azure/media-services/media-services-dotnet-get-started).</span></span>

<span data-ttu-id="5d6fe-113">直接从 Visual Studio [包管理器控制台][PackageManager]或使用 [.NET Core CLI][DotNetCLI] 安装 [NuGet 包](https://www.nuget.org/packages/windowsazure.mediaservices)。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-113">Install the [NuGet package](https://www.nuget.org/packages/windowsazure.mediaservices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5d6fe-114">Visual Studio 包管理器</span><span class="sxs-lookup"><span data-stu-id="5d6fe-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a><span data-ttu-id="5d6fe-115">代码示例</span><span class="sxs-lookup"><span data-stu-id="5d6fe-115">Code Example</span></span>

<span data-ttu-id="5d6fe-116">以下代码示例使用媒体服务 .NET SDK 执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="5d6fe-116">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="5d6fe-117">创建编码作业。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-117">Create an encoding job.</span></span>
- <span data-ttu-id="5d6fe-118">获取对 Media Encoder Standard 编码器的引用。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-118">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="5d6fe-119">指定使用自适应流式处理预设。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-119">Specify to use the Adaptive Streaming preset.</span></span>
- <span data-ttu-id="5d6fe-120">将一个编码任务添加到该作业。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-120">Add a single encoding task to the job.</span></span>
- <span data-ttu-id="5d6fe-121">指定要编码的输入资产。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-121">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="5d6fe-122">创建一个输出资产用于接收编码的资产。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-122">Create an output asset to receive the encoded asset.</span></span>
- <span data-ttu-id="5d6fe-123">提交作业。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-123">Submit the job.</span></span>


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
> [<span data-ttu-id="5d6fe-124">了解客户端 API</span><span class="sxs-lookup"><span data-stu-id="5d6fe-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a><span data-ttu-id="5d6fe-125">示例</span><span class="sxs-lookup"><span data-stu-id="5d6fe-125">Samples</span></span>

- [<span data-ttu-id="5d6fe-126">流式传输受 Apple FairPlay 保护的 HLS 内容</span><span class="sxs-lookup"><span data-stu-id="5d6fe-126">Stream your HLS content Protected with Apple FairPlay</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [<span data-ttu-id="5d6fe-127">使用 .NET SDK 扩展将 Blob 复制到 Azure 媒体服务资产</span><span class="sxs-lookup"><span data-stu-id="5d6fe-127">Copy blob into an Azure Media Services asset using .NET SDK Extensions</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)
- [<span data-ttu-id="5d6fe-128">使用 .NET SDK 通过 Azure 媒体服务编码和传送实时流</span><span class="sxs-lookup"><span data-stu-id="5d6fe-128">Encode and Deliver a Live Stream with Azure Media Services using .NET SDK</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)

<span data-ttu-id="5d6fe-129">查看 Azure 媒体服务示例的[完整列表](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services)。</span><span class="sxs-lookup"><span data-stu-id="5d6fe-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) of Azure Media Services samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
