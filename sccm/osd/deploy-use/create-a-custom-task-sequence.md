---
title: "建立自訂工作順序 | Microsoft Docs"
description: "在 System Center Configuration Manager 中編輯自訂工作順序，以在工作順序中新增步驟。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 03c844084c72fc52806123d9f4c11a410a3ec775
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立自訂工作順序

*適用對象：System Center Configuration Manager (最新分支)*

當您在 System Center Configuration Manager 中建立自訂工作順序時，它不會包含任何工作順序步驟。 建立工作順序之後，您必須編輯它，並新增您需要的工作順序步驟。  

##  <a name="BKMK_CustomTS"></a> 建立自訂工作順序  
 使用下列程序建立自訂工作順序。  

#### <a name="to-create-a-custom-task-sequence"></a>建立自訂工作順序  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序]  啟動 [建立工作順序精靈]。  

4.  在 [建立新的工作順序]  頁面上，選取 [建立新的自訂工作順序] 。  

5.  在 [工作順序資訊]  頁面指定工作順序的名稱、工作順序的描述，以及工作順序可使用的選用開機映像，然後完成精靈。  

 完成 [建立工作順序精靈] 之後，Configuration Manager 會將自訂的工作順序新增至 [工作順序] 節點。 您現在可以編輯此工作順序，為其新增工作順序步驟。  

 如需可用工作順序步驟的清單，請參閱[工作順序步驟](../understand/task-sequence-steps.md)。  

 如需如何編輯工作順序的詳細資訊，請參閱[編輯工作順序](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence)。  

 通常您會使用工作順序將作業系統部署的工作自動化，但是您可以建立自訂工作順序，以自動化各種工作。 如需詳細資訊，請參閱[建立非作業系統部署的工作順序](create-a-task-sequence-for-non-operating-system-deployments.md)。  

 ## <a name="next-steps"></a>後續步驟
 [部署工作順序](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
