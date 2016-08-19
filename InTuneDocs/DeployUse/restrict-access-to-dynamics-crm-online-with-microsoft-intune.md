---
title: "限制对 Dynamics CRM Online 的电子邮件访问 | Microsoft Intune"
description: "使用条件访问保护和控制对 Dynamics CRM Online 的访问。"
keywords: 
author: karthikaraman
manager: angrobe
ms.date: 07/22/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: f1c4522b-5a34-4f5a-89d2-7809c4352af7
ms.reviewer: chrisgre
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: be1ebcdf2514e45d383dd49890e0e21acf6ede44
ms.openlocfilehash: 875da922b311b06fa8a1eb8ba7207108684825d5


---

# 使用 Intune 限制对 Dynamics CRM Online 的电子邮件访问
你可以使用 Microsoft Intune 条件访问限制从 iOS 和 Android 设备对 Microsoft Dynamics CRM Online 进行访问。  Intune 条件访问包含两个组成部分：
* [设备合规性策略](introduction-to-device-compliance-policies-in-microsoft-intune.md)，设备必须符合该策略才可被视为合规。
* [条件访问策略](restrict-access-to-email-and-o365-services-with-microsoft-intune.md)，你可在其中指定设备必须满足才能访问服务的条件。

若要了解有关条件访问如何工作的详细信息，请阅读文章[限制对电子邮件、O365 服务和其它服务的访问](restrict-access-to-email-and-o365-services-with-microsoft-intune.md)。

当目标用户尝试在其设备上使用 Dynamics CRM 应用时，会进行以下评估：

![图示显示了用于确定允许还是阻止设备访问服务的决策点](../media/mdm-ca-dynamics-crm-flow-diagram.png)

需要访问 Dynamics CRM Online 的设备必须：
* 是 **Android** 或 **iOS** 设备。
* 已向 Microsoft Intune **注册**。
* **符合**任何已部署的 Microsoft Intune 合规性策略。

基于指定的条件，设备状态存储在可授予或阻止访问权限的 Azure Active Directory 中。

如果不满足条件，则用户将在登录时看到以下消息的其中一条：
* 如果设备未向 Microsoft Intune 注册，或未在 Azure Active Directory 中注册，则会显示一条消息，说明如何安装公司门户应用并进行注册。
* 如果设备不合规，则会显示一条消息，将用户定向到 Microsoft Intune 公司门户网站或公司门户应用，用户可在其中找到有关该问题及其修正方式的信息。

## 配置 Dynamics CRM Online 的条件访问  
### 步骤 1：配置 Active Directory 安全组

在开始之前，针对条件访问策略配置 Azure Active Directory 安全组。 你可以在“Office 365 管理中心”中配置这些组。 这些组将用于以用户为目标或从策略中免除用户。 如果将某个用户设定为策略的目标，则其使用的每个设备必须合规才能访问资源。

你可以指定两个用于 Dynamics CRM 策略的组类型：
* **目标组** – 包含将应用策略的用户组。
* **免除组** – 包含从策略中免除的用户组。

如果用户位于两个组中，则会将其从策略中免除。

### 步骤 2：配置和部署合规性策略
[创建](create-a-device-compliance-policy-in-microsoft-intune.md)合规性策略并将其[部署](deploy-and-monitor-a-device-compliance-policy-in-microsoft-intune.md)到将受此策略影响的所有设备。 这些将是“目标组”中的用户所使用的所有设备。

> [!NOTE]
> 将合规性策略部署到 Microsoft Intune 组，而条件访问策略以 Azure Active Directory 安全组为目标。

> [!IMPORTANT]
> 如果尚未部署合规性策略，那么设备将被视为合规。

准备就绪后，继续执行步骤 3。
### 步骤 3：配置 Dynamics CRM 策略
接下来，配置策略以要求只有托管及合规设备才能访问 Dynamics CRM。 此策略会存储在 Azure Active Directory 中。

1.  在 Microsoft Intune 管理控制台中，选择“策略”>“条件访问”>“Dynamics CRM Online 策略”。

  ![Dynamics CRM Online 条件访问策略页面的屏幕截图](../media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  选择“启用条件访问”策略。
3.  在“应用程序访问”下，可以选择将条件性访问策略应用到：
  * **iOS**
  * **Android**
4.  在“目标组”下，选择“修改”以选择将应用策略的 Azure Active Directory 安全组。 你可以选择将此应用于所有用户或仅针对选择的用户组。
5.  或者，在“免除组”下，选择“修改”以选择从此策略中免除的 Azure Active Directory 安全组。
6.  完成后，选择“保存”。

现在你已配置了Dynamics CRM 的条件访问。 不需要部署条件访问策略，它将立即生效。
##  监视遵从性和条件性访问策略

在“组”  工作区中，可以查看设备的条件访问状态。

选择任何移动设备组，然后在“设备”  选项卡上，选择以下“筛选器” 之一:
* **未向 AAD 注册的设备** – 从 Dynamics CRM 阻止这些设备。
* **不合规的设备** – 从 Dynamics CRM 阻止这些设备。
* **已向 AAD 注册的合规设备** – 这些设备可以访问 Dynamics CRM。

##  后续步骤
[限制对 Exchange Online 的访问](restrict-access-to-exchange-online-with-microsoft-intune.md)

[限制对 Exchange 内部部署的访问](restrict-access-to-exchange-onpremises-with-microsoft-intune.md)
[限制对 SharePoint Online 的访问](restrict-access-to-sharepoint-online-with-microsoft-intune.md)

[限制对 Skype for Business Online 的访问](restrict-access-to-skype-for-business-online-with-microsoft-intune.md)



<!--HONumber=Jul16_HO5-->

