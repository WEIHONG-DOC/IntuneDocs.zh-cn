---
title: 创建和部署应用保护策略
titleSuffix: Microsoft Intune
description: 了解如何创建和分配 Microsoft Intune 应用保护策略。
keywords: ''
author: msmimart
ms.author: mimart
manager: dougeby
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: f31b2964-e932-4cee-95c4-8d5506966c85
ms.reviewer: joglocke
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 83320c78d461981f1bfff52d2fddf4f121a88b8c
ms.sourcegitcommit: e814cfbbefe818be3254ef6f859a7bf5f5b99123
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "43329659"
---
# <a name="how-to-create-and-assign-app-protection-policies"></a>如何创建和分配应用保护策略

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

了解如何创建并向用户分配 Microsoft Intune 应用保护策略。 本主题还介绍如何对现有策略进行更改。

## <a name="before-you-begin"></a>在开始之前

无论设备是否由 Intune 托管，都可以将应用保护策略应用到该设备上运行的应用中。 若要详细了解应用保护策略的工作原理以及 Intune 应用保护策略支持的方案，请参阅[什么是 Microsoft Intune 应用保护策略](app-protection-policy.md)。

如果你要查找 MAM 支持应用的列表，请参阅 [MAM 应用列表](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)。

有关将组织的业务线 (LOB) 应用添加到 Microsoft Intune 以准备应用保护策略的信息，请参阅[将应用添加到 Microsoft Intune](apps-add.md)。

##  <a name="create-an-app-protection-policy"></a>创建应用保护策略
1. 在“客户端应用”工作负载中，从“管理”部分选择“应用保护策略”。 此选项会打开“应用保护策略”详细信息，可在此创建新策略和编辑现有策略。
2. 选择**添加策略**。

   ![“添加策略”边栏选项卡的屏幕截图](./media/app-protection-add-policy.png)

3. 为策略键入名称、添加简要说明并为策略选择平台类型。 如有需要，可以为每个平台创建多个策略。

4. 选择“应用”以打开“应用”边栏选项卡，其中显示了可用应用的列表。 从该列表中选择希望与正创建的策略关联的一个或多个应用。
5. 选中应用后，选择“选择”以保存选择。

    > [!IMPORTANT]
    > 必须至少选择一个应用才能创建策略。

6. 在“添加策略”边栏选项卡中，选择“配置所需设置”以打开“设置”。

   有两种类别的策略设置：“数据重定位”和“访问”。  数据重定位策略适用于应用内外的数据移动。 访问策略决定最终用户如何在工作环境中访问应用。
   为了帮助你入门，策略设置具有默认值。 如果默认值满足需求，则无须进行任何更改。

   > [!TIP]
   > 仅在工作环境中使用应用时，才强制执行这些策略设置。 最终用户使用应用执行个人任务时，不受这些策略的影响。

7. 选择“确定”保存此配置。 现将返回“添加策略”窗格。 选择“创建”以创建策略并保存设置。
8. 选择“确定”保存此配置。 现将返回“添加策略”边栏选项卡。
9. 选择“创建”以创建策略并保存设置。

