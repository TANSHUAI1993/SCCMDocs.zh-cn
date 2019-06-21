---
title: 请求分发点
titleSuffix: Configuration Manager
description: 了解在结合使用 Configuration Manager 和拉取分发点方面的配置和限制。
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f3e759ef44170c460118d3629d8a7b9648ed8528
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251648"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>结合使用 Configuration Manager 和拉取分发点

适用范围：  System Center Configuration Manager (Current Branch)


如果将内容分发给 Configuration Manager 控制台中的标准分发点，站点服务器会将该内容推送至分发点。 拉取分发点通过从客户端等源位置进行下载来获取内容。  

在将内容分发到多个分发点时，拉取分发点有助于降低站点服务器的处理负荷。 它们还能更快地将内容传输到每个服务器。 通常，站点服务器上的分发管理器组件将内容发送到每个分发点。 相对的，站点则卸载将内容传输至拉取分发点的进程。  

可以将单独的分发点配置为请求分发点。 对于每个拉取分发点，请指定可从中获取内容的一个或多个源分发点。 拉取分发点只能从指定为源分发点的分发点中下载内容。 

在将内容分发到控制台中的拉取分发点时，站点服务器会向其发送通知。 然后，拉取分发点从源分发点下载内容。 拉取分发点通过从已具有内容副本的分发点下载内容，实现内容传输的管理。  

拉取分发点支持的配置和功能与典型的分发点所支持的相同。 例如，拉取分发点支持以下内容： 
- 多播和 PXE 配置
- 内容验证
- 按需内容分发
- 来自客户端的 HTTP 或 HTTPS 通信
- 与其他分发点相关的证书选项
- 单独管理或作为分发点组的成员进行管理  

> [!IMPORTANT]  
> 尽管拉取分发点支持通过 HTTP 和 HTTPS 通信，但在使用 Configuration Manager 控制台时，你只能指定配置为通过 HTTP 通信的源分发点。 你可以使用 Configuration Manager SDK 来指定为 HTTPS 配置的源分发点。  

在安装分发点时配置拉取分发点。 创建分发点之后，可通过编辑角色属性将其配置为拉取分发点。 要详细了解如何使分发点成为拉取分发点，请参阅[拉取分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pull)。  

通过编辑分发点属性，可删除要成为拉取分发点的配置。 如果删除作为拉取分发点的配置，则它将返回到正常操作。 站点服务器对之后到分发点的内容传输进行管理。  



### <a name="distribution-process"></a>分发过程

在将内容分发到拉取分发点时，按下列顺序发生事件：

-   将内容分发到控制台中的拉取分发点之后，站点服务器上的包传输管理器组件会检查站点数据库，确认内容在源分发点上是否可用。 如果无法确认内容位于拉取分发点的源分发点上，则每 20 分钟重复检查一次，直至内容可用为止。  

-   当包传输管理器确认内容可用后，它将通知请求分发点下载内容。 如果此通知失败，则它根据拉取分发点的软件分发组件“重试设置”进行重试  。 拉取分发点收到此通知后，会尝试从其源分发点下载内容。  

-   在拉取分发点下载内容时，包传输管理器将根据拉取分发点的软件分发组件“状态轮询设置”轮询状态  。  在请求分发点完成内容下载后，它会将此状态提交到管理点。  



## <a name="configure-site-component-settings"></a>配置站点组件设置

使用拉取分发点时，请查看并配置以下站点组件设置：  

1.  在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。  

2.  选择站点。 在功能区中，单击“配置站点组件”并选择“软件分发”   。  

3. 切换到“拉取分发点”选项卡  。  

4.  在“重试设置”组中查看以下值  ：  

    -   **重试次数**：包传输管理器尝试通知拉取分发点下载内容的次数。 在尝试次数达到该值后，包传输管理器会取消传输。 该值默认为 30。  

    -   **重试前的延迟(分钟)** ：包传输管理器在两次尝试之间等待的分钟数。 该值默认为 20。  

5.  在“状态轮询设置”组中查看以下值  ：  

    -   **轮询次数**：包传输管理器联系拉取分发点以检索作业状态的次数。 如果尝试次数在作业完成之前达到了该值，包传输管理器会取消传输。 该值默认为 72。   

    -   **重试前的延迟(分钟)** ：包传输管理器在两次尝试之间等待的分钟数。 该值默认为 60。   
    
    > [!NOTE]  
    >  当包传输管理器由于超过轮询重试次数而取消作业时，拉取分发点会继续下载内容。 下载完毕时，拉取分发点将发送相应的状态消息，且控制台将反映出新的状态。  
    


## <a name="limitations"></a>限制 

