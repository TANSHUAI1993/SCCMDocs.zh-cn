---
title: SCAP 故障排除
titleSuffix: System Center Configuration Manager
description: 导入 SCAP 符合性设置作为配置基线并导出结果
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 8270db5f0a43f1c94c876bdbd59e45ee2ca85ac6
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshoot-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Microsoft System Center Configuration Manager 的 SCAP 扩展故障排除

*适用范围：System Center Configuration Manager (Current Branch)*

> [!Tip]  
> 此功能在 Technical Preview 1803 版中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 SCAP 扩展的此预发行版本可以安装在当前支持的任何 Configuration Manager Current Branch 和 LTSB 1606 版本上。 从 1803 Technical Preview 开始，安装文件位于 cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi 中。 

Microsoft System Center Configuration Manager 的 SCAP 扩展的设计旨在与 SCAP 数据流（用于经 SCAP 验证的、具有 ACS 功能的工具）一并使用以支持 USGCB。 从 NIST 网站下载的这些 USGCB SCAP 数据流通常不会出现什么问题。

但是，你可以使用以下方法诊断和解决可能遇到的问题：

- 确保所有目标计算机上都安装了 SCAP 扩展客户端 (scmdcm.msi) 组件。
- 查看 Microsoft.Sces.ScapToDcm.exe 工具的日志文件输出。
- 在使用 SCAP 扩展时查看常见问题和解决方案。
- 如有关于 SCAP 扩展的问题或需获得相关反馈，请联系 Microsoft。



## <a name="review-microsoftscesscaptodcmexe-tool-log"></a>查看 Microsoft.Sces.ScapToDcm.exe 工具日志

当指定了 –log 参数时，Microsoft.Sces.ScapToDcm.exe 工具会创建以自定义方式命名的日志文件。 日志文件包含有关 Microsoft.Sces.ScapToDcm.exe 工具运行结果的信息。 例如，日志文件包含 XCCDF/DataStream 输入文件中已删除的或运行 Microsoft.Sces.ScapToDcm.exe 工具时跳过的项目的数目。

下表列出了日志文件中显示的某些信息以及每种类型的信息的说明。

### <a name="description-of-information-found-in-microsoftscesscaptodcmexe-log-files"></a>在 Microsoft.Sces.ScapToDcm.exe 日志文件中找到的信息的相关说明

| 信息 | 说明 |
| --- | --- |
| 删除 | 项目可能会因测试类型不受支持而被删除。 |
| 跳过 |OVAL 定义用于无效平台。 </br> </br> XCCDF/DataStream 输入文件不引用 OVAL 定义 ID。</br> </br> XCCDF/DataStream 输入文件不引用 OVAL 测试 ID。 </br> </br> XCCDF 配置文件 ID 不包含任何等于 1 的 @select 语句。 </br> </br> XCCDF 配置文件 ID 包括为 true 的抽象属性。 </br> </br> XCCDF 配置文件 ID 不包含符合条件的规则。|

## <a name="common-problems-and-solutions"></a>常见问题和解决方案

下表列出了一些常见问题和解决方案，以帮助你进行故障排除。

表 1.6 常见问题和解决方案

| 问题 | 可能的解决方案 |
| --- | --- |
| 如果见到任何“错误”或“未知”基线状态且 IE 无法成功显示报告。 IE 显示“报告为空或无效”&quot;&quot; | 选择基线并单击“评估”以再次运行基线，然后等待监控“符合状态”/“上次评估更新”。 “上次评估”日期更新到当前日期/时间（表示其已完成评估）后，再次选择基线并查看报表。 如果 IE 仍不能查看报表，这可能意味着基线过大。 使用较小批大小重新生成内容来创建较小子基线。 如果父基线上出现此问题，请尝试改为部署子基线。 |
| 我已创建包括规定的 USGCB 设置的组策略对象 (GPO)，并将其链接到包含运行 Windows 7 的计算机的组织单位 (OU)，但符合性报告显示一些设置未正确配置。 | 可能组策略权限不正确或未链接到正确的 OU。 但是，更有可能是新设置尚未生效。 默认情况下，属于 Active Directory 域的客户端计算机中的组策略每 90 分钟检查一次组策略更新。 这可能是即使你已正确配置策略，但似乎仍未应用设置的原因。 需要记住的另一个因素是许多计算机设置需要重启才能生效。 例如，称为“系统加密”的设置：将 FIPS 符合算法用于加密、哈希和签名要求在重新启动计算机后，Windows 才可以使用指定的加密算法。 通过使用管理员权限在命令提示符处输入以下命令，可绕过组策略刷新间隔：gpupdate /force 组策略刷新完成后，重新启动计算机，以确保所有设置生效。 有关详细信息，请参阅知识库文章 298444[“组策略更新实用工具说明”](http://support.microsoft.com/kb/298444)。 |
| 向数据库连接提供我的组织信息时遇到问题。 | 有关如何配置数据库连接信息的过程信息，请参阅[安装和配置 SCAP](/sccm/compliance/plan-design/scap/install-configure-scap) 一文。 

## <a name="next-step"></a>下一步
> [!div class="nextstepaction"]
> [安装和配置 SCAP 扩展](/sccm/compliance/plan-design/scap/install-configure-scap)