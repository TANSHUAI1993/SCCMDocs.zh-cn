---
title: "Technical Preview 1705 | Microsoft 文档"
description: "了解在 System Center Configuration Manager 的 Technical Preview 1705 中的可用功能。"
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b977a79baec73999caa21648adcb6fcfec4a4935
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1705-for-system-center-configuration-manager"></a>在 System Center Configuration Manager 的 Technical Preview 1705 中的功能

*适用范围：System Center Configuration Manager（Technical Preview）*

本文介绍了在 System Center Configuration Manager 的 Technical Preview 1705 中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此 Technical Preview 前，请查看 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，熟悉使用 Technical Preview 的常规要求和限制，如何在两版本之间进行更新，以及如何对 Technical Preview 中的有关功能提供反馈。    

**此 Technical Preview 中的已知问题：**
-   **Operations Manager 套件连接器不升级**。 从配置了 OMS 连接器的 Technical Preview 之前版本升级时，该连接器不会升级且在控制台中变得不再可用。 在升级后，必须[使用 Azure 服务向导](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms)并重新建立到 OMS 工作区的连接。
-   **Surface 驱动程序无法成功同步**。 即使支持 Technical Preview 的 Configuration Manager 控制台“新增功能”中所列的 Surface 驱动程序，此功能也无法按预期方式工作。
-   **无法创建 Windows Update for Business 延迟策略**。 即使在 Technical Preview 的 Configuration Manager 控制台“新增功能”中列出了配置 Windows Update for Business 延迟策略的功能，向导也不会打开，且无法配置任何策略。


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**以下是可以试用的此版本的新功能。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>更新重置工具  
在控制台内更新出现下载或复制问题时，可以使用 Configuration Manager 更新重置工具 CMUpdateReset.exe 修复这些问题。 Technical Preview 1705 中提供了此工具。 在 \cd.latest\SMSSETUP\TOOLS 文件夹中安装预览版后，可以在 Technical Preview 站点的站点服务器上找到此工具。

你可以在 Technical Preview 1606 或更高版本中使用此工具。 此工具提供向后支持，因此，它可与一系列 Technical Preview 的更新方案一起使用，而无需等到推出下一个 Technical Preview。

控制台内更新尚未安装且处于失败状态时，可以使用此工具。 失败状态可能意味着更新下载仍在进行，但处于停滞状态，且花费了相当长的时间，与类似大小的更新包所花费的历史预期时间相比，可能还要长数小时。 另外，也可能是无法将更新复制到子主站点。  

运行此工具时，它会基于你指定的更新运行。 默认情况下，该工具不会删除已成功安装或下载的更新。  

### <a name="prerequisites"></a>先决条件
用于运行此工具的帐户需要具有以下权限：
-   对管理中心站点和层次结构中每个主站点的站点数据库的“读取”和“写入”权限。 若要设置这些权限，可以将用户帐户添加为每个站点的 Configuration Manager 数据库上 db_datawriter 和 db_datareader[固定数据库角色](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles)的成员。 该工具不与辅助站点进行交互。
-   在层次结构的顶层站点上为“本地管理员”。
-   在托管服务连接点的计算机上为“本地管理员”。

需要你希望进行重置的更新包的 GUID。 要获取 GUID，请执行以下操作：
-   在控制台中，转到“管理” > “更新和服务”，然后在显示窗格中，右键单击某一列的标题（如“状态”），然后选择“包 GUID”。 这会将该列添加到显示中，并且该列会显示更新包 GUID。

> [!TIP]  
> 若要复制此 GUID，请选择想要重置的更新包的行，然后使用 CTRL+C 复制该行。 如果将复制的选定内容粘贴到文本编辑器，则可以在运行该工具时仅复制 GUID 用作命令行参数。

### <a name="run-the-tool"></a>运行该工具    
该工具必须在层次结构的顶层站点上运行。

在运行该工具时，使用命令行参数来指定层次结构的顶层站点的 SQL Server、站点数据库名称以及想要重置的更新包的 GUID。 然后，该工具根据更新状态确定它需要访问的其他服务器。   

如果更新包处于下载后状态，则该工具不会清理此包。 或者，也可以使用强制删除参数强制删除已成功下载的更新（请参阅本主题后续介绍的命令行参数）。

