---
title: 在管理中注册组织提供的 macOS 设备 | Microsoft Docs
description: 介绍如何在 Intune 中注册由组织购买和提供的 macOS 设备。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/29/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: japoehlm
ms.suite: ems
ms.custom: intune-enduser
ms.openlocfilehash: a5808a0ac80390b76058827d2ca0870249b043b9
ms.sourcegitcommit: 11cad61c565c474a8d653181675cc1109d562626
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2018
ms.locfileid: "43241824"
---
# <a name="enroll-your-organization-provided-macos-device-in-management"></a>在管理中注册组织提供的 macOS 设备

了解如何在 Intune 中管理新的 macOS 设备。  

工作单位或学校提供的设备通常会在分配前进行预配置。 首次打开并登录设备后，组织会将预配置的设置发送到设备。 设备完成设置后，将获得工作单位或学校资源的访问权限。 

要开始管理设置，请打开设备电源并使用工作单位或学校凭据登录。 本文的其余部分介绍使用“设置助理”过程中将看到的步骤和屏幕。   

## <a name="what-is-apple-dep"></a>什么是 Apple DEP？
组织可以通过“Apple 设备注册计划”(DEP) 购买设备。 组织可通过 Apple DEP 购买大量的 iOS 或 macOS 设备。 然后，组织可以在其首选的移动设备管理提供程序（例如 Intune）中配置和管理这些设备。 如果你是管理员并想了解有关 Apple DEP 的详细信息，请参阅[使用 Apple 设备注册计划自动注册 macOS 设备](https://docs.microsoft.com/intune/device-enrollment-program-enroll-macos)。  

## <a name="set-up-your-macos-device"></a>设置 macOS 设备  
完成以下步骤以在管理中注册 macOS 设备。 如果使用的是自己的设备，而不是组织提供的设备，请按照[个人设备和自带设备](enroll-your-device-in-intune-macos-cp.md)步骤进行操作。  

1. 打开 macOS 设备电源。 
2. 选择“语言”，然后单击“继续”。  

   ![macOS 设备设置助理“欢迎”屏幕的屏幕截图，显示可供选择的语言列表。](./media/macos-dep-welcome-1808.png)   
3. 选择键盘布局。 此列表根据所选语言显示一个或多个选项。 要查看所有布局选项，而不考虑所选语言，请单击“全部显示”。 完成后，单击“继续”。  

   ![macOS 设备设置助理“键盘布局”屏幕的屏幕截图，显示可供选择的键盘语言列表、未选中的“全部显示”选项以及“后退”和“继续”按钮。](./media/macos-dep-keyboard-1808.png)  
4. 选择 Wi-Fi 网络。 必须具有 Internet 连接才能继续设置。 如果未看到网络或需要通过有线网络进行连接，请单击“其他网络选项”。 完成后，单击“继续”。  

   ![macOS 设备设置助理“选择 Wi-Fi 网络”屏幕的屏幕截图，显示可供选择的可用网络列表。 还显示有“其他网络选项”按钮、“后退”按钮和“继续”按钮。](./media/macos-dep-wifi-1808.png)  
5. 连接 Wi-Fi 后，将显示“远程管理”屏幕。 使用远程管理，组织的管理员可以使用公司所需的帐户、设置、应用和网络对设备进行配置。 在继续操作之前，请阅读文档以帮助了解管理设备的方式。 然后单击 **“继续”**。  

   ![macOS 设备设置助理“远程管理”屏幕的屏幕截图，其中包含说明远程管理的文本以及指向文档的链接，可供了解详细信息。 还显示有“后退”按钮和“继续”按钮。](./media/macos-dep-remote-management-1-1808.png)  
6. 出现提示时，请使用工作或学校帐户登录。 进行身份验证后，设备将安装管理配置文件。 该配置文件配置并启用对组织资源的访问权限。  
7. 阅读有关 Apple 数据和隐私图标的信息，以便之后可以明确收集个人信息的情况。 然后单击 **“继续”**。  

   ![macOS 设备设置助理“数据和隐私”屏幕的屏幕截图，显示了两个人握手的图示，并介绍了 Apple 对个人信息的使用情况。 还显示有“后退”和“继续”按钮。](./media/macos-dep-apple-data-privacy-1808.png)  
8. 注册设备后，可能还需要完成其他步骤。 所见步骤取决于组织如何自定义设置体验。 它可能要求完成以下操作：
    * 登录 Apple 帐户
    * 同意条款和条件
    * 创建计算机帐户
    * 引导完成快速设置
    * 设置 Mac  
## <a name="get-the-company-portal-app"></a>获取公司门户应用      
转到 App Store 以在设备上获取 Intune 公司门户应用。 使用此应用可以监视、同步、添加并删除管理中的设备，并可安装应用。

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。
