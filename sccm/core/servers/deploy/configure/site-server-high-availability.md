---
title: 站点服务器高可用性
titleSuffix: Configuration Manager
description: 如何通过添加被动模式站点服务器来配置 Configuration Manager 站点服务器高可用性。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be12cfe29ff470f2f577bab2c685695ae5770bae
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131415"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Configuration Manager 中的站点服务器高可用性

适用范围：System Center Configuration Manager (Current Branch)

<!--1128774-->

从 Configuration Manager 1806 版开始，站点服务器角色的高可用性（一个基于 Configuration Manager 的解决方案）可用于安装被动模式下的其他站点服务器。 被动模式下的站点服务器是对主动模式下的现有站点服务器的补充。 在需要时可立即使用被动模式下的站点服务器。 将此附加站点服务器作为整体设计的一部分，从而使 Configuration Manager 服务获得[高可用性](/sccm/core/servers/deploy/configure/high-availability-options)。  

被动模式下的站点服务器：
- 使用同一站点数据库作为主动模式下的站点服务器。
- 只要它处于被动模式，就不会向站点数据库写入数据。
- 使用同一内容库作为主动模式下的站点服务器。

要使站点服务器处于被动模式，请手动将其提升。 此操作将主动模式下的站点服务器切换为被动模式下的站点服务器。 只要该计算机可以访问，在原始主动模式服务器上可用的站点系统角色将仍然可用。 仅站点服务器角色会在主动和被动模式之间切换。

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。



## <a name="prerequisites"></a>先决条件

