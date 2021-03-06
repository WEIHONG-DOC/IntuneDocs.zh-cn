---
title: 将 Windows 10 设备的日志发送给公司支持人员 | Microsoft Docs
description: 将 Windows 10 1511 设备注册到 Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/25/2017
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 038747fb-5b52-47c4-a2b6-f9218da4cfe1
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.openlocfilehash: 1e9b9908fcc48e9137c07f9a5397661d66e5be95
ms.sourcegitcommit: 490365fb8b5405f323b4358fb1ec9dfdd9ff2d58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2018
ms.locfileid: "43146733"
---
# <a name="send-logs-to-your-company-support-from-the-settings-app-for-windows-10"></a>通过 Windows 10 的“设置”应用将日志发送给公司支持人员

如果在使用公司管理的 Windows 10 设备时遇到错误，可以通过电子邮件向公司支持人员发送信息，以帮助他们解决问题。 此信息保留在设备上一个名为_诊断日志_的专用文档中。

1. 通过转到“开始菜单”并选择“设置”按钮，打开 Windows“设置”应用。 还可以在搜索栏中搜索“设置”。
2. 转至“帐户” > “访问工作或学校”。
3. 选择“导出管理日志文件”。

   ![“访问工作或学校屏幕”显示了“相关设置”标题下的“导出”选项。](./media/w10-export-logs.png)

4. 日志将保存在 **C:\Users\Public\Public Documents\MDMDiagnostics** 中。 将创建两个文件：一个是日志本身；另一个是一个特殊文档，允许管理员使用其他程序（如 Microsoft Excel）查看日志。 将这两个文件附加到电子邮件中发送给管理员。如果多次执行此操作，请仅从创建日志的那天选择文件。 

另外，可能还需要[通过公司门户应用发送日志](send-logs-to-your-it-admin-cp-windows.md)，以便为公司支持人员提供更多帮助，协助他们尽力对所发现的问题进行故障排除。 

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。
