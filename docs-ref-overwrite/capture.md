---
<span data-ttu-id="d12a6-101">uid: Microsoft.Azure.Management.Compute.VirtualMachinesOperationsExtensions.Capture(Microsoft.Azure.Management.Compute.IVirtualMachinesOperations,System.String,System.String,Microsoft.Azure.Management.Compute.Models.VirtualMachineCaptureParameters) summary: *content</span><span class="sxs-lookup"><span data-stu-id="d12a6-101">uid: Microsoft.Azure.Management.Compute.VirtualMachinesOperationsExtensions.Capture(Microsoft.Azure.Management.Compute.IVirtualMachinesOperations,System.String,System.String,Microsoft.Azure.Management.Compute.Models.VirtualMachineCaptureParameters) summary: *content</span></span>
---

<span data-ttu-id="d12a6-102">此处是通过覆盖文件方法注入的内容，因此作者可以根据需要将任意数量的内容添加到 Markown 格式的已生成 API 文档。</span><span class="sxs-lookup"><span data-stu-id="d12a6-102">Here is content that is injected by the overwrite file method, so writers can add as much as they want to the generated API documentation in Markown format.</span></span>

---
<span data-ttu-id="d12a6-103">uid: Microsoft.Azure.Management.Compute.VirtualMachinesOperationsExtensions.Capture(Microsoft.Azure.Management.Compute.IVirtualMachinesOperations,System.String,System.String,Microsoft.Azure.Management.Compute.Models.VirtualMachineCaptureParameters) remarks: *content</span><span class="sxs-lookup"><span data-stu-id="d12a6-103">uid: Microsoft.Azure.Management.Compute.VirtualMachinesOperationsExtensions.Capture(Microsoft.Azure.Management.Compute.IVirtualMachinesOperations,System.String,System.String,Microsoft.Azure.Management.Compute.Models.VirtualMachineCaptureParameters) remarks: *content</span></span>
---

<span data-ttu-id="d12a6-104">下面的代码演示如何使用 Azure.NET SDK 调用捕获方法。</span><span class="sxs-lookup"><span data-stu-id="d12a6-104">The code below demonstrates how to call the Capture method using the Azure .NET SDK.</span></span> 

```csharp
using Microsoft.Azure.Management.Compute;
using Microsoft.Azure.Management.Compute.Models;
using Microsoft.Rest;

namespace MyAzureVmClientApp
{
    class Program
    {
        static void Main(string[] args)
        {
            var token = "[Token Obtained from ADAL]";

            var credential = new TokenCredentials(token);

            var captureResponse = 
                new ComputeManagementClient(credential)
                .VirtualMachines
                    .Capture(
                        "myResourceGroup",
                        "myVmName",
                        new VirtualMachineCaptureParameters
                        {
                            DestinationContainerName = "myblobcontainer",
                            OverwriteVhds = true,
                            VhdPrefix = "backup"
                        });
        }
    }
}
```

