---
title: "工作順序媒體的啟動前置命令 | Microsoft Docs"
description: "建立用於啟動前置命令的指令碼，並發佈與啟動前置命令相關聯的內容，然後在媒體中設定啟動前置命令。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 1c396534425179c6828d48acc578295167c566be
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prestart-commands-for-task-sequence-media-in-system-center-configuration-manager"></a>System Center Configuration Manager 中工作順序媒體的啟動前置命令

*適用於：System Center Configuration Manager (最新分支)*

您可以在 System Center Configuration Manager 建立啟動前置命令，將它與開機媒體、獨立媒體和預先設置的媒體搭配使用。 啟動前置命令是指令碼或可執行檔，其可在選取工作順序之前執行，而且可在 Windows PE 中與使用者互動。 啟動前置命令會提示要求使用者提供資訊，並將該資訊儲存在工作順序環境中，或查詢工作順序變數的相關資訊。 當目的地電腦開機時，會在從管理點下載原則之前執行命令列。 使用下列程序，建立用於啟動前置命令的指令碼，發佈與啟動前置命令相關聯的內容，並且在媒體中設定啟動前置命令。  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>建立用於啟動前置命令的指令碼檔  
 在執行工作順序的同時，可藉由使用 Microsoft.SMS.TSEnvironment COM 物件來讀取及寫入工作順序變數。 以下範例說明查詢 _SMSTSLogPath 工作順序變數的 Visual Basic 指令碼檔，以取得目前的記錄位置。 指令碼也會設定自訂變數。  

```  
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>建立用於指令碼檔案的套件並發佈內容  
 建立用於啟動前置命令的指令碼或可執行檔之後，您必須建立套件來源以裝載指令碼檔或可執行檔、建立檔案的套件 (不需要程式)，然後將內容發佈到發佈點。  

 如需建立套件的詳細資訊，請參閱[套件和程式](../../apps/deploy-use/packages-and-programs.md)。  

 如需發佈內容的詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  

## <a name="configure-the-prestart-command-in-media"></a>在媒體中設定啟動前置命令  
 您可以在 [建立工作順序媒體精靈] 中為獨立媒體、可開機媒體或預先設置的媒體設定啟動前置命令。 如需媒體類型的詳細資訊，請參閱[建立工作順序媒體](../deploy-use/create-task-sequence-media.md)。 利用下列程序在媒體中建立啟動前置命令。  

#### <a name="to-create-a-prestart-command-in-media"></a>在媒體中建立啟動前置命令  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序媒體]  以啟動 [建立工作順序媒體精靈]。  

4.  在 [選取媒體類型]  頁面上，選取 [獨立媒體] 、[可開機媒體] 或 [預先設置的媒體] ，然後按 [下一步] 。  

5.  瀏覽至精靈的 [自訂]  頁面。 如需在精靈中設定其他頁面的詳細資訊，請參閱[建立工作順序媒體](../deploy-use/create-task-sequence-media.md)。  

6.  在 [自訂]  頁面指定下列資訊，然後按 [下一步] 。  

    -   選取 [啟用啟動前置命令] 。  

    -   在 [命令列]  文字方塊中，輸入您為啟動前置命令建立的指令碼或可執行檔。  

        > [!IMPORTANT]  
        >  使用 **cmd /C <啟動前置命令\>** 指定啟動前置命令。 例如，假設您將 TSScript.vbs 當成啟動前置命令指令碼的名稱使用，您會在命令列輸入 **cmd /C TSScript.vbs** 。 其中 **cmd /C** 會開啟新的 Windows 命令直譯器視窗，並使用 Path 環境變數尋找啟動前置命令指令碼或可執行檔。 您也可為啟動前置命令指定完整路徑，但磁碟機代號會因電腦不同的磁碟機設定而不同。  

    -   選取 [包含啟動前置命令的檔案] 。  

    -   按一下 [設定]  ，選取與啟動前置命令檔案相關聯的套件。  

    -   按一下 [瀏覽]  ，選取裝載啟動前置命令之內容的發佈點。  

7.  完成精靈。  
