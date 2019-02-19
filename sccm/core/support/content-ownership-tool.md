---
title: 内容所有权工具
titleSuffix: Configuration Manager
description: 使用内容所有权工具在 Configuration Manager 中更改孤立包的所有权。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ba864914afb6794d460b81f5df346902b8ab0ce
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121874"
---
# <a name="content-ownership-tool"></a>内容所有权工具

适用范围：System Center Configuration Manager (Current Branch)

内容所有权工具是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 它可以在 Configuration Manager 中更改孤立包的所有权。 孤立包没有自己所拥有的站点服务器。 删除站点服务器时，如果包仍然属于此站点服务器，它们可能会变为孤立包。

可在 Configuration Manager 层次结构中的任何站点服务器上运行内容所有权工具。 以具有足够包权限的管理用户身份登录。  

> [!Tip]  
> 使用 `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` 中的 ContentLibraryCleanup.exe 来从分发点删除孤立的内容。 有关详细信息，请参阅[内容库清理工具](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool)。  



## <a name="features"></a>功能

- 显示所有孤立包  

- 显示所有包（即使不是孤立的）  

- 查看与站点的连接状态  

- 按名称、站点代码或包类型筛选包  

- 按任何显示的列排序  

- 使用单个操作更改一个或多个包的分配  

- 查看所有权转移活动的进度  



## <a name="usage"></a>用法

运行 ContentOwnershipTool.exe 以启动该工具。 运行该工具不需要计算机上的本地管理员权限。

没有任何命令行参数。

> [!Important]   
> 此工具会更改孤立包的所有权。 包本身不会从存储它的分发点中移动。 此所有权更改不会导致在分发点上更新包。 也不会导致客户端重新评估包的部署策略。 所有权发生更改后，请确保新的站点服务器可以访问源文件。 它至少应具有对每个包的源文件的读取权限。 



## <a name="see-also"></a>另请参阅

- [内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [内容库](/sccm/core/plan-design/hierarchy/the-content-library)
