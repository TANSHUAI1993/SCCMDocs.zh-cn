---
title: "用於管理 BIOS 轉換到 UEFI 的工作順序步驟 | Configuration Manager"
description: "了解如何自訂作業系統部署工作順序，以準備轉換到 UEFI 的 FAT32 磁碟分割。"
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 528ce515c86c4e778532290026a90a46476c4576
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>用於管理 BIOS 轉換到 UEFI 的工作順序步驟
Windows 10 提供許多新安全性功能，都需要啟用 UEFI 的裝置。 您可能有支援 UEFI，不過是使用傳統 BIOS 的新型 Windows 電腦。 在過去，將裝置轉換為 UEFI 需要您實際操作每部電腦，重新分割硬碟，並重新設定韌體。 透過使用 Configuration Manager 中的工作順序，您可以準備硬碟以進行 BIOS 至 UEFI 轉換，以就地升級程序之一部分的方式從 BIOS 轉換至 UEFI，並以硬體清查之一部分的方式收集 UEFI 資訊。

## <a name="hardware-inventory-collects-uefi-information"></a>硬體清查會收集 UEFI 資訊
從 1702 版開始，新的硬體清查類別 (**SMS_Firmware**) 和屬性 (**UEFI**) 都可以協助您判斷電腦是否是以 UEFI 模式啟動。 以 UEFI 模式啟動電腦時，**UEFI** 屬性設為 [TRUE]。 在硬體清查中，預設會啟用此項目。 如需硬體清查的詳細資訊，請參閱[如何設定硬體清查](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>建立自訂工作順序，以為硬碟進行 BIOS 至 UEFI 轉換的準備
從 Configuration Manager 1610 版開始，您現在可以使用新變數 TSUEFIDrive 來自訂作業系統部署工作順序，如此一來，[重新啟動電腦] 步驟就會在硬碟上準備用於轉換成 UEFI 的 FAT32 磁碟分割。 下列程序提供範例，說明如何建立工作順序步驟，以準備用於將 BIO 轉換成 UEFI 的硬碟。

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>若要準備用於轉換成 UEFI 的 FAT32 磁碟分割：
在安裝作業系統的現有工作順序中，您將新增具有執行 BIOS 轉換成 UEFI 之步驟的新群組。

1. 在擷取檔案和設定的步驟之後，以及安裝作業系統的步驟之前，建立新的工作順序群組。 例如，在 [擷取檔案和設定] 之後，建立名為 **BIOS-to-UEFI** 的群組。
2. 在新群組的 [選項] 索引標籤中，新增工作順序變數作為條件，其中 **_SMSTSBootUEFI** **不等於** **true**。 當電腦已在 UEFI 模式時，這會防止執行群組中的步驟。

  ![BIOS to UEFI 群組](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. 在新群組底下，新增 [重新啟動電腦] 工作順序步驟。 在 [指定重新啟動後執行的項目] 中，選取 [指派給此工作順序的開機映像] 以在 Windows PE 中啟動電腦。  
4. 在 [選項] 索引標籤上，新增工作順序變數作為條件，其中 **_SMSTSInWinPE 等於 false**。 如果電腦已在 Windows PE 中，這會防止執行此步驟。

  ![重新啟動電腦步驟](../../core/get-started/media/restart-in-windows-pe.png)
5. 新增啟動 OEM 工具的步驟，以將韌體從 BIOS 轉換成 UEFI。 這通常會是 [執行命令列] 工作順序步驟，其中包含啟動 OEM 工具的命令列。
6. 新增 [格式化和分割磁碟] 工作順序步驟，對硬碟進行分割與格式化。 在此步驟中，執行下列動作：
  1. 安裝作業系統之前，先建立將轉換成 UEFI 的 FAT32 磁碟分割。 選擇 [GPT] 作為 [磁碟類型]。
    ![格式化和分割磁碟步驟](../media/format-and-partition-disk.png)
  2. 移至 FAT32 的 [磁碟分割內容]。 在 [變數] 欄位中輸入 **TSUEFIDrive**。 當工作順序偵測到此變數時，它會準備 UEFI 轉換，再重新啟動電腦。
    ![磁碟分割內容](../../core/get-started/media/partition-properties.png)
  3. 建立工作順序引擎用來儲存其狀態及存放記錄檔的 NTFS 磁碟分割。
7. 新增 [重新啟動電腦] 工作順序步驟。 在 [指定重新啟動後執行的項目] 中，選取 [指派給此工作順序的開機映像] 以在 Windows PE 中啟動電腦。  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>在就地升級期間從 BIOS 轉換至 UEFI
Windows 10 Creators Update 引進一個簡單的轉換工具，能夠為支援 UEFI 的硬體自動執行硬碟重新分割程序，並將轉換工具整合至 Windows 7 到 Windows 10 的就地升級程序中。 當您將此工具與您的作業系統升級工作順序，以及將韌體從 BIOS 轉換至 UEFI 的 OEM 工具結合時，您可以在就地升級至 Windows 10 Creators Update 的期間，將您的電腦從 BIOS 轉換至 UEFI。

**需求**：
- Windows 10 Creators Update
- 支援 UEFI 的電腦
- 可將電腦韌體從 BIOS 轉換至 UEFI 的 OEM 工具

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>在就地升級期間從 BIOS 轉換至 UEFI
1. 建立能就地升級至 Windows 10 Creators Update 的作業系統升級工作順序。
2. 編輯工作順序。 在 [後置處理群組] 中，新增下列工作順序步驟：
   1. 在 [一般] 中，新增 [執行命令列] 步驟。 您將新增 MBR2GPT 工具的命令列，此工具會在不修改或刪除磁碟資料的情況下，將磁碟從 MBR 轉換至 GPT。 在命令列中，輸入下列命令：**MBR2GPT /convert /disk:0 /AllowFullOS**。 您也可以選擇在 Windows PE (而非完整作業系統) 中執行 MBR2GPT.EXE 工具。 若要這麼做，您可以在執行 MBR2GPT.EXE 工具的步驟之前，新增將電腦重新啟動至 WinPE 的步驟，並從命令列移除 /AllowFullOS 選項。 如需工具和可用選項的相關詳細資料，請參閱 [MBR2GPT.EXE (英文)](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt)。
   2. 新增啟動 OEM 工具的步驟，以將韌體從 BIOS 轉換成 UEFI。 這通常會是「執行命令列」工作順序步驟，其中包含啟動 OEM 工具的命令列。
   3. 在 [一般] 中，新增 [重新啟動電腦] 步驟。 如需指定重新啟動後要執行的項目，請選取 [目前安裝的預設作業系統]。
3. 部署工作順序。
