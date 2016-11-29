---
title: "管理批量购买的 iOS 应用 | System Center Configuration Manager"
description: "部署、管理和跟踪通过 iOS App Store 购买的应用的许可证。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4289f4853f77392df420e44e179961609f83683f


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*



 iOS App Store 使得能够为你想在公司中运行的应用购买多个许可证。 这有助于降低跟踪多个已购买应用副本的管理成本。  

 System Center Configuration Manager 可通过从应用商店中导入许可证信息以及跟踪已使用的许可证的数量来帮助部署和管理通过该计划购买的 iOS 应用。  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>管理批量采购的适用于 iOS 设备的应用程序  
 你通过 Apple 批量采购计划 (VPP) 购买多个 iOS 应用许可证。 这涉及从 Apple 网站设置一个 Apple VPP 帐户，并将 Apple VPP 令牌上传到提供以下功能的 Configuration Manager：  

-   将批量购买信息与 Configuration Manager 同步。  

-   购买的应用显示在 Configuration Manager 控制台中。  

-   可以部署和监控这些应用，还可以跟踪已使用的每个应用的许可证数量。  

-   Configuration Manager 可以通过卸载已部署到用户的批量购买的应用，帮助在必要时回收许可证。  

## <a name="before-you-start"></a>开始之前  
 开始之前，需要从 Apple 获取 VPP 令牌，并将其上传到 Configuration Manager。  

> [!IMPORTANT]  
>  -   目前，每个组织只能有一个 VPP 帐户和令牌。  
> -   仅支持 Apple Volume Purchase Program 企业版。  
> -   一旦你将 Apple VPP 帐户和 Intune 相关联，随后将不能关联不同的帐户。 出于此原因，有超过一个人拥有你所使用的帐户的详细信息是非常重要的。  
> -   如果以前在现有的 Apple VPP 帐户中使用过不同 MDM 产品的 VPP 令牌，必须使用 Configuration Manager 生成一个新的令牌以供使用。  
> -   每个令牌的有效期为一年。  
> -   默认情况下，Configuration Manager 与 Apple VPP 服务一天同步两次以确保许可证与 Configuration Manager 保持同步。  
>   
>      仅同步对许可证的更改。 但是，将每隔 7 天执行一次完全同步。  
>   
>      单击“同步”以执行手动同步时，该操作将始终执行完全同步。  
> -   如果需要恢复或还原 Configuration Manager 数据库，建议之后执行手动同步，以确保同步的许可证数据保持最新。  
> -   虽然可以将 iOS 批量购买的应用部署到用户或设备集合，但不会安装部署到无用户的设备的 VPP 应用（例如，使用设备注册计划 (DEP) 或 Apple Configurator 在没有用户关联的情况下注册的设备）。  

 此外，必须从 Apple 导入有效的 Apple 推送通知服务 (APN) 证书，以允许管理 iOS 设备（包括应用部署）。 有关详细信息，请参阅[设置 iOS 混合设备管理](../../mdm/deploy-use/set-up-ios-hybrid-device-management.md)。  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>步骤 1 - 获取并上载 Apple VPP 令牌  
  
1.  在 Configuration Manager 控制台中，单击“管理” > “云服务” > “Apple Volume Purchase Program 令牌”。   
  
3.  在“主页”的“Apple Volume Purchase Program 令牌”组中，单击“添加 Apple Volume Purchase Program 令牌”。  

4.  在“添加 Apple Volume Purchase Program 令牌”向导的“常规”页上，配置以下项：   

    -   **名称** - 输入此令牌的名称，因为它将显示在 Configuration Manager 控制台中。  

    -   **令牌** - 单击“浏览”，然后选择从 Apple 网站下载的 VPP 令牌。  

         单击“查看 Apple VPP 帐户”链接，如果尚未注册，请注册企业或教育批量购买计划。 一旦注册完成，下载你的帐户的 Apple VPP 令牌。  

    -   **说明** - 可选择输入说明，帮助在 Configuration Manager 控制台中识别此 VPP 令牌。  

    -   **改进搜索和筛选的分配类别** -（可选）可以将类别分配到 VPP 令牌以使其在 Configuration Manager 控制台中更易搜索。  

5.  单击“下一步”，然后完成向导。  
  
从“Apple Volume Purchase Program 令牌”节点中，现在可以查看有关 Apple VPP 令牌的信息，包括其上次更新的时间、到期时间以及上次同步的时间。 
  
在“主页”选项卡的“同步”组中单击“同步”，可以随时将 Apple 保存的数据与 Configuration Manager 完全同步。  
  
## <a name="step-2---deploy-a-volume-purchased-app"></a>步骤 2 - 部署批量采购的应用  

1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用商店应用的许可证信息”。  

3.  选择要部署的应用，然后在“主页”选项卡的“创建”组中，单击“创建应用程序”。
将创建包含适用于企业的 Windows 应用商店应用的 Configuration Manager 应用程序。 然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。

    > [!IMPORTANT]  
    > 必须选择部署目的为“必需”。 当前不支持可用的安装。

 在部署应用时，安装该应用的每个用户使用一个许可证。  

 若要回收许可证，必须将部署操作为“卸载” 。 应用卸载后，将回收许可证。  

## <a name="step-3---monitor-ios-vpp-apps"></a>步骤 3 - 监视 iOS VPP 应用  
 “软件库”工作区的“应用商店应用的许可证信息”节点显示有关批量购买的 iOS 应用的信息，包括拥有的每个应用的许可证总数，以及已部署的数量。

 还可以监视所有通过使用“具有许可证计数的适用于 iOS 的 Apple Volume Purchase Program 应用”报表购买的所有 VPP 应用的许可证使用情况。  

 此报表显示每个应用程序名称，以及你购买的许可证总数、可用许可证数量以及更多内容。  

 有关运行 Configuration Manager 报表的帮助信息，请参阅 [System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)。  



<!--HONumber=Nov16_HO1-->


