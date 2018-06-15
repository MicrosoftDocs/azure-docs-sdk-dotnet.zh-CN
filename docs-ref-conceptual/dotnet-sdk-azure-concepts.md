---
title: 用于 .NET 的 Azure 管理库用法概念和模式
description: ''
keywords: Azure, .NET, SDK, API, 模式, 概念, fluent, 日志记录
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: b817216e114e5ab3ff22c1c5adb0f892c7874147
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2018
ms.locfileid: "29752859"
---
# <a name="azure-management-library-for-net-fluent-concepts"></a>用于 .NET 的 Azure 管理库的 Fluent 概念

本文帮助读者了解如何有效使用用于 .NET 的 Azure 管理库中的 Fluent 界面。

## <a name="building-resources-using-a-fluent-interface"></a>使用 Fluent 界面生成资源

Fluent 界面是特定形式的生成器模式，可通过用于强制实施正确资源配置的方法链来创建对象。 例如，入口点 Azure 对象就是使用 Fluent 界面创建的：

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a>资源集合

上面所示的 `Microsoft.Azure.Management.Fluent.Azure` 对象是 Fluent 管理库库中所有资源创建操作的入口点。 使用 `Azure` 对象的资源集合来选择要处理的资源类型。 例如，对于 SQL 数据库：

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

如上所示，使用 API 建立的大多数 Fluent“对话”首先都会针对所要处理的 Azure 资源选择适当的资源集合。  然后，Intellisense in Visual Studio 会引导你完成对话。 

![驱动 Fluent 对话的 Intellisense in Visual Studio 的 GIF](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a>列表和迭代

每个资源集合提供一个 `List()` 方法来返回当前订阅中该资源的每个实例。 例如，`Azure.SqlServers.List()` 返回订阅中的所有 SQL 服务器。

使用 `ListByResourceGroup()` 方法可将返回列表的范围限定为特定的 [Azure 资源组](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)。  

可以像执行普通的 `List<T>` 一样循环访问返回的集合：

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a>可操作的谓词

名称中包含谓词的资源集合方法在 Azure 中立即执行。 这些方法以同步方式工作，在完成之前会阻止当前线程中的执行。 

| Verb   |  示例用法 |
|--------|---------------|
| 创建 | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| 应用  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| 删除 | `azure.Disks.DeleteById(id)` | 
| 列出   | `azure.SqlServers.List()` | 
| Get    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> `Define()` 和 `Update()` 是谓词，但除非后接 `Create()` 或 `Apply()`，否则不会阻塞。
 
特定的资源对象包含可更改 Azure 中资源状态的谓词。 例如：

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

本部分中所述的大多数方法也具有异步版本（以 `Async` 后缀表示）。

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a>延缓资源创建

如果某个新资源依赖于尚不存在的另一个资源，创建 Azure 资源时会出现难题。 例如，在创建新虚拟机时保留公共 IP 地址和设置磁盘。 我们不需要确认是否保留了地址或创建了磁盘，而只需使用这些资源配置虚拟机。

使用可创建对象可以定义要在代码中使用的 Azure 资源，但仅当需要在 Azure 中使用时才创建这些资源。 使用可创建对象编写的代码可将 Azure 环境中的资源创建过程卸载到管理 API，从而大幅提升性能。 

通过资源集合的不带 `Create()` 谓词的 `Define()` 谓词生成可创建对象：

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

可创建对象定义的 Azure 资源尚不在订阅中存在。 可创建对象是管理 API 根据需要（调用 `.Create()` 时）创建的资源的本地表示形式。 可以在需要此资源的其他 Azure 资源的定义中使用此可创建对象。 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

使用资源集合的 `Create()` 方法在 Azure 订阅中创建资源。 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

将可创建对象传递给 `Create()` 会返回 `ICreatedResources` 对象而非单个资源对象。  使用 `CreatedRelatedResource` 对象可以访问 `Create()` 调用创建的所有资源，而不仅仅是资源集合中的类型。 访问 Azure 中针对上述示例中创建的虚拟机所创建的公共 IP 地址：

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a>异常处理

管理 API 可定义用于扩展 `Microsoft.Rest.RestException` 的异常类。 在相关的 `try` 语句后面使用 `catch (RestException exception)` 块捕获管理 API 生成的异常。

## <a name="logs-and-tracing"></a>日志和跟踪

用于 .NET 的 Fluent Azure 管理库中的日志记录利用基础 [AutoRest](https://github.com/Azure/AutoRest) 服务客户端跟踪。

创建用于实现 `Microsoft.Rest.IServiceClientTracingInterceptor` 的类。  此类负责截获日志消息并将其传递给所用的任何日志记录机制。  在此示例中，我们只需将消息写入控制台，但也可将其传递给 Log4Net、`Microsoft.Extensions.Logging` 或其他任何日志记录框架。

```csharp
class ConsoleTracer : IServiceClientTracingInterceptor
{
    public void Information(string message)
    {
        Console.WriteLine(message);
    }

    public void TraceError(string invocationId, Exception exception)
    {
        Console.WriteLine("Exception in {0}: {1}", invocationId, exception);
    }

    public void ReceiveResponse(string invocationId, HttpResponseMessage response) { }

    public void SendRequest(string invocationId, HttpRequestMessage request) { }

    public void Configuration(string source, string name, string value) { }

    public void EnterMethod(string invocationId, object instance, string method, IDictionary<string, object> parameters) { }

    public void ExitMethod(string invocationId, object returnValue) { }
}
```

在创建 `Microsoft.Azure.Management.Fluent.Azure` 对象之前，请通过调用 `ServiceClientTracing.AddTracingInterceptor()` 来初始化上面创建的 `IServiceClientTracingInterceptor`，并将 `ServiceClientTracing.IsEnabled` 设置为 *true*。  创建 `Azure` 对象时，请包含 `.WithDelegatingHandler()` 和 `.WithLogLevel()` 方法，将客户端连接到 AutoRest 的服务客户端跟踪。

```csharp
ServiceClientTracing.AddTracingInterceptor(new ConsoleTracer());
ServiceClientTracing.IsEnabled = true;

var azure = Azure
    .Configure()
    .WithDelegatingHandler(new HttpLoggingDelegatingHandler())
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

按如下所述定义 `HttpLoggingDelegatingHandler` 日志级别：

| 跟踪级别 | 日志记录已启用 
| ------------ | ---------------
| HttpLoggingDelegatingHandler.Level.None | 无输出
| HttpLoggingDelegatingHandler.Level.Basic | 记录基础 REST 调用的 URL、响应代码和时间
| HttpLoggingDelegatingHandler.Level.Body | Basic 中的所有内容，加上 REST 调用的请求和响应正文
| HttpLoggingDelegatingHandler.Level.Headers | Basic 中的所有内容，加上请求和响应标头 REST 调用
| HttpLoggingDelegatingHandler.Level.BodyAndHeaders | Body 和 Headers 日志级别中的所有内容
