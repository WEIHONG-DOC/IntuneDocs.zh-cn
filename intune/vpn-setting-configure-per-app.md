---
title: 在 Microsoft Intune 中设置适用于 iOS 设备的每个应用程序 VPN - Azure | Microsoft 文档
description: 查看先决条件，为虚拟专用网络 (VPN) 用户创建组，添加 SCEP 证书配置文件，配置每个应用程序 VPN 配置文件，以及将一些应用分配到 iOS 设备上 Microsoft Intune 中的 VPN 配置文件。 此外，还列出了在设备上验证 VPN 连接的步骤。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/28/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: D9958CBF-34BF-41C2-A86C-28F832F87C94
ms.reviewer: karanda
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 7cf005b225dd11ca6b95dbed0a82330544575f92
ms.sourcegitcommit: 2d1e89fa5fa721e79648e41fde147a035e7b047d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "43347468"
---
# <a name="set-up-per-app-virtual-private-network-vpn-in-intune-for-ios-devices"></a>在 Intune 中为 iOS 设备设置每应用虚拟专用网络 (VPN)

可指定哪些托管应用可在 Intune 托管的 iOS 设备上使用虚拟专用网络 (VPN)。 在 Intune 中创建每应用 VPN 时，最终用户访问公司文档时会自动通过 VPN 进行连接。

每应用 VPN 当前对以下提供程序可用：

 - 检查点远程访问 VPN
 - Cisco AnyConnect
 - Citrix
 - F5
 - 脉冲连接安全
 - SonicWall
 - 帕洛阿尔托网络全局保护
 - Zscaler

## <a name="prerequisites-for-per-app-vpn"></a>每个应用 VPN 的先决条件

> [!IMPORTANT]
> 你的 VPN 供应商可能对每个应用 VPN 有其他特定要求，例如特定硬件或许可。 在 Intune 中设置每个应用 VPN 之前，请务必检查其文档并满足这些先决条件。

为了证明其身份，VPN 服务器提供了设备必须在提示的情况下必须接受的证书。 若要确保自动批准证书，请创建包含由证书颁发机构 (CA) 颁发的 VPN 服务器根证书的受信任证书配置文件。 

导出证书并添加 CA。

1. 在 VPN 服务器上打开管理控制台。
2. 验证 VPN 服务器是否使用基于证书的身份验证。 
3. 导出受信任的根证书文件。 其扩展名为 .cer，在创建受信任的证书配置文件时添加它。
4. 添加颁发用于对 VPN 服务器进行身份验证的证书的 CA 名称。
    如果该设备提供的 CA 与 VPN 服务器上受信任 CA 列表中的某个 CA 匹配，则 VPN 服务器可成功对该设备进行验证。

## <a name="create-a-group-for-your-vpn-users"></a>为 VPN 用户创建组

在 Azure Active Directory (Azure AD) 中创建组或选择现有组，以包含有权访问每应用 VPN 的成员。

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 选择“所有服务”，筛选“Intune”，然后选择“Microsoft Intune”。
2. 选择“组”，再单击“新建组”。
3. 为该组选择“组类型”。 
3. 键入组的“组名称”。 
4. 键入组的“组说明”。 
5. 对“成员身份类型”选择“已分配”。
7. 在“成员”窗格中按名称或电子邮件地址搜索 VPN 用户。
8. 选择每个用户，然后单击“选择”。
9. 单击“创建”

## <a name="create-a-trusted-certificate-profile"></a>创建受信任的证书配置文件

将 CA 颁发的 VPN 服务器根证书导入到 Intune 中创建的配置文件中。 受信任的证书配置文件指示 iOS 设备自动信任 VPN 服务器提供的 CA。

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 选择“所有服务”，筛选“Intune”，然后选择“Microsoft Intune”。
2. 选择“设备配置”，然后单击“配置文件”。
3. 单击“创建配置文件”。 在“创建配置文件”中：
    1. 键入“名称”。
    2. 键入“说明”。
    3. 对“平台”选择“iOS”。
    4. 对“配置文件类型”选择“受信任的证书”。
