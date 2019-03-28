---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 5c8cb328802cfb94e944e4241852fb9568e8507f
ms.sourcegitcommit: e534dad2d96b72ab6a9bc4b5567508962bd7e05c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58343326"
---
<span data-ttu-id="279bf-101">若要使用用于 .NET 的 Azure 管理库，.NET 应用程序需要拥有在 Azure 订阅中读取和创建资源的权限。</span><span class="sxs-lookup"><span data-stu-id="279bf-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="279bf-102">创建一个服务主体，并将应用配置为使用该服务主体的凭据运行，以授予此访问权限。</span><span class="sxs-lookup"><span data-stu-id="279bf-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="279bf-103">通过服务主体可以创建一个与用户标识关联的非交互式帐户，该帐户仅拥有运行应用所需的特权。</span><span class="sxs-lookup"><span data-stu-id="279bf-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="279bf-104">首先登录到 [Azure Cloud Shell](https://shell.azure.com/bash)。</span><span class="sxs-lookup"><span data-stu-id="279bf-104">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="279bf-105">验证当前使用的是要在其中创建服务主体的订阅。</span><span class="sxs-lookup"><span data-stu-id="279bf-105">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="279bf-106">此时将显示订阅信息。</span><span class="sxs-lookup"><span data-stu-id="279bf-106">Your subscription information is displayed.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "15dbcfa8-4b93-4c9a-881c-6189d39f04d4",
  "isDefault": true,
  "name": "my-subscription",
  "state": "Enabled",
  "tenantId": "43413cc1-5886-4711-9804-8cfea3d1c3ee",
  "user": {
    "cloudShellID": true,
    "name": "jane@contoso.com",
    "type": "user"
  }
}
```

<span data-ttu-id="279bf-107">如果尚未登录到正确的订阅，请通过键入 `az account set -s <name or ID of subscription>` 选择正确的订阅。</span><span class="sxs-lookup"><span data-stu-id="279bf-107">If you're not logged into the correct subscription, select the correct one by typing `az account set -s <name or ID of subscription>`.</span></span>

<span data-ttu-id="279bf-108">使用以下命令创建服务主体：</span><span class="sxs-lookup"><span data-stu-id="279bf-108">Create the service principal with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

<span data-ttu-id="279bf-109">服务主体信息将以 JSON 格式显示。</span><span class="sxs-lookup"><span data-stu-id="279bf-109">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "b52dd125-9272-4b21-9862-0be667bdf6dc",
  "clientSecret": "ebc6e170-72b2-4b6f-9de2-99410964d2d0",
  "subscriptionId": "ffa52f27-be12-4cad-b1ea-c2c241b6cceb",
  "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="279bf-110">将 JSON 输出复制并粘贴到文本编辑器中，供以后使用。</span><span class="sxs-lookup"><span data-stu-id="279bf-110">Copy and paste the JSON output to a text editor for use later.</span></span>
