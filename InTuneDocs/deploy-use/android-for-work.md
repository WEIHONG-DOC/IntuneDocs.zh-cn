---
title: "关于 Android for Work | Microsoft Intune"
description: "Intune 管理 Android for Work，在用户将其 Android 设备用于工作时提供其他管理功能和隐私。"
keywords: 
author: nathbarn
manager: angrobe
ms.date: 11/29/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: aa0002d9-f5a0-466e-98ac-3970cb77e3a2
translationtype: Human Translation
ms.sourcegitcommit: 83914246bde673b188ca3f7d9cf50b4d0de2edd4
ms.openlocfilehash: 127db326fc96625c719b8136964bae014a904b3d


---

# <a name="manage-android-for-work-devices-with-intune"></a>使用 Intune 管理 Android for Work 设备

Android for Work 是一组 Android 设备功能和服务。 这些功能和服务在用户将其 Android 设备用于工作时提供其他管理功能和隐私。 Intune 可帮助用户将应用和公司资源部署到 Android for Work 设备，确保将工作和个人信息分开。 部署成功后，他们访问的应用和数据仍单独保留在设备上的 Android for Work 环境中。

[!INCLUDE[wit_nextref](../includes/afw_rollout_disclaimer.md)]

## <a name="supported-devices"></a>支持的设备

Android for Work 需要较新版本的 Android 硬件，因为许多管理功能依赖于较新 Android 操作系统中的功能。 目前，运行 Android 5.0 Lollipop 及更高版本的设备和具有工作配置文件支持的设备支持 Android for Work。 对于不具有 Android for Work 本机支持的设备，传统 Android 管理仍然可用。 详细了解 [Android for Work 的要求](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)。

## <a name="onboarding"></a>载入

