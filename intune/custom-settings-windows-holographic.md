---
title: Microsoft Intune 中 Windows Holographic for Business 设备的自定义设置 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中为运行 Windows Holographic for Business 的设备创建使用 OMA-URI 设置的自定义配置文件。 可以设置 AllowFastReconnect、AllowVPN、AllowUpdateService、UpdateServiceURL、RequireUpdatesApproval、ApprovedUpdates 和 ApplicationLaunchRestrictions 策略配置服务提供程序 (CSP) 设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 4/26/2018
ms.article: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 7272e8e088ae2c2ecad1756233281c42a80a279b
ms.sourcegitcommit: 2061f7a442efc96c8afd5db764d11531563c7e39
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "32328072"
---
# <a name="custom-device-settings-for-devices-running-windows-holographic-for-business-in-intune"></a>Intune 中运行 Windows Holographic for Business 的设备的自定义设备设置

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

 使用 Windows Holographic for Business 的 Microsoft Intune 自定义配置文件部署可用于控制设备功能的 OMA-URI（开放移动联盟统一资源标识符）设置。 通过 Windows Holographic for Business 可以进行很多配置服务提供程序 (CSP) 设置。 有关 CSP 的概述，请参阅[面向 IT 专业人员的配置服务提供程序 (CSP) 简介](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers)。 如需了解 Windows Holographic 支持的具体 CSP，请参阅 [Windows Holographic 中支持的 CSP](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens)。

如果正在寻找特定设置，请牢记 [Windows Holographic for Business 设备限制配置文件](device-restrictions-windows-holographic.md)包含许多内置设置，无需指定自定义值。

## <a name="create-the-custom-oma-uri-profile"></a>创建自定义 OMA-URI 配置文件

1. 按照[在 Microsoft Intune 中配置自定义设备设置](custom-settings-configure.md)中的说明进行操作。
2. 在“创建配置文件”上，选择“设置”添加一个或多个 OMA-URI 设置。
3. 在“自定义 OMA-URI 设置”上，单击“添加”可添加新值。 还可以单击“导出”创建逗号分隔值 (.csv) 文件中配置的所有值的列表。
4. 对于要添加的每个 OMA URI 设置，请输入以下信息：
  - **设置名称**：输入 OMA-URI 设置的唯一名称，以帮助你在设置列表中识别它。
  - **设置描述** -（可选）输入设置的描述。
  - **数据类型**：从以下各项选择：
    - **字符串**
    - **字符串 (XML)**
    - **日期和时间**
    - **整数**
    - **浮点**
    - **布尔值**
  - **OMA-URI（区分大小写）**：输入想要为其提供设置的 OMA-URI。
  - **值**：输入要与已输入的 OMA-URI 关联的值。
5. 完成后，返回“创建配置文件”，然后单击“创建”。 配置文件随即创建并显示在配置文件列表中。

## <a name="recommended-custom-settings"></a>推荐的自定义设置

以下设置也可用于运行 Windows Holographic for Business 的设备：

### <a name="allowfastreconnecthttpsdocsmicrosoftcomwindowsclient-managementmdmpolicy-csp-authenticationauthentication-allowfastreconnect"></a>[AllowFastReconnect](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|Integer<br/>0 - 不允许<br/>1 - 允许（默认值）|

### <a name="allowupdateservicehttpsdocsmicrosoftcomwindowsclient-managementmdmpolicy-csp-updateupdate-allowupdateservice"></a>[AllowUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|Integer<br/>0 – 不允许更新服务 <br/>1 – 允许更新服务（默认值）。|

### <a name="allowvpnhttpsdocsmicrosoftcomwindowsclient-managementmdmpolicy-csp-settingssettings-allowvpn"></a>[AllowVPN](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|Integer<br/>0 - 不允许<br/>1 - 允许（默认值）|