按上述流程创建策略后，它未部署到任何用户。 若要部署策略，请参阅[将策略部署到用户](app-protection-policies.md#deploy-a-policy-to-users)。

## <a name="deploy-a-policy-to-users"></a>将策略部署到用户


1. 在“应用保护策略”窗格中，选择一个策略。

1. 在“策略”窗格中，选择“分配”，这将打开“Intune 应用保护 - 分配”窗格。 在“分配”窗格中，选择“选择要包括的组”，以打开“选择要包括的组”窗格。

   ![“分配”窗格的屏幕截图，其中突出显示“选择要包括的组”菜单选项](./media/app-protection-policy-add-users.png)

2.  用户组列表会显示在“添加用户组”窗格中。 此列表显示“Azure Active Directory”中的所有安全组。 可选择希望将此策略应用于的用户组，然后选择“选择”。 选择“选择”会将策略部署到用户。

    ![显示 Azure Active Directory 用户列表的“添加用户组”窗格的屏幕截图](./media/azure-ad-user-group-list.png)

现已创建策略并将其部署到用户。

该策略仅影响分配有 Microsoft Intune 许可证的用户。 所选安全组中没有已分配的 Intune 许可证的用户不受影响。

>[!IMPORTANT]
> 如果配合使用 Intune 和 Configuration Manager 来管理设备，则该策略仅应用于直接位于所选组中的用户。 所选组中嵌套子组的成员不受影响。

最终用户可以从 App Store 或 Google Play 下载应用。 有关详情，请参阅：
* [Android 应用由应用保护策略托管时会出现的情况](app-protection-enabled-apps-android.md)
* [iOS 应用由应用保护策略托管时会出现的情况](app-protection-enabled-apps-ios.md)

##  <a name="change-existing-policies"></a>更改现有策略
你可以编辑现有策略并将其应用于目标用户。 但是，更改现有策略时，已登录到应用的用户在 8 小时内将看不到更改。

若要立即看到更改的效果，最终用户必须注销应用，然后重新登录。

### <a name="to-change-the-list-of-apps-associated-with-the-policy"></a>更改与策略关联的应用列表的步骤

1.  在“应用保护策略”窗格中，选择要更改的策略以打开特定于刚才所选策略的窗格。

2.  在策略窗格中，选择“目标应用”以打开应用列表。

3.  在列表中删除或添加应用，然后选择“保存”图标以保存所做的更改。

### <a name="to-change-the-list-of-user-groups"></a>更改用户组列表的步骤


1.  在“应用保护策略”窗格中，选择要更改的策略以打开特定于所选策略的窗格。

2.  在策略窗格中，选择“分配”以打开“Intune 应用保护 - 分配”窗格，其中显示具有此策略的当前用户组的列表。

3.  若要向策略添加新用户组，请在“包括”选项卡中选择“选择要包括的组”，然后选择用户组。 选择“选择”以将策略部署到所选组。

4.  若要删除用户组，在“排除”选项卡中，选择“选择要排除的组”，然后选择用户组。 选择“选择”以删除用户组。

### <a name="to-change-policy-settings"></a>更改策略设置的步骤

1.  在“应用保护策略”窗格中，选择要更改的策略以打开特定于刚才所选策略的窗格。

2.  选择“策略设置”以打开“策略设置”窗格。

3.  更改设置，然后选择“保存”图标以保存所做的更改。

## <a name="target-app-protection-policies-based-on-device-management-state"></a>根据设备管理状态设置应用保护策略的适用对象
在许多组织中，允许最终用户使用 Intune 移动设备管理 (MDM) 托管的设备（如公司拥有的设备）和使用仅由 Intune 应用保护策略提供保护的非托管设备（例如 BYO 设备）的情况都很常见。

Intune 应用保护策略是一种针对用户身份的策略，因此用户的保护设置历来适用于已注册（MDM 托管）和未注册（非 MDM）设备。 因此可以将 Intune 应用保护策略应用于已注册或未注册 Intune 的 iOS 和 Android 设备。 你可以对非托管设备应用具备严格数据丢失防护 (DLP) 措施的保护策略，并对 MDM 托管设备应用 DLP 措施较为宽松的单独保护策略。 

若要创建这些策略，请在 Intune 控制台中浏览找到“客户端应用” > “应用保护”策略，然后单击“添加策略”。 还可以编辑现有的应用保护策略。 如果想将应用保护策略同时应用到托管和非托管设备，请确保将“面向所有应用类型”设置为“是”（这是默认设置）。 如果想根据管理状态逐渐分配，请将“面向所有应用类型”设置为“否”。 

对于视为“已托管”的 iOS 应用，需要为每个应用部署 IntuneMAMUPN 配置策略设置。 有关详细信息，请参阅[如何在 Microsoft Intune 中管理 iOS 应用之间的数据传输](https://docs.microsoft.com/en-us/intune/data-transfer-between-apps-manage-ios#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm)。

> [!NOTE]
> 有关根据设备管理状态分配应用保护策略的 iOS 具体支持信息，请参阅[根据管理状态应用 MAM 保护策略](whats-new.md#mam-protection-policies-targeted-based-on-management-state-)。

## <a name="policy-settings"></a>策略设置
若要查看 iOS 和 Android 的策略设置的完整列表，请选择以下链接之一：

- [iOS 策略](app-protection-policy-settings-ios.md)
- [Android 策略](app-protection-policy-settings-android.md)

## <a name="next-steps"></a>后续步骤
[监视合规性和用户状态](app-protection-policies-monitor.md)

### <a name="see-also"></a>另请参阅
* [Android 应用由应用保护策略托管时会出现的情况](app-protection-enabled-apps-android.md)
* [iOS 应用由应用保护策略托管时会出现的情况](app-protection-enabled-apps-ios.md)
