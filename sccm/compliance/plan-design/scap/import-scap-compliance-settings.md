---
title: 导入 SCAP 符合性设置
titleSuffix: Configuraton Manager
description: 导入 SCAP 符合性设置作为配置基线并导出结果
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 1f6b1fa0dd0775083eff9925a65509083b3f47d3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="import-the-compliance-settings-compliant-cab-files-into-system-center-configuration-manager"></a>将符合性设置符合 .cab 文件导入 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

> [!Tip]  
> 此功能在 Technical Preview 1803 版中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 SCAP 扩展的此预发行版本可以安装在当前支持的任何 Configuration Manager Current Branch 和 LTSB 1606 版本上。 从 1803 Technical Preview 开始，安装文件位于 cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi 中。 

该过程的下一步是使用 Configuration Manager 控制台将符合性设置符合 .cab 文件导入 Configuration Manager。 导入此过程中早些时候创建的 .cab 文件后，将在 Configuration Manager 数据库中创建一个或多个配置项目和配置基线。 此过程后期，你可将每个配置基线分配给 Configuration Manager 中的计算机集合。

## <a name="to-import-the-compliance-settings-compliant-cab-files-into-configuration-manager"></a>将符合性设置符合 .cab 文件导入 Configuration Manager

1. 打开 **Configuration Manager 控制台**。
2. 在 **Configuration Manager 控制台的导航窗格中，转到“资产和符合性”> “符合性设置” > “配置基线”。

3. 在操作窗格中，单击“导入配置数据”以启动“导入配置数据向导”。

1. 使用下表中的信息并接受默认值（除非另有指定）来完成“导入配置数据向导”。



“导入配置数据向导”过程

| 向导页名称 | 用户操作 |
| --- | --- |
| **选择文件** |1.单击“添加” 。 </br>出现“打开”对话框。|
||2.在“打开”对话框中，转到 **&lt;compliant cab output\_folder &gt;**。 单击 **&lt; compliant\_cab&gt;**.cab 文件，其中 _compliant cab **output\_folder** 是运行 Sces.ScapToDcm.exe 工具时在 –output 开关后面指定的文件夹。 **compliant\_file** 是此过程中早些时候创建的 .cab 文件的名称。 然后，单击“打开”。 </br> Configuration Manager 控制台 – 出现“安全警告”对话框。|
||3.在“Configuration Manager 控制台 - 安全警告”对话框中，单击“运行”。 在“选择文件”页上，要导入的基线列表中出现配置数据。|
||3.单击“下一步” 。|
| **摘要** |5.单击“下一步” 。 |
| **完成“导入配置数据向导”** |6.单击“关闭” 。 |

新的配置基线将显示在 Configuration Manager 控制台的信息窗格中。

>[!IMPORTANT]
> 你需要为此过程中早些时候创建的每个 .cab 文件重复此过程。 从 NVD 网站下载的 XCCDF/DataStream XML 文件中的每个所选配置文件均有一个 .cab 文件，此文件可通过运行 Microsoft.Sces.ScapToDcm.exe 工具进行处理。

导入的配置基线为只读，状态为“已启用”且初始部署状态为“否”。  “修改日期”属性指示导入基线的时间。  配置基线的名称来自 XCCDF/Datastream XML 的显示名称部分。 该名称使用以下约定构造而成：

ABC[XYZ]，其中 ABC 是 XCCDF 基准 ID，而 XYZ 是 XCCDF 配置文件 ID（如果选择了配置文件）。



## <a name="assign-configuration-baselines-to-the-computer-collections"></a>将配置基线分配到计算机集合

为要评估 SCAP 符合性的计算机创建合适的计算机集合后，即可分配所导入的配置基线来关联计算机集合。 此部分为你提供使用 Configuration Manager 控制台将配置基线分配给计算机集合的信息。

若要将配置基线分配到计算机集合，请执行以下操作：

1. 打开 **Configuration Manager** **控制台**。

2. 在 **Configuration Manager 控制台的导航窗格中，转到“资产和符合性” > “符合性设置” >“配置基线”****。
3. 在导航窗格中，单击 &lt; **configuration\_baseline>，其中 &lt;_configuration\_baseline&gt;_ 是要分配给计算机集合的配置基线的名称。

    配置基线的配置项目列表显示在 Configuration Manager 的信息窗格中。

4. 在“操作”窗格中，单击“部署”。 

5. 使用下表中的信息并接受默认值（除非另有指定）来完成“部署配置基线对话框”。

### <a name="deploy-configuration-baseline-dialog-process"></a>“部署配置基线对话框”过程

