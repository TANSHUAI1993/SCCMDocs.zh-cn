---
title: 站点组件
titleSuffix: Configuration Manager
description: 了解如何配置站点组件来修改站点系统角色和站点状态报告的行为。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c64968ca0348b94e3fb20367af7f739d8a699c58
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673592"
---
# <a name="site-components-for-configuration-manager"></a>Configuration Manager 的站点组件

适用范围：System Center Configuration Manager (Current Branch)

在每个 Configuration Manager 站点上，均可以配置站点组件来修改站点系统角色和站点状态报告的行为。 站点组件配置适用于站点以及站点中适用的站点系统角色的每个实例。  

在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。 选择一个站点。 在功能区的“设置”组中，选择“配置站点组件”。 选择下列选项之一：

- [软件分发](#software-distribution)  
- [软件更新点](#software-update-point) 
- [操作系统部署](#operating-system-deployment)
- [管理点](#management-point)  
- [状态报告](#status-reporting)  
- [电子邮件通知](#email-notification)
- [集合成员身份评估](#bkmk_colleval)


## <a name="about-site-components"></a>有关站点组件  

 在 Configuration Manager 控制台中查看时，各种站点组件的大多选项均一目了然。 但是，以下详细信息有助于解释一些更复杂的配置，或将指引你找到附加内容。  

> [!Note]  
> 无论选择管理中心站点、主站点还是辅助站点，某些组件的可用选项都会有所不同。 某些组件根本无法用于某些类型的站点。  



### <a name="software-distribution"></a>软件分发  

#### <a name="content-distribution-settings"></a>内容分发设置
在“常规”选项卡上，可以指定设置，该设置可修改站点服务器将内容传输到其分发点的方式。 当增加用于并发分发设置的值时，内容分发可以使用更多的网络带宽。  

#### <a name="pull-distribution-point"></a>拉取分发点
有关详细信息，请参阅[使用拉取分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。

#### <a name="network-access-account"></a>网络访问帐户
有关详细信息，请参阅[网络访问帐户](/sccm/core/plan-design/hierarchy/accounts#network-access-account)。  


### <a name="software-update-point"></a>软件更新点  

有关详细信息，请参阅[安装软件更新点](/sccm/sum/get-started/install-a-software-update-point)。  


### <a name="operating-system-deployment"></a>操作系统部署

有关详细信息，请参阅[指定用于为脱机 OS 映像提供服务的驱动器](/sccm/osd/get-started/manage-operating-system-images#bkmk_servicing-drive)。


### <a name="management-point"></a>管理点  

在“常规”选项卡上，可设置站点，将有关其管理点的信息发布到 Active Directory 域服务。  

Configuration Manager 客户端使用管理点查找服务，并查找站点信息（例如边界组成员身份和 PKI 证书选择选项）。 此外，客户端还使用管理点查找站点中的其他管理点以及从中下载软件的分发点。 管理点还可帮助客户端完成站点分配、下载客户端策略和上传客户端信息。  

在 Active Directory 域服务中发布管理点是客户端查找它们最安全的方法。 此服务定位方法需要以下内容为 true：

- 为 Configuration Manager 扩展架构。
- 存在具有相应安全权限的“系统管理”容器，以便站点服务器发布到此容器。
- 已设置 Configuration Manager 站点，可发布到 Active Directory 域服务。
- 客户端与站点服务器林属于相同的 Active Directory 林。  

当 Intranet 上的客户端无法使用 Active Directory 域服务来查找管理点时，请使用 [DNS 发布](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_dns)。  

有关服务定位的信息，请参阅[了解客户端如何查找站点资源和服务](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services)。  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>在 DNS 中发布所选的 Intranet 管理点
当 Intranet 上的客户端无法从 Active Directory 域服务中找到管理点时，请指定此选项。 但它们可以使用 DNS 服务定位资源记录 (SRV RR) 在为其分配的站点中查找管理点。  

要使 Configuration Manager 能够将 Intranet 管理点发布到 DNS，必须满足下列所有条件：  

-   你的 DNS 服务器的 BIND 版本为 8.1.2 或更高。  

-   你的 DNS 服务器已设置为自动更新并支持服务定位资源记录。  

-   Configuration Manager 中管理点的指定完全限定域名 (FQDN) 在 DNS 中具有主机条目（A 或 AAA 记录）。  

> [!WARNING]  
>  为了使客户端能够查找 DNS 中发布的管理点，必须将客户端分配给特定站点（而不是使用自动站点分配）。 将这些客户端设置为使用具有其管理点的域后缀的站点代码。 有关详细信息，请参阅[查找管理点](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points)。  

如果 Configuration Manager 客户端无法使用 Active Directory 域服务或 DNS 在 Intranet 上查找管理点，它们将使用 [WINS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_wins)。 如果为站点安装的第一个管理点设置为接受 Intranet 上的 HTTP 客户端连接，则它将自动发布到 WINS。  


### <a name="status-reporting"></a>状态报告  

这些设置直接设置详细级别（包括在来自站点和客户端的状态报告中）。  


### <a name="email-notification"></a>电子邮件通知  

指定帐户和电子邮件服务器的详细信息以启用 Configuration Manager 发送电子邮件警报通知。  

有关详细信息，请参阅[使用警报和状态系统](/sccm/core/servers/manage/use-alerts-and-the-status-system)。


### <a name="bkmk_colleval"></a>集合成员身份评估  

使用此组件来设置以增量方式对集合成员身份进行评估的频率。 增量评估仅使用新资源或已更改资源来更新集合成员身份。  

有关详细信息，请参阅[集合的最佳做法](/sccm/core/clients/manage/collections/best-practices-for-collections)。



##  <a name="BKMK_ServiceMgr"></a> 使用 Configuration Manager 服务管理器管理站点组件  

可以使用 Configuration Manager Service Manager 控制 Configuration Manager 服务，以及查看任何 Configuration Manager 服务或工作线程的状态。 这些服务和线程统称为 Configuration Manager 组件。 了解以下关于 Configuration Manager 组件的内容：  

-   组件可在任何站点系统上运行。  

-   管理组件的方式与在 Windows 中管理服务的方式相同。 可以启动、停止、暂停、恢复或查询 Configuration Manager 组件。  

有要执行的操作时，Configuration Manager 服务就会运行。 通常在将配置文件写入组件的收件箱时执行此操作。 


### <a name="use-the-configuration-manager-service-manager"></a>使用 Configuration Manager 服务管理器  

1.  在 Configuration Manager 控制台中，转到“监视”工作区，展开“系统状态”，然后选择“组件状态”节点。  

2.  在功能区的“组件”组中，选择“启动”，然后选择“Configuration Manager Service Manager”。  

3.  当 Configuration Manager 服务管理器打开时，连接到要管理的站点。  

     如果看不到想要管理的站点，请转到“站点”菜单，选择“连接”。 然后输入正确站点的站点服务器名称。  

4.  展开站点并导航到“组件”  或“服务器” ，具体情况视你要管理的组件位于何处而定。  

5.  在右侧窗格中，选择一个或多个组件。 然后在“组件”菜单上选择“查询”，更新所选组件的状态。  

6.  更新组件状态后，可使用“组件”菜单上四个基于操作的选项之一来修改组件操作。 请求操作之后，你必须查询组件以显示组件的新状态。  

7.  修改完组件的操作状态后，关闭 Configuration Manager Service Manager。  
