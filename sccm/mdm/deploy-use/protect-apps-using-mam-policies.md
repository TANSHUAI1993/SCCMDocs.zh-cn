---
title: 使用移动应用程序管理策略保护应用
titleSuffix: Configuration Manager
description: 修改部署的应用的功能，使它们符合公司的合规性和安全策略。
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 28115475-e563-4e16-bf30-f4c9fe704754
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 231988b9c6b41a904e2ae8225bdb070f0b047618
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678909"
---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>使用 System Center Configuration Manager 中的移动应用程序管理策略保护应用

适用范围：  System Center Configuration Manager (Current Branch)

通过 System Center Configuration Manager 应用程序管理策略，可修改部署的应用的功能，帮助应用符合公司的合规性策略和安全策略。 例如，可限制在受限应用内进行剪切、复制和粘贴操作，或配置应用以打开托管浏览器内的所有 URL。 应用管理策略支持：  

-   运行 Android 4 和更高版本的设备  

-   运行 iOS 9 及更高版本的设备  

还可使用移动应用管理策略保护不由 Intune 管理的设备上的应用。 可使用这项新功能，将移动应用管理策略应用到连接到 Office 365 服务的应用。 此操作不支持用于连接到本地 Exchange 或 SharePoint 的应用。  

若要使用这项新功能，需使用 Azure 预览门户。 下列主题可帮你入门：  
- [在 Azure 门户中开始使用移动应用管理策略](https://technet.microsoft.com/library/mt627830.aspx)  
- [使用 Microsoft Intune 创建和部署移动应用管理策略](https://technet.microsoft.com/library/mt627829.aspx)  

  与 Configuration Manager 中的配置项目和基线不同，不会直接部署应用程序管理策略。 而是将该策略与你想要进行限制的应用程序部署类型关联。 在设备上部署并安装了应用部署类型后，指定的设置将生效。  

若要将限制应用到应用，该应用必须结合 Microsoft Intune 应用软件开发工具包 (SDK)。 有两种方式获得此类应用：  

-   **使用策略托管的应用**（Android 和 iOS）：这些应用具有内置了 App SDK。 要添加此类型的应用，你可以从 iTunes 应用商店或 Google Play 等应用商店指定应用的链接。 对于此类应用，无需进一步的处理。 有关可用于 iOS 和 Android 设备的策略托管应用的列表，请参阅 [Managed apps for Microsoft Intune mobile application management policies](https://technet.microsoft.com/library/dn708489.aspx)（Microsoft Intune 移动应用程序管理策略的托管应用）。  

-   **使用"包装"应用**（Android 和 iOS）：这些应用进行重新封装，以使用将应用 SDK **Microsoft Intune 应用包装工具**。 该工具通常用于处理公司内部开发的应用。 它可用于处理从应用商店下载的应用。 有关详细信息，请参阅下列文章：
    - [使用 Microsoft Intune 应用包装工具为移动应用程序管理准备 iOS 应用](https://technet.microsoft.com/library/dn878028.aspx)

    - [使用 Microsoft Intune 应用包装工具为移动应用程序管理准备 Android 应用](https://technet.microsoft.com/library/mt147413.aspx)  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>创建和部署具有移动应用程序管理策略的应用  

##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>步骤 1：获取指向策略托管应用的链接或创建已包装的应用  

-   **获取指向策略托管应用**:从应用商店查找并记录你想要部署的策略托管应用的 URL。  

     例如，Microsoft Word for iPad 应用的 URL 是 https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8   

-   **若要创建已包装的应用**:使用主题中的信息[使用 Microsoft Intune 应用包装工具为移动应用管理准备 iOS 应用](https://technet.microsoft.com/library/dn878028.aspx)和[为使用 Microsoft Intune 的移动应用程序管理准备 Android 应用应用包装工具](https://technet.microsoft.com/library/mt147413.aspx)创建已包装的应用。  

     创建处理过的应用和关联的清单文件的工具。 创建包含该应用的 Configuration Manager 应用程序时，使用这些文件。  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>步骤 2:创建包含应用的 Configuration Manager 应用程序  
 创建 Configuration Manager 应用程序的过程有所不同，具体取决于使用的是策略托管应用（外部链接）还是通过适用于 iOS 的 Microsoft Intune 应用包装工具（iOS 应用包）创建的应用。 使用以下过程之一创建 Configuration Manager 应用程序。  

1. 在 Configuration Manager 控制台中，选择“软件库”   > “应用程序管理”   > “应用程序”  。  

2. 在“主页”  选项卡上的“创建”  组中，选择“创建应用程序”  ，打开“创建应用程序”  向导。  

3. 在“常规”  页上，选择“自动检测安装文件中有关此应用程序的信息”  。  

4. 在“类型”下拉列表中，选择“iOS 应用包(\*.ipa 文件)”。    

5. 选择“浏览”  ，选择要导入的应用包，然后选择“下一步”  。  

6. 在“常规信息”  页上，输入希望用户在公司门户中看到的描述性文本和类别信息。  

7. 完成向导。  

   新应用程序会显示在“软件库”  工作区的“应用程序”  节点中。  

### <a name="create-an-application-that-contains-a-link-to-a-policy-managed-app"></a>创建包含策略托管应用链接的应用程序  

1. 在 Configuration Manager 控制台中，选择“软件库”   > “应用程序管理”   > “应用程序”  。  

2. 在“主页”  选项卡上的“创建”  组中，选择“创建应用程序”  ，打开“创建应用程序”  向导。  

3. 在“常规”  页上，选择“自动检测安装文件中有关此应用程序的信息”  。  

4. 在“类型”  下拉列表中，选择以下一项：  

   -   对于 iOS:**App Store 中的 iOS 应用包**  

   -   对于 Android:**Google Play 上的 Android 应用包**  

5. 输入应用的 URL（来自步骤 1），然后选择“下一步”  。  

6. 在“常规信息”  页上，输入希望用户在公司门户中看到的描述性文本和类别信息。  

7. 完成向导。  

   新应用程序会显示在“软件库”  工作区的“应用程序”  节点中。  

##  <a name="step-3-create-an-application-management-policy"></a>步骤 3：创建应用程序管理策略  
 接下来，创建一个与该应用程序关联的应用程序管理策略。 可以创建一个常规或托管浏览器策略。  

1)  在 Configuration Manager 控制台中，选择“软件库”   > “应用程序管理”   > “应用程序管理策略”  。  

2)  在“主页”  选项卡的“创建”  组中，选择“创建应用程序管理策略”  。  

3)  在“常规”  页上，输入策略的名称和说明，然后选择“下一步”  。  

4)  在“策略类型”  页上，选择此策略的平台和策略类型，然后选择“下一步”  。 可以使用下列策略类型：  

-   **常规**:常规策略类型可让你修改你部署以帮助其符合公司的合规性和安全策略的应用程序的功能。 例如，可以限制受限应用中的剪切、复制和粘贴操作。  

-   **托管浏览器**:托管浏览器策略，可以决定是允许还是阻止托管浏览器打开 Url 列表。 “托管浏览器”策略类型可让你修改 Intune 托管浏览器应用的功能。 这是一个 Web 浏览器，可让你管理用户可以执行的操作（包括他们可以访问的站点）以及打开指向浏览器中内容的链接的方式。 详细了解  [适用于 iOS 的 Intune 托管浏览器应用](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) 和 [适用于 Android 的 Intune 托管浏览器应用](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en)。

5)  在“iOS 策略”  或“Android 策略”  页上，按需配置以下值，然后选择“下一步”  。 该选项可能有所差异，这取决于你配置策略的设备类型。  

|值|更多信息|  
|-----------|----------------------|  
|**限制显示在企业托管浏览器内的 Web 内容**|确保在托管浏览器中打开应用中的所有链接。 你必须部署此应用，此选项才能工作。|  
|**“阻止 Android 备份”** 或 **“阻止 iTunes 和 iCloud 备份”**|禁止从应用备份任何信息。|  
|**允许应用向其他应用传送数据**|指定该应用可以发送数据的应用。 可选择不允许将数据传输到任何应用、仅允许传输到其他受限应用或允许传输到任何应用。<br /><br /> 对于 iOS 设备，若要防止在托管和非托管应用之间传输文档，你也必须配置并部署禁用 **“允许在其他非托管应用中使用托管文档”** 设置的移动设备安全策略。<br /><br /> 如果选择仅允许传输到其他受限应用，则 Intune PDF 和图片查看器（如果已部署）将打开各自类型的内容。|  
|**允许应用从其他应用接收数据**|指定应用可以接收数据的应用。 可选择不允许从任何应用传输数据、仅允许从其他受限应用传输数据或允许从任何应用传输数据。|  
|**防止“另存为”**|在任何使用此策略的应用中禁用“另存为”  选项。|  
|**限制剪切、复制和粘贴到其他应用程序**|指定应用使用剪切、复制和粘贴操作的方法。 选择：<br /><br /> **阻止** – 不允许在本应用和其他应用间进行剪切、复制和粘贴操作。<br /><br /> **策略托管应用** – 仅允许在本应用和其他受限应用间进行剪切、复制和粘贴操作。<br /><br /> **可粘贴的策略托管应用** – 允许将从本应用剪切或复制的数据粘贴到其他受限应用。 允许将剪切或复制自任何应用的数据粘贴至本应用。<br /><br /> **任何应用** – 不限制本应用的剪切、复制和粘贴操作。|  
|**访问需要简单 PIN**|要求用户输入他们指定使用此应用的 PIN。 要求用户在首次运行该应用时进行设置。|  
|**重置 PIN 前的尝试次数**|指定输入 PIN 码的尝试次数，达到该次数后用户必须重置 PIN。|  
|**访问需要公司凭据**|要求用户必须输入其公司登录信息，才能访问该应用。|  
|**访问要求设备符合公司策略**|仅允许设备在未越狱或获取根权限时使用此应用。|  
|**在一定时间后重新检查访问要求（分钟）**|指定应用启动后重新检查访问要求前的时间段（在“超时”  字段中）。<br /><br /> 在“离线宽限期”  字段，如果设备离线，指定应用重新检查访问要求前的时间段。|  
|**加密应用数据**|指定加密与本应用相关的所有数据，包括外部存储的数据，例如存储在 SD 卡上的数据。<br /><br /> **适用于 iOS 的加密**<br /><br /> 对于与 Configuration Manager 移动应用程序管理策略关联的应用，使用操作系统提供的设备级加密对静止数据进行加密。 通过必须由 IT 管理员设置的设备 PIN 策略启用此操作。需要 PIN 时，根据移动应用程序管理策略的设置对数据进行加密。 正如 Apple 文档所述，[iOS 7 所使用的模块经过了 FIPS 140-2 的认证](http://support.apple.com/en-us/HT202739)。<br /><br /> **适用于 Android 的加官**<br /><br /> 对于与 Configuration Manager 移动应用程序管理策略关联的应用，加密由 Microsoft 提供。 根据移动应用程序管理策略的设置，数据在文件 I/O 运行过程中同步加密。 Android 上托管的应用利用平台加密库使用 CBC 模式的 AES-128 加密。 加密方法没有获得 FIPS 140-2 认证。 设备存储中的内容始终处于加密状态。|  
|**“阻止屏幕捕捉”** （仅限于 Android 设备）|指定在使用该应用时，阻止设备的屏幕捕捉功能。|  
|**禁用联系人同步**| 从版本 1710 开始，此选项阻止应用将数据保存到设备上的本机“联系人”应用。 如果选择“否”，应用可将数据保存到设备上的本机“联系人”应用。|  
|**禁用打印**| 从版本 1710 开始，此选项阻止应用打印工作或学校数据。 |  

6)  在“托管浏览器”  页上，选择允许托管浏览器只打开列表中的 URL 或是阻止托管浏览器打开列表中的 URL，然后选择“下一步”  。  
有关详细信息，请参阅[使用托管浏览器策略管理 Internet 访问](manage-internet-access-using-managed-browser-policies.md)。  

7)  完成向导。  

 新策略显示在“软件库”  工作区的“应用程序管理策略”  节点中。  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>步骤 4：将应用程序管理策略与部署类型相关联  

 为需要应用程序管理策略的应用创建部署类型后，Configuration Manager 会对其进行识别，并提示用户关联应用管理策略。 对于托管浏览器，将需要关联“常规”和“托管浏览器”策略。 有关详细信息，请参阅[创建应用程序](create-applications.md)。  

