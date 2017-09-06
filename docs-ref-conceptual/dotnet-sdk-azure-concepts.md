---
title: "用于 .NET 的 Azure 管理库用法概念和模式"
description: 
keywords: "Azure, .NET, SDK, API, 模式, 概念, fluent, 日志记录"
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
ms.openlocfilehash: b2e6849f06c36de18471e55c468e984f4205f646
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-library-for-net-fluent-concepts"></a><span data-ttu-id="7c991-103">用于 .NET 的 Azure 管理库的 Fluent 概念</span><span class="sxs-lookup"><span data-stu-id="7c991-103">Azure management library for .NET fluent concepts</span></span>

<span data-ttu-id="7c991-104">本文帮助读者了解如何有效使用用于 .NET 的 Azure 管理库中的 Fluent 界面。</span><span class="sxs-lookup"><span data-stu-id="7c991-104">This article will help you understand how to effectively use the fluent interface in the Azure management libraries for .NET.</span></span>

## <a name="building-resources-using-a-fluent-interface"></a><span data-ttu-id="7c991-105">使用 Fluent 界面生成资源</span><span class="sxs-lookup"><span data-stu-id="7c991-105">Building resources using a fluent interface</span></span>

<span data-ttu-id="7c991-106">Fluent 界面是特定形式的生成器模式，可通过用于强制实施正确资源配置的方法链来创建对象。</span><span class="sxs-lookup"><span data-stu-id="7c991-106">A fluent interface is a specific form of the builder pattern that creates objects through a method chain that enforces correct configuration of a resource.</span></span> <span data-ttu-id="7c991-107">例如，入口点 Azure 对象就是使用 Fluent 界面创建的：</span><span class="sxs-lookup"><span data-stu-id="7c991-107">For example, the entry-point Azure object is created using a fluent interface:</span></span>

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a><span data-ttu-id="7c991-108">资源集合</span><span class="sxs-lookup"><span data-stu-id="7c991-108">Resource collections</span></span>

<span data-ttu-id="7c991-109">上面所示的 `Microsoft.Azure.Management.Fluent.Azure` 对象是 Fluent 管理库库中所有资源创建操作的入口点。</span><span class="sxs-lookup"><span data-stu-id="7c991-109">The `Microsoft.Azure.Management.Fluent.Azure` object shown above is the entry point for all resource creation in the fluent management libraries.</span></span> <span data-ttu-id="7c991-110">使用 `Azure` 对象的资源集合来选择要处理的资源类型。</span><span class="sxs-lookup"><span data-stu-id="7c991-110">Select which type of resources to work with using the resource collections in the `Azure` object.</span></span> <span data-ttu-id="7c991-111">例如，对于 SQL 数据库：</span><span class="sxs-lookup"><span data-stu-id="7c991-111">For example, for SQL Database:</span></span>

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

<span data-ttu-id="7c991-112">如上所示，使用 API 建立的大多数 Fluent“对话”首先都会针对所要处理的 Azure 资源选择适当的资源集合。</span><span class="sxs-lookup"><span data-stu-id="7c991-112">As seen above, most fluent "conversations" you have with the API start with selecting the appropriate resource collection for the Azure resources you need to work with.</span></span>  <span data-ttu-id="7c991-113">然后，Intellisense in Visual Studio 会引导你完成对话。</span><span class="sxs-lookup"><span data-stu-id="7c991-113">Intellisense in Visual Studio then guides you through the conversation.</span></span> 

