---
title: "使用移动应用程序管理策略保护应用 | System Center Configuration Manager"
description: "修改部署的应用的功能，使它们符合公司的合规性和安全策略。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b7936-a5ca-45c5-8bef-10424eb2e091
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dfbf6b2001e3259abb7246ab463682b0ead4f4e8


---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>使用 System Center Configuration Manager 中的移动应用程序管理策略保护应用

*适用范围：System Center Configuration Manager (Current Branch)*

通过 System Center Configuration Manager 应用程序管理策略，可以修改部署的应用的功能，帮助应用符合公司的合规性策略和安全策略。 例如，你可以限制在受限制的应用内进行剪切、复制和粘贴操作，或配置应用以打开托管浏览器内的所有 Web 链接。 应用管理策略支持：  

-   运行 Android 4 和更高版本的设备。  

-   运行 iOS 7 和更高版本的设备。  

除了托管设备，你还可以移动应用管理策略以保护不由 Intune 管理的设备上的应用。 你可以使用这项新功能，为连接到 Office 365 服务的应用应用移动应用管理策略。 连接到内部部署 Exchange 或 SharePoint 的应用不支持此操作。  
若要使用这项新功能，必须使用 Azure 预览门户。 下列主题可帮你入门：  
-   [在 Azure 门户中开始使用移动应用管理策略](https://technet.microsoft.com/library/mt627830.aspx)  
-   [使用 Microsoft Intune 创建和部署移动应用管理策略](https://technet.microsoft.com/library/mt627829.aspx)  

与 Configuration Manager 中的配置项目和基线不同，不会直接部署应用程序管理策略。 而是将该策略与你想要进行限制的应用程序部署类型关联。 在设备上部署并安装了应用部署类型后，你指定的设置将生效。  

若要将限制应用到应用，该应用必须结合 Microsoft Intune 应用软件开发工具包 (SDK)。 有两种方式获得此类应用：  

-   **使用策略托管应用** （Android 和 iOS）：内置了应用 SDK。 要添加此类型的应用，你可以从 iTunes 应用商店或 Google Play 等应用商店指定应用的链接。 对于此类应用，无需进一步的处理。 有关可用于 iOS 和 Android 设备的策略托管应用的列表，请参阅 [Managed apps for Microsoft Intune mobile application management policies](https://technet.microsoft.com/en-us/library/dn708489.aspx)（Microsoft Intune 移动应用程序管理策略的托管应用）。  

-   **使用“已包装的”应用** —（Android 和 iOS）：使用 **Microsoft Intune 应用包装工具**重新进行封装以将应用 SDK 包括在内的应用。 该工具通常用于处理公司内部开发的应用。 它可用于处理从应用商店下载的应用。 请参阅 [Prepare iOS apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/dn878028.aspx) （使用 Microsoft Intune 应用包装工具为移动应用程序管理准备 iOS 应用）和 [Prepare Android apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/mt147413.aspx)（使用 Microsoft Intune 应用程序包装工具为移动应用程序管理准备 Android 应用）。  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>创建和部署具有移动应用程序管理策略的应用  
  
##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>步骤 1：获取指向策略托管应用的链接，或创建已包装的应用  

-   **“要获取策略托管应用的链接”** - 从应用商店查找并记录你想要部署的策略托管应用的 URL。  

     例如，Microsoft Word for iPad 应用的 URL 是 **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **创建包装的应用** - 使用主题 [Prepare iOS apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/dn878028.aspx) （使用 Microsoft Intune 应用包装工具为移动应用程序管理准备 iOS 应用）和 [Prepare Android apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/mt147413.aspx) （使用 Microsoft Intune 应用包装工具为移动应用程序管理准备 Android 应用）中的信息创建包装的应用。  

     创建处理过的应用和关联的清单文件的工具。 在创建包含该应用的 Configuration Manager 应用程序时，将使用这些文件。  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>步骤 2：创建包含应用的 Configuration Manager 应用程序  
 创建 Configuration Manager 应用程序的过程有所不同，具体取决于使用的是策略托管应用（外部链接）还是通过适用于 iOS 的 Microsoft Intune 应用包装工具（iOS 应用包）创建的应用。 使用以下过程之一创建 Configuration Manager 应用程序。  

1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建应用程序”  ，打开“创建应用程序向导”。  

4.  在“常规”  页上，选择“自动检测安装文件中有关此应用程序的信息” 。  

5.  在“类型”下拉列表中，选择“iOS 应用包(\*.ipa 文件)”。**  

6.  单击“浏览”  ，选择要导入的应用包，然后单击“下一步” 。  

7.  在“常规信息”  页上，输入希望用户在公司门户中看到的描述性文本和类别信息。  

8.  完成向导。  

 新应用程序会显示在“软件库”  工作区的“应用程序”  节点中。  
  
### <a name="create-an-application-containing-a-link-to-a-policy-managed-app"></a>创建包含指向策略托管应用的链接的应用程序  
  
1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序”。  
  
3.  在“主页”  选项卡上的“创建”  组中，单击“创建应用程序”  ，打开“创建应用程序向导”。  

4.  在“常规”  页上，选择“自动检测安装文件中有关此应用程序的信息” 。  

5.  在“类型”  下拉列表中，选择以下一项：  

    -   对于 iOS： **应用商店中的 iOS 应用包**  

    -   对于 Android： **Google Play 上的 Android 应用包**  

6.  （从步骤 1）输入应用的 URL，然后单击“下一步” 。  

7.  在“常规信息”  页上，输入希望用户在公司门户中看到的描述性文本和类别信息。  

8.  完成向导。  

 新应用程序会显示在“软件库”  工作区的“应用程序”  节点中。  

##  <a name="step-3-create-an-application-management-policy"></a>步骤 3：创建应用程序管理策略  
 接下来，创建一个将与该应用程序相关联的应用程序管理策略。 可以创建一个常规或托管浏览器策略。  
  
1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序管理策略”。  
3.  在“主页”  选项卡的“创建”  组中，单击“创建应用程序管理策略” 。  

4.  在“常规”  页上，输入策略的名称和说明，然后单击“下一步” 。  

5.  在“策略类型”  页上，选择此策略的平台和策略类型，然后单击“下一步” 。 可以使用下列策略类型：  

    -   **常规**：“常规”策略类型允许你修改所部署应用的功能，以帮助其符合公司的合规性和安全策略。 例如，可以限制受限应用中的剪切、复制和粘贴操作。  

    -   **托管浏览器**：配置是允许还是阻止托管浏览器打开 URL 列表。 “托管浏览器”策略类型可让你修改 Intune 托管浏览器应用的功能。 这是一个 Web 浏览器，可让你管理用户可以执行的操作（包括他们可以访问的站点）以及打开指向浏览器中内容的链接的方式。 详细了解  [适用于 iOS 的 Intune 托管浏览器应用](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) 和 [适用于 Android 的 Intune 托管浏览器应用](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en)。  

6.  在“iOS 策略”  或“Android 策略”  页上，根据需要配置以下值，然后单击“下一步” 。 该选项可能有所差异，这取决于你配置策略的设备类型。  

|值|更多信息|  
|-----------|----------------------|  
|**限制显示在企业托管浏览器内的 Web 内容**|如果启用此设备，应用内的任何链接都将在托管浏览器中打开。 你必须部署此应用，此选项才能工作。|  
|**“阻止 Android 备份”** 或 **“阻止 iTunes 和 iCloud 备份”**|禁止从应用备份任何信息。|  
|**允许应用向其他应用传送数据**|指定该应用可以发送数据的应用。 你可以选择不允许将数据传输到任何应用、仅允许传输到其他受限制的应用或允许传输到任何应用。<br /><br /> 对于 iOS 设备，若要防止在托管和非托管应用之间传输文档，你也必须配置并部署禁用 **“允许在其他非托管应用中使用托管文档”**设置的移动设备安全策略。<br /><br /> 如果你选择仅允许传输到其他受限制的应用，则 Intune PDF 和图片查看器（如果已部署）将用于打开各自类型的内容。|  
|**允许应用从其他应用接收数据**|指定应用可以接收数据的应用。 你可以选择不允许从任何应用传输数据、仅允许从其他受限制的应用传输数据或允许从任何应用传输数据。|  
|**防止“另存为”**|禁用任何使用此策略的应用使用 **“另存为”** 选项。|  
|**限制剪切、复制和粘贴到其他应用程序**|指定应用使用剪切、复制和粘贴操作的方法。 选择：<br /><br /> **“阻止”** – 不允许在本应用和其他应用间进行剪切、复制和粘贴操作。<br /><br /> **“策略托管的应用”** – 仅允许在本应用和其他受限制的应用间进行剪切、复制和粘贴操作。<br /><br /> **“可粘贴的策略托管应用”** – 允许从本应用剪切或复制的数据粘贴到其他受限制的应用。 允许将剪切或复制自任何应用的数据粘贴至此应用。<br /><br /> **“任何应用”** – 没有任何剪切、复制和粘贴操作限制。|  
|**访问需要简单 PIN**|要求用户输入他们指定使用此应用的 PIN 号码。 将会要求用户在首次运行该应用时进行设置。|  
|**重置 PIN 前的尝试次数**|指定输入 PIN 码的尝试次数，达到该次数后用户必须重置 PIN。|  
|**访问需要公司凭据**|要求用户在访问应用前必须输入他们的公司登录信息。|  
|**访问要求设备符合公司策略**|仅允许设备在未越狱或获取根权限时使用此应用。|  
|**在一定时间后重新检查访问要求（分钟）**|在 **“超时”** 字段，指定应用启动后重新检查访问要求前的时间段。<br /><br /> 在“离线宽限期”  字段，如果设备离线，指定应用重新检查访问要求前的时间段。|  
|**加密应用数据**|指定与本应用相关的所有数据都将加密，包括外部存储的数据，例如 SD 卡。<br /><br /> **适用于 iOS 的加密**<br /><br /> 对于与 Configuration Manager 移动应用程序管理策略相关的应用，使用操作系统提供的设备级别的加密对静止数据进行加密。 通过必须由 IT 管理员设置的设备 PIN 策略启用。 需要 PIN 时，数据将根据移动应用程序管理策略的设置进行加密。 正如 Apple 文档所述， [iOS 7 所使用的模块经过了 FIPS 140-2 的认证](http://support.apple.com/en-us/HT202739)。<br /><br /> **适用于 Android 的加官**<br /><br /> 对于与 Configuration Manager 移动应用程序管理策略关联的应用，加密由 Microsoft 提供。 根据移动应用程序管理策略的设置，数据在文件 I/O 运行过程中同步加密。 Android 上托管的应用利用平台加密库使用 CBC 模式的 AES-128 加密。 加密方法没有获得 FIPS 140-2 认证。 设备存储中的内容将始终被加密。|  
    |**“阻止屏幕捕捉”** （仅限于 Android 设备）|指定在使用该应用时，阻止设备的屏幕捕捉功能。|  

7.  在“托管浏览器”  页上，选择允许托管浏览器只打开列表中的 URL 或是阻止托管浏览器打开列表中的 URL，管理列表中的 URL，然后单击“下一步” 。  

    > [!WARNING]  
    >  有关详细信息，请参阅[使用托管浏览器策略管理 Internet 访问](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md)。  
  
8.  完成向导。  

 新策略显示在“软件库”  工作区的“应用程序管理策略”  节点中。  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>步骤 4：将应用程序管理策略与部署类型相关联  
 
 在为某个需要应用程序管理策略的应用创建部署类型时，Configuration Manager 将在部署相关应用时确认应用管理策略必须已链接到此部署类型并且提示你关联应用管理策略。 对于托管浏览器，将需要关联常规和托管浏览器策略。 有关详细信息，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md)。  
  
> [!IMPORTANT]  
>  如果已部署应用程序，新部署类型的部署将失败，除非完成此关联。 可以在“应用程序管理”  选项卡上应用程序的“属性”  中建立关联。  

> [!IMPORTANT]  
>  对于运行 iOS 7.1 之前的操作系统的设备，关联的策略只有在卸载应用后才能删除。  
>   
>  如果从 Configuration Manager 取消注册设备，则策略不会从应用中删除。 应用了策略的应用将保留策略设置，甚至在卸载并重新安装了该应用后也是如此。  

##  <a name="step-5-monitor-the-app-deployment"></a>步骤 5：监视应用部署  
 创建并部署关联移动应用程序管理策略的应用后，可以监视应用并解决任何策略冲突的问题。  
  
1.  在 Configuration Manager 控制台中，单击“软件库” > “概述” > “部署”。  
  
3.  选择该部署并在“主页”  选项卡上单击“属性” 。  

4.  在部署的详细信息窗格中，单击“相关对象”  下的“应用程序的管理策略” 。  

 有关监视应用程序的详细信息，请参阅[监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

##  <a name="how-policy-conflicts-are-resolved"></a>如何解决策略冲突  
 如果在第一次部署到用户或设备时出现移动应用程序管理策略冲突，则冲突中指定的设置值将从部署到应用的策略中删除，并且应用将使用内置冲突值。  

 如果在后续部署到应用或用户时出现移动应用管理策略冲突，则冲突的指定设备值将不会更新到部署到应用的移动应用管理策略，并且应用将使用该设置的现有值。  

 如果设备或用户收到两个冲突策略，则适用以下行为：  

-   如果策略已经部署到设备，则现有策略设置不会被覆盖。  

-   如果尚无策略部署到设备，并且两个冲突设置已经部署，则将使用设备内的默认设置。  

##  <a name="available-policy-managed-apps"></a>可用的策略托管应用  
 有关可用于 iOS 和 Android 设备的策略托管应用列表，请参阅 [Microsoft Intune 应用程序合作伙伴](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners)。  



<!--HONumber=Nov16_HO1-->


