---
title: "自訂開機映像 - Configuration Manager | Microsoft Docs"
description: "了解使用 Configuration Manager 或部署映像服務與管理 (DISM) 命令列工具來自訂開機映像的數種方式。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: ab2ecb64c9c80b4effed79ba08769c99473db0c4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="customize-boot-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 自訂開機映像

*適用於：System Center Configuration Manager (最新分支)*

Configuration Manager 的每個版本都可支援特定版本的 Windows 評定及部署套件 (Windows ADK)。 如果開機映像是以支援的 Windows ADK 版本中的 Windows PE 版本為基礎，您可以在 Configuration Manager 主控台中處理或自訂這些開機映像。 您必須使用其他方法來自訂其他開機映像，例如使用屬於 Windows AIK 和 Windows ADK 一部分的部署映像服務與管理 (DISM) 命令列工具。  

 以下提供 Windows ADK 的支援版本、可從 Configuration Manager 主控台自訂之開機映像所依據的 Windows PE 版本，以及您可以使用 DISM 自訂然後新增映像到 Configuration Manager 之開機映像所依據的 Windows PE 版本。  

-   **Windows ADK 版本**  

     Windows ADK for Windows 10  

-   **可從 Configuration Manager 主控台自訂之開機映像的 Windows PE 版本**  

     Windows PE 10  

-   **無法從 Configuration Manager 主控台自訂之開機映像的支援 Windows PE 版本**  

     Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

     <sup>1</sup> 只有當開機映像以 Windows PE 3.1 為基礎時，您才能將開機映像新增至 Configuration Manager。 請安裝適用於 Windows 7 SP1 的 Windows AIK 補充元件，以便使用適用於 Windows 7 SP1 的 Windows AIK 補充元件 (以 Windows PE 3.1 為基礎) 來升級適用於 Windows 7 的 Windows AIK (以 Windows PE 3 為基礎)。 您可以從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=5188)下載適用於 Windows 7 SP1 的 Windows AIK 補充元件。  

     例如，當您有 Configuration Manager 時，便可從 Configuration Manager 主控台，使用適用於 Windows 10 的 Windows ADK (以 Windows PE 10 為基礎) 來自訂開機映像。 不過，若支援以 Windows PE 5 為基礎的開機映像，您必須從不同的電腦自訂開機映像，並使用與 Windows ADK for Windows 8 一起安裝的 DISM 版本。 接著，您可以將開機映像新增到 Configuration Manager 主控台。  

 本主題中的程序示範如何使用下列 Windows PE 套件，將 Configuration Manager 所需的選用元件新增到開機映像：  

-   **WinPE-WMI**：新增 Windows Management Instrumentation (WMI) 支援。  

-   **WinPE-Scripting**：新增 Windows Script Host (WSH) 支援。  

-   **WinPE-WDS-Tools**：安裝 Windows 部署服務工具。  

 另外還有其他可以新增的 Windows PE 封裝。 下列資源提供您可新增到開機映像之選用元件的詳細資訊。  

-   對於 Windows PE 5，請參閱 [WinPE：新增封裝 (選擇性元件參考)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)  

-   如果是 Windows PE 3.1，請參閱 Windows 7 TechNet 文件庫中的 [將封裝新增至 Windows PE 映像](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) 主題。  

> [!NOTE]
>當您從包含您所新增之工具的自訂開機映像開機進入 WinPE，您可以從 WinPE 開啟命令提示字元，然後輸入工具的檔案名稱來執行它。 這些工具的位置會自動新增到路徑變數中。 唯有在開機映像內容的 [自訂] 索引標籤上，選取 [啟用命令支援 (僅限測試)] 設定時，才可新增命令提示字元。

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>自訂使用 Windows PE 5 的開機映像  
 若要自訂使用 Windows PE 5 的開機映像，您必須安裝 Windows ADK，並使用 DISM 命令列工具來掛接開機映像、新增選用的元件和驅動程式，以及認可對開機映像的變更。 請使用下列程序來自訂開機映像。  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>自訂使用 Windows PE 5 的開機映像  

1.  在沒有其他 Windows AIK 或 Windows ADK 版本且未安裝任何 Configuration Manager 元件的電腦上安裝 Windows ADK。  

2.  請從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=39982)下載適用於 Windows 8.1 的 Windows ADK。  

3.  將開機映像 (wimpe.wim) 從 Windows AIK 安裝資料夾 (例如 <安裝路徑>\Windows Kits\\<版本>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<x86 或 amd64>\\<地區設定>) 複製到您要自訂開機映像之電腦上的目的地資料夾。 本程序使用 C:\WinPEWAIK 作為目的地資料夾名稱。  

