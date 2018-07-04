若要使用用于 .NET 的 Azure 管理库，.NET 应用程序需要拥有在 Azure 订阅中读取和创建资源的权限。 创建一个服务主体，并将应用配置为使用该服务主体的凭据运行，以授予此访问权限。 通过服务主体可以创建一个与用户标识关联的非交互式帐户，该帐户仅拥有运行应用所需的特权。

首先登录到 Azure PowerShell：

```powershell
Login-AzureRmAccount
```

记下有关租户和订阅的显示信息：

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

[使用 PowerShell 创建服务主体](/powershell/azure/create-azure-service-principal-azureps)，如下所示。 

> [!NOTE]
> 如果下面的 `New-AzureRmADServicePrincipal` cmdlet 返回“Another object with the same value for property identifierUris already exists”，那么你的租户中已存在具有该名称的服务主体。 请将其他值用于 **DisplayName** 参数。 

```powershell
# Create the service principal (use a strong password)
$cred = Get-Credential
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password $cred.Password

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

请务必记下 ApplicationId：

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
