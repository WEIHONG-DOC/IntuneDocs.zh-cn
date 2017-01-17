---
title: "Microsoft Intune VPN 配置文件的自定义配置 | Microsoft Docs"
description: "使用自定义配置在 Intune 中创建 VPN 配置文件。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 12/15/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 4c0bd439-3b58-420b-9a9a-282886986786
ms.reviewer: karanda
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f2b364b2c57adab33df2a8e6b34c1f30c02988d3
ms.openlocfilehash: 9dbb44981c1525e6137dd8a469b1582731ee9719


---

# <a name="custom-configurations-for-microsoft-intune-vpn-profiles"></a>Microsoft Intune VPN 配置文件的自定义配置

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

## <a name="create-a-custom-configuration"></a>创建自定义配置
可使用 Intune 自定义配置策略为以下设备创建 VPN 配置文件：

* 运行 Android 4 和更高版本的设备
* Android for Work 设备
* 运行 Windows 8.1 和更高版本的已注册设备
* 运行 Windows Phone 8.1 和更高版本的设备
* 运行 Windows 10 桌面版的已注册设备 
* 运行 Windows 10 移动版的设备

此类型的策略在标准 Intune VPN 策略不包含要使用的设置时很有用。

## <a name="to-create-a-custom-configuration-policy"></a>创建自定义配置策略：

   1. 在 [Intune 管理控制台](https://manage.microsoft.com)中，选择“策略” > “添加策略” > “展开平台” > “自定义配置” > “创建策略”。
   2. 输入策略的名称。
   3. 对于要指定的每个 URI 设置，选择“添加”并提供要求的信息。 下面是一个示例：

   ![VPN 配置文件自定义配置对话框](./media/Intune_Add_VPN_URI.png)

   4.  输入所有 URI 设置后，选择“保存策略”，然后部署策略。

然后，照常[部署策略](/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#deploy-a-configuration-policy)。

## <a name="example-uri-settings"></a>示例 URI 设置

这些设置可用于在名为 Contoso 的虚构公司为 VPN 创建自定义配置。
有关可使用的所有设置的完整详细信息，请参阅 [VPNv2 CSP](https://msdn.microsoft.com/en-us/library/windows/hardware/dn914776.aspx)。

Native Contoso VPN (IKEv2): ./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/Servers

vpn.contoso.com ./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/NativeProtocolType

Ikev2 ./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/RoutingPolicyType

SplitTunnel ./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/Authentication/UserMethod

Eap ./Vendor/MSFT/VPNv2/ContosoVPN/NativeProfile/Authentication/Eap/Configuration &lt;EapHostConfig xmlns="http://www.microsoft.com/provisioning/EapHostConfig"&gt;&lt;EapMethod&gt;&lt;Type xmlns="http://www.microsoft.com/provisioning/EapCommon"&gt;13&lt;/Type&gt;&lt;VendorId xmlns="http://www.microsoft.com/provisioning/EapCommon"&gt;0&lt;/VendorId&gt;&lt;VendorType xmlns="http://www.microsoft.com/provisioning/EapCommon"&gt;0&lt;/VendorType&gt;&lt;AuthorId xmlns="http://www.microsoft.com/provisioning/EapCommon"&gt;0&lt;/AuthorId&gt;&lt;/EapMethod&gt;&lt;Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig"&gt;&lt;Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"&gt;&lt;Type&gt;13&lt;/Type&gt;&lt;EapType xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"&gt;&lt;CredentialsSource&gt;&lt;CertificateStore&gt;&lt;SimpleCertSelection&gt;true&lt;/SimpleCertSelection&gt;&lt;/CertificateStore&gt;&lt;/CredentialsSource&gt;&lt;ServerValidation&gt;&lt;DisableUserPromptForServerValidation&gt;false&lt;/DisableUserPromptForServerValidation&gt;&lt;ServerNames&gt;&lt;/ServerNames&gt;&lt;/ServerValidation&gt;&lt;DifferentUsername&gt;false&lt;/DifferentUsername&gt;&lt;PerformServerValidation xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"&gt;false&lt;/PerformServerValidation&gt;&lt;AcceptServerName xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"&gt;false&lt;/AcceptServerName&gt;&lt;/EapType&gt;&lt;/Eap&gt;&lt;/Config&gt;&lt;/EapHostConfig&gt;

**./Vendor/MSFT/VPNv2/ContosoVPN/ByPassForLocal** True

**./Vendor/MSFT/VPNv2/ContosoVPN/RememberCredentials** 1

**./Vendor/MSFT/VPNv2/ContosoVPN/DomainNameInformationList/1/DomainName** Corp.Contoso.com

**./Vendor/MSFT/VPNv2/ContosoVPN/DnsSuffix** Corp.Contoso.com

**./Vendor/MSFT/VPNv2/ContosoVPN/TrustedNetworkDetection** Corp.Contoso.com

**./Vendor/MSFT/VPNv2/ContosoVPN/RouteList/1/Address** 10.0.0.0

**./Vendor/MSFT/VPNv2/ContosoVPN/RouteList/1/PrefixSize** 8

**./Vendor/MSFT/VPNv2/ContosoVPN/AlwaysOn** true

**./Vendor/MSFT/VPNv2/ContosoVPN/AppTriggerList/0/App/Id** %PROGRAMFILES%\Internet Explorer\iexplore.exe

**./Vendor/MSFT/VPNv2/ContosoVPN/AppTriggerList/1/App/Id** %PROGRAMFILES% (x86)\Internet Explorer\iexplore.exe

**./Vendor/MSFT/VPNv2/ContosoVPN/AppTriggerList/2/App/Id** Microsoft.MicrosoftEdge_8wekyb3d8bbwe

**./Vendor/MSFT/VPNv2/ContosoVPN/TrafficFilterList/0/App/Id** %PROGRAMFILES% (x86)\Internet Explorer\iexplore.exe

**./Vendor/MSFT/VPNv2/ContosoVPN/TrafficFilterList/1/App/Id** Microsoft.MicrosoftEdge_8wekyb3d8bbwe

有关应如何使用这些设置的任何问题或者有关其作用的更多详细信息，客户应参考配置服务供应商 (CSP) 文档：https://msdn.microsoft.com/en-us/library/windows/hardware/dn914776(v=vs.85).aspx。

## <a name="uri-settings-for-android-per-app-vpn-on-pulsesecure"></a>PulseSecure 上的 Android 每应用 VPN 的 URI 设置
### <a name="custom-uri-for-package-list"></a>包列表的自定义 URI
-  数据类型 = 字符串
-  OMA-URI = ./Vendor/MSFT/VPN/Profile/Name/PackageList
-  值 = 分隔符分隔的包列表。
   - 分隔符：分号 (;)、冒号 (:)、逗号 (,)、竖线 (|)

例如：
- com.android.chrome
- com.android.chrome;com.android.browser

### <a name="custom-uri-for-mode-optional"></a>模式的自定义 URI（可选）
- 数据类型 = 字符串
- OMA-URI = ./Vendor/MSFT/VPN/Profile/NAME/Mode

> 注意
> - 请使用分配给自定义配置文件的同一个*名称*
> - 可能的值：“全局”、“允许列表”、“阻止列表”
> - 如果未提供 PackageList，则默认为“全局”（与整个系统的配置文件向后兼容）
> - 如果提供了 PackageList，则默认为“允许列表”


### <a name="see-also"></a>另请参阅
[Microsoft Intune 中的 VPN 连接](vpn-connections-in-microsoft-intune.md)



<!--HONumber=Dec16_HO3-->

