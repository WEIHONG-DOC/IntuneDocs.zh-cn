---
title: Microsoft Intune App SDK Xamarin Bindings
description: 借助 Intune App SDK Xamarin Bindings，可在使用 Xamarin 生成的 iOS 和 Android 应用中启用 Intune 应用保护策略。
keywords: sdk、Xamarin、intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/08/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 275d574b-3560-4992-877c-c6aa480717f4
ms.reviewer: aanavath
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 079b27c73a466ae19dad950564ba0d56d8e20f8d
ms.sourcegitcommit: a474a6496209ff3b60e014a91526f3d163a45438
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "44031263"
---
# <a name="microsoft-intune-app-sdk-xamarin-bindings"></a>Microsoft Intune App SDK Xamarin Bindings

> [!NOTE]
> 你可能希望首先阅读 [ Intune App SDK 入门指南](app-sdk-get-started.md)一文，其中介绍了如何为每个受支持的平台上的集成做准备。

## <a name="overview"></a>概述
借助 [Intune App SDK Xamarin Bindings](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)，可在使用 Xamarin 生成的 iOS 和 Android 应用中启用 [Intune 应用保护策略](/intune-classic/deploy-use/protect-app-data-using-mobile-app-management-policies-with-microsoft-intune)。 该绑定使开发人员可以轻松将 Intune 应用保护功能内置到基于 Xamarin 的应用中。

通过 Microsoft Intune App SDK Xamarin Bindings，可将 Intune 应用保护策略（也称为 APP 或 MAM 策略）合并到使用 Xamarin 开发的应用中。 启用了 MAM 的应用程序是指与 Intune App SDK 集成的应用程序。 在 Intune 主动管理移动应用时，IT 管理员可将应用保护策略部署到该应用。

## <a name="whats-supported"></a>支持的功能

### <a name="developer-machines"></a>开发人员计算机
* Windows（Visual Studio 版本 15.7+）
* macOS

### <a name="mobile-app-platforms"></a>移动应用平台
* Android
* iOS

### <a name="intune-mobile-application-management-scenarios"></a>Intune 移动应用程序管理方案

* Intune APP-WE（无需设备注册）
* 注册了 Intune MDM 的设备
* 注册了第三方 EMM 的设备

使用 Intune App SDK Xamarin Bindings 生成的 Xamarin 应用现在可以在已注册和未注册 Intune 移动设备管理 (MDM) 的设备上接收 Intune 应用保护策略。

## <a name="prerequisites"></a>必备条件

查看[许可条款](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/blob/master/Microsoft%20License%20Terms%20Intune%20App%20SDK%20Xamarin%20Component.pdf)。 打印并保留一份许可条款，以留作记录。 下载和使用 Intune App SDK Xamarin Bindings 即表示你同意这些许可条款。 如果不接受这些条款，请不要使用此软件。

