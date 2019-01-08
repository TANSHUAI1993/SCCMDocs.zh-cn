---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager Technical Preview（版本 1801）中的可用功能。
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 135fc21cf122650e70eedf5e87873c93f08d4907
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417636"
---
# <a name="capabilities-in-technical-preview-1801-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1801 中的功能

适用范围：*System Center Configuration Manager (Technical Preview)*

本文介绍了适用于 System Center Configuration Manager 的 Technical Preview（版本 1801）中的可用功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 

在安装此版本的 Technical Preview 之前，请查看[适用于 System Center Configuration Manager 的 Technical Preview](/sccm/core/get-started/technical-preview)。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**此 Technical Preview 中的已知问题：**
- 如果站点服务器处于被动模式，则无法更新到新的预览版本。 如果具有[被动模式的主站点服务器](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)，那么在更新到此新的预览版本之前，必须卸载该被动模式站点服务器。 可以在站点完成更新后，重新安装被动模式站点服务器。

  若要卸载被动模式站点服务器，请执行以下操作：
  1. 在 Configuration Manager 控制台中，依次转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”，再选择被动模式站点服务器。
  2. 在“站点系统角色”窗格中，右键单击“站点服务器”角色，再选择“删除角色”。
  3. 右键单击被动模式站点服务器，再选择“删除”。
  4. 卸载站点服务器后，在处于主动模式的主站点服务器上重启服务 CONFIGURATION_MANAGER_UPDATE。
  <!--sms 489412-->


**以下是此版本可以试用的新功能。**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>创建分阶段部署
<!-- 1357405 --> 分阶段部署可自动协调有序地推出软件，无需创建多个部署。 在此 Technical Preview 版本中，可针对管理控制台中的任务序列完成分阶段部署向导。 但不创建部署。 

### <a name="try-it-out"></a>试试看！  
  尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。
 
**针对任务序列创建分阶段部署** </br>
1. 在“软件库”工作区中，展开“操作系统”，并选择“任务序列”。
2. 右键单击现有任务序列并选择“创建分阶段部署”。 
3. 在“常规”选项卡上，为分阶段部署提供名称、说明（可选），并选择“自动创建默认试点和生产阶段”。 
4. 填充“试点集合”和“生产集合”字段。 选择“下一步”。
5. 在“设置”选项卡上，为每个计划设置选择一个选项，然后在完成后选择“下一步”。 
6. 在“阶段”选项卡上，如果需要，可编辑其中任一阶段，然后单击“下一步”。
7. 在“摘要”选项卡上确认所选，然后单击“下一步”以继续操作。

## <a name="co-management-reporting"></a>共同管理报告
<!-- 1356648 --> 如果正在使用[共同管理](/sccm/core/clients/manage/co-management-overview)功能，现在可以在环境中查看具有联合管理相关信息的仪表板。 在 Configuration Manager 控制台中，导航至“监视”工作区，展开“升级就绪情况”，并选择“共同管理”仪表板。 该仪表板具有以下磁贴：
- **共同管理的设备**：环境中为进行共同管理而启用的设备的百分比
- **OS 分发**：按版本的操作系统 (OS) 细目。 此图表使用下列分组方式：
  - Windows 7 和 8.x
  - Windows 10 1709 以下版本
  - Windows 10 1709 及更高版本
    > [!NOTE] 
    > Windows 10 1709 及更高版本，是共同管理的先决条件
- **共同管理状态**：设备成功或失败分类细目如下：
   - 成功，已联接混合 Azure AD
   - 成功，已联接 Azure AD
   - 失败：自动注册失败
- **工作负荷转换**：一个条形图，显示为了三个可用工作负荷而转换为 Microsoft Intune 的设备数： 
   - 符合性策略
   - 资源访问
   - Windows Update for Business

### <a name="prerequisites"></a>先决条件
- 运行 Configuration Manager 控制台的计算机要求使用 Internet Explorer 9 或更高版本。



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>自动部署规则评估计划改进
<!-- 1357133 --> 根据[用户语音反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling)，现可计划自动部署规则 (ADR) 评估，从基准日计算偏移。 例如，当月第二个星期二后的两天偏移量意味着在星期四评估规则。 

### <a name="try-it-out"></a>试试看！  
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。 <br/>

**创建自定义计划进行评估，且 ADR 从基准日偏移** </br>
1.  在“软件库”工作区中，展开“软件更新”，并选择“自动部署规则”。
2. 右键单击“自动部署规则”并选择“创建自动部署规则”。 
3. 按照提示完成“常规”、“部署设置”和“软件更新”选项卡。 
4. 在“评估计划”选项卡上，选择“按计划运行规则”和“自定义”。
5. 对于自定义的计划，请选择“每月”并输入基准日（如第二个星期二）。 
6. 选中“偏移(天)”和偏移的天数，完成后选择“确定”。  
7. 完成“创建自动部署规则向导”的剩余部分。 



