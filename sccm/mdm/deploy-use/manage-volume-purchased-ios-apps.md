---
title: Manage volume-purchased iOS apps
titleSuffix: Configuration Manager
description: 部署、管理和跟踪通过 Apple iOS App Store 购买的应用的许可证。
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 21d8666f6c05b540891037cc1917b755ed22fdcc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129386"
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理批量购买的 iOS 应用

适用范围：System Center Configuration Manager (Current Branch)



 通过 Apple iOS App Store，可以为要在公司中运行的应用购买多个许可证。 这样有助于降低跟踪已购买的多个应用副本产生的管理开销。  

 使用 Configuration Manager，可以部署和管理通过计划购买的 iOS 应用。 可以从 App Store 导入许可证信息，并跟踪正在使用的许可证数。  



## <a name="manage-volume-purchased-apps-for-ios-devices"></a>管理批量采购的适用于 iOS 设备的应用程序  
 通过 Apple Volume Purchase Program (VPP) 购买多个 iOS 应用许可证。 首先，需要在 Apple 网站中创建 Apple VPP 帐户。 然后，将 Apple VPP 令牌上传到 Configuration Manager，它具有以下功能：  

-   将批量购买信息与 Configuration Manager 同步  
 
- 同步通过 Apple Volume Purchase Program 企业版和 Apple Volume Purchase Program 教育版购买的应用  

- 将多个 Apple Volume Purchase Program 令牌与 Configuration Manager 相关联  

-   在 Configuration Manager 控制台中显示已购买的应用  

-   部署和监视这些应用  

-   跟踪每个应用的使用许可证数   

-   如果必须回收许可证，才能卸载已部署的批量购买应用，Configuration Manager 可以有助于回收许可证  



## <a name="before-you-start"></a>开始之前  
 开始前，必须先从 Apple 获取 VPP 令牌，并将它上传到 Configuration Manager。  

-   如果之前在现有的 Apple VPP 帐户中将 VPP 令牌用于其他 MDM 产品的 ，则必须创建一个新的令牌供 Configuration Manager 使用。  
-   每个令牌的有效期为一年。  
-   默认情况下，Configuration Manager 每天与 Apple VPP 服务同步两次，确保许可证与 Configuration Manager 保持同步。 将仅同步对许可证进行的更改。 每七天执行一次完全同步。 如果选择“同步”执行手动同步，此操作始终执行完全同步。  
-   如果需要恢复或还原 Configuration Manager 数据库，建议稍后执行手动同步。 这样可确保同步的许可证数据为最新。  
-   此外，还必须已从 Apple 导入有效的 Apple Push Notification 服务 (APN) 证书。 使用此证书，可以管理 iOS 设备（包括应用部署）。 有关详细信息，请参阅[设置 iOS 混合设备管理](enroll-hybrid-ios-mac.md)。  
-   Configuration Manager 最多支持添加 3000 个 VPP 令牌。

可以将许可的应用同时部署到设备和用户。 部署应用时，将声明相应的许可证（如下所示），具体视应用是否支持设备授权而定：

|应用是否支持设备授权？|部署集合类型|已声明的许可证|
|---|---|---|
|是|用户|用户许可证|
|否|用户|用户许可证|
|是|设备|设备许可证|
|否|设备|用户许可证|



## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>步骤 1 - 获取并上载 Apple VPP 令牌  

1.  在 Configuration Manager 控制台中，选择“管理” > “云服务” > “Apple Volume Purchase Program 令牌”。   

3.  在“主页”选项卡的“Apple Volume Purchase Program 令牌”组中，选择“添加 Apple Volume Purchase Program 令牌”。  

4.  在“添加 Apple Volume Purchase Program 令牌”向导的“常规”页上，配置以下设置：   

    -   **名称** - 输入要在 Configuration Manager 控制台中显示的此令牌名称。  

    -   **令牌** - 选择“浏览”，然后选择从 Apple 网站下载的 VPP 令牌。  

         单击“查看 Apple VPP 帐户”链接。 如果尚未注册，请注册企业版或教育版 Volume Purchase Program。 注册完成后，下载适用于自己帐户的 Apple VPP 令牌。  

    -   **说明** - 根据需要，输入有助于用户在 Configuration Manager 控制台中识别此令牌的说明。  

    -   **改进搜索和筛选的分配类别** -（可选）可以将类别分配到 VPP 令牌以使其在 Configuration Manager 控制台中更易搜索。  
    -   **Apple ID** - 输入与 VPP 令牌相关联的 Apple 电子邮件 ID。
    -   **令牌类型** - 选择想要使用的 VPP 令牌的类型。 可以选择**业务**和 **EDU** 令牌类型。

5.  选择“下一步”，然后完成该向导。  

现在，通过“Apple Volume Purchase Program 令牌”节点，可以查看 Apple VPP 令牌的相关信息。 此视图包含令牌的上次更新时间、到期时间和上次同步时间。

通过选择功能区中的“同步”，可以随时将 Apple 保存的数据与 Configuration Manager 完全同步。  



## <a name="step-2---deploy-a-volume-purchased-app"></a>步骤 2 - 部署批量采购的应用  

1. 在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用商店应用的许可证信息”。  

2. 选择要部署的应用，然后在“主页”选项卡的“创建”组中，选择“创建应用程序”。
   所创建的 Configuration Manager 应用程序包含适用于企业的 Microsoft Store 应用。 然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。  

   > [!IMPORTANT]  
   > 必须选择部署目的为“必需”。 当前不支持可用的安装。

   部署应用时，每个用户使用一个许可证，或对于设备安装，安装该应用的每个设备使用一个许可证。 如果你面向的设备集合包含支持设备授权的应用，则声明设备许可证。 如果定目标到的设备集合包含不支持设备授权的应用，声明的是用户许可证。 

   从**应用商店的许可证信息**节点创建应用时，该应用将与你所选的应用的令牌的许可证相关联。 例如，可能在节点中看到同一个应用的两个版本。 出现此行为是因为，应用的每个版本都与不同的 Apple VPP 令牌相关联。 然后，可以通过各个令牌创建应用，并单独进行部署。

   若要回收许可证，必须新建应用部署，并且将部署操作设置为“卸载”。 无法更改原始部署中的部署操作。 应用卸载后，就会回收许可证。  



## <a name="step-3---monitor-ios-vpp-apps"></a>步骤 3 - 监视 iOS VPP 应用  
 “软件库”工作区的“应用商店应用的许可证信息”节点显示了批量采购的 iOS 应用的信息。 该信息包括每个应用拥有的许可证总数，以及已部署的许可证数量。 此外，该视图显示应用关联了哪个 VPP 令牌及其类型

 还可以监视通过使用“适用于 iOS 且具有许可证计数的 Apple Volume Purchase Program 应用”报表购买的所有 VPP 应用的许可证使用情况。  

 此报表显示每个应用程序的名称，以及购买的许可证总数、可用许可证数量以及更多内容。  

 有关运行 Configuration Manager 报表的帮助信息，请参阅 [System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)。  



## <a name="delete-an-apple-vpp-token"></a>删除 Apple VPP 令牌  
<!--505268-->

若要从 Configuration Manager 中删除令牌，请按照以下过程操作：  

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“云服务”，再选择“Apple Volume Purchase Program 令牌”。  

2. 选择要删除的令牌。  

3. 单击功能区中的“删除”选项。  

