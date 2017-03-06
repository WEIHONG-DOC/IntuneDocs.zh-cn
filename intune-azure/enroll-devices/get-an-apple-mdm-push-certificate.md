---
title: "获取 Apple MDM Push Certificate"
titleSuffix: Intune Azure preview
description: "Intune Azure 预览版：了解获取 Apple MDM Push Certificate 以使用 Intune 管理 iOS 设备的步骤。"
keywords: 
author: staciebarker
ms.author: stabar
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: 153cce3809e24303b8f88a833e2fc7bdd9428a4a
ms.openlocfilehash: 26991bd0c7632d04b75ecbec023d96c1045f337a
ms.lasthandoff: 02/18/2017


---

# <a name="get-an-apple-mdm-push-certificate"></a>获取 Apple MDM Push Certificate 

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

Intune 启用了 iPad、iPhone 和 Mac OS X 设备的移动设备管理 (MDM)，并允许用户访问公司电子邮件和应用。 必须拥有 Apple 推送通知服务 (APNs) 证书，才能使用 Intune 管理 iOS 和 Mac 设备。 在将证书添加到 Intune 后，用户可以安装公司门户应用以注册其设备，或者你可以设置公司拥有的 iOS 设备管理。

## <a name="steps-to-get-your-certificate"></a>获取证书的步骤
在 Azure 门户中，选择“更多服务” > “监视 + 管理” > “Intune”。 在“Intune”边栏选项卡上，选择“注册设备” > “Apple MDM Push Certificate”，然后按照 Azure 门户中的编号步骤操作，如下所示。

**步骤 1.下载创建 Apple MDM Push Certificate 所需的 Intune 证书签名请求。**<br>
选择“下载 CSR”，本地下载并保存 .csr 文件。 .Csr 文件用于从 Apple 推送证书门户请求信任关系证书。

**步骤 2：创建 Apple MDM Push Certificate。**<br>
选择“创建 MDM Push Certificate”，转到 Apple Push Certificate 门户。 使用公司 Apple ID 登录，从而使用 .csr 文件创建 Push Certificate。 在 Apple Push Certificates 门户上选择“上传”后，将收到 .json 文件。 请将此文件用于 Push Certificate。 完成下载后，返回第三方服务器证书的 Apple Push Certificates 门户，然后选择“下载”。 下载 Push Certficate（.pem 文件）并在本地保存该文件。
备注

**步骤 3：输入用于创建 Apple MDM Push Certificate 的 Apple ID。**

**步骤 4：浏览到你的 Apple MDM Push Certificate 以进行上传。**<br>
转到证书 (.pem) 文件，选择“打开”，然后选择“上传”。 使用 Push Certificate，Intune 可通过将策略推送到已注册的移动设备来注册和管理 iOS 设备。
