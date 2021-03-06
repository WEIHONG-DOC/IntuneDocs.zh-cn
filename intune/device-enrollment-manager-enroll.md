---
title: 使用设备注册管理员帐户注册设备
titlesuffix: Microsoft Intune
description: 使用设备注册管理器帐户在 Intune 中注册设备。 "
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd
ms.reviewer: damionw
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: ce785ad7898f9e792feeadcd1623bd0989f0d6d0
ms.sourcegitcommit: 40b1d82df99f09a75a17065cdd0e84d8038f460a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "40255534"
---
# <a name="enroll-devices-by-using-a-device-enrollment-manager-account"></a>通过使用设备注册管理员帐户注册设备

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

组织可以使用 Intune 来管理大量带有单一用户帐户的移动设备。 设备注册管理器 (DEM) 帐户是可注册最多 1,000 台设备的特殊用户帐户。 将现有用户添加到要为其提供专用 DEM 选项的 DEM 帐户。 每台已注册设备均使用单一许可证。 我们建议将通过此帐户注册的设备用作共享设备，而不是个人 ("BYOD") 设备。  

用户必须在 [Azure 门户](https://portal.azure.com)中存在才能添加为设备注册管理员。 为获得最佳安全性，DEM 用户也不应是 Intune 管理员。

>[!NOTE]
>DEM 注册方法不能与以下其他注册方法一起使用：[Apple Configurator 与设置助手](apple-configurator-setup-assistant-enroll-ios.md)、[Apple Configurator 与直接注册](apple-configurator-direct-enroll-ios.md)、[Apple School Manager (ASM)](apple-school-manager-set-up-ios.md)，或[设备注册计划 (DEP)](device-enrollment-program-enroll-ios.md)。

## <a name="example-of-a-device-enrollment-manager-scenario"></a>设备注册管理器方案示例

一家餐厅想为服务员提供 50 台销售点平板电脑，为厨房员工提供订单监视器。 员工无需访问公司数据或以用户身份登录。 Intune 管理员将为餐厅主管创建新的设备注册管理员帐户。  此帐户独立于主管的主帐户，仅用于使用 Intune 注册共享设备。 现在主管便可使用 DEM 凭据注册这 50 台平板电脑。

只有 [Azure 门户](https://portal.azure.com)中的用户可以成为设备注册管理员。 设备注册管理器用户不能充当 Intune 管理员。

DEM 用户可以：

-   在 Intune 中最多注册 1000 台设备
-   登录到公司门户以获得公司应用
-   通过向平板电脑部署特定于角色的应用来配置对公司数据的访问权限

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>使用 DEM 帐户注册的设备限制

使用设备注册管理器帐户注册的设备具有以下限制：

  - 不是每一个用户都可以访问。 因为设备没有分配的用户，所以设备没有电子邮件或公司数据访问权限。 例如，VPN 配置等仍可用于向设备应用提供数据访问权限。
  - DEM 用户无法在设备本身上使用公司门户注销 DEM 注册的设备。 Intune 管理员可以取消注册。
  - 公司门户应用或网站中仅显示本地设备。
  - 用户无法通过用户许可证使用 Apple Volume Purchase Program (VPP) 应用，因为每个用户都需具有 Apple ID 才可管理应用。
  - （仅限 iOS）如果使用 DEM 注册 iOS 设备，则无法使用 Apple Configurator、Apple 设备注册计划 (DEP) 或 Apple School Manager (ASM) 注册设备。
  - （仅限 Android）使用单个 DEM 帐户注册 Android 工作配置文件设备时，可注册的设备数量有限。 每个 DEM 帐户最多可注册 10 台 Android 工作配置文件设备。 旧版 Android 注册不受此限制。
  - 如果设备具有设备许可证，则可以安装 VPP 应用。
  - 无需 Intune 设备许可证，即可使用 DEM。 详细了解[用户和设备许可证](licenses-assign.md#how-user-and-device-licenses-affect-access-to-services)。


> [!NOTE]
> 你可以将公司应用部署到设备注册管理器管理的设备。 将公司门户应用以“必需安装”的形式部署到设备注册管理器的用户帐户。
> 为提高性能，在 DEM 设备上查看公司门户应用将仅显示本地设备。 仅可通过 Intune 管理控制台执行其他 DEM 设备的远程管理。


## <a name="add-a-device-enrollment-manager"></a>添加一个设备注册管理器

1.  在 [Azure 门户中的 Intune](https://aka.ms/intuneportal) 中，选择“设备注册” > “设备注册管理员”。

2.  选择“添加”。

3.  在“添加用户”边栏选项卡上，输入 DEM 用户的用户主体名称，并选择“添加”。 DEM 用户将添加到 DEM 用户列表。

## <a name="permissions-for-dem"></a>DEM 的权限

需要全局或 Intune 服务管理员 Azure AD 角色
- 完成管理门户中与 DEM 注册相关的任务
- 尽管在自定义用户角色下列出了可用的 RBAC 权限，但还需要查看全部 DEM 用户。

未分配到全局管理员或 Intune 服务管理员角色，但具有设备注册管理器角色读取权限的用户，仅可查看他们创建的 DEM 用户。 将在以后公布对这些功能的 RBAC 角色支持。


## <a name="remove-a-device-enrollment-manager"></a>删除设备注册管理器

删除设备注册管理器后：

-   已注册的设备不受影响，仍能继续对其进行完全管理。
-   已删除的 DEM 帐户凭据仍然有效。
-   已删除的 DEM 仍无法擦除或停用设备。
-   已删除的 DEM 仅可注册不超过 Intune 管理员配置的每用户限制数量的设备。

**删除设备注册管理器**

1. 在 [Azure 门户中的 Intune](https://aka.ms/intuneportal) 中，选择“设备注册”，然后选择“设备注册管理器”。
2. 在“设备注册管理员”边栏选项卡上，选择 DEM 用户，然后选择“删除”。

