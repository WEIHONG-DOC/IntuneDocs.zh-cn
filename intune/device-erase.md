---
title: 清除 macOS 设备
titleSuffix: Microsoft Intune
description: 了解如何从 macOS 设备中清除所有数据（包括操作系统）。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/31/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: d99bef78d635f98f9c888d8096247f314ade6a52
ms.sourcegitcommit: 5eba4bad151be32346aedc7cbb0333d71934f8cf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31020922"
---
# <a name="erase-all-data-from-a-macos-device"></a>从 macOS 设备中清除所有数据

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

可以清除 macOS 设备中的所有数据，包括操作系统。 该设备也会从 Intune 管理中删除。 最终用户不会看到任何警告。

1. 在 [Azure 门户的 Intune 中](https://aka.ms/intuneportal)，选择“设备” > “所有设备”，然后选择要清除的设备。
![屏幕截图](./media/device-erase/choosedevice.png)
2. 单击“更多” > “清除”，然后提供 6 位数的恢复 PIN。 必须将此 PIN 提供给用户，以便其在设备上重新安装操作系统。 请务必记下此 PIN，因为在清除操作完成后它不会显示。
![屏幕截图](./media/device-erase/providepin.png)
3. 单击“确定”以清除设备。