运行该工具后：
-   如果包被删除，请重启顶层站点 SMS_Executive 服务，然后再次检查更新以下载此包。
-   如果包未被删除，则无需执行任何操作，因为此更新将重新初始化并重新开始复制或安装。

**命令行参数：**  

| 参数        |描述                 |  
|------------------|----------------------------|  
|**-S &lt;顶层站点的 SQL Server 的 FQDN>** | *必需* <br> 必须指定为层次结构的顶层站点托管站点数据库的 SQL Server 的 FQDN。    |  
| **-D &lt;数据库名称>**                        | *必需* <br> 必须指定顶层站点数据库的名称。  |  
| **-P &lt;包 GUID>**                         | *必需* <br> 必须指定想要重置的更新包的 GUID。   |  
| **-I &lt;SQL Server 实例名称>**             | *可选* <br> 使用此参数确定托管站点数据库的 SQL Server 的实例。 |
| **-FDELETE**                              | *可选* <br> 使用此参数强制删除已成功下载的更新包。 |  
 **示例：**  
 在一个典型方案中，你想要重置具有下载问题的更新。 SQL Server FQDN 是 server1.fabrikam.com，站点数据库是 CM_XYZ，包 GUID 是 61F16B3C-F1F6-4F9F-8647-2A524B0C802C。  可以运行：CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C

 在比较极端的情形下，你希望强制删除存在问题的更新包。 SQL Server FQDN 是 server1.fabrikam.com，站点数据库是 CM_XYZ，包 GUID 是 61F16B3C-F1F6-4F9F-8647-2A524B0C802C。  可以运行：CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C

### <a name="test-the-tool-with-the-technical-preview"></a>使用 Technical Preview 测试此工具  
你可以在 Technical Preview 1606 或更高版本中使用此工具。 此工具提供向后支持，因此，它可与很多 Technical Preview 的更新方案一起使用，而无需等到推出下一个 Technical Preview。

在更新完成其先决条件检查之前，在 Technical Preview 的更新包上运行该工具。 在“管理” > “更新和维护服务”中，通过包的以下状态之一来确定已完成的先决条件检查状态：  
-   **已通过先决条件检查**
-   **已通过先决条件检查，但有警告**
-   **先决条件检查失败**


## <a name="high-dpi-console-support"></a>高 DPI 控制台支持

使用此版本，应能修复在高 DPI 设备（如 Surface Book）上进行查看时，Configuration Manager 控制台如何缩放和显示 UI 不同部分的问题。


## <a name="peer-cache-improvements"></a>对等缓存功能改进
从该 Technical Preview 开始，对等缓存功能[不再使用网络访问帐户](/sccm/core/plan-design/hierarchy/client-peer-cache)来验证对等项的下载请求。


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性组改进  
借助此版本，现在可以在与 Configuration Manager 配合使用的 SQL Server AlwaysOn 可用性组中使用异步提交副本。  这意味着，你可以将其他副本添加到可用性组，用作场外（远程）备份，然后在灾难恢复方案中使用它们。  

-   Configuration Manager 支持使用异步提交副本来恢复同步副本。  请参阅备份和恢复主题中的[站点数据库恢复选项](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption)，了解有关如何实现此操作的信息。

-   此版本不支持故障转移后使用异步提交副本作为站点数据库。
> [!CAUTION]  
> 由于 Configuration Manager 不会验证异步提交副本的状态来确认它是否为最新，而[此类副本设计可以为不同步](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes)，因此，使用异步提交副本作为站点数据库可能会危及站点和数据的完整性。  

-   可以在可用性组中使用与所用 SQL Server 版本支持的数量和类型相同的副本。   （先前支持限制为两个同步提交副本。）

### <a name="configure-an-asynchronous-commit-replica"></a>配置异步提交副本
若要将异步副本添加到[与 Configuration Manager 配合使用的可用性组](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)，则不需要运行配置同步副本所需的配置脚本。 （这是因为不支持将该异步副本用作站点数据库。）请参阅 [SQL Server 文档](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot))，了解有关如何将辅助副本添加到可用性组的信息。

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>使用异步副本恢复站点
使用异步副本恢复站点数据库之前，必须停止活动主站点，防止到站点数据库的其他写入。 停止站点后，可以使用异步副本替代[手动恢复的数据库](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption)。

若要停止该站点，可以使用[层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)来停止站点服务器上的密钥服务。 使用命令行：Preinst.exe /stopsite   

