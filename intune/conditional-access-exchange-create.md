---
title: 创建 Exchange 条件访问策略
titlesuffix: Microsoft Intune
description: 在 Intune 中配置 Exchange 内部部署的条件访问和旧版 Exchange Online Dedicated。
keywords: ''
author: msmimart
ms.author: mimart
manager: dougeby
ms.date: 02/22/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 127dafcb-3f30-4745-a561-f62c9f095907
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 4fd82cf211360e77b17f8ea915c13719b8ab3408
ms.sourcegitcommit: cd97505d6f5dc54db7f35a691376bcbf6f36ac9d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39323236"
---
# <a name="create-a-conditional-access-policy-for-exchange-on-premises-and-legacy-exchange-online-dedicated"></a>为本地 Exchange 和旧版 Exchange Online Dedicated 配置条件访问策略

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

本文介绍如何基于设备符合性配置本地 Exchange 的条件访问。

如果你具有 Exchange Online Dedicated 环境并需要确定其采用的是新配置还是旧配置，请与帐户管理员联系。 若要控制对 Exchange 内部部署或旧版 Exchange Online Dedicated 环境的电子邮件访问，请在 Intune 中配置 Exchange 内部部署的条件性访问。

## <a name="before-you-begin"></a>在开始之前

在可配置条件访问之前，请先验证以下内容：

- Exchange 版本必须是 **Exchange 2010 SP1 或更高版本**。 支持 Exchange Server 客户端访问服务器 (CAS) 阵列。

- 必须使用 [Exchange Active Sync 本地 Exchange 连接器](exchange-connector-install.md)，它将 Intune 连接到本地 Exchange。

    >[!IMPORTANT]
    >本地 Exchange 连接器特定于你的 Intune 租户，且不能用于其他任何租户。 Intune 现支持每个订阅有多个本地 Exchange 连接器。 如果你拥有多个本地Exchange组织，则可以为每个 Exchange 组织设置一个单独的连接器。

- 本地 Exchange 组织的连接器可以安装在任何能够与 Exchange 服务器通信的计算机上。

- 此连接器支持 **Exchange CAS 环境**。 如果愿意，可在 Exchange CAS 服务器上直接安装该连接器，但不建议这样做，因为这增加了服务器上的负荷。 在配置连接器时，必须对其进行设置，以便与其中一个 Exchange CAS 服务器通信。

- 必须使用基于证书的身份验证或用户凭据条目来配置 Exchange ActiveSync。

- 当配置条件性访问策略并将其面向用户时，在用户可以连接到其电子邮件前，他们使用的**设备**必须：
    - **已注册**到 Intune 或是已加入域的 PC。
    - **已在 Azure Active Directory 中注册**。 此外，还必须向 Azure Active Directory 注册客户端 Exchange ActiveSync ID。
<br></br>
- Azure AD 设备注册服务 (DRS) 会对 Intune 和 Office 365 客户自动激活。 已经部署了 ADFS 设备注册服务的用户不会在他们本地的 Active Directory 上看到已注册的设备。 **这不适用于 Windows 电脑和 Windows Phone 设备**。

- **符合**部署到该设备的设备符合性策略。

- 如果设备不满足条件性访问设置，则用户会在登录时会看到以下消息的其中一条：
    - 如果未向 Intune 注册设备，或未在 Azure Active Directory 中注册，则会显示一条消息，其中包含有关如何安装公司门户应用、注册设备和激活电子邮件的说明。 此过程也将设备的 Exchange ActiveSync ID 和 Azure Active Directory 中的设备记录相关联。
    - 如果设备不合规，则会显示一条消息，将用户定向到 Intune 公司门户网站或公司门户应用，用户可在其中找到有关该问题及其修正方式的信息。

### <a name="support-for-mobile-devices"></a>对移动设备的支持

- Windows Phone 8.1 及更高版本
- iOS 上的本机电子邮件应用。
- EAS 邮件客户端（如 Android 4 或更高版本上的 Gmail）。
- EAS 邮件客户端 Android 工作配置文件设备：Android 工作配置文件设备上仅支持工作配置文件中的 Gmail 和 Nine Work for Android Enterprise。 为了使条件访问适用于 Android 工作配置文件，必须为 Gmail 或 Nine Work for Android Enterprise 部署电子邮件配置文件，还要将这些应用部署为必需的安装。

