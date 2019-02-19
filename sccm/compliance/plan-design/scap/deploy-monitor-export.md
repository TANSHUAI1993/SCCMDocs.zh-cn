---
title: 部署和监视 SCAP 符合性
titleSuffix: Configuration Manager
description: 部署 SCAP 符合性设置作为配置基线、监视符合性并导出结果。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e3280edbe900e96cf97af8e59578ceab5322ee2a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137290"
---
# <a name="deploy-and-monitor-scap-compliance-in-configuration-manager"></a>在 Configuration Manager 中部署和监视 SCAP 符合性

适用范围：System Center Configuration Manager (Current Branch)

[转换并导入](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) SCAP 数据流文件后，请参阅以下后续步骤：  

- 将配置基线[部署](#bkmk_deploy)到集合，以评估设备的 SCAP 符合性  

- [监视](#bkmk_monitor)目标客户端返回的符合性数据  

- 将符合性结果[导出](#bkmk_export)为 SCAP 格式  



## <a name="bkmk_deploy"></a> 部署 SCAP 配置基线

首先，为要评估 SCAP 符合性的计算机创建设备集合。 有关详细信息，请参阅[创建集合](/sccm/core/clients/manage/collections/create-collections)。  

你已准备好部署要导入到这些设备集合中的配置基线。 有关详细信息，请参阅[如何部署配置基线](/sccm/compliance/deploy-use/deploy-configuration-baselines)。  

> [!Tip]  
> 对要部署到每个设备集合的每个配置基线重复此过程。 至少需要将每个配置基线部署到至少一个设备集合。



## <a name="bkmk_monitor"></a> 监视 SCAP 符合性数据 

将符合性数据导回 SCAP 格式前，你需要验证并确保站点已收集数据。 将配置基线部署到设备集合后，集合中每台计算机上的 Configuration Manager 客户端会自动收集符合性信息。 并将符合性信息储存在 Configuration Manager 数据库中。

查看 Configuration Manager 中配置基线部署的状态，以确保 Configuration Manager 客户端已收集适当的数据。 务必确保 Configuration Manager 中已收集适当的符合性数据，因为这可帮助验证你在此过程晚些时候创建的 XCCDF/DataStream 结果文件。

有关详细信息，请参阅[监视符合性设置](/sccm/compliance/deploy-use/monitor-compliance-settings)。


### <a name="validate-the-xccdfdatastream-results"></a>验证 XCCDF/Datastream 结果

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“符合性设置”，然后选择“SCAP 仪表板”。  

2. 选择“配置基线”、“分配”、“SCAP 文件”、“数据流”、“基准”和“配置文件”（如果适用）。  

3. 单击“显示报告”
 “示例 SCAP 报告”![](./media/scap-report.png)



## <a name="bkmk_export"></a> 将符合性结果导出为 SCAP 格式

此过程的下一步是将符合性数据导出为 SCAP 格式，这是 XML/用户可读格式的 ARF 报告文件。 SCAP 扩展导出向导和 Microsoft.Sces.DcmToScap.exe 命令行工具为每个配置基线导出单独的 XCCDF/DataStreamARF 结果文件。 这些文件对应于 Microsoft.Sces.ScapToDcm.exe 工具用于创建每个配置基线的每个 XCCDF/DataStream 输入文件。


### <a name="manually-export-with-the-console-wizard"></a>使用控制台向导手动导出

> [!Note]  
> 本部分介绍使用 Configuration Manager 控制台导出符合性结果的手动过程。 若要自动执行此过程，请参阅[使用命令行工具自动导出](#bkmk_auto-export)的下一部分。  


1. 右键单击“SCAP 仪表板”节点，启动“导出 SCAP 报告”向导。  
![从 SCAP 仪表板启动“导出 SCAP 报告”向导](./media/import-from-scap-dashboard.png)

2. 选择“配置基线”，“分配”和“SCAP 内容类型”。  
![选择基线](./media/select-ci-baseline.png)

3. 选择 SCAP 数据流文件、XCCDF/CPE 文件或 Oval 内容和变量文件的位置。  
![选择数据流](./media/export-scap-report-datastream.png)

4. 指定组织名称，并选择文件夹位置以导出 SCAP 报告。  
 ![选择数据流](./media/specify-org-export.png)
   > [!Tip]  
   > 此向导页面显示将与 **DcmToScap.exe** 工具配合使用以自动执行相同过程的命令行。  

5. 确认设置。  
 ![选择数据流](./media/confirm-export.png)

6. 选择“下一步”导出报告。 完成向导。  
 ![完成导出](./media/complete-report-export.png)


### <a name="bkmk_auto-export"></a> 使用命令行工具自动导出

打开命令提示符，转到 Configuration Manager 的 **AdminConsole\Bin** 文件夹。 使用以下命令行示例之一：  

> [!NOTE]  
> 你的帐户必须具有 Configuration Manager 提供程序的读取权限。 你还需要对命令行的 `–out` 参数中指定的文件夹具有写入权限。

**对于 SCAP 1.0/1.1 内容（例如 USGCB 和 DISA 内容）：**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf <xccdf.xml> -cpe <cpe.xml>  -select <xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

  > [!NOTE]  
  > 如果内容中有多个基准/配置文件，则应使用 `–select` 参数来指定客户端上已评估的基准/配置文件。  

**对于 SCAP1.2 内容（例如最新的 USGCB 内容）：**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select <datastream/xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > 如果内容中有多个数据流/基准/配置文件，则应使用 `–select` 参数来指定客户端上已评估的数据流/基准/配置文件。  

**对于带外部变量的单个 OVAL 文件：**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > Microsoft.Sces.DcmToScap.exe 仅为每台目标计算机生成 OVAL 定义结果报告。 不会生成 ARF 报告。  


#### <a name="how-to-get-the-baselineciid-and-assignmentid"></a>如何获取 BaselineCIID 和 AssignmentID

在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“符合性设置”，然后选择“配置基线”。 `BaselineCIID` 是配置基线的标识符 (ID)。  
![获取 CI ID 和分配 ID](./media/get-to-baselines.png)

选择所需的配置基线，然后单击“部署”选项卡。`AssignmentID` 是设备集合的配置基线部署的标识符 (ID)。 如果未显示分配 ID，请右键单击列标题，然后选择“分配 ID”。  
![获取 CI ID 和分配 ID](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Microsoft.Sces.DcmToScap.exe 命令行参数

| 参数 | 用法 | 必需 |
| --- | --- | --- |
| `-baseline [Baseline CI ID]` | 指定配置基线 | 是 |
| `-assignment [Assignment ID]` | 指定配置基线部署 | 是 |
| `-organization [organization name]` | 指定组织名称，此名称将显示在报告中。 可通过 `;` 将其分隔，以指定多行组织名称。 | 否 |
| `-type [thin/full/fullnosc]` | 指定 OVAL 结果类型：精简结果、完整结果或没有系统特征的完整结果。 | 否（如果未指定，则默认值是完整结果） |
| `-scap [scap data stream file]` | 指定 SCAP 数据流文件 | 是（对于 SCAP 1.2 数据流，分别与 –xccdf 和 –oval/-variable 互斥） |
| `-xccdf [xccdf file]` | 指定 XCCDF 文件 | 是（对于 SCAP 1.0/1.1 XCCDF，分别与 –scap 和 –oval/-variable 互斥） |
| `-cpe [cpe file]` | 指定 CPE 文件 | 是（对于 SCAP 1.0/1.1 XCCDF，分别与 –scap 和 –oval/-variable 互斥） |
| `-oval [oval file]` | 指定 OVAL 文件 | 是（对于独立 OVAL 文件，分别与 –xccdf 和 -scap 互斥） |
| `-variable [oval external variable file]` | 指定 OVAL 外部变量文件 | 否（如果有外部 OVAL 变量文件与 –xccdf 和 -scap 互斥，则对于独立 OVAL 文件可选） |
| `-select [xccdf benchmark/profile]` | 从 SCAP 数据流或 XCCDF 文件选择 XCCDF 基准、配置文件 | 是（必须做出选择以生成报告，以便在 Configuration Manager 数据库中匹配相应的 DCM 基线） |
| `-out [output directory]` | 指定符合性设置 cab 文件的输出位置 | 否（如果未指定，则此工具仅列出内容而不转换） |
| `-log [log file]` | 指定日志文件 | 否（如果未指定，则将日志写入 Microsoft.Sces.DcmToScap.log 文件） |
| `-help` 或 `-?` | 打印输出工具使用情况 | 否 |

 > [!TIP]  
 > 可指定 `-?`、`–h` 或 `–help` 参数以显示 Microsoft.Sces.DcmToScap.exe 工具的语法和参数列表。

默认情况下，Microsoft.Sces.DcmToScap.exe 工具使用你的凭据访问 Configuration Manager 数据库。 Microsoft.Sces.DcmToScap.exe 工具至少需要对 Configuration Manager 数据库具有读取权限。

运行该工具后，验证是否存在以下文件： 
- **ARF** 报告：`_ARF_xxxx.xml_` 和/或**用户可读**报告：`xxx.txt`
- **Cyberscope** 报告：`LASR_xxx.xml`
- **ConsumedOval** 报告：`xx-oval-<machineName>.xml`
- **XCCDF 基准结果**报告：`xccdf_xxx.xml` 



## <a name="next-step"></a>下一步
> [!div class="nextstepaction"]
> [故障排除](/sccm/compliance/plan-design/scap/troubleshooting-scap)
