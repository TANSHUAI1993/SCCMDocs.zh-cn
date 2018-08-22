---
title: 内容库传输工具
titleSuffix: Configuration Manager
description: 使用内容库传输工具将内容从一个磁盘驱动器传输到另一个 Configuration Manager 分发点上。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0196ce1fd3561e63fc3445758d90b535ac9bc8ab
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386438"
---
# <a name="content-library-transfer-tool"></a>内容库传输工具

*适用范围：System Center Configuration Manager (Current Branch)*

内容库传输工具是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 它将内容从一个磁盘驱动器传输到另一个磁盘驱动器。 该工具旨在分发点站点系统上运行。 它支持与站点或远程站点系统并置的分发点。  

当托管内容库的磁盘驱动器已满时，该工具非常有帮助。 首先添加或标识具有足够空间来托管内容库的另一个磁盘驱动器。 然后使用 ContentLibraryTransfer.exe 将内容从旧的已满硬盘传输到新的空磁盘。
 
传输完成后，客户端计算机可从新位置访问内容。



## <a name="usage"></a>用法 

以具有分发点上的管理权限的用户身份运行 ContentLibraryTransfer.exe。 

#### <a name="syntax"></a>语法 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>示例
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>限制

- 在分发点上本地运行该工具。 不能从远程计算机运行该工具。  

- 仅在客户端未主动访问分发点时使用该工具。 如果在客户端访问内容的同时运行该工具，则目标驱动器上的内容库可能具有不完整的数据。 数据传输可能会失败，导致内容库无法使用。  

- 运行工具时，请勿将内容分发到分发点。 如果在内容写入到分发点的同时运行该工具，则目标驱动器上的内容库可能具有不完整的数据。 数据传输可能会失败，导致内容库无法使用。



## <a name="see-also"></a>另请参阅

- [内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [内容库](/sccm/core/plan-design/hierarchy/the-content-library)
