---
title: "使用 SDK 启用针对 MAM 的应用 | Microsoft Docs"
description: "本主题简要概述了应使用 Intune App SDK 的原因。"
keywords: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.date: 12/19/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 26b00081-7c05-4969-ace1-0585e44d5cd2
ms.reviewer: oydang
ms.suite: ems
ms.custom: intune-classic
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: ec4e2f966fa8c24505ce1fa74a59c95908273bd1
ms.contentlocale: zh-cn
ms.lasthandoff: 05/23/2017


---

# <a name="use-the-sdk-to-enable-apps-for-mobile-application-management"></a>使用 SDK 启用针对移动应用程序管理的应用

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

使用 Microsoft Intune App SDK 来允许 Intune管理 iOS 或 Android 应用的某些功能。 启用应用后，即可向应用部署策略。 这些策略使用这些功能来帮助保护公司数据。 可使用 SDK 实现的保护功能类型的示例包括：

-   防止用户将公司文档复制到云中。

-   要求对应用保存到设备的数据进行加密。

-   强制使用托管浏览器。

-   从应用远程擦除公司数据。

你需要访问应用的源代码才可使用 SDK，但你可启用大部分 SDK 功能而无需更改应用的行为。

有关 SDK 的概述，请参阅[概述](/intune-classic/develop/intune-app-sdk-get-started)。

### <a name="see-also"></a>另请参阅
[决定如何使用 Microsoft Intune 为移动应用程序管理准备应用](decide-how-to-prepare-apps-for-mobile-application-management-with-microsoft-intune.md)
