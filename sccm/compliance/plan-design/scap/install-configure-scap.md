---
title: 安装并配置 SCAP 扩展
titleSuffix: Configuration Manager
description: 安装并配置 Configuration Manager 的安全内容自动化协议 (SCAP) 扩展。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fd440905bb736dfbfac01de804373d29c9fbb59
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384608"
---
# <a name="install-and-configure-the-scap-extensions-for-configuration-manager"></a>安装并配置 Configuration Manager 的 SCAP 扩展

*适用范围：System Center Configuration Manager (Current Branch)*

在[准备基础结构](/sccm/compliance/plan-design/scap/about-scap#bkmk_prepare)后，即可在需要运行此进程的计算机上安装并配置 Configuration Manager 的 SCAP 扩展。



## <a name="bkmk_install"></a> 安装 SCAP 扩展

安装文件位于 Configuration Manager 站点服务器上安装目录中的以下路径：  
`cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi`

1. 将 ConfigMgrExtensionsforSCAP.msi 复制到需要运行此进程的、具有 Configuration Manager 控制台的计算机。  

2. 在 Windows 资源管理器中，转到复制 ConfigMgrExtensionsforSCAP.msi 的文件夹。 双击打开该文件，并启动 Configuration Manager 的 SCAP 扩展安装向导。  

3. 查看许可协议。 单击“我接受许可协议中的条款”，然后单击“安装”。  

4. 安装完成之后，单击“完成”以关闭安装向导。  

安装向导会将 SCAP 扩展安装在 Configuration Manager 控制台安装文件夹中。 默认情况下，控制台安装文件夹为 `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole`。  



## <a name="bkmk_scap-data-stream-files"></a> 下载并安装 SCAP 数据流文件

必须先从美国国家漏洞数据库 (NVD) 的[下载页](https://csrc.nist.gov/Projects/United-States-Government-Configuration-Baseline)下载 SCAP 数据流文件，才能运行 SCAP 扩展。 然后将它们复制到安装 SCAP 扩展的文件夹。

根据你的环境，你可能不需要下载页上列出的所有 SCAP 数据流文件。

### <a name="install-the-scap-data-streams"></a>安装 SCAP 数据流

1. 请访问 [NVD 网站](http://nvd.nist.gov/) 确定你的组织要求的 SCAP 数据流。
NIST 发布的 SCAP 数据流被分成多个捆绑包，这些捆绑包也称作_清单_。  

2. 从 [NVD 网站](http://nvd.nist.gov/home.cfm)下载 SCAP 数据流，这些数据流存储在压缩文件中，带有 .zip 文件扩展名或标记为 DataStream XML 文件。  

    > [!IMPORTANT]  
    > 有许多可从 NVD 下载的带有 .xml 扩展名的 SCAP 数据流文件。 但是，只有包含 XCCDF（SCAP1.0 和 1.1）/DataStream (SCAP1.2) 内容的 .xml 文件才适用于 SCAP 扩展。  

3. 提取下载到相同文件夹（安装 SCAP 扩展的位置）的 SCAP 数据流 .zip 文件/DataStream XML 文件。  



## <a name="bkmk_convert-and-import"></a> 手动转换并导入 SCAP 数据流文件 

获取 SCAP 数据流后，即可导入数据流并将其转换为配置基线。 NIST 发布的 SCAP 数据流被组织到多个包。 按照 NIST 的说明操作以验证要在你的环境中使用哪些绑定。 例如，每个 Windows 版本均有一个单独的捆绑包，防火墙配置有其他特定于版本的捆绑包，以及一个 Internet Explorer 的捆绑包。 使用以下过程完成此任务。  

> [!Note]  
> 本文介绍通过 Configuration Manager 控制台转换和导入数据流文件的手动过程。 要自动完成此过程，请参阅下一节以[自动转换并导入 SCAP 数据流文件](#bkmk_auto-convert-and-import)。  

1. 从配置基线组的功能区单击“导入 SCAP 内容”向导。

     ![控制台功能区中的“导入 SCAP 内容”按钮](./media/import-scap-content.png)

2. 选择 SCAP 内容选项。

      ![选择导入向导的 SCAP 内容选项页](./media/import-new-scap-content.png)

3. 选择 SCAP 数据流文件、XCCDF 和 CPE 字典文件或 Oval 内容文件。

     ![选择 SCAP 数据流文件](./media/select-datastream-file.png)

4. 如果是 SCAP 1.2，则选择数据流。 然后选择 SCAP 1.x 的基准和配置文件。 单击“下一步”以转换内容。 

      ![选择 SCAP 1.2 的基准和配置文件](./media/select-benchmark-and-profile.png)

      > [!Tip]  
      > 此向导页面显示将与 ScapToDcm.exe 工具配合使用以自动执行相同过程的命令行。  

5. 确认要导入的配置数据。

      ![确认配置屏幕截图](./media/confirm-configuration.png)

6. 单击“下一步”，导入配置数据。

      ![完成导入](./media/complete-import.png)



## <a name="bkmk_auto-convert-and-import"></a> 自动转换并导入 SCAP 数据流文件 

### <a name="import-with-the-command-line-tool"></a>使用命令行工具进行导入

获取 SCAP 数据流后，可使用 Microsoft.Sces.ScapToDcm.exe 工具将 SCAP 数据流转换为符合性设置符合 .cab 文件。 然后将 .cab 文件导入 Configuration Manager。 Microsoft.Sces.ScapToDcm.exe 工具将 SCAP 数据流转换为可在 Configuration Manager 中使用的配置项目和配置基线。 Microsoft.Sces.ScapToDcm.exe 工具将 SCAP 数据流转换为 XML 清单。 然后，它将 XML 清单打包成一个 .cab 文件，你可以将该文件导入 Configuration Manager。

> [!Tip]  
> 上一节中手动过程的步骤 4 中显示了此向导页，其中显示的是将和 ScapToDcm.exe 工具配合使用以便自动执行相同过程的命令行。  


#### <a name="use-microsoftscesscaptodcmexe-to-convert-scap-data-streams-into-cab-files"></a>使用 Microsoft.Sces.ScapToDcm.exe 将 SCAP 数据流转换为 .cab 文件

在命令提示符处，转至 AdminConsole\Bin 文件夹，然后运行 Microsoft.Sces.ScapToDcm.exe。 此工具生成符合性设置符合 .cab 文件，并将其导入 Configuration Manager 站点。

   > [!NOTE]  
   > 帐户必须具备输出文件夹的读/写权限。

**SCAP 1.0/1.1 内容（XCCDF XML 文件，例如 USGCB 和 DISA 内容）的对应用法：**  

`Microsoft.Sces.ScapToDcm.exe –xccdf <xccdf.xml> -cpe <cpe.xml> -out <outputFolder> [-select benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > 如果不使用 `–select` 参数指定基准/配置文件，则此工具会为内容文件中的每个基准生成一个 .cab 文件。  

**SCAP 1.2 内容（DataStream XML 文件，例如最新的 USGCB 内容）的对应用法：**  

`Microsoft.Sces.ScapToDcm.exe –scap <scapdatastreamfile.xml> -out <outputFolder> [-select datastream/benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > 如果不使用 `–select` 参数指定数据流/基准/配置文件，则此工具会为内容文件中的每个基准生成一个 .cab 文件。

**带外部变量的单个 OVAL 文件的对应用法：**  

`Microsoft.Sces.ScapToDcm.exe –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputFolder> [-log LogFileName]`  

   > [!NOTE]  
   > 如果外部变量文件中的一个变量有多个值，则 Microsoft.Sces.ScapToDcm.exe 工具会将这些值视为此变量的一个数组。  



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe 命令行参数

| 参数 | 用法 | 必需 |
| --- | --- | --- |
| `-scap [scap data stream file]` | 指定 SCAP 数据流文件 | 是（对于 SCAP 1.2 数据流，分别与 –xccdf 和 –oval/-variable 互斥） |
| `-xccdf [xccdf file]` | 指定 XCCDF 文件 | 是（对于 SCAP 1.0/1.1 XCCDF，分别与 –scap 和 –oval/-variable 互斥） |
| `-cpe [cpe file]` | 指定 CPE 文件 | 是（对于 SCAP 1.0/1.1 XCCDF，分别与 –scap 和 –oval/-variable 互斥） |
| `-oval [oval file]` | 指定 OVAL 文件 | 是（对于独立 OVAL 文件，分别与 –xccdf 和 -scap 互斥） |
| `-variable [oval external variable file]` | 指定 OVAL 外部变量文件 | 否（如果有外部 OVAL 变量文件与 –xccdf 和 -scap 互斥，则对于独立 OVAL 文件可选） |
| `-select [xccdf benchmark/profile]` | 从 SCAP 数据流或 XCCDF 文件选择 XCCDF 基准、配置文件 | 否（此参数不是必需的，但建议指定。 如果未指定，则此工具会针对所有嵌入的数据流/基准中的所有配置文件生成一个 cab） |
| `-out [output directory]` | 指定 DCM cab 文件的输出位置 | 否（如果未指定，则此工具仅列出内容而不转换） |
| `-log [log file]` | 指定日志文件 | 否（如果未指定，则将日志写入 Microsoft.Sces.ScapToDcm.log 文件） |
| `-help` 或 `-?` | 打印输出工具使用情况 | 否 |


#### <a name="microsoftscesscaptodcmexe-examples"></a>Microsoft.Sces.ScapToDcm.exe 示例

**SCAP 1.2 内容：**  

`Microsoft.Sces.ScapToDcm.exe –scap scap_gov.nist_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID`  

**SCAP 1.0/1.1 内容：**  

`Microsoft.Sces.ScapToDcm.exe–xccdf scap_gov.nist_Test-WinXP_xccdf.xml –cpe scap_gov.nist_Test-WinXP_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID`  

**SCAP OVAL 内容：**  

`Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder`  


#### <a name="sample-output-from-microsoftscesscaptodcmexe"></a>Microsoft.Sces.ScapToDcm.exe 的示例输出

```
  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Process XCCDF Benchmark xccdf_tst.bvt_benchmark_Windows-F

  Process XCCDF Profile: xccdf_tst.bvt_profile_version_1.0.0.0-BVT Profile #1

  Process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml
   Process SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip
    SCAP Data Stream: [scap_tst.bvt_datastream_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml]
  Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf_tst.bvt_benchmark_Windows-F]

  Version:       [v1.0.0.0]
   Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf_tst.bvt_profile_version_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip

  Processing CPE dictionary: scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf_tst.bvt_profile_version_1.0.0.0 into DCM baseline xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab
```


### <a name="import-the-cab-file"></a>导入 .cab 文件

该过程的下一步是使用 Configuration Manager 控制台将符合性设置符合 .cab 文件导入 Configuration Manager。 导入此过程中早些时候创建的 .cab 文件后，将在 Configuration Manager 数据库中创建一个或多个配置项目和配置基线。 在此过程后期，可将配置基线部署至设备集合。 有关详细信息，请参阅[导入配置数据](/sccm/compliance/deploy-use/import-configuration-data)。

之前所创建的 .cab 文件就位于通过 Microsoft.Sces.ScapToDcm.exe 工具的 `–output` 参数所指定的文件夹。

> [!IMPORTANT]  
> 请为在此过程前期所创建的每个 .cab 文件重复此过程。 对于从 NVD 网站下载的 XCCDF/DataStream XML 文件，在其中所选的每个配置文件均有一个 .cab 文件。 可通过运行 Microsoft.Sces.ScapToDcm.exe 工具来处理这些文件。  

导入的配置基线是只读的，状态为“启用”，且部署状态为“否”。 “修改日期”属性显示的是导入基线的时间。 配置基线的名称来自 XCCDF/Datastream XML 的显示名称部分。 名称是使用约定 `ABC[XYZ]` 构造的，其中 ABC 是 XCCDF 基准 ID，而 XYZ 是 XCCDF 配置文件 ID（如果选择了配置文件）。



## <a name="next-step"></a>下一步
> [!div class="nextstepaction"]
> [部署并监视 SCAP 符合性，然后导出符合性结果](/sccm/compliance/plan-design/scap/deploy-monitor-export)