> [!NOTE]
> 不支持 Android 和 iOS 上的 Microsoft Outlook 应用。 

### <a name="support-for-pcs"></a>对 PC 的支持

Windows 8.1 和更高版本上的本机**邮件**应用程序（向 Intune 注册时）


## <a name="configure-exchange-on-premises-access"></a>配置 Exchange 内部部署访问权限

1. 转到 [Azure 门户](https://portal.azure.com/)，然后使用 Intune 凭据登录。

1. 成功登录后，会看到“Azure 仪表板”。

1. 从左侧菜单中选择“所有服务”，然后在文本框筛选器中键入 Intune。

1. 选择“Intune”，将看到“Intune 仪表板”。

1. 选择“本地访问”。 “本地访问”窗格中显示了条件访问策略的状态和受其影响的设备。

1. 在“管理”下，选择“Exchange 内部部署访问”。

1. 在“Exchange 本地访问”窗格上，选择“是”以启用 Exchange本地访问控制。

    > [!NOTE]
    > 如果尚未配置 Exchange Active Sync 本地连接器，则禁用此选项。  启用 Exchange 本地部署的条件性访问之前，必须首先安装并配置至少一个连接器。 有关详细信息，请参阅[安装 Intune 本地 Exchange Connector](exchange-connector-install.md)

1. 在“分配”下，选择“包含的组”。  使用应该应用条件性访问的安全用户组。 用户需在 Intune 中注册设备并满足符合性配置文件的要求，然后才可执行此操作。

1. 如果想排除特定的用户组，可通过选择“排除的组”，并选择不需要设备注册和符合性的用户组。

1. 在“设置”下，选择“用户通知”以修改默认的电子邮件消息。 设备不符合要求，且用户想访问 Exchange 内部部署时将向用户发送此消息。 消息模板使用的是标记语言。  键入时还可看到消息的预览显示情况。
    > [!TIP]
    > 若要了解有关标记语言的详细信息，请参阅这篇维基百科[文章](https://en.wikipedia.org/wiki/Markup_language)。

1. 在“高级 Exchange Active Sync 访问设置”窗格上，针对非 Intune 托管的设备的访问设置全局默认规则，而针对平台级别的规则，请按以下两个步骤操作。

1. 对于不受条件性访问或其他规则影响的设备，可以选择允许或阻止该设备访问 Exchange。

   - 将此项设置为允许访问时，所有设备均可立即访问本地 Exchange。  如果属于“包含的组”中用户的设备之后被评估为不符合合规性策略或未在 Intune 中注册，将阻止此设备。
   - 将此项设置为阻止访问时，一开始会立即阻止所有设备访问本地 Exchange。  “包含的组”中的用户在 Intune 中注册其设备且该设备被评为符合之后，这些设备即获得访问权限。 始终阻止未运行 Samsung Knox Standard 的 Android 设备，因为系统不支持此设置。

1. 在“设备平台例外”下，选择“添加”以指定平台。 如果将“非托管设备访问”设置为“已阻止”，则即使平台专门阻止，已注册且符合要求的设备仍可访问。 选择“确定”保存设置。

1. 在“本地”窗格上，单击“保存”以保存条件访问策略。

## <a name="create-azure-ad-conditional-access-policies-in-intune"></a>在 Intune 中创建 Azure AD 条件性访问策略

自 Intune 1704 版本起，管理员可通过 Intune Azure 门户创建 Azure AD 条件访问策略，而无需在 Azure 和 Intune 工作负荷之间切换。

> [!IMPORTANT]
> 需要具备 Azure AD Premium 许可证才能从 Intune Azure 门户创建 Azure AD 条件性访问策略。

### <a name="to-create-azure-ad-conditional-access-policy"></a>创建 Azure AD 条件访问策略

1. 在“Intune 仪表板”中，选择“条件访问”。

2. 在“策略”窗格中，选择“新建策略”，创建新的 Azure AD 条件访问策略。

## <a name="see-also"></a>另请参阅

[Azure Active Directory 中的条件访问](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
