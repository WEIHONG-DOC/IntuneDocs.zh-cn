---
title: "设备注册疑难解答"
titleSuffix: Intune Azure preview
description: "Intune Azure 预览版：了解如何排查设备注册问题。"
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: c324c74e-e225-40ad-88b7-72a6d9ea09b5
ms.reviewer: damionw
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 3084b7179a310a44c520dd42a8e194490dca90d8
ms.contentlocale: zh-cn
ms.lasthandoff: 05/23/2017


---

# <a name="troubleshoot-device-enrollment-in-intune"></a>排查 Intune 中的设备注册问题

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

本主题提供有关设备注册问题故障排除的建议。 如果此信息未解决你的问题，请参阅[如何获取对 Microsoft Intune 的支持](https://docs.microsoft.com/intune-classic/troubleshoot/get-support)，了解更多获得帮助的方法。


## <a name="initial-troubleshooting-steps"></a>初始故障排除步骤

开始故障排除之前，请确保已正确配置 Intune 以启用注册。 请参阅[注册 Android 和标准 Knox 设备](android-enroll.md)，获取针对每个平台的注册步骤的链接。

托管的设备用户可收集注册和诊断日志以供你查看。 以下提供了有关收集日志的用户说明：

- [将 Android 注册错误发送给 IT 管理员](https://docs.microsoft.com/intune-user-help/send-enrollment-errors-to-your-it-admin-android)
- [将 iOS 错误发送给 IT 管理员](https://docs.microsoft.com/intune-user-help/send-errors-to-your-it-admin-ios)

## <a name="general-enrollment-issues"></a>常规注册问题
所有设备平台上都可能发生这些问题。

### <a name="device-cap-reached"></a>已达到设备上限
**问题：**注册期间，用户在设备上收到一个错误，例如 iOS 设备上的“公司门户暂时不可用”错误，并且 Configuration Manager 上的 DMPdownloader.log 包含错误“DeviceCapReached”。

**解决方法：**

#### <a name="check-number-of-devices-enrolled-and-allowed"></a>检查已注册的和允许的设备数量

在 Azure 门户中，选择“更多服务” > “监视 + 管理” > “Intune”。 在 Azure 门户的 Intune 边栏选项卡上，转到“注册设备” > “注册限制”，并确认用户分配到的设备未超过 15 台的允许上限。

<!--- Mobile device users can delete devices at the following URL: [https://byodtestservice.azurewebsites.net/](https://byodtestservice.azurewebsites.net/). --->

管理员可以在 Azure Active Directory 门户中删除设备。

#### <a name="to-delete-devices-in-the-azure-active-directory-portal"></a>在 Azure Active Directory 门户中删除设备

1.  浏览到 [http://aka.ms/accessaad](http://aka.ms/accessaad) 或从 [https://portal.office.com](https://portal.office.com) 选择**管理**&gt; **Azure AD**。

2.  单击页面左侧的链接，使用组织 ID 登录。

3.  创建 Azure 订阅（如果没有）。 如果有付费帐户，应该不会要求提供信用卡或付款（请选择**注册免费的 Azure Active Directory**订阅链接）。

4.  选择“Active Directory”  ，然后选择你的组织。

5.  选择“用户”  选项卡。

6.  选择要删除其设备的用户。

7.  选择**设备**。

8.  根据需要删除设备，例如那些不再使用的设备或者定义不准确的设备。

> [!NOTE]

> 可通过使用设备注册管理器来避免达到设备注册上限，如[使用设备注册管理器注册设备](device-enrollment-manager-enroll.md)中所述。
>
> 如果对添加到设备注册管理器组的用户帐户强制实施条件访问策略，该特定用户登录将无法完成注册。

### <a name="company-portal-temporarily-unavailable"></a>公司门户暂时不可用
**问题：**用户的设备上收到“公司门户暂时不可用”错误。

**解决方法：**

1.  从设备中删除 Intune 公司门户应用。

2.  在设备上，打开浏览器，浏览到 [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com)，然后尝试用户登录。

3.  如果用户无法登录，则让他们尝试另一个网络。

4.  如果仍然失败，请确保用户的凭据已与 Azure Active Directory 正确同步。

5.  如果用户成功登录，iOS 设备将提示你安装 Intune 公司门户应用并注册。 在 Android 设备上，你需要手动安装 Intune 公司门户应用，之后才能重试注册。

### <a name="mdm-authority-not-defined"></a>未定义 MDM 机构
**问题：**用户收到“未定义 MDM 机构”错误。

**解决方法：**

1.  验证是否已针对使用的 Intune 服务类型（即 Intune、Office 365 或 System Center Configuration Manager with Intune）正确设置 MDM 机构。 请参阅[设置移动设备管理机构](mdm-authority-set.md)中的相关说明。

    > [!NOTE]
    > 设置 MDM 机构后，只能通过联系支持人员对其进行更改，如[如何获取对 Microsoft Intune 的支持](https://docs.microsoft.com/intune-classic/troubleshoot/get-support)中所述。

2.  确保该用户的凭据已与 Azure Active Directory 正确同步，方法是检查其 UPN 是否与帐户门户中的 Active Directory 信息匹配。
    如果 UPN 与 Active Directory 信息不匹配：

    1.  关闭本地服务器上的目录同步。

    2.  从“Intune 帐户门户”  用户列表中删除不匹配的用户。

    3.  等待大约一小时，让 Azure 服务删除不正确的数据。

    4.  再次打开目录同步，并检查该用户现在是否已正确同步。

3.  如果使用的是 System Center Configuration Manager with Intune，请确保该用户具有有效的云用户 ID：

    1.  打开 SQL Management Studio。

    2.  连接到相应的数据库。

    3.  打开数据库文件夹，找到并打开 **CM_DBName** 文件夹，其中 DBName 是客户数据库的名称。

    4.  在顶部选择**新建查询**并执行以下查询：

        -   查看所有用户：`select * from [CM_ DBName].[dbo].[User_DISC]`

        -   若要查看特定用户，请使用下面的查询，其中 %testuser1% 表示要查找的用户的 username@domain.com：`select * from [CM_ DBName].[dbo].[User_DISC] where User_Principal_Name0 like '%testuser1%'`

        编写查询后，选择**!执行**。
        返回结果后，即可查找云用户 ID。  如果找不到任何 ID，则表示未授权该用户使用 Intune。

### <a name="unable-to-create-policy-or-enroll-devices-if-the-company-name-contains-special-characters"></a>如果公司名称包含特殊字符，则无法创建策略或注册设备
**问题：**无法创建策略或注册设备。

**解决方法：**在 [Office 365 管理中心](https://portal.office.com/)，删除公司名称中的特殊字符并保存公司信息。

### <a name="unable-to-log-in-or-enroll-devices-when-you-have-multiple-verified-domains"></a>如果有多个已验证的域，则无法登录或注册设备
**问题：**向 ADFS 添加第二个已验证的域时，具有第二个域的用户主体名称 (UPN) 后缀的用户可能无法登录门户或注册设备。


**解决方法：**对于通过 AD FS 2.0 使用单一登录 (SSO) 且其组织中拥有用户 UPN 后缀的多个顶级域（如 @contoso.com 或 @fabrikam.com）的 Microsoft Office 365 客户，他们需要为每个后缀部署 AD FS 2.0 联合身份验证服务的一个单独实例。  现在有了 [AD FS 2.0 汇总](http://support.microsoft.com/kb/2607496)，其与**SupportMultipleDomain** 切换结合使用可启用 AD FS 服务器，以在无需其他 AD FS 2.0 服务器的情况下支持此方案。 有关详细信息，请参阅[此博客](https://blogs.technet.microsoft.com/abizerh/2013/02/05/supportmultipledomain-switch-when-managing-sso-to-office-365/)。


## <a name="android-issues"></a>Android 的问题
### <a name="devices-fail-to-check-in-with-the-intune-service-and-display-as-unhealthy-in-the-intune-admin-console"></a>设备无法签入 Intune 服务，并在 Intune 管理控制台中显示为“不正常”
**问题：**运行 Android 版本 4.4.x 和 5.x 的某些 Samsung 设备可能会停止签入 Intune 服务。 如果设备不签入：

- 它们将无法从 Intune 服务接收策略、应用和远程命令。
- 它们在管理控制台中显示的管理状态为“不正常”。
- 受条件访问策略保护的用户可能失去对公司资源的访问权限。

Samsung 已经确认 Samsung Smart Manager 软件（预装在某些 Samsung 设备上）会停用 Intune 公司门户及其组件。 当公司门户处于停用状态时，它无法在后台运行，因此无法联系 Intune 服务。

**解决方法 #1：**

告知你的用户手动启动公司门户应用。 应用重启后，设备将签入 Intune 服务。

> [!IMPORTANT]
> 手动打开公司门户应用只是一种临时解决方案，因为 Samsung Smart Manager 可能会再次停用公司门户应用。

**解决方法 #2：**

告知你的用户尝试升级到 Android 6.0。 停用问题不会发生在 Android 6.0 设备上。 若要检查是否有可用的更新，用户可以转到“设置” > “关于设备” > “手动下载更新”，然后按照设备上的提示进行操作。

**解决方法 #3：**

如果解决方案 #2 无效，请让你的用户按照以下步骤操作，使 Smart Manager 排除公司门户网站应用：

1. 在设备上启动 Smart Manager 应用。

  ![选择设备上的“Smart Manager”图标](./media/smart-manager-app-icon.png)

2. 选择“电池”磁贴。

  ![选择“电池”磁贴](./media/smart-manager-battery-tile.png)

3. 在“应用省电”或“应用优化”下，选择“详细信息”。

  ![在“应用省电”或“应用优化”下选择“详细信息”](./media/smart-manager-app-power-saving-detail.png)

4. 从应用列表中选择“公司门户”。

  ![从应用列表中选择“公司门户”](./media/smart-manager-company-portal.png)

5. 选择“关闭”。

  ![从“应用优化”对话框中选择“关闭”](./media/smart-manager-app-optimization-turned-off.png)

6. 在“应用省电”或“应用优化”下，确认公司门户已关闭。

  ![验证公司门户已关闭](./media/smart-manager-verify-comp-portal-turned-off.png)


### <a name="profile-installation-failed"></a>配置文件安装失败
**问题：**用户在 Android 设备上收到**配置文件安装失败**错误。

**解决方法：**

1.  确认针对你在使用的 Intune 服务版本，该用户分配有适当的许可证。

2.  确认尚未向另一个 MDM 提供程序注册该设备，或者该设备尚未安装管理配置文件。

3.  确认默认浏览器为适用于 Android 的 Chrome，并且已启用 Cookie。

### <a name="android-certificate-issues"></a>Android 证书问题

**问题**：用户在其设备上收到以下消息：*无法登录，因为设备缺少必需的证书。*

**解决方法 1**：

让用户按照[设备缺少必需的证书](https://docs.microsoft.com/intune-user-help/your-device-is-missing-a-required-certificate-landing-android#your-device-is-missing-a-certificate-required-by-your-it-administrator)中的说明操作。 如果用户按照此说明操作后仍出现此错误，请尝试解决方法 2。

**解决方法 2**：

如果用户输入其公司凭据并在联合登录体验中重定向后仍然看到缺少证书的错误，那么 Active Directory 联合服务 (AD FS) 服务器可能缺失中间证书。

此证书错误的发生是因为 Android 设备需要在 [SSL 服务器问候](https://technet.microsoft.com/library/cc783349.aspx)中包含中间证书，但是当前默认的 AD FS 服务器或 AD FS 代理服务器安装仅向 SSL 客户端问候发送 SSL 服务器问候响应中的 AD FS 的服务 SSL 证书。

若要解决此问题，请按以下步骤将证书导入 AD FS 服务器或代理上的计算机个人证书：

1.    在 ADFS 服务器和代理服务器上，右键单击“开始”按钮，选择“运行”，然后键入“certlm.msc”，以启动本地计算机的证书管理控制台。
2.    展开“个人”，然后选择“证书”。
3.    查找用于 AD FS 服务通信的证书（公共签名证书），然后双击以查看其属性。
4.    选择“证书路径”选项卡以查看证书的父证书。
5.    在每个父证书上，选择“查看证书”。
6.    选择“详细信息”选项卡，然后选择“复制到文件...”。
7.    按照向导提示将证书的公钥导出或保存到所需的文件位置。
8.    将步骤 3 中导出的父证书导入到本地计算机\个人\证书，方法是右键单击“证书”，选择“所有任务” > “导入”，然后按照向导提示导入证书。
9.    重启 AD FS 服务器。
10.    在所有 AD FS 和代理服务器上重复上述步骤。
现在用户应能够在 Android 设备上登录到公司门户。

**若要验证是否正确安装证书**：

以下步骤只描述了用于验证是否正确安装证书的许多方法和工具中的一种。

1. 转到[免费的 Digicert 工具](ttps://www.digicert.com/help/)。
2. 输入 AD FS 服务器的完全限定域名（例如，sts.contoso.com），并选择“检查服务器”。

如果已正确安装服务器证书，则会在结果中看见所有复选标记。 如果存在上述问题，则会在报告的“证书名称匹配”和“已正确安装 SSL 证书”部分看见红色的 X。


## <a name="ios-issues"></a>iOS 的问题

### <a name="devices-are-inactive-or-the-admin-console-cannot-communicate-with-them"></a>设备处于非活动状态，或管理控制台不能与其通信
**问题：**iOS 设备未使用 Intune 服务签入。 设备必须定期使用该服务签入，以保持对受保护的公司资源的访问权限。 如果设备不签入：

- 它们将无法从 Intune 服务接收策略、应用和远程命令。
- 它们在管理控制台中显示的管理状态为“不正常”。
- 受条件访问策略保护的用户可能失去对公司资源的访问权限。

**解决方法：**与最终用户共享以下解决方法，帮助他们重新获得公司资源的访问权限。

如果用户启动了 iOS 公司门户应用，则可确定他们的设备是否与 Intune 失去联系。 如果没有检测到任何联系，则会自动尝试与 Intune 同步以重新连接，用户将看到“正在尝试同步...” 内联通知。 

  ![尝试同步通知](./media/ios_cp_app_trying_to_sync_notification.png)

如果同步成功，将在 iOS 公司门户应用中看到“同步成功”内联通知，指示你的设备处于正常状态。

  ![同步成功通知](./media/ios_cp_app_sync_successful_notification.png)

如果同步失败，用户将在 iOS 公司门户应用中看到“无法同步”内联通知。 

  ![无法同步通知](./media/ios_cp_app_unable_to_sync_notification.png)

若要解决此问题，用户必须选择“设置”按钮，该按钮位于“无法同步”通知的右侧。 通过“设置”按钮，用户可转到“公司访问设置”流屏幕，在此处，用户可按提示注册设备。 

  ![“公司访问设置”屏幕](./media/ios_cp_app_company_access_setup.png)

注册后，设备将恢复到正常状态，并重新获得对公司资源的访问权限。

### <a name="profile-installation-failed"></a>配置文件安装失败
**问题：**用户的 iOS 设备上收到**配置文件安装失败**错误。

### <a name="troubleshooting-steps-for-failed-profile-installation"></a>失败配置文件安装的故障排除步骤

1.  确认针对你在使用的 Intune 服务版本，该用户分配有适当的许可证。

2.  确认尚未向另一个 MDM 提供程序注册该设备，或者该设备尚未安装管理配置文件。

3.  导航到 [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com)，并根据提示尝试安装配置文件。

4.  确认默认浏览器为适用于 iOS 的 Safari，并且已启用 Cookie。

### <a name="enrolled-ios-device-doesnt-appear-in-console-when-using-system-center-configuration-manager-with-intune"></a>通过 Intune 使用 System Center Configuration Manager 时，注册的 iOS 设备不会在控制台中显示
**问题：**用户注册了 iOS 设备，但它未出现在 Configuration Manager 管理控制台中。 该设备未指示已注册。 可能的原因：

- 你可能已向某个帐户注册了 Intune 连接器，然后又将其注册到其他帐户。
- 你可能已从某个帐户下载了 MDM 证书，而在其他帐户上使用了它。


**解决方法：**执行以下步骤：

1. 禁用 Windows Intune 连接器内部的 iOS。
    1. 右键单击 Intune 订阅，然后选择**属性**。
    1. 在“iOS”选项卡上，取消选中“启用 iOS 注册”。



2. 在 SQL 中的 CAS 数据库上运行以下步骤

    1. 更新 SC_ClientComponent_Property 设置 Value2 = ''，其中名称类似“%APNS%”
    1. 从 MDMPolicy（其中 PolicyType = 7）中删除
    1. 从 MDMPolicyAssignment（其中 PolicyType = 7）中删除
    1. 更新 SC_ClientComponent_Property 设置 Value2 = ''，其中名称类似“%APNS%”
    1. 从 MDMPolicy（其中 PolicyType = 11）中删除
    1. 从 MDMPolicyAssignment（其中 PolicyType = 11）中删除
    1. 删除 Drs_Signals
3. 重启 SMS Executive 服务或 CM 服务器。

4. 获取新的 APN 证书并上传它。 要实现此操作，请右键单击 Configuration Manager 左侧窗格中的“Intune 订阅”。 选择“创建 APNs 证书请求”，并按照说明进行操作。
5. 
## <a name="issues-when-using-system-center-configuration-manager-with-intune"></a>使用 System Center Configuration Manager with Intune 时的问题

### <a name="mobile-devices-disappear"></a>移动设备消失

**问题：**向 Configuration Manager 成功注册移动设备后，设备从移动设备集合中消失，但该设备仍然具有管理配置文件，并且列示在 CSS 网关中。

**解决方法：**出现此问题可能是因为你有一个自定义进程用于删除未加入域的设备，或者是因为用户已从订阅停用该设备。 若要验证并检查从 Configuration Manager 控制台中删除了该设备的是哪个进程或用户帐户，请执行以下步骤来查看设备是如何被删除的。

1.  在 Configuration Manager 管理控制台中，选择“监视”&gt;“系统状态”&gt;“状态消息查询”。

2.  右键单击“已手动删除的集合成员资源”，并选择“显示消息”。

3.  选择适当的时间/日期或过去 12 小时。

4.  找到有问题的设备，并查看该设备的删除途径。 下面的示例显示帐户 SCCMInstall 是通过某个未知应用程序删除设备的。

    ![设备删除诊断的屏幕快照](./media/cm-with-intune-unknown-app-deleted-device.png)

5.  确保 Configuration Manager 没有计划的任务、脚本或其他可能自动清除非域设备、移动设备或相关设备的进程。




### <a name="other-ios-enrollment-errors"></a>其他 iOS 注册错误

将看到一个 [iOS 注册错误](https://docs.microsoft.com/intune-user-help/you-see-errors-while-trying-to-enroll-your-device-in-intune-ios)列表，最终用户也可能会看到该列表。 该列表提供了有关最终用户可能看到的错误消息，以及解决错误需采取的步骤的信息。

## <a name="pc--issues"></a>PC 问题

### <a name="the-machine-is-already-enrolled---error-hr-0x8007064c"></a>该计算机已注册 - 错误 hr 0x8007064c
**问题：**注册失败，出现“该计算机已注册”错误。 注册日志显示错误 **hr 0x8007064c**。

出现此错误的可能原因是计算机先前已注册，或具有某台已注册的计算机的克隆映像。 先前帐户的帐户证书仍在此计算机上。

**解决方法：**

1. 在“开始”菜单中，键入“运行” -> “MMC”。
1. 选择“文件” > “添加/删除管理单元”。
1. 双击“证书”，选择“计算机帐户” > “下一步”，然后选择“本地计算机”。
1. 双击“证书(本地计算机)”，然后选择“个人/证书”。
1. 查找 Sc_Online_Issuing 发布的 Intune 证书，并将其删除（若存在）。
1. 如果以下注册表项存在，请将其删除：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\OnlineManagement regkey** 及所有子项。
1. 尝试重新注册。
1. 如果仍无法注册电脑，请查找并删除此项（若存在）：**KEY_CLASSES_ROOT\Installer\Products\6985F0077D3EEB44AB6849B5D7913E95**。
1. 尝试重新注册。

    > [!IMPORTANT]
    > 此部分、方法或任务包含教你如何修改注册表的步骤。 但是，如果注册表修改不正确，可能会发生严重问题。 因此，请确保认真遵循这些步骤。 为提高保护程度，请在修改之前备份注册表。 那么，如果发生问题，你也可以恢复注册表。
    > 有关如何备份和还原注册表的详细信息，请阅读[如何在 Windows 中备份和还原注册表](https://support.microsoft.com/en-us/kb/322756)。

## <a name="general-enrollment-error-codes"></a>常规注册错误代码

|错误代码|可能的问题|建议的解决方法|
|--------------|--------------------|----------------------------------------|
|0x80CF0437 |未将客户端计算机上的时钟设置为正确的时间。|确保将客户端计算机上的时钟和时区设置为正确的时间和时区。|
|0x80240438、0x80CF0438、0x80CF402C|无法连接到 Intune 服务。 检查客户端代理设置。|验证 Intune 是否支持客户端计算机上的代理配置，以及客户端计算机是否能够访问 Internet。|
|0x80240438，0x80CF0438|未配置 Internet Explorer 和本地系统中的代理设置。|无法连接到 Intune 服务。 检查客户端代理设置，确认客户端计算机的代理配置受 Intune 支持，且客户端计算机拥有 Internet 访问。|
|0x80043001、0x80CF3001、0x80043004、0x80CF3004|注册程序包过期。|从“管理”工作区中下载并安装最新的客户端软件包。|
|0x80043002、0x80CF3002|帐户处于维护模式。|当帐户处于维护模式时，你无法注册新客户端计算机。 若要查看帐户设置，请登录到你的帐户。|
|0x80043003、0x80CF3003|帐户被删除。|验证你的帐户和 Intune 订阅是否仍处于活动状态。 若要查看帐户设置，请登录到你的帐户。|
|0x80043005、0x80CF3005|客户端计算机已停用。|等几个小时并从计算机中删除任何较旧版本的客户端软件，然后重试客户端软件安装。|
|0x80043006、0x80CF3006|已达到允许此帐户拥有的最大座位数。|贵组织必须购买附加的座位，你才能在服务中注册更多客户端计算机。|
|0x80043007、0x80CF3007|在安装程序所在的文件夹中找不到证书文件。|在开始安装之前提取所有文件。 请不要重命名或重新定位任何提取的文件：所有文件必须位于同一文件夹中，否则安装将失败。|
|0x8024D015、0x00240005、0x80070BC2、0x80070BC9、0x80CFD015|无法安装软件，因为客户端计算机的重启处于挂起状态。|重启计算机，然后重试客户端软件安装。|
|0x80070032|在客户端计算机上未找到用于安装客户端软件的一个或多个先决条件。|确保所有必需的更新都已安装在客户端计算机上，然后重试客户端软件安装。|
|0x80043008、0x80CF3008|未能启动 Microsoft Online Management 更新服务。|请联系 Microsoft 支持部门，如[如何获取对 Microsoft Intune 的支持](https://docs.microsoft.com/intune-classic/troubleshoot/get-support)中所述。|
|0x80043009、0x80CF3009|已在服务中注册客户端计算机。|你必须先停用客户端计算机，然后才能在服务中重新注册该客户端计算机。|
|0x8004300B、0x80CF300B|无法运行客户端软件安装包，因为不支持客户端上运行的 Windows 的版本。|Intune 不支持客户端计算机上运行的 Windows 的版本。|
|0xAB2|Windows Installer 无法针对自定义操作访问 VBScript 运行时。|此错误是由基于动态链接库 (DLL) 的自定义操作引起的。 对 DLL 进行疑难解答时，可能必须使用 [Microsoft 支持 KB198038：用于打包和部署问题的有用工具](https://support.microsoft.com/en-us/kb/198038)中描述的工具。|
|0x80cf0440|到服务终结点的连接已终止。|试用或付费帐户处于挂起状态。 创建一个新的试用或付费帐户，并重新注册。|




### <a name="next-steps"></a>后续步骤
如果此疑难解答信息没有帮助到你，请联系 Microsoft 支持部门，如[如何获取对 Microsoft Intune 的支持](https://docs.microsoft.com/intune-classic/troubleshoot/get-support)中所述。
