---
# required metadata

title: 使用 Microsoft Intune 中的设备注册管理器注册企业拥有的设备 | Microsoft Intune
description:
keywords:
author: NathBarn
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: a23abc61-69ed-44f1-9b71-b86aefc6ba03

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: jeffgilb
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用 Microsoft Intune 中的“设备注册管理器”注册企业自有设备
组织可以使用 Intune 来管理大量带有单一用户帐户的移动设备。  *设备注册管理员* 帐户是有权限注册五个以上设备的特殊 Intune 帐户。 你可以指定存储管理员或主管，例如，允许用户执行下列操作的设备注册管理员用户帐户：

-   在 Intune 中注册设备

-   登录到公司门户以获得公司应用

-   安装和卸载软件

-   配置对公司数据的访问权限

仅对不会收到电子邮件或以特定用户身份登录的设备使用设备管理器帐户。 使用设备管理器帐户管理的设备不能使用条件性访问进行配置，因为这些也是针对每个用户的方案。 存储管理员无法从公司门户重置设备。

设备注册管理员方案示例： 一家餐厅想给服务员销售点平板电脑，给厨房员工订单监视器。 员工无需访问公司数据或作为用户登录。 Intune 管理员创建设备注册管理员帐户并使用该帐户注册公司自有设备。

或者，管理员也可以将设备注册管理员凭据交给餐厅经理，允许他或她注册和管理设备。 管理员或经理可以将特定于角色的应用部署到餐厅设备。

> [!NOTE]
> 管理员还可以在 Intune 控制台中选择设备，并使用管理控制台从移动设备管理中将其停用。 注册了超过 20 个设备的设备注册管理员用户帐户在使用公司门户应用时可能会遇到问题。

## 若要将公司应用部署到设备注册管理器托管的设备，请将公司门户应用作为“必需的安装”部署到此设备注册管理器用户帐户。
创建设备注册管理器帐户 设备注册管理员帐户是有权限注册大量企业自有设备的用户帐户。

#### 只有 Intune 控制台中的用户可以是设备注册管理员。

1.  将设备注册管理员添加到 Intune

2.  转到 [Microsoft Intune 帐户门户](http://go.microsoft.com/fwlink/?LinkId=698854)并登录你的管理员帐户。

3.  单击“添加用户”。 确认已列出将成为设备注册管理员的用户帐户。 否则，则通过单击 **“新建”** 和完成添加用户过程来添加用户。 每个访问该服务的用户都必须有订阅许可证并且 *设备注册管理器* 不能是 Intune 的管理员。

4.  确定是否需要在使用此功能之前添加更多许可证。

5.  使用你的管理员登录账号登录到 [Microsoft Intune 管理控制台](http://manage.microsoft.com) 中。 在导航窗格中，单击“管理员” 并转到“管理员管理”  ，再选择“设备注册管理员” 。

6.  打开设备注册管理员页。 单击“添加…” 。

7.  打开“添加设备注册管理员”  对话框。 输入 Intune 帐户的“用户 ID”  ，然后单击“确定” 。

8.  设备注册管理员用户不能是 Intune 管理员。

## 设备注册管理器现在可以使用相同的过程注册移动设备，同最终用户在公司门户中针对 BYOD 方案采用的过程相同。

1.  从 Intune 删除设备注册管理员

2.  使用你的管理员登录帐号登录到 [Microsoft Intune 管理员门户](http://manage.microsoft.com)。 在导航窗格中，单击“管理员”  并转到“管理员管理”  ，选择“设备注册管理员” 。

3.  打开设备注册管理员页。 选择想要删除的设备注册管理员“用户”  ，然后单击“删除” 。 不会从 Intune 中删除此用户，并且 Intune 中将保留注册此用户管理的设备。

4.  删除设备注册管理员可防止该用户在 Intune 中注册更多设备。

单击“是”  ，确认删除此设备注册管理员。 删除设备注册管理器不会影响注册的设备。

-   删除设备注册管理器时：

-   注册的设备均不会受到影响

-   仍能够完全管理注册的设备

-   已删除的设备注册管理员帐户凭据仍有效，能够登录到公司门户来访问应用程序

-   已删除的设备注册管理员帐户凭据仍无法擦除或停用设备


<!--HONumber=May16_HO2-->

