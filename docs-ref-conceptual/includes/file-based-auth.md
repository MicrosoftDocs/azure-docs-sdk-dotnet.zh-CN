<span data-ttu-id="74050-101">使用服务主体凭据创建名为 `azureauth.properties` 的文本文件：</span><span class="sxs-lookup"><span data-stu-id="74050-101">Create a text file named `azureauth.properties` using the service principal credentials:</span></span>

```plaintext
# sample management library properties file
subscription=15dbcfa8-4b93-4c9a-881c-6189d39f04d4
client=a2ab11af-01aa-4759-8345-7803287dbd39
key=password
tenant=43413cc1-5886-4711-9804-8cfea3d1c3ee
managementURI=https://management.core.windows.net/
baseURL=https://management.azure.com/
authURL=https://login.windows.net/
graphURL=https://graph.windows.net/
```

- <span data-ttu-id="74050-102">subscription：使用运行 `Login-AzureRmAccount` 后返回的 *SubscriptionId* 值。</span><span class="sxs-lookup"><span data-stu-id="74050-102">subscription: use the *SubscriptionId* value from when you ran `Login-AzureRmAccount`.</span></span>
- <span data-ttu-id="74050-103">client：使用服务主体输出中的 *ApplicationId* 值。</span><span class="sxs-lookup"><span data-stu-id="74050-103">client: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="74050-104">key：使用运行 `New-AzureRmADServicePrincipal`（不带引号）时分配的 *-Password* 参数。</span><span class="sxs-lookup"><span data-stu-id="74050-104">key: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="74050-105">tenant：使用运行 `Login-AzureRmAccount` 后返回的 *TenantId* 值。</span><span class="sxs-lookup"><span data-stu-id="74050-105">tenant: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="74050-106">将此文件保存在系统上可供代码读取的安全位置。</span><span class="sxs-lookup"><span data-stu-id="74050-106">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="74050-107">使用 PowerShell 设置包含文件完整路径的名为 `AZURE_AUTH_LOCATION` 的环境变量，例如：</span><span class="sxs-lookup"><span data-stu-id="74050-107">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