> [!IMPORTANT]  
>  如果已部署应用程序，此关联完成前，将无法成功部署新部署类型。 可以在“应用程序管理”  选项卡上应用程序的“属性”  中建立关联。  

> [!IMPORTANT]  
>  对于运行 iOS 7.1 之前的操作系统的设备，关联的策略只有在卸载应用后才能删除。  
>   
>  如果从 Configuration Manager 取消注册设备，则策略不会从应用中删除。 应用了策略的应用会保留策略设置，甚至在卸载并重新安装了该应用后也是如此。  

##  <a name="step-5-monitor-the-app-deployment"></a>步骤 5:监视应用部署  
 创建并部署关联移动应用程序管理策略的应用后，可监视应用并解决任何策略冲突问题。  

1. 在 Configuration Manager 控制台中，选择“软件库”   > “概述”   > “部署”  。  

2. 选择创建的部署。 然后，在“主页”  选项卡上，选择“属性”  。  

3. 在部署的详细信息窗格中的“相关对象”  下，选择“应用程序的管理策略”  。  

   有关监视应用程序的详细信息，请参阅[监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

##  <a name="learn-how-policy-conflicts-are-resolved"></a>了解如何解决策略冲突  
 如果在第一次部署到用户或设备时出现移动应用管理策略冲突，则会从部署到应用的策略中删除处于冲突的特定设置值。 然后应用将使用内置冲突值。  

 如果在后续部署到应用或用户时出现移动应用管理策略冲突，则不会在部署到应用的移动应用管理策略上更新处于冲突的特定设备值，且应用会使用该设置的现有值。  

 如果设备或用户收到两个冲突策略，则适用以下行为：  

-   如果尚未将策略部署到设备，则现有策略设置不会被覆盖。  

-   如果尚无策略部署到设备，且已部署了两个冲突设置，则将使用设备内的默认设置。  

##  <a name="see-a-list-of-available-policy-managed-apps"></a>查看可用的策略托管应用列表  
 有关可用于 iOS 和 Android 设备的策略托管应用列表，请参阅 [Microsoft Intune 应用程序合作伙伴](https://www.microsoft.com/cloud-platform/microsoft-intune-partners)。  
