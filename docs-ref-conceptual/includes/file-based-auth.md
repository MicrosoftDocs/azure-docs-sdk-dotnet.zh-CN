创建名为 `azureauth.json` 的文本文件。 粘贴在创建服务主体时获得的 JSON 输出。

将此文件保存在系统上可供代码读取的安全位置。 使用 PowerShell 设置包含文件完整路径的名为 `AZURE_AUTH_LOCATION` 的环境变量，例如：

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
