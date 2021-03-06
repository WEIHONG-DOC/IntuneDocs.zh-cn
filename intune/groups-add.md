---
title: 添加用于组织用户和设备的组
titlesuffix: Microsoft Intune
description: 添加组，以便按地理位置、部门或硬件详情来组织用户和设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/26/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: f0a2b858-a824-4598-ab81-bdd8e62ac3b3
ms.reviewer: amyros
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 613d64e396e969b8b6bde76ee6c4474a60be8ba9
ms.sourcegitcommit: 5eba4bad151be32346aedc7cbb0333d71934f8cf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="add-groups-to-organize-users-and-devices"></a>添加用于组织用户和设备的组
Intune 使用 Azure Active Directory (AD) 组来管理设备和用户。 作为 Intune 管理员，可以设置适合组织需要的组。 创建组，以便按地理位置、部门或硬件特性来组织用户或设备。 使用组来管理大规模的任务。 例如，可设置用于大量用户的策略，或向一组设备部署应用。

本主题说明如何添加要在 Intune 中使用的组。

可以添加下列类型的组：
- **分配组** - 将用户或设备手动添加到静态组
- 动态组 -（使用 Azure Active Directory Premium）允许动态生成使用简单或高级规则定义的用户或设备组

## <a name="add-a-new-group"></a>添加新组

使用以下步骤来创建新组。
1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 选择“所有服务” > “Intune”。 Intune 位于“监视 + 管理”部分中。
3. 在 Intune 窗格中，选择“组”，然后在“所有组”窗格中选择“新建组”。
   ![显示“新建组”已选择的 Azure 门户的屏幕截图](./media/groups-add-new.png)
4. 指定此新组的“组类型”、“名称”和“说明”。 这些属性仅出现在管理门户中，并且不会向用户显示。

5. 选择成员身份类型：
   - **已分配**：创建一个手动分配的成员的组。 深入了解 [Azure AD 已分配的组](https://docs.microsoft.com/azure/active-directory/active-directory-groups-create-azure-portal)。
   - **动态用户**：创建使用动态查询定义的用户组。
   - **动态设备**：创建使用**动态查询**定义的设备组。

   ![Intune 组属性的屏幕截图](./media/groups-add-properties.png)

   Azure AD 允许基于定义成员身份的规则创建动态组。 了解如何[创建基于属性的动态组](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal)。

6. 可选择“启用 Office 功能”向用户组成员授予访问共享 Office 365 应用的权限。 了解有关 [Office 365 组](https://support.office.com/article/Learn-about-Office-365-groups-b565caa1-5c40-40ef-9915-60fdb2d97fa2)的详细信息。
7. 选择“创建”以添加新组。

## <a name="see-also"></a>另请参阅
- [使用 Azure Active Directory 组管理对资源的访问](https://docs.microsoft.com/azure/active-directory/active-directory-manage-groups)
- [Azure 门户中的 Intune 经典组](groups-get-started.md)
