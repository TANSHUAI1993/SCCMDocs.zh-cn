---
title: "基于云的分发点 | Microsoft Docs"
description: "了解有关配合使用 System Center Configuration Manager 和基于云的分发点的配置和限制。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8caf3319d93b98680ed4a719a8db714c7e4e96ce
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>将基于云的分发点用于 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

基于云的分发点是托管于 Microsoft Azure 中的 System Center Configuration Manager 分发点。 以下信息旨在帮助你了解有关使用基于云的分发点的配置和限制。

安装完成主站点并准备好安装基于云的分发点后，请参阅[在 Azure 中安装基于云的分发点](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)。


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>规划使用基于云的分发点
当你使用基于云的分发点时，你应当：  

-   **配置客户端设置**以便用户和设备能够访问内容。  

-   **指定主站点来管理内容**到分发点的传输。  

-   为想在分发点上存储的内容量**指定阈值**，以及为希望使客户端能够通过分发点传输的内容量指定阈值。  


根据配置的阈值，当在分发点上存储的内容总量接近指定的存储量时，或者当客户端传输的数据量接近定义的阈值时，Configuration Manager 可能会发出警告性警报。  

基于云的分发点支持多种功能，本地分发点也提供这些功能：  

-   可以单独或者作为分发点组成员来管理基于云的分发点。  

-   可以将基于云的分发点用作回退内容位置。  

-   你获得 Intranet 客户端和基于 Internet 的客户端的支持。  


基于云的分发点提供下列其他好处：  

-   发送给基于云的分发点的内容在 Configuration Manager 发送给 Azure 之前会由 Configuration Manager 进行加密。  

-   在 Azure 中，可以手动按比例缩放云服务，以满足客户端内容请求不断变化的需求，而不需要安装和设置其他分发点。  

-   基于云的分发点支持针对 Windows BranchCache 配置的客户端下载内容。  


基于云的分发点具有下列限制：  

-  使用具有修补程序 KB4010155 的 1610 版之前，不能使用基于云的分发点来承载软件更新包。 从 1702 及更高版本开始，此问题已得到解决。  

-   无法将基于云的分发点用于 PXE 或启用多播的部署。  

-   不会向客户端提供基于云的分发点作为通过使用部署选项“需要时通过运行任务序列本地下载内容” 部署的任务序列的内容位置。 但是，通过使用部署选项“启动任务序列之前本地下载所有内容”  部署的任务序列可以将基于云的分发点用作有效的内容位置。  

-   基于云的分发点不支持从分发点运行的包。 客户端必须下载然后在本地运行所有内容。  

-   基于云的分发点不支持使用 Application Virtualization 或类似程序对应用程序进行流式处理。  

-   基于云的分发点不支持预留的内容。 管理分发点的主站点的分发管理器将所有内容传输至分发点。  

-   无法将基于云的分发点配置为请求分发点。  

##  <a name="BKMK_PrereqsCloudDP"></a> 基于云的分发点的先决条件  
 基于云的分发点需要使用下列先决条件：  

