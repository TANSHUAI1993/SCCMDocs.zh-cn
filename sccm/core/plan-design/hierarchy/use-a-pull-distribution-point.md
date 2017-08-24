---
title: "请求分发点 | Microsoft Docs"
description: "了解通过 System Center Configuration Manager 使用请求分发点的配置和限制相关信息。"
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: db5039ff6cb93e3099b096196d49a1f06c315a6b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>将请求分发点用于 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*


System Center Configuration Manager 的请求分发点是一个标准分发点，该分发点通过从源位置（例如客户端）下载来获取分发内容，而不是将内容从站点服务器推送到分发点来获取。  

 如果将内容部署到一个站点上的大量分发点，则请求分发点可以帮助减少站点服务器上的处理负荷，并且可以有助于加快内容向每个分发点的传输速度。 此效率是通过从站点服务器上的分发管理器流程中卸载将内容传输到每个分发点的流程来实现的。  

-   可以将单独的分发点配置为请求分发点。  

-   对于每个请求分发点，必须指定一个或多个源分发点，请求分发点可以从这些源分发点获取部署（请求分发点仅可从指定为源分发点的分发点获取内容）。  

-   将内容分发到请求分发点时，站点服务器会通知随后从源分发点中发起内容下载（传输）的请求分发点。 请求分发点会通过从已具有内容副本的分发点中下载内容来单独管理内容传输。  

请求分发点支持的配置和功能与典型的 Configuration Manager 分发点支持的配置和功能相同。 例如，配置为请求分发点的分发点支持使用多播和 PXE 配置、内容验证和按需内容分发。 请求分发点支持来自客户端的 HTTP 或 HTTPS 通信、支持与其他分发点相同的证书选项，并且可以单独管理或作为分发点组的成员来进行管理。  

> [!IMPORTANT]
> 尽管请求分发点支持通过 HTTP 和 HTTPS 的通信，但在使用 Configuration Manager 时，只能指定为 HTTP 配置的源分发点。 你可以使用 Configuration Manager SDK 来指定为 HTTPS 配置的源分发点。  

 **在将内容分发到请求分发点时将按下列顺序发生事件：**  

-   将内容分发到请求分发点后，站点服务器上的包传输管理器将立即检查站点数据库，以确认内容在源分发点上是否可用。 如果它无法确认内容位于请求分发点的源分发点上，则会每隔 20 分钟重复检查一次，直至内容可用为止。  

-   当包传输管理器确认内容可用后，它将通知请求分发点下载内容。 请求分发点收到此通知后，将尝试从其源分发点下载内容。  

-   请求分发点完成内容下载后，会将此状态提交到管理点。 但是，如果在 60 分钟后未收到此状态，则包传输管理器将唤醒，并与请求分发点核对以确认请求分发点是否已下载了内容。 如果内容下载正在进行，则包传输管理器将休眠 60 分钟，之后再次与请求分发点核对。 此循环将持续，直至请求分发点完成内容传输。  

在安装分发点时或在安装分发点后，你可以通过编辑分发点站点系统角色的属性来**配置请求分发点** 。  

通过编辑分发点属性，可以删除**要成为请求分发点的配置**。 删除请求分发点配置后，分发点将恢复正常操作，并且站点服务器将管理以后将内容传输到分发点的方式。  

## <a name="limitations-for-pull-distribution-points"></a>请求分发点的限制  

-   无法将基于云的分发点配置为请求分发点。  

-   站点服务器上的分发点无法配置为请求分发点。  

-   **预留内容配置覆盖请求分发点配置**。 为预留内容配置的请求分发点将等待该内容。 它不会从源分发点中请求内容，并且，与具有预留内容配置的标准分发点相似，它也不会从站点服务器接收内容。  

-   请求分发点在传输内容时**不使用速率限制配置** 。 如果将以前安装的分发点配置为请求分发点，则会保存速率限制配置，但不使用此配置。 如果在以后删除请求分发点配置，则会实现以前配置的速率限制配置。  

    > [!NOTE]  
    >  如果分发点配置为请求分发点，则在该分发点的属性中看不到“速率限制”  选项卡。  

-   请求分发点不会为内容分发使用“重试设置”  。 可以为每个站点将“重试设置” 配置为“软件分发组件属性”  的一部分。 若要查看或配置这些属性，请在 Configuration Manager 控制台的“管理”工作区中展开“站点配置”，然后选择“站点”。 接着，在结果窗格中选择站点，然后在“主页”选项卡上选择“配置站点组件”。 最后，选择“软件分发”。  

-   要从远程林内的源分发点中传输内容，则必须在承载请求分发点的计算机上安装 Configuration Manager 客户端。 必须配置为使用可以访问源分发点的网络访问帐户。  

-   在配置为请求分发点并运行 Configuration Manager 客户端的计算机上，该客户端的版本必须与安装请求分发点的 Configuration Manager 站点相同。 这是请求分发点使用请求分发点和 Configuration Manager 客户端共有的 CCMFramework 的一项要求。  

## <a name="about-source-distribution-points"></a>关于源分发点  
 配置请求分发点时，必须指定一个或多个源分发点：  

-   系统仅显示有资格成为源分发点的分发点。  

-   可以将请求分发点指定为另一个请求分发点的源分发点。  

-   使用 Configuration Manager 时，只能将支持 HTTP 的分发点指定为源分发点。  

-   你可以使用 Configuration Manager SDK 来指定为 HTTPS 配置的源分发点。 若要使用为 HTTPS 配置的源分发点，请求分发点必须在运行 Configuration Manager 客户端的计算机上共存。  

可为请求分发点源分发点列表上的每个分发点分配一个优先级：  

-   你可以为每个源分发点分配单独的优先级，或将多个源分发点分配给同一优先级。  

-   优先级确定请求分发点按什么顺序从其源分发点请求内容。  

-   请求分发点首先将与优先级值最低的源分发点联系。  如果有多个具有同一优先级的源分发点，请求分发点将非确定性地选择优先级相同的源分发点中的其中一个。  

-   如果所选源上的内容不可用，则请求分发点随后将尝试从具有该相同优先级的另一个分发点下载内容。  

-   如果具有给定优先级的分发点都没有内容，则请求分发点将尝试从具有分配的下一个较大优先级值的分发点下载内容，直至找到内容或请求分发点在再次开始该过程之前休眠 30 分钟为止。  

当请求分发点从源分发点下载内容时，会将该请求分发点计为“分发点使用情况摘要”  报表中“已访问客户端(唯一)”  列中的一个客户端。  

 默认情况下，请求分发点使用其 **计算机帐户** 从源分发点中传输内容。 但是，当请求分发点从远程林内的源分发点中传输内容时，请求分发点始终使用网络访问帐户。 此过程要求计算机安装 Configuration Manager 客户端，并且配置要使用网络访问帐户，使其能够访问源分发点。  

## <a name="about-content-transfers"></a>关于内容传输  
 为了管理内容传输，请求分发点将使用 Configuration Manager 客户端软件的 **CCMFramework** 组件。  

-   此框架是在将分发点配置为请求分发点时由 **Pulldp.msi** 进行配置。 该框架不需要 Configuration Manager 客户端。  

-   安装请求分发点后，分发点计算机上的 CCMExec 服务必须运行，以便请求分发点正常工作。  

-   请求分发点传输内容时，它会使用 **后台智能传输服务** (BITS) 传输内容，在分发点计算机上的 **datatransferservice.log** 和 **pulldp.log** 中记录其操作。  

## <a name="see-also"></a>另请参阅  
 [System Center Configuration Manager 中内容管理的基础知识](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
