---
title: 管理查询
titleSuffix: Configuration Manager
description: 了解如何管理查询。 包括用于详细参考的表。
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 456289520e25fe94da7e94f6a795537f68ba069e
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561966"
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理查询

适用范围：  System Center Configuration Manager (Current Branch)

本文介绍了如何在 System Center Configuration Manager 中管理查询。  

 有关如何创建查询的信息，请参阅[如何在 System Center Configuration Manager 中创建查询](../../../core/servers/manage/create-queries.md)。  

## <a name="manage-queries"></a>管理查询
 在“监视”  工作区中，选择“查询”  ，接着选择要管理的查询，然后选择管理任务。  

 下表列出了管理任务的相关信息。  

|管理任务|详细信息| 
|---------------------|-------------|
|**运行**|运行所选查询并在 Configuration Manager 控制台中显示结果。|
|**安装客户端**|打开“安装客户端向导”  。使用此向导，可以在选定查询返回的计算机上安装 Configuration Manager 客户端。<br /><br /> 此选项不适用于返回移动设备、用户或用户组的查询。 <br /><br /> 有关如何使用客户端请求安装 Configuration Manager 客户端的详细信息，请参阅[将客户端部署到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。| 
|**导出**|打开“导出对象向导”  。 使用此向导，可以将查询导出到随后可在其他站点导入的托管对象格式 (MOF) 文件。
|**移动**|打开“移动选定项”  对话框。 在此对话框中，可以将选定查询移到之前在“查询”  节点下创建的文件夹中。|

## <a name="next-steps"></a>后续步骤 
 [在 System Center Configuration Manager 中创建查询](../../../core/servers/manage/create-queries.md)
