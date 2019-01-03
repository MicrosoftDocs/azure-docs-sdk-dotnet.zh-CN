---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: e25b6ac74033f3b0a7610bf66feb654acb43054c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53430513"
---
<span data-ttu-id="05f01-101">创建名为 `azureauth.json` 的文本文件。</span><span class="sxs-lookup"><span data-stu-id="05f01-101">Create a text file named `azureauth.json`.</span></span> <span data-ttu-id="05f01-102">粘贴在创建服务主体时获得的 JSON 输出。</span><span class="sxs-lookup"><span data-stu-id="05f01-102">Paste the JSON output from when you created the service principal.</span></span>

<span data-ttu-id="05f01-103">将此文件保存在系统上可供代码读取的安全位置。</span><span class="sxs-lookup"><span data-stu-id="05f01-103">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="05f01-104">使用 PowerShell 设置包含文件完整路径的名为 `AZURE_AUTH_LOCATION` 的环境变量，例如：</span><span class="sxs-lookup"><span data-stu-id="05f01-104">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
