---
title: "遠端管理 Windows 電腦 | Microsoft Docs"
description: "使用 System Center Configuration Manager 管理遠端的 Windows 用戶端電腦。"
ms.custom: na
ms.date: 07/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: aecc4ccfec98932f3988f1ca1fcdc898cd417933
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>如何使用 System Center Configuration Manager 從遠端管理 Windows 用戶端電腦

*適用於：System Center Configuration Manager (最新分支)*

開始使用遠端控制之前，請確定您已檢閱下列主題中的資訊：  

-   [System Center Configuration Manager 中遠端控制的必要條件](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [在 System Center Configuration Manager 中設定遠端控制](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

以下是啟動遠端控制檢視器的三種方式：  

-   在 Configuration Manager 主控台中。  

-   在 Windows 命令提示字元中。  

-   在執行 Configuration Manager 主控台 (位於 **Microsoft System Center** 程式群組) 之電腦的 Windows [開始] 功能表。  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>在 Configuration Manager 主控台從遠端管理用戶端電腦  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [裝置] 或 [裝置集合]。  

3.  選取要遠端管理的電腦，然後在 [首頁] 索引標籤的 [裝置] 群組中，選擇 [開始] > [遠端控制]。  

    > [!IMPORTANT]  
    >  如果用戶端設定 [提示使用者提供遠端控制權限]  設為 [True] ，在遠端電腦使用者對遠端控制提示表示同意前，不會啟動連線。 如需詳細資料，請參閱 [在 System Center Configuration Manager 中設定遠端控制](../../../../core/clients/manage/remote-control/configuring-remote-control.md)。  

4.  [Configuration Manager 遠端控制]  視窗開啟後，您就可以從遠端管理用戶端電腦。 請使用下列選項設定連線。  

    > [!NOTE]  
    >  如果連線的電腦有多個監視器，遠端控制視窗會顯示所有監視器的畫面。  

    -   **檔案 - 連線** - 連線到另一部電腦。 使用遠端控制工作階段時無法使用此選項。  

    -   **檔案 - 中斷連線** - 中斷作用中的遠端控制工作階段連線，但不關閉 [Configuration Manager 遠端控制] 視窗。  

    -   **檔案 - 結束** - 中斷作用中的遠端控制工作階段連線，並關閉 [Configuration Manager 遠端控制] 視窗。  

        > [!NOTE]  
        >  當您中斷遠端控制工作階段的連線時，會刪除您檢視電腦上的 Windows 剪貼簿內容。  

    -   **檢視 - 全螢幕** - 最大化 [Configuration Manager 遠端控制] 視窗。  

        > [!NOTE]  
        >  若要結束全螢幕模式，請按 Ctrl+Alt+Break。  

    -   **檢視 - 配合調整大小** - 縮放遠端電腦的顯示畫面至適合 [Configuration Manager 遠端控制] 視窗的大小。  

    -   **檢視 - 狀態列** - 切換顯示 [Configuration Manager 遠端控制] 視窗的狀態列。  

    -   **動作 - 傳送 Ctrl+Alt+Del 鍵** - 將 Ctrl+Alt+Del 按鍵組合傳送到遠端電腦。  

    -   **動作 - 啟用剪貼簿共用** - 讓您在遠端電腦上複製和貼上項目。 如果變更這個值，您必須重新啟動遠端控制工作階段，變更才會生效。  

        > [!NOTE]  
        >  如果不想在 Configuration Manager 主控台中啟用剪貼簿共用，請在執行主控台的電腦上，將登錄機碼 **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** 的值設成 **0**。  

    -   **動作 - 鎖定遠端鍵盤和滑鼠** - 鎖定遠端鍵盤及滑鼠，以防止使用者操作遠端電腦。  

    -   **說明 - 關於遠端控制** - 顯示檢視器的目前版本。  

5.  當遠端電腦上的使用者按一下 Windows 通知區域的 Configuration Manager **遠端控制**圖示或遠端控制工作階段列上的圖示時，即可檢視遠端控制工作階段的詳細資訊。  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>從 Windows 命令列啟動遠端控制檢視器  

-   在 Windows 命令提示字元中，輸入 *<Configuration Manager 安裝資料夾\>***\AdminConsole\Bin\x64\CmRcViewer.exe**  

CmRcViewer.exe 支援下列命令列選項：  

- *位址* - 指定 NetBIOS 名稱、完整的網域名稱 (FQDN) 或您想要連線的用戶端電腦 IP 位址。
- *站台伺服器名稱* - 指定要傳送遠端控制工作階段狀態相關訊息的目標 System Center Configuration Manager 站台伺服器名稱。
- **/?** - 顯示遠端控制檢視器的命令列選項。  
     
**範例：CmRcViewer.exe** *<位址\>* *<\\\站台伺服器名稱>*  
