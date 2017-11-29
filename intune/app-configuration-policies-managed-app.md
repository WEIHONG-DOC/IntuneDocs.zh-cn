---
title: "为受管理应用添加应用配置策略（无需设备注册）| Microsoft Docs"
titlesuffix: Azure portal
description: "了解如何为受管理应用添加应用配置策略（无需设备注册）。"
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.date: 10/31/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: c46d7e8f4291345a9da87f7a7a6f3180415b69a4
ms.sourcegitcommit: ce35790090ebe768d5f75c108e8d5934fd19c8c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>为受管理应用添加应用配置策略（无需设备注册）

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

可将应用配置策略用于托管应用，这些应用甚至在未注册设备上也支持 Intune App SDK。 

1. 登录到 Azure 门户。
2. 选择“更多服务” > “监视 + 管理” + “Intune”。
3. 选择“移动应用”工作负荷。
4. 在“管理”组中，选择“应用配置策略”，然后选择“添加”。
5. 设置以下详细信息：
    - **名称**  
      在 Azure 门户中显示的配置文件名称。
    - **描述**  
      在 Azure 门户中显示的配置文件说明。
    - **设备注册类型**  
      选择“管理应用”。
6. 选择“关联的应用”以选择要配置的应用。 从已同意并与 Intune 同步的应用列表中选择应用。
7. 对于该应用支持的每个配置设置，请键入“名称”和“值”，然后选择省略号 (…)。  
    若要删除配置，请选择省略号 (…)，然后选择“删除”。  
    启用了 Intune App SDK 的应用支持键值对形式的配置。 若要详细了解支持哪些键值配置，请参阅每个应用的相关文档。  
    此外，可使用将由应用程序生成的数据动态填充的令牌。

## <a name="configuration-values-for-using-tokens"></a>为使用令牌配置值

Intune 可以生成特定令牌，并将其发送至托管的应用程序。 例如，如果应用配置可使用电子邮件设置，则可通过使用令牌添加动态电子邮件。 在“名称”字段键入应用所需名称，然后在“值”字段键入 `\{\{mail\}\}`。

Intune 支持在配置设置中使用以下令牌类型：

- \{\{userprincipalname\}\} - 例如 John@contoso.com
- \{\{mail\}\} - 例如 John@contoso.com
- \{\{partialupn\}\} - 例如 John
- \{\{accountid\}\} - 例如 fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{deviceid\}\} - 例如 b9841cd9-9843-405f-be28-b2265c59ef97
- \{\{userid\}\} - 例如 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\} - 例如 John Doe
- \{\{PrimarySMTPAddress\}\} - 例如 testuser@ad.domain.com 


> [!Note]  
> \{\{ 和 \}\} 字符仅供令牌类型使用，不得用于其他目的。

## <a name="next-steps"></a>后续步骤

照常继续[分配](apps-deploy.md)和[监视](apps-monitor.md)应用。