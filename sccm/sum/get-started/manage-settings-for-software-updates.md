---
title: "管理软件更新的设置 | Microsoft Docs"
description: "了解安装软件更新点后适用于你的站点的软件更新的客户端设置。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/26/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
ms.openlocfilehash: fe4a8f56e0b554e206bcc4503a0268dc761ded81
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_ManageSUSettings"></a>管理软件更新的设置  

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中同步软件更新后，配置并验证以下部分中的设置。

##  <a name="BKMK_ClientSettings"></a> 软件更新的客户端设置  
安装软件更新点之后，默认情况下会在客户端上启用软件更新，而且客户端设置中的  “软件更新”页上的设置具有默认值。 客户端设置将用于整个站点，且会影响扫描软件更新以检查其符合性的时间以及在客户端计算机上安装软件更新的方式和时间。 部署软件更新前，请验证客户端设置是否适用于站点中的软件更新。  

> [!IMPORTANT]  
>  默认情况下会启用“在客户端上启用软件更新”  设置。 如果清除此设置，Configuration Manager 会从客户端中删除现有的部署策略。  

有关如何配置客户端设置的信息，请参阅[如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

有关客户端设置的详细信息，请参阅[关于客户端设置](../../core/clients/deploy/about-client-settings.md)。  

##  <a name="BKMK_GroupPolicy"></a> 软件更新的组策略设置  
客户端计算机上的 Windows 更新代理 (WUA) 使用特定的组策略设置来连接到在软件更新点上运行的 WSUS。 这些组策略设置还用于成功扫描软件更新的符合性，以及自动更新软件更新和 WUA。

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>“指定 Intranet Microsoft 更新服务位置”本地策略  
在为站点创建软件更新点时，客户端会获得计算机策略，此策略提供软件更新点服务器的名称，并且在计算机上配置“指定 Intranet Microsoft 更新服务位置”  本地策略。 WUA 检索在“设置检测更新的 Intranet 更新服务”  设置中指定的服务器名称，之后，它在扫描软件更新符合性时会连接到此服务器。 在为“指定 Intranet Microsoft 更新服务位置”  设置创建域策略时，它将替代本地策略，而且 WUA 可能会连接到软件更新点以外的服务器。 如果出现此情况，客户端可能会根据不同的产品、分类和语言扫描软件更新符合性。 因此，不应为客户端计算机配置 Active Directory 策略。  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>“允许来自 Intranet Microsoft 更新服务位置的签名内容”组策略  
在计算机上的 WUA 扫描已创建并利用 System Center Updates Publisher 发布的软件更新之前，你必须启用“允许来自 Intranet Microsoft 更新服务位置的签名内容”  组策略设置。 在启用此策略设置时，如果在本地计算机上的“受信任的发布者”  证书存储中签署软件更新，则 WUA 将接受通过 Intranet 位置收到的这些软件更新。 有关 Updates Publisher 所需的组策略设置的详细信息，请参阅 [Updates Publisher 2011 文档库](http://go.microsoft.com/fwlink/p/?LinkId=232476)。  

### <a name="automatic-updates-configuration"></a>自动更新的配置  
自动更新允许在客户端计算机上接收安全更新和其他重要的下载内容。 若要配置自动更新，可通过“配置自动更新”  组策略设置或本地计算机上的“控制面板”进行。 在启用自动更新时，客户端计算机将收到更新通知，而且，视已配置的设置而定，客户端计算机将下载并安装所需的更新。 在自动更新与软件更新共存时，每台客户端计算机都可能会为同一个更新显示通知图标和弹出通知窗口。 而且，在需要重新启动时，每台客户端计算机都可能会为同一个更新显示重新启动对话框。  

### <a name="self-update"></a>自我更新  
在客户端计算机上启用自动更新时，如果有可用的更新版本，或者如果 WUA 组件出现问题，则 WUA 会自动执行自我更新。 在未配置或禁用自动更新，而且客户端计算机具有较早版本的 WUA 时，客户端计算机必须运行 WUA 安装文件。  

## <a name="software-updates-properties"></a>软件更新属性
软件更新属性提供了有关软件更新和相关内容的信息。 你也可以使用这些属性为软件更新配置设置。 打开多个软件更新的属性时，仅显示“最大运行时间”  和“自定义严重性”  选项卡。   

使用下面的过程打开软件更新属性。  

#### <a name="to-open-software-update-properties"></a>打开软件更新属性  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  
2.  在“软件库”工作区中，展开“软件更新” ，并单击“所有软件更新” 。  
3.  选择一个或多个软件更新，然后在“主页”  选项卡上的“属性”  组中，单击“属性”  。  

   > [!NOTE]  
   >  在“所有软件更新”节点上，Configuration Manager 只显示分类为“严重”和“安全”且在过去 30 天内发布的软件更新。  

###  <a name="BKMK_SoftwareUpdatesInformation"></a> 查看软件更新信息  
在软件更新属性中，你可以查看关于软件更新的详细信息。 当你选择多个软件更新时，不会显示详细信息。 以下部分描述可用于所选软件更新的信息。  

####  <a name="BKMK_SoftwareUpdateDetails"></a> 软件更新详细信息  
在“更新详细信息”  选项卡中，你可以查看关于所选软件更新的以下摘要信息：  

- “公告 ID”：指定与安全软件更新相关联的公告 ID。 通过在 [Microsoft Security Bulletin Search（Microsoft 安全公告搜索）](http://go.microsoft.com/fwlink/p/?LinkId=58313) 网页上根据公告 ID 进行搜索，你可以查找安全公告详细信息。  

- “文章 ID”：指定软件更新的文章 ID。 引用的文章提供了关于软件更新以及软件更新所修复或改进的问题的更多详细信息。  

- “修订日期”：指定软件更新的上次修改日期。  

- “最大严重性分级”：指定软件更新的供应商定义的严重性分级。  

- “说明”：概述软件更新所修复或改进的情况。  

- “适用的语言”：列出软件更新适用的语言。  

- “受影响产品”：列出软件更新适用的产品。  

####  <a name="BKMK_ContentInformation"></a> 内容信息  
在“内容信息”  选项卡中，查看与选定软件更新关联内容有关的下列信息：  

-   “内容 ID”：指定软件更新的内容 ID。  

-   **已下载**：指示 Configuration Manager 是否已下载软件更新文件。  

-   “语言”：指定软件更新的语言。  

-   “源路径”：指定软件更新源文件的路径。  

-   **大小(MB)**：指定软件更新源文件的大小。  

####  <a name="BKMK_CustomBundleInformation"></a> 自定义捆绑信息  
在“自定义捆绑信息”  选项卡中，查看软件更新的自定义捆绑信息。 当选定软件更新包含在软件更新文件中所包含的捆绑软件更新时，它们会显示在“捆绑信息”  部分。 此选项卡不会显示在“内容信息”  选项卡中显示的捆绑软件更新，如不同语言的更新文件。  

####  <a name="BKMK_SupersedenceInformation"></a> 取代信息  
在“取代信息”  选项卡中，你可以查看关于软件更新取代的下列信息：  

- “此更新已由下列更新取代”：指定取代此更新的软件更新，这意味着所列的更新较新。 在大多数情况下，你将部署取代该软件更新的其中一项软件更新。 在列表中显示的软件更新包含提供详细软件更新信息的网页超链接。 当此更新未取代时，将显示“无”  。  

- “此更新会取代下列更新”：指定由此软件更新所取代的软件更新，这意味着此软件更新较新。 在大多数情况下，你将会部署此软件更新以替换取代的软件更新。 在列表中显示的软件更新包含提供详细软件更新信息的网页超链接。 当此更新未取代任何其他更新时，将显示“无”  。  

###  <a name="BKMK_SoftwareUpdatesSettings"></a> 配置软件更新设置  
在属性中，你可以为一个或多个软件更新配置软件更新设置。 你仅可以在管理中心站点或独立主站点中配置大多数软件更新设置。 下列部分将帮助你配置软件更新的设置。  

####  <a name="BKMK_SetMaxRunTime"></a> 设置最长运行时间  
在“最长运行时间”  选项卡中，设置对在客户端计算机上完成某软件更新所分配的最长时间。 如果更新所用时间比最长运行时值更长，Configuration Manager 将创建状态消息并停止监视软件更新安装的部署。 你仅可以在管理中心站点或独立主站点中配置此设置。  

Configuration Manager 还使用此设置来确定是否在配置的维护时段中启动软件更新安装。 如果最长运行时间的值大于维护时段中的可用剩余时间，则软件更新安装会延迟，直到下个维护时段开始。 当要在具有配置的维护时段（时间段）的客户端计算机上安装多个软件更新时，首先将安装最长运行时间最短的软件更新，然后安装下一个最长运行时间最短的软件更新，并照此类推。 在其安装每个软件更新之前，客户端将验证可用的维护时段是否提供足够时间来安装软件更新。 在软件更新开始安装后，即使安装超过维护时段的结束时间，也将仍然继续安装。 有关维护时段的详细信息，请参阅[如何在 System Center Configuration Manager 中使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。  

在“最长运行时间”  选项卡上，你可以查看和配置下列设置：  

- **最长运行时间**：指定为完成软件更新安装分配的最大分钟数，在此时段后，Configuration Manager 将不再监视安装。 此设置还用于确定在维护时段结束前是否有足够的可用剩余时间来安装更新。 对于 Service Pack，默认设置为 60 分钟。 对于其他类型的软件更新，如果你执行了 Configuration Manager 版本 1511 或更高版本的全新安装，则默认时间为 10 分钟，如果从之前的版本升级，则默认时间为 5 分钟。 值可以介于 5 至 9999 分钟之间。  

> [!IMPORTANT]  
>  确保设置小于配置的维护时段时间的最长运行时间值。 否则，将永远无法启动软件更新安装。  

####  <a name="BKMK_SetCustomSeverity"></a> 设置自定义严重性  
在软件更新属性中，你可以使用“自定义严重性”  选项卡来配置软件更新的自定义严重性值。 如果预定义的严重性值不能满足你的需要，则这项操作可能必不可少。 Configuration Manager 控制台的“自定义严重性”列中列出了自定义值。 你可按定义的自定义严重性值对软件更新排序，并且还可以创建可对这些值进行筛选的查询和报表。 你仅可以在管理中心站点或独立主站点中配置此设置。  

你可以在“自定义严重性”  选项卡上配置下列设置。  

- “自定义严重性”：为软件更新设置自定义的严重性值。 从列表中选择“严重” 、“重要” 、“中” 或“低”  。 默认情况下，自定义严重性值为空。

## <a name="crl-checking-for-software-updates"></a>软件更新的 CRL 检查
默认情况下，在验证 System Center Configuration Manager 软件更新上的签名时不会检查证书吊销列表 (CRL)。 如果在每次使用证书时都检查 CRL，则能更好地抵御因使用已吊销的证书而造成的安全威胁，但这样做会使连接出现延迟，并在执行 CRL 检查的计算机上引发额外的处理操作。  

如果使用，则必须在处理软件更新的 Configuration Manager 控制台上启用 CRL 检查。  

#### <a name="to-enable-crl-checking"></a>启用 CRL 检查  
在执行 CRL 检查的计算机上，从产品 DVD 上的命令提示符运行以下命令：**\SMSSETUP\BIN\X64\\**<*language*>**\UpdDwnldCfg.exe /checkrevocation**。  

例如，对于英语（美国），运行 **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**  
