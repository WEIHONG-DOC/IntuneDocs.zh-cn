---
title: S/MIME 电子邮件签名和加密 - Azure | Micrososft Docs
description: 在 Microsoft Intune 中使用或启用 S/MIME 签名和加密电子邮件
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/21/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 3a31a43cfe45060891c30a7f159123a30b43173d
ms.sourcegitcommit: 488be75cbee88455b33c68a3ec2acb864d461bf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "41910660"
---
# <a name="smime-email-signing-and-encryption-in-intune"></a>Intune 中的 S/MIME 电子邮件签名和加密

> [!IMPORTANT]
> 我们即将对本文介绍的 S/MIME 功能进行一些改进。 因此，Intune 暂不提供 S/MIME 功能。 我们将在这项功能发布后删除此说明。

S/MIME 通过使用加密和解密为电子邮件通信提供更高的安全级别。 Microsoft Intune 可以使用 S/MIME 对运行 iOS、Windows、Windows Phone、Android 和 macOS 的移动设备的电子邮件进行签名和加密。

在 iOS 设备上，可以创建 Intune 管理的电子邮件配置文件，该配置文件使用 S/MIME 和证书对传入和传出的电子邮件进行签名和加密。 对于其他平台，S/MIME 的受支持情况各不相同。 如果支持，则可以安装使用 S/MIME 签名和加密的证书。 然后，最终用户可以在其电子邮件应用程序中启用 S/MIME。

有关 S/MIME 电子邮件签名和加密的详细信息，请参阅 [用于电子邮件签名和加密的 S/MIME](https://docs.microsoft.com/Exchange/policy-and-compliance/smime)。

## <a name="signing-certificates"></a>签名证书

用于签名的证书允许客户端电子邮件应用与电子邮件服务器进行安全通信。

若要使用签名证书，请在证书颁发机构上创建一个专用于签名的模板。 Microsoft Active Directory 证书颁发机构上，[配置服务器证书模板](https://docs.microsoft.com/windows-server/networking/core-network-guide/cncg/server-certs/configure-the-server-certificate-template)列出了创建证书模板的步骤。

Intune 中的签名证书使用 PKCS 证书。 [配置和使用 PKCS 证书](certficates-pfx-configure.md)介绍了如何在 Intune 环境中部署和使用 PKCS 证书。 这些步骤包括：

- 下载并安装 Microsoft Intune 证书连接器以支持 PKCS 证书请求。
- 为设备创建受信任的根证书配置文件。 此步骤包括为证书颁发机构使用受信任的根证书和中间证书，然后将配置文件部署到设备。
- 使用创建的证书模板创建 PKCS 证书配置文件。 此配置文件向设备颁发签名证书，并将 PKCS 证书配置文件部署到设备。

此外还可以导入特定用户的签名证书。 签名证书部署在用户注册的所有设备上。 若要将证书导入 Intune，请使用 [GitHub 中的 PowerShell cmdlet](https://github.com/Microsoft/Intune-Resource-Access)。 若要将已导入 Intune 的 PKCS 证书部署为用于电子邮件签名，请按照[在 Intune 中配置和使用 PKCS 证书](certficates-pfx-configure.md)中的步骤进行操作。 这些步骤包括：

- 下载并安装 Microsoft Intune 的 PFX 证书连接器。 此连接器将导入的 PKCS 证书传递到设备。
- 将 S/MIME 电子邮件签名证书导入到 Intune。
- 创建 PKCS 导入的证书配置文件。 此配置文件将导入的 PKCS 证书传递到相应的用户设备。

## <a name="encryption-certificates"></a>加密证书

加密证书用于确认加密电子邮件只能由预期收件人解密。 S/MIME 加密是可以在电子邮件通信中使用的额外安全层。

向另一个用户发送加密电子邮件时，将获取该用户的加密证书公钥，并对发送的电子邮件进行加密。 收件人使用其设备上的私钥对电子邮件进行解密。 用户拥有用于加密电子邮件的证书历史记录。 必须将每个证书部署到特定用户的所有设备，以便成功解密其电子邮件。

建议不要在 Intune 中创建电子邮件加密证书。 尽管 Intune 可以颁发支持加密的 PKCS 证书，但 Intune 会为每台设备创建一个唯一的证书。 每台设备一个唯一证书不适用于 S/MIME 加密方案，因为该方案中加密证书应在用户的所有设备之间共享。

若要使用 Intune 部署 S/MIME 证书，必须将用户的所有加密证书导入 Intune。 然后，Intune 将所有这些证书部署到用户注册的每个设备。 若要将证书导入 Intune，请使用 [GitHub 中的 PowerShell cmdlet](https://github.com/Microsoft/Intune-Resource-Access)。

若要将已导入 Intune 的 PKCS 证书部署为用于电子邮件加密，请按照[在 Intune 中配置和使用 PKCS 证书](certficates-pfx-configure.md)中的步骤进行操作。 这些步骤包括：

- 下载并安装 Microsoft Intune 的 PFX 证书连接器。 此连接器将导入的 PKCS 证书传递到设备。
- 将 S/MIME 电子邮件加密证书导入到 Intune。
- 创建 PKCS 导入的证书配置文件。 此配置文件将导入的 PKCS 证书传递到相应的用户设备。

 > [!NOTE]
 > 删除公司数据或从管理中取消注册用户后，Intune 将删除导入的 S/MIME 加密证书。 但是，不会在证书颁发机构撤销证书。

## <a name="smime-email-profiles"></a>S/MIME 电子邮件配置文件

创建 S/MIME 签名和加密证书配置文件后，即可[为 iOS 本机邮件启用 S/MIME](email-settings-ios.md)。