4.  使用 DISM 將開機映像掛接到本機 Windows PE 資料夾。 例如，請輸入下列命令列：  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     其中 C:\WinPEWAIK 是包含開機映像的資料夾，而 C:\WinPEMount 是掛接資料夾。  

    > [!NOTE]
    >  如需 DISM 的詳細資訊，請參閱 Windows 8.1 和 Windows 8 TechNet 文件庫中的 [DISM - Deployment Image Servicing and Management Technical Reference (DISM - 部署映像服務與管理技術參照)](http://technet.microsoft.com/library/hh824821.aspx) 主題。

5.  在您掛接開機映像之後，請使用 DISM 將選用元件新增到開機映像。 在 Windows PE 5 中，64 位元的選用元件位於 <安裝路徑>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs。  

    > [!NOTE]
    >  這個程序針對選用元件使用下列位置：C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs。 依據您為 Windows ADK 選擇的版本和安裝選項，您使用的路徑可能不同。  

     輸入下列命令以新增選用元件：  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** <地區設定*\>* **\WinPE-SecureStartup_** <地區設定*\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** <地區設定*\>* **\WinPE-WMI_** <地區設定*\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** <地區設定*\>* **\WinPE-Scripting** <地區設定*\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** <地區設定*\>* **\WinPE-WDS-Tools_** <地區設定*\>* **.cab"**  

     其中 C:\WinPEMount 是掛接資料夾，locale 是元件的地區設定。 例如，若是 **en-us** 地區設定，您應輸入：  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

    > [!TIP]
    >  如需您可新增到開機映像之選用元件的詳細資訊，請參閱 Windows 8.1 和 Windows 8 TechNet 文件庫中的 [Windows PE 選用元件參考](http://technet.microsoft.com/library/hh824926.aspx) 主題。  

6.  視需要使用 DISM 將特定驅動程式新增到開機映像。 請輸入下列命令將驅動程式新增到開機映像：  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *驅動程式 .inf 檔案的路徑* **>**  

     其中 C:\WinPEMount 是掛接資料夾。  

7.  輸入下列命令以取消掛接開機映像檔案並認可變更。  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     其中 C:\WinPEMount 是掛接資料夾。  

8.  將更新的開機映像新增到 Configuration Manager ，讓您可以在工作順序中使用它。 請使用下列步驟來匯入更新的開機映像：  

    1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

    2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

    3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增開機映像]  ，啟動 [新增開機映像精靈]。  

    4.  在 [資料來源]  頁面上指定下列選項，然後按 [下一步] 。  

        -   在 [路徑]  方塊中，指定更新的開機映像檔案的路徑。 指定的路徑必須是使用 UNC 格式的有效網路路徑。 例如：**\\\\<**伺服器名稱**>\\<**WinPEWAIK 共用**>\winpe.wim**。  

        -   從 [開機映像]  下拉式清單選取開機映像。 如果 WIM 檔包含多個開機映像，每個映像都會列出。  

    5.  在 [一般]  頁面指定下列選項，然後按 [下一步] 。  

        -   在 [名稱]  方塊中，為開機映像指定唯一的名稱。  

        -   在 [版本]  方塊中，指定開機映像的版本號碼。  

        -   在 [註解]  方塊中，指定有關如何使用開機映像的簡單描述。  

    6.  完成精靈。  

9. 您可以在開機映像中啟用命令殼層，以便在 Windows PE 中對開機映像進行偵錯和疑難排解。 請使用下列步驟來啟用命令殼層。  

    1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

    2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

    3.  在清單中找出新的開機映像，並識別該映像的套件識別碼。 您可以在開機映像的 [映像識別碼]  欄中找到套件識別碼。  

    4.  從命令提示字元輸入 **wbemtest** ，開啟 Windows Management Instrumentation 測試器。  

    5.  在 [命名空間] 中輸入 \\\\<SMS 提供者電腦>\root\sms\site_<站台碼>，然後按一下 [連線]。  

    6.  按一下 **[開啟執行個體]**，輸入 **sms_bootimagepackage.packageID="<封裝識別碼\>"**，然後按一下 **[確定]**。 針對「套件識別碼」，請輸入您在步驟 3 中識別的值。  

    7.  按一下 [重新整理物件] ，然後在 [內容]  窗格中按一下 [EnableLabShell]  。  

    8.  按一下 [編輯內容] ，將值變更為 **TRUE**，然後按一下 [儲存內容] 。  

    9. 按一下 [儲存物件] ，然後結束 Windows Management Instrumentation 測試器。  

10. 您必須先將開機映像發佈到發佈點、發佈點群組或與發佈點群組相關聯的集合，才能在工作順序中使用開機映像。 請使用下列步驟來發佈開機映像。  

    1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

    2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

    3.  按一下步驟 3 中識別的開機映像。  

    4.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [更新發佈點] 。  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>自訂使用 Windows PE 3.1 的開機映像  
 若要自訂使用 WinPE 3.1 的開機映像，您必須安裝 Windows AIK、安裝適用於 Windows 7 SP1 的 Windows AIK 補充元件，並使用 DISM 命令列工具來掛接開機映像、新增選用的元件和驅動程式，以及認可對開機映像的變更。 請使用下列程序來自訂開機映像。  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>自訂使用 Windows PE 3.1 的開機映像  

1.  在沒有其他 Windows AIK 或 Windows ADK 版本且未安裝任何 Configuration Manager 元件的電腦上安裝 Windows AIK。 請從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=5753)下載 Windows AIK。  

