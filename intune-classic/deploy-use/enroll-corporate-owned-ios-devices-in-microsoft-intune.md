---
title: "注册企业自有的 iOS 设备 | Microsoft Docs"
description: "使用 Apple 设备注册程序 (DEP) 或 Apple 配置器注册企业自有的 iOS 设备"
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 02/21/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 2d3ca4ab-f20c-4d56-9413-f8ef19cf0722
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-classic
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 44b4fbad45decde806fb5be41ea12f0d8bcf9c95
ms.contentlocale: zh-cn
ms.lasthandoff: 05/23/2017


---

# <a name="enroll-corporate-owned-ios-devices-in-microsoft-intune"></a>在 Microsoft Intune 中注册企业所有的 iOS 设备

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

Microsoft Intune 支持注册公司所有的 iOS 设备，方法是使用 Apple 的设备注册程序 (DEP)，或在 Mac 计算机上运行的 [Apple 配置器](https://go.microsoft.com/fwlink/?LinkId=518017)工具。

**先决条件：**[Apple Push Notification 服务证书](set-up-ios-and-mac-management-with-microsoft-intune.md)

可通过以下三种方式之一注册公司拥有的 iOS 设备：

- Apple Configurator，使用设置助理或直接注册
- 设备注册计划
- 公司门户应用

>[!NOTE]
>Apple Configurator 和设备注册计划注册方法不能与[设备注册管理器](enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune.md)方法共同使用。

默认情况下，所有 iOS 设备都可在 Intune 中进行注册。 若要阻止个人或公司拥有的设备进行注册，请使用管理员凭据登录 [Microsoft Intune 管理门户](https://manage.microsoft.com)。 选择“管理” > “移动设备管理” > “注册规则”，然后清除相应选项。

## <a name="use-apple-configurator"></a>使用 Apple 配置器

可通过导出公司注册配置文件，然后将那些移动设备连接到运行 Apple 配置器的 Mac 来注册 iOS 设备。 Apple 配置器支持两种形式的注册：

- “**设置助理注册**”：将设备重置为出厂设置，使其准备好由设备的新用户进行设置。 此方法要求管理员通过 USB 将 iOS 设备连接到运行 [Apple 配置器](https://go.microsoft.com/fwlink/?LinkId=518017) 的 Mac 计算机以预配置注册。 然后，将设备提供给运行设置助理过程的用户。 此过程使用工作或学校凭据配置该设备，并完成注册过程。 有关详细信息，请参阅[使用 Apple 配置器和设置助理注册 iOS 设备](ios-setup-assistant-enrollment-in-microsoft-intune.md)。

- **直接注册**：在设备准备过程中创建 Apple 配置器兼容文件以供使用。 已注册设备没有进行出厂重置，但没有用户隶属关系。 此方法要求管理员通过 USB 将 iOS 设备连接到运行 [Apple 配置器](https://go.microsoft.com/fwlink/?LinkId=518017)的 Mac 计算机以注册设备。 有关详细信息，请参阅[使用 Apple 配置器直接注册注册 iOS 设备](ios-direct-enrollment-in-microsoft-intune.md)。

## <a name="use-the-device-enrollment-program-dep"></a>使用设备注册程序 (DEP)
DEP 将注册配置文件“无线”部署到通过 DEP 购买的设备。 用户在设备上运行设置助理时，设备会在 Intune 中进行注册。 有关详细信息，请参阅[注册设备注册程序 iOS 设备](ios-device-enrollment-program-in-microsoft-intune.md)。

## <a name="use-the-company-portal-on-dep-enrolled-or-apple-configurator-enrolled-devices"></a>在注册了 DEP 或 Apple 配置器的设备上使用公司门户

配置了用户关联的设备可以安装和运行公司门户应用，以下载应用和管理设备。 用户收到设备后，必须完成一些其他步骤，以便完成设置助理并安装公司门户应用。

需要关联用户才可支持以下内容：
  - 移动应用程序管理 (MAM) 应用
  -    对电子邮件和公司数据的条件性访问
  -    公司门户应用

**用户如何注册具有用户关联的公司所有的 iOS 设备**
1. 用户打开设备时，系统会提示其完成设置助理。 安装过程中，系统会提示用户输入其凭据。 用户必须使用与其在 Intune 中的订阅相关的凭据（即唯一的个人名称或 UPN）。

2. 安装过程中，系统会提示用户输入 Apple ID。 必须提供 Apple ID 才能允许设备安装公司门户。 设置完成后，他们还可以提供 iOS 设置菜单中的 ID。

3. 完成设置后，iOS 设备必须从应用商店安装公司门户应用。

4. 现在用户可以使用在设置设备时使用的 UPN 登录公司门户。

5. 登录后，系统会提示用户注册其设备。 第一步是识别其设备。 应用会提供一份已为公司注册并已被分配到用户的 Intune 帐户的 iOS 设备列表。 他们应选择匹配的设备。

  如果该设备还不是公司注册的设备，他们应选择“**新设备**”以使用标准注册流程继续操作。

6. 在下一个屏幕上，用户必须确认新设备的序列号。 用户可以点击“**确认序列号**”链接以启动设置应用来验证序列号。 然后用户必须将序列号的最后 4 个字符输入到公司门户应用中。

  此步骤验证该设备是否是在 Intune 中注册的企业设备。 如果设备上的序列号不匹配，则选择了错误的设备。 用户需返回到上一屏幕并选择其他设备。

7. 验证序列号后，公司门户应用将重定向到公司门户网站以完成注册。 然后该网站会提示用户返回到应用。

8. 注册现已完成。 现在用户可以使用此设备的完整功能集。

### <a name="about-corporate-owned-managed-devices-with-no-user-affinity"></a>有关无用户关联的企业拥有的托管设备

配置为无用户关联的设备不支持公司门户，并且不应安装应用。 公司门户适用于具有企业凭据的用户，并且需要访问个性化企业资源（例如邮件）的权限。 注册为无用户关联的设备并不具有专用的用户登录。 展台、销售点 (POS) 或共享实用程序设备是注册为“无用户关联”的设备的典型用例。

如果需要用户关联，注册设备前请确保设备的注册配置文件选中“**用户关联**”。 若要更改设备的关联状态，必须停用并重新注册设备。



### <a name="see-also"></a>另请参阅
[在 Microsoft Intune 中注册设备的先决条件](prerequisites-for-enrollment.md)
