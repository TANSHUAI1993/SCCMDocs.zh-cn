---
title: "查找站点资源 | Microsoft Docs"
description: "了解 System Center Configuration Manager 客户端如何以及何时使用服务定位查找站点资源。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1c9e7ada6a8aa228b30e58865baae0f6e529e6af
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="learn-how-clients-find-site-resources-and-services-for-system-center-configuration-manager"></a>了解客户端如何查找 System Center Configuration Manager 的站点资源和服务

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 客户端使用名为*服务定位*的进程来查找可与之通信的站点系统服务器，此服务器提供客户端定向使用的服务。 了解客户端如何以及何时使用服务定位查找站点资源有助于配置站点，使其成功支持客户端任务。 这些配置可能需要站点与域和网络配置（如 Active Directory 域服务 (AD DS) 和 DNS）进行交互。 或者需要配置更复杂的替代项。  

 提供服务的站点系统角色的示例包括：

 - 用于客户端的核心站点系统服务器。
 - 管理点。
 - 可与客户端通信的其他站点系统服务器，例如分发点和软件更新点等。  



##  <a name="bkmk_fund"></a> Fundamentals of service location  
 使用服务定位查找可与之通信的管理点时，客户端会评估其当前网络位置、通信协议首选项和分配的站点。  

 **客户端与管理点进行通信从而实现以下几点：**  
-   下载有关站点的其他管理点的信息，以便可以为未来的服务定位周期生成已知管理点列表（称为 *MP 列表*）。  
-   上传配置详细信息，如清单和状态。  
-   下载策略，该策略用于在客户端上设置配置，并可通知客户端其可以或必须安装的软件以及其他相关任务。  
-   请求有关其他站点系统角色的信息，这些站点系统角色提供客户端已配置并要使用的服务。 示例包括客户端可安装的软件分发点，或可从中获取更新的软件更新点。  

**Configuration Manager 客户端提出服务定位请求：**  
-   每 25 小时的连续操作。  
-   客户端检测到其网络配置或位置发生更改时。  
-   计算机（核心客户端服务）上的 **ccmexec.exe** 服务启动时。  
-   客户端必须找到提供所需服务的站点系统角色时。  

**客户端尝试查找承载站点系统角色的服务器时**，它使用服务定位查找支持客户端协议（HTTP 或 HTTPS）的站点系统角色。 默认情况下，客户端使用提供给它们的最安全的方法。 请考虑下列各项：  

-   要使用 HTTPS，你必须具有公钥基础结构 (PKI) 并且必须在客户端和服务器上安装 PKI 证书。 有关如何使用证书的信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

-   在部署使用 Internet 信息服务 (IIS) 并支持来自客户端的通信的站点系统角色时，必须指定客户端是否使用 HTTP 或 HTTPS 连接到站点系统。 如果使用 HTTP，还必须考虑签名和加密选项。 有关详细信息，请参阅[在 System Center Configuration Manager 中规划安全性](../../../core/plan-design/security/plan-for-security.md)中的[规划签名和加密](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption)。  

##  <a name="BKMK_Plan_Service_Location"></a>服务定位和客户端如何确定向其分配的管理点  
客户端首次被分配给主站点时，它会选择此站点的默认管理点。 主站点支持多个管理点，且每个客户端将管理点独立标识为其默认的管理点。 此默认管理点之后将成为客户端的分配管理点。 （还可以使用客户端安装命令，在安装时为客户端设置分配的管理点。）  

客户端基于客户端当前网络位置和边界组配置，选择要与之通信的管理点。 即使已分配有管理点，这仍可能不是客户端使用的管理点。  

    > [!NOTE]  
    >  A client always uses the assigned management point for registration messages and certain policy messages, even when other communications are sent to a proxy or local management point.  

可使用首选管理点。 首选管理点是客户端的已分配站点中的管理点，它与客户端用于查找站点系统服务器的边界组相关联。 首选管理点作为站点系统服务器与边界组相关联，其关联方式与分发点或状态迁移点与边界组的关联方式类似。 如果为层次结构启用首选管理点，则当客户端从其已分配站点使用管理点时，它将在从其分配的站点使用其他管理点之前尝试使用首选管理点。  

还可使用 TechNet.com 上[管理点相关性](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx)博客中的信息来配置管理点相关性。 管理点相关性重写已分配管理点的默认行为，并使客户端能够使用一个或多个特定管理点。  

