---
title: 使用 Microsoft Intune 管理 Windows Holographic 设备 - Azure | Microsoft Docs
description: 通过 Microsoft Intune 可以在运行 Windows Holographic for Business 的设备上完成各种任务，包括配置公司门户、创建符合性策略、自定义 OMA-URI 设置、部署应用、将设备分类为组、创建配置文件、限制设备、进行软件更新、设置条款和条件、配置 VPN 和 Wi-Fi 设置，以及使用 Windows Hello 企业版。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 6/11/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 825ceb1eee8f6fdd38f8a203324ce3cad7291918
ms.sourcegitcommit: 4d314df59747800169090b3a870ffbacfab1f5ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43317989"
---
# <a name="customize-devices-running-windows-holographic-with-intune"></a>使用 Intune 对运行 Windows Holographic 的设备进行自定义设置

Microsoft Intune 支持运行 Windows Holographic for Business 的设备，例如 [Microsoft HoloLens](https://docs.microsoft.com/en-us/hololens/)。

若要使用 Microsoft Intune 管理运行 Windows Holographic 的设备，必须创建一个 Edition Upgrade 配置文件。 此升级配置文件能将设备从 Windows Holographic 升级至 Windows Holographic for Business。 对于 Microsoft HoloLens，则可以通过购买商业套件来获得升级所需的许可证。 有关详细信息，请参阅[将运行 Windows Holographic 的设备升级到 Windows Holographic for Business](holographic-upgrade.md)。

本文中的任务可帮助你管理和自定义运行 Windows Holographic for Business 的设备。 例如，你可以管理软件更新、配置 VPN 设置以及进行其他操作。

## <a name="azure-active-directory"></a>Azure Active Directory

Azure Active Directory (AD) 是帮助管理和控制运行 Windows Holographic for Business 的设备的绝佳资源。 使用 Intune 和 Azure AD 可以： 

- **[设置已加入 Azure Active Directory 的设备](https://docs.microsoft.com/azure/active-directory/device-management-azuread-joined-devices-setup)**：在 Azure Active Directory (AD) 中，可添加工作所有的 Windows 10 设备，包括运行 Windows Holographic for Business 的设备。 Azure AD 可使用此功能来控制设备。 此功能有助于确保用户从满足安全性和符合性标准的设备访问公司资源。

  请参阅 [Azure AD 中的设备管理简介](https://docs.microsoft.com/azure/active-directory/device-management-introduction)了解更多详细信息。

- **[Windows 设备的批量注册](windows-bulk-enroll.md)**：可将大量新的 Windows 设备加入到 Azure Active Directory (AD) 和 Intune。 此功能称为批量注册，并使用预配包。 这些包将运行 Windows Holographic for Business 的设备加入到 Azure AD 租户，并在 Intune 中注册它们。

## <a name="company-portal"></a>Company Portal
**[配置公司门户应用](company-portal-app.md)**

Intune 提供了公司门户应用，用户可使用该应用访问公司数据、注册设备、安装应用、联系 IT 部门等。 你可以为运行 Windows Holographic for Business 的设备自定义公司门户应用。

使用公司门户应用，还可以执行下列操作：

- 使用设置应用或公司门户应用[从 Intune 删除设备](/intune-user-help/unenroll-your-device-from-intune-windows)
- [重命名设备](/intune-user-help/rename-your-device-cpapp)
- 在设备上[安装应用](/intune-user-help/install-apps-cpapp-windows)
- 从设置应用或公司门户应用[手动同步设备](/intune-user-help/sync-your-device-manually-windows)


## <a name="compliance-policy"></a>合规性策略
**[创建设备符合性策略](compliance-policy-create-windows.md)**

符合性策略即设备为符合要求必须满足的规则和设置。 可以将这些策略与条件访问结合使用，阻止不符合要求的设备访问公司资源。 在 Intune 中可以为运行 Windows Holographic for Business 的设备创建符合性策略，从而允许或阻止其访问权限。 例如，可以创建一个要求启用 Bitlocker 的策略。

另请参阅[设备符合性策略入门](device-compliance-get-started.md)。

## <a name="deploy-and-manage-apps"></a>部署和管理应用
**[向 Intune 添加应用](apps-add.md)**

使用 Intune 可以向运行 Windows Holographic for Business 的设备添加应用。 有多种部署应用的方法，包括：

- [添加 Microsoft Store 应用](store-apps-windows.md)
- [添加自己创建的应用](lob-apps-windows.md)
- [将应用分配给组](apps-deploy.md)

Microsoft Intune 可以向运行 Windows Holographic for Business 的 Microsoft HoloLens 设备部署通用 Windows 应用。 可以直接在 Intune Azure 门户中上传应用包，或者从适用于企业的 Microsoft Store 对其进行部署。 有关相关区域的详细信息，请参阅下列文章：
- 要使用 Intune Azure 门户来部署业务线 (LOB) 应用，请参阅[如何向 Microsoft Intune 添加 Windows 业务线应用](lob-apps-windows.md)。
- 要使用适用于企业的 Microsoft Store 部署应用，请参阅[如何使用 Microsoft Intune 管理从适用于企业的 Microsoft Store 中购买的应用](windows-store-for-business.md)。 
- 要了解 Microsoft Intune 的应用管理，请参阅 [Microsoft Intune 中的应用管理](app-management.md)。
- 要详细了解如何开发 Microsoft HoloLens 应用，请参阅 [Microsoft HoloLens 混合现实应用](https://www.microsoft.com/hololens/apps)。 

> [!NOTE]
> 运行 Windows 10 Holographic for Business 1607 的 HoloLens 设备不支持来自适用于企业的 Microsoft Store 的在线许可应用。 若要了解详细信息，请参阅[在 HoloLens 上安装应用](https://docs.microsoft.com/en-us/hololens/hololens-install-apps)。

## <a name="device-actions"></a>设备操作
Intune 具有一些内置操作，允许 IT 管理员在本地设备上执行不同的任务，或者在 Azure 门户中使用 Intune 远程执行不同的任务。 用户还可从 Intune 公司门户中向在 Intune 中注册的个人所有设备发出远程命令。

使用运行 Windows Holographic for Business 的设备时，可使用以下操作： 

- **[擦除](devices-wipe.md#wipe)**：执行“擦除”操作可从 Intune 中删除设备，并将设备还原到其出厂默认设置。 请在将设备交给新用户之前或设备丢失或被盗时使用此操作。

- **[停用](devices-wipe.md#retire)**：执行“停用”操作可从 Intune 中删除设备。 此外，它还会删除 Intune 分配的托管应用数据、设置和电子邮件配置文件。 用户的个人数据保留在设备上。

- **[同步设备以获取最新策略和操作](device-sync.md)**：执行“同步”操作会强制设备使用 Intune 立即签入。 当设备签入时，该设备会立即收到分配给自己的任何挂起的操作或策略。 此功能有助于验证和对已分配的策略进行故障排除，而无需等待下一个安排的签入。

**[什么是 Microsoft Intune 设备管理？](device-management.md)** 是了解使用 Azure 门户管理设备的最佳资源。 

## <a name="device-categories-and-groups"></a>设备类别和组
**[将设备分类为组](device-group-mapping.md)**

使用 Intune 可以创建设备类别，例如销售、财务和人力资源等，并根据创建的类别将设备自动添加到组。 其目的是让管理运行 Windows Holographic for Business 的设备变得更轻松。

## <a name="device-configuration-profiles"></a>设备配置文件 
**[开始使用配置文件](device-profiles.md)并[创建自己的配置文件](device-profile-create.md)**

Intune 提供可在组织内的不同设备上启用或禁用的设置和功能。 这些设置和功能通过配置文件进行管理。 例如，可以创建一个在运行 Windows Holographic for Business 的设备上启用 Cortana 或使用 Windows Defender Smart Screen 的配置文件。

在配置文件中，可以使用 OMA-URI 来自定义某些设置、创建设备限制并配置虚拟专用网络 (VPN) 和 Wi-Fi。

#### <a name="custom-device-settingscustom-settings-windows-holographicmd"></a>[自定义设备设置](custom-settings-windows-holographic.md)

可通过在 Intune 中创建一个自定义配置文件来配置 OMA-URI（开放移动联盟统一资源标识符）设置。 可使用 OMA-URI 设置来控制 Windows Holographic for Business 设备上的各种功能，例如启用 VPN 或检查 Microsoft 更新上有无更新。

#### <a name="configure-kiosk-modekiosk-settingsmdwindows-holographic-for-business"></a>[配置展台模式](kiosk-settings.md#windows-holographic-for-business)

使用 Intune 提供的共享或来宾 PC 功能，可将 Windows Holographic for Business 设备配置为作为展台运行。 这些设备可以运行一个（单个应用展台模式）或多个应用（多个应用展台模式）。

#### <a name="device-restrictionsdevice-restrictions-windows-holographicmd"></a>[设备限制](device-restrictions-windows-holographic.md)

通过设备限制可以控制设备上的各种设置和功能，包括要求提供密码、从 [Microsoft Store](https://www.microsoft.com/store/apps/windows?icid=CNavAppsWindowsApps) 安装应用以及启用蓝牙等。 应在 Intune 配置文件中创建这些限制。 此配置文件可应用于运行 Windows Holographic for Business 的多个设备。

#### <a name="configure-vpnvpn-settings-configuremd"></a>[配置 VPN](vpn-settings-configure.md)

虚拟专用网络 (VPN) 可让你的用户安全远程访问你的公司网络。 在 Intune 中可以创建 VPN 配置文件并使其包含针对运行 Windows Holographic for Business 的设备的特定设置。 例如可以创建一个 VPN 配置文件，让所有 Windows Holographic for Business 设备均使用 Citrix VPN 作为连接类型。

#### <a name="configure-wi-fiwi-fi-settings-configuremd"></a>[配置 Wi-Fi](wi-fi-settings-configure.md)

还可以在 Intune 中创建 Wi-Fi 配置文件，为 Windows Holographic for Business 设备分配无线网络设置。 分配 Wi-Fi 配置文件后，最终用户无需进行任何网络配置即可获得企业网络访问权限。 例如，可以创建一个仅供 Windows Holographic for Business 设备使用的 Wi-Fi 网络。

## <a name="software-updates"></a>软件更新
**[管理软件更新](windows-update-for-business-configure.md)**

Intune 提供了一个名为“更新圈”的功能供 Windows 10 设备使用。 这些更新圈包括一组用于确定更新安装方式的设置。 例如，你可以创建一个维护时段来安装更新，也可以选择在安装更新后重新启动。 更新圈可应用于运行 Windows Holographic for Business 的多个设备。

## <a name="terms-and-conditions"></a>条款和条件
**[设置公司的用户访问条款和条件](terms-and-conditions-create.md)**

可以要求用户先接受你所在公司的条款和条件，然后才能注册设备和访问公司应用，包括电子邮件。 在 Intune 中可以定义条款和条件在公司门户中的显示方式，并将这些条款和条件分配给运行 Windows Holographic for Business 的设备。

## <a name="windows-hello-for-business"></a>Windows Hello 企业版
**[使用 Windows Hello 企业版](windows-hello.md)**

Windows Hello 企业版是使用 Azure Active Directory 帐户取代密码、智能卡或虚拟智能卡进行登录的一种替代方法。 Windows Holographic for Business 可以与 Windows Hello 企业版配合使用，使用你设置的最短 PIN 进行登录。
