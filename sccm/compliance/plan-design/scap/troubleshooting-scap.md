---
title: SCAP 故障排除
titleSuffix: Configuration Manager
description: 了解如何对 Configuration Manager 的 SCAP 扩展进行故障排除。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58a3c69e6206aa651e55f96286f98f64f748de70
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137130"
---
# <a name="troubleshoot-the-scap-extensions-for-configuration-manager"></a>对 Configuration Manager 的 SCAP 扩展进行故障排除

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 的 SCAP 扩展的设计旨在与 SCAP 数据流（用于经 SCAP 验证的、具有 ACS 功能的工具）一并使用以支持 USGCB。 从 NIST 网站下载的这些 USGCB SCAP 数据流通常不会出现什么问题。

使用以下方法诊断和解决问题：  

- 确保所有目标计算机上都安装了 SCAP 扩展客户端 (scmdcm.msi) 组件。  

- 查看 Microsoft.Sces.ScapToDcm.exe 工具的日志文件输出。  

- 在使用 SCAP 扩展时查看常见问题和解决方案。  

- 如有关于 SCAP 扩展的问题，或者需要进行相关反馈，请联系 Microsoft。



## <a name="review-microsoftscesscaptodcmexe-log"></a>查看 Microsoft.Sces.ScapToDcm.exe 日志

如果指定了 `–log` 参数，Microsoft.Sces.ScapToDcm.exe 工具会创建以自定义方式命名的日志文件。 日志文件包含有关 Microsoft.Sces.ScapToDcm.exe 工具运行结果的信息。 例如，它包含 XCCDF/DataStream 输入文件中已删除的或运行 Microsoft.Sces.ScapToDcm.exe 工具时跳过的项目的数目。

下表列出了日志文件中显示的某些信息以及每种类型的信息的说明。

### <a name="information-found-in-the-microsoftscesscaptodcmexe-log-file"></a>在 Microsoft.Sces.ScapToDcm.exe 日志文件中找到的信息

| 信息 | 说明 |
| --- | --- |
| **删除** | 项目可能因为测试类型不受支持而被删除。 |
| **跳过** | OVAL 定义用于无效平台。 </br> </br> XCCDF/DataStream 输入文件不引用 OVAL 定义 ID。</br> </br> XCCDF/DataStream 输入文件不引用 OVAL 测试 ID。 </br> </br> XCCDF 配置文件 ID 不包含任何等于 1 的 `@select` 语句。 </br> </br> XCCDF 配置文件 ID 包括为 true 的抽象属性。 </br> </br> XCCDF 配置文件 ID 不包含符合条件的规则。|



## <a name="common-problems-and-solutions"></a>常见问题和解决方案

下面是一些常见问题和解决方案，有助于进行故障排除。

- 出现“错误”或“未知”基线状态且 Internet Explorer 无法成功显示报表。 浏览器错误显示：“报表为空或无效”。  

     - 再次运行基线。 选择基线并单击“评估”。 然后等待监视“符合状态”/“上次评估更新”。 在“上次评估”日期更新到当前日期/时间（表示其已完成评估）后，请再次选择基线并查看报表。  

     - 如果 Internet Explorer 仍不能查看报表，这可能意味着基线过大。 使用较小批大小重新生成内容来创建较小子基线。  

     - 如果父基线上出现此问题，请尝试改为部署子基线。  

- 创建了包括指定的 USGCB 设置的组策略对象 (GPO)。 将它们链接到了包含运行 Windows 7 的计算机的组织单位 (OU)。 相容性报告表明部分设置没有正确配置。  

     - 可能组策略权限不正确或未链接到正确的 OU。  

     - 更有可能是新设置尚未生效。 默认情况下，Active Directory 客户端每 90 分钟检查一次对组策略的更新。 此周期可能是这些设置还未应用的一个原因（即使已正确配置策略）。  

     - 很多计算机设置都需要重启才能生效。 例如，设置“系统加密：将 FIPS 符合算法用于加密、哈希和签名”要求在重新启动计算机后，Windows 才可以使用指定的加密算法。 请使用管理员权限在命令提示符处输入以下命令来绕过组策略刷新间隔：`gpupdate /force`。 组策略刷新完成后，重新启动计算机，以确保所有设置生效。 有关详细信息，请参阅[组策略更新实用工具说明](https://support.microsoft.com/help/298444)。

- 向数据库连接提供组织信息时遇到问题。  

     - 若要详细了解如何配置数据库连接，请参阅[安装和配置 SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)。  
