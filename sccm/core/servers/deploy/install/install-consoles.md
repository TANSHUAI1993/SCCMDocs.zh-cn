---
title: "安裝主控台 | Microsoft Docs"
description: "閱讀如何安裝 Configuration Manager 主控台以連線至管理中心網站或主要站台。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 88ecbc48fd03ce988f04408d0378844cbed1de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="install-the-system-center-configuration-manager-console"></a>安裝 System Center Configuration Manager 主控台

*適用於：System Center Configuration Manager (最新分支)*

系統管理員會使用 System Center Configuration Manager 主控台來管理 Configuration Manager 環境。 每個 Configuration Manager 主控台都可以連線至管理中心網站或主要站台。 不過，您無法將 Configuration Manager 主控台連線至次要站台。

> [!NOTE]  
>  執行主控台的系統管理員所看到的物件，取決於指派給其使用者帳戶的權限。 如需以角色為基礎之系統管理的詳細資訊，請參閱 [System Center Configuration Manager 以角色為基礎之系統管理的基礎](../../../../core/understand/fundamentals-of-role-based-administration.md)。  

 您可以在站台伺服器安裝期間透過 [安裝精靈] 安裝 Configuration Manager 主控台，也可以執行使用 [安裝精靈] 的獨立安裝應用程式。  

 請使用以下程序，利用獨立應用程式安裝 Configuration Manager 主控台。  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>使用安裝精靈安裝 Configuration Manager 主控台  

1.  確定您符合這些需求：  

    -  您具有執行主控台之電腦上的**本機系統管理員**權限。  

    -   您具有 Configuration Manager 主控台安裝檔位置的**讀取**權限。  

2.  移至其中一個位置︰  

    -   在站台伺服器上，移至 **<*Configuration Manager 站台伺服器安裝路徑*>\Tools\ConsoleSetup**。  

    -   從 Configuration Manager 來源媒體中，移至 **<*Configuration Manager 原始程式碼*>\Smssetup\Bin\I386**。  

    > [!TIP]  
    >  最佳做法是從站台伺服器，而不是從 System Center Configuration Manager 安裝媒體起始 Configuration Manager 主控台安裝。 站台伺服器安裝方法會將 Configuration Manager 主控台安裝檔案與站台的支援語言套件，複製到 **Tools\ConsoleSetup** 子資料夾。 不論站台伺服器上支援的語言為何，或電腦上執行的作業系統語言設定為何，從安裝媒體安裝 Configuration Manager 主控台一律都會安裝英文版。 您也可以選擇將 **ConsoleSetup** 資料夾複製到替代位置，以啟動安裝。

3.  若要開啟 Configuration Manager 主控台安裝精靈，請按兩下 **consolesetup.exe**。  

    > [!IMPORTANT]  
    >  請一律使用 consolesetup.exe 安裝 Configuration Manager 主控台。 雖然 Configuration Manager 主控台可藉由執行 adminconsole.msi 加以安裝，但此方法不會執行必要條件或相依性檢查，且安裝可能會不正確。  

4.  在精靈中，選取 [下一步]。  

5.  在 [站台伺服器] 頁面上，輸入 Configuration Manager 主控台要連線之站台伺服器的完整網域名稱 (FQDN)。  

6.  在 [安裝資料夾] 頁面上，輸入 Configuration Manager 主控台的安裝資料夾。 資料夾路徑結尾不可有空格，路徑中不可有 Unicode 字元。  

7.  在 [客戶經驗改進計畫] 頁面上，選取是否要加入客戶經驗改進計畫 (CEIP)。  

8.  在 [安裝準備就緒] 頁面上，選取 [安裝] 即可安裝 Configuration Manager 主控台。  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>從命令提示字元安裝 Configuration Manager 主控台  

1.  在安裝 Configuration Manager 主控台的伺服器上，開啟命令提示字元視窗，並移至下列其中一個位置：  

    -   **<*Configuration Manager 站台伺服器安裝路徑*>\Tools\ConsoleSetup**  

    -   **<*Configuration Manager 安裝媒體*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  不論電腦上執行的作業系統語言設定為何，當您從命令提示字元安裝 Configuration Manager 主控台時，一律都會安裝英文版。 若要安裝非英文版的 Configuration Manager 主控台，您必須[使用安裝精靈安裝 Configuration Manager 主控台](#to-install-the-configuration-manager-console-by-using-the-setup-wizard)。  

2.  在命令提示字元中，輸入 **consolesetup.exe**。 選擇下列命令列選項。  

|  命令列選項     | 說明     |
  | :------------- | :------------- |
  |/q|自動安裝 Configuration Manager。 只有在使用此選項時，才需要 **EnableSQM**、 **TargetDir**和 **DefaultSiteServerName** 選項。|  
  |/uninstall|解除安裝 Configuration Manager 主控台。 當您搭配 **/q** 選項使用時，必須指定此選項。|  
  |LangPackDir|指定包含語言檔案的資料夾路徑。 您可以使用 **安裝程式下載程式** 來下載語言檔案。 如果未使用此選項，則安裝程式會在目前資料夾中尋找語言資料夾。 如果沒有找到語言資料夾，則安裝程式只會繼續安裝英文版。 如需詳細資訊，請參閱[安裝程式下載程式](setup-downloader.md)。|  
  |TargetDir|指定安裝資料夾以安裝 Configuration Manager 主控台。 只有在使用 **/q** 選項時，才需要此選項。|  
  |EnableSQM|指定是否加入客戶經驗改進計畫 (CEIP)。 使用 **1** 的值加入 CEIP，**0** 的值則不加入計畫。 只有在使用 **/q** 選項時，才需要此選項。|  
  |DefaultSiteServerName|指定主控台開啟時所連線的網站伺服器 FQDN。 只有在使用 **/q** 選項時，才需要此選項。|  


  **範例：**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
