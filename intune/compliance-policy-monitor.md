---
title: "监视 Intune 设备符合性策略"
titleSuffix: Intune Azure preview
description: "Intune Azure 预览版：了解如何监视设备符合性策略。"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 03/10/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 503d1dd2-a647-4aea-bf48-55319a3dd8a7
ms.reviewer: muhosabe
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 9c57a45ed93b12c3b9fd9635bfa1aec465f63bbc
ms.contentlocale: zh-cn
ms.lasthandoff: 05/23/2017


---
# <a name="monitor-intune-device-compliance-policies"></a>监视 Intune 设备符合性策略

符合性报告可帮助管理员分析其组织中设备的符合性状态，并快速解决组织内用户遇到的符合性相关的问题。 你可以查看有关设备的整体符合性状态、各设置的符合性状态、各策略的符合性状态，并向下钻取到各设备，以查看影响设备的特定设置和策略。

## <a name="before-you-begin"></a>在开始之前

按照以下步骤在 Azure 门户中查找 **Intune 设备符合性仪表板**：

1.  转到 [Azure 门户](https://portal.azure.com)，然后使用 Intune 凭据登录。

2.  从左侧菜单中选择“**更多服务**”，然后在文本框筛选器中键入 **Intune**。

3.  选择“ **Intune** ”&gt;“**设备符合性**”&gt;“**概述**”，“**设备符合性仪表板**”将打开。

> [!IMPORTANT] 
> 设备必须注册到 Intune 才能接收设备符合性策略。

## <a name="device-compliance-dashboard"></a>设备符合性仪表板

在“**设备符合性仪表板**”中，你可以监控设备符合性策略状态，该状态在不同的磁贴中提供不同的报告，可为组织中的设备提供符合性状态。 你可以查看以下报告：

-   整体设备符合性汇总

-   基于策略的设备符合性

-   基于设置的设备符合性

![设备符合性仪表板](./media/idc-1.png)

你还可以查看适用于单个设备的特定符合性策略和设置，以及设备上每个设置的最终符合性状态。

### <a name="overall-device-compliance-aggregate-report"></a>整体设备符合性汇总报告

它是一个环形图，显示所有 Intune 已注册设备的汇总符合性状态。 设备符合性状态保存在 Intune 和 Azure Active Directory 这两个不同的数据库中。 以下是有关设备符合性策略状态的详细信息：

-   **符合**：设备已成功应用管理员指定的一个或多个设备符合性策略设置。

-   **不符合**：设备未能应用由管理员指定的一个或多个设备符合性策略设置，或用户未遵守管理员指定的策略。

-   **宽限期：**管理员已使用一个或多个设备符合性策略设置指定设备，但用户尚未应用该策略，这意味着设备不符合，但它处于管理员所定义的宽限期内。

    -   详细了解针对不符合设备的操作。

-   **设备未同步：**设备未能报告其设备符合性策略状态，原因为以下几项之一：

    -   **未知**：由于其他原因，设备脱机或无法与 Intune 或 Azure AD 通信。

    -   **错误**：设备无法与 Intune 和 Azure AD 通信，并收到一条注明原因的错误消息。

> [!IMPORTANT] 
> 已注册到 Intune 但未由任何设备符合性策略指定的设备将包含在位于**符合性**存储桶下的此报告中。

#### <a name="drill-down-option"></a>向下钻取选项

在**设备符合性仪表板**中，如果单击“设备符合性”磁贴，则可以向下钻取到每个设备（由设备符合性策略指定）的**符合性状态**、**用户的电子邮件别名**、**设备模型**和**位置**。

![设备符合性仪表板向下钻取](./media/idc-2.png)

如果需要有关特定用户的详细信息，可以通过键入用户电子邮件别名来筛选“设备符合性”图表报告。

![设备符合性仪表板特定用户](./media/idc-3.png)

还可以在设备符合性图表上单击不同的符合性状态，查看有关用户设备符合性策略状态的详细信息。

![设备符合性仪表板不同的状态](./media/idc-4.png)

#### <a name="filter"></a>Filter

如果单击“**筛选器**”按钮，筛选器弹出窗口会打开，并显示以下选项：

-   型号

    -   接受自由格式的搜索字符串的文本框
<br></br>
-   平台

    -   Android

    -   iOS

    -   Mac OS

    -   Windows

    -   Windows Phone

-   状态

    -   是否满足条件

    -   不符合

    -   处于宽限期

    -   Unknown

    -   错误

如果单击“**更新**”按钮，弹出窗口应关闭，结果应根据所选的筛选条件进行更新。

![筛选器更新按钮](./media/idc-5.png)

##### <a name="device-details"></a>设备详细信息

单击设备，打开选定设备的“**设备**”边栏选项卡。 这将提供有关应用于该设备的设备符合性策略设置的详细信息。

![设备符合性仪表板](./media/idc-6.png)

在设备策略设置上单击时，可以看到来源于管理员指定的设备符合性设置的设备符合性策略名称。

![设备符合性设置名称](./media/idc-7.png)

### <a name="per-policy-device-compliance-report"></a>基于策略的设备符合性报告

此报告提供每个符合性策略视图以及每个符合性状态下的设备总数。 **设备符合性仪表板**提供**策略符合性**磁贴，其中显示了管理员先前创建的所有策略、应用策略的平台、符合设备的数量以及不符合设备的数量。

![基于策略的设备符合性报告](./media/idc-8.png)

单击策略符合性磁贴后，接着单击其中一个设备符合性策略，就可以看到每个设备（由该设备符合性策略指定）的**符合性状态**、**用户的电子邮件别名**、**设备模型**和**位置**。

![策略符合性磁贴](./media/idc-9.png)

### <a name="per-setting-device-compliance-report"></a>基于设置的设备符合性报告

可通过此报告根据符合性设置查看每个符合性状态下的设备总数。 **设备符合性仪表板**提供**设置符合性**磁贴，其中显示管理员创建的所有设备符合性策略的所有设备符合性策略设置、应用策略设置的平台以及不符合设备的数量。

![基于设置的设备符合性报告](./media/idc-10.png)

单击设置符合性磁贴后，接着单击其中一个设备符合性策略设置，将可以看到每个设备（由设备符合性策略设置指定）的**符合性状态**、**用户的电子邮件别名**、**设备模型**和**位置**。

![设置符合性磁贴](./media/idc-11.png)
