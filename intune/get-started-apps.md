---
title: Microsoft Intune 中的应用入门
titlesuffix: ''
description: 查找应用并将其添加到设备，以便员工完成工作。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/05/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: a1542fc3-672e-47c1-a21f-82826a2f8ac4
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 6b69934edc70e10ee01394cf5b6a4fed75334660
ms.sourcegitcommit: e814cfbbefe818be3254ef6f859a7bf5f5b99123
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "43330052"
---
# <a name="get-started-with-adding-apps-in-microsoft-intune"></a>在 Microsoft Intune 中添加应用入门

必须首先将应用添加到 Intune 中，才可以分配、监视、配置或保护它们。 Intune 支持几种不同的应用类型。 此外，每种应用类型的可用选项也各不相同。

通过 Intune，可向公司设备添加并分配以下应用类型：
- **应用商店中的应用** - 适用于需要对 App Store 中获得的应用实施额外的移动应用程序管理的设备。
- **内部编写的应用（业务线）**- 用于上传下载到用户设备的文件。
- **内置应用** - 用于向 iOS 和 Android 设备分配特选托管应用（例如 Office 365 应用）。
- **Web 上的应用** - 可供 Intune 用于在设备主屏幕上创建一个到 Web 应用的快捷方式。

> [!NOTE]
> 应用到动态设备组的新策略可能需要 8 小时才可传播到组中的所有设备。

## <a name="how-do-i-assign-a-public-store-app"></a>如何分配公共应用商店应用？

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 选择“所有服务” > “Intune”。 Intune 位于“监视 + 管理”部分中。
3. 选择“客户端应用”，然后选择“应用”。
4. 选择“添加”，然后选择“iOS”作为“应用类型”。
5. 选择“选择应用”，显示“搜索 App Store”窗格。
6. 在文本框中，搜索要分配到设备的应用。 选择应用，然后单击“选择”。
7. 在“添加应用”窗格中，选择“应用信息”，然后确保完整填入所有应用程序信息。 可添加其他可选填的详细信息，来帮助组织此应用，如“所有者”、“说明”、“开发人员”和用于公司隐私策略的“隐私 URL”。
8. 针对“在公司门户中将其显示为特色应用”，请确保选择“是”，然后选择“确定”。
9. 从“添加应用”窗格中选择“添加”，以添加该应用。 此操作将转到应用的“概述”。 选择“分配”，然后单击“添加组”以将其分配到测试组。 让应用**可供下载**。 然后在测试设备上，应用应显示为**特色应用**。


- [如何将应用分配到组](apps-deploy.md)

## <a name="learn-more"></a>了解详细信息

* [什么是使用 Intune 进行应用管理？](app-management.md)
* [应用生命周期概述](app-lifecycle.md)
* [什么是应用保护策略？](app-protection-policy.md)
