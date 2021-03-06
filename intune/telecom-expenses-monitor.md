---
title: 设置电信费用管理服务
titleSuffix: Microsoft Intune
description: 将 Intune 与 Saaswedo 电信费用管理服务相集成。
keywords: Saaswedo
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/28/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: b7bf5802-4b65-4aeb-ac99-8e639dd89c2a
ms.reviewer: sumitp
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 53f6adba610f1ddb817e04ac8e9a0fdb2665b21a
ms.sourcegitcommit: 2d1e89fa5fa721e79648e41fde147a035e7b047d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "43347808"
---
# <a name="set-up-a-telecom-expense-management-service-in-intune"></a>设置 Intune 中的电信支出管理服务
[!INCLUDE [azure_portal](./includes/azure_portal.md)]

借助 Intune，可管理企业拥有的移动设备上数据使用产生的电信费用。 为启用此功能，Intune 已集成第三方软件开发商 Saaswedo 的 Datalert 电信费用管理解决方案。 Datalert 是实时电信费用管理软件，使你能够管理电信数据使用情况。 它可帮助避免你的 Intune 托管设备产生成本高昂的超额意外数据和漫游量。

Intune 与 Datalert 相集成，实现了集中设置、监视和强制实施漫游和国内数据流量限制。 当限制超出定义的阈值时，会触发自动警报。 可以将服务配置为针对单个最终用户或最终用户组应用不同的操作（例如禁用漫游或超出阈值）。 可在 Datalert 管理控制台中查看提供数据流量和监视信息的报告。

下图显示 Intune 如何与 Datalert 集成。

  ![Intune 和 Datalert 集成的图示](./media/tem-datalert-intune-solution-diagram.png)

通过 Intune 使用 Datalert 之前，需要在 Datalert 控制台和 Intune 中配置设置。 请务必打开 Datalert 服务和 Intune 的连接。 如果 Datalert 端已启用连接，但 Intune 端未启用，那么 Intune 虽然能接收到通信，但会将其忽略。

## <a name="supported-platforms"></a>受支持的平台

- Samsung Knox
- iOS 8.0 及更高版本

## <a name="prerequisites"></a>必备条件

- 订阅 Microsoft Intune 和拥有 Azure 门户的访问权限。
- Datalert 电信费用管理服务订阅

## <a name="list-of-telecom-expense-management-providers"></a>电信费用管理提供商列表

Intune 目前与下列电信费用管理提供商集成：

