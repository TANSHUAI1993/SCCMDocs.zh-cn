---
title: "命令列安裝 | Microsoft Docs"
description: "了解如何在命令提示字元執行 System Center Configuration Manager 安裝程式，以進行各種站台安裝。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8ff48b08d1abb7481592c0ea076d4efa15c3d8ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>使用命令列來安裝 System Center Configuration Manager 站台

*適用對象：System Center Configuration Manager (最新分支)*

 您可以在命令提示字元執行 System Center Configuration Manager 安裝程式，以安裝各種站台類型。

## <a name="supported-tasks-for-command-line-installations"></a>支援的命令列安裝工作
 這種執行安裝程式的方法支援下列站台安裝和站台維護工作︰

-   **從命令提示字元安裝管理中心網站或主要站台**  
  檢視[安裝程式的命令列選項](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

-  **修改管理中心網站或主要站台所使用的語言**  
    若要從命令提示字元修改站台所安裝的語言 (包括行動裝置語言)，您必須：  

     -   從站台伺服器的 **&lt;ConfigurationManager 安裝路徑\>\Bin\X64** 執行安裝程式。
     -   使用 **/MANAGELANGS** 命令列選項。
     -   指定語言指令碼檔，其會指定您要新增或移除的語言。  

    例如，使用下列命令語法：**setupwpf.exe /MANAGELANGS &lt;語言指令檔\>**  

    若要建立語言指令檔，請使用[用以管理語言的命令列選項](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)中的資訊  

-  **使用安裝指令檔進行自動站台安裝或站台復原**  
    您可以使用安裝指令碼從命令提示字元執行安裝程式，然後執行自動站台安裝。 您也可以使用此選項來復原站台。    

    若要搭配指令碼與安裝程式一起使用：  

    -   使用命令列選項 **/SCRIPT** 執行安裝程式，並指定指令碼檔。  

    -   必須使用必要的金鑰與值設定指令碼檔。  

    針對自動安裝管理中心網站或主要站台，指令碼檔必須具有下列區段：  

    -   識別    
    -   選項    
    -   SQLConfigOptions    
      -   HierarchyOptions    
    -   CloudConnectorOptions   

    若要復原站台，您也必須包括指令碼檔的下列區段：  

    -   識別  
    -   復原

如需詳細資訊，請參閱 [Configuration Manager 的自動站台復原](/sccm/protect/understand/unattended-recovery)。  

如需在自動安裝指令碼檔中使用的索引鍵和值清單，請參閱[自動安裝指令碼檔案索引鍵](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended)。  

## <a name="about-the-command-line-script-file"></a>關於命令列指令檔  
 若要自動安裝 Configuration Manager，您可以使用命令列選項 **/SCRIPT** 執行安裝程式，並指定包含安裝選項的指令碼檔。 使用這種方法來支援下列工作：  

-   安裝管理中心網站  
-   安裝主要站台  
-   安裝 Configuration Manager 主控台  
-   復原站台  

> [!NOTE]  
>  您無法使用自動執行指令碼檔，將評估網站升級為 Configuration Manager 的授權安裝。  

### <a name="the-cdlatest-key-name"></a>CDLatest 索引鍵名稱
當您使用 CD.Latest 資料夾中的媒體，來執行下列四個安裝選項的指令碼式安裝時，您的指令碼必須包含值為 **1** 的 **CDLatest** 索引鍵：
- 安裝新的管理中心網站
- 安裝新的主要站台
- 復原管理中心網站
- 復原主要站台

此值不支援搭配從 Microsoft 大量授權網站取得的安裝媒體使用。
如需如何在指令碼檔案中使用此索引鍵名稱，請參閱[命令列選項](/sccm/core/servers/deploy/install/command-line-options-for-setup)。



### <a name="create-the-script"></a>建立指令碼
當您[執行安裝程式以透過使用者介面安裝站台](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)時，會自動建立安裝指令碼。  確認精靈之 [摘要] 頁面上的設定時，會發生下列情況：  

-   安裝程式會建立指令碼 **%TEMP%\ConfigMgrAutoSave.ini**。  您可以在使用前先重新命名這個檔案，但它副檔名必須保留為 .ini 檔案。  
-   自動安裝指令碼包含您在精靈中選取的設定。  
-   建立指令碼後，您就可以修改指令碼以安裝階層中的其他網站。  
-   然後即可使用此指令碼來執行 Configuration Manager 的自動安裝。  

指令碼檔提供的資訊與 [安裝精靈] 提示的資訊相同，但沒有預設值。   
您必須指定適用於您所使用之安裝類型的安裝識別碼的所有值。   

當安裝程式建立自動安裝指令碼時，會填入您在安裝期間輸入的產品金鑰值。 這可以是有效的產品金鑰，若是安裝 Configuration Manager 的評估版，則為 **EVAL**。 指令碼中所填入的產品金鑰值，可用來完成先決條件檢查。   

當安裝程式啟動實際的網站安裝時，會再次寫入自動建立的指令碼，以清除所建立指令碼中的產品金鑰值。 為新站台的自動安裝使用指令碼之前，可以編輯指令碼，以提供有效的產品金鑰，或指定 Configuration Manager 的評估安裝。  

### <a name="section-names-key-names-and-values"></a>區段名稱、索引鍵名稱與值
指令碼包含區段名稱、索引鍵名稱與值。 請注意下列資訊：
-   根據您進行指令碼處理時的安裝類型，所需的區段索引鍵名稱也不同。
-   各區段中索引鍵的順序與檔案內區段的順序都不重要。     
-   索引鍵不區分大小寫。  
-   提供索引鍵的值時，索引鍵名稱後必須加上等號 (=) 與索引鍵的值。    

> [!TIP]  
>  若要檢視一組完整選項，請參閱[安裝程式和指令碼的命令列選項](../../../../core/servers/deploy/install/command-line-options-for-setup.md)。  

## <a name="use-the-script-setup-command-line-option"></a>使用 /SCRIPT 安裝命令列選項

-   您必須使用安裝指令碼檔，並在 **/SCRIPT** 安裝命令列選項後面指定檔案名稱。 請注意下列資訊：   
    -   檔案名稱的副檔名必須是 **.ini**。  
    -   當您參考命令提示字元的安裝設定檔時，必須提供檔案的完整路徑。 例如，若您將安裝初始設定檔命名為 Setup.ini，並將其儲存在 C:\Setup 資料夾中，則請在命令提示字元輸入：**setup /script c:\setup\setup.ini**。  

-   執行安裝程式的帳戶，在電腦上必須具有 [系統管理員] 權限。 使用自動指令碼執行安裝程式時，請使用 [以系統管理員身分執行] 選項開啟 [命令提示字元] 視窗。   
