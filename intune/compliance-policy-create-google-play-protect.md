---
title: "使用 Intune 启用 Google Play 保护符合性"
titleSuffix: Azure portal
description: "了解如何创建用于启用 Google Play 保护的 Android 设备符合性策略。"
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: E9810BEB-000A-4DFB-B5C7-A22A92082B22
ms.reviewer: muhosabe
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: d610bc338c1bcf81ed3bc71f1357e001914c5877
ms.sourcegitcommit: 71e6e80b7370024624ce2e5fad1ca5b372975748
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-create-a-device-compliance-policy-to-enable-google-play-protect"></a>如何创建用于启用 Google Play 保护的设备符合性策略

可以针对 Android 平台创建新的符合性策略，来检查 Google Play 保护 (GPP) 符合性。

然后可以将需要这些设置的符合性策略定位到一组 Android 用户或设备。 如果设备没有启用这些设置，则不符合符合性。

## <a name="create-a-compliance-policy"></a>创建合规性策略

1. 登录到 Azure 门户。 选择“更多服务” > “监视 + 管理” + “Intune”。
2. 选择“管理”组中的“设备符合性”。 
3. 选择“策略”，然后选择“创建策略”。
4. 键入策略“名称”和“说明”。
5. 对于“平台”，选择“Android”。
6. 选择“设置” > “设备运行状况”。
7. 配置“Google Play 保护”设置。
8. 设置 Google Play 保护设置后，指定“安全性”和“设备属性”设置。 完成后，选择“确定”。

## <a name="configure-the-google-play-protect-settings"></a>配置“Google Play 保护”设置

 - **配置 Google Play Services**  
   要求安装并启用 Google Play Services 应用程序。 可通过 Google Play Services 进行安全更新，它是已获得认证的 Google 设备上的很多安全功能的基本依赖项。
 - **最新的安全提供程序**  
   要求最新的安全提供程序可以保护设备免受已知的漏洞攻击。
 - **对应用进行威胁扫描**  
   要求启用 Android“验证应用”功能。
    > [!Note]  
    > 在旧版 Android 平台上，此功能是符合性设置。 Intune 只能检查在设备级别是否启用了此设置。 在具有工作配置文件（以前称为 Android for Work）的设备上，此设置可以作为配置策略设置找到。 这允许管理员为设备启用此设置。

    如果企业使用 Android 工作配置文件，则可以为已注册的设备启用“对应用进行威胁扫描”。 建立设备配置文件，并且需要进行系统安全设置。 有关详细信息，请参阅 [Microsoft Intune 中的 Android for Work 设备限制设置](device-restrictions-android-for-work.md)。

 - **SafetyNet 设备证明**  
   设置必须满足的 SafetyNet 设备证明完整性的级别。 级别包括“未配置”、“检查基本的完整性”**和“检查基本的完整性和认证设备”**。




## <a name="next-steps"></a>后续步骤

若要了解有关使用 Intune 设备符合性策略的详细信息，请参阅 [Intune 设备符合性策略入门](device-compliance-get-started.md)。