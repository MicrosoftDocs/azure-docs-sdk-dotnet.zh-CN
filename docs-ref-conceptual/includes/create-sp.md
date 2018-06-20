<span data-ttu-id="3eab4-101">若要使用用于 .NET 的 Azure 管理库，.NET 应用程序需要拥有在 Azure 订阅中读取和创建资源的权限。</span><span class="sxs-lookup"><span data-stu-id="3eab4-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="3eab4-102">创建一个服务主体，并将应用配置为使用该服务主体的凭据运行，以授予此访问权限。</span><span class="sxs-lookup"><span data-stu-id="3eab4-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="3eab4-103">通过服务主体可以创建一个与标识关联的非交互式帐户，该帐户仅拥有运行应用所需的特权。</span><span class="sxs-lookup"><span data-stu-id="3eab4-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="3eab4-104">首先登录到 Azure PowerShell：</span><span class="sxs-lookup"><span data-stu-id="3eab4-104">First, login to Azure PowerShell:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3eab4-105">记下有关租户和订阅的显示信息：</span><span class="sxs-lookup"><span data-stu-id="3eab4-105">Note the information displayed about your tenant and subscription:</span></span>

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

<span data-ttu-id="3eab4-106">[使用 PowerShell 创建服务主体](/powershell/azure/create-azure-service-principal-azureps)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3eab4-106">[Create a service principal using PowerShell](/powershell/azure/create-azure-service-principal-azureps), like this:</span></span>

```powershell
# Create the service principal (use a strong password)
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password "password"

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

<span data-ttu-id="3eab4-107">请务必记下 ApplicationId：</span><span class="sxs-lookup"><span data-stu-id="3eab4-107">Make sure to note the ApplicationId:</span></span>

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
