---
title: "删除软件更新点 | Microsoft Docs"
description: "按照此过程可通过 Configuration Manager 控制台删除站点中的软件更新点站点系统角色。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
ms.openlocfilehash: 22de02c51be3a0cd66b1be0f04b2fbdeb897858c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_RemoveSUP"></a> 删除软件更新点站点系统角色  

*适用范围：System Center Configuration Manager (Current Branch)*

可以通过 Configuration Manager 控制台删除站点中的软件更新点站点系统角色。 客户端策略将更新，以便从列表中删除软件更新点。 在删除站点中的最后一个软件更新点时，软件更新点列表将不包含软件更新点，而且实质上将在站点中禁用软件更新。 如果主站点中有多个软件更新点，而且你删除了配置为同步源的软件更新点，则必须将站点中的另一个软件更新点选为新的同步源。  

> [!NOTE]  
>  从站点系统中删除软件更新点站点角色时，请等待至少 15 分钟，然后再重新安装软件更新点站点角色。  

 使用下列过程来删除软件更新点。  

#### <a name="to-remove-the-software-update-point"></a>删除软件更新点  

1.  在“Configuration Manager”  控制台中，单击“管理” 。  

2.  在“管理”工作区中，展开“站点配置” ，然后单击“服务器和站点系统角色” 。  

3.  选择带有要删除的软件更新点的站点系统服务器，然后在“站点系统角色” 中选择“软件更新点” 。  

4.  在“站点角色”  选项卡上的“站点角色”  组中，单击“删除角色” 。 确认要删除软件更新点，或者在该站点为其他软件更新点选择新的同步源。  
