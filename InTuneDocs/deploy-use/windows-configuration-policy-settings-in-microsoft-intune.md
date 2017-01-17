---
title: "Windows 策略设置 ｜ Microsoft Docs"
description: "使用 Intune Windows 常规配置策略（Windows 8.1 及更高版本）为已注册的 Windows 8 和 Windows 8.1 设备配置设置。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 10/11/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 6982a2bc-aafa-475a-9236-4840b709e5a1
ms.reviewer: jeffgilb
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b6d5ea579b675d85d4404f289db83055642ffddd
ms.openlocfilehash: 53ac1c31cf2a2054080e43716b30c50c73961759


---

# <a name="windows-policy-settings-in-microsoft-intune"></a>Microsoft Intune 中的 Windows 策略设置

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

使用 Microsoft Intune **Windows 常规配置策略（Windows 8.1 及更高版本）**为已注册的 Windows 8、Windows 8.1 和 Windows RT 8.1 设备配置以下设置：

## <a name="applicability-settings"></a>适用性设置

|设置名|详细信息|
|----------------|----------------------------------|
|**将所有配置应用到 Windows 10**|使此策略中的设置除了可以应用到 Windows 8 和 Windows 8.1 设备外，还可以应用到 Windows 10 设备。|

## <a name="security-settings"></a>安全设置

|设置名|详细信息|
|----------------|------|
|**所需的密码类型**|指定需要的密码类型，例如仅限字母数字或数字。|
|**必填密码类型 – 字符集最小数量**|指定密码中必须包括多少个不同的字符集。 有以下四个字符集：小写字母、大写字母、数字和符号。 但是，对于 iOS 设备，此设置指定密码中必须包括的符号的数量。|
|**最短密码长度**|配置密码的最小所需长度（以字符计算）。|
|**擦除设备前允许的重复登录失败次数**|如果登录尝试失败达到此次数，则擦除设备。|
|**屏幕关闭前处于不活动状态的分钟数**|指定需要密码以进行解锁之前，设备必须保持空闲的分钟数。|
|**密码过期（天数）**|指定必须更改设备密码前的天数。|
|**记住密码历史记录**|指定用户是否可以配置以前用过的密码。|
|**“记住密码历史记录”** – **“防止重用以前的密码”**|指定设备记住的以前用过的密码数目。|
|**允许图片密码和 PIN**|允许使用图片密码和 PIN。 图片密码允许用户使用图片上的手势登录。 PIN 允许用户使用 4 位代码快速登录。|

## <a name="encryption-settings"></a>加密设置

|设置名|详细信息|
|----------------|-----|
|**需要对移动设备加密**<sup>1</sup>|要求对设备上的文件进行加密。|
<sup>1</sup>运行 Windows 8.1 的设备的其他信息

-   若要在运行 Windows 8.1 的设备上强制加密，必须在每台设备上安装 [用于 Windows 的 December 2014 MDM 客户端更新](http://support.microsoft.com/kb/3013816) 。

-   如果对 Windows 8.1 设备启用此设置，则该设备的所有用户必须都具有 Microsoft 帐户。

-   为了使加密正常工作，该设备必须满足 Microsoft [InstantGo](http://blogs.windows.com/bloggingwindows/2014/06/19/instantgo-a-better-way-to-sleep/) 硬件认证要求。

-   在设备上强制加密时，恢复密钥仅可从用户的 Microsoft 帐户（从用户的 OneDrive 帐户访问）进行访问。 无法代表用户恢复此密钥。

## <a name="malware-settings"></a>恶意软件设置

|设置名|详细信息|
|----------------|-----|
|**需要网络防火墙**|需要 Windows 防火墙处于打开状态。|
|**启用 SmartScreen**|需要使用 Windows SmartScreen。|

## <a name="system-settings"></a>系统设置

|设置名|详细信息|
|----------------|-------|
|**需要自动更新**|打开设备上的自动更新设置。|
|**需要自动更新 - 要自动安装的最小更新分类**|选择将自动安装的更新分类：<br /><br />-   **重要** - 安装归类为重要的所有更新。<br />-   **推荐** - 安装归类为重要或推荐的所有更新。|
|**用户帐户控制**|需要在设备上使用用户帐户控制 (UAC)。|
|**允许提交诊断数据**|允许设备将诊断信息提交到 Microsoft。|


## <a name="cloud-settings--documents-and-data"></a>云设置 – 文档和数据

|设置名|详细信息|
|----------------|------|
|**工作文件夹 URL**|设置工作文件夹的 URL，以允许文档跨设备同步。|

## <a name="email-settings"></a>电子邮件设置

|设置名|详细信息|
|----------------|-----|
|**在 Windows 邮件应用程序中将 Microsoft 帐户设为可选**|允许在没有 Microsoft 帐户的情况下访问 Windows Mail 应用程序。|

## <a name="application-settings---browser"></a>应用设置 - 浏览器

|设置名|详细信息|
|----------------|-----|
|**允许自动填充**|允许用户更改浏览器中的自动完成设置。|
|**允许使用弹出窗口阻止程序**|启用或禁用浏览器弹出窗口阻止程序。|
|**允许使用插件**|允许用户向 Internet Explorer 添加插件。|
|**允许使用活动脚本**|允许浏览器运行脚本，如 Active X 脚本。|
|**允许使用欺诈警告**|启用或禁用对潜在欺诈网站的警告。|
|**允许 Intranet 站点使用单字条目**|允许使用单字将 Internet Explorer 转到“必应”之类的网站。|
|**允许自动检测 Intranet 网络**|帮助在 Internet Explorer 中配置 intranet 站点安全性。|
|**互联网的安全级别**|设置 Internet 站点的 Internet Explorer 安全级别。|
|**Intranet 安全级别**|设置 Intranet 站点的 Internet Explorer 安全级别。|
|**受信任的站点的安全级别**|配置受信任的站点区域的安全级别。|
|**受限制的站点的安全级别**|配置受限制的站点区域的安全级别。|
|**发送“不跟踪”标头**|在 Internet Explorer 中，将“不跟踪”标头发送到访问过的网站。|
|**允许企业模式菜单访问**|允许用户从 Internet Explorer 访问企业模式菜单选项。<br>如果选择此设置，你还可以指定**日志记录报告位置**，其中包含指向一个报表的 URL，该报表显示了用户为其启用了企业模式访问的网站。|
|**企业模式网站列表位置**|指定活动状态下将使用企业模式的网站列表的位置。|

## <a name="device-capabilities-settings---cellular"></a>设备性能设置 - 蜂窝网络

|设置名|详细信息|
|----------------|----|
|**允许数据漫游**|当设备处于移动电话网络中时允许数据漫游。|



### <a name="see-also"></a>另请参阅
[使用 Microsoft Intune 策略管理设备上的设置和功能](manage-settings-and-features-on-your-devices-with-microsoft-intune-policies.md)



<!--HONumber=Dec16_HO2-->

