---
title: 使用 Power BI 连接到数据仓库
titlesuffix: Microsoft Intune
description: 可下载一个文件与 Microsoft Power BI 结合使用，从而为 Microsoft Intune 租户加载动态生成的交互式报表。
keywords: Intune 数据仓库
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/15/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 5E5A35D3-88F8-441B-8A0B-C5D7A1E5137B
ms.reviewer: aanavath
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: ac71716ed09e39817743ebe4301c08a898e8f41f
ms.sourcegitcommit: 34e96e57af6b861ecdfea085acf3c44cff1f3d43
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
ms.locfileid: "34223469"
---
# <a name="connect-to-the-data-warehouse-with-power-bi"></a>使用 Power BI 连接到数据仓库

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

可下载一个文件与 Microsoft Power BI 结合使用，从而为 Intune 租户加载动态生成的交互式报表。 数据仓库 Power BI 文件 (pbix) 包含租户连接设置及以下示例报表和图表：  

  -  设备
  -  注册
  -  应用保护策略
  -  合规性策略
  -  设备配置文件
  -  软件更新
  -  设备清单日志

还有十分有用的有关注册、符合性、设备配置文件和软件更新的趋势。 示例图表和报表向画布应用便于用户使用的筛选器。 若要使用高级筛选器，请查看 Power BI Desktop 中的“筛选器”窗格。

以下步骤介绍如何下载 Power BI 文件以及如何配合使用 Power BI 和 OData 链接。

[!INCLUDE [reports-credential-reqs](./includes/reports-credential-reqs.md)]

## <a name="install-power-bi"></a>安装 Power BI

安装最新版本的 Power BI Desktop。 可从 [PowerBI.microsoft.com](https://powerbi.microsoft.com/desktop) 下载 Power BI Desktop

## <a name="load-the-data-and-reports-using-the-power-bi-file-pbix"></a>使用 Power BI 文件 (pbix) 加载数据和报表

Power BI 文件 (pbix) 包含租户连接信息和一组基于数据仓库数据模型的预置报表。 在 Power BI Desktop 中打开文件并登录 Azure AD。 报表从 Intune 租户加载数据。

> [!Important]  
> 每个 Power BI 文件 (pbix) 可能会因租户位置而有所不同。 如果要管理多个 Intune 租户，请在登录该租户时，确保使用从 Azure 门户下载的文件。  

1.  登录 Azure 门户，选择“监视 + 管理” > “Intune”。 还可搜索 Intune 资源。  
2.  打开“Microsoft Intune 数据仓库 API (预览)”边栏选项卡。
3.  选择“下载 PowerBI 文件”。 扩展名为 (Pbix) 的文件将下载到指定位置。
4.  使用 Power BI 打开文件。 此时会加载“Intune 数据仓库报表”，但可能需要一些时间才能获取租户数据。
5.  选择“刷新”，加载租户数据并查看报表。
6.  如果 Power BI 尚未对 Azure Active Directory 凭据进行身份验证，则 Power BI 会提示用户提供凭据。 选择凭据时，请选择“组织帐户”作为身份验证方法。

## <a name="load-the-data-in-power-bi-using-the-odata-link"></a>使用 OData 链接加载 Power BI 中的数据

借助经 Azure AD 身份验证的客户端，OData URL 可连接到数据仓库 API 中的 RESTful 终结点，该终结点向报告客户端公开数据模型。 按以下说明使用 Power BI Desktop 连接并创建自己的报表。 无需局限于 Power BI Desktop，可将自己最喜爱的分析工具与 OData URL 配合使用，前提是客户端支持 OAUTH2.0 身份验证和 OData v4.0 标准。

1.  登录 Azure 门户，选择“监视 + 管理” > “Intune”。 还可搜索 Intune 资源。  
2.  打开“Microsoft Intune 数据仓库 API (预览)”边栏选项卡。
3. 在报表边栏选项卡中检索自定义源 URL，例如 `https://fef.{yourinfo}.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=beta`
4. 打开 Power BI Desktop。
5. 选择“开始” > “获取数据”。 选择“OData 源”。
6. 选择“基本”。
7. 在 URL 框中键入或粘贴 OData URL。
8. 选择“确定”。
9. 如果尚未从 Power BI 桌面客户端为租户进行 Azure AD 身份验证，请键入凭据。 必须使用 OAuth 2.0 获得 Azure Active Directory (Azure AD) 授权后才能访问数据。  
    1.  选择“组织帐户”。  
    2.  键入用户名和密码。  
    3.  选择“登录”。  
    4.  选择“**连接**”。  
10. 选择“加载”。

## <a name="next-steps"></a>后续步骤

可获取环境相关问题的答案，例如在上周白天注册的设备数。 可借助一些报表来获取有关 Intune 租户和客户总体的见解，这些报表使用从 Azure 中边栏选项卡检索的 Intune 数据仓库 Power BI 文件 (pbix)。 同时，Intune 还提供其他许多扩展或重用数据的方法。 可使用 Power BI 和 Intune 数据仓库 API 执行的操作还有许多，例如：

<!-- -  You can use Power BI Desktop to create additional report types with your data. For example, you could create a custom chart representing the ratio of device manufactures in your enterprise. For more information about creating custom reports with Power BI and the Intune Data Warehouse, see `BLOG POST ON POWER BI`. -->
 -  已整理租户数据，便于用户从数据中获取见解。 有关数据组织方式的详细信息，请参阅[数据仓库数据模型](reports-ref-data-model.md)。
 -  还可以从 RESTful 接口访问数据，并将数据整合到自己的应用中。 有关详细信息，请参阅[使用 REST 客户端从数据仓库 API 获取数据](reports-proc-data-rest.md)。