-   无法将云分发点配置为拉取分发点。  

-   无法将站点服务器上的分发点角色配置为拉取分发点。  

-   预留内容配置覆盖拉取分发点配置。 如果在拉取分发点上打开“为预留的内容启用此分发点”选项，则它会等待内容  。 它不会从源分发点拉取内容。 就像为预留内容启用的标准分发点一样，它不从站点服务器接收内容。 有关详细信息，请参阅[预留内容](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent)。  

-   拉取分发点不使用计划或速率限制配置。 如果将之前安装的分发点配置为拉取分发点，则会保存计划和速率限制配置，但不使用这些配置。 如果在以后删除请求分发点配置，则会实现以前配置的计划和速率限制配置。  

    > [!NOTE]  
    >  “计划”和“速率限制”选项卡在分发点属性中隐藏   。  

-   对于每个站点，拉取分发点不使用“软件分发组件属性”的“常规”选项卡上的设置   。 这些设置包括“并发分发”和“多播重试”   。  

-   要从远程林中的源分发点传输内容，请在拉取分发点上安装 Configuration Manager 客户端。 此外，请配置可访问源分发点的网络访问帐户。 自版本 1806 起，如果启用“将 Configuration Manager 生成的证书用于 HTTP 站点系统”  站点选项，则不需要网络访问帐户。<!--1358228-->  

-   如果拉取分发点还是一个 Configuration Manager 客户端，则该客户端的版本必须与安装拉取分发点的 Configuration Manager 站点相同。 拉取分发点使用该分发点和 Configuration Manager 客户端共有的 CCMFramework。  



## <a name="about-source-distribution-points"></a>关于源分发点  

配置拉取分发点时，请指定一个或多个源分发点：  

-   向导仅显示有资格成为源分发点的分发点。  

-   可以将请求分发点指定为另一个请求分发点的源分发点。  

-   在使用 Configuration Manager 控制台时，只能将支持 HTTP 的分发点指定为源分发点。  

-   请使用 Configuration Manager SDK 来指定为 HTTPS 配置的源分发点。 若要使用为 HTTPS 配置的源分发点，请在拉取分发点上安装 Configuration Manager 客户端。  

-   自版本 1806 起，如果远程办公室与 Internet 建立了更好的连接，或者希望减少 WAN 链路负载，可在 Microsoft Azure 中将[云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)用作源。 请求分发点需要访问 Internet 才能与 Microsoft Azure 通信。 必须内容将分发到源云分发点。<!--1321554-->  

    > [!Note]  
    > 此功能确实会对你的 Azure 数据存储和网络出口订阅收取费用。 有关详细信息，请参阅[使用云分发点所产生的成本](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost)。  


> [!Tip]  
> 当请求分发点从源分发点下载内容时，会将该请求分发点计为“分发点使用情况摘要”  报表中“已访问客户端(唯一)”  列中的一个客户端。  


### <a name="source-priorities"></a>源优先级

-   可为每个源分发点分配单独的优先级，也可向多个源分发点分配相同的优先级。  

-   优先级确定拉取分发点按什么顺序从其源分发点请求内容。  

-   请求分发点首先将与优先级值最低的源分发点联系。 如果有多个源分发点具有相同的优先级，则拉取分发点随机选择该优先级上的某个源分发点。  

-   如果所选源上的内容不可用，拉取分发点随后会尝试从该优先级上的其他分发点下载内容。  

-   如果具有给定优先级的分发点均没有内容，则拉取分发点会尝试从下一优先级的源分发点下载内容。 它会继续此搜索，直到找到内容。   

- 如果所分配的源分发点均没有内容，则则拉取分发点会等待 30 分钟，然后重新开始此过程。  



## <a name="inside-the-pull-distribution-point"></a>在拉取分发点中 

-   拉取分发点使用 CCMFramework 组件来管理内容传输  。 Configuration Manager 客户端包含此组件。  

-   在启用拉取分发点时，站点会安装 pulldp.msi  。 此安装程序还会添加 CCMFramework 组件。 该框架不需要 Configuration Manager 客户端。  

-   安装拉取分发点后，主要使用 CCMExec 服务进行运行  。  

-   当拉取分发点传输内容时，它使用 Windows 中内置的后台智能传输服务 (BITS)  。 拉取分发点不要求安装 IIS 服务器的 BITS 扩展。<!--sms.503672 -Clarified BITS use-->

-  要了解操作的详细信息，请参阅有关拉取分发点的下述日志文件：  
    - **DataTransferService.log**
    - **PullDP.log**



## <a name="see-also"></a>另请参阅  
 [内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
