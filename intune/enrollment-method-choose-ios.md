---
title: "选择如何在 Intune 中注册 iOS 设备"
titleSuffix: Intune Azure preview
description: "Intune Azure 预览版：了解如何在 Microsoft Intune 中设置 iOS 设备注册。"
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: e6c0a430-1851-4108-812a-87e0fc2623b5
ms.reviewer: damionw
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: ee0ecf26a333ec441eb95e79473a9bf405e4120c
ms.contentlocale: zh-cn
ms.lasthandoff: 05/23/2017


---

# <a name="choose-how-to-enroll-ios-devices"></a>选择 iOS 设备注册方式

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

本主题介绍可用于注册 iOS 设备的方法和注册的先决条件。

使用以下信息确定哪些要用于注册 iOS 设备的方法。 除 BYOD 方法外，以下所有方法都用于注册公司拥有的设备。

**先决条件：**需要 [Apple 推送通知服务证书](apple-mdm-push-certificate-get.md)。

## <a name="user-owned-ios-devices-byod"></a>用户拥有的 iOS 设备 (BYOD)

如果用户要注册其个人、BYOD（自带设备）设备，唯一可用注册方法是让该用户从 App Store 下载适用于 iOS 的公司门户应用，然后按照应用中的注册说明进行操作。 注册后，用户可连接到公司网络、加入域或 Azure Active Directory，并有权访问公司资源。 可阻止个人拥有的 iOS 设备的注册。 请参阅 [Set device type restrictions](enrollment-restrictions-set.md#set-device-type-restrictions)（设置设备类型限制）了解相关说明。

## <a name="apple-configurator"></a>Apple Configurator

可通过导出公司注册配置文件，然后将那些移动设备连接到运行 [Apple Configurator](http://go.microsoft.com/fwlink/?LinkId=518017) 的 Mac 来注册 iOS 设备。 Apple Configurator 支持两种形式的注册：

- “**设置助理注册**”：将设备重置为出厂设置，使其准备好由设备的新用户进行设置。 此方法要求管理员通过 USB 将 iOS 设备连接到运行 Apple Configurator 的 Mac 计算机以预配置注册。 然后，将设备提供给运行设置助理过程的用户。 此过程使用用户的工作或学校凭据配置该设备，并完成注册过程。 有关详细信息，请参阅[使用 Apple Configurator 和设置助理注册 iOS 设备](apple-configurator-setup-assistant-enroll-ios.md)。

- **直接注册**：在设备准备过程中创建 Apple Configurator 兼容文件以供使用。 已注册设备没有进行出厂重置，且没有用户隶属关系。 若要注册设备，需要管理员通过 USB 将 iOS 设备连接到运行 Apple Configurator 的 Mac 计算机。 有关详细信息，请参阅[使用 Apple Configurator 直接注册注册 iOS 设备](apple-configurator-direct-enroll-ios.md)。

## <a name="use-the-device-enrollment-program-dep"></a>使用设备注册程序 (DEP)

DEP 将注册配置文件“无线”部署到通过 DEP 购买的设备。 用户在设备上运行设置助理时，设备会在 Intune 中进行注册。 用户无法注销通过 DEP 注册的设备。 有关详细信息，请参阅[使用设备注册计划注册 iOS 设备](device-enrollment-program-enroll-ios.md)。

## <a name="use-the-device-enrollment-manager-dem"></a>使用设备注册管理器 (DEM)
设备注册管理器是可注册和管理最多 1,000 台设备的用户帐户类型。 将现有用户添加到 DEM 帐户以向他们提供这些功能。 DEM 用户注册的每个设备使用各自的 Intune 许可证。 有关详细信息，请参阅[使用设备注册管理器注册设备](device-enrollment-manager-enroll.md)。