[Saaswedo Datalert 电信费用管理服务](http://www.datalert.biz/)

## <a name="deploy-the-intune-and-datalert-integrated-solution"></a>部署集成了 Intune 和 Datalert 的解决方案

开始之前，请确保已拥有 Intune 和 Datalert 电信费用管理服务订阅。

### <a name="step-1-connect-the-datalert-service-to-microsoft-intune"></a>步骤 1：将 Datalert 服务连接到 Microsoft Intune

1. 使用管理员凭据登录 Datalert 管理控制台。

2. 在 Datalert 管理控制台上，转到“设置”选项卡，然后转到“MDM 配置”。

3. 选择“解锁”，在页面上输入设置。

4. 对于“服务器 MDM”，选择“Microsoft Intune”。

5. 对“Azure AD 域”，输入 Azure 租户 ID，然后选择“连接”按钮。

    选择“连接”将使 Datalert 服务登记到 Intune，以确保与 Intune 之间没有预先存在的 Datalert 连接。 几秒钟后将出现 Microsoft 登录页，随后是 Datalert Azure 身份验证。

6. 在 Microsoft 身份验证页上，选择“接受”。 将重定向到 Datalert“谢谢”页，该页会在几秒钟后关闭。 Datalert 会验证连接，并在其验证的项列表旁显示绿色复选标记。 如果验证失败，则会出现一条红色的消息，并且应该联系 Datalert 支持人员以获取帮助。

    以下屏幕截图显示连接成功后可以看到的绿色复选标记。

   ![显示连接成功的 Datalert 页面](./media/tem-mdm-configuration-mdm-server-page.png)

### <a name="step-2-check-that-the-telecom-expense-management-feature-is-active-in-intune"></a>步骤 2：检查电信费用管理功能在 Intune 中是否处于活动状态

完成上述步骤 1 后，应将自动启用连接，且 Azure 门户中应显示连接状态“活动”。 这些步骤演示了如何检查“活动”状态。

1. 登录到 [Azure 门户](https://portal.azure.com)。

2. 选择“所有服务” > “Intune”。 Intune 位于“监视 + 管理”部分中。

3. 在“Intune”窗格上，选择“设备配置”。

4. 在“设备配置”窗格上，选择“设置” > “电信费用管理”。

   在页面顶部查找“活动”连接状态。

   ![显示 Datalert 连接状态为“活动”的 Intune 页面](./media/tem-azure-portal-enable-service.png)

### <a name="step-3-deploy-the-datalert-app-to-corporate-enrolled-devices"></a>步骤 3：将 Datalert 应用部署到企业注册的设备

若要确保收集仅来自公司拥有的线路的数据使用情况，必须执行以下两项操作：
- 在 Intune 中创建设备类别
- 使 Datalert 应用仅面向公司手机。

#### <a name="define-device-categories-and-device-groups-mapped-to-the-categories"></a>定义设备类别和映射到各类别的设备组

根据组织的需求，至少创建两个设备类别（例如，“公司”和“个人”）。 然后为每个类别创建动态设备组。 可以根据需要为组织创建更多类别。

在注册过程中，将向用户显示这些类别。 根据用户选择的类别，会将已注册的设备移至相应的设备组。 有关如何创建设备类别的步骤，请参阅[将设备映射到组](device-group-mapping.md)。

  ![“添加策略”窗格的屏幕截图](./media/tem-dynamic-membership-rules.png)

#### <a name="create-the-datalert-app-in-intune"></a>在 Intune 中创建 Datalert 应用

按照下列步骤，在 Intune 中为每个平台创建 Datalert 应用。 以下步骤使用 iOS 作为示例。

1. 在 [Azure 门户](https://portal.azure.com)的“Intune”窗格上，选择“客户端应用”。

2. 在“客户端应用”窗格上，选择“管理” > “应用”。

3. 选择“添加”添加一个应用。

4. 选择应用类型。 例如，对于 iOS，选择“iOS 应用商店应用”。

5. 在“搜索应用商店”中，通过在搜索窗口中键入 **Datalert** 查找 Datalert 应用。

6. 选择“Datalert”应用，然后选择“选择”。

   ![“添加策略”窗格的屏幕截图](./media/tem-select-app-from-apple-app-store.png)

7. 完成其余步骤，创建用于 iOS 的应用。

   ![“添加策略”窗格的屏幕截图](./media/tem-steps-to-create-the-app.png)

#### <a name="assign-the-datalert-app-to-the-corporate-device-group"></a>将 Datalert 应用分配给公司设备组

1. 从“移动应用 - 应用”窗格中，选择在前一步骤中创建的 iOS Datalert 应用。

2. 在“应用”窗格上，选择“管理” > “分配”。

3. 选择“添加组”，然后按照步骤选择公司设备组。

4. 选择对于该组要将应用安装设置为必需还是可选。 以下示例屏幕截图显示该安装为“必需”，这意味着用户注册其设备后必须安装 Datalert 应用。

   ![“添加策略”窗格的屏幕截图](./media/tem-assign-datalert-app-to-device-group.png)

### <a name="step-4-add-corporate-paid-phone-lines-to-the-datalert-console"></a>步骤 4：将公司付费电话线路添加到 Datalert 控制台

现已配置 Intune 和 Datalert 服务以彼此进行通信。 现需将公司付费电话线路添加到 Datalert 控制台，并为任何手机网络或漫游使用冲突定义阈值和操作。 可以将公司付费的电话线路手动添加到 Datalert 控制台，或者在 Intune 中注册设备后可以自动添加这些线路。

若要设置这些项，请转到[适用于 Microsoft Intune 的 Datalert 设置页面](http://www.datalert.fr/microsoft-intune/intune-setup) (http://www.datalert.fr/microsoft-intune/intune-setup))，然后按照“设置”选项卡下的设置向导中的步骤操作。

  ![“添加策略”窗格的屏幕截图](./media/tem-add-phone-lines-to-datalert-console.png)


Datalert 服务目前处于活动状态，它开始监控数据流量，并在超过所配置流量限制的设备上禁用手机网络和漫游数据。

## <a name="client-enrollment-experience"></a>客户端注册体验
有关客户端注册体验的信息，请参阅以下内容：
-   [在电信费用管理中注册 iOS 设备](https://docs.microsoft.com/intune-user-help/enroll-your-device-with-telecom-expense-management-ios)
-   [在电信费用管理中注册 Android 设备](https://docs.microsoft.com/intune-user-help/enroll-your-device-with-telecom-expense-management-android)

## <a name="turning-off-the-datalert-service"></a>关闭 Datalert 服务

如果在 Azure 门户中禁用 Datalert 服务：

- 因为之前违反流量限制而应用到设备的所有操作都将撤销。
- 将不再阻止用户进行数据访问和漫游。
- Intune 仍然会接收来自服务的信号，但将忽略它们。

**关闭服务**

1. 在 Azure 门户中的“电信费用管理”窗格上，选择“禁用”。

2. 选择“保存”。

## <a name="viewing-data-usage-and-roaming-reports"></a>查看数据流量和漫游报告

目前，仅在 Saaswedo 的 Datalert 管理控制台中提供数据流量报告。

即将添加最终用户安装 Datalert 应用需遵循的操作说明。
