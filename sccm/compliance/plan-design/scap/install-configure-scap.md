---
title: 安装和配置安全内容自动化协议 (SCAP) 扩展
titleSuffix: System Center Configuration Manager
description: 安装和配置安全内容自动化协议 (SCAP) 扩展
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 03fc9fa9f82aeae8ab22d6b4c3fa7858e93401cc
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-configure-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>安装和配置 Microsoft System Center Configuration Manager 的 SCAP 扩展

*适用范围：System Center Configuration Manager (Current Branch)*

> [!Tip]  
> 此功能在 Technical Preview 1803 版中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 SCAP 扩展的此预发行版本可以安装在当前支持的任何 Configuration Manager Current Branch 和 LTSB 1606 版本上。 从 1803 Technical Preview 开始，安装文件位于 cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi 中。   

在准备必备的基础结构后，即可在需要运行此过程的计算机上安装和配置 Microsoft System Center Configuration Manager 的 SCAP 扩展。

## <a name="install-scap-extensions-configuration-manager"></a>安装 SCAP 扩展 Configuration Manager

1. 运行 ConfigMgr\_Extensions\_for\_SCAP.msi 安装此工具。
2. 在 Windows 资源管理器中，转到下载 **ConfigMgr\_Extensions\_for\_SCAP.msi** 文件的文件夹，然后双击 **ConfigMgr\_Extensions\_for\_SCAP.msi** 文件。 这会启动“Microsoft System Center Configuration Manager 的 SCAP 扩展安装向导”。

使用下表中的信息并接受向导的默认值（除非需要另外指定）来完成“Microsoft System Center Configuration Manager 的 SCAP 扩展安装向导”。

**表 1.0**“Microsoft System Center Configuration Manager 的 SCAP 扩展安装向导”过程

| 向导页名称 | 用户操作 |
| --- | --- |
| 欢迎和最终用户许可协议 |1.查看许可协议|
| 欢迎和最终用户许可协议|2.单击“我接受许可协议中的条款”。|
| 欢迎和最终用户许可协议|3.单击“安装” 。|
| 完成 Microsoft System Center Configuration Manager 安装向导的 SCAP 扩展 |4.单击 **“完成”**。|
 



默认情况下，“Microsoft System Center Configuration Manager 的 SCAP 扩展安装向导”将扩展安装在 Configuration Manager 控制台安装文件夹中。



## <a name="download-and-install-the-scap-data-stream-files"></a>下载并安装 SCAP 数据流文件

