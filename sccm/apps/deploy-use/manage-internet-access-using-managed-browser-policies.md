---
title: "使用托管浏览器策略管理 Internet 访问 | System Center Configuration Manager"
description: "部署 Intune Managed Browser 来管理和限制 Internet 访问。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 735c45b8-a545-4805-84e5-46204fabd1a6
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e5efee7b94f5c61a610fd9f9fa278c992f9c64b8


---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 的托管浏览器策略管理 Internet 访问

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中，可以部署 Intune Managed Browser（这是一款 Web 浏览应用程序），还可将应用程序与托管浏览器策略关联。 托管浏览器策略可配置允许列表或阻止列表，用于限制托管浏览器用户可以访问的网站。  
  
 由于此应用是托管应用，因此你还可以向其应用移动应用程序管理策略，如控制使用剪切、复制和粘贴，阻止屏幕捕获，以及确保用户单击的内容链接仅在其他托管应用中打开。 有关详细信息，请参阅[使用移动应用程序管理策略保护应用](../../apps/deploy-use/protect-apps-using-mam-policies.md)。  
  
> [!IMPORTANT]  
>  如果用户自行安装托管浏览器，则该浏览器将不受任何所指定策略的管理。 若要确保浏览器由 Configuration Manager 管理，则用户必须先卸载该应用，然后才可以将其作为托管应用部署给这些用户。  

 可以针对以下设备类型创建托管浏览器策略：  

-   运行 Android 4 和更高版本的设备  

-   运行 iOS 7 和更高版本的设备  

> [!NOTE]  
>  若要了解详细信息和下载 Intune Managed Browser 应用，请参阅 [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)（对于 iOS）和 [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en)（对于 Android）。  
  
## <a name="create-a-managed-browser-policy"></a>创建托管浏览器策略  

1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序管理策略”。  

3.  在“主页”  选项卡的“创建”  组中，单击“创建应用程序管理策略” 。  

4.  在“常规”  页上，输入策略的名称和说明，然后单击“下一步” 。  

5.  在“策略类型”  页上，依次选择平台和策略类型的“托管浏览器”  ，然后单击“下一步” 。  

     在“托管浏览器”  页上，选择下列选项之一：  

    -   **仅允许托管浏览器打开下面列出的 URL** – 指定托管浏览器可以打开的 URL 列表。  

    -   **阻止托管浏览器打开下面列出的 URL** – 指定将阻止托管浏览器打开的 URL 列表。  

    > [!NOTE]  
    >  不能在相同的托管浏览器策略中同时包括允许的 URL 和阻止的 URL。  

     有关可以指定的 URL 格式的详细信息，请参阅本主题中的 **允许的 URL 和阻止的 URL 的格式** 。  

    > [!NOTE]  
    >  “常规”  策略类型可让你修改你部署的应用的功能，以帮助其符合公司的合规性和安全策略。 例如，可以限制受限应用中的剪切、复制和粘贴操作。 有关常规策略类型的详细信息，请参阅[使用移动应用程序管理策略保护应用](../../apps/deploy-use/protect-apps-using-mam-policies.md)。  

6.  完成向导。  

 新策略显示在“软件库”  工作区的“应用程序管理策略”  节点中。  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>创建托管浏览器应用的软件部署  
 在创建托管浏览器策略后，可以创建托管浏览器应用的软件部署类型。 必须关联托管浏览器应用的常规和托管浏览器策略。  
  
 有关详细信息，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md)。  
  
## <a name="security-and-privacy-for-the-managed-browser"></a>托管浏览器的安全和隐私  

-   在 iOS 设备上，如果用户访问的网站的证书已过期或不受信任，则无法打开该网站。  

-   托管浏览器不使用用户在设备上对内置浏览器进行的设置。 这是因为托管浏览器无权访问这些设置。  

-   如果在与托管浏览器关联的移动应用程序管理策略中配置 **“访问需要简单 PIN”** 或 **“访问需要公司凭据”** 选项，并且用户单击身份验证页上的帮助链接，则他们可以浏览任何 Internet 站点，而无论这些网站是否已添加到托管浏览器策略中的阻止列表。  

-   托管浏览器仅能在直接访问站点时阻止访问。 使用中间服务（例如翻译服务）访问站点时，该策略则无法阻止访问。  

## <a name="reference-information"></a>参考信息  
  
###  <a name="url-format-for-allowed-and-blocked-urls"></a>允许的 URL 和阻止的 URL 的格式  

使用以下信息来了解有关指定允许和阻止列表中的 URL 时允许使用的格式和通配符。  

-   可以根据下面的允许模式列表中的规则使用通配符“**\***”。  

-   在将 URL 输入列表时，确保对所有 URL 添加 **“http”** 或 **“https”** 作为前缀。  

-   可以在地址中指定端口号。 如果未指定端口号，将使用以下值：  

    -   对于 http，使用端口 80  

    -   对于 https，使用端口 443  

     不支持对端口号使用通配符，例如，**http://www.contoso.com:\*** 和 **http://www.contoso.com: /\***  

-   使用下表了解指定 URL 时可以使用的允许模式：  

    |URL|匹配|不匹配|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> 匹配单个页面|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> 匹配单个页面|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> 匹配以 www.contoso.com 开头的所有 URL|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> 匹配 contoso.com 下的所有子域|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> 匹配单个文件夹|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> 匹配单个页面（使用端口号）|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> 匹配单个安全页面|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> 匹配单个文件夹和所有子文件夹|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   以下是一些你不能指定的输入的示例：  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   IP 地址  

    -   https://*  

    -   http://*  

    -   “http://www.contoso.com:*”  

    -   “http://www.contoso.com: / *”  

> [!NOTE]  
>  始终允许 *.microsoft.com。  
  
### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>允许和阻止列表之间的冲突的解决方式  
 如果向一个设备部署多个托管浏览器策略，并且出现设置冲突，则将评估模式（允许或阻止）以及 URL 列表中的冲突。 发生冲突时，以下行为适用：  

-   如果每个策略中的模式相同但 URL 列表不同，则不会在设备上强制执行 URL。  

-   如果每个策略中的模式不同但 URL 列表相同，则不会在设备上强制执行 URL。  

-   如果设备是首次接收托管浏览器策略而两个策略发生冲突，则不会在设备上强制执行 URL。 使用 **“策略”** 工作区的 **“策略冲突”** 节点查看这些冲突。  

-   如果设备已接收托管浏览器策略而部署的第二个策略具有冲突的设置，则将在设备上保留原始设置。 使用 **“策略”** 工作区的 **“策略冲突”** 节点查看这些冲突。  



<!--HONumber=Nov16_HO1-->


