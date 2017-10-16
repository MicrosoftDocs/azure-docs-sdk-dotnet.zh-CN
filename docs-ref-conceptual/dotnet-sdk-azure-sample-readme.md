---
title: "用于 .NET 的 Azure 管理库的示例说明"
description: "获取有关使用用于 .NET 的 Azure 管理库创建和更新资源的示例代码。"
keywords: "Azure, .NET, SDK, API, 示例, 例子"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: ffda7cca724962e6f953432c5cab04485ddabb03
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a>用于 .NET 的 Azure 管理库的示例说明

本文介绍运行用于 .NET 的 Azure 管理库示例所要满足的先决条件和执行的身份验证。

## <a name="prerequisties"></a>先决条件 

* [Visual Studio 2017](https://www.visualstudio.com/vs/) 或 [.NET Core SDK](https://www.microsoft.com/net/download/core)
* [Microsoft Azure 订阅](https://azure.microsoft.com/free/)
* [Git 命令行客户端](https://git-scm.com/)
* [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a>对所有示例进行身份验证

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a>运行示例

使用 Git 克隆示例后，可在 Visual Studio 中打开示例并使用 IDE 运行示例。  或者，使用 .NET Core SDK 从命令行生成并运行示例，如下所示：

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```