在运行 SCAP 扩展以转换 SCAP 数据流文件并将其导入符合性设置功能前，必须从美国国家漏洞数据库 (NVD) 网站的[下载页](http://nvd.nist.gov/fdcc/download_fdcc.cfm)下载 SCAP 数据流文件。 然后将文件复制到你安装 SCAP 扩展的文件夹

根据你的环境，你可能不需要下载页上列出的所有 SCAP 数据流文件。

安装 SCAP 数据流

1. 请访问 [NVD 网站](http://nvd.nist.gov/) 确定你的组织要求的 SCAP 数据流。
NIST 发布的 SCAP 数据流被分成多个捆绑包，这些捆绑包也称作_清单_。

2. 从 [NVD 网站](http://nvd.nist.gov/home.cfm)下载 SCAP 数据流，这些数据流存储在压缩文件中，带有 .zip 文件扩展名或标记为 DataStream XML 文件。

    >[!IMPORTANT] 
    >有许多可从 NVD 下载的带有 .xml 扩展名的 SCAP 数据流文件。 但是，只有包含 XCCDF（SCAP1.0 和 1.1）/DataStream (SCAP1.2) 内容的 .xml 文件才适用于 SCAP 扩展。

3. 提取你下载到相同文件夹（安装 SCAP 扩展的位置）的 SCAP 数据流 zip 文件/DataStream XML 文件。

## <a name="convert-and-import-the-scap-data-stream-files-using-the-import-scap-content-wizard"></a>使用“导入 SCAP 内容向导”转换并导入 SCAP 数据流文件

获取 SCAP 数据流后，即可导入数据流并将其转换为配置基线。 NIST 发布的 SCAP 数据流被组织到多个包。 按照 NIST 的说明验证要在环境中使用哪些捆绑包。 例如，每个 Windows 版本均有一个单独的捆绑包，防火墙配置有其他特定于版本的捆绑包，Internet Explorer 8.0 有一个捆绑包。 使用以下过程完成此任务。

### <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>将 SCAP 数据流导入 Configuration Manager

1. 从配置基线的功能区启动“导入 SCAP 内容向导”。

     ![从 CI 基线功能区启动“导入 SCAP 内容向导”](./media/import-scap-content.png)

2. 选择“内容类型”。

      ![选择“内容类型”](./media/import-new-scap-content.png)

3. 选择 SCAP 数据流文件、XCCDF 和 CPE 字典文件或 Oval 内容文件。

     ![选择 SCAP 数据流文件](./media/select-datastream-file.png)

4. 如果是 SCAP 1.2，则选择数据流。 然后选择 SCAP 1.x 的基准和配置文件。  选择“下一步”转换内容。 你会看到一个进度栏。

      ![选择 SCAP 1.2 的基准和配置文件](./media/select-benchmark-and-profile.png)

5. 确认要导入的配置数据。

      ![确认配置屏幕截图](./media/confirm-configuration.png)

6. 单击“下一步”导入配置数据。

      ![完成导入](./media/complete-import.png)

## <a name="alternate-method-convert-and-import-the-scap-data-stream-files-using-the-cmd-line-tool"></a>（备选方法）使用命令行工具转换并导入 SCAP 数据流文件

获取 SCAP 数据流后，可以使用 Microsoft.Sces.ScapToDcm.exe 工具将 SCAP 数据流转换为符合性设置符合 .cab 文件。 然后将 .cab 文件导入 Configuration Manager。 Microsoft.Sces.ScapToDcm.exe 工具将 SCAP 数据流转换为可使用符合性设置功能在 Configuration Manager 中访问的配置项目和配置基线。 Microsoft.Sces.ScapToDcm.exe 工具将 SCAP 数据流转换为 XML 清单。 然后，它将 XML 清单打包成一个 .cab 文件，你可以将该文件导入 Configuration Manager。

NIST 发布的 SCAP 数据流被组织到多个包。 按照 NIST 的说明验证要在环境中使用哪些捆绑包。 例如，每个 Windows 版本均有一个单独的捆绑包，防火墙配置有其他特定于版本的捆绑包，Internet Explorer 8.0 有一个捆绑包。 使用以下过程完成此任务。





## <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>将 SCAP 数据流导入 Configuration Manager

1. 则将 SCAP 数据流转换为符合性设置符合 .cab 文件。
2. 将 .cab 文件导入 Configuration Manager。

### <a name="convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files"></a>将 SCAP 数据流转换为符合性设置符合 .cab 文件

在分析和访问你的系统的符合性前，你需要将 XML 格式的 SCAP 数据流转换为符合符合性设置配置项目和配置基线的 XML 清单。 Microsoft.Sces.ScapToDcm.exe 工具将 SCAP 数据流转换为 XML 清单。 然后，它将 XML 清单打包成一个 .cab 文件，你稍后可以将该文件导入 Configuration Manager。

#### <a name="to-convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files-using-the-microsoftscesscaptodcmexe-tool"></a>**使用 Microsoft.Sces.ScapToDcm.exe 工具将 SCAP 数据流转换为符合性设置符合 .cab 文件**

在命令提示符下，转到 AdminConsole\Bin 文件夹，运行 Microsoft.Sces.ScapToDcm.exe 以生成符合性设置符合 cab，并将其导入 Configuration Manager 站点。

   >[!NOTE] 
   > 你的帐户必须对输出文件夹具有读/写权限

**对于 SCAP 1.0/1.1 内容（XCCDF XML 文件，例如 USGCB 和 DISA 内容）：**

 Microsoft.Sces.ScapToDcm.exe –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -out &lt;outputFolder&gt; [-select benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   >如果不使用 –select 参数指定基准/配置文件，则此工具将为内容文件中的每个基准生成一个 DCM cab。

**对于 SCAP1.2 内容（DataStream XML 文件，例如最新的 USGCB 内容）：**

Microsoft.Sces.ScapToDcm.exe –scap &lt;scapdatastreamfile.xml&gt; -out &lt;outputFolder&gt; [-select datastream/benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   > 如果不使用 –select 参数指定数据流/基准/配置文件，则此工具将为内容文件中的每个基准生成一个 DCM cab。

**对于带外部变量的单个 OVAL 文件：**

Microsoft.Sces.ScapToDcm.exe –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;outputFolder&gt; [-log LogFileName]

   >[!NOTE] 
   > 如果外部变量文件中的一个变量有多个值，则 Microsoft.Sces.ScapToDcm.exe 工具将这些值视为此变量的一个数组。



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe。 命令行参数

| **参数** | **用法** | **必需** |
| --- | --- | --- |
| -scap [scap 数据流文件] | 指定 SCAP 数据流文件 | 是（对于 SCAP 1.2 数据流，分别与 –xccdf 和 –oval/-variable 互斥） |
| -xccdf [xccdf 文件] | 指定 XCCDF 文件 | 是（对于 SCAP 1.0/1.1 XCCDF，分别与 –scap 和 –oval/-variable 互斥） |
| -cpe [cpe file] | 指定 CPE 文件 | 是（对于 SCAP 1.0/1.1 XCCDF，分别与 –scap 和 –oval/-variable 互斥） |
| -oval [oval 文件] | 指定 OVAL 文件 | 是（对于独立 OVAL 文件，分别与 –xccdf 和 -scap 互斥） |
| -variable [oval 外部变量文件] | 指定 OVAL 外部变量文件 | 否（如果有外部 OVAL 变量文件，则对于独立 OVAL 文件可选，分别与 –xccdf 和 -scap 互斥） |
| -select [xccdf benchmark/profile] | 从 SCAP 数据流或 XCCDF 文件选择 XCCDF 基准、配置文件 | 否（我们建议指定此开关。 如果未指定，则此工具将针对在所有嵌入的数据流/基准中的所有配置文件生成一个 cab） |
| -out [输出目录] | 指定 DCM cab 文件的输出位置 | 否（如果未指定，则此工具仅列出内容而不转换） |
| -log [日志文件] | 指定日志文件 | 否（如果未指定，则将日志写入 Microsoft.Sces.ScapToDcm.log 文件） |
| -help / -? | 打印输出工具使用情况 | 否 |





#### <a name="the-following-command-lines-are-samples-for-the-microsoftscesscaptodcmexe-tool"></a>以下命令行是 Microsoft.Sces.ScapToDcm.exe 工具的示例：

**SCAP1.2 Content:**

  Microsoft.Sces.ScapToDcm.exe –scap scap\_gov.nist\_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID

**SCAP1.0/1.1 Content:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_Test-WinXP\_xccdf.xml –cpe scap\_gov.nist\_Test-WinXP\_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID

**SCAP OVAL Content:**

  Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder

**以下输出是 Microsoft.Sces.ScapToDcm.exe 工具中的示例：**

  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Process XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Process XCCDF Profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0-BVT Profile #1

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml Process SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip SCAP Data Stream: [scap\_tst.bvt\_datastream\_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml] Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Version:       [v1.0.0.0] Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf\_tst.bvt\_profile\_version\_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip

  Processing CPE dictionary: scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0 into DCM baseline xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

## <a name="next-step"></a>下一步
> [!div class="nextstepaction"]
> [导入 SCAP 符合性设置并导出符合性结果](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)
