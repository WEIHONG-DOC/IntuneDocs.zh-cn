---
title: "部署 Lookout for Work 应用 | Microsoft Docs"
description: "配置并部署 Android 版 Lookout for Work 应用。"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.date: 12/20/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 524c4209-ad57-4d35-955e-a00d796bf858
ms.reviewer: sandera
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 53862e49c922b75b414fd5aceec3bba2b10299a6
ms.openlocfilehash: a7c1a2b7ec1719a47c36e1fe09d1deccd0eed1b1


---

# <a name="configure-and-deploy-lookout-for-work-apps"></a>配置并部署 Lookout for Work 应用

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

本文介绍了如何为 Android 和 iOS 设备配置和部署 Lookout for Work 应用。

## <a name="android-google-play-store-app"></a>Android（Google Play 商店应用）

1.  在 [Microsoft Intune 管理员控制台](https://manage.microsoft.com)中，转到“应用”并选择“添加应用”。
2.  在发布者的“软件设置”页，选择“外部链接”，并指定下列 URL：https://play.google.com/store/apps/details?id=com.lookout.enterprise
  >[!NOTE]
  >请勿单击要求使用托管浏览器的框。

3.  在“软件描述”页填入以下信息：
  * **发布者：**Lookout Mobile Security
  * **名称：**Lookout for Work
  * **说明：**Lookout 能为设备提供针对移动威胁的最佳保护。 在设备上安装 Lookout 应用后，该应用可让设备免受威胁，并将在发现任何威胁时向用户、公司和管理员发出警报。
  * **类型：**计算机管理

4. 成功完成时将显示消息“数据已成功上传至 Microsoft Intune”。

  在 Intune 控制台单击“应用”时，现可在列表中看到 **Lookout for Work** 应用 ![在列表中显示 Lookout for Work 应用的 Intune 管理员控制台应用页屏幕截图](../media/mtp/lookout-app-listed-intune-console.png)

5. 通过选择 Lookout for Work 应用，并选择“管理部署”，将应用部署到用户。

  选择的用户必须与添加到 Lookout MTP 控制台“注册管理”选项中的用户一致。  请参阅[为订阅配置 Lookout MTP](configure-and-deploy-lookout-for-work-apps.md) 部分中的步骤 3，了解有关将用户组添加到 Lookout MTP 的信息。

  >[!IMPORTANT]
  > Intune 应用部署向导不会感知 Azure AD 用户组，而会使用 Intune 用户组。 因此，必须以在 Lookout MTP 控制台中注册的 Azure AD 用户组为基础创建 Intune 用户组，如[本主题](plan-your-user-and-device-groups.md)所述。

6. 选择“必需安装”选项，该选项要求在用户设备上安装 Lookout 应用。

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS（企业签名的 Lookout 应用版本）

1. 确保在设备上设置了 **iOS 管理**。 有关如何针对 iOS 管理设置设备的说明，请参阅[设置 iOS 和 Mac 设备管理](set-up-ios-and-mac-management-with-microsoft-intune.md)。

2. **重新签名** Lookout for Work iOS 应用。 Lookout 会在 iOS 应用商店之外分发其 Lookout for Work iOS 应用。 **分发应用之前**，必须使用 iOS 企业开发人员证书对应用重新签名。 有关对 Lookout for Work iOS 应用重新签名的详细说明，请参阅 Lookout 站点上的 [Lookout for Work iOS 应用重新签名过程](https://personal.support.lookout.com/hc/en-us/articles/114094038714)。

3. 通过执行以下操作为 iOS 用户启用 Azure Active Directory 身份验证：
  1.  登录到 [Azure Active Directory 管理门户](https://manage.windowsazure.com)，并导航到应用程序页。
  2.  添加 **Lookout for Work iOS 应用**作为**本机客户端应用程序**。
  ![显示本机客户端应用选项的添加应用对话框屏幕截图](../media/mtp/aad-add-app.png)
  3. 将 **com.lookout.enterprise.yourcompanyname** 替换为对 IPA 签名时选择的客户捆绑 ID。
  4.  添加其他重定向 URI：**&lt;companyportal://code/>**，后跟原始重定向 URI 的 URL 编码形式版本。
  5.  将**委托的权限**添加到应用。

  有关详细信息，请参阅[配置本机客户端应用程序](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application)。

4. 按照[在 Microsoft Intune 中为移动设备添加应用](https://docs.microsoft.com/en-us/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune)主题中所述，上传重新签名的 .ipa 文件。 将最低操作系统版本为 iOS 8.0 或更高版本。

  ![Intune 管理员控制台中在应用列表中显示了 Lookout for work 应用的应用页的屏幕截图](../media/mtp/ios-app-uploaded-intune.png)

5. 按照[使用 Microsoft Intune 中的移动应用配置策略配置 iOS 应用](https://docs.microsoft.com/en-us/intune/deploy-use/configure-ios-apps-with-mobile-app-configuration-policies-in-microsoft-intune)主题中所述，创建托管应用配置策略。

  ![突出显示了 iOS 8.0 或更高版本应用配置策略的创建新策略向导的屏幕截图](../media/mtp/ios-app-config.png)

6. **若要将应用部署到用户**，请选择 Lookout for Work 应用，然后选择“管理部署”。

  选择的用户必须与添加到 Lookout 控制台“注册管理”选项中的用户一致。  请参阅[为订阅配置 Lookout 设备威胁保护](configure-and-deploy-lookout-for-work-apps.md)部分中的步骤 3，了解有关将用户组添加到 Lookout MTP 的信息。

  >[!IMPORTANT]
  > Intune 应用部署向导并未识别到 Azure AD 用户组且使用的是 Intune 用户组，因此必须基于在 Lookout 控制台中注册的 Azure AD 用户组创建 Intune 用户组（如[本](plan-your-user-and-device-groups.md)主题所述）。

  选择“必需安装”选项，该选项要求在用户设备上安装 Lookout 应用。

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>在设备上打开部署的应用时发生的情况

用户在设备上打开 Lookout for Work 时，将提示其激活应用并选择“使用 Azure Active Directory 登录”选项。 以下主题中提供了最终用户操作流程的详细指导：

* [系统提示在 Android 设备上安装 Lookout for Work](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [解除 Lookout for Work 在 Android 设备上发现的威胁](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>后续步骤
* [在合规性策略中启用设备威胁保护规则](enable-device-threat-protection-rule-in-compliance-policy.md)



<!--HONumber=Jan17_HO2-->

