---
title: "為使用者與目的地電腦建立關聯 | Microsoft Docs"
description: "部署作業系統時，設定 System Center Configuration Manager 將使用者與目的地電腦產生關聯。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c0331567b94a99b29cc73c16de17a9f3bc6b9e43
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>將使用者與 System Center Configuration Manager 中的目的地電腦產生關聯

適用於：System Center Configuration Manager (最新分支)

當您使用 System Center Configuration Manager 部署作業系統時，可以將使用者與部署作業系統所在的目的地電腦產生關聯。 這項設定包括指定下列各項：  

-   單一使用者為目的地電腦的主要使用者。  

-   多位使用者為目的地電腦的主要使用者。  

 使用者裝置親和性支援部署應用程式時使用者為中心的管理。 當您將使用者與安裝作業系統所在的目的地電腦產生關聯時，您之後可將應用程式部署給該使用者，應用程式會自動安裝到目的地電腦上。 不過，即使部署作業系統時可以設定支援使用者裝置親和性，您仍無法利用使用者裝置親和性部署作業系統。  

 如需使用者裝置親和性的詳細資訊，請參閱[使用使用者裝置親和性連結使用者和裝置](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>如何在部署作業系統時指定使用者  
 下表列出可將使用者裝置親和性整合至作業系統部署中的動作。 您可以將使用者裝置親和性整合至 PXE 部署、可開機媒體部署和預先設置的媒體部署。  

|動作|詳細資訊|  
|------------|----------------------|  
|建立包含 **SMSTSAssignUsersMode** 變數的工作順序|使用 **Set Task Sequence Variable** 工作順序步驟將  [SMSTSAssignUsersMode](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) 變數加入工作順序的開頭。 此變數會指定工作順序處理使用者資訊的方式。<br /><br /> 將變數設定為下列其中一個值：<br /><br /> <br /><br /> **自動**：工作順序會自動建立使用者與目的地電腦之間的關聯性，並且部署作業系統。<br /><br /> **擱置**：工作順序會建立使用者與目的地電腦之間的關聯性，但是會等候管理使用者核准，才部署作業系統。<br /><br /> **已停用**：工作順序不會將使用者與目的地電腦產生關聯，並且會繼續部署作業系統。<br /><br /> <br /><br /> 此變數也可以在電腦或集合上設定。 如需內建變數的詳細資訊，請參閱[工作順序內建變數](../../osd/understand/task-sequence-built-in-variables.md)。|  
|建立收集使用者資訊的啟動前置命令|啟動前置命令可以是含有輸入方塊的 Visual Basic (VB) 指令碼，也可以是會驗證所輸入使用者資料的 HTML 應用程式 (HTA)。<br /><br /> 啟動前置命令必須設定工作順序執行時使用的 **SMSTSUdaUsers** 變數。 此變數可以在電腦、集合或工作順序變數上設定。 請使用下列格式加入多位使用者： *網域\使用者 1, 網域\使用者 2, 網域\使用者 3*。|  
|設定發佈點和媒體將使用者與目的地電腦產生關聯的方式|當您 [設定發佈點接受 PXE 開機要求](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) ，以及使用 建立 [建立工作順序媒體精靈](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) 或 [預先設置媒體](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) 時，可以指定發佈點或媒體支援將使用者與作業系統部署所在目的地電腦產生關聯的方式。<br /><br /> 設定使用者裝置親和性支援並沒有內建方法可驗證使用者識別。 佈建電腦的技術人員代表使用者輸入資訊時，這點就會相當重要。 除了設定工作順序處理使用者資訊的方式之外，在發佈點和媒體上設定這些選項可提供限制從 PXE 開機或特定類型媒體啟動部署的能力。|  
