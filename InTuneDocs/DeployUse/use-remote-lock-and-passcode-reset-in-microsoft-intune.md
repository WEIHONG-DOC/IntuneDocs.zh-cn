---
title: 使用远程锁定和密码重置 | Microsoft Intune
description:
keywords:
author: NathBarn
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 970f8c81-7c7f-4789-9ed4-2133d50b9db6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:
---
# 使用远程锁定和密码重置功能帮助保护设备
Microsoft Intune 提供远程锁定和密码重置功能。

## 远程锁定设备
如果用户丢失其设备，你可以远程锁定该设备。 下表列出了在不同的移动平台上是如何远程锁定的。

|平台|远程锁定|
|------------|---------------|
|iOS|支持|
|Android|支持|
|Windows 10 移动版|支持|
|Windows Phone 8 和 Windows Phone 8.1|支持|
|Windows RT 8.1 和 Windows RT|如果设备的当前用户是注册设备的相同用户，则支持。|
|Windows 8.1|如果设备的当前用户是注册设备的相同用户，则支持。|


### 通过 Intune 控制台远程锁定移动设备

1.  在 [Intune 管理员控制台](https://manage.microsoft.com/)中，依次选择“组” &gt; ”所有设备” &gt; ”所有移动设备”。

2.  对于在 Intune 中注册的设备，选择**所有直接托管设备**或**所有 Exchange ActiveSync 托管设备**

    > [!TIP]
    > 你还可以按用户导航到设备。 选择**所有用户**。 在用户的“属性”页，选择**设备**，然后选择要擦除的移动设备的名称。

3.  在列表中，选择要锁定的某个设备或多个设备。 在任务栏上，选择**远程任务**，然后选择**远程锁定**

## 重置设备的密码
如果用户忘记密码，则你可以删除设备中的密码，或者在设备上强制使用新的临时密码，从而帮助用户解决问题。 下表列出了在不同的移动平台上是如何重置密码的。

|平台|密码重置|
|------------|------------------|
|iOS|支持以便清除设备中的密码。 不创建新的临时密码。|
|Android|支持并且创建临时密码。|
|Windows 10 移动版|支持|
|Windows Phone 8 和 Windows Phone 8.1|支持|
|Windows RT 8.1 和 Windows RT|不支持|
|Windows 8.1|不支持|

### 重置密码

1.  在 [Intune 管理员控制台](https://manage.microsoft.com/)中，依次选择**组** &gt; **所有设备** &gt; **所有移动设备**。

2.  对于在 Intune 中注册的设备，选择**所有直接托管设备**或**所有 Exchange ActiveSync 托管设备**

    > [!TIP]
    > 你还可以按用户导航到设备。 单击“所有用户”。 在用户的“属性”页，单击“设备”，然后单击你要擦除的移动设备的名称。

3.  在列表中，选择要锁定的某个设备或多个设备。 在任务栏上，选择“远程任务”，然后选择“密码重置”


### 另请参阅
停用设备


<!--HONumber=May16_HO2-->