| 向导页名称 | 用户操作 |
| --- | --- |
| **选择集合** | 1.单击“浏览” 。|
||2.在“选择集合”对话框中，选择“设备集合”。 然后单击 **&lt;computer\_collection&gt;**，其中 &lt;_computer\_collection&gt;_ 是此过程中早些时候创建的计算机集合的名称。 单击" **确定**"。|
| **设置计划** |3.选择适合你的组织的日程安排。|
 
>[!IMPORTANT]
> 为每个要分配给每个配置基线的计算机集合重复此过程。 至少将每个配置基线分配给至少一个计算机集合。

## <a name="verify-that-the-compliance-data-has-been-collected"></a>确保已收集符合性数据

将符合性数据导出回到 SCAP 格式前，你需要验证数据已收集。 将配置基线分配给计算机集合后，集合中每台计算机上的 Configuration Manager 客户端将自动收集符合性信息。 并将符合性信息储存在 Configuration Manager 数据库中。

查看 Configuration Manager 中配置基线部署的状态以确保 Configuration Manager 客户端已收集适当的数据。 务必确保 Configuration Manager 中已收集适当的符合性数据，因为这可帮助验证你在此过程晚些时候创建的 XCCDF/DataStream 结果文件。



### <a name="verify-that-the-compliance-data-has-been-collected"></a>验证符合性数据已收集

1. 请打开 Configuration Manager 控制台。
2. 在 Configuration Manager 控制台的导航窗格中，转到“监视” > “部署”。
3. 单击“功能类型”对部署类型排序，并找到列表中类型为“基线”的项。
4. 右键单击列表中刚部署到集合的 &lt;configuration\_baseline&gt;，单击“查看状态”。
5. 然后移动到 &lt;configuration\_baseline&gt; 节点查看符合性状态，如果有计算机处于未知状态，则意味着仍未对此计算机完成符合性数据收集。

### <a name="validate-the-xccdfdatastream-results"></a>验证 XCCDF/Datastream 结果

1. 打开 Configuration Manager 控制台。
2. 在 Configuration Manager 控制台的导航窗格中，转到“符合性设置” > “SCAP 仪表板”。
3. 选择“配置基线”、“分配”、“SCAP 文件”、“数据流”、“基准”和“配置文件”（如果适用）。
4. 单击“显示报告”
 “SCAP 报告”![](./media/scap-report.png)



## <a name="export-compliance-results-to-scap-format"></a>将符合性结果导出为 SCAP 格式

此过程的下一个任务是将符合性设置符合性数据导出为 SCAP 格式，这是 XML/用户可读格式的 ARF 报告文件。 SCAP 扩展导出向导和 Microsoft.Sces.DcmToScap.exe 工具为每个符合性设置配置基线导出单独的 XCCDF/DataStream ARF 结果文件。 这些文件对应于 Microsoft.Sces.ScapToDcm.exe 工具用于创建每个符合性设置配置基线的每个 XCCDF/DataStream 输入文件。

### <a name="export-the-compliance-settings-compliance-data-using-the-export-scap-report-wizard"></a>使用“导出 SCAP 报告向导”导出符合性设置符合性数据

1. 从 SCAP 仪表板的右击菜单中启动“导出 SCAP 报告向导”。
![从 SCAP 仪表板导入](./media/import-from-scap-dashboard.png)

2. 选择“配置基线”和“分配” ![选择基线](./media/select-ci-baseline.png)

3. 选择 SCAP 数据流文件、XCCDF/CPE 文件或 Oval 内容和变量文件的位置。
![选择数据流](./media/export-scap-report-datastream.png)

4. 指定组织名称，并选择文件夹位置以导出 SCAP 报告。
 ![选择数据流](./media/specify-org-export.png)

5. 确认设置。
 ![选择数据流](./media/confirm-export.png)

6. 选择“下一步”导出报告。  你会看到一个进度栏，然后看到一个完成页面。
 ![完成导出](./media/complete-report-export.png)



### <a name="alternate-method-export-the-compliance-settings-compliance-data-using-the-microsoftscesdcmtoscapexe-tool"></a>（备选方法）使用 Microsoft.Sces.DcmToScap.exe 工具导出符合性设置符合性数据

1. 在命令提示符下，转到 AdminConsole\Bin 文件夹，键入下表中列出的命令行参数，然后按 Enter：

    >[!NOTE] 
    >你的帐户必须对 Configuration Manager 提供程序具有读取权限，同时必须对命令行 –out 参数中指定的 out 文件夹具有写入权限。

