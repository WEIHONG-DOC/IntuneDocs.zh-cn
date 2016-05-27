---
# required metadata

title: Intune 的常见使用方式 | Microsoft Intune
description:
keywords:
author: jeffgilb
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 1f37d4ff-b5a7-4a89-8884-a6184908b09c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: jeffgilb
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Intune 的常见使用方式

在深入探讨实现任务之前，务必使公司的企业移动性利益干系人在业务目标上保持一致。  不管你是刚购买企业移动性产品还是迁移自另一个产品，这一点都很重要。  对企业移动性的需求在不断地动态演化，用于解决这些需求的 Microsoft 方法有时可能不同于市场上的其他解决方案。  在业务目标上保持一致的最好办法是，从你想要为员工、合作伙伴和 IT 实现的方案的角度，来表达你想达成的目标。  下面简单介绍了 6 种依赖于 Intune 的最常见的方案，并附有关于如何规划和部署其中每个方案的详细信息的链接。

>[!NOTE] 是否想了解 Microsoft IT 如何使用 Intune 来允许 Microsoft 员工访问其移动设备上的公司资源，同时保护公司数据？ 若要详细了解 Microsoft IT 如何使用 Intune 和其他服务来管理标识、设备、应用及数据，请[阅读本技术案例研究](https://www.microsoft.com/itshowcase/Article/Content/588)。  

## 保护你的本地电子邮件和数据以供移动设备安全访问
大多数企业移动性战略的第一步是制定一项计划，使在外部 Internet 上使用移动设备的员工能够安全地访问电子邮件。 许多组织仍然在公司网络上托管了本地数据和应用程序服务器（如 Microsoft Exchange）。 Intune 和企业移动性套件 (EMS) 为 Exchange Server 提供了独一无二的集成式条件性访问解决方案，确保在向 Intune 注册设备之前，任何移动应用都无法访问电子邮件，并且完全无需在公司网络边缘再部署一个网关计算机！

除了电子邮件，Intune 还支持对需要安全访问本地数据的移动应用（例如业务线应用服务器）启用访问权限。  为此，通常需要将用于访问控制的 Intune 托管证书与外围中的标准 VPN 网关或代理（如 Microsoft Azure AD 应用程序代理）结合使用。  在这些情况下，访问公司数据的唯一方法是将设备注册到管理系统中。  注册后，管理系统可确保访问公司数据的设备符合你的策略。  此外，可以借用 Intune 的应用包装工具将已访问的数据包含在业务线应用中，这样它就不能将公司数据传递给消费者应用或服务。

<!-- Learn more about how to plan and deploy Intune to help secure on-premises email and data. -->

## 保护你的 Office 365 电子邮件和数据以供移动设备安全访问
在 Office 365 中保护公司数据（电子邮件、文档、即时消息、联系人）既方便了你，又给用户带来了更加顺畅的体验。 Intune 和企业移动性套件提供了独一无二的集成式条件性访问解决方案，确保用户、应用或设备在符合公司的合规性要求（已执行多重身份验证，已向 Intune 注册，使用托管应用、受支持的 OS 版本、设备 PIN 和低用户风险配置文件等等）之前无法访问 Office 365 数据。 位于其各自应用存储中的 Office 移动应用可以与数据包含策略（可通过 Intune 配置）结合使用，使你能够避免与不受 IT 管理的应用（例如本机电子邮件应用）和存储位置（例如 Dropbox）共享数据。  此功能完全内置于 Office 365 和 EMS 中。  你无需部署其他基础结构便可获得此功能。

在常见的 Office 365 部署做法中，如果需要使用公司应用/证书/Wi-Fi/VPN 配置完全预配设备（通常是公司拥有的设备），则必须将设备注册到管理系统中。  但是，如果用户只需访问公司电子邮件和文档（通常是个人拥有的设备），那么他需要使用 Office 移动应用（你已向其应用数据包含策略）并且完全跳过设备注册！  无论哪种方式，Office 365 数据都将受到已定义策略的保护。

<!-- Learn more about how to plan and deploy Intune to help secure Office 365 email and data. -->

## 为所有员工提供一个“自带设备办公”(BYOD) 计划
BYOD 可以降低硬件开销或增加员工的移动工作效率选择，因此受到越来越多组织的青睐。 现如今几乎人手一部手机，因此为什么还要往他们的口袋里再添一个？ 公司一直以来的主要难题就是说服员工将其个人设备注册到管理系统中，因为他们担心 IT 部门能看到其设备中的信息并对其设备进行处理。  

在设备注册不可行的情况下，Intune 提供替代的 BYOD 方法，可简单地管理包含公司数据的应用。  与 Office 移动应用一样，即使是有问题的应用访问公司和个人数据，Intune 也能保护公司数据。  作为管理员，你可以要求用户从 Office 移动应用访问 Office 365 并使用可保护数据的策略（已加密、受 PIN 保护等等）配置应用。  这些策略可防止在不受管理的应用和存储位置中丢失数据 — 无论是在这些应用的内部还是外部。  例如，这些策略会阻止用户将公司电子邮件配置文件中的文本复制到消费者电子邮件配置文件，即使这两个配置文件都是在 Outlook Mobile 中配置的。  可以为 BYOD 用户所需的其他服务和应用程序部署类似的配置。

<!-- Learn more about how to plan and deploy Intune to support BYOD.-->

## 向信息工作者发放公司拥有的手机
现在的大多数信息工作者都是移动办公，这使得移动设备上的工作效率成为提高竞争力的必要途径。  这些员工需要随时随地无缝访问所有公司应用和数据。  你需要确保公司数据是安全的并且管理成本较低。  

Intune 提供了大量预配和管理解决方案，这些解决方案与当今市场上的主流公司设备管理平台集成，包括 Apple 设备注册计划和 Samsung KNOX 移动安全平台。  通过使用 Intune 集中创作设备配置，可实现公司设备预配的高度自动化。  

想象一下：将一个未开封的 iPhone 手机盒发放给员工。 员工打开手机后，完成公司自创的设置流程，在此过程中他必须进行身份验证。 这部 iPhone 手机无缝配置了安全策略（加密硬盘驱动器、设备 PIN 等等）、电子邮件/Wi-Fi/VPN/证书配置文件和一系列基础应用。 然后，员工启动 Intune 公司门户应用来访问提供给他们的可选公司应用。

<!-- Learn more about how to plan and deploy Intune to support corporate owned devices. -->

## 向任务工作者发放使用受限的共享平板电脑
任务工作者开始越来越多地使用移动技术。  例如，共享平板电脑现在对于零售店员工已经是司空见惯了。  无论是用于处理销售还是即时检查库存，平板电脑都有助于创造良好的顾客交互体验。  在这种情况下，用户体验的简单性至关重要。  出于此原因，发放给员工的平板电脑通常采用使用受限模式，使员工只能与单个业务线应用交互。  Intune 允许你批量预配、保护和集中管理这些可配置为在此使用受限模式下运行的共享平板电脑。

<!-- Learn more about how to plan and deploy Intune to support shared tablets. -->

## 允许你的员工从不受管理的公用网亭安全访问 Office 365
有时，你的员工需要使用你无法管理的设备、应用或浏览器，例如展销会和酒店大堂的公用计算机。  你是否应该允许你的员工从其访问公司电子邮件？  使用 Intune 和企业移动性套件，你有多种选择。  答案可以是“不”，你只需限制为只允许受组织管理的设备访问电子邮件。  或者，你也可以选择允许这些不受信任的计算机进行有限访问，方法是：要求进行多重身份验证，并且仅允许在无法下载文件（例如电子邮件附件）的模式下进行浏览器访问 (Outlook Web Access)。  这将确保经过强身份验证的员工不会无意中将公司数据留在不受信任的计算机上。

<!-- Learn more about how to plan and deploy Intune to support kiosks. -->


<!--HONumber=May16_HO1-->