## <a name="reassign-distribution-point"></a>重新分配分发点
<!-- 1306937 --> 许多客户都有大型 Configuration Manager 基础结构，并且正要通过减少主站点或辅助站点来简化自己的环境。 他们仍需要在分支机构位置保留分发点，以向托管客户提供内容。 这些分发点通常包含多个 TB 或更多的内容。 将此内容分发到这些远程服务器所需的时间和网络带宽成本高昂。 

此功能允许向其他主站点重新分配分发点，而无需重新分发内容。 此操作可更新站点系统分配，同时在服务器上保留所有内容。 如果需要重新分配多个分发点，请首先对一个分发点执行此操作，然后在其他服务器上继续，一次只能操作一个服务器。

> [!IMPORTANT]
> 站点系统服务器只能承载分发点角色。 如果站点系统服务器承载其他 Configuration Manager 服务器角色，例如状态迁移点，则无法重新分配分发点。 无法重新分配云分发点。 

此选项对此版本不起作用，因为 Technical Preview 有单个主站点的限制。 请考虑此方案，然后从功能区的“主文件夹”选项卡发送有关此操作的功能的“反馈”。
1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“分发点”节点。
2. 右键单击目标分发点，然后选择“重新分配分发点”。 
  ![重新分配分发点](media/1306937-reassign-dp.png)
3. 选择想要向其重新分配分发点的站点服务器和站点代码。 
  ![选择站点服务器](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>硬件清单改进
<!-- 1357389 --> 对于新添加的类，可为非键的硬件清单属性指定长度大于 255 个字符的字符串。

### <a name="try-it-out"></a>试试看！  
尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。<br/>

1. 单击“管理”工作区中的“客户端设置”，突出显示客户端设备设置以便编辑，右键单击然后选择“属性”。 
2. 依次选择“硬件清单”、“设置类”和“添加”。
3. 单击“连接”按钮。
4. 填写“计算机名称”、“WMI 命名空间”，如有必要，选择“递归”。 如有必要，请提供凭据以连接。 单击“连接”以查看命名空间类。
5. 选择新类，然后单击“编辑”。
6. 至少将一个非键且为字符串的属性的长度更改为大于 255。 单击" **确定**"。 
7. 确保为“添加硬件清单类”选择编辑的属性，并单击“确定”。 
8. 使用新添加的类收集硬件清单，该类包含长度大于 255 个字符的属性。 



## <a name="improvements-to-client-settings-for-software-center"></a>软件中心的客户端设置改进
<!-- 1351224 & 1355146 --> 此版 Technical Preview 中，已对客户端设置下的软件中心自定义进行了改进。 

1. 软件中心的客户端设置现在包含“自定义”按钮。
2. 已添加预览，用于显示软件中心横幅的外观<!--1351224-->。
    - 如果未选择徽标，预览将显示公司名称文本和颜色。
    - 如果已选择徽标，预览将显示徽标和公司名称文本。  
3.  **在软件中心隐藏未批准的应用程序**是新的软件中心设置。 启用此选项后，软件中心会隐藏需要审批的用户可用的应用程序。<!--1355146-->

### <a name="try-it-out"></a>试试看！  
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

1. 在“管理”工作区中，单击“客户端设置”。 选择要编辑的客户端设备设置。 右键单击它并选择“属性”，然后选择“软件中心”。
2.  单击“自定义”按钮。 试用包括预览在内的其他自定义设置。
3. 启用设置“在软件中心隐藏未批准的应用程序”。 观察软件中心的更改。 



## <a name="new-settings-for-windows-defender-application-guard"></a>新的 Windows Defender 应用程序防护设置
<!-- 1356256 --> 对于安装 Windows 10 版本 1709 及更高版本的设备，新推出两个适用于 [Windows Defender 应用程序防护](/sccm/protect/deploy-use/create-deploy-application-guard-policy)的主机交互设置。 
1. 可向网站授予主机虚拟图形处理器的访问权限。 
2. 容器内已下载的文件可保存在主机上。 </br>



## <a name="improvements-to-run-scripts"></a>运行脚本的改进
<!-- 1236459 --> 现可借助[**运行脚本**功能](/sccm/apps/deploy-use/create-deploy-scripts)，导入和运行已分配的 PowerShell 脚本。 
- 为保持脚本完整性，必须导入分配的脚本，而非使用复制/粘贴。 
- 已分配的脚本导入后不能进行编辑。
    
>[!IMPORTANT]
>在此 Technical Preview 中，有两个临时限制。
>- 只能在“运行脚本”功能中导入脚本，且无法直接从控制台进行编辑。
>- 使用非 Unicode 编码导入的脚本可能无法在控制台中正确显示。 脚本仍然按照最初编写的方式的执行。





## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
