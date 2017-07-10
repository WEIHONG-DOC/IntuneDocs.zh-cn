---
title: "如何使用 Azure AD 访问 Intune Graph API"
description: "描述应用使用 Azure AD 访问 Intune Graph API 所需的步骤"
keywords: "Intune graphapi c# powershell 权限角色"
author: lleonard-msft
manager: angrobe
ms.author: alleonar
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 79A67342-C06D-4D20-A447-678A6CB8D70A
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 6f2f0b610b900bb41a3c2bd7416b6db28434a155
ms.openlocfilehash: 64b476151d03978f30e15ab1743ae6e63d7a69ff
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="how-to-use-azure-ad-to-access-the-intune-graph-api"></a>如何使用 Azure AD 访问 Intune Graph API

[Microsoft Graph API](https://developer.microsoft.com/en-us/graph/) 现在支持具有特定 API 和权限角色的 Microsoft Intune。  Graph API 使用 Azure Active Directory (Azure AD) 进行身份验证和访问控制。  
对 Intune Graph API 的访问要求：

- 应用程序 ID 需要具有：

    - 调用 Azure AD 和 Graph ApI 的权限。
    - 与具体应用程序任务相关的权限范围。

- 用户凭据需要具有：

    - 访问与应用程序关联的 Azure AD 租户的权限。
    - 支持应用程序权限范围所需的角色权限。

- 授予应用权限以为其 Azure 租户执行应用程序任务的最终用户。

本文：

- 说明如何注册一个可以访问 Graph API 和相关权限角色的应用程序。

- 描述 Intune Graph API 权限角色。

- 提供 C# 和 PowerShell 的 Intune Graph API 身份验证示例。

- 描述如何支持多个租户 

若要了解更多信息，请参阅以下文章：

- [授权使用 OAuth 2.0 和 Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-protocols-oauth-code) 访问 Web 应用程序
- [Azure AD 身份验证入门](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/oauth)
- [将应用程序与 Azure Active Directory 集成](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)
- [了解 OAuth 2.0](https://oauth.net/2/)

## <a name="register-apps-to-use-graph-api"></a>注册应用以使用 Graph API

若要注册应用以使用 Graph API，请执行以下操作：

1.  使用管理凭据登录到 [Azure 门户](https://portal.azure.com)。

    根据需要可以使用：
    - 租户管理员帐户。
    - 启用了**用户可以注册应用程序**设置的租户用户帐户。

2.  从菜单中依次选择“Azure Active Directory”&gt;“应用注册”。

    <img src="./media/app-registration-manage.png" width="239" height="276" alt="The App registrations menu command" />

3.  选择“新应用程序注册”，以创建新的应用程序，或选择现有应用程序。  （如果你选择现有应用程序，请跳过下一步。）

4.  在“创建”边栏选项卡上，指定下列信息： 

    1.  应用程序的**名称**（用户登录时显示）。

    2.  “应用程序类型”和“重定向 URI”值。

        这些信息会因要求的不同而异。 例如，如果你正在使用 Azure AD [Authentication Library](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-libraries) (ADAL)，请将“应用程序类型”设置为 `Native`，将“重定向 URI”设置为 `urn:ietf:wg:oauth:2.0:oob`。

        <img src="media/app-registration-redirect.png" width="355" height="232" alt="The Redirect URI value" />

        要了解详细信息，请参阅 [Azure AD 的身份验证方案息](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios)。

5.  从应用程序边栏选项卡：

    1.  注意“应用程序 ID”值。

    2.  选择“设置”&gt;“API 访问”&gt;“所需权限”。

    <img src="media/app-registration-req-perms.png" width="554" height="217" alt="The Required permissions setting" />

6.  从“所需权限”边栏选项卡中，选择“添加”&gt;“添加 API 访问权限”&gt;“选择 API”。

    <img src="media/app-registration-graph-api.png" width="558" height="165" alt="The Microsoft Graph setting" />

7.  从“选择 API”边栏选项卡中，依次选择“Microsoft Graph”&gt;“选择”。  打开“启用访问权限”边栏选项卡，并列出你的应用程序可用的权限范围。

    <img src="media/aad-auth-role-permissions.png" width="479" height="293" alt="Intune Graph API permission scopes" />

    通过在相关名称的左侧打一个复选标记来选择应用所需的角色。  要了解具体的 Intune 权限范围，请参阅 [Intune 权限范围](#user-content-intune-permission-scopes)。  要了解其他 Graph API 权限范围，请参阅 [Microsoft Graph 权限引用](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference)。

    为获得最佳效果，请选择实现应用程序所需的最少角色。

    完成后，选择“选择”和“完成”保存更改。

此时，你也可以：

- 选择将权限授予所有租户帐户，以无需提供凭据即可使用该应用程序。  

    为此，请选择“授予权限”并接受确认提示。

    第一次运行应用程序时，系统会提示你授予应用程序执行所选角色的权限。

    <img src="media/app-registration-grant-perms.png" width="512" height="232" alt="The Grant permissions button" />

- 使应用可供租户之外的用户使用。  （这通常仅适用于支持多个租户/组织的合作伙伴。）  

    为此，请执行以下操作：

    1. 从应用程序边栏选项卡中选择“清单”，将打开“编辑清单”边栏选项卡。

    <img src="media/app-registration-other-tenants.png" width="531" height="168" alt="The Edit manifest blade" />

    2. 将 `availableToOtherTenants` 设置的值更改为 `true`。

    3. 保存你的更改。

## <a name="intune-permission-scopes"></a>Intune 权限范围

Azure AD 和 Graph API 使用权限范围来控制对公司资源的访问。  

权限范围（也称为 _OAuth 范围_）控制对特定 Intune 实体及其属性的访问权限。 本节概要总结了 Intune Graph API 功能的权限范围。

若要了解更多信息，请参阅以下内容：
- [Azure AD 身份验证](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication)
- [应用程序权限范围](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)

当向 Graph API 授予权限时，你可以指定以下范围来控制对 Intune 功能的访问权限：下表总结了 Intune Graph API 权限范围。  第一列显示 Azure 门户中显示的功能名称，第二列显示权限范围名称。

_启用访问权限_设置 | 作用域名称
:--|:--
__在 Microsoft Intune 设备上执行影响用户的远程操作（预览）__ | [DeviceManagementManagedDevices.PrivilegedOperations.All](#user-content-mgd-po)
__读取和写入 Microsoft Intune 设备（预览）__ | [DeviceManagementManagedDevices.ReadWrite.All](#mgd-rw)
__Microsoft Intune 设备（预览）__ | [DeviceManagementManagedDevices.Read.All](#mgd-ro)
__读取和写入 Microsoft Intune RBAC 设置（预览）__ | [DeviceManagementRBAC.ReadWrite.All](#rac-rw)
__读取 Microsoft Intune RBAC 设置（预览）__ | [DeviceManagementRBAC.Read.All](#rac=ro)
__读取和写入 Microsoft Intune 应用（预览）__ | [DeviceManagementApps.ReadWrite.All](#app-rw)
__读取 Microsoft Intune 应用（预览）__ | [DeviceManagementApps.Read.All](#app-ro)
__读取和写入 Microsoft Intune 设备配置和策略（预览）__ | [DeviceManagementConfiguration.ReadWrite.All](#cfg-rw)
__读取和写入 Microsoft Intune 设备配置和策略（预览）__ | [DeviceManagementConfiguration.Read.All](#cfg-ro)
__读取和写入 Microsoft Intune 配置（预览）__ | [DeviceManagementServiceConfiguration.ReadWrite.All](#svc-rw)
__读取 Microsoft Intune 配置（预览）__ | [DeviceManagementServiceConfiguration.Read.All](#svc-ra)

该表按照设置在 Azure 门户中的显示顺序进行列示。 以下部分按字母顺序描述范围。

此时，所有 Intune 权限范围都需要管理员访问权限。  这意味着在运行访问 Intune Graph API 资源的应用或脚本时需要相应的凭据。

### <a name="app-ro"></a>DeviceManagementApps.Read.All

- **启用访问权限**设置：__读取 Microsoft Intune 应用（预览）__

- 允许对以下实体属性和状态执行读取访问权限：
    - Mobile Apps
    - 移动应用类别
    - 应用保护策略
    - 应用配置

### <a name="app-rw"></a>DeviceManagementApps.ReadWrite.All

- **启用访问权限**设置：__读取和写入 Microsoft Intune 应用（预览）__

- 允许与 __DeviceManagementApps.Read.All__ 相同的操作

- 此外，允许对以下实体作出更改：

    - Mobile Apps
    - 移动应用类别
    - 应用保护策略
    - 应用配置

### <a name="cfg-ro"></a>DeviceManagementConfiguration.Read.All

- **启用访问权限**设置：__读取 Microsoft Intune 设备配置和策略（预览）__

- 允许对以下实体属性和状态执行读取访问权限：
    - 设备配置
    - 设备符合性策略
    - 通知消息

### <a name="cfg-ra"></a>DeviceManagementConfiguration.ReadWrite.All

- **启用访问权限**设置：__读取和写入 Microsoft Intune 设备配置和策略（预览）__

- 允许与 __DeviceManagementConfiguration.Read.All__ 相同的操作

- 应用还可以创建、分配、删除和更改以下实体：
    - 设备配置
    - 设备符合性策略
    - 通知消息

### <a name="mgd-po"></a>DeviceManagementManagedDevices.PrivilegedOperations.All

- **启用访问权限**设置：__对 Microsoft Intune 设备执行影响用户的远程操作（预览）__

- 允许对受管理设备执行下列远程操作：
    - 停用
    - 擦除
    - 重置/恢复密码
    - 远程锁定
    - 禁用/启用丢失模式
    - 清理电脑
    - 重新启动
    - 从共享设备删除用户

### <a name="mgd-ro"></a>DeviceManagementManagedDevices.Read.All

- **启用访问权限**设置：__读取和写入 Microsoft Intune 设备（预览）__

- 允许对以下实体属性和状态执行读取访问权限：
    - 受管理设备
    - 设备类别
    - 检测到的应用
    - 远程操作
    - 恶意软件信息

### <a name="mgd-rw"></a>DeviceManagementManagedDevices.ReadWrite.All

- **启用访问权限**设置：__读取和写入 Microsoft Intune 设备（预览）__

- 允许与 __DeviceManagementManagedDevices.Read.All__ 相同的操作

- 应用还可以创建、删除和更改以下实体：
    - 受管理设备
    - 设备类别

- 此外，还将允许以下远程操作：
    - 定位设备
    - 绕过激活锁定
    - 请求远程协助

### <a name="rac-ro"></a>DeviceManagementRBAC.Read.All

- **启用访问权限**设置：__读取 Microsoft Intune RBAC 设置（预览）__

- 允许对以下实体属性和状态执行读取访问权限：
    - 角色分配
    - 角色定义
    - 资源操作

### <a name="rac-rw"></a>DeviceManagementRBAC.ReadWrite.All

- **启用访问权限**设置：__读取和写入 Microsoft Intune RBAC 设置（预览）__

- 允许与 __DeviceManagementRBAC.Read.All__ 相同的操作

- 应用还可以创建、分配、删除和更改以下实体：
    - 角色分配
    - 角色定义

### <a name="svc-ro"></a>DeviceManagementServiceConfiguration.Read.All

- **启用访问权限**设置：__读取 Microsoft Intune 配置（预览）__

- 允许对以下实体属性和状态执行读取访问权限：
    - 设备注册
    - Apple Push Notification 证书
    - Apple 设备注册计划
    - Apple Volume Purchase Program
    - Exchange Connector
    - 条款和条件
    - 电信支出管理
    - 云 PKI
    - 品牌打造
    - 移动威胁防御

### <a name="svc-rw"></a>DeviceManagementServiceConfiguration.ReadWrite.All

- **启用访问权限**设置：__读取和写入 Microsoft Intune 配置（预览）__

- 允许与 DeviceManagementServiceConfiguration.Read.All_ 相同的操作

- 此外，应用还可以配置以下 Intune 功能：
    - 设备注册
    - Apple Push Notification 证书
    - Apple 设备注册计划
    - Apple Volume Purchase Program
    - Exchange Connector
    - 条款和条件
    - 电信支出管理
    - 云 PKI
    - 品牌打造
    - 移动威胁防御

## <a name="azure-ad-authentication-examples"></a>Azure AD 身份验证示例

本节介绍如何将 Azure AD 纳入到 C# 和 PowerShell 项目中。

在每个示例中，将需要指定至少一个具有 `DeviceManagementManagedDevices.Read.All` 权限范围（前面讨论过）的应用程序 ID。

测试任一示例时，可能会收到类似下面所示的 HTTP 状态 403（禁止）错误： 

``` javascript
{
  "error": {
    "code": "Forbidden",
    "message": "Application is not authorized to perform this operation - Operation ID " + 
       "(for customer support): 00000000-0000-0000-0000-000000000000 - " + 
       "Activity ID: cc7fa3b3-bb25-420b-bfb2-1498e598ba43 - " + 
       "Url: https://example.manage.microsoft.com/" + 
       "Service/Resource/RESTendpoint?" + 
       "api-version=2017-03-06 - CustomApiErrorPhrase: ",
    "innerError": {
      "request-id": "00000000-0000-0000-0000-000000000000",
      "date": "1980-01-0112:00:00"
    }
  }
}
```

如果发生这种情况，请验证：

- 你是否已将应用程序 ID 更新为经授权使用 Graph API 和 `DeviceManagementManagedDevices.Read.All` 权限范围的应用程序 ID。

- 租户凭据是否支持管理功能。

- 你的代码是否与显示的示例类似。 


### <a name="authenticate-azure-ad-in-c"></a>在 C\# 中验证 Azure AD

此示例说明如何使用 C# 检索与 Intune 帐户关联的设备列表。 

1.  启动 Visual Studio，然后创建新的 Visual C# 控制台应用（.net 框架）项目。 

2.  输入项目的名称，并根据需要提供其他详细信息。

    <img src="media/aad-auth-cpp-new-console.png" width="624" height="433" alt="Creating a C# console app project in Visual Studio"  />

3.  使用解决方案资源管理器将 Microsoft ADAL NuGet 包添加到项目中。

    1.  右键单击解决方案资源管理器。
    2.  选择“管理 NuGet 程序包...” &gt;“浏览”。
    3.  选择 `Microsoft.IdentityModel.Clients.ActiveDirectory`，然后选择“安装”。

    <img src="media/aad-auth-cpp-install-package.png" width="624" height="458" alt="Selecting the Azure AD identity model module" />

4.  在 Program.cs 顶部添加以下语句：

    ``` csharp
    using Microsoft.IdentityModel.Clients.ActiveDirectory;</p>
    using System.Net.Http;
    ```

5.  添加一个方法以创建授权标头：

    ``` csharp
    private static async Task<string> GetAuthorizationHeader()
    {
        string applicationId = "<Your Application ID>";
        string authority = "https://login.microsoftonline.com/common/";
        Uri redirectUri = new Uri("urn:ietf:wg:oauth:2.0:oob");
        AuthenticationContext context = new AuthenticationContext(authority);
        AuthenticationResult result = await context.AcquireTokenAsync(
            "https://graph.microsoft.com", 
            applicationId, redirectUri,
            new PlatformParameters(PromptBehavior.Auto));
        return result.CreateAuthorizationHeader();
    ```

    记住要更改 `application_ID` 的值，以匹配至少授予 `DeviceManagementManagedDevices.Read.All` 权限范围的值，如前所述。

6. 添加方法以检索设备列表：

    ``` csharp
    private static async Task<string> GetMyManagedDevices()
    {
        string authHeader = await GetAuthorizationHeader();
        HttpClient graphClient = new HttpClient();
        graphClient.DefaultRequestHeaders.Add("Authorization", authHeader);
        return await graphClient.GetStringAsync(
            "https://graph.microsoft.com/beta/me/managedDevices");
    }
    ```

7.  更新 **Main** 以调用 **GetMyManagedDevices**：

    ``` csharp
    string devices = GetMyManagedDevices().GetAwaiter().GetResult();
    Console.WriteLine(devices);
    ```

8.  编译并运行程序。  

第一次运行程序时，应该会收到两个提示。  第一个提示请求凭据，第二个提示授予 `managedDevices` 请求的权限。  

作为参考，下面是已完成的程序：

``` csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;
using System.Net.Http;
using System.Threading.Tasks;

namespace IntuneGraphExample
{
    class Program
    {
        static void Main(string[] args)
        {
            string devices = GetMyManagedDevices().GetAwaiter().GetResult();
            Console.WriteLine(devices);
        }

        private static async Task<string> GetAuthorizationHeader()
        {
            string applicationId = "<Your Application ID>";
            string authority = "https://login.microsoftonline.com/common/";
            Uri redirectUri = new Uri("urn:ietf:wg:oauth:2.0:oob");
            AuthenticationContext context = new AuthenticationContext(authority);
            AuthenticationResult result = await context.AcquireTokenAsync("https://graph.microsoft.com", applicationId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
            return result.CreateAuthorizationHeader();
        }

        private static async Task<string> GetMyManagedDevices()
        {
            string authHeader = await GetAuthorizationHeader();
            HttpClient graphClient = new HttpClient();
            graphClient.DefaultRequestHeaders.Add("Authorization", authHeader);
            return await graphClient.GetStringAsync("https://graph.microsoft.com/beta/me/managedDevices");
        }
    }
}
```

### <a name="authenticate-azure-ad-powershell"></a>验证 Azure AD (PowerShell)

以下 PowerShell 脚本使用 AzureAD PowerShell 模块进行身份验证。  要了解详细信息，请参阅 [Azure Active Directory PowerShell 版本 2](https://docs.microsoft.com/en-us/powershell/azure/install-adv2?view=azureadps-2.0) 和 [Intune PowerShell 示例](https://github.com/microsoftgraph/powershell-intune-samples)。

在此示例中，更新 `$clientID` 的值以匹配有效的应用程序 ID。

``` powershell
function Get-AuthToken {
    [cmdletbinding()]
    param
    (
        [Parameter(Mandatory = $true)]
        $User
    )

    $userUpn = New-Object "System.Net.Mail.MailAddress" -ArgumentList $User
    $tenant = $userUpn.Host
   
    Write-Host "Checking for AzureAD module..."

    $AadModule = Get-Module -Name "AzureAD" -ListAvailable
    if ($AadModule -eq $null) {
        Write-Host "AzureAD PowerShell module not found, looking for AzureADPreview"
        $AadModule = Get-Module -Name "AzureADPreview" -ListAvailable
    }

    if ($AadModule -eq $null) {
        write-host
        write-host "AzureAD Powershell module not installed..." -f Red
        write-host "Install by running 'Install-Module AzureAD' or 'Install-Module AzureADPreview' from an elevated PowerShell prompt" -f Yellow
        write-host "Script can't continue..." -f Red
        write-host
        exit
    }

    # Getting path to ActiveDirectory Assemblies
    # If the module count is greater than 1 find the latest version

    if ($AadModule.count -gt 1) {
        $Latest_Version = ($AadModule | select version | Sort-Object)[-1]
        $aadModule = $AadModule | ? { $_.version -eq $Latest_Version.version }
        $adal = Join-Path $AadModule.ModuleBase "Microsoft.IdentityModel.Clients.ActiveDirectory.dll"
        $adalforms = Join-Path $AadModule.ModuleBase "Microsoft.IdentityModel.Clients.ActiveDirectory.Platform.dll"
    }

    else {
        $adal = Join-Path $AadModule.ModuleBase "Microsoft.IdentityModel.Clients.ActiveDirectory.dll"
        $adalforms = Join-Path $AadModule.ModuleBase "Microsoft.IdentityModel.Clients.ActiveDirectory.Platform.dll"
    }

    [System.Reflection.Assembly]::LoadFrom($adal) | Out-Null
    [System.Reflection.Assembly]::LoadFrom($adalforms) | Out-Null

    $clientId = "<Your Application ID>"
    $redirectUri = "urn:ietf:wg:oauth:2.0:oob"
    $resourceAppIdURI = "https://graph.microsoft.com"
    $authority = "https://login.microsoftonline.com/$Tenant"
     
    try {
        $authContext = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext" -ArgumentList $authority
        # https://msdn.microsoft.com/library/azure/microsoft.identitymodel.clients.activedirectory.promptbehavior.aspx
        # Change the prompt behaviour to force credentials each time: Auto, Always, Never, RefreshSession
        $platformParameters = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.PlatformParameters" -ArgumentList "Auto"
        $userId = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.UserIdentifier" -ArgumentList ($User, "OptionalDisplayableId")
        $authResult = $authContext.AcquireTokenAsync($resourceAppIdURI, $clientId, $redirectUri, $platformParameters, $userId).Result
        # If the accesstoken is valid then create the authentication header
        if ($authResult.AccessToken) {
            # Creating header for Authorization token
            $authHeader = @{
                'Content-Type' = 'application/json'
                'Authorization' = "Bearer " + $authResult.AccessToken
                'ExpiresOn' = $authResult.ExpiresOn
            }
            return $authHeader
        }
        else {
            Write-Host
            Write-Host "Authorization Access Token is null, please re-run authentication..." -ForegroundColor Red
            Write-Host
            break
        }
    }
    catch {
        write-host $_.Exception.Message -f Red
        write-host $_.Exception.ItemName -f Red
        write-host
        break
    }   
}

$authToken = Get-AuthToken -User "<Your AAD Username>"

try {
    $uri = "https://graph.microsoft.com/beta/me/managedDevices"
    Write-Verbose $uri
    (Invoke-RestMethod -Uri $uri –Headers $authToken –Method Get).Value
}
catch {
    $ex = $_.Exception
    $errorResponse = $ex.Response.GetResponseStream()
    $reader = New-Object System.IO.StreamReader($errorResponse)
    $reader.BaseStream.Position = 0
    $reader.DiscardBufferedData()
    $responseBody = $reader.ReadToEnd();
    Write-Host "Response content:`n$responseBody" -f Red
    Write-Error "Request to $Uri failed with HTTP Status $($ex.Response.StatusCode) $($ex.Response.StatusDescription)"
    write-host
    break
}
```

## <a name="support-multiple-tenants-and-partners"></a>支持多个租户和合作伙伴

如果组织支持拥有自己的 Azure AD 租户的组织，你可能需要允许客户与其各自的租户一起使用你的应用程序。

为此，请执行以下操作：

1.  验证客户帐户是否存在于目标 Azure AD 租户中。

2.  验证租户帐户是否允许用户注册应用程序（请参阅**用户设置**）。

3.  建立每个租户之间的关系。  

    为此，请执行以下操作之一：

    a. 使用 [Microsoft 合作伙伴中心](https://partnercenter.microsoft.com/)定义与客户及其电子邮件地址的关系。

    b. 邀请用户成为租户的来宾。

若需邀请用户成为租户的来宾，请执行以下操作：

1.  从“快速任务”面板选择“添加来宾用户”。

    <img src="media/aad-multiple-tenant-add-user.png" width="559" height="166" alt="Use Quick Tasks to add a guest user" />

2.  输入客户的电子邮件地址并添加个性化邮件进行邀请（可选）。

    <img src="media/aad-multiple-tenant-invite-guest.png" width="508" height="373" alt="Inviting an external user as a guest" />

3.  选择“邀请”。

此操作将会向用户发送一个邀请。

   <img src="media/aad-multiple-tenant-invitation.png" width="624" height="523" alt="A sample guest invitation" />

   用户需要选择“开始使用”链接才能接受邀请。

关系建立（或邀请被接受）后，将用户帐户添加到“目录角色”。

请记住，根据需要将用户添加到其他角色。 例如，要允许用户管理 Intune 设置，他们需要成为“全局管理员”或“Intune 服务管理员”。

此外：

- 使用 http://portal.office.com 为用户帐户分配 Intune 许可证。

- 更新应用程序代码，以验证客户端的 Azure AD 租户域，而不是你自己的域。

    例如，假设你的租户域为 `contosopartner.onmicrosoft.com`，客户端租户域名为 `northwind.onmicrosoft.com`，则你将更新代码以对客户端租户进行身份验证。

    若要在基于前面示例的 C# 应用程序中执行此操作，你可以更改 `authority` 变量的值：

    ``` csharp
    string authority = "https://login.microsoftonline.com/common/";
    ```

    设置为

    ``` csharp
    string authority = "https://login.microsoftonline.com/northwind.onmicrosoft.com/";
    ```
