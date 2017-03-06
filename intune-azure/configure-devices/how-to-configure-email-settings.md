---
title: "如何配置 Intune 电子邮件设置"
titleSuffix: Intune Azure preview
description: "Intune Azure 预览版：了解如何配置 Intune 以在托管的设备上创建与公司电子邮件的连接。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 484bd9b0-fbf1-4f4f-940c-6b12fa07e228
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: 153cce3809e24303b8f88a833e2fc7bdd9428a4a
ms.openlocfilehash: e9d1c64ef617a134f05c3e80c23145fd1fdc5399
ms.lasthandoff: 02/18/2017


---

# <a name="how-to-configure-email-settings-in-microsoft-intune"></a>如何在 Microsoft Intune 中配置电子邮件设置

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

电子邮件配置文件设置可用于配置使用连接和同步公司电子邮件所需的设置管理的设备。 这有助于确保设置在所有设备中是标准的，还有助于减少对不了解正确电子邮件设置的最终用户的支持呼叫。

大多数平台支持内置邮件客户端。 当前不支持大多数第三方电子邮件应用。

你可以使用电子邮件配置文件配置下列设备类型上的本机电子邮件客户端：

- Android 4.0 及更高版本
- iOS 8.0 及更高版本
- Windows Phone 8.1 及更高版本
- Windows 10（桌面版）和 Windows 10 移动版

使用本主题中的信息了解有关配置电子邮件配置文件的基础知识，然后阅读有关每个平台的深入主题以了解设备规范。

## <a name="create-a-device-profile-containing-email-settings"></a>创建包含电子邮件设置的设备配置文件

1. 登录到 Azure 门户中。
2. 选择“更多服务” > “其他” > “Intune”。
3. 在“Intune”边栏选项卡上，选择“配置设备”。
2. 在“设备配置”边栏选项卡上，选择“管理” > “配置文件”。
3. 在配置文件边栏选项卡上，选择“创建配置文件”。
4. 在“创建配置文件”边栏选项卡上，输入电子邮件配置文件的“名称”和“说明”。
5. 从“平台”下拉列表中，选择要应用电子邮件设置的设备平台。 目前，可以为电子邮件设备设置选择以下平台之一：
    - **Android**
    - **iOS**
    - **Windows Phone 8.1**
    - **Windows 10 及更高版本**
6. 在“配置文件”键入下拉列表中，选择“电子邮件”。
7. 根据所选择的平台，可配置的设置将有所不同。 有关每个平台的详细设置，请转到以下主题之一：
    - [Android 设置](email-profile-settings-for-android.md)
    - [iOS 设置](email-profile-settings-for-ios.md)
    - [Windows Phone 8.1 设置](email-profile-settings-for-windows-phone-8-1.md)
    - [Windows 10 设置](email-profile-settings-for-windows-10.md)
8. 完成后，返回“创建配置文件”边栏选项卡，然后点击“创建”。

将创建配置文件并在“配置文件列表”边栏选项卡上显示。
如果想要继续操作并将此配置文件分配到组，请参阅[如何分配设备配置文件](how-to-assign-device-profiles.md)。

## <a name="further-information"></a>更多信息

### <a name="remove-an-email-profile"></a>删除电子邮件配置文件

如果想要从设备中删除电子邮件配置文件，请编辑分配并删除包含该设备的任何组。 请注意，如果电子邮件配置文件是设备上唯一的电子邮件配置文件，则无法通过此方法将其删除。

### <a name="securing-email-access"></a>保护电子邮件访问权限

可以使用以下两种方法之一来帮助保护电子邮件配置文件：

1. **证书** - 创建电子邮件配置文件时，可以选择之前在 Intune 中创建的证书配置文件。 该配置文件又称为身份证书，用于根据受信任的证书配置文件（或根证书）进行身份验证，以确定用户的设备可以连接。 受信任的证书会部署到对电子邮件连接进行身份验证的计算机（通常是本机邮件服务器）。
有关如何在 Intune 中创建和使用证书配置文件的详细信息，请参阅[如何使用 Intune 配置证书](/intune-azure/configure-devices/how-to-configure-certificates)。
2. **用户名和密码** - 用户通过提供其用户名和密码向本机邮件服务器进行身份验证。
密码不包含在电子邮件配置文件中，因此用户在连接到电子邮件时需要提供密码。


### <a name="how-intune-handles-existing-email-accounts"></a>Intune 如何处理现有电子邮件帐户

如果用户已配置电子邮件帐户，Intune 电子邮件配置文件分配结果将取决于设备平台：

- **iOS**：基于主机名和电子邮件地址检测到现有的重复电子邮件配置文件。 重复的电子邮件配置文件将阻止分配 Intune 配置文件。 在这种情况下，公司门户将通知用户其不符合规定并提示用户手动删除已配置的配置文件。 若要帮助防止此问题，请告知用户在安装电子邮件配置文件前进行注册，这可允许 Intune 设置配置文件。
- **Windows**：基于主机名和电子邮件地址检测到现有的重复电子邮件配置文件。 Intune 会覆盖由用户创建的现有电子邮件配置文件。
- **Android**：基于电子邮件地址检测到现有的重复电子邮件帐户，并使用 Intune 配置文件将其覆盖。
由于 Android 不使用主机名来识别配置文件，因此我们建议不要创建多个电子邮件配置文件并在不同主机的同一邮件地址中使用，因为它们会相互覆盖。
