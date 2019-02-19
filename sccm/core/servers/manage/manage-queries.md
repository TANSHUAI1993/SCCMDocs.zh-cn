---
title: 管理查询
titleSuffix: Configuration Manager
description: 了解如何管理查询。 包括用于详细参考的表。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87b92bb857f6a39a99e3aee1e4bc862904bcc4ef
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126906"
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理查询

适用范围：System Center Configuration Manager (Current Branch)

使用本主题中的信息有助于在 System Center Configuration Manager 中管理查询。  

 有关如何创建查询的信息，请参阅[如何在 System Center Configuration Manager 中创建查询](../../../core/servers/manage/create-queries.md)。  

## <a name="how-to-manage-queries"></a>如何管理查询  
 在“监视”  工作区中，选择“查询” ，接着选择要管理的查询，然后选择管理任务。  

 使用下表以详细了解可能需要一些信息才能让你选择的管理任务。  

|管理任务|详细信息|更多信息|  
|---------------------|-------------|----------------------|  
|**运行**|运行所选查询并在 Configuration Manager 控制台中显示结果。|无更多信息。|  
|**安装客户端**|打开“安装客户端向导”，通过此向导可在所选查询返回的计算机上安装 Configuration Manager 客户端。<br /><br /> 此选项不可用于返回移动设备、用户或用户组的查询。|有关如何使用客户端请求安装 Configuration Manager 客户端的详细信息，请参阅[将客户端部署到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。|  
|**导出**|打开“导出对象向导”  ，将此查询导出为托管对象格式 (MOF) 文件，该文件可以在其他站点导入。|无更多信息。|  
|**移动**|打开“移动所选项目”  对话框，从中你可以将所选的查询移动到你之前在“查询”  节点下创建的文件夹。|无更多信息。|  

## <a name="see-also"></a>另请参阅  
 [System Center Configuration Manager 中查询的操作和维护](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