2.  在步驟 1 的電腦上安裝適用於 Windows 7 SP1 的 Windows AIK 補充元件。 請從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=5188)下載適用於 Windows 7 SP1 的 Windows AIK 補充元件。  

3.  將開機映像 (wimpe.wim) 從 Windows AIK 安裝資料夾 (例如 <安裝路徑>\Windows AIK\Tools\PETools\amd64\\) 複製到您要自訂開機映像之電腦上的資料夾。 本程序使用 C:\WinPEWAIK 作為資料夾名稱。  

4.  使用 DISM 將開機映像掛接到本機 Windows PE 資料夾。 例如，請輸入下列命令列：  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     其中 C:\WinPEWAIK 是包含開機映像的資料夾，而 C:\WinPEMount 是掛接資料夾。  

    > [!NOTE]
    >  如需 DISM 的詳細資訊，請參閱 Windows 7 TechNet 文件庫中的 [部署映像服務與管理技術參照](http://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx) 主題。  

5.  在您掛接開機映像之後，請使用 DISM 將選用元件新增到開機映像。 例如，在 Win PE 3.1 中，選用元件位於 <安裝路徑>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\。  

    > [!NOTE]
    >  這個程序針對選用元件使用下列位置：C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs。 依據您為 Windows AIK 選擇的版本和安裝選項，您使用的路徑可能不同。  

     輸入下列命令以新增選用元件：  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** <地區設定*\>* **\winpe-wmi_** <地區設定*\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** <地區設定*\>* **\winpe-scripting_** <地區設定*\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** <地區設定*\>* **\winpe-wds-tools_** <地區設定*\>* **.cab"**  

     其中 C:\WinPEMount 是掛接資料夾，locale 是元件的地區設定。 例如，若是 **en-us** 地區設定，您應輸入：  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

    > [!TIP]
    >  如需可新增到開機映像之不同封裝的詳細資訊，請參閱 Windows 7 TechNet 文件庫中的 [將封裝新增至 Windows PE 映像](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) 主題。  

6.  視需要使用 DISM 將特定驅動程式新增到開機映像。 如有需要，請輸入下列命令將驅動程式新增到開機映像：  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *驅動程式 .inf 檔案的路徑* **>**  

     其中 C:\WinPEMount 是掛接資料夾。  

7.  輸入下列命令以取消掛接開機映像檔案並認可變更。  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     其中 C:\WinPEMount 是掛接資料夾。  

8.  將更新的開機映像新增到 Configuration Manager ，讓您可以在工作順序中使用它。 請使用下列步驟來匯入更新的開機映像：  

    1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

    2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

    3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增開機映像]  ，啟動 [新增開機映像精靈]。  

    4.  在 [資料來源]  頁面上指定下列選項，然後按 [下一步] 。  

        -   在 [路徑]  方塊中，指定更新的開機映像檔案的路徑。 指定的路徑必須是使用 UNC 格式的有效網路路徑。 例如：**\\\\<**伺服器名稱**>\\<**WinPEWAIK 共用**>\winpe.wim**。  

        -   從 [開機映像]  下拉式清單選取開機映像。 如果 WIM 檔包含多個開機映像，每個映像都會列出。  

    5.  在 [一般]  頁面指定下列選項，然後按 [下一步] 。  

        -   在 [名稱]  方塊中，為開機映像指定唯一的名稱。  

        -   在 [版本]  方塊中，指定開機映像的版本號碼。  

        -   在 [註解]  方塊中，指定有關如何使用開機映像的簡單描述。  

    6.  完成精靈。  

9. 您可以在開機映像中啟用命令殼層，以便在 Windows PE 中對開機映像進行偵錯和疑難排解。 請使用下列步驟來啟用命令殼層。  

    1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

    2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

    3.  在清單中找出新的開機映像，並識別該映像的套件識別碼。 您可以在開機映像的 [映像識別碼]  欄中找到套件識別碼。  

    4.  從命令提示字元輸入 **wbemtest** ，開啟 Windows Management Instrumentation 測試器。  

    5.  在 [命名空間] 中輸入 \\\\<SMS 提供者電腦>\root\sms\site_<站台碼>，然後按一下 [連線]。  

    6.  按一下 **[開啟執行個體]**，輸入 **sms_bootimagepackage.packageID="<封裝識別碼\>"**，然後按一下 **[確定]**。 針對「套件識別碼」，請輸入您在步驟 3 中識別的值。  

    7.  按一下 [重新整理物件] ，然後在 [內容]  窗格中按一下 [EnableLabShell]  。  

    8.  按一下 [編輯內容] ，將值變更為 **TRUE**，然後按一下 [儲存內容] 。  

    9. 按一下 [儲存物件] ，然後結束 Windows Management Instrumentation 測試器。  

10. 您必須先將開機映像發佈到發佈點、發佈點群組或與發佈點群組相關聯的集合，才能在工作順序中使用開機映像。 請使用下列步驟來發佈開機映像。  

    1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

    2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

    3.  按一下步驟 3 中識別的開機映像。  

    4.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [更新發佈點] 。  