- 被动模式下的站点服务器可以是本地服务器或是 Azure 中基于云的服务器。  
    > [!Note]  
    > 被动模式下基于云的站点服务器使用 Azure基础结构即服务 (IaaS)。 有关详细信息，请参阅下列文章：  
    > - [Azure 虚拟机（用于基于云的基础结构）](/sccm/core/understand/use-cloud-services#azure-virtual-machines-for-cloud-based-infrastructure)
    > - [Azure 上的 Configuration Manager 常见问题解答](/sccm/core/understand/configuration-manager-on-azure)  

- 两个站点服务器必须加入同一个 Active Directory 域。  

- 站点是独立主站点。 

- 两个站点服务器必须使用同一站点数据库，该数据库对每个站点服务器必须是远程的。  

     - 两个站点服务器都需要对承载站点数据库的 SQL Server 实例拥有 sysadmin 权限。

     - 承载站点数据库的 SQL Server 可以使用默认实例、命名实例、[SQL Server 群集](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database)或 [SQL Server Always On 可用性组](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。  

     - 被动模式下的站点服务器被配置为使用与主动模式站点服务器相同的站点数据库。 被动模式下的站点服务器仅从数据库中进行读取。 在将数据库提升为主动模式之前，它都不会向数据库写入数据。  

- 站点内容库必须位于远程网络共享上。 两个站点服务器都需要对共享及其内容拥有完全控制权限。 有关详细信息，请参阅[管理内容库](/sccm/core/plan-design/hierarchy/the-content-library#manage-content-library)。<!--1357525-->  

    - 站点服务器无法获得分发点角色。 分发点也使用内容库，并且此角色不支持远程内容库。 移动内容库后，无法将分发点角色添加到站点服务器。  

- 被动模式下的站点服务器：  

     - 必须满足[安装主站点的先决条件](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site)。  

     - 在主动模式站点服务器的本地 Administrator 组中必须要有其计算机帐户。<!--516036-->

     - 使用与主动模式站点服务器的版本相匹配的源文件进行安装。  

     - 在安装被动模式下的站点服务器之前，无法从任何站点获得站点系统角色。  

- 只要 [Configuration Manager 支持](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)，两个站点服务器都可以运行不同的 OS 或 Service Pack 版本。  



## <a name="limitations"></a>限制
- 每个主站点均支持在被动模式下的单一站点服务器。  

- 层次结构中不支持被动模式下的站点服务器。 层次结构中包含管理中心站点和子主站点。 仅在独立主站点上创建被动模式站点服务器。<!--1358224-->

- 辅助站点不支持被动模式下的站点服务器。<!--SCCMDocs issue 680-->  

- 将被动模式下的站点服务器提升到主动模式下站点服务器需要手动进行。 没有任何自动故障转移。  

- 在添加被动模式站点服务器之前，无法在新服务器上安装站点系统角色。  

    > [!Note]  
    > 在安装被动模式站点服务器之后，可以根据需要添加其他角色。 例如，SMS 提供程序或主站点上的管理点。  

- 对于使用数据库的报告点等角色，请在远离这两个站点服务器的服务器上托管数据库。  

- SMS_Provider 不会安装在被动模式站点服务器上。 连接到站点的提供程序，手动将被动模式下的站点服务器提升为主动模式。 在另一台服务器上至少安装一个提供程序的其他实例。 有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。  

- Configuration Manager 控制台不会自动安装在被动模式下的站点服务器上。  



## <a name="add-a-site-server-in-passive-mode"></a>添加被动模式站点服务器

有关添加角色的一般过程的详细信息，请参阅[安装站点系统角色](/sccm/core/servers/deploy/configure/install-site-system-roles)。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，选择“站点”节点，然后在功能区中单击“创建站点系统服务器”。   

2. 在“创建站点系统服务器向导”的“常规”页面上，指定用于托管被动模式站点服务器的服务器。 在安装被动模式下的站点服务器之前，所指定的服务器无法承载任何站点系统角色。  

3. 在“系统角色选择”页上，仅选择“被动模式下的站点服务器”。  

    > [!Note]  
    > 该向导在此页面上执行以下初始必备项检查：  
    > - 所选服务器不是辅助站点服务器
    > - 所选服务器并不是被动模式下的站点服务器
    > - 该站点的内容库位于远程位置  
    >  
    > 如果这些初始必备项检查失败，则无法继续完成此向导页面。  

4. 请在“被动模式下的站点服务器”页面上，提供用于在指定服务器上运行安装程序并安装站点服务器角色的以下信息：

     - 选择下列选项之一：  

         - **通过网络从主动模式下的站点服务器复制安装源文件**：此选项创建压缩包并将其发送到新的站点服务器。  

         - **在处于被动模式的站点服务器上的以下位置使用源文件**：例如，已将源文件复制到的本地路径。 确保此内容与主动模式下的站点服务器中的相同。  

         - （推荐）**使用以下网络位置中的源文件**：从主动模式下的站点服务器直接指定 CD.Latest 文件夹内容的路径。 例如，`\\Server\SMS_ABC\CD.Latest` 中，“Server”是主动模式站点服务器的名称，“ABC”是站点代码。  

     - 指定在新站点服务器上安装 Configuration Manager 的本地路径。 例如：`C:\Program Files\Configuration Manager`  

5. 完成向导。 然后，Configuration Manager 在指定服务器上安装被动模式站点服务器。

有关详细的安装状态，请在控制台中转到“监视”工作区，然后选择“站点服务器状态”节点。 被动模式下的站点服务器状态将显示为“正在安装”。 有关更多详细信息，请选择服务器并单击“显示状态”。 此操作将打开“站点服务器安装状态”窗口。 完成此过程后，针对这两个服务器，状态都将显示“确定”。   

有关安装过程的详细信息，请参阅[流程图 - 设置被动模式下的站点服务器](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)。

添加被动模式下的站点服务器之后，请在控制台“站点”节点的“节点”选项卡上查看这两个站点服务器。 

所有 Configuration Manager 站点服务器组件在被动模式下的站点服务器上都处于待机状态。 Windows 服务仍在运行。



## <a name="site-server-promotion"></a>站点服务器提升  

与备份和恢复类似，请规划并实施流程，以更改站点服务器。 在提升规划中请考虑以下几点：  

- 实施已规划的提升（其中两个站点服务器处于联机状态）。 此外，还可以通过强制断开或关闭主动模式下的站点服务器来实施未规划的故障转移。  

- 确定故障转移期间的操作流程以及与其他 Configuration Manager 管理员进行通信的内容。  

- 在执行规划的提升之前：  

    - 检查站点和站点组件的总体状态。 确保环境中一切正常运行。  

    - 检查在站点之间进行主动复制的任何包的内容状态。  

    - 不要启动任何新的内容分发作业。 

        > [!Note]  
        > 如果在故障转移期间正在站点之间复制文件，则新站点服务器可能无法接收复制的文件。 如果发生这种情况，请在新站点服务器处于主动模式后重新分发软件内容。<!--515436-->  


### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>将被动模式下的站点服务器提升到主动模式的流程

本节介绍如何将被动模式下的站点服务器更改为主动模式。 若要访问该站点并执行此更改，你需要能够访问 SMS 提供程序的实例。 有关更多信息，请参阅[使用多个 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_MultiSMSProv)。  

> [!Important]  
> 默认情况下，只有原始站点服务器具有 SMS 提供程序角色。 如果此服务器处于脱机状态，则无法连接到该站点，因为没有可用的提供程序。 添加被动模式下的站点服务器时，不会自动添加 SMS 提供程序。 为站点添加至少一个其他 SMS 提供程序角色，以获得高可用性服务。  

> [!Tip]  
> Configuration Manager 控制台从站点服务器上的 WMI 请求可用 SMS 提供程序列表。 在站点上安装多个 SMS 提供程序时，站点会随机分配每个新连接请求以使用安装的 SMS 提供程序。 你无法指定要用于特定连接会话的 SMS 提供程序位置。 如果控制台因当前站点服务器处于脱机状态而无法连接到站点，请在“站点连接”窗口中指定其他站点服务器。  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。 选择站点，然后切换到“节点”选项卡。选择被动模式下的站点服务器，然后在功能区中单击“提升为主动”。 单击“是”，确认并继续。   
  
2. 刷新控制台节点。 正在提升的服务器的“状态”列在“节点”选项卡中显示为“正在提升”。  

3. 提升完成后，对于新的主动模式站点服务器和新的被动模式站点服务器，“状态”列都将显示“确定”。 站点的“服务器名称”列现在显示新的主动模式站点服务器的名称。

有关详细状态，请转到“监视”工作区，然后选择“站点服务器状态”节点。 “模式”列将标识哪个服务器为主动或被动。 将服务器从被动模式提升到主动模式时，选择要提升为主动模式的站点服务器，然后从功能区选择“显示状态”。 此操作将会打开“站点服务器提升状态”窗口，其中显示有关该流程的其他详细信息。

当主动模式下的站点服务器切换为被动模式时，仅站点系统角色会成为被动模式。 在该计算机上安装的所有其他站点系统角色则保持主动状态，并可供客户端访问。

有关“规划的”提升流程的详细信息，请参阅[流程图 - 提升站点服务器（规划）](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)。


### <a name="unplanned-failover"></a>未计划的故障转移

如果当前的主动模式站点服务器处于脱机状态，则要进行提升的站点服务器会尝试联系当前的主动模式站点服务器（需要 30 分钟）。 如果脱机服务器在此时间之前恢复，它会成功收到通知，并且更改会正常进行。 否则，要进行提升的站点服务器会强制更新站点配置以更改为主动状态。 如果脱机服务器在此时间之后恢复，它首先会检查站点数据库中的当前状态。 然后，继续降级为被动模式下的站点服务器。

在此 30 分钟的等待期间，该站点没有主动模式下的站点服务器。 客户端仍然与面向客户端的角色（例如管理点、软件更新点和分发点）进行通信。 用户可以安装已部署的软件。 在此期间无法进行站点管理。 有关详细信息，请参阅[站点失败影响](/sccm/core/servers/manage/site-failure-impacts)。  

如果脱机服务器已损坏而无法返回，请从控制台中删除此站点服务器。 然后创建新的被动模式站点服务器，以还原高可用性服务。 

有关“未规划”的故障转移流程的详细信息，请参阅[流程图 - 提升站点服务器（未规划）](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)。


### <a name="additional-tasks-after-site-server-promotion"></a>站点服务器提升后的其他任务  

切换站点服务器后，无需执行[恢复站点](/sccm/core/servers/manage/recover-sites#post-recovery-tasks)时所需的大多数其他任务。 例如，无需重置密码或重新连接 Microsoft Intune 订阅。

如有必要，在环境中可能需要执行以下步骤：  

- 如果为分发点导入 PKI 证书，请为受影响的服务器重新导入证书。 有关更多信息，请参阅[为分发点重新生成证书](/sccm/core/servers/manage/recover-sites#regenerate-the-certificates-for-distribution-points)。  

- 如果将 Confguration Manager 与适用于企业的 Microsoft 应用商店集成，请重新配置该连接。 有关详细信息，请参阅[管理来自适用于企业的 Microsoft 应用商店的应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)。  



## <a name="daily-monitoring"></a>每日监视

如果有被动模式下的站点服务器，请每天进行监视。 确保其状态为“确定”，且随时可供使用。 在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“站点服务器状态”节点。 查看这两个站点服务器及其当前状态。 此外，还应在“管理”工作区中查看状态。 展开“站点配置”，然后选择“站点”节点。 选择站点，然后切换到“节点”选项卡。 