4. 单击文件夹图标，浏览到从 VPN 管理控制台导出的 VPN 证书（.cer 文件）。 单击" **确定**"。
5. 单击“创建”。

    ![创建受信任的证书配置文件](./media/vpn-per-app-create-trusted-cert.png)

## <a name="create-a-scep-certificate-profile"></a>创建 SCEP 证书配置文件

受信任的根证书配置文件允许 iOS 自动信任 VPN 服务器。 SCEP 证书提供 iOS VPN 客户端到 VPN 服务器的凭据。 该证书允许设备以不提示 iOS 设备用户输入用户名和密码的方式进行身份验证。 

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 选择“所有服务”，筛选“Intune”，然后选择“Microsoft Intune”。
2. 选择“设备配置”，然后单击“配置文件”。
3. 单击“创建配置文件”。 在“创建配置文件”中：
    1. 键入“名称”。
    2. 键入“说明”。
    3. 对“平台”选择“iOS”。
    4. 对“配置文件类型”选择“SCEP 证书”。
4. 选择“年”并在“证书有效期”中键入 `2`。
5. 对“使用者名称格式”选择“公用名”。
6. 对“使用者可选名称”选择“用户主体名称(UPN)”。
7. 对“密钥用法”选择“数字签名”和“密钥加密”。
8. 对“密钥大小(位)”选择“2048”。
9. 单击根证书并选择一个 SCEP 证书。 单击" **确定**"。
10. 在“扩展密钥用法”的“名称”中键入 `Client Authentication`。
11. 在“对象标识符”中键入 `1.3.6.1.5.5.7.3.2`。
12. 单击“添加” 。
13. 键入“服务器 URL”并单击“添加”。
14. 单击" **确定**"。
15. 单击“创建”。

    ![创建 SCEP 证书配置文件](./media/vpn-per-app-create-scep-cert.png)

## <a name="create-a-per-app-vpn-profile"></a>创建每个应用 VPN 配置文件

VPN 配置文件包含附带客户端凭据的 SCEP 证书、VPN 的连接信息以及每应用 VPN 标志，用于启用供 iOS 应用程序使用的每应用 VPN 功能。

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 选择“所有服务”，筛选“Intune”，然后选择“Microsoft Intune”。
2. 选择“设备配置”，然后单击“配置文件”。
3. 单击“创建配置文件”。 在“创建配置文件”中：
    1. 键入“名称”。
    2. 键入“说明”。
    3. 对“平台”选择“iOS”。
    4. 对“配置文件类型”选择“VPN”。
4. 选择“基础 VPN”。 在“Base VPN”中：
    1. 键入“连接名称”。
    2. 键入“IP 地址或 FQDN”。
    3. 对“身份验证方法”选择“证书”。
    4. 在“身份验证证书”下选择 SCEP 证书并单击“确定”。
    5. 对“连接类型”选择你的 VPN。
    6. 如有必要，请为 VPN 配置属性。
    7. 对“拆分隧道”选择“禁用”。
5. 单击“自动 VPN”。 在“自动 VPN”中：
    1. 对“自动 VPN 类型”选择“每应用 VPN”。
    2. 键入 VPN 的 URL 并单击“添加”。
    3. 单击" **确定**"。
6. 单击" **确定**"。
7. 单击“创建”。

    ![创建每个应用 VPN 配置文件](./media/vpn-per-app-create-vpn-profile.png)


## <a name="associate-an-app-with-the-vpn-profile"></a>将应用与 VPN 配置文件相关联

添加 VPN 配置文件后，将应用和 Azure AD 组与配置文件关联。

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 选择“所有服务”，筛选“Intune”，然后选择“Microsoft Intune”。
3. 选择“客户端应用”。
4. 单击“应用”。
5. 从应用列表中选择应用。
6. 单击“分配”。
7. 单击“添加组”。
8. 在“添加组”窗格中对“分配类型”选择“必需”。
9. 选择前面定义的组，然后进行选择，使此应用为必需。
10. 对“VPN”选择你的 VPN 定义。
 
    > [!NOTE]  
    > 有时 VPN 定义会占用长达一分钟的时间来检索值。 单击“保存”之前等待 3-5 分钟。