注册 Android for Work 设备前，必须完成一些载入步骤。 这些步骤将在 Intune 租户和 Google Play for Work 服务之前建立连接，这是 Android for Work 应用分发和管理过程中不可或缺的一部分。 详细了解[启用 Android for Work 注册](https://docs.microsoft.com/en-us/intune/deploy-use/set-up-android-for-work)。

## <a name="work-profile-management"></a>工作配置文件管理

使用 Intune 管理 Android for Work 设备时，不会管理整个设备。 管理功能只会对在注册期间创建的工作配置文件有影响。 使用 Intune 部署到设备上的任何应用都是工作配置文件的一部分。 工作配置文件中的应用图标显示为橙色公文包。 此标记将设备上的公司应用与个人应用区分开来。 设备中 Android for Work 部分以外的所有 Android 应用和数据保留为个人，且受最终用户的控制。 用户可将任何所选应用安装到设备的个人端，而管理员可管理和监视限于工作配置文件的操作。

## <a name="app-publishing-and-distribution"></a>应用发布和分发

Google Play for Work 服务是应用分发和管理的必要组成部分。 所有部署到工作配置文件中 Android for Work 设备上的应用都来自 Play for Work。 若要管理和部署 Play Store 中的应用，需以 Intune 管理员的身份登录到 Play for Work 网站，为 Intune 租户核准应用。 这些应用将同步到 Intune 控制台中，然后可在控制台中使用 Intune 进行部署和管理。 组织开发的业务线 (LOB) 应用必须使用 Google Android 应用发布控制台发布到 Play for Work。 业务线应用必须在 Android 应用发布控制台中进行配置，限制对组织的访问。

应用安装无需用户交互，且不要求用户允许**从未知源安装**。 若要浏览和安装可选或可用应用，用户应在其设备上安装带工作徽章的 Play Store 应用。 详细了解[为 Android for Work 部署应用](https://docs.microsoft.com/en-us/intune/deploy-use/android-for-work-apps)。

## <a name="app-configuration"></a>应用配置

Android for Work 提供基础结构，用于将应用配置值部署到支持它们的应用。 通过为工作应用指定配置值，确保在用户首次启动该应用时已正确对其进行设置。 要支持应用配置，需要应用开发人员创建自己的 Android 应用，专门支持托管的配置值。 完成此操作后，可使用 Intune 指定和应用这些配置设置。 详细了解 [Android for Work 应用配置设置](afw-app-configuration-policy.md)。

## <a name="email-configuration"></a>电子邮件配置

Android for Work 不提供默认电子邮件应用或如 iOS 提供的本机电子邮件配置文件对象。 而可以通过将应用配置设置应用到支持它们的电子邮件应用中，来设置电子邮件配置。 Gmail 和 Nine Work 是 Play Store 中的两种 Exchange ActiveSync (EAS) 客户端应用，它们支持使用 Android for Work 应用配置进行配置。

Intune 为 Gmail 和 Nine Work 应用提供配置模板。 其他支持应用配置的配置文件的电子邮件应用可使用移动应用配置策略进行配置。

如果对 Android for Work 设备使用的是 EAS 条件访问，则必须使用 Gmail 或 Nine Work 电子邮件应用。 同样支持 Microsoft Outlook for Android 应用，以及任何通过 ADAL 使用新式验证的其他电子邮件应用。 详细了解[公司电子邮件的电子邮件配置文件](configure-access-to-corporate-email-using-email-profiles-with-microsoft-intune.md)。

## <a name="mobile-app-management-policies"></a>移动应用管理策略

工作配置文件和个人配置文件中完全支持应用到为移动应用程序管理 (MAM) 启用的应用上的限制策略。 可在 Android 应用发布控制台中发布业务线应用，地址为 https://play.google.com/apps/publish。 此控制台包含让应用专用于组织的选项。 详细了解[合规性策略设置](afw-compliance-policy-settings-in-microsoft-intune.md)。 有关详细信息，请参阅[移动应用管理策略](protect-app-data-using-mobile-app-management-policies-with-microsoft-intune.md)。

## <a name="vpn-profiles"></a>VPN 配置文件

VPN 支持类似于 Android VPN 配置文件。 提供了同样的 VPN 提供商和基本配置选项。 但存在两个根本差别：

1.  **限于工作配置文件的 VPN** - VPN 连接仅限于部署到工作配置文件的应用。 仅 Android for Work 托管应用可使用 VPN 连接。 设备上的个人应用无法使用托管 VPN 连接。

2.  **特定于应用的 VPN** - 如果 VPN 提供商支持特定于应用的 VPN 配置，并提供通过 Android for Work 应用配置的配置文件配置 per-app VPN 的功能，则可在 Intune 中配置特定于应用的 VPN。 请咨询 VPN 提供商，确定他们是否支持此功能。 详细了解 [VPN 连接配置文件](vpn-connections-in-microsoft-intune.md)。

## <a name="certificate-profiles"></a>证书配置文件

适用于传统 Android 管理的相同证书配置文件配置选项在 Android for Work 设备也适用。 Android for Work 提供增强的证书管理 API。 增强的证书管理提供以下功能：

1.  确保用户的证书部署静默且无缝。

2.  设备从 Intune 停用并删除了工作配置文件时，确保已完全删除部署的证书。

3.  提供改进的消息传送功能，通知用户 IT 部门通过管理服务部署和配置证书。

详细了解[证书配置文件](secure-resource-access-with-certificate-profiles.md)。

## <a name="wi-fi-profiles"></a>Wi-Fi 配置文件

设备从 Intune 中停用且删除了工作配置文件时，确保删除 Android for Work 管理的 Wi-Fi 配置文件。 详细了解 [Wi-Fi 配置文件](wi-fi-connections-in-microsoft-intune.md)。

## <a name="next-steps"></a>后续步骤
[启用 Android for Work 注册](https://docs.microsoft.com/en-us/intune/deploy-use/set-up-android-for-work)
[为 Android for Work 部署应用](https://docs.microsoft.com/en-us/intune/deploy-use/android-for-work-apps)



<!--HONumber=Nov16_HO5-->