### <a name="requireupdatesapprovalhttpsdocsmicrosoftcomwindowsclient-managementmdmpolicy-csp-updateupdate-requireupdateapproval"></a>[RequireUpdatesApproval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|Integer<br/>0 – 未配置。 设备安装所有适用的更新。<br/>1 – 设备仅安装既适用又在已批准更新列表中的更新。 如果 IT 想控制设备上的更新部署（例如部署前需要测试），请将此策略设置为 1。|

### <a name="scheduledinstalltimehttpsdocsmicrosoftcomwindowsclient-managementmdmpolicy-csp-updateupdate-scheduledinstalltime"></a>[ScheduledInstallTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|整数 0-23，其中 0 表示中午 12 点，23 表示晚上 11 点<br/>默认值为 3。|

### <a name="updateserviceurlhttpsdocsmicrosoftcomwindowsclient-managementmdmpolicy-csp-updateupdate-updateserviceurl"></a>[UpdateServiceURL](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|字符串<br/>URL - 设备从指定的 URL 上的 WSUS 服务器检查更新。<br/>未配置 - 设备从 Microsoft 更新检查更新。|

### <a name="approvedupdateshttpsdocsmicrosoftcomwindowsclient-managementmdmupdate-csp"></a>[ApprovedUpdates](https://docs.microsoft.com/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/GUID<br/><br/>**重要说明**<br/>必须代表最终用户阅读和接受更新 EULA。 如果不这样做，将被视为违反法律或合同义务。|更新批准的节点和代表最终用户的 EULA 接受。<br/><br/>有关详细信息，请参阅[更新 CSP](https://docs.microsoft.com/windows/client-management/mdm/update-csp)。|

### <a name="applicationlaunchrestrictionshttpsdocsmicrosoftcomwindowsclient-managementmdmapplocker-csp"></a>[ApplicationLaunchRestrictions](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**重要说明**<br/>AppLocker CSP 一文使用转义 XML 示例。 若要使用 Intune 自定义配置文件配置设置，必须使用纯 XML。|字符串<br/>有关详细信息，请参阅 [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)。|

### <a name="deletionpolicyhttpsdocsmicrosoftcomwindowsclient-managementmdmaccountmanagement-csp"></a>[DeletionPolicy](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|Integer<br/>0 - 设备返回到当前没有活动用户的状态时立即删除<br/>1 - 按存储容量阈值删除（默认）<br/>2 - 按存储容量阈值和配置文件非活动阈值删除|

### <a name="enableprofilemanagerhttpsdocsmicrosoftcomwindowsclient-managementmdmaccountmanagement-csp"></a>[EnableProfileManager](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|布尔值<br/>True - 启用<br/>False - 禁用（默认值）|

### <a name="profileinactivitythresholdhttpsdocsmicrosoftcomwindowsclient-managementmdmaccountmanagement-csp"></a>[ProfileInactivityThreshold](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|Integer<br/>默认值为 30。|


### <a name="storagecapacitystartdeletionhttpsdocsmicrosoftcomwindowsclient-managementmdmaccountmanagement-csp"></a>[StorageCapacityStartDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|Integer<br/>默认值为 25。|

### <a name="storagecapacitystopdeletionhttpsdocsmicrosoftcomwindowsclient-managementmdmaccountmanagement-csp"></a>[StorageCapacityStopDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|Integer<br/>默认值为 50。|

## <a name="find-the-policies-you-can-configure"></a>查找可以配置的策略

在 [Windows Holographic 中支持的 CSP](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) 中，可以找到 Windows Holographic 支持的所有配置服务提供程序 (CSP) 的完整列表。 并非所有设置都与所有 Windows Holographic 版本兼容。 Windows 文章中的表将说明各个 CSP 支持的版本。

此外，Intune 并不支持文章中列出的所有设置。 若要查明 Intune 是否支持所需的设置，请打开针对该设置的文章。 每个设置页面将显示其支持的操作。 若要使用 Intune，设置必须支持“添加”或“替换”操作。