11. 单击“确定”，然后单击“保存”。

    ![将应用与 VPN 相关联](./media/vpn-per-app-app-to-vpn.png)

当存在以下条件时，在下一个设备签入期间，将删除应用和配置文件之间的关联：
- 通过所需的安装意向来定向应用。
- 配置文件和应用都定向到同一组。
- 从应用分配中删除每个应用 VPN 配置。

当存在以下条件时，应用和配置文件之间的关联仍将存在，直到最终用户从公司门户请求重新安装：
- 通过可用的安装意向来定向应用。
- 配置文件和应用都定向到同一组。
- 最终用户从公司门户请求安装应用，导致在设备上安装应用和配置文件。
- 从应用分配中删除每个应用 VPN 配置。

## <a name="verify-the-connection-on-the-ios-device"></a>验证 iOS 设备上的连接

设置每应用 VPN 并将其与应用相关联后，从设备验证连接是否有效。

### <a name="before-you-attempt-to-connect"></a>尝试连接之前请确保满足以下各项

 - 确保运行的是 iOS 9 或更高版本。
 - 确保部署将上述所有策略部署到同一用户组。 如果未能执行此操作，这极有可能会中断每应用 VPN 体验。  
 - 确保安装有支持的第三方 VPN 应用。 支持以下 VPN 应用：
    - Check Point Capsule 连接
    - Cisco AnyConnect
    - Citrix VPN
    - F5 Access
    - 脉冲安全
    - SonicWall Mobile Connect
    - Zscaler 应用

    > [!NOTE]
    > 如果使用 Pulse Secure VPN 应用，可以选择使用应用层或数据包层隧道。 针对应用层隧道，将 ProviderType 值设置为 app-proxy，针对数据包层隧道，将其设置为 packet-tunnel。

### <a name="connect-using-the-per-app-vpn"></a>使用每应用 VPN 进行连接

无需选择 VPN 或键入凭据即可连接，感受“零接触”体验。 “零接触”体验意味着：

 - 设备不要求你信任 VPN 服务器。 也就是说，不会显示“动态信任”对话框。
 - 无需键入凭据。
 - 点击“连接”按钮后即会连接到 VPN。

验证 iOS 设备上的连接。

1. 点击 VPN 应用。
2. 点击“连接”。  
VPN 成功连接，而没有任何额外提示。

<!-- ## Troubleshooting the per-app VPN

The user experiences the feature by silently connecting to the VPN. This experience, however, can provide little information for troubleshooting. You can review the event logs crated by the iOS device.

`Note -- use the Apple Configurator as the supported tool. Only runs on a mac.'

To review event logs:

1. Connect your iOS device to a PC
2. Open the **iPhone Configuration Utility** (IPCU). If you do not have a copy, you can install it from [CompatCenter](http://www.microsoft.com/en-us/windows/compatibility/CompatCenter/ProductDetailsViewer?Name=iPhone%20Configuration%20Utility&vendor=Apple&Locale=1033%2C2057%2C3081%2C4105%2C16393&ModelOrVersion=3&BreadCrumbPath=iphone%20configuration%20utility&LastSearchTerm=iphone%2Bconfiguration%2Butility&Type=Software&tempOsid=Windows%208.1)
3. Review the logs. -->

## <a name="next-steps"></a>后续步骤

- 若要查看 iOS 设置，请参阅 [Microsoft Intune 中适用于 iOS 设备的 VPN 设置](vpn-settings-ios.md)。
-  若要详细了解 VPN 设置和 Intune，请参阅[如何在 Microsoft Intune 中配置 VPN 设置](vpn-settings-configure.md)。
