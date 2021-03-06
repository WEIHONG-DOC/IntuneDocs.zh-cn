---
title: iOS 用户如何获取其应用
description: 使 iOS 应用可供最终用户使用的方法
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/28/2016
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 7744d8422e774242e0883c8d77814c42fd71895f
ms.sourcegitcommit: 2198a39ae48beca5fc74316976bc3fc9db363659
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38224819"
---
# <a name="how-your-ios-users-get-their-apps"></a>iOS 用户如何获取其应用

[!INCLUDE [both-portals](./includes/note-for-both-portals.md)]

使用此信息可了解最终用户如何以及在何处获取你通过 Microsoft Intune 分发的应用。

**必需应用** -- 管理员所要求并且在用户参与程度最小的情况下安装在设备上的应用（具体取决于平台）。

**可用应用** -- 在公司门户应用列表中提供的应用和用户可以根据需要选择安装的应用。

**托管应用** - 可通过策略管理，并由 Intune“包装”或使用 Intune 应用软件开发工具包 (SDK) 生成的应用。 这些应用可以由 Intune 进行管理，应用保护策略可以应用于它们。

**非托管应用** - 可通过策略管理，并且未由 Intune 包装或不包含 Intune App SDK 的应用。 应用程序策略不能应用于这些应用。

Apple 限制禁止公司门户应用列出业务线应用和托管应用商店应用。 要解决这一问题，用户可根据 iOS 公司门户应用中磁贴的指示，在同一位置（公司门户网站）切换到其他视图，以查看所有应用。

在公司门户应用上的“应用”屏幕上，已注册用户可以通过点击以下磁贴获取他们的应用：

- **所有应用**指向[公司门户网站](https://portal.manage.microsoft.com)“全部”选项卡中所有应用的列表。

- **特色应用**使用户进入公司门户网站的“特别推荐”选项卡。

- **类别**指向公司门户网站的“类别”选项卡。


![iOS 公司门户应用屏幕](./media/ios-cp-app-main-apps-screen.png)

有关如何添加应用的相关信息，请参阅[如何将应用添加到 Microsoft Intune](apps-add.md)。

### <a name="see-also"></a>另请参阅
[Android 用户如何获取其应用](end-user-apps-android.md)

[Windows 用户如何获取其应用](end-user-apps-windows.md)
