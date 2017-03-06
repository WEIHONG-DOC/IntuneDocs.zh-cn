---
title: "适用于 Windows Phone 8.1 设备的 Intune 自定义设置"
titleSuffix: Intune Azure preview
description: "Intune Azure 预览版：了解可以在 Windows Phone 8.1 自定义配置文件中使用的设置。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 21c55041-3821-4a62-9f85-855b97dba269
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: 153cce3809e24303b8f88a833e2fc7bdd9428a4a
ms.openlocfilehash: 652eca69f3e53365b75fd8590fce299209e2a12f
ms.lasthandoff: 02/18/2017


---

# <a name="custom-settings-for-windows-phone-81-devices-in-microsoft-intune"></a>Microsoft Intune 中适用于 Windows Phone 8.1 设备的自定义设置

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

使用 Microsoft Intune 的 Windows Phone 8.1 **自定义**配置文件来部署可用于控制 Windows Phone 8.1 设备功能的 OMA-URI 设置。 这些设置是许多移动设备制造商用来控制设备功能的标准设置。

此功能的目的是允许用户部署不能使用其他 Intune 策略配置的设置。

## <a name="custom-policy-settings-for-windows-phone-81-devices"></a>适用于 Windows Phone 8.1 设备的自定义策略设置

1. 按照[如何在 Microsoft Intune 中配置自定义设备设置](how-to-configure-custom-settings.md)中的说明进行操作。
2. 在“创建配置文件”边栏选项卡上，选择“设置”添加&1; 个或多个 OMA-URI 设置。
3. 在“添加行”边栏选项卡上，为每个设置配置以下值：
    - **名称** - 输入 OMA-URI 设置的唯一名称，以帮助你在设置列表中识别它。
    - **说明** - 提供对设置进行概述的说明以及帮助你找到该设置的其他相关信息。
    - **OMA-URI** 指定需为其提供设置的 OMA-URI。
    - **数据类型** - 选择将在其中指定此 OMA-URI 设置的数据类型。 从“字符串”、“日期和时间”、“整数”、“浮点”或者“布尔值”中进行选择。
    - **值** - 输入要与已输入的 OMA-URI 关联的值。

4. 完成后，单击“确定”，根据需要继续添加其他设置。
