---
title: 配置适用于运行 Android 的设备的 Microsoft Intune Wi-Fi 设置
titleSuffix: ''
description: 了解运行 Android 的设备上的 Intune Wi-Fi 配置设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 7/6/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 0157815322488525a4ce7a3d6d2c90cbb8d3ff2a
ms.sourcegitcommit: 98b444468df3fb2a6e8977ce5eb9d238610d4398
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2018
ms.locfileid: "37905659"
---
# <a name="configure-wi-fi-settings-in-microsoft-intune-for-devices-running-android-android-work-profiles-and-android-kiosk-devices"></a>在 Microsoft Intune 中为运行 Android、Android 工作配置文件和 Android 展台设备的设备配置 Wi-Fi 设置

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

本文介绍可在 Microsoft Intune 中为运行 Android 和 Android 工作配置文件的设备配置的 Wi-Fi 设置。

## <a name="wi-fi-settings-for-basic-and-enterprise-profiles"></a>适用于基本配置文件和企业配置文件的 Wi-Fi 设置

以下 Wi-Fi 设置可用于 Android 和 Andorid 工作配置文件设备：

- **网络名称** - 输入此 Wi-Fi 连接的名称。 用户浏览设备上的可用连接列表时，会看到该名称。
- **SSID** - 服务设置标识符的英文缩写。 这是设备连接到的无线网络的真实名称。 但是，用户在选择连接时只会看到你之前配置的网络名称。
- **自动连接** - 只要设备处于此网络的范围内，即进行连接。
- **隐藏网络** - 阻止此网络显示在设备上的可用网络列表中。

## <a name="wi-fi-settings-available-for-enterprise-kiosk-profiles"></a>可用于企业展台配置文件的 Wi-Fi 设置
- **Wi-Fi 类型**：这些 Wi-Fi 类型设置仅在选择“配置文件类型” > “仅限设备所有者” > “Wi-Fi”时可用。
    - **开放式（无身份验证）**
    - **WEP 预共享密钥**：必须在“预共享密钥”框中提供密码。
    - **WPA 预共享密钥**：必须在“预共享密钥”框中提供密码

## <a name="wi-fi-settings-for-android-legacy-and-android-work-profiles-only"></a>仅适用于 Android 旧版和 Android 工作配置文件的 Wi-Fi 设置

- **EAP 类型** - 从以下项中选择用于对安全无线连接进行身份验证的可扩展身份验证协议 (EAP) 类型：
    - **EAP-TLS**
    - **EAP-TTLS**
    - **PEAP**

### <a name="further-options-when-you-choose-an-eap-type"></a>选择 EAP 类型时的其他选项

#### <a name="server-trust"></a>服务器信任



|设置名|更多信息|使用时间|
|-------------|---------------|-----------|
|**证书服务器名称**|指定由受信任的证书颁发机构 (CA) 颁发的证书中使用的一个或多个常用名称。 如果提供此信息，则可在用户设备连接到此 Wi-Fi 网络时，绕过设备上显示的动态信任对话框。|EAP 类型为 **EAP-TLS** 或 **EAP-TTLS**|
|**用于服务器验证的根证书**|选择用于对连接进行身份验证的受信任的根证书配置文件。 |EAP 类型为 **EAP-TLS**、**EAP-TTLS** 或 **PEAP**|
|**标识隐私（外部标识）**|请指定为响应 EAP 标识请求而发送的文本。 此文本可以是任何值。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。|EAP 类型为 **PEAP**|


#### <a name="client-authentication"></a>客户端身份验证


|                                     设置名                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       更多信息                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                            使用时间                            |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| <strong>用于客户端身份验证的客户端证书（身份证书）</strong> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       选择用于对连接进行身份验证的 SCEP 或 PKCS 证书配置文件。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |              EAP 类型为 <strong>EAP-TLS</strong>              |
|                        <strong>身份验证方法</strong>                        | 选择连接的身份验证方法：<br>- <strong>证书</strong> 选择要作为标识证书提交给服务器的 SCEP 或 PKCS 客户端证书。<br><br>- <strong>用户名和密码</strong> 可指定进行身份验证的其他方法。 <br><br>如果选择了“用户名和密码”，请配置：<br><br>-  <strong>非 EAP 方法（内部标识）</strong>，然后从以下项中选择要验证连接的方式：<br>- <strong>无</strong><br>- <strong>未加密的密码 (PAP)</strong><br>- <strong>质询握手身份验证协议 (CHAP)</strong><br>- <strong>Microsoft CHAP (MS-CHAP)</strong><br>- <strong>Microsoft CHAP 版本 2 (MS-CHAP v2)</strong><br>可用的选项取决于你选择的 EAP 类型。<br><br><strong>和</strong><br><br>- <strong>标识隐私（外部标识）</strong> - 指定为响应 EAP 标识请求而发送的文本。 此文本可以是任何值。 在身份验证过程中，将首先发送此匿名标识，然后在安全隧道内发送真实标识。 | EAP 类型为 <strong>EAP-TTLS</strong> 或 <strong>PEAP</strong> |