每当客户端需要联系管理点时，它就会检查 MP 列表，该列表本地存储在 Windows Management Instrumentation (WMI) 中。 安装客户端后，客户端会创建一个初始 MP 列表。 然后客户端会使用层次结构中有关每个管理点的详细信息定期更新该列表。  

在其 MP 列表中找不到有效管理点时，客户端会在下列服务定位源中按顺序进行搜索，直至找到可使用的管理点：  

1.  管理点  
2.  AD DS  
3.  DNS  
4.  WINS  

客户端成功定位并联系管理点后，它将下载该层次结构中可用管理点的当前列表并更新本地 MP 列表。 这同样适用于加入域以及未加入域的客户端。  

例如，当位于 Internet 上的 Configuration Manager 客户端连接到基于 Internet 的管理点时，管理点会向该客户端发送一个站点中基于 Internet 的可用管理点列表。 同样，加入域的客户端或工作组中的客户端也会接收到它们可能会使用到管理点的列表。  

对于没有针对 Internet 进行配置的客户端，不会向其提供仅面向 Internet 的管理点。 针对 Internet 配置的工作组客户端仅与面向 Internet 的管理点通信。  

##  <a name="BKMK_MPList"></a> MP 列表  
MP 列表是客户端的首选服务定位源，因为它是客户端先前标识的按优先级排列的管理点列表。 在客户端更新列表时，每个客户端都会根据其网络位置对此列表进行排序，然后此列表会本地存储在客户端上的 WMI 中。  

### <a name="building-the-initial-mp-list"></a>生成初始 MP 列表  
在安装客户端的过程中，使用以下规则生成客户端的初始 MP 列表：  

-   初始列表中包括在安装客户端的过程中指定的管理点（使用“SMSMP = 或 /MP”选项时）。  
-   客户端会对 AD DS 进行查询，以识别已发布的管理点。 为了从 AD DS 中识别出管理点，管理点必须是客户端的已分配站点，并且其产品版本必须与客户端版本相同。  
-   如果未在客户端安装过程中指定管理点，并且未扩展 Active Directory 架构，则客户端会检查 DNS 和 WINS 以识别已发布的管理点。  
-   客户端生成初始列表时，层次结构中有关某些管理点的信息可能是未知的。  

### <a name="organizing-the-mp-list"></a>组织 MP 列表  
客户端使用下列分类组织其管理点列表：  

-   **代理**：位于辅助站点的管理点。  
-   **本地**：与站点边界定义的客户端当前网络位置关联的任何管理点。 请注意关于边界的下列信息：
    -   如果客户端属于多个边界，则本地管理点列表由包括客户端当前网络位置的所有边界的联合确定。  
    -   通常情况下，本地管理点是客户端的已分配管理点的子集，除非客户端位于与另一站点关联的网络位置，且该站点上有为其边界组提供服务的管理点。   


-   **已分配**：作为客户端的已分配站点的站点系统的任何管理点。  

可使用首选管理点。 对于位于不与边界组关联的站点处，或是不位于与客户端当前网络位置关联的边界组中的站点处的管理点，不会将其视为首选。 这些管理点将在客户端无法确定可用首选管理点时使用。  

### <a name="selecting-a-management-point-to-use"></a>选择要使用的管理点  
对于典型的通信，客户端根据客户端的网络位置按以下顺序尝试使用分类的管理点：  

1.  代理  
2.  本地  
3.  已分配  

但是，对于注册消息和特定策略消息，客户端始终使用已分配管理点，即使向代理管理点或本地管理点发送了其他通信。  

在每个分类（代理、本地、或已分配）中，客户端根据首选项按以下顺序尝试使用管理点：  

1.  信任的林或本地林中支持 HTTPS 的管理点（针对 HTTPS 通信配置客户端时）  
2.  信任的林或本地林中不支持 HTTPS 的管理点（针对 HTTPS 通信配置客户端时）  
3.  信任的林或本地林中支持 HTTPS 的管理点  
4.  信任的林或本地林中不支持 HTTPS 的管理点  

客户端从按首选项排序的管理点集尝试使用该列表上的第一个管理点。 此排序的管理点列表是随机的，不能对其排序。 客户端每次更新其 MP 列表时，列表顺序都会发生变化。  

