---
title: "如何将 Android 业务线应用添加到 Intune"
titleSuffix: Intune Azure preview
description: "Intune Azure 预览版：了解如何将 Android 业务线应用添加到 Intune。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 04/12/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 061d793c-c724-4cd9-9240-adb0cbda5661
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 3758df744311392528be01c826527c2a9d879975
ms.openlocfilehash: 168b054180c4df1a66a03525222a23d97027bb84
ms.contentlocale: zh-cn
ms.lasthandoff: 05/10/2017

---

# <a name="how-to-add-android-line-of-business-lob-apps-to-microsoft-intune"></a>如何将 Android 业务线 (LOB) 应用添加到 Microsoft Intune

[!INCLUDE[azure_preview](../includes/azure_preview.md)]


## <a name="step-1---specify-the-software-setup-file"></a>步骤 1 - 指定软件安装程序文件

1. 登录到 Azure 门户中。
2. 选择“更多服务” > “监视 + 管理” > “Intune”。
3. 在“Intune”边栏选项卡上，选择“管理应用”。
4. 在“移动应用”工作负荷中，选择“管理” > “应用”。
5. 在应用列表的上方，选择“添加”。
6. 在“添加应用”边栏选项卡中，选择“业务线应用”。

## <a name="step-2---configure-the-app-package-file"></a>步骤 2 - 配置应用包文件

1. 在“添加应用”边栏选项卡上，选择“应用包”文件。
2. 在“应用包”文件边栏选项卡，选择浏览按钮，然后选择扩展名为 **.apk** 的 Android 安装文件。
3. 完成后，请选择“确定”。


## <a name="step-3---configure-app-information"></a>步骤 3 - 配置应用信息

1. 在“添加应用”边栏选项卡上，选择“应用包”文件。
2. 在“应用信息”边栏选项卡上，配置以下信息。 根据所选择的应用，此边栏选项卡中的某些值可能已自动填充：
    - **名称** — 输入应用的名称，该名称将显示在公司门户中。 请确保使用的所有应用名称都是唯一的。 如果同一应用名称存在两次，则在公司门户中将仅向用户显示其中一个应用。
    - **描述** — 为应用输入描述。 这将在公司门户中向用户显示。
    - **发行者** — 输入应用的发行者名称。
    - **最低操作系统** - 从列表中选择可安装应用的最低操作系统版本。 如果将应用分配到具有较低操作系统的设备，则不会安装该应用。
    - **类别** - 选择一个或多个内置应用类别或你创建的类别。 这可让用户在浏览公司门户时更轻松地查找应用。
    - **在公司门户中将此应用显示为特色应用** - 当用户浏览应用时，在公司门户的主页上突出显示此应用。
    - **信息 URL** -（可选）输入包含此应用相关信息的网站 URL。 将在公司门户中向用户显示该 URL。
    - **隐私 URL** -（可选）输入包含此应用相关隐私信息的网站 URL。 将在公司门户中向用户显示该 URL。
    - **开发者** -（可选）输入应用开发者的名称。
    - **所有者** -（可选）输入此应用的所有者的名称，例如，**HR 部门**。
    - **说明** - 输入要与此应用关联的任何备注。
    - **徽标** - 上载将与应用关联的图标。 用户浏览公司门户时，此图标将与应用一同显示。
3. 完成后，请选择“确定”。

## <a name="step-4---finish-up"></a>步骤 4 - 完成

1. 在“添加应用”边栏选项卡上，验证配置的信息是否正确。
2. 选择“添加”将应用上传到 Intune。

创建的应用将显示在应用列表中，可在该列表中将其分配到所选择的组。 如需帮助，请参阅[如何将应用分配到组](deploy-apps.md)。
