---
title: "服務連接工具 | Microsoft Docs"
description: "了解這個工具可讓您連線到 Configuration Manager 雲端服務手動上傳使用資訊。"
ms.custom: na
ms.date: 4/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
caps.latest.revision: "11"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0da80521bf223a765c3731f8ad59623d85a4c9fa
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-service-connection-tool-for-system-center-configuration-manager"></a>使用 System Center Configuration Manager 的服務連接工具

*適用於：System Center Configuration Manager (最新分支)*

在您的服務連接點處於離線模式時，或在 Configuration Manager 站台系統伺服器未連線到網際網路時，使用**服務連線工具**。 這個工具可以協助您讓站台隨時取得 Configuration Manager 的最新更新。  

執行時，工具會手動連線到 Configuration Manager 雲端服務以上傳您階層的使用資訊，以及下載更新。 必須先上傳使用資料，才能啟用雲端服務來提供您部署的正確更新。  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>使用服務連接工具的必要條件
必要條件和已知問題如下。

**必要條件：**

-   您已安裝服務連接點，並且將它設為 **[離線，需要時連線]**。  

-   這個工具必須從命令提示字元執行。  

-   執行此工具的每部電腦 (服務連接點電腦，以及連線到網際網路的電腦)，都必須是 x64 系統且已安裝下列項目：  

    -   **Visual C++ 可轉散發** x86 檔案與 x64 檔案。   Configuration Manager 預設會將 x64 版本安裝在裝載服務連接點的電腦上。  

         若要下載 Visual C++ 檔案的複本，請瀏覽 Microsoft 下載中心的 [適用於 Visual Studio 2013 的 Visual C++ 可轉散發套件](http://www.microsoft.com/download/details.aspx?id=40784) 。  

    -   .NET Framework 4.5.2 或更新版本。  

-   您用來執行此工具的帳戶必須具有下列權限：
    -   裝載服務連接點之電腦 (此工具執行所在的電腦) 的**本機系統管理員** 權限。
    -   站台資料庫的**讀取** 權限。  



-   您將需要一個擁有足夠可用空間的 USB 磁碟機來儲存檔案和更新 (或其他可在服務連接點電腦之間傳輸檔案的方法)，以及一部能夠存取網際網路的電腦。 (此案例假設您的站台和受管理電腦未直接連線到網際網路)。  



## <a name="use-the-service-connection-tool"></a>使用服務連接工具  

 您可在 **%path%\smssetup\tools\ServiceConnectionTool** 資料夾的 Configuration Manager 安裝媒體中，找到服務連接工具 (**serviceconnectiontool.exe**)。 一律使用符合所使用 Configuration Manager 版本的服務連接工具。


 在這個程序中，命令列範例會使用下列檔案名稱和資料夾位置 (您不需要使用這些路徑和檔案名稱，可以改用符合您環境和喜好設定的替代項目)：  

-   用於儲存資料的 USB 隨身碟路徑，以便在伺服器之間傳輸：**D:\USB\\**  

-   包含從站台匯出之資料的 .cab 檔案名稱：**UsageData.cab**  

-   空資料夾的名稱，您可在其中儲存下載的 Configuration Manager 更新，以便在伺服器之間傳輸： **UpdatePacks**  

在裝載服務連接點的電腦上：  

-   使用系統管理權限開啟命令提示字元，然後將目錄變更為包含 **serviceconnectiontool.exe**的位置。  

     根據預設，您可以在 **%path%\smssetup\tools\ServiceConnectionTool** 資料夾的 Configuration Manager 安裝媒體中找到此工具。 這個資料夾中的所有檔案都必須位在相同的資料夾中，這樣服務連接工具才能運作。  

當您執行下列命令時，工具會準備一個包含使用資訊的 .cab 檔案，並將它複製到您指定的位置。 .cab 檔案中的資料是根據已設定您網站收集的診斷使用資料層級。 (請參閱 [System Center Configuration Manager 的診斷和使用方式資料](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md))。  請執行下列命令來建立 .cab 檔案：  

-   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

您也必須將 ServiceConnectionTool 資料夾及其所有內容複製到 USB 磁碟機，或在您將用於步驟 3 和 4 的電腦上提供此資料。  

### <a name="overview"></a>概觀
**使用服務連接工具有三個主要步驟：**  

1.  **準備**：此步驟會在裝載服務連接點的電腦上執行。 工具在執行時，會將使用方式資料放入 .cab 檔，並將其儲存在 USB 磁碟機 (或指定的其他傳輸位置)。  

2.  **連線**：在這個步驟中，您將於連線到網際網路的遠端電腦上執行工具，以上傳使用方式資料與下載更新。  

3.  **重要**：此步驟會在裝載服務連接點的電腦上執行。 執行時，工具會匯入您的下載並將其新增到您的站台，以便您從 Configuration Manager 主控台檢視及安裝這些更新。  

從版本 1606 開始，當您連接到 Microsoft 時，可以一次上傳多個 .cab 檔案 (每一個從不同階層)，並指定 Proxy 伺服器和 Proxy 伺服器的使用者。   

**若要上傳多個 .cab 檔案：**
 -  將從不同階層匯出的每個 .cab 檔案，放入相同的資料夾。 每個檔案名稱必須是唯一的，您可以視需要手動重新命名。
 -  接著，當您執行要將資料上傳至 Microsoft 的命令時，即可指定包含 .cab 檔案的資料夾 (在 1606 版之前的更新，您一次只能上傳來自單一階層的資料，且此工具會要求您指定資料夾中的 .cab 檔案名稱)。
 -  之後，當您在某階層的服務連接點上執行匯入工作時，工具只會自動匯入該階層的資料。  

**若要指定 Proxy 伺服器：**  
若要指定 Proxy 伺服器，您可以使用下列選用參數 (如需使用這些參數的詳細資訊，請參閱本主題的＜命令列參數＞一節)：
  - **-proxyserveruri [FQDN_of_proxy_sever]**  ：使用這個參數可指定要用於此連線的 Proxy 伺服器。
  -  **-proxyusername [username]**  ：若您必須指定 Proxy 伺服器的使用者，請使用這個參數。



### <a name="to-use-the-service-connection-tool"></a>使用服務連接工具  

1.  在裝載服務連接點的電腦上：  

    -   使用系統管理權限開啟命令提示字元，然後將目錄變更為包含 **serviceconnectiontool.exe**的位置。   

2.  當您執行下列命令時，工具會準備一個包含使用方式資訊的 .cab 檔案，並將它複製到您指定的位置：  

    -   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

    如果您要同時從一個以上的階層上傳 .cab 檔案，則資料夾中的每個 .cab 檔案必須具有唯一的名稱。 針對新增至資料夾的檔案，您可以手動重新命名。

    如果您想要檢視已收集並上傳至 Configuration Manager 雲端服務的使用方式資訊，請執行下列命令，將相同的資料匯出為 .csv 檔案，即可使用類似 Excel 的應用程式來檢視：  

    -   **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3.  準備步驟完成之後，請將 USB 磁碟機 (或透過另一種方法傳送匯出的資料) 移至可存取網際網路的電腦。  

4.  在能夠存取網際網路的電腦上，以系統管理權限開啟命令提示字元，然後將目錄變更到包含  **serviceconnectiontool.exe** 工具複本及該資料夾中其他檔案的位置。  

5.  執行下列命令以開始上傳使用資訊以及下載 Configuration Manager 的更新：  

    -   **serviceconnectiontool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**

    如需此命令列的更多範例，請參閱本主題稍後的[命令列選項](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd)一節。

    > [!NOTE]  
    >  當您執行命令列來連線至 Configuration Manager 雲端服務時，可能會發生與下面類似的錯誤：  
    >   
    >  -   未處理的例外狀況: System.UnauthorizedAccessException:  
    >   
    >      拒絕存取路徑 'C:\  
    >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql'。  
    >   
    > 您可以放心地忽略這個錯誤、關閉錯誤視窗，然後繼續。  

6.  完成下載 Configuration Manager 的更新之後，請將 USB 磁碟機 (或透過另一種方法傳送匯出的資料) 移至裝載服務連接點的電腦。  

7.  在裝載服務連接點的電腦上，使用系統管理權限開啟命令提示字元，並將目錄變更為包含 **serviceconnectiontool.exe**的位置，然後執行下列命令：  

    -   **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8.  匯入完成之後，您可以關閉命令提示字元。 (僅會匯入適用階層的更新)。  

9. 開啟 Configuration Manager 主控台，然後瀏覽至 [系統管理] > [更新與服務]。 已匯入的更新現在可供安裝。 (1702 版之前，[更新與服務] 位於 [系統管理] > [雲端服務] 底下)。

 如需安裝更新的資訊，請參閱[安裝適用於 System Center Configuration Manager 的主控台內更新](../../../core/servers/manage/install-in-console-updates.md)。  

## <a name="bkmk_cmd"></a> 命令列選項  
 若要檢視服務連接點工具的說明資訊，請將命令提示字元開啟到包含工具的資料夾，然後執行命令：  **serviceconnectiontool.exe**。  

|命令列選項|詳細資料|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [drive:][path][filename.cab]**|這個命令會將目前的使用資料儲存到 .cab 檔案中。<br /><br /> 在裝載服務連接點的伺服器上，以 **本機系統管理員** 身分執行這個命令。<br /><br /> 範例：   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [drive:][path] -updatepackdest [drive:][path] -proxyserveruri [FQDN of proxy server] -proxyusername [username]** <br /> <br /> 如果您使用比 1606 更早的 Configuration Manager 版本，就必須指定 .cab 檔案名稱，而且無法使用 Proxy 伺服器的選項。  支援的命令參數如下： <br /> **-connect -usagedatasrc [drive:][path][filename] -updatepackdest [drive:][path]** |此命令會連線至 Configuration Manager 雲端服務，以從指定的位置上傳使用方式資料 .cab 檔案，並下載可用的更新套件和主控台內容。 Proxy 伺服器的選項為選擇性。<br /><br /> 在可連線到網際網路的電腦上，以 **本機系統管理員** 身分執行這個命令。<br /><br /> 不使用 Proxy 伺服器連接的範例： **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> 使用 Proxy 伺服器連接的範例： **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> 如果您使用 1606 之前的版本，就必須指定 .cab 檔案的檔案名稱，而且無法指定 Proxy 伺服器。 請使用下列命令列範例： **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [drive:][path]**|這個命令會匯入先前下載到 Configuration Manager 主控台的更新套件和主控台內容。<br /><br /> 在裝載服務連接點的伺服器上，以 **本機系統管理員** 身分執行這個命令。<br /><br /> 範例：  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [drive:][path][filename.csv]**|這個命令會將使用資料匯出至 .csv 檔案，以供您進行檢視。<br /><br /> 在裝載服務連接點的伺服器上，以 **本機系統管理員** 身分執行這個命令。<br /><br /> 範例： **-export -dest D:\USB\usagedata.csv**|  