无法与第一个管理点建立联系时，客户端会尝试依次与列表上的每个管理点联系。 客户端会先尝试连接该类中的每个首选管理点，然后才尝试联系非首选管理点。 如果客户端无法与该类中的任何管理点成功通信，那么它会尝试联系下一分类中的首选管理点，依此类推，直到客户端找到要使用的管理点。  

与管理点建立通信后，客户端将继续使用同一管理点，直至：  

-   25 小时后。  
-   客户端在 10 分钟内进行了五次尝试仍无法与管理点通信。

随后客户端会随机选择要使用的新管理点。  

##  <a name="bkmk_ad"></a> Active Directory  
加入域的客户端可以将 AD DS 用于服务定位。 这要求站点 [将数据发布到 Active Directory](http://technet.microsoft.com/library/hh696543.aspx)。  

当以下所有条件为 true 时，客户端可将 AD DS 用于服务定位：  

-   Active Directory [架构已扩展](https://technet.microsoft.com/library/mt345589.aspx)或已针对 System Center 2012 Configuration Manager 进行了扩展。  
-   [配置 Active Directory 林以进行发布](http://technet.microsoft.com/library/hh696542.aspx)，并配置 Configuration Manager 站点以进行发布。  
-   客户端计算机是 Active Directory 域的成员，并可访问全局编录服务器。  

如果客户端在 AD DS 中找不到用于服务定位的管理点，那么它会尝试使用 DNS。  

##  <a name="bkmk_dns"></a> DNS  
Intranet 上的客户端可将 DNS 用于服务定位。 这要求层次结构中至少有一个站点将有关管理点的信息发布到 DNS。  

当以下任意条件为 true 时，请考虑将 DNS 用于服务定位：
-   未扩展 AD DS 架构以支持 Configuration Manager。
-   Intranet 上的客户端位于没有为 Configuration Manager 发布启用的林中。  
-   你的客户端位于工作组计算机上，并且未针对仅 Internet 的客户端管理对这些客户端进行配置。 （针对 Internet 配置的工作组客户端只与面向 Internet 的管理点通信，并且不会将 DNS 用于服务定位。）  
-   你可以 [将客户端配置为从 DNS 中查找管理点](http://technet.microsoft.com/library/gg682055)。  

当一个站点将管理点的服务定位记录发布到 DNS 时：  

-   发布仅适用于接受来自 Intranet 的客户端连接的管理点。  
-   发布操作将在管理点计算机的 DNS 区域中添加一个服务定位资源记录 (SRV RR)。 该计算机的 DNS 中必须包含一个对应的主机条目。  

默认情况下，加入域的客户端从其本地域搜索 DNS 以获取管理点记录。 对于具有发布到 DNS 的管理点信息的域，可配置用于为域指定域后缀的客户端属性。  

有关如何配置 DNS 后缀客户端属性的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端计算机以使用 DNS 发布查找管理点](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md)。  

如果客户端在 DNS 中找不到用于服务定位的管理点，那么它会尝试使用 WINS。  

### <a name="publish-management-points-to-dns"></a>将管理点发布到 DNS  
要将管理点发布到 DNS，必须满足下面两个条件：  

-   你的 DNS 服务器通过使用版本至少为 8.1.2 的 BIND 支持服务定位资源记录。  
-   Configuration Manager 中管理点的指定 Intranet FQDN 在 DNS 中具有主机条目（例如，A 记录）。  

> [!IMPORTANT]  
>  Configuration Manager DNS 发布不支持非连续命名空间。 如果有不连续的命名空间，则可将管理点手动发布到 DNS，或使用本部分中记录的一种其他服务定位方法。  

**DNS 服务器支持自动更新时**，可以配置 Configuration Manager 以将 Intranet 上的管理点自动发布到 DNS，或者可以将这些记录手动发布到 DNS。 将管理点发布到 DNS 时，会在服务定位 (SRV) 记录中发布其 Intranet FQDN 和端口号。 可在站点的“管理点组件属性”中配置站点的 DNS 发布。 有关详细信息，请参阅 [System Center Configuration Manager 的站点组件](../../../core/servers/deploy/configure/site-components.md)。  

**将 DNS 区域设置为“仅安全”以进行动态更新时**，仅第一个发布到 DNS 的管理点可以使用默认权限成功进行操作。

如果只有一个管理点可成功发布和更改其 DNS 记录，且该管理点服务器运行良好，那么客户端就可从该管理点获取完整 MP 列表，然后查找其首选管理点。


**如果 DNS 服务器不支持自动更新，但确实支持服务定位记录**，你可以将管理点手动发布到 DNS。 为完成此操作，你必须在 DNS 中手动指定服务定位资源记录 (SRV RR)。  

Configuration Manager 支持服务定位记录的 RFC 2782。 这些记录格式如下：*_Service._Proto.Name TTL Class SRV Priority Weight Port Target*  

若要将管理点发布到 Configuration Manager，请指定下列值：  

-   **_Service**：输入 **_mssms_mp**_&lt;sitecode\>，其中 &lt;sitecode\> 是管理点的站点代码。  
-   **._Proto**：指定 **._tcp**。  
-   **.Name**：输入管理点的 DNS 后缀，例如 **contoso.com**。  
-   **TTL**：输入 **14400**，代表四个小时。  
-   **类**：指定 **IN** （符合 RFC 1035）。  
-   **Priority**：Configuration Manager 不使用此字段。
-   **Weight**：Configuration Manager 不使用此字段。  
-   **端口**：输入管理点使用的端口号，例如 **80** （适用于 HTTP）和 **443** （适用于 HTTPS）。  

    > [!NOTE]  
    >  SRV 记录端口应与管理点使用的通信端口匹配。 默认情况下，对于 HTTP 通信，该端口为 **80**，对于 HTTPS 通信，端口为 **443**。  

-   “目标”：输入为配置为具有管理点站点角色的站点系统指定的 Intranet FQDN。  

如果使用 Windows Server DNS，你可以使用下列部分来为 Intranet 管理点输入此 DNS 记录。 如果使用 DNS 的其他实现，请使用此部分中有关字段值的信息，并查阅该 DNS 文档以适应此过程。  

##### <a name="to-configure-automatic-publishing"></a>配置自动发布：  

1.  在 Configuration Manager 控制台中，展开“管理” > “站点配置” > “站点”。  

2.  选择站点，然后选择“配置站点组件”。  

3.  选择“管理点”。  

4.  选择要发布的管理点。 （此选项适用于发布到 AD DS 和 DNS。）  

5.  勾选该框以发布到 DNS。 此框的作用：  

    -   可选择要发布到 DNS 的管理点。  

    -   不会配置发布到 AD DS。  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>将管理点手动发布到 Windows Server 上的 DNS  

1.  在 Configuration Manager 控制台中，指定站点系统的 Intranet FQDN。  

2.  在 DNS 管理控制台中，选择管理点计算机的 DNS 区域。  

3.  验证是否有站点系统的 Intranet FQDN 的主机记录（A 或 AAAA）。 如果此记录不存在，则创建它。  

4.  通过使用“新建其他记录”选项，在“资源记录类型”对话框中选择“服务位置(SRV)”，选择“创建记录”，输入下列信息，然后选择“完成”：  

    -   **域**：必要时，输入管理点的 DNS 后缀，例如 **contoso.com**。  
    -   **服务**：键入 **_mssms_mp**_&lt;sitecode\>，其中 &lt;sitecode\> 是管理点的站点代码。  
    -   **协议**：键入 **_tcp**。  
    -   **Priority**：Configuration Manager 不使用此字段。  
    -   **Weight**：Configuration Manager 不使用此字段。  
    -   **端口**：输入管理点使用的端口号，例如 **80** （适用于 HTTP）和 **443** （适用于 HTTPS）。  

        > [!NOTE]  
        >  SRV 记录端口应与管理点使用的通信端口匹配。 默认情况下，对于 HTTP 通信，该端口为 **80**，对于 HTTPS 通信，端口为 **443**。  

    -   **提供此服务的主机**：输入为站点系统指定的 Intranet FQDN，该站点系统配置有管理点站点角色。  

为 Intranet 上每个要发布到 DNS 的管理点重复这些步骤。  

##  <a name="bkmk_wins"></a> WINS  
当其他服务定位机制失败时，客户端可通过检查 WINS 来查找初始管理点。  

默认情况下，主站点在站点上将针对 HTTP 配置的第一个管理点和针对 HTTPS 配置的第一个管理点发布到 WINS。  

如果你不希望客户端在 WINS 中找到 HTTP 管理点，则使用 CCMSetup.exe Client.msi 属性 **SMSDIRECTORYLOOKUP=NOWINS**配置客户端。  
