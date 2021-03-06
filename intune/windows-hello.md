---
title: 如何将 Windows Hello 企业版与 Microsoft Intune 集成
titleSuffix: ''
description: 了解如何创建策略以控制 Windows Hello 企业版在托管设备上的使用。
keywords: ''
author: msmimart
ms.author: mimart
manager: dougeby
ms.date: 08/28/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: ff3b482f974641dd7255dc98d3af62542d802de9
ms.sourcegitcommit: 4d314df59747800169090b3a870ffbacfab1f5ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43313728"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>将 Windows Hello 企业版与 Microsoft Intune 集成


[!INCLUDE [azure_portal](./includes/azure_portal.md)]

可以将 Windows Hello 企业版（以前称为 Microsoft Passport for Work）与 Microsoft Intune 集成。

 Hello 企业版是使用 Active Directory 或 Azure Active Directory 帐户取代密码、智能卡或虚拟智能卡进行登录的一种替代方法。 通过它可以使用“用户手势”取代密码进行登录。 用户手势可以是简单 PIN、Windows Hello 等生物识别身份验证或指纹读取器等外部设备。

Intune 与 Hello for Business 集成的两种方式：

-   可在“设备注册”下创建 Intune 策略。 此策略面向整个组织（租户级）。 它支持 Windows AutoPilot 全新体验 (OOBE)，并在设备注册时应用。 
-  可在“设备配置”下创建标识保护配置文件。 此配置文件面向分配的用户和设备，并在签入期间应用。 

使用本文创建面向整个组织的默认 Windows Hello 企业版策略。 要创建应用于选择用户和设备组的标识保护配置文件，请参阅[配置标识保护配置文件](identity-protection-configure.md)。  

<!--- -   You can store authentication certificates in the Windows Hello for Business key storage provider (KSP). For more information, see [Secure resource access with certificate profiles in Microsoft Intune](secure-resource-access-with-certificate-profiles.md). --->

> [!IMPORTANT]
> 在周年更新前的 Windows 10 桌面版和移动版中，可以设置两种不同的 PIN，用于对资源进行身份验证：
> - **设备 PIN** 用于解锁设备并连接到云资源。
> - **工作 PIN** 用于访问用户个人设备 (BYOD) 上的 Azure AD 资源。
> 
> 在周年更新中，这两个 PIN 合并为一个设备 PIN。
> 设置用于控制设备 PIN 的任何 Intune 配置策略，以及所配置的任何 Windows Hello 企业版策略，现在都会设置这一新的 PIN 值。
> 如果已设置这两个策略类型以控制 PIN，则 Windows Hello 企业版策略同时适用于 Windows 10 桌面和移动设备。
> 为确保解决策略冲突并正确应用 PIN 策略，请更新 Windows Hello 企业版策略以在配置策略中匹配该设置，并要求用户在公司门户应用中同步他们的设备。



## <a name="create-a-windows-hello-for-business-policy"></a>创建 Windows Hello for Business 策略

1. 在 [Azure 门户](https://portal.azure.com)中，选择“所有服务” > “监视 + 管理” > “Intune”。

2. 在“Intune”窗格中，选择“设备注册”，然后选择“Windows 注册” > “Windows Hello 企业版”。

3. 在打开的页面中，选择“默认”设置。

4. 在“所有用户”窗格中，单击“属性”，然后输入 Windows Hello 企业版设置的“名称”和可选“说明”。

5. 在“所有用户”窗格中，单击“设置”，然后为“配置 Windows Hello 企业版”选择下列某一选项：

    - “禁用”。 如果不想要使用 Windows Hello 企业版，请选择此设置。 屏幕上的所有其他设置将不可用。
    - “启用”。 如果想要配置 Windows Hello 企业版设置，请选择此设置。
    - “不配置”。 如果不想使用 Intune 来控制 Windows Hello 企业版设置，请选择此设置。 Windows 10 设备上的任何现有 Windows Hello 企业版设置不会更改。 窗格中的所有其他设置将不可用。

6. 如果在上一步中选择了“启用”，请配置应用于所有已注册 Windows 10 和 Windows 10 移动版设备的必需设置。

   - “使用受信任的平台模块 (TPM)”。 TPM 芯片额外提供了一层数据安全。<br>选择下列值之一：

     - “必需”（默认）。 仅限可访问 TPM 的设备预配 Windows Hello 企业版。
     - “首选”。 首次尝试使用 TPM 的设备。 如果不可用，他们可以使用软件加密。

   - 最小 PIN 长度/最大 PIN 长度。 将设备配置为使用你指定的最小和最大 PIN 长度，以帮助确保安全登录。 默认 PIN 长度为 6 个字符，但可以强制使用 4 个字符的最小长度。 最大 PIN 长度为 127 个字符。

   - 在 PIN 中使用小写字母/在 PIN 中使用大写字母/在 PIN 中使用特殊字符。 你可以通过要求在 PIN 中使用大写字母、小写字母和特殊字符，从而强制实施更强的 PIN。 选择：

     - “允许”。 用户可以在其 PIN 中使用该字符类型，但不强制使用。

     - “必需”。 用户在其 PIN 中必须至少包含其中一种字符类型。 例如，常见的做法是要求包含至少一个大写字母和一个特殊字符。

     - “不允许”（默认）。 用户必须在他们的 PIN 中使用这些字符类型。 （这也是不配置此设置时的行为。）<br>特殊字符包括：! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~

   - “PIN 有效期（天数）”。 比较好的一种做法是指定 PIN 的有效期，在超过此期限后，最终用户必须更改该 PIN。 默认值为 41 天。

   - “记住 PIN 历史记录”。 限制重复使用以前用过的 PIN。 默认情况下，不能重复使用最近用过的 5 个 PIN。

   - “允许生物识别身份验证”。 启用面部识别或指纹等生物识别身份验证作为 Windows Hello 企业版 PIN 的替代方法。 如果生物识别身份验证失败，则用户仍必须配置工作 PIN。 选择：

     - “是”。 Windows Hello 企业版允许进行生物识别身份验证。
     - “否”。 Windows Hello 企业版阻止生物识别身份验证（适用于所有帐户类型）。

   - “在可用时使用增强的反电子欺骗技术”。 配置是否在支持 Windows Hello 反电子欺骗功能的设备上使用该功能（例如，检测面部照片而非真实的面部）。<br>如果设置为“是”，则 Windows 将在支持反电子欺骗技术时要求所有用户对面部识别功能使用此技术。

   - **使用电话登录**。 如果将此选项设置为“是”，则用户可以使用远程 Passport 充当台式计算机身份验证的便携伴侣设备。 台式计算机必须加入 Azure Active Directory，并且伴侣设备必须配置 Windows Hello 企业版 PIN。

## <a name="windows-holographic-for-business-support"></a>Windows Holographic for Business 支持

Windows Holographic for Business 支持以下 Windows Hello for Business 设置：

- 使用受信任的平台模块 (TPM)
- 最小 PIN 长度
- 最大 PIN 长度
- 在 PIN 中使用小写字母
- 在 PIN 中使用大写字母
- 在 PIN 中使用特殊字符
- PIN 有效期（天数）
- 记住 PIN 历史记录

## <a name="further-information"></a>更多信息
有关 Microsoft Passport 的详细信息，请参阅 Windows 10 文档中的[指南](https://technet.microsoft.com/library/mt589441.aspx)。
