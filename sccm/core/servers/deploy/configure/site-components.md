---
title: "Configuration Manager 的站点组件 | Microsoft Docs"
description: "了解如何配置站点组件来修改站点系统角色和站点状态报告的行为。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 83550fbf0ef1f9adb0bb2c51a4f3c26a7500d352
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="site-components-for-system-center-configuration-manager"></a>System Center Configuration Manager 的站点组件

*适用范围：System Center Configuration Manager (Current Branch)*

在每个 System Center Configuration Manager 站点上，均可设置站点组件来修改站点系统角色和站点状态报告的行为。 站点组件配置适用于站点以及站点中适用的站点系统角色的每个实例。  

## <a name="about-site-components"></a>有关站点组件  
 在 Configuration Manager 控制台中查看时，各种站点组件的大多选项均一目了然。 但是，以下详细信息有助于解释一些更复杂的配置，或将指引你找到对其进行说明的附加内容。  

### <a name="software-distribution"></a>软件分发  

-   **内容分发设置：**可以指定设置，该设置可修改站点服务器将内容传输到其分发点的方式。 当增加用于并发分发设置的值时，内容分发可以使用更多的网络带宽。  

-   **网络访问帐户：**有关设置和使用网络访问帐户的信息，请参阅[网络访问帐户](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA)。  

### <a name="software-update-point"></a>软件更新点  

-   若要了解软件更新点组件的配置选项，请参阅[安装软件更新点](../../../../sum/get-started/install-a-software-update-point.md)。  

### <a name="management-point"></a>管理点  

-   **管理点：**可设置站点，将有关其管理点的信息发布到 Active Directory 域服务。  

     Configuration Manager 客户端使用管理点查找服务，并查找站点信息（例如边界组成员身份和 PKI 证书选择选项）。 此外，客户端还使用管理点查找站点中的其他管理点以及从中下载软件的分发点。 管理点还可帮助客户端完成站点分配、下载客户端策略和上传客户端信息。  

     由于客户端查找管理点的最安全方法是在 Active Directory 域服务中发布它们，因此你通常会始终选择所有正常运行的管理点以发布到 Active Directory 域服务。 但是，此服务定位方法需要以下内容为 true：

     - 为 Configuration Manager 扩展架构。
     - 存在具有相应安全权限的“系统管理”容器，以便站点服务器发布到此容器。
     - 已设置 Configuration Manager 站点，可发布到 Active Directory 域服务。
     - 客户端与站点服务器林属于相同的 Active Directory 林。  

     如果 Intranet 上的客户端无法使用 Active Directory 域服务查找管理点，请改为使用 [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) 发布。  

 有关服务定位的信息，请参阅 [了解客户端如何查找 System Center Configuration Manager 的站点资源和服务](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

-   **在 DNS 中发布所选的 Intranet 管理点：**如果 Intranet 上的客户端无法从 Active Directory 域服务中查找管理点，请指定此选项。 但它们可以使用 DNS 服务定位资源记录 (SRV RR) 在为其分配的站点中查找管理点。  

    要使 Configuration Manager 能够将 Intranet 管理点发布到 DNS，必须满足下列所有条件：  

    -   你的 DNS 服务器的 BIND 版本为 8.1.2 或更高。  

    -   你的 DNS 服务器已设置为自动更新并支持服务定位资源记录。  

    -   Configuration Manager 中管理点的指定完全限定域名 (FQDN) 在 DNS 中具有主机条目（A 或 AAA 记录）。  

    > [!WARNING]  
    >  为了使客户端能够查找 DNS 中发布的管理点，必须将客户端分配给特定站点（而不是使用自动站点分配）。 将这些客户端设置为使用具有其管理点的域后缀的站点代码。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端分配到一个站点](/sccm/core/clients/deploy/assign-clients-to-a-site)中的[定位管理点](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points)。  

     如果 Configuration Manager 客户端无法使用 Active Directory 域服务或 DNS 在 Intranet 上查找管理点，它们将使用 [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins)。 如果为站点安装的第一个管理点设置为接受 Intranet 上的 HTTP 客户端连接，则它将自动发布到 WINS。  

### <a name="status-reporting"></a>状态报告  

-   这些设置直接设置详细级别（包括在来自站点和客户端的状态报告中）。  

### <a name="email-notification"></a>电子邮件通知  

-   指定帐户和电子邮件服务器的详细信息以启用 Configuration Manager 发送电子邮件警报通知。  

### <a name="collection-membership-evaluation"></a>集合成员身份评估  

-   使用此任务来设置以增量方式对集合成员身份进行评估的频率。 增量评估仅使用新资源或已更改资源来更新集合成员身份。  

### <a name="edit-the-site-components-at-a-site"></a>编辑站点上的站点组件  

使用以下步骤编辑站点组件：

1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” > “站点”，然后选择具备要配置的站点组件的站点。  

2.  在“主页”选项卡上的“设置”组中，单击“配置站点组件”。 然后选择要配置的站点组件。  

##  <a name="BKMK_ServiceMgr"></a> 使用 Configuration Manager 服务管理器管理站点组件  
可以使用 Configuration Manager Service Manager 控制 Configuration Manager 服务，以及查看任何 Configuration Manager 服务或工作线程（统称为 Configuration Manager 组件）的状态。 了解以下关于 Configuration Manager 组件的内容：  

-   组件可在任何站点系统上运行。  

-   管理组件的方式与在 Windows 中管理服务的方式相同。 可以启动、停止、暂停、恢复或查询 Configuration Manager 组件。  

Configuration Manager 服务会在其有要执行的操作时（通常，在将配置文件写入组件的收件箱时）运行。 如果必须确定操作中涉及的组件，可以使用 Configuration Manager 服务管理器操作各种服务和线程。 然后查看 Configuration Manager 的行为中因此所发生的变化。 例如，可以一次停止一个 Configuration Manager 服务，直至排除特定响应为止。 通过这样做，你将能够确定哪个服务导致了该行为。  

> [!TIP]  
>  可以使用下列过程来操作 Configuration Manager 组件操作。  

### <a name="use-the-configuration-manager-service-manager"></a>使用 Configuration Manager 服务管理器  

1.  在 Configuration Manager 控制台中，单击“监视” >  “系统状态”然后单击“组件状态”。  

2.  在“主页”选项卡上的“组件”组中，单击“启动”。 然后选择“Configuration Manager 服务管理器”。  

3.  当 Configuration Manager 服务管理器打开时，连接到要管理的站点。  

     如果看不到要管理的站点，请单击“站点” ，单击“连接” ，然后输入正确的站点的站点服务器的名称。  

4.  展开站点并导航到“组件”  或“服务器” ，具体情况视你要管理的组件位于何处而定。  

5.  在右侧窗格中，选择一个或多个组件。 然后在“组件”菜单上单击“查询”，更新所选组件的状态。  

6.  更新组件状态后，可使用“组件”菜单上四个基于操作的选项之一来修改组件操作。 请求操作之后，你必须查询组件以显示组件的新状态。  

7.  修改完组件的操作状态后，关闭 Configuration Manager Service Manager。  
