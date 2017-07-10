---
title: "基于应用的条件性访问与 Intune 的协作"
description: "了解基于应用的条件性访问如何与 Intune 协作的概念。"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 05/31/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: b399fba0-5dd4-4777-bc9b-856af038ec41
ms.reviewer: chrisgre
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: df3c42d8b52d1a01ddab82727e707639d5f77c16
ms.openlocfilehash: 95edaa22f90743bb2821f2f656fdb8e9013c4b35
ms.contentlocale: zh-cn
ms.lasthandoff: 06/08/2017


---

# <a name="app-based-conditional-access-with-intune"></a>基于应用的条件性访问与 Intune 的协作

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

[Intune 应用保护策略](app-protection-policy.md)可帮助保护在 Intune 中已注册设备上的公司数据。 另外，应用保护策略还可用在没有注册 Intune 进行管理的员工自有设备上。 在这种情况下，即使你的公司不管理该设备，仍需要确保公司数据和资源受保护。

通过确保仅支持 Intune 应用保护策略的移动应用可以访问 Exchange online 及其他 Office 365 服务，基于应用的条件性访问和移动应用程序管理从而增加了一个安全层。

> [!NOTE]
> 受管理应用是一种自身执行应用保护策略的应用，可由 Intune 管理。

仅允许 Microsoft Outlook 应用访问 Exchange Online 时，你可以阻止 iOS 和 Android 上的内置邮件应用。 此外，你还可以阻止未执行 Intune 应用保护策略的应用访问 SharePoint Online。

## <a name="prerequisites"></a>先决条件
在创建基于应用的条件性访问策略之前，你必须具有：

- **企业移动性 + 安全性或 Azure Active Directory Premium 订阅**，并且用户必须获得 EMS 或 Azure AD 许可。
    - 有关详细信息，请参阅[企业移动性定价页](https://www.microsoft.com/cloud-platform/enterprise-mobility-pricing)或 [Azure Active Directory 定价页](https://azure.microsoft.com/pricing/details/active-directory/)。

## <a name="supported-apps"></a>受支持的应用

- **Exchange Online**：
    - 适用于 Android 和 iOS 的 Microsoft Outlook
<br></br>
- **SharePoint Online**
    - 适用于 iOS 和 Android 的 Microsoft Word
    - 适用于 iOS 和 Android 的 Microsoft Excel
    - 适用于 iOS 和 Android 的 Microsoft PowerPoint
    - 适用于 iOS 和 Android 的 Microsoft OneDrive for Business
    - 适用于 iOS 的 Microsoft OneNote

    > [!NOTE] 
    > 基于应用的条件性访问[还支持 LOB 应用](https://docs.microsoft.com/intune-classic/deploy-use/block-apps-with-no-modern-authentication)，但这些应用需要使用 [Office 365 现代身份验证](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)。

## <a name="how-app-based-conditional-access-works"></a>基于应用的条件性访问的工作方式

在此示例中，管理员必须遵循条件性访问规则，将应用保护策略应用到 Outlook 应用，将 Outlook 应用添加到可在访问企业电子邮件时使用的已批准的应用列表。

> [!NOTE] 
> 以下流程图结构可用于其他受管理的应用。

![使用流程图的基于应用的 CA](./media/ca-intune-common-ways-3.png)

1.  用户尝试从 Outlook 应用对 Azure AD 进行身份验证。

2.  首次尝试身份验证时，用户将被重定向到应用商店来安装代理应用。 代理应用可以是适用于 iOS 的 Microsoft Authenticator，也可以是适用于 Android 设备的 Microsoft 公司门户。

    > [!NOTE]
    > 在此方案中，如果用户尝试使用本机电子邮件应用，则将被重定向到应用商店，然后安装 Outlook 应用。

3.  在设备上安装代理应用。

4.  代理应用将开启 Azure AD 注册进程，在 Azure AD 中创建一个设备记录。 这与移动设备管理 (MDM) 注册过程不同，但此记录是必须的，以便可在设备上强制执行条件性访问策略。

5.  代理应用将验证应用程序的身份。 有一个安全层，以便代理应用可验证该应用是否授权用户使用。

6.  代理应用将应用客户端 ID 作为用户身份验证过程的一部分发送到 Azure AD，以查看其是否存在于策略批准列表中。

7.  Azure AD 允许用户根据策略批准列表验证并使用应用。 如果策略批准列表中没有此应用，Azure AD 将拒绝对其进行访问。

8.  Outlook 应用与 Outlook 云服务通信，以启动与 Exchange Online 的通信。

9.  Outlook 云服务与 Azure AD 通信，以为用户检索 Exchange Online 服务访问令牌。

10.  Outlook 应用与 Exchange Online 通信，以检索用户的企业电子邮件。

11.  将企业电子邮件发送到用户的邮箱。

## <a name="next-steps"></a>后续步骤
[为 MAM 应用创建 Exchange Online 策略](app-based-conditional-access-intune-exchange-online-create.md)

[为 MAM 应用创建 SharePoint Online 策略](app-based-conditional-access-intune-sharepoint-online-create.md)

[阻止不具有新式验证的应用](app-modern-authentication-block.md)