![驱动 Fluent 对话的 Intellisense in Visual Studio 的 GIF](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a><span data-ttu-id="7c991-115">列表和迭代</span><span class="sxs-lookup"><span data-stu-id="7c991-115">Lists and iterations</span></span>

<span data-ttu-id="7c991-116">每个资源集合提供一个 `List()` 方法来返回当前订阅中该资源的每个实例。</span><span class="sxs-lookup"><span data-stu-id="7c991-116">Every resource collection has a `List()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="7c991-117">例如，`Azure.SqlServers.List()` 返回订阅中的所有 SQL 服务器。</span><span class="sxs-lookup"><span data-stu-id="7c991-117">For example, `Azure.SqlServers.List()` returns all SQL servers in the subscription.</span></span>

<span data-ttu-id="7c991-118">使用 `ListByResourceGroup()` 方法可将返回列表的范围限定为特定的 [Azure 资源组](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="7c991-118">Use the `ListByResourceGroup()` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="7c991-119">可以像执行普通的 `List<T>` 一样循环访问返回的集合：</span><span class="sxs-lookup"><span data-stu-id="7c991-119">Iterate over the returned collection just as you would a normal `List<T>`:</span></span>

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a><span data-ttu-id="7c991-120">可操作的谓词</span><span class="sxs-lookup"><span data-stu-id="7c991-120">Actionable verbs</span></span>

<span data-ttu-id="7c991-121">名称中包含谓词的资源集合方法在 Azure 中立即执行。</span><span class="sxs-lookup"><span data-stu-id="7c991-121">Resource collection methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="7c991-122">这些方法以同步方式工作，在完成之前会阻塞当前线程中的执行。</span><span class="sxs-lookup"><span data-stu-id="7c991-122">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="7c991-123">Verb</span><span class="sxs-lookup"><span data-stu-id="7c991-123">Verb</span></span>   |  <span data-ttu-id="7c991-124">示例用法</span><span class="sxs-lookup"><span data-stu-id="7c991-124">Sample usage</span></span> |
|--------|---------------|
| <span data-ttu-id="7c991-125">创建</span><span class="sxs-lookup"><span data-stu-id="7c991-125">Create</span></span> | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| <span data-ttu-id="7c991-126">应用</span><span class="sxs-lookup"><span data-stu-id="7c991-126">Apply</span></span>  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| <span data-ttu-id="7c991-127">删除</span><span class="sxs-lookup"><span data-stu-id="7c991-127">Delete</span></span> | `azure.Disks.DeleteById(id)` | 
| <span data-ttu-id="7c991-128">列出</span><span class="sxs-lookup"><span data-stu-id="7c991-128">List</span></span>   | `azure.SqlServers.List()` | 
| <span data-ttu-id="7c991-129">Get</span><span class="sxs-lookup"><span data-stu-id="7c991-129">Get</span></span>    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="7c991-130">`Define()` 和 `Update()` 是谓词，但除非后接 `Create()` 或 `Apply()`，否则不会阻塞。</span><span class="sxs-lookup"><span data-stu-id="7c991-130">`Define()` and `Update()` are verbs but do not block unless followed by a `Create()` or `Apply()`.</span></span>
 
<span data-ttu-id="7c991-131">特定的资源对象包含可更改 Azure 中资源状态的谓词。</span><span class="sxs-lookup"><span data-stu-id="7c991-131">Specific resource objects have verbs that change the state of the resource in Azure.</span></span> <span data-ttu-id="7c991-132">例如：</span><span class="sxs-lookup"><span data-stu-id="7c991-132">For example:</span></span>

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

<span data-ttu-id="7c991-133">本部分中所述的大多数方法也具有异步版本（以 `Async` 后缀表示）。</span><span class="sxs-lookup"><span data-stu-id="7c991-133">Most of the methods described in this section have an asynchronous version as well, denoted by the suffix `Async`.</span></span>

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a><span data-ttu-id="7c991-134">延缓资源创建</span><span class="sxs-lookup"><span data-stu-id="7c991-134">Lazy resource creation</span></span>

<span data-ttu-id="7c991-135">如果某个新资源依赖于尚不存在的另一个资源，创建 Azure 资源时会出现难题。</span><span class="sxs-lookup"><span data-stu-id="7c991-135">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="7c991-136">例如，在创建新虚拟机时保留公共 IP 地址和设置磁盘。</span><span class="sxs-lookup"><span data-stu-id="7c991-136">An example is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="7c991-137">我们不需要确认是否保留了地址或创建了磁盘，而只需使用这些资源配置虚拟机。</span><span class="sxs-lookup"><span data-stu-id="7c991-137">You don't want to verify reserving the address or the creating the disk, you just want to configure the virtual machine with those resources.</span></span>

<span data-ttu-id="7c991-138">使用可创建对象可以定义要在代码中使用的 Azure 资源，但仅当需要在 Azure 中使用时才创建这些资源。</span><span class="sxs-lookup"><span data-stu-id="7c991-138">Use creatable objects to define Azure resources for use in your code but only create them when needed in Azure.</span></span> <span data-ttu-id="7c991-139">使用可创建对象编写的代码可将 Azure 环境中的资源创建过程卸载到管理 API，从而大幅提升性能。</span><span class="sxs-lookup"><span data-stu-id="7c991-139">Code written with creatable objects offloads resource creation in the Azure environment to the management API, boosting performance.</span></span> 

<span data-ttu-id="7c991-140">通过资源集合的不带 `Create()` 谓词的 `Define()` 谓词生成可创建对象：</span><span class="sxs-lookup"><span data-stu-id="7c991-140">Generate creatable objects through the resource collections' `Define()` verb without a `Create()` verb:</span></span>

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

<span data-ttu-id="7c991-141">可创建对象定义的 Azure 资源尚不在订阅中存在。</span><span class="sxs-lookup"><span data-stu-id="7c991-141">The Azure resource defined by the creatable object does not yet exist in your subscription.</span></span> <span data-ttu-id="7c991-142">可创建对象是管理 API 根据需要（调用 `.Create()` 时）创建的资源的本地表示形式。</span><span class="sxs-lookup"><span data-stu-id="7c991-142">A creatable object is a local representation of a resource that the management API will create when it's needed (when `.Create()` is called).</span></span> <span data-ttu-id="7c991-143">可以在需要此资源的其他 Azure 资源的定义中使用此可创建对象。</span><span class="sxs-lookup"><span data-stu-id="7c991-143">Use this creatable object in the definition of other Azure resources that need this resource.</span></span> 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

<span data-ttu-id="7c991-144">使用资源集合的 `Create()` 方法在 Azure 订阅中创建资源。</span><span class="sxs-lookup"><span data-stu-id="7c991-144">Create the resources in your Azure subscription using the `Create()` method for the resource collection.</span></span> 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

<span data-ttu-id="7c991-145">将可创建对象传递给 `Create()` 会返回 `ICreatedResources` 对象而非单个资源对象。</span><span class="sxs-lookup"><span data-stu-id="7c991-145">Passing creatable objects to `Create()` returns a `ICreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="7c991-146">使用 `CreatedRelatedResource` 对象可以访问 `Create()` 调用创建的所有资源，而不仅仅是资源集合中的类型。</span><span class="sxs-lookup"><span data-stu-id="7c991-146">The `CreatedRelatedResource` object lets you access all resources created by the `Create()` call, not just the type from the resource collection.</span></span> <span data-ttu-id="7c991-147">访问 Azure 中针对上述示例中创建的虚拟机所创建的公共 IP 地址：</span><span class="sxs-lookup"><span data-stu-id="7c991-147">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a><span data-ttu-id="7c991-148">异常处理</span><span class="sxs-lookup"><span data-stu-id="7c991-148">Exception handling</span></span>

<span data-ttu-id="7c991-149">管理 API 可定义用于扩展 `Microsoft.Rest.RestException` 的异常类。</span><span class="sxs-lookup"><span data-stu-id="7c991-149">The management API defines exception classes that extend `Microsoft.Rest.RestException`.</span></span> <span data-ttu-id="7c991-150">在相关的 `try` 语句后面使用 `catch (RestException exception)` 块捕获管理 API 生成的异常。</span><span class="sxs-lookup"><span data-stu-id="7c991-150">Catch exceptions generated by management API, with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-tracing"></a><span data-ttu-id="7c991-151">日志和跟踪</span><span class="sxs-lookup"><span data-stu-id="7c991-151">Logs and tracing</span></span>

<span data-ttu-id="7c991-152">用于 .NET 的 Fluent Azure 管理库中的日志记录利用基础 [AutoRest](https://github.com/Azure/AutoRest) 服务客户端跟踪。</span><span class="sxs-lookup"><span data-stu-id="7c991-152">Logging in the fluent Azure management libraries for .NET leverages the underlying [AutoRest](https://github.com/Azure/AutoRest) service client tracing.</span></span>

<span data-ttu-id="7c991-153">创建用于实现 `Microsoft.Rest.IServiceClientTracingInterceptor` 的类。</span><span class="sxs-lookup"><span data-stu-id="7c991-153">Create a class that implements `Microsoft.Rest.IServiceClientTracingInterceptor`.</span></span>  <span data-ttu-id="7c991-154">此类负责截获日志消息并将其传递给所用的任何日志记录机制。</span><span class="sxs-lookup"><span data-stu-id="7c991-154">This class will be responsible for intercepting log messages and passing them to whatever logging mechanism you're using.</span></span>  <span data-ttu-id="7c991-155">在此示例中，我们只需将消息写入控制台，但也可将其传递给 Log4Net、`Microsoft.Extensions.Logging` 或其他任何日志记录框架。</span><span class="sxs-lookup"><span data-stu-id="7c991-155">In this example, we're just writing messages to the console, but you could also pass them to Log4Net, `Microsoft.Extensions.Logging`, or any other logging framework.</span></span>

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

<span data-ttu-id="7c991-156">在创建 `Microsoft.Azure.Management.Fluent.Azure` 对象之前，请通过调用 `ServiceClientTracing.AddTracingInterceptor()` 来初始化上面创建的 `IServiceClientTracingInterceptor`，并将 `ServiceClientTracing.IsEnabled` 设置为 *true*。</span><span class="sxs-lookup"><span data-stu-id="7c991-156">Before creating the `Microsoft.Azure.Management.Fluent.Azure` object, initialize the `IServiceClientTracingInterceptor` you created above by calling `ServiceClientTracing.AddTracingInterceptor()` and set `ServiceClientTracing.IsEnabled` to *true*.</span></span>  <span data-ttu-id="7c991-157">创建 `Azure` 对象时，请包含 `.WithDelegatingHandler()` 和 `.WithLogLevel()` 方法，将客户端连接到 AutoRest 的服务客户端跟踪。</span><span class="sxs-lookup"><span data-stu-id="7c991-157">When you create the `Azure` object, include the `.WithDelegatingHandler()` and `.WithLogLevel()` methods to wire up the client to AutoRest's service client tracing.</span></span>

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

<span data-ttu-id="7c991-158">按如下所述定义 `HttpLoggingDelegatingHandler` 日志级别：</span><span class="sxs-lookup"><span data-stu-id="7c991-158">The `HttpLoggingDelegatingHandler` log levels are defined as follows:</span></span>

| <span data-ttu-id="7c991-159">跟踪级别</span><span class="sxs-lookup"><span data-stu-id="7c991-159">Trace level</span></span> | <span data-ttu-id="7c991-160">日志记录已启用</span><span class="sxs-lookup"><span data-stu-id="7c991-160">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="7c991-161">HttpLoggingDelegatingHandler.Level.None</span><span class="sxs-lookup"><span data-stu-id="7c991-161">HttpLoggingDelegatingHandler.Level.None</span></span> | <span data-ttu-id="7c991-162">无输出</span><span class="sxs-lookup"><span data-stu-id="7c991-162">No output</span></span>
| <span data-ttu-id="7c991-163">HttpLoggingDelegatingHandler.Level.Basic</span><span class="sxs-lookup"><span data-stu-id="7c991-163">HttpLoggingDelegatingHandler.Level.Basic</span></span> | <span data-ttu-id="7c991-164">记录基础 REST 调用的 URL、响应代码和时间</span><span class="sxs-lookup"><span data-stu-id="7c991-164">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="7c991-165">HttpLoggingDelegatingHandler.Level.Body</span><span class="sxs-lookup"><span data-stu-id="7c991-165">HttpLoggingDelegatingHandler.Level.Body</span></span> | <span data-ttu-id="7c991-166">Basic 中的所有内容，加上 REST 调用的请求和响应正文</span><span class="sxs-lookup"><span data-stu-id="7c991-166">Everything in Basic plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="7c991-167">HttpLoggingDelegatingHandler.Level.Headers</span><span class="sxs-lookup"><span data-stu-id="7c991-167">HttpLoggingDelegatingHandler.Level.Headers</span></span> | <span data-ttu-id="7c991-168">Basic 中的所有内容，加上请求和响应标头 REST 调用</span><span class="sxs-lookup"><span data-stu-id="7c991-168">Everything in Basic plus the request and response headers REST calls</span></span>
| <span data-ttu-id="7c991-169">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span><span class="sxs-lookup"><span data-stu-id="7c991-169">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span></span> | <span data-ttu-id="7c991-170">Body 和 Headers 日志级别中的所有内容</span><span class="sxs-lookup"><span data-stu-id="7c991-170">Everything in both Body and Headers log level</span></span>