## <a name="enabling-intune-app-protection-polices-in-your-ios-mobile-app"></a>在 iOS 移动应用中启用 Intune 应用保护策略
1. 向 Xamarin.iOS 项目添加 [Microsoft.Intune.MAM.Xamarin.iOS NuGet 包](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.iOS)。
2.  按照将 Intune App SDK 集成到 iOS 移动应用的常规必需步骤操作。 可以从 [Intune App SDK for iOS 开发人员指南](app-sdk-ios.md#build-the-sdk-into-your-mobile-app)中集成说明的第 3 步开始操作。 可跳过运行 IntuneMAMConfigurator 一节中的最后一步，因为此工具包含在 Microsoft.Intune.MAM.Xamarin.iOS 包中，并将在生成时自动运行。
    **重要说明**：在 Visual Studio 中为应用启用密钥链共享与在 Xcode 中略有不同。 打开应用的“权利”plist 文件，并确保已启用“启用密钥链”选项，且已在相应部分中添加了相应的密钥链共享组。 然后，对于所有相应的配置/平台组合，请确保已在项目的“iOS 捆绑包签名”选项的“自定义权利”字段中指定了“权利”plist 文件。
3.  添加绑定且正确配置应用后，应用即可开始使用 Intune SDK 的 API。 为此，必须添加以下命名空间：

      ```csharp
      using Microsoft.Intune.MAM;
      ```
4. 若要开始接收应用保护策略，必须在 Intune MAM 服务中注册应用。 如果应用已使用 Azure Active Directory Authentication Library (ADAL) 验证用户，应用应在成功验证用户后，向 IntuneMAMEnrollmentManager 的 registerAndEnrollAccount 方法提供用户的 UPN：
      ```csharp
      IntuneMAMEnrollmentManager.Instance.RegisterAndEnrollAccount(string identity);
      ```
      **重要说明**：请务必使用应用中的设置替代 Intune App SDK 的默认 ADAL 设置。 可以通过应用 Info.plist 中的 IntuneMAMSettings 字典执行此操作，如 [Intune App SDK for iOS 开发人员指南](app-sdk-ios.md#configure-settings-for-the-intune-app-sdk)中所述。也可以使用 IntuneMAMPolicyManager 实例的 AAD 替代属性。 对于 ADAL 设置是静态的应用，建议使用 Info.plist 方法；对于在运行时确定这些值的应用，建议使用替代属性。 
      
      如果应用不使用 ADAL，且希望使用 Intune SDK 处理身份验证，应用应调用 IntuneMAMEnrollmentManager 的 loginAndEnrollAccount 方法：
      ```csharp
       IntuneMAMEnrollmentManager.Instance.LoginAndEnrollAccount([NullAllowed] string identity);
      ```
      
> [!NOTE] 
> 没有适用于 iOS 的重映射器。 集成到 Xamarin.Forms 应用应与集成到常规 Xamarin.iOS 项目的操作相同。 

## <a name="enabling-intune-app-protection-policies-in-your-android-mobile-app"></a>在 Android 移动应用中启用 Intune 应用保护策略

对于不使用 UI 框架的基于 Xamarin 的 Android 应用，需要阅读并遵循 [Intune App SDK for Android 开发人员指南](app-sdk-android.md)。 对于基于 Xamarin 的 Android 应用，需要根据本指南所包含的[表](app-sdk-android.md#replace-classes-methods-and-activities-with-their-mam-equivalent)将类、方法和活动替换为其 MAM 等效项。 如果应用没有定义 `android.app.Application` 类，则需要创建一个，并确保继承自 `MAMApplication`。

### <a name="xamarinandroid-integration"></a>Xamarin.Android 集成

1. 向 Xamarin.Android 项目添加 [Microsoft.Intune.MAM.Xamarin.Android NuGet 包](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.Android)的最新版本。 这将向你提供使用 Intune 启用应用程序的必要参考。

2. 请完整阅读并遵循[用于 Android 的 Intune App SDK 开发人员指南](app-sdk-android.md)，并特别注意：
    1. [整个类和方法替换部分](app-sdk-android.md#replace-classes-methods-and-activities-with-their-mam-equivalent)。 
    2. [MAMApplication 部分](app-sdk-android.md#mamapplication)。 确保你的子类用 `[Application]` 属性正确修饰并替代 `(IntPtr, JniHandleOwnership)` 构造函数。
    3. 如果你的应用针对 AAD 执行身份验证，请注意 [ADAL 集成部分](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal)。
    4. 如果计划从应用程序中的 MAM 服务获取策略，请注意 [MAM-WE 注册部分](app-sdk-android.md#app-protection-policy-without-device-enrollment)。

> [!NOTE]
> 尝试在[用于 Android 的 Intune App SDK 开发人员指南](app-sdk-android.md)中查找 `Microsoft.Intune.MAM.Xamarin.Android` Bindings 的等效 API 时或根据该指南转换代码片段时，请注意 Xamarin 的绑定生成器会对 Android API 进行以下重要修改：
> * 会将所有标识符都转换为帕斯卡拼写法 (com.foo.bar -> Com.Foo.Bar)
> * 会将所有 get/set 操作转换为属性操作（例如 Foo.getBar() -> Foo.Bar、Foo.setBar("zap") -> Foo.Bar = "zap"）
> * 所有接口的名称都加上了字符“I”(FooInterface -> IFooInterface)

### <a name="xamarinforms-integration"></a>Xamarin.Forms 集成

除执行上述所有步骤外，对于 `Xamarin.Forms` 应用，我们还提供了 `Microsoft.Intune.MAM.Remapper` 包。 此包通过将 `MAM` 类注入到 `FormsAppCompatActivity` 和 `FormsApplicationActivity` 等常用 `Xamarin.Forms` 类的类层次结构中来为你完成类替换，因此可通过为 `OnMAMCreate` 和 `OnMAMResume` 等 MAM 等效函数提供替代以继续使用这些类。 若要使用该工具，请执行下列操作：

1.  向项目添加 [Microsoft.Intune.MAM.Remapper.Tasks](https://www.nuget.org/packages/Microsoft.Intune.MAM.Remapper.Tasks) NuGet 包。 如果尚未包含它们，它将自动添加 Intune APP SDK Xamarin 绑定。

2.  在上述步骤 2.2 中创建的 `MAMApplication` 类的 `OnMAMCreate` 函数中添加对 `Xamarin.Forms.Forms.Init(Context, Bundle)` 的调用。 此操作很有必要，因为通过 Intune 管理，你的应用程序可在后台时启动。

> [!NOTE]
> 由于此操作会重新编写 Visual Studio 用于 Intellisense 自动完成的依赖项，因此建议在重映射器首次运行后重启 Visual Studio 以使 Intellisense 正确识别这些更改。 


## <a name="support"></a>Support

你已完成将组件内置到应用中的基本步骤。 现在可以按照 Xamarin Android 示例应用中的所述步骤进行操作。 我们提供了两个示例，一个用于 Xamarin.Forms，另一个用于 Android。

## <a name="requiring-intune-app-protection-policies-in-order-to-use-your-xamarin-based-android-lob-app-optional"></a>需要 Intune 应用保护策略才能使用基于 Xamarin 的 Android LOB 应用（可选） 

按照以下指南，可确保基于 Xamarin 的 Android LOB 应用只能由受 Intune 保护的用户在其设备上使用。 

### <a name="general-requirements"></a>一般要求
* Intune SDK 团队需要应用的应用程序 ID。 可在 [Azure 门户](https://portal.azure.com/)中“所有应用程序”下的“应用程序 ID”列找到此内容。 建议通过电子邮件 msintuneappsdk@microsoft.com 联系 Intune SDK 团队。
     
### <a name="working-with-the-intune-sdk"></a>使用 Intune SDK
以下说明专门面向最终用户设备上要求使用 Intune 应用保护策略的所有 Android 和 Xamarin 应用。

1. 使用 [Intune SDK for Android 指南](https://docs.microsoft.com/en-us/intune/app-sdk-android#configure-azure-active-directory-authentication-library-adal)中定义的步骤配置 ADAL。
> [!NOTE] 
> “客户端 ID”一词与 Azure 门户中与应用关联的“应用程序 ID”一词的含义相同。 
* 启用 SSO 需要“通用 ADAL 配置”#2。

2. 通过将以下值放入清单来启用默认注册：```xml <meta-data android:name="com.microsoft.intune.mam.DefaultMAMServiceEnrollment" android:value="true" />```
> [!NOTE] 
> 这必须是应用中唯一的 MAM-WE 集成。 如果有任何其他调用 MAMEnrollmentManager API 的尝试，则可能发生冲突。

3. 通过将以下值放入清单来启用所需的 MAM 策略：```xml <meta-data android:name="com.microsoft.intune.mam.MAMPolicyRequired" android:value="true" />```
> [!NOTE] 
> 这将强制应用在设备上下载公司门户，并且需要完成默认注册流程才能使用。

### <a name="working-with-adal"></a>使用 ADAL
以下说明是要求在最终用户设备上使用 Intune 应用保护策略的 .NET/Xamarin 应用的要求。

1. 请按照 ADAL 文档中 [Android 代理身份验证](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/tree/dev/adal#brokered-authentication-for-android)下定义的所有步骤操作。
> [!NOTE] 
> .NET ADAL 下一次将发布的版本 (3.17.4) 预计将包含实现此工作所需的修补程序。

如果你的组织已经是 Intune 的客户，请与 Microsoft 支持代表合作打开支持票证并在 [Github 问题页](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/issues)上创建一个问题，我们会尽快为你提供帮助。 

