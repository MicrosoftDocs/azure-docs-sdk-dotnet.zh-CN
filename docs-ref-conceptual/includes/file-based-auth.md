---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190710"
---
<span data-ttu-id="2ae19-101">创建名为 `azureauth.json` 的文本文件。</span><span class="sxs-lookup"><span data-stu-id="2ae19-101">Create a text file named `azureauth.json`.</span></span> <span data-ttu-id="2ae19-102">粘贴在创建服务主体时获得的 JSON 输出。</span><span class="sxs-lookup"><span data-stu-id="2ae19-102">Paste the JSON output from when you created the service principal.</span></span>

<span data-ttu-id="2ae19-103">将此文件保存在系统上可供代码读取的安全位置。</span><span class="sxs-lookup"><span data-stu-id="2ae19-103">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="2ae19-104">使用 PowerShell 设置包含文件完整路径的名为 `AZURE_AUTH_LOCATION` 的环境变量，例如：</span><span class="sxs-lookup"><span data-stu-id="2ae19-104">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