停止站点相当于停止站点服务器上后跟 SMS_Executive 服务的站点组件管理器服务 (sitecomp)。

> [!TIP]  
> 如果使用主被动副本（作为[站点服务器角色高可用性](#site-server-role-high-availability)引入此 Technical Preview），则无需停止被动副本。 只需停止活动主站点。



## <a name="improved-user-notifications-for-office-365-updates"></a>改进了 Office 365 更新的用户通知
已进行了改进，在客户端安装 Office 365 更新时利用 Office 即点即用用户体验。 这包括弹出通知、应用内通知以及倒计时体验。 在此版本之前，在向客户端发送 Office 365 更新时，之前打开的 Office 应用程序会自动关闭而不发出警告。 此更新后，Office 应用程序将不会再意外关闭。

### <a name="prerequisites"></a>先决条件
此更新适用于 Office 365 ProPlus 客户端。

### <a name="known-issues"></a>已知问题
如果客户端是首次评估 Office 365 更新分配，且更新具有在过去计划的截止时间、立即计划的截止时间或在 30 分钟内计划的截止时间，Office 365 用户体验可能会不一致。 例如，客户端可能会收到用于更新的一个 30 分钟倒计时对话框，但实际的强制措施可能会在倒计时结束之前启动。 若要避免此行为，请考虑以下方面的内容：
- 部署具有截止时间的 Office 365 更新，该截止时间计划比当前时间提前超过 60 分钟。
- 配置非营业时间的收集维护时段或配置部署的实施宽限期。

### <a name="try-it-out"></a>试试看！
请尝试完成以下任务，然后从功能区的“主页”选项卡向我们发送“反馈”，让我们了解它的工作状况：
- 将客户端部署到具有以下截止时间的 Office 365 更新，该截止时间设置为比当前时间至少提前 60 分钟的时间。 观察客户端上的新行为。


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>配置和部署 Windows Defender 应用程序防护策略

[Windows Defender 应用程序防护](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)是一项新的 Windows 功能，通过在操作系统的其他部分无法访问的安全隔离容器中打开不受信任的网站来帮助保护用户安全。 在此 Technical Preview 版中，我们使用在配置后部署到集合的 Configuration Manager 符合性设置增加了对配置此功能的支持。
此功能将在 64 位版本的 Windows 10 创意者更新预览版 (codename: RS2) 中发布。 现在，若要测试此功能，必须使用此更新的预览版本。


### <a name="before-you-start"></a>开始之前

若要创建和部署 Windows Defender 应用程序防护策略，必须使用网络隔离策略配置要部署此策略的 Windows 10 设备。 有关更多详细信息，请参阅稍后引用的博客文章。
此功能仅适用于当前的 Windows 10 预览体验成员版本。 若要对其进行测试，客户端必须运行最新的 Windows 10 预览体验成员版本。

### <a name="try-it-out"></a>试试看！

请务必阅读博客文章，以便了解有关 Windows Defender 应用程序防护的基础知识。

若要创建策略，并浏览可用设置，请执行以下操作：

1.  在 Configuration Manager 控制台中，选择“资产和符合性”。
2.  在“资产和符合性”工作区中，选择“概述” > “终结点保护” > “Windows Defender 应用程序防护”。
3.  在“主页”选项卡的“创建”组中，单击“创建 Windows Defender 应用程序防护策略”。
4.  将此博客文章用作参考，可以浏览和配置可用的设置来试用此功能。
5.  结束后，完成向导操作，并将策略部署到一个或多个 Windows 10 设备。

### <a name="further-reading"></a>延伸阅读

若要了解有关 Windows Defender 应用程序防护的详细信息，请参阅[这篇博客文章]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。
此外，若要详细了解 Windows Defender 应用程序防护独立模式，请参阅[这篇博客文章](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)。




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Azure AD 和云管理的新功能

在此版本中，可以配置云服务以使用 Azure AD 来支持以下方案：

- 从 Internet 手动安装 Configuration Manager 客户端，并将其分配到 Configuration Manager 站点。
- 使用 Intune 将 Configuration Manager 客户端部署到 Internet 上的设备。

### <a name="advantages"></a>优点

使用云服务和 Azure AD，而无需再使用客户端身份验证证书。

可以在站点中发现 Azure AD 用户，从而在集合和其他 Configuration Manager 操作中使用。

### <a name="before-you-start"></a>开始之前

- 必须具有 Azure AD 租户。
- 设备必须运行 Windows 10，并加入 Azure AD。  除加入 Azure AD 外，客户端还可以加入域。
- 除了管理点站点系统角色的[现有先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)外，还必须确保 ASP.NET 4.5（和随此项自动选择的任何其他选项）在托管此站点系统角色的计算机上启用。
- 若要使用 Microsoft Intune 部署 Configuration Manager 客户端，请按照以下步骤操作：
    - 必须具有有效的 Intune 租户（不需要连接 Configuration Manager 和 Intune）。
    - 在 Intune 中，创建并部署包含 Configuration Manager 客户端的应用。 有关如何执行此操作的详细信息，请参阅“如何将客户端安装到 Intune MDM 托管的 Windows 设备”。
- 若要使用 Configuration Manager 部署客户端，请按照以下步骤操作：
    - 必须至少为 HTTPS 模式配置一个管理点。
    - 必须设置云管理网关。


### <a name="set-up-the-cloud-management-gateway"></a>设置云管理网关

设置云管理网关，以让客户端从 Internet 访问 Configuration Manager 站点，而无需使用证书。

可以在以下主题中找到有关如何执行此操作的帮助：

- [在 Configuration Manager 中规划云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)。
- [为 Configuration Manager 设置云管理网关](/sccm/core/clients/manage/setup-cloud-management-gateway)。
- [在 Configuration Manager 中监视云管理网关](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)。

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>在 Configuration Manager 云服务中设置 Azure 服务应用

这会将 Configuration Manager 站点连接到 Azure AD，这也是本节中所有其他操作的先决条件。 要执行此操作：

1.  在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后单击“Azure 服务”。
2.  在“主页”选项卡上的“Azure 服务”组中，单击“配置 Azure 服务”。
3.  在 Azure 服务向导的“Azure 服务”页上，选择“云管理”以允许客户端使用 Azure AD 对层次结构进行身份验证。
4.  在向导的“常规”页上，指定一个名称和 Azure 服务的说明。
5.  在向导的“应用”页上，从列表中选择 Azure 环境，然后单击“浏览”以选择将用于配置 Azure 服务的服务器和客户端应用：
    - 在“服务器应用”窗口中，选择要使用的服务器应用，然后单击“确定”。 服务器应用是包含 Azure 帐户配置的 Azure Web 应用，包括客户端的租户 ID、客户端 ID 和密钥。 如果没有可用的服务器应用，请使用以下操作之一：
        - **创建**：若要创建新的服务器应用，请单击“创建”。 为应用和租户提供友好名称。 然后，登录 Azure 后，Configuration Manager 将在 Azure 中为用户创建 Web 应用，包括用于 Web 应用的客户端 ID 和密钥。 之后，可在 Azure 门户中查看这些内容。
        - **导入**：若要使用 Azure 订阅中已存在的 Web 应用，请单击“导入”。 为应用和租户提供友好名称，然后为 Configuration Manager 要使用的 Azure Web 应用指定租户 ID、客户端 ID 和密钥。 验证此信息后，单击“确定”以继续。 此选项当前在此 Technical Preview 中不可用。
    - 为客户端应用重复相同的过程。

  在使用“应用程序导入”时，需要授予“读取目录数据”应用程序权限以在门户中设置正确的权限。 如果使用“应用程序创建”，则权限将自动随应用程序创建，但仍需要在 Azure 门户中同意该应用程序。
6.  在向导的“发现”页上，根据需要选择“启用 Azure Active Directory 用户发现”，然后单击“设置”。
在“Azure AD 用户发现设置”对话框中，配置出现发现的时间计划。 此外，还可以启用增量发现，用于仅查看 Azure AD 中新增或更改的帐户。
7.  完成向导。

此时，已将 Configuration Manager 站点连接到 Azure AD。


### <a name="install-the-cm-client-from-the-internet"></a>从 Internet 安装 CM 客户端

在开始之前，请确保客户端安装源文件已本地存储在用于安装此客户端的设备上。
然后，使用[如何将客户端部署到 System Center Configuration Manager 中的 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually)中的说明，使用以下安装命令行（将示例中的值替换为你自己的值）：

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=<GUID> AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck**：如果管理点或云管理网关使用非公共服务器证书，则客户端可能无法访问 CRL 位置。
- **/Source**：本地文件夹 - 客户端安装文件的位置。
- **CCMHOSTNAME**：Internet 管理点的名称。 可以通过从托管客户端的命令提示符处运行 gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate 找到此名称。
- **SMSMP**：查找管理点的名称，这可以是在 Intranet 上。
- **SMSSiteCode**：Configuration Manager 站点的站点代码。
- **AADTENANTID**、**AADTENANTNAME**：链接到 Configuration Manager 的 Azure AD 租户的 ID 和名称。 可以通过从加入 Azure AD 的设备上的命令提示符处运行 dsregcmd.exe /status 找到上述内容。
- **AADCLIENTAPPID**：Azure AD 客户端应用 ID。 有关查找此内容的帮助，请参阅[使用门户创建可访问资源的 Azure Active Directory 应用程序和服务主体](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)。
- **AADResourceUri**：载入的 Azure AD 服务器应用的标识符 URI。

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>使用 Azure 服务向导配置与 OMS 的连接
从 Technical Preview 1705 版本开始，可以使用 Azure 服务向导配置从 Configuration Manager 到 Operations Management Suite (OMS) 云服务的连接。 向导将替换以前的工作流，以配置此连接。

-   该向导用于配置适用于 Configuration Manager 的云服务，如 OMS、适用于企业的 Windows 应用商店 (WSfB) 和 Azure Active Directory (Azure AD)。  

-   Configuration Manager 连接到 OMS 以实现[日志分析](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)或[升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-analytics)等功能。

### <a name="prerequisites-for-the-oms-connector"></a>OMS 连接器的先决条件
配置与 OMS 的连接的先决条件与 [Current Branch 版本 1702 中记录的](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites)先决条件并无任何区别。 此处重复了该信息：  

-   向 OMS 提供 Configuration Manager 权限。

-   必须在托管[联机模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)下的[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)的计算机上安装 OMS 连接器。

-   必须为在服务连接点上安装的 OMS 安装 Microsoft Monitoring Agent 以及 OMS 连接器。 必须将代理和 OMS 连接器配置为使用相同的 **OMS 工作区**。 若要安装代理，请参阅 OMS 文档中的[下载并安装代理](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)。
-   安装连接器和代理后，必须配置 OMS 以使用 Configuration Manager 数据。 为此，请在 OMS 门户中[导入 Configuration Manager 集合](/azure/log-analytics/log-analytics-sccm#import-collections)。

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>使用 Azure 服务向导配置与 OMS 的连接

1.  在控制台中，转到“管理” > “概述” > “云服务” > “Azure 服务”，然后从功能区的“主页”选项卡上选择“配置 Azure 服务”，以启动“Azure 服务向导”。

2.  在“Azure 服务”页上，选择 Operation Management Suite 云服务。 提供“Azure 服务名称”的友好名称和可选说明，然后单击“下一步”。

3.  在“应用”页上，指定 Azure 环境（Technical Preview 仅支持公有云）。 然后，单击“浏览”以打开“服务器应用”窗口。

4.  选择 Web 应用：

    -   **导入**：若要使用 Azure 订阅中已存在的 Web 应用，请单击“导入”。 为应用和租户提供友好名称，然后为 Configuration Manager 要使用的 Azure Web 应用指定租户 ID、客户端 ID 和密钥。 “验证”信息后，单击“确定”以继续。   

    > [!NOTE]   
    > 在使用此预览配置 OMS 时，OMS 仅支持 Web 应用的导入功能。 不支持创建新的 Web 应用。 同样，无法为 OMS 重用现有的应用。

5.  如果已成功完成所有其他过程，则“OMS 连接配置”屏幕上的信息将自动显示在此页上。 应显示“Azure 订阅”、“Azure 资源组”和“Operations Management Suite 工作区”的连接设置的信息。

6.  向导使用输入的信息连接到 OMS 服务。 选择想要与 OMS 同步的设备集合，然后单击“添加”。

7.  在“摘要”屏幕上验证连接设置，然后选择“下一步”。 “进度”屏幕会显示连接状态，然后应显示“完成”。

8.  完成向导后，Configuration Manager 控制台会显示已将“Operation Management Suite”配置为“云服务类型”。
