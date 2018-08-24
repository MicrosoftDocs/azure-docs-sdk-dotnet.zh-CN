若要使用用于 .NET 的 Azure 管理库，.NET 应用程序需要拥有在 Azure 订阅中读取和创建资源的权限。 创建一个服务主体，并将应用配置为使用该服务主体的凭据运行，以授予此访问权限。 通过服务主体可以创建一个与用户标识关联的非交互式帐户，该帐户仅拥有运行应用所需的特权。

首先登录到 [Azure Cloud Shell](https://shell.azure.com/bash)。 验证当前使用的是要在其中创建服务主体的订阅。 

```azurecli-interactive
az account show
```

此时将显示订阅信息。

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

如果尚未登录到正确的订阅，请通过键入 `az account set -s <name or ID of subscription>` 选择正确的订阅。

使用以下命令创建服务主体：

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

服务主体信息将以 JSON 格式显示。

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

将 JSON 输出复制并粘贴到文本编辑器中，供以后使用。
