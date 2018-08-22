---
title: 内容库资源管理器
titleSuffix: Configuration Manager
description: 使用内容库资源管理器查看 Configuration Manager 分发点上的内容库并对其进行故障排除。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7950447776c5c2dd756d6632a65d74d91adfba01
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385808"
---
# <a name="content-library-explorer"></a>内容库资源管理器

*适用范围：System Center Configuration Manager (Current Branch)*

内容库资源管理器是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 使用该工具进行以下活动：  

- 浏览特定分发点上的内容库  

- 对内容库的问题进行故障排除  

- 从内容库中复制包、内容、文件夹和文件  

- 将包重新分发到分发点  

- 验证远程分发点上的包  



## <a name="requirements"></a>要求

- 使用具有以下管理访问权限的帐户运行该工具：  

    - 目标分发点  

    - 站点服务器上的 WMI 提供程序  

    - Configuration Manager 提供程序  

- 只有**完全权限管理员**和**只读分析员**角色才有足够的权限通过此工具查看所有信息。  

    - 其他角色（例如**应用程序管理员**）可以查看部分信息。 有关详细信息，请参阅[禁用的包](#bkmk_disabled-packages)。  

    - **只读分析员**无法通过此工具重新分发包。  

- 只要该工具可以连接到以下对象，就可以从任何计算机运行该工具：  

    - 目标分发点  

    - 主站点服务器  

    - Configuration Manager 提供程序  

- 如果分发点与站点服务器共置，则仍然需要拥有站点服务器的管理访问权限。  



## <a name="usage"></a>用法 

启动 **ContentLibraryExplorer.exe** 时，请输入目标分发点的完全限定的域名 (FQDN)。 它随后会连接到分发点。 如果分发点是辅助站点的一部分，则会提示输入主站点服务器的 FQDN 和主站点代码。

在左窗格中，查看分发到此分发点的包。 展开包并浏览其文件夹结构。 此结构与根据其创建包的文件夹结构匹配。

选择文件夹时，它会在右窗格中显示文件夹内的所有文件。 此视图包含以下信息： 
- 文件名
- 文件大小
- 文件所处的驱动器
- 驱动器上使用相同文件的其他包
- 在分发点上最后更改文件的时间

该工具还会连接到 Configuration Manager 提供程序。 此连接用于确定分发到分发点的包，以及它们是否实际位于分发点的内容库中。 例如，待分发的包可能尚不存在于内容库中。 此类包在工具中显示为“待定”，并且没有为此包启用任何操作。


### <a name="bkmk_disabled-packages"></a> 禁用的包

某些包存在于分发点中，但在 Configuration Manager 控制台中不可见。 这些包标有星号 (\*)。 可能不会对这些包执行任何操作。 其他包也可能标有星号并禁用操作。 

禁用包的三个主要原因包括：  

- 包是 Configuration Manager 客户端升级包。 包中包含“ccmsetup.exe”。  

- 用户帐户无法访问包，且可能原因在于基于角色的管理。 例如，**应用程序作者**角色无法在控制台中看到驱动程序包，因此分发点上的所有驱动程序包都标记为禁用。  

- 包在分发点上是孤立的。  


### <a name="validate-packages"></a>验证包

使用工具栏上的“包” > “验证”来验证包。 首先，在左窗格中选择一个包节点。不要选择内容或文件夹。 该工具为此操作连接到分发点上的 WMI 提供程序。 工具启动时，缺少一个或多个内容的包会被标记为无效。 验证包可显示缺少的内容。 如果所有内容都存在，但数据已损坏，则验证会检测到损坏。


### <a name="redistribute-packages"></a>重新分发包

使用工具栏上的“包” > “重新分发”来重新分发包。 首先，在左窗格中选择一个包节点。 此操作要求提供重新分发包的权限。


### <a name="other-actions"></a>其他操作

使用“编辑” > “复制”从内容库将包、内容、文件夹和文件复制到指定的文件夹。 无法复制内容库本身。 请选择多个文件，但不可选择多个文件夹。

使用“编辑” > “查找包”来搜索包。 此操作会在包名称和包 ID 中搜索你的查询。



## <a name="limitations"></a>限制

- 该工具无法以任何方式直接操纵内容库。 对内容库的更改可能会导致故障。  

- 该工具可以重新分发包，但仅限于重新分发到目标分发点。  

- 将分发点与站点服务器共置时，无法验证包数据。 请改用 Configuration Manager 控制台。 该工具仍会检查包来确保所有内容都存在，但内容不一定完整。  

- 无法使用此工具删除内容。



## <a name="see-also"></a>另请参阅

- [内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [内容库](/sccm/core/plan-design/hierarchy/the-content-library)
