---
title: "Zimperium MTD 连接器与 Intune"
titleSuffix: Intune on Azure
description: "Zimperium 连接器与 Intune 集成"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 09/06/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 78214293a66784d4bc05e441c2c1cdbf718b0a9a
ms.sourcegitcommit: d434dfab7ef7a6c4082d675717fa22d5581b4f51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2017
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Zimperium 移动威胁防御连接器与 Intune

可根据 Zimperium 进行的风险评估，使用条件访问控制移动设备对公司资源的访问，Zimperium 是与 Microsoft Intune 集成的移动威胁防御 (MTD) 解决方案。 基于从运行 Zimperium 应用的设备收集的遥测评估风险。

可以基于通过 Intune 设备符合性策略启动的 Zimperium 风险评估配置条件访问策略，从而根据检测到的威胁允许或阻止不符合要求的设备访问公司资源。

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Intune 和 Zimperium 如何帮助你保护公司资源？

适用于 Android 或 iOS 的 Zimperium 应用可捕获文件系统、网络堆栈，以及设备和应用程序遥测（如果有），然后将遥测数据发送到 Zimperium 云服务，评估设备的移动威胁风险。

Intune 设备符合性策略包括基于 Zimperium 风险评估的 Zimperium 移动威胁防御规则。 启用此规则后，Intune 将评估设备是否符合已启用的策略。 如果发现设备不符合策略，将阻止对 Exchange Online 和 SharePoint Online 等公司资源的访问。 用户还可通过安装在设备上的 Zimperium 应用获取指导，以便解决问题并重新访问公司资源。

## <a name="sample-scenarios"></a>示例方案

将 Zimperium 与 Intune 集成时，请参阅下面的几个方案：

### <a name="control-access-based-on-threats-from-malicious-apps"></a>基于来自恶意应用的威胁来控制访问

在设备上检测到恶意应用（如恶意软件）时，可阻止设备，直到解除威胁：

-   连接到公司电子邮件

-   使用 OneDrive for Work 应用同步企业文件

-   访问公司应用

**检测到恶意应用时对其进行阻止：**

![检测到恶意应用](./media/Maliciousapps_blocked_Zimperium.png)

**威胁解除后授予访问权限：**

![检测到恶意应用，授予访问权限](./media/maliciousapps_unblocked_Zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>基于对网络的威胁来控制访问

检测**中间人**等网络威胁，并基于设备风险保护对 WiFi 网络的访问。

**阻止通过 Wi-Fi 访问网络：**

![阻止通过 Wi-Fi 访问网络](./media/network_wifi_blocked_Zimperium.png)

**威胁解除后授予访问权限：**

![威胁解除后授予访问权限](./media/network_wifi_unblocked_Zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>基于对网络的威胁来控制对 SharePoint Online 的访问

检测**中间人**等网络威胁，根据设备风险阻止公司文件的同步。

**检测到网络威胁时阻止 SharePoint Online：**

![检测到网络威胁时阻止 SharePoint Online](./media/network_spo_blocked_Zimperium.png)

**威胁解除后授予访问权限：**

![Sharepoint 的威胁解除后授予访问权限示例](./media/network_spo_unblocked_Zimperium.png)

## <a name="supported-platforms"></a>受支持的平台

-   **Android 4.1 及更高版本**

-   **iOS 8 及更高版本**

## <a name="prerequisites"></a>先决条件

-   Azure Active Directory Premium

-   Microsoft Intune 订阅

-   Zimperium 移动威胁防御订阅

    -   请访问 [Zimperium 网站](https://www.zimperium.com/zips-mobile-ips)以了解详细信息。

## <a name="next-steps"></a>后续步骤

- [将 Zimperium 与 Intune 集成](zimperium-mtd-connector-integration.md)

- [设置 Zimperium 应用](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [创建 Zimperium 设备符合性策略](mtd-device-compliance-policy-create.md)

- [启用 Zimperium MTD 连接器](mtd-connector-enable.md)