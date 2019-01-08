---
title: 内容库清理工具
titleSuffix: Configuration Manager
description: 使用内容库清理工具删除不再与 Configuration Manager 部署关联的孤立内容。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bd347cecce0ae1317fe51a701ce67b4766fbcd10
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423178"
---
# <a name="content-library-cleanup-tool"></a>内容库清理工具

适用范围：System Center Configuration Manager (Current Branch)

使用内容库清理命令行工具删除不再与分发点上的任何包或应用程序关联的内容。 此类内容被称为孤立内容。 此工具替换了针对过去的 Configuration Manager 产品发布的较旧版本的类似工具。  

该工具只影响你运行该工具时指定的分发点上的内容。 该工具无法删除站点服务器上内容库中的内容。

查找站点服务器上 `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` 中的 ContentLibraryCleanup.exe。



## <a name="requirements"></a>要求  

- 一次只对一个分发点运行该工具。  

- 直接在承载要清理的分发点的计算机上运行，或从另一台计算机远程运行。  

- 运行该工具的用户帐户必须具有与 Configuration Manager 中的“完全权限管理员”安全角色相同的权限。  



## <a name="modes-of-operation"></a>操作模式

可以在以下两种模式中运行该工具：[假设](#what-if-mode)和[删除](#delete-mode)。

> [!Tip]  
> 从假设模式开始。 如果对结果满意，接着在删除模式下运行该工具。  


### <a name="what-if-mode"></a>假设模式   

如果未指定 `/delete` 参数，则在假设模式下运行该工具。 此模式标识将从分发点中删除的内容。

- 在此模式下运行时，该工具不会删除任何数据。  

- 该工具会向日志文件写入有关它将删除的内容的信息。 不会提示用户确认每个可能的删除操作。  


### <a name="delete-mode"></a>删除模式   

使用 `/delete` 参数运行工具时，工具将在删除模式下运行。

- 在此模式下运行时，可从分发点的内容库删除在指定分发点上找到的孤立内容。  

- 删除每个文件之前，用户需确认工具是否应删除该文件。 若要删除，请选择“是”；若不删除，请选择“否”；或者选择“删除所有”，跳过后续提示并删除所有孤立内容。  


### <a name="log-file"></a>日志文件

当工具以任一模式运行时，会自动创建日志。 它使用以下信息命名日志文件： 
- 该工具运行的模式  
- 分发点的名称  
- 操作的日期和时间  

工具结束时，会在 Windows 中自动打开日志文件。 

默认情况下，该工具会将日志文件写入运行该工具的用户帐户的临时文件夹。 此位置位于运行该工具的计算机上，该计算机并不一定是工具的目标。 使用 `/log` 参数将日志文件重定向到其他位置，包括网络共享。



## <a name="run-the-tool"></a>运行该工具

要运行该工具，请执行以下操作： 

1. 以管理员身份打开命令提示符。 将目录更改为包含 ContentLibraryCleanup.exe 的文件夹。  

2. 输入命令行，其中包含必需的[命令行参数](#bkmk_params)和要使用的任何可选参数。



## <a name="bkmk_params"></a>命令行参数  

按任何顺序使用命令行参数。   

### <a name="required-parameters"></a>必需参数

|参数|详细信息|
|---------|-------|
| `/dp <distribution point FQDN>`  | 指定待清理分发点的完全限定的域名 (FQDN)。 |
| `/ps <primary site FQDN>` | 仅在从辅助站点的分发点清除内容时需要。 该工具连接到父主站点，针对 SMS 提供程序运行查询。 工具通过这些查询确定分发点上应有的内容。 然后，它可以识别要删除的孤立内容。 必须为辅助站点上的分发点创建与父主站点的连接，因为所需的详细信息无法直接从辅助站点获取。|
| `/sc <primary site code>`  | 仅在从辅助站点的分发点清除内容时需要。 指定父主站点的站点代码。 |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>例如：扫描并记录要删除的内容（假设）
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>例如：扫描并记录辅助站点上分发点的内容
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>可选参数

|参数|详细信息|
|---------|-------|
|`/delete`| 准备好从分发点删除内容时，请使用此参数。 它会在删除内容之前提示用户。 </br></br> 如果不使用此参数，工具会记录有关待删除内容的结果。 如果没有此参数，它实际上不会从分发点删除任何内容。 |
| `/q` | 此参数以安静模式运行工具，该模式禁止所有提示。 这些提示包括删除内容的时间。 它也不会自动打开日志文件。 |
| `/ps <primary site FQDN>` | 仅在从主站点的分发点清除内容时可选。 指定分发点所属主站点的 FQDN。 |
| `/sc <primary site code>` | 仅在从主站点的分发点清除内容时可选。 指定分发点所属主站点的站点代码。 |
| `/log <log file directory>` | 指定该工具写入日志文件的位置。 此位置可以是本地驱动器，也可以是网络共享。</br></br> 如果不使用此参数，工具会将日志文件放在用户临时目录中（位于运行工具的计算机上）。|

#### <a name="example-delete-content"></a>例如：删除内容 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>例如：无提示情况下删除内容
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>例如：记录到本地驱动器
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>例如：记录到网络共享
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>已知问题

当任何包或部署失败或正在进行时，该工具可能会返回以下错误：`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

此问题没有任何解决方法。 当内容正在进行处理或部署失败时，该工具无法可靠地识别孤立文件。 必须先解决该问题，工具才会允许清理内容。
