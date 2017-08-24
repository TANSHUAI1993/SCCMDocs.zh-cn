---
title: "内容库清理工具 | Microsoft Docs"
description: "使用内容库清理工具删除不再与 System Center Configuration Manager 部署关联的孤立内容。"
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76e6772bdd5cbd32d525e728f6ebc988b045da78
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>适用于 System Center Configuration Manager 的内容库清理工具

*适用范围：System Center Configuration Manager (Current Branch)*

 从版本 1702 开始，用户可以使用命令行工具 (**ContentLibraryCleanup.exe**) 从分发点删除不再与任何包或应用程序关联的内容（即孤立内容）。 此工具称为内容库清理工具，可替换针对过去的 Configuration Manager 产品发布的较旧版本的类似工具。  

该工具只影响你运行该工具时指定的分发点上的内容。 该工具无法删除站点服务器上的内容库中的内容。

你可以在管理中心站点或主站点的站点服务器上的 *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* 文件夹中找到 **ContentLibraryCleanup.exe**。

## <a name="requirements"></a>要求  
 该工具一次只能对一个分发点运行。  
 - 该工具可在承载你要清理的分发点的计算机上直接运行，或者从其他服务器远程运行。
 - 运行该工具的用户帐户必须具有基于角色的直接管理权限，相当于 Configuration Manager 层次结构中的完全权限管理员。 当帐户收到这些具有完全权限管理员权限的 Windows 安全组成员权限时，该工具不能运行。

## <a name="modes-of-operation"></a>操作模式
可以在以下两种模式中运行该工具。 我们建议在*假设*模式下运行该工具以查看结果，然后在*删除模式*下运行该工具：
  1.    **假设模式**：   
      如果未指定 **/delete** 开关，该工具会以假设模式运行，并且标识将从分发点删除的内容。
   - 当在此模式下运行时，该工具不会删除任何数据。
   - 有关被删除的内容的信息会写入工具日志文件中，并且不会提示你确认每次可能的删除。  
      </br>   

  2. **删除模式**：   
    使用 **/delete** 开关运行工具时，工具将以删除模式运行。

     - 以此模式运行时，可从分发点的内容库删除指定分发点上的孤立内容。
     -  删除每个文件之前，你必须确认是否要删除文件。  若要删除，请选择“是”；若不删除，请选择“否”；或者选择“删除所有”，跳过后续提示并删除所有孤立内容。  
     </br>

工具在其中任一模式下运行时，会自动创建带名称的日志，该日志包括运行采用的模式、分发点名称、操作日期和时间等内容。 工具结束时，日志文件会自动打开。

默认情况下，日志文件会写入运行该工具的计算机上运行该工具的用户帐户的临时文件夹中。 你可以使用 **/log** 开关将日志文件重定向到其他位置，包括网络共享。


## <a name="run-the-tool"></a>运行该工具
要运行该工具，请执行以下操作：
1. 使用管理命令提示符打开包含 **ContentLibraryCleanup.exe** 的文件夹。  
2. 接下来，输入包含所需命令行开关和可选开关的命令行。

**已知问题** 运行该工具时，当任何程序包或部署失败或正在进行时，可能会返回以下错误：
-  *System.InvalidOperationException：由于程序包 <packageID> 未完全安装，因此无法清理此内容库。*

**解决方法：** 无。 当内容正在进行处理或部署失败时，该工具无法可靠地识别孤立的文件。 因此，该工具将不允许你清理内容，直到该问题解决。

### <a name="command-line-switches"></a>命令行开关  
可以按任何顺序使用以下命令行开关。   

|开关|详细信息|
|---------|-------|
|**/delete**  |**可选** </br> 要从分发点删除内容时使用此开关。 删除内容之前，系统会进行提示。 </br></br> 如果不使用此开关，该工具将记录有关要删除的内容的结果，但不会从分发点删除内容。 </br></br> 示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**可选** </br> 此开关在取消所有提示（如删除内容的提示）的安静模式下运行该工具，并且不会自动打开日志文件。 </br></br> 示例：***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;distribution point FQDN>**  | **必需** </br> 指定要清理的分发点的完全限定域名 (FQDN)。 </br></br> 示例：***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;primary site FQDN>**       | **可选** - 从主站点上的分发点清除内容时。</br>**必需** - 从辅助站点上的分发点清除内容时。 </br></br>该工具连接到父主站点，以针对 SMS_Provider 运行查询。 这些查询可让工具确定哪些内容应该处于分发点上，这样它就可以标识孤立的和可删除的内容。 与父主站点的连接必须用于辅助站点上的分发点，因为所需的详细信息无法直接从辅助站点获取。</br></br> 当分发点位于辅助站点上时，指定分发点所属的主站点的 FQDN，或父级主站点的 FQDN。 </br></br> 示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;primary site code>**  | **可选** - 从主站点上的分发点清除内容时。</br>**必需** - 从辅助站点上的分发点清除内容时。 </br></br> 当分发点位于辅助站点上时，指定分发点所属的主站点的站点代码，或父级主站点的站点代码。</br></br> 示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**可选** </br> 指定该工具写入日志文件的位置。 此目录可以是本地驱动器，也可以位于网络共享上。</br></br> 如果不使用此开关，则日志文件位于运行该工具的计算机上的用户的临时文件夹中。</br></br> 本地驱动器示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>网络共享示例：***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|
