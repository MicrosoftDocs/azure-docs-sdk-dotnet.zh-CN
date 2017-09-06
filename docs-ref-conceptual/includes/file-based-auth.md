使用服务主体凭据创建名为 `azureauth.properties` 的文本文件：

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

- subscription：使用运行 `Login-AzureRmAccount` 后返回的 *SubscriptionId* 值。
- client：使用服务主体输出中的 *ApplicationId* 值。
- key：使用运行 `New-AzureRmADServicePrincipal`（不带引号）时分配的 *-Password* 参数。
- tenant：使用运行 `Login-AzureRmAccount` 后返回的 *TenantId* 值。

将此文件保存在系统上可供代码读取的安全位置。 使用 PowerShell 设置包含文件完整路径的名为 `AZURE_AUTH_LOCATION` 的环境变量，例如：

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
