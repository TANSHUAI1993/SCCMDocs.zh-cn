---
title: "管理批量采购的 iOS 应用 | Microsoft Docs"
description: "部署、管理和跟踪通过 iOS App Store 购买的应用的许可证。"
ms.custom: na
ms.date: 05/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: ce706e938f558406044f7890c80bb7156c3b262b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理批量购买的 iOS 应用

*适用范围：System Center Configuration Manager (Current Branch)*



 可在 iOS App Store 中为要在公司中运行的应用购买多个许可证。 这有助于降低跟踪多个已购买应用副本的管理成本。  

 System Center Configuration Manager 可通过从 App Store 中导入许可证信息以及跟踪已使用的许可证数量来帮助部署和管理通过该计划购买的 iOS 应用。  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>管理批量采购的适用于 iOS 设备的应用程序  
 通过 Apple Volume Purchase Program (VPP) 购买多个 iOS 应用许可证。 这涉及从 Apple 网站设置一个 Apple VPP 帐户，并将 Apple VPP 令牌上传到提供以下功能的 Configuration Manager：  

-   将批量购买信息与 Configuration Manager 同步。 
 
- 同步 Apple Volume Purchase Program 企业版和 Apple Volume Purchase Program 教育版的应用。

- 将多个 Apple 批量采购计划令牌与 Configuration Manager 相关联。

-   购买的应用显示在 Configuration Manager 控制台中。  

-   可以部署和监控这些应用，还可以跟踪每个应用已使用的许可证数量。  

-   Configuration Manager 可以通过卸载已部署的批量购买的应用，帮助在必要时回收许可证。  

## <a name="before-you-start"></a>开始之前  
 开始之前，需要从 Apple 获取 VPP 令牌，并将其上传到 Configuration Manager。  

-   如果之前在现有的 Apple VPP 帐户中将 VPP 令牌用于其他 MDM 产品的 ，则必须创建一个新的令牌供 Configuration Manager 使用。  
-   每个令牌的有效期为一年。  
-   默认情况下，Configuration Manager 每天与 Apple VPP 服务同步两次，确保许可证与 Configuration Manager 保持同步。  
      将仅同步对许可证进行的更改。 但每隔七天都会执行一次完全同步。  
      选择“同步”执行手动同步时，将始终执行完全同步。  
-   如果需要恢复或还原 Configuration Manager 数据库，建议稍后执行手动同步，确保同步的许可证数据保持最新。  
-   此外，必须从 Apple 导入有效的 Apple Push Notification 服务 (APN) 证书，以允许管理 iOS 设备（包括应用部署）。 有关详细信息，请参阅[设置 iOS 混合设备管理](enroll-hybrid-ios-mac.md)。  
-   Configuration Manager 最多支持添加 3000 个 VPP 令牌。

从 System Center Configuration Manager 1702 开始，现在可以向设备和用户部署已授权的应用。 具体取决于应用支持设备授权的能力，合适的许可证将在部署时按以下方式声明：

|||||
|-|-|-|-|
|Configuration Manager 版本|应用是否支持设备授权？|部署集合类型|已声明的许可证|
|早于 1702|是|用户|用户许可证|
|早于 1702|否|用户|用户许可证|
|早于 1702|是|设备|用户许可证|
|早于 1702|否|设备|用户许可证|
|1702 及更高版本|是|用户|用户许可证|
|1702 及更高版本|否|用户|用户许可证|
|1702 及更高版本|是|设备|设备许可证|
|1702 及更高版本|否|设备|用户许可证|

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>步骤 1 - 获取并上载 Apple VPP 令牌  

1.  在 Configuration Manager 控制台中，选择“管理” > “云服务” > “Apple Volume Purchase Program 令牌”。   

3.  在“主页”选项卡的“Apple Volume Purchase Program 令牌”组中，选择“添加 Apple Volume Purchase Program 令牌”。  

4.  在“添加 Apple Volume Purchase Program 令牌”向导的“常规”页上，配置以下项：   

    -   **名称** - 输入此令牌的名称，因为它将显示在 Configuration Manager 控制台中。  

    -   **令牌** - 选择“浏览”，然后选择从 Apple 网站下载的 VPP 令牌。  

         选择“查看 Apple VPP 帐户”链接，如果尚未注册，请注册企业或教育批量购买计划。 注册完成后，下载适用于帐户的 Apple VPP 令牌。  

    -   **说明** - 可选择输入说明，帮助在 Configuration Manager 控制台中识别此 VPP 令牌。  

    -   **改进搜索和筛选的分配类别** -（可选）可以将类别分配到 VPP 令牌以使其在 Configuration Manager 控制台中更易搜索。  
    -   **Apple ID** - 输入与 VPP 令牌相关联的 Apple 电子邮件 ID。
    -   **令牌类型** - 选择想要使用的 VPP 令牌的类型。 可以选择**业务**和 **EDU** 令牌类型。

5.  选择“下一步”，然后完成该向导。  

从“Apple Volume Purchase Program 令牌”节点中，现在可以查看有关 Apple VPP 令牌的信息，包括其上次更新的时间、到期时间以及上次同步的时间。

在“主页”选项卡的“同步”组中选择“同步”，可以随时将 Apple 保存的数据与 Configuration Manager 完全同步。  

## <a name="step-2---deploy-a-volume-purchased-app"></a>步骤 2 - 部署批量采购的应用  

1.  在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用商店应用的许可证信息”。  

3.  选择要部署的应用，然后在“主页”选项卡的“创建”组中，选择“创建应用程序”。
所创建的 Configuration Manager 应用程序包含适用于企业的 Windows 应用商店应用。 然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。

    > [!IMPORTANT]  
    > 必须选择部署目的为“必需”。 当前不支持可用的安装。

 部署应用时，每个用户使用一个许可证，或对于设备安装，安装该应用的每个设备使用一个许可证。  如果你面向的设备集合包含支持设备授权的应用，则声明设备许可证。  如果你面向的设备集合包含不支持设备授权的应用，则声明用户许可证。 

 从**应用商店的许可证信息**节点创建应用时，该应用将与你所选的应用的令牌的许可证相关联。  例如，可能在节点中看到同一个应用的两个版本。 这是因为，应用的每个版本都与不同的 Apple VPP 令牌相关联。  然后，可以从每个令牌创建应用，并单独对其部署。

 若要回收许可证，必须新建应用部署，并且将部署操作设置为“卸载”。 不能更改原始部署中的部署操作。 应用卸载后，将回收许可证。  

## <a name="step-3---monitor-ios-vpp-apps"></a>步骤 3 - 监视 iOS VPP 应用  
 “软件库”工作区的“应用商店应用的许可证信息”节点显示了批量采购的 iOS 应用的信息。 该信息包括每个应用拥有的许可证总数，以及已部署的许可证数量。 此外，该视图显示应用关联了哪个 VPP 令牌及其类型

 还可以监视通过使用“适用于 iOS 且具有许可证计数的 Apple Volume Purchase Program 应用”报表购买的所有 VPP 应用的许可证使用情况。  

 此报表显示每个应用程序的名称，以及购买的许可证总数、可用许可证数量以及更多内容。  

 有关运行 Configuration Manager 报表的帮助信息，请参阅 [System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)。  
