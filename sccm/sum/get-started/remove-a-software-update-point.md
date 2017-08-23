---
title: "移除軟體更新點 | Microsoft Docs"
description: "請依照此程序，以從站台的 Configuration Manager 主控台移除軟體更新點站台系統角色。"
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
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_RemoveSUP"></a> 移除軟體更新點站台系統角色  

*適用於：System Center Configuration Manager (最新分支)*

您可以從站台的 Configuration Manager 主控台移除軟體更新點站台系統角色。 用戶端原則會更新，並從清單中移除軟體更新點。 當您移除站台上的最後一個軟體更新點時，軟體更新點清單將不會包含任何軟體更新點，而實際上該站台的軟體更新會停用。 當主要站台上有超過一個軟體更新點，而且您移除設定為同步處理來源的軟體更新點時，就必須在站台上選擇另一個軟體更新點作為新的同步處理來源。  

> [!NOTE]  
>  您從站台系統移除軟體更新點站台角色時，請至少稍候 15 分鐘，再重新安裝軟體更新點站台角色。  

 利用下列程序移除軟體更新點。  

#### <a name="to-remove-the-software-update-point"></a>若要移除軟體更新點  

1.  在 **Configuration Manager** 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理] 工作區中，展開 [站台設定] ，然後按一下 [伺服器和站台系統角色] 。  

3.  選取包含要移除之軟體更新點的站台系統伺服器，然後在 [站台系統角色] 中選取 [軟體更新點] 。  

4.  在 [站台角色]  索引標籤的 [站台角色]  群組中，按一下 [移除角色] 。 確認您想要移除軟體更新點，或為站台的其他軟體更新點選取新的同步處理來源。  
