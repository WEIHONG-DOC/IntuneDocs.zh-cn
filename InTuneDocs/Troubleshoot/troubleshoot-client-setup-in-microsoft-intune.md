---
# required metadata

title: 客户端安装程序疑难解答 | Microsoft Intune
description:
keywords:
author: Nbigman
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: e46d292b-1d16-46db-a87f-d53eefa4d22a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: jeffgilb
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 排查 Microsoft Intune 中的客户端安装问题
使用以下信息有助于排除常见的客户端安装程序问题。 如果此信息未解决你的问题，请参阅[如何获取对 Microsoft Intune 的支持](how-to-get-support-for-microsoft-intune.md)，了解更多获得帮助的方法。

## 客户端安装失败

-   如果 [Microsoft Intune 管理员控制台](https://manage.microsoft.com/)中未显示计算机的客户端软件部署警报，请检查计算机的网络连接和代理配置，并确保计算机能够与服务 URL [https://manage.microsoft.com](https://manage.microsoft.com/) 通信。 然后重新安装客户端软件。

-   当出现客户端软件部署故障警报时，你可以通过在  “管理员”工作区中配置通知规则向选中的收件人发送邮件。 有关详细信息，请参阅[通过 Microsoft Intune 警报获取通知](/intune/deploy-use/get-notified-by-microsoft-intune-alerts)

-   如果客户端软件部署失败，Intune 会显示重要警报“客户端软件部署故障”。 这将显示在“系统概述”页面和 [Microsoft Intune 管理员控制台](https://manage.microsoft.com/)的“警报”页面。 下面介绍了如何检查警报：

1.  在 [Microsoft Intune 管理员控制台](https://manage.microsoft.com/)中，单击“警报” &gt; “概述”

2.  在“警报概述”页面，  你可以查看以下信息：

    -   前三个警报，可按日期、类别或严重性对这些警报排序

    -   活动警报的总数

3.  单击“所有警报”  以在“警报”页面显示以下信息。   首先显示重要警报：

    -   **名称** – 生成警报的警报类型的名称。

    -   **源** – 指向警报的源的链接。  如果将警报类型的显示阈值设置为“全部” ，则此链接将显示单个受影响的设备。  如果将警报类型的显示阈值设置为一个值，则此链接将显示受此警报影响的所有设备的列表。

    -   **上次更新时间** – 此项指明上次修改警报的时间。 如果警报已关闭，则显示警报关闭时的时间。

    -    “严重程度”– 表示警报的严重程度

## 计算机注册包未下载
**问题：**尝试注册计算机时遇到以下问题：
-  注册包下载失败 
-  出现下载对话框但超时

**解决方法：**在下载使用的浏览器上，确保已在下载进行期间启用了下载，且加密文件可以保存到本地磁盘。

## 客户端安装挂起，错误代码 0x80040154
**问题：**
 
-  注册挂起期间的客户端安装。

-  无法注册设备 

-  WindowsUpdate.log 中的错误 0x80040154

原因可能是电脑上缺少关键软件更新。

解决方法： 


## 确保你的软件更新策略启用了关键更新的安装，如[在 Microsoft Intune 中利用软件更新使 Windows 电脑保持最新版本](/intune/deploy-use/keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune)中所述
policyplatform.log 中与 Microsoft Intune 策略相关的错误 对于非 MDM Windows 设备，policyplatform.log 文件中的策略错误可能是因设备上 Windows 用户帐户控制 (UAC) 中的非默认设置导致的。

### 某些非默认 UAC 设置会影响 Microsoft Intune 客户端安装和策略执行。

1.  解决 UAC 问题

2.  停用计算机，如[从 Microsoft Intune 管理停用数据和设备](/intune/deploy-use/retire-devices-from-microsoft-intune-management)中所述

    > 等待 20 分钟，以便删除客户端软件。

3.  请勿尝试从“程序和功能”中删除客户端。

4.  在开始菜单上，键入 **UAC** 以打开用户帐户控制设置。

## 将通知滑块移动到默认设置。

### 如果客户端无法从 Microsoft Intune 管理员控制台卸载怎么办

1.  使用 Microsoft Intune 命令行工具删除客户端软件

2.  在管理员模式中打开命令提示符。

3.  转到文件夹 *%programfiles%\Microsoft\OnlineManagement\Common* ``ProvisioningUtil.exe /UninstallAgents /MicrosoftIntune``

## 运行以下命令
客户端安装错误代码 下表描述了在客户端软件安装失败的情况下显示在“警报”  中的错误代码。

|其中包括用于解决每个错误代码所代表的问题的建议。|错误代码|可能的问题|
|--------------|--------------------|------------------------|
|**建议的解决方法**|0x80CF0437|未将客户端计算机上的时钟设置为正确的时间。|
|确保将客户端计算机上的时钟和时区设置为正确的时间和时区。|“0x80240438”、“0x80CF0438” 、“0x80CF401B”  无法连接到 Intune 服务。|检查客户端代理设置。 验证 Intune 是否支持客户端计算机上的代理配置，以及客户端计算机是否能够访问 Internet。|
|**若要深入了解受支持的代理配置，请参阅[使用适用于 Microsoft Intune 的 Endpoint Protection 帮助保障 Windows 电脑的安全](/intune/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)**|0x80CF402C 无法连接到 Intune 服务。|检查网络连接。 验证计算机是否具有网络连接。|
|**确保网络电缆保持连接状态或启用了无线网络。**|0x80240438，0x80CF0438|未配置 Internet Explorer 和本地系统中的代理设置。 检查客户端代理设置，确认客户端计算机的代理配置受 Intune 支持，且客户端计算机拥有 Internet 访问。|
|**若要深入了解受支持的代理配置，请参阅[使用适用于 Microsoft Intune 的 Endpoint Protection 帮助保障 Windows 电脑的安全](/intune/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)**|0x80043001|注册程序包过期。 从“管理员”  工作区中下载并安装最新的客户端软件包。|
|**相关说明，请参阅[使用 Microsoft Intune 安装 Windows 电脑客户端](/intune/deploy-use/install-the-windows-pc-client-with-microsoft-intune)主题。**|0x80043004|订阅不存在或被禁用。 验证你的帐户和 Intune 订阅是否仍处于活动状态。|
|**若要查看帐户设置，请在 [Office 365 管理中心](http://go.microsoft.com/fwlink/?LinkId=698854%20)中登录你的帐户**|0x80043002|帐户处于维护模式。 当帐户处于维护模式时，你无法注册新客户端计算机。|
|**若要查看帐户设置，请在 [Office 365 管理中心](http://go.microsoft.com/fwlink/?LinkId=698854%20)中登录你的帐户**|0x80043003|帐户被删除。 验证你的帐户和 Intune 订阅是否仍处于活动状态。|
|**若要查看帐户设置，请登录到你的帐户。**|0x80043005|客户端计算机被停用。 等几个小时并从计算机中删除任何较旧版本的客户端软件，然后重试客户端软件安装。|
|**有关说明，请参阅以上**如果客户端无法从 Microsoft Intune 管理员控制台卸载怎么办**。**|0x80043006|达到帐户所允许的最大座位数。|
|**贵组织必须购买附加的座位，你才能在服务中注册更多客户端计算机。**|0x80043007|在安装程序所在的文件夹中找不到证书文件。 在开始安装之前提取所有文件。 请不要重命名或重新定位任何提取的文件：所有文件必须位于同一文件夹中，否则安装将失败。|
|有关详细信息，请参阅[使用 Microsoft Intune 安装 Windows 电脑客户端](/intune/deploy-use/install-the-windows-pc-client-with-microsoft-intune)|“0x8024D015”、“0x00240005”、“0x80070BC2”、“0x80070BC9”、“0x80CFD015”|无法安装软件，因为客户端计算机的重启处于挂起状态。|
|**重启计算机，然后重试客户端软件安装。**|0x80070032|在客户端计算机上未找到用于安装客户端软件的一个或多个先决条件。 确保所有必需的更新都已安装在客户端计算机上，然后重试客户端软件安装。|
|**若要深入了解用于安装客户端软件的先决条件，请参阅 [Microsoft Intune 的网络基础结构要求](/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)**|0x80043008|无法启动 Microsoft Online Management 更新服务。|
|**请联系支持部门，如[如何获取对 Microsoft Intune 的支持](how-to-get-support-for-microsoft-intune.md)中所述**|0x80043009|已在服务中注册客户端计算机。 你必须先停用客户端计算机，然后才能在服务中重新注册该客户端计算机。|
|**相关说明，请参阅[从 Microsoft Intune 管理停用设备](/intune/deploy-use/retire-devices-from-microsoft-intune-management)**|0x8004300B|无法运行客户端软件安装包，因为不支持客户端上运行的 Windows 的版本。 Intune 不支持客户端计算机上运行的 Windows 的版本。|
|**有关受支持的操作系统的列表，请参阅 [Microsoft Intune 的网络基础结构要求](/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)**|0xAB2|Windows Installer 无法针对自定义操作访问 VBScript 运行时。 此错误是由基于动态链接库 (DLL) 的自定义操作引起的。|
|**对 DLL 进行疑难解答时，可能必须使用 [Microsoft 支持 KB198038：用于打包和部署问题的有用工具](http://go.microsoft.com/fwlink/?LinkID=234255)中描述的工具**|0x8004300f|软件无法安装，是因为已安装了 System Center Configuration Manager 客户端。|
|**删除 Configuration Manager 客户端，然后重试客户端软件安装。**|0x80043010|无法安装此软件，因为已经安装了开放移动联盟设备管理 (OMADM) 客户端。|
注销 OMADM 客户端，然后重试客户端软件安装。 如果安装问题仍然存在，请联系支持部门，如[如何获取对 Microsoft Intune 的支持](how-to-get-support-for-microsoft-intune.md)中所述。

### 使客户端计算机注册日志（位于 %*programfiles*%\Microsoft\OnlineManagement\Logs\Enrollment.log 和 %*userprofile*%\AppData\Local\Microsoft\OnlineManagement\Logs\Enrollement.log 中）和 Windows 更新日志 (%*windir*%\windowsupdate.log)可对支持工程师显示。
后续步骤


<!--HONumber=May16_HO2-->

