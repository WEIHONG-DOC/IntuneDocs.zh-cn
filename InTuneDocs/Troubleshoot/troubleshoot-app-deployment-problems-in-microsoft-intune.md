---
# required metadata

title: 应用部署问题疑难解答 | Microsoft Intune
description:
keywords:
author: Nbigman
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 28ac298e-fb73-4c1c-b3fd-8336639e05e6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: jeffgilb
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Microsoft Intune 中的应用部署问题疑难解答
本主题有助于解决 Microsoft Intune 中的应用部署问题。

如果此信息未解决你的问题，请参阅[如何获取对 Microsoft Intune 的支持](how-to-get-support-for-microsoft-intune.md)，了解更多获得帮助的方法。


## 典型应用部署问题

### 如果你不能登录到 Microsoft Intune 公司门户

1.  检查你的帐户是否存在于 [Office 365 门户](http://go.microsoft.com/fwlink/p/?LinkId=698854)中或者是否被禁用。

2.  确保你在 [Office 365 门户](http://go.microsoft.com/fwlink/p/?LinkId=698854)中对此帐户进行了设置

3.  在 [Office 365 门户](http://go.microsoft.com/fwlink/p/?LinkId=698854)中，确保你正在使用正确的用户名和密码登录到 Intune，并且其格式为：**joe@domain.com**

### 如果公司门户中缺少“联系 IT”信息

1.  在 Intune 管理员控制台中，单击“管理” &gt; “公司门户”

2.  设置“联系 IT”  详细信息。

### 如果在列表中看不到特定应用

1.  确保检查部署了该应用的用户或设备的应用列表。

2.  确保设备满足应用的要求。

### 如果在下载应用时收到错误

1.  请确保每个用户最多有一个并发下载。 每个用户一次可以下载一个应用。

2.  确保每个帐户没有过多的并发下载。 等待几分钟，然后重试。

3.  如果收到 iOS 本机消息，称“你无法安装”、“已取消安装”或“你需要重试”，则可能是由高流量造成。 等待几分钟，然后重试。

4.  如果 iOS 应用下载进程栏已完成但应用安装失败，则你提供的应用文件可能存在问题。

### 如果单击指向 iOS 应用的链接将你带到 iTunes 应用商店中的前一个位置

1.  当前 iTunes 应用商店会话会打开到上一个应用页面。

2.  关闭设备上的 iTunes 应用商店，并重试该链接。

### 如果在启动 iOS 应用时收到错误

1.  应用的到期日期可能不是有效日期。

### 如果应用在上载时一直显示“正在进行”

1.  在上载应用时，首先会添加元数据，然后添加应用包。 上载了元数据后，应用将显示为正在进行。 如果你看到应用处于正在进行状态的时间特别长，请删除应用，然后再次上传。

2.  确保不要在应用处于“正在进行”状态时对应用的部署进行管理。

### 如果在安装 iOS 应用时遇到失败情况

1.  确保组织的防火墙允许访问 Apple 设置和认证网站。

2.  有关详细信息，请查看 Apple 开发人员文档。

### 错误：发布服务器不存在
使用“添加其他软件协议”以添加第三方许可协议。 尝试从“其他软件许可协议”页添加发布服务器。 该页按字母顺序提供现有发布服务器的列表。
输入缺少的发布服务器，但收到错误“发布服务器不存在” 

这是由于设计而导致的。 Intune 提供仅适用于常用软件标题的许可证跟踪。 Intune 要求至少有 4 个独立帐户报告此软件，才能将其提供为许可工作负荷中的一个选项。

### 如果托管应用没有报告安装状态

对于 2014 年 11 月 Microsoft Intune 服务更新之前的托管应用安装，不收集安装状态。 对于在此服务更新之前安装了托管应用的设备，通过适当部署操作（例如 **可用安装**）更新每个关联应用部署。 各个设备将在自动检查可用应用期间更新应用。 有关更多信息，请参阅[使用 Microsoft Intune 更新应用](/intune/deploy-use/update-apps-using-microsoft-intune)

## <a name="BKMK_SoftDistErrorCodes"></a>应用部署错误代码
下表列出了 Intune 应用部署过程中可能发生的常见错误、可能的原因，以及有助于解决问题的潜在解决方案。

|错误代码|可能的问题|建议的解决方法|
|--------------|--------------------|------------------------|
|0x80073CFF<br /><br />0x80CF201C（客户端错误）|若要安装此应用，你必须具有支持旁加载的系统。|确保使用受信任的签名对应用包进行了签名，并且确保在已启用 AllowAllTrustedApps 策略且已加入域的设备上安装了该应用包，或者在具有 Windows 旁加载许可证且已启用 AllowAllTrustedApps 策略(在注册 Windows RT 设备时应用)的设备上安装了该应用包。|
|0x80073CF0|无法打开包。|可能的原因：<br /><br />-   未对包进行签名。<br />-   发布者名称与签名证书使用者不匹配。<br /><br />有关详细信息，请检查 AppxPackagingOM 事件日志。|
|0x80073CF3|包未通过更新、依赖关系或冲突验证|可能的原因：<br /><br />-   传入的包与已安装的包冲突。<br />-   找不到指定的包依赖关系。<br />-   包不支持正确的处理器体系结构。<br /><br />有关详细信息，请检查 AppXDeployment-Server 事件日志。|
|0x80073CFB|已经安装了提供的包，阻止重新安装此包|如果你正在安装的包与已安装的包并不完全相同，则可能会收到此错误。 确认数字签名也是包的一部分。 对包进行重新构建或者重新签名时，该包与以前安装的包在位方面不再完全相同。 用于修复此错误的两个可能的选项如下所示：<br /><br />-   递增应用的版本号，然后对包进行重新构建并重新签名。<br />-   在安装新包之前，请删除系统上每个用户的旧包。|

### 后续步骤
如果此疑难解答信息没有帮助到你，请联系 Microsoft 支持部门，如[如何获取对 Microsoft Intune 的支持](how-to-get-support-for-microsoft-intune.md)中所述


<!--HONumber=May16_HO2-->