-   Azure 订阅（请参阅本主题中的[关于订阅和证书](#BKMK_CloudDPCerts)）。

-   自签名或公钥基础结构 (PKI) 管理证书，用于从 Configuration Manager 主站点服务器到 Azure 中的云服务的通信（请参阅本主题中的[关于订阅和证书](#BKMK_CloudDPCerts)）。

-   Configuration Manager 客户端连接到基于云的分发点并通过 HTTPS 从这些分发点下载内容所使用的服务证书 (PKI)。  

-  在设备或用户可以从基于云的分发点访问内容之前，必须将“云服务”客户端设置中的“允许访问云分发点”设为“是”。 默认情况下，此值设为“否” 。  

-   客户端必须能够解析云服务的名称，这需要 DNS 命名空间中的域名系统 (DNS) 别名和 CNAME 记录。  

-   客户端必须能够访问 Internet 以使用基于云的分发点。  

##  <a name="BKMK_CloudDPCost"></a> 使用基于云的分发的成本  
 当使用基于云的分发点时，请规划 Configuration Manager 客户端进行数据存储和下载传输的成本。  

 Configuration Manager 包括用于帮助控制成本和监视数据访问的选项：  

-   你可以控制和监视云服务中存储的内容量。  

-   可将 Configuration Manager 配置为在客户端下载的“阈值”达到或超过每月限制时发出通知。  

-   此外，可以使用对等缓存 (Windows BranchCache) 来帮助减少客户端进行的从基于云的分发点传输的数据量。 为 BranchCache 配置的 Configuration Manager 客户端可以使用基于云的分发点来传输内容。  


**选项：**  

-   **适用于云的客户端设置**：通过使用“客户端设置”来控制对层次结构中所有基于云的分发点的访问。  

     在“客户端设置” 中，“云设置”  类别支持“允许访问云分发点” 设置。 默认情况下，此设置设为“否” 。 可以为用户和设备启用此设置。  

-   **数据传输阈值**：可以为你想在分发点上存储的数据量配置阈值，以及为客户端从分发点下载的数据量配置阈值。  

     基于云的分发点的阈值包括下列阈值：  

    -   **存储警报阈值**：存储警报阈值为你想存储在基于云的分发点上的数据量或内容量设置上限。 Configuration Manager 可以在剩余可用空间达到指定的水平时生成警告性警报。  

    -   **传输警报阈值**：传输警报阈值帮助你监视 30 天内从分发点传输到客户端的内容量。 传输警报阈值监视过去 30 天的数据传输量，并且在传输量达到定义的值时可能会发出警告性警报和关键警报。  

        > [!IMPORTANT]  
        >  Configuration Manager 监视数据传输，但在数据传输量超出指定的传输警报阈值时不会停止数据传输。  

 可以在安装分发点的过程中为每个基于云的分发点指定阈值，也可以在安装分发点后编辑每个基于云的分发点的属性。  

-   **警报**：可以配置 Configuration Manager，让其根据指定的数据传输阈值发出与每个基于云的分发点接收和发送的数据有关的警报。 这些警报帮助监视数据传输，并可以帮助决定何时停止云服务、调整存储在分发点上的内容或者改变可以使用基于云的分发点的客户端。  

     在每小时周期中，监视基于云的分发点的主站点从 Azure 下载事务数据，并将其存储在站点服务器的 CloudDP-&lt;ServiceName\>.log 中。 Configuration Manager 会依据每个基于云的分发点的存储和传输配额评估此信息。 在数据传输量达到或超过为警告性警报或关键警报指定的数量时，Configuration Manager 会生成相应的警报。  

    > [!WARNING]  
    >  由于是每小时从 Azure 下载一次有关数据传输的信息，因此，在 Configuration Manager 可以访问此数据并发出警报之前，数据使用量可能已超过警告阈值或关键阈值。  

    > [!NOTE]  
    >  基于云的分发点的警报视 Azure 提供的使用量统计信息而定，且可能需要最多 24 小时才能变得可用。 有关 Azure Storage Analytics 的信息（包括 Azure 更新使用量统计信息的频率），请参阅 MSDN 库中的 [Storage Analytics](http://go.microsoft.com/fwlink/p/?LinkID=275111)（存储分析）。  


-   **按需停止或启动云服务**：可以随时使用此选项来停止云服务，以阻止客户端持续使用此服务。 停止云服务时，将立即阻止客户端通过此服务下载更多的内容。 此外，可以重新启动云服务以恢复客户端访问。 例如，你可能想在达到数据阈值时停止云服务。  

     在停止云服务时，云服务不会从分发点中删除内容，也不会阻止站点服务器将更多的内容传输到基于云的分发点。  

     若要停止云服务，在 Configuration Manager 控制台中，在“管理”工作区中的“云服务”下的“云分发点”节点中选择分发点。 接着，选择“停止服务”以停止在 Azure 中运行的云服务。  

##  <a name="BKMK_CloudDPCerts"></a> 关于基于云的分发点的订阅和证书  
 基于云的分发点需要证书，以使 Configuration Manager 能够管理承载分发点的云服务，以及让客户端访问分发点中的内容。 以下信息对这些证书进行了概述。 有关详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

 **证书**  

-   **站点服务器到分发点通信的管理证书**：管理证书将在 Azure 管理 API 和 Configuration Manager 之间建立信任关系。 当执行诸如部署内容或启动和停止云服务之类的任务时，此身份验证使 Configuration Manager 能够调用 Azure API。 通过使用 Azure，可以创建自己的管理证书，此证书可以是自签名的证书或证书颁发机构 (CA) 颁发的证书：  

    -   为 Configuration Manager 配置 Azure 时向 Azure 提供管理证书的 .cer 文件。 .cer 文件包含管理证书的公钥。 在安装基于云的分发点之前，必须将此证书上传到 Azure。 此证书使 Configuration Manager 能够访问 Azure API。  

    -   安装基于云的分发点时向 Configuration Manager 提供管理证书的 .pfx 文件。 .pfx 文件包含管理证书的私钥。 Configuration Manager 将此证书存储在站点数据库中。 因为 .pfx 文件包含私钥，所以必须提供密码以将此证书文件导入到 Configuration Manager 数据库中。  

    如果创建自签名证书，则必须首先将证书导出为 .cer 文件，然后再次将其导出为 .pfx 文件。  

    （可选）可以指定 Azure SDK 1.7 中的版本 1 **.publishsettings** 文件。 有关 publishsettings 文件的信息，请参阅 Azure 文档。  

    有关详细信息，请参阅 MSDN 库的“Azure 平台”部分中的 [如何创建管理证书](http://go.microsoft.com/fwlink/p/?LinkId=220281)和[如何将管理证书添加到 Azure 订阅](http://go.microsoft.com/fwlink/p/?LinkId=241722)。  

-   **用于客户端到分发点通信的服务证书**：Configuration Manager 基于云的分发点服务证书会在 Configuration Manager 客户端和基于云的分发点之间建立信任，并保护客户端使用安全套接字层 (SSL) 通过 HTTPS 从分发点中下载的数据。  

    > [!IMPORTANT]  
    >  服务证书的证书使用者框中的公用名在域中必须唯一，并且不与任何加入域的设备匹配。  

   有关此证书的示例部署，请参阅 [System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)主题中的**为基于云的分发点部署服务证书**部分。  

##  <a name="bkmk_Tasks"></a> 基于云的分发点的常见管理任务  

-   **站点服务器到基于云的分发点的通信**：安装基于云的分发点时，必须分配一个主站点以管理将内容传输到云服务的方式。 此操作等效于在特定站点上安装分发点站点系统角色。  

-   **客户端到基于云的分发点的通信**：为设备或设备的用户配置启用基于云的分发点的客户端设置时，设备可能会收到基于云的分发点作为有效的内容位置。  

    -   当客户端评估可用内容位置时，基于云的分发点被认为是远程分发点。  

    -   只有当本地分发点不可用时，Intranet 上的客户端才会使用基于云的分发点作为回退选项。  

    即使在 Azure 的特定区域中安装基于云的分发点，使用基于云的分发点的客户端也不会知道 Azure 区域，并且会不确定地选择基于云的分发点。

这意味着如果在多个区域中安装基于云的分发点，并且客户端接收多个基于云的分发点作为内容位置，则该客户端可能不会使用它所在 Azure 区域中的基于云的分发点。  

使用基于云的分发点的客户端使用下列顺序进行内容位置请求：  

1.  配置为使用基于云的分发点的客户端始终尝试首先从首选分发点中获取内容。  

2.  当首选分发点不可用时，如果部署支持此选项并且远程分发点可用，则客户端将使用远程分发点。  

3.  当首选分发点或远程分发点不可用时，则客户端可能会回退以从基于云的分发点中获取内容。  



  当客户端使用基于云的分发点作为内容位置时，客户端使用 Configuration Manager 访问令牌自行向基于云的分发点进行身份验证。 如果客户端信任 Configuration Manager 基于云的分发点证书，则客户端可以下载请求的内容。  

-   **监视基于云的分发点**：你可以监视你部署到每个基于云的分发点的内容，并且可以监视托管分发点的云服务。  

    -   **内容**：在监视部署到基于云的分发点的内容时，所用的方式与将内容部署到本地分发点的方式相同。  

    -   **云服务**：Configuration Manager 会定期检查 Azure 服务，而且会在此服务处于不活动状态或者存在订阅或证书问题时发出警报。 还可以在 Configuration Manager 控制台的“管理”工作区中的“云服务”下的“云分发点”节点中，查看有关分发点的详细信息。 在这里，可查看有关分发点的高级信息。 还可以选择分发点，并编辑其属性。  

    在编辑基于云的分发点的属性时，可以:  

    -   调整用于存储和警报的数据阈值。  

    -   管理内容，与对本地分发点执行的操作相同。  

    最后，对于每个基于云的分发点，可以查看（但不能编辑）订阅 ID、服务名称和在安装基于云的分发点时指定的其他相关详细信息。  

-   **备份和恢复基于云的分发点**：在层次结构中使用基于云的分发点时，请使用下列信息来帮助你规划分发点的备份或恢复：  

    -   使用预定义“备份站点服务器”维护任务时，Configuration Manager 会自动包括基于云的分发点的配置。  

    -   最佳方案是，备份与基于云的分发点一起使用的管理证书和服务证书，并保存它们的副本。 如果将管理基于云的分发点的 Configuration Manager 主站点还原到另一台计算机，则必须重新导入证书才能继续使用这些证书。  

-   **卸载基于云的分发点**：若要卸载基于云的分发点，可在 Configuration Manager 控制台中选择该分发点，然后选择“删除”。  

    从层次结构中删除基于云的分发点时，Configuration Manager 会从 Azure 中的云服务中删除内容。  