**对于 SCAP 1.0/1.1 内容（例如 USGCB 和 DISA 内容）：**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt;  -select &lt;xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt;  [-log logFileName]

  >[!NOTE] 
    >如果内容中有多个基准/配置文件，则应使用 –select 参数来指定客户端上已评估的基准/配置文件。

**对于 SCAP1.2 内容（例如最新的 USGCB 内容）：**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID  -select &lt;datastream/xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt;  [-log logFileName]

   >[!NOTE] 
   >如果内容中有多个数据流/基准/配置文件，则应使用 –select 参数来指定客户端上已评估的数据流/基准/配置文件。

**对于带外部变量的单个 OVAL 文件：**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;]  -out &lt;outputResultFolder&gt;  [-log logFileName]

   >[!NOTE] 
    >Microsoft.Sces.DcmToScap.exe 将为每个目标计算机仅生成 OVAL 定义结果报告，而不会生成 ARF 报告。

#### <a name="how-to-get-baseline-ci-id-and-assignment-id"></a>如何获取基线 CI ID 和分配 ID

在管理控制台中，转到“资产和符合性” > “符合性设置” > “配置基线”。 CI ID 是指配置基线 CI ID。

![获取 CI ID 和分配 ID](./media/get-to-baselines.png)

选择所需的配置基线，单击“部署”选项卡，如果其中未显示分配 ID，则右键单击列标题，单击“分配 ID”启用它。
![获取 CI ID 和分配 ID](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Microsoft.Sces.DcmToScap.exe 命令行参数

| **参数** | **用法** | **必需** |
| --- | --- | --- |
| -baseline [Baseline CI ID] | 指定配置基线 | 是 |
| -assignment [Assignment ID] | 指定配置基线部署 | 是 |
| -organization [组织名称] | 指定组织名称，此名称将显示在报告中。 可通过“;”将其分隔以指定多行组织名称。 | 否 |
| -type [精简/完整/fullnosc] | 指定 OVAL 结果类型：精简结果、完整结果或没有系统特征的完整结果。 | 否（如果未指定，则默认值是完整） |
| -scap [scap 数据流文件] | 指定 SCAP 数据流文件 | 是（对于 SCAP 1.2 数据流，分别与 –xccdf 和 –oval/-variable 互斥） |
| -xccdf [xccdf 文件] | 指定 XCCDF 文件 | 是（对于 SCAP 1.0/1.1 XCCDF，分别与 –scap 和 –oval/-variable 互斥） |
| -cpe [cpe file] | 指定 CPE 文件 | 是（对于 SCAP 1.0/1.1 XCCDF，分别与 –scap 和 –oval/-variable 互斥） |
| -oval [oval 文件] | 指定 OVAL 文件 | 是（对于独立 OVAL 文件，分别与 –xccdf 和 -scap 互斥） |
| -variable [oval 外部变量文件] | 指定 OVAL 外部变量文件 | 否（如果有外部 OVAL 变量文件，则对于独立 OVAL 文件可选，分别与 –xccdf 和 -scap 互斥） |
| -select [xccdf benchmark/profile] | 从 SCAP 数据流或 XCCDF 文件选择 XCCDF 基准、配置文件 | 是（必须做出选择以生成报告，以便在 Configuration Manager 数据库中匹配相应的 DCM 基线） |
| -out [输出目录] | 指定符合性设置 cab 文件的输出位置 | 否（如果未指定，则此工具仅列出内容而不转换） |
| -log [日志文件] | 指定日志文件 | 否（如果未指定，则将日志写入 Microsoft.Sces.DcmToScap.log 文件） |
| -help / -? | 打印输出工具使用情况 | 否 |



 >[!TIP] 
 >你可指定 -? –h 或 –help 参数以显示 Microsoft.Sces.DcmToScap.exe 工具的语法和参数列表。

默认情况下，Microsoft.Sces.DcmToScap.exe 工具使用你的凭据访问 Configuration Manager 数据库。 Microsoft.Sces.DcmToScap.exe 工具至少需要对 Configuration Manager 数据库具有读取权限。

确保存在合适的 **ARF** 报告：_ARF\_xxxx.xml_ 和/或**用户可读的**报告：xxx.txt、**Cyberscope** 报告：LASR\_xxx.xml、**ConsumedOval** 报告：xx-oval-&lt;machineName&gt;.xml、**XCCDF 基准结果**报告：xccdf\_xxx.xml 文件之后，在命令行上，键入“exit”，然后按 **Enter** 退出命令提示符。

## <a name="next-step"></a>下一步
> [!div class="nextstepaction"]
> [故障排除](/sccm/compliance/plan-design/scap/troubleshooting-scap)
