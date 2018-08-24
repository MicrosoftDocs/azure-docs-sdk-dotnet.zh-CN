<span data-ttu-id="a9de7-101">创建名为 `azureauth.json` 的文本文件。</span><span class="sxs-lookup"><span data-stu-id="a9de7-101">Create a text file named `azureauth.json`.</span></span> <span data-ttu-id="a9de7-102">粘贴在创建服务主体时获得的 JSON 输出。</span><span class="sxs-lookup"><span data-stu-id="a9de7-102">Paste the JSON output from when you created the service principal.</span></span>

<span data-ttu-id="a9de7-103">将此文件保存在系统上可供代码读取的安全位置。</span><span class="sxs-lookup"><span data-stu-id="a9de7-103">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="a9de7-104">使用 PowerShell 设置包含文件完整路径的名为 `AZURE_AUTH_LOCATION` 的环境变量，例如：</span><span class="sxs-lookup"><span data-stu-id="a9de7-104">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
