---
title: "针对不符合 Intune 的设备的操作"
titleSuffix: Intune on Azure
description: "了解如何创建针对不符合 Intune 的设备的操作"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 10/21/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 6d0e0c4b-a562-44f3-82a4-80eb688d4733
ms.reviewer: muhosabe
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 3adc3c01d4657accfdb5cd70970ff191d06a9aef
ms.sourcegitcommit: a1c751959c9b3d5678bd9d67007e762df30eab59
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2017
---
# <a name="automate-actions-for-noncompliance"></a>针对不符合设备的自动操作

通过“针对不符合设备的操作”，可配置按时间顺序排列的操作序列，并将其应用于不满足符合性策略条件的设备。 默认情况下，如果检测到某一设备不满足符合性策略条件，Intune 会立即将其标记为不符合，然后 Azure AD 条件访问将阻止该设备。 “针对不符合设备的操作”可让你更灵活地决定在设备不符合时如何执行操作。 例如，你可以决定不立即阻止设备，然后给予用户宽限期以符合要求。

有两种类型的操作：

-   **通过电子邮件通知最终用户**：可在向最终用户发送电子邮件通知之前，事先对其进行自定义。 Intune 提供对主题、邮件正文的自定义，包括公司徽标、联系人信息和其他收件人。

-   **将设备标记为不符合**：可在设备被标记为不符合之后的几天内确定计划。 这可以即刻执行，但也可以给予用户宽限期，等待其设备满足设备符合性策略。

## <a name="before-you-begin"></a>在开始之前

你需要创建至少一个设备符合性策略，以设置针对不符合设备的操作。

-   了解如何为以下系统创建设备符合性策略：

    -   [Android](compliance-policy-create-android.md)

    -   [Android for Work](compliance-policy-create-android-for-work.md)

    -   [iOS](compliance-policy-create-ios.md)
    
    -   [macOS](compliance-policy-create-mac-os.md)

    -   [Windows](compliance-policy-create-windows.md)

若要使用设备符合性策略来阻止设备使用公司资源，请先设置 Azure AD 条件访问。

- 了解[如何设置 EMS 条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)。

此外，需要创建通知消息模板。 在稍后创建针对不符合设备的操作以向用户发送电子邮件时，将使用通知消息模板。

### <a name="to-create-a-notification-message-template"></a>创建通知消息模板

1. 转到 [Azure 门户中的 Intune](https://portal.azure.com)，然后使用 Intune 凭据登录。

2. 从左侧菜单中选择“**更多服务**”，然后在文本框筛选器中键入 **Intune**。

3. 选择“Intune”

4. 选择“设备符合性”，然后选择“管理”部分下的“通知”。

5. 选择“创建通知”，然后输入以下内容：

    a.  Name

    b。  使用者

    c.  Message

    d.  电子邮件标头 – 包括公司徽标

    e.  电子邮件页脚 – 包括公司名称

    f.  电子邮件页脚 - 包括联系人信息

![通知消息模板示例](./media/actionsfornoncompliance-1.PNG)

在完成信息添加后，选择“创建”。 就可以使用“通知”消息模板了。

> [!NOTE] 
> 你还可以编辑先前创建的“通知”模板。

## <a name="to-create-actions-for-non-compliance"></a>创建针对不符合设备的操作

> [!TIP]
> 默认情况下在针对不符合设备的操作中，Intune 会提供一个预定义的操作。 当检测到设备不满足设备符合性策略条件时，此操作会将该设备标记为不符合。 可以自定义在检测的多长时间后将设备标记为不符合。 此操作无法删除。

可以在创建新的设备符合性策略或编辑现有设备符合性策略时添加操作。

1.  在 Intune 工作负载的“设备符合性策略”边栏选项卡中，选择“管理”部分下的“策略”。

2.  通过单击选择一个设备符合性策略，然后选择“管理”部分下的“属性”。

3.  打开“**设备符合性策略属性**”边栏选项卡后，选择“**针对不符合设备的操作**”。

4.  打开“针对不符合的操作”边栏选项卡后，选择“**添加**”指定操作参数。 可选择先前创建的消息模板、其他收件人和宽限期计划。 可在计划中指定天数（0 到 365），然后可强制执行条件访问策略。 如果指定 0 天，意味着一旦设备不符合设备符合性策略，条件访问必须立即阻止其访问企业资源。

5.  在完成信息添加后，依次选择“添加”和“确定”。

## <a name="next-steps"></a>后续步骤

可在设备符合性边栏选项卡中，通过运行报告来监视设备符合性活动。 详细了解[如何使用 Intune 监视设备符合性](device-compliance-monitor.md)
