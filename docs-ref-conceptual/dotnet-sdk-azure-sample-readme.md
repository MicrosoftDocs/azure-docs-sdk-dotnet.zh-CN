---
title: 用于 .NET 的 Azure 管理库的示例说明
description: 获取有关使用用于 .NET 的 Azure 管理库创建和更新资源的示例代码。
keywords: Azure, .NET, SDK, API, 示例, 例子
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a931e623768e1fddad263c7da8eb864c37613379
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2018
ms.locfileid: "29752469"
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a><span data-ttu-id="40900-104">用于 .NET 的 Azure 管理库的示例说明</span><span class="sxs-lookup"><span data-stu-id="40900-104">Azure management libraries for .NET sample instructions</span></span>

<span data-ttu-id="40900-105">本文介绍运行用于 .NET 的 Azure 管理库示例所要满足的先决条件和执行的身份验证。</span><span class="sxs-lookup"><span data-stu-id="40900-105">This article describes the prerequisites and authentication required for running the samples for the Azure management libraries for .NET.</span></span>

## <a name="prerequisties"></a><span data-ttu-id="40900-106">先决条件</span><span class="sxs-lookup"><span data-stu-id="40900-106">Prerequisties</span></span> 

* <span data-ttu-id="40900-107">[Visual Studio 2017](https://www.visualstudio.com/vs/) 或 [.NET Core SDK](https://www.microsoft.com/net/download/core)</span><span class="sxs-lookup"><span data-stu-id="40900-107">[Visual Studio 2017](https://www.visualstudio.com/vs/) or [.NET Core SDK](https://www.microsoft.com/net/download/core)</span></span>
* <span data-ttu-id="40900-108">[Microsoft Azure 订阅](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="40900-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [<span data-ttu-id="40900-109">Git 命令行客户端</span><span class="sxs-lookup"><span data-stu-id="40900-109">Git command line client</span></span>](https://git-scm.com/)
* [<span data-ttu-id="40900-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="40900-110">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a><span data-ttu-id="40900-111">对所有示例进行身份验证</span><span class="sxs-lookup"><span data-stu-id="40900-111">Authentication for all samples</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a><span data-ttu-id="40900-112">运行示例</span><span class="sxs-lookup"><span data-stu-id="40900-112">Running the samples</span></span>

<span data-ttu-id="40900-113">使用 Git 克隆示例后，可在 Visual Studio 中打开示例并使用 IDE 运行示例。</span><span class="sxs-lookup"><span data-stu-id="40900-113">Once you have used Git to clone the sample, you can open the sample in Visual Studio and run the sample using the IDE.</span></span>  <span data-ttu-id="40900-114">或者，使用 .NET Core SDK 从命令行生成并运行示例，如下所示：</span><span class="sxs-lookup"><span data-stu-id="40900-114">Alternatively, use the .NET Core SDK to build and run the sample from the command line, like this:</span></span>

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```