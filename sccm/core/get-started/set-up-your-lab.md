---
title: "設定 System Center Configuration Manager 實驗室 | Microsoft Docs"
description: "設定實驗室，以使用模擬實際活動來評估 Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
caps.latest.revision: "11"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 11f5d0c3c61d675a8182e985f82e6af363b34592
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-your-system-center-configuration-manager-lab"></a>設定 System Center Configuration Manager 實驗室

*適用於：System Center Configuration Manager (最新分支)*

遵循本主題中的指引可讓您設定實驗室，以使用模擬實際活動來評估 Configuration Manager 。  

##  <a name="BKMK_LabCore"></a> 核心元件  
 設定 System Center Configuration Manager 的環境需要一些核心元件，才能支援 Configuration Manager 安裝。    

-   **實驗室環境會使用 Windows Server 2012 R2** (在其中安裝 System Center Configuration Manager)。  

     您可以從 [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012) 下載 Windows Server 2012 R2 評估版。  

     請考慮修改或停用 Internet Explorer 增強式安全性設定，以更輕鬆地存取這些練習過程中所參考的一些下載項目。 如需深入了解 WCF，請檢閱 [Internet Explorer：增強式安全性設定](https://technet.microsoft.com/en-us/library/dd883248\(v=ws.10\).aspx) 。  

-   **實驗室環境會使用 SQL Server 2012 SP2** (適用於站台資料庫)。  

     您可以從 [Microsoft 下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=29066)下載 SQL Server 2012 評估版。  

     SQL Server 具有必須符合才能與 System Center Configuration Manager 搭配使用的[支援的 SQL Server 版本](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions)。  

    -   Configuration Manager 需要 64 位元版本的 SQL Server 才能裝載站台資料庫。  

    -   **SQL_Latin1_General_CP1_CI_AS** 作為 **SQL 定序** 類別。  

    -   **Windows 驗證**，而非 [SQL 驗證](https://technet.microsoft.com/en-us/library/ms144284.aspx)，而非 is required.  

    -   需要專用 **SQL Server 執行個體**。  

    -   不會限制 SQL Server 的**系統可定址記憶體**。  

    -   設定 **SQL Server 服務帳戶**，使用**網域本機使用者**帳戶執行。  

    -   您必須安裝 **SQL Server Reporting Services**。  

    -   **站台間通訊** 會使用預設連接埠 TCP 4022 上的 SQL Server Service Broker。  

    -   SQL Server 資料庫引擎與所選取 Configuration Manager 站台系統角色之間的**站台內通訊**會使用預設連接埠 TCP 1433。  

-   **網域控制站會使用 Windows Server 2008 R2** (其已安裝 Active Directory 網域服務)。 網域控制站也會當成 DHCP 和 DNS 伺服器的主機運作，以與完整網域名稱搭配使用。  

     如需其他資訊，請檢閱本 [Active Directory 網域服務概觀](https://technet.microsoft.com/en-us/library/hh831484)。  

-   **Hyper-V 與一些虛擬機器搭配使用**，確認這些練習中採取的管理步驟如預期地運作。 建議最少使用三部已安裝 Windows 7 (或更新版本) 的虛擬機器。  

     如需其他資訊，請檢閱本 [Hyper-V 概觀](https://technet.microsoft.com/en-us/library/hh831531.aspx)。  

-   **系統管理員權限** 。  

    -   Configuration Manager 需要具有 Windows Server 環境內本機權限的系統管理員  

    -   Active Directory 需要具有架構修改權限的系統管理員  

    -   虛擬機器需要機器本身的本機權限  

雖然這個實驗室不需要，但是您可以檢閱 [System Center Configuration Manager 的支援設定](../../core/plan-design/configs/supported-configurations.md)以取得 System Center Configuration Manager 實作需求的其他資訊。 請參閱軟體版本文件，而非這裡所參考的文件。  

安裝所有這些元件之後，還必須採取其他步驟，才能設定 Configuration Manager 的 Windows 環境：  

###  <a name="BKMK_LabADPrep"></a> 準備實驗室的 Active Directory 內容  
 在本實驗室中，您將建立安全性群組，然後在其中加入網域使用者。  

-   安全性群組： **Evaluation**  

    -   群組領域： **Universal**  

    -   群組類型： **Security**  

-   網域使用者： **ConfigUser**  

     在正常情況下，您不會將通用存取權授與環境內的所有使用者。 您與此使用者如此做，才能簡化實驗室的上線作業。  

下列程序列出讓 Configuration Manager 用戶端查詢 Active Directory 網域服務以找到站台資源所需的後續步驟。  

###  <a name="BKMK_CreateSysMgmtLab"></a> 建立系統管理容器  
 Configuration Manager 不會在擴充架構時，自動在 Active Directory 網域服務中建立必要系統管理容器。 因此，您將為實驗室建立這個項目。 這個步驟將要求您 [安裝 ADSI 編輯](https://technet.microsoft.com/en-us/library/cc773354\(WS.10\).aspx#BKMK_InstallingADSIEdit)。  

 請確定您以具有 Active Directory 網域服務之 [系統]  容器 [建立所有子物件]  權限的帳戶登入。  

##### <a name="to-create-the-system-management-container"></a>建立系統管理容器：  

1.  執行 [ADSI 編輯] ，並連線至網站伺服器所在的網域。  

2.  依序展開 [網域 &lt;電腦完整網域名稱\>] 和 [<辨別名稱\>]，並以滑鼠右鍵按一下 [CN=System]，然後依序按一下 [新增] 和 [物件]。  

3.  在 [建立物件]  對話方塊中，選取 [容器] ，然後按 [下一步] 。  

4.  在 [值]  方塊中輸入 **System Management**，然後按一下 [下一步] 。  

5.  按一下 [完成]  完成程序。  

###  <a name="BKMK_SetSecPermLab"></a> 設定系統管理容器的安全性權限  
 請將站台資訊發佈到容器所需的權限授與站台伺服器的電腦帳戶。 您也將針對這個工作使用 ADSI 編輯。  

> [!IMPORTANT]  
>  確認您已連線到站台伺服器的網域，再開始進行下列程序。  

##### <a name="to-set-security-permissions-for-the-system-management-container"></a>設定系統管理容器的安全性權限：  

1.  在主控台窗格中，展開**站台伺服器的網域**，並展開 [&lt;DC=伺服器辨別名稱\>]，然後展開 [CN=System]。 以滑鼠右鍵按一下 [CN=System Management] ，然後按一下 [內容] 。  

2.  在 [CN=System Management Properties]  對話方塊中，按一下 [安全性]  索引標籤，然後按一下 [新增]  新增站台伺服器電腦帳戶。 將 [完全控制]  權限授與帳戶。  

3.  按一下 [進階]，並選取站台伺服器的電腦帳戶，然後按一下 [編輯]。  

4.  在 [套用到]  清單中，選取 [此物件及所有子系物件] 。  

5.  按一下 [確定]  關閉 [ADSI 編輯]  主控台並完成程序。  

     如需此程序的其他資訊，請檢閱[擴充 System Center Configuration Manager 的 Active Directory 架構](../../core/plan-design/network/extend-the-active-directory-schema.md)。  

###  <a name="BKMK_ExtADSchLab"></a> 使用 extadsch.exe 延伸 Active Directory 架構  
 您將擴充這個實驗室的 Active Directory 架構，這可讓您以最少的管理成本來使用所有的 Configuration Manager 特性和功能。 延伸 Active Directory 架構是對每個樹系都只能執行一次的整個樹系組態。 永久延伸架構會修改基底 Active Directory 組態中的這組類別和屬性。 這項動作無法復原。 擴充架構可讓 Configuration Manager 存取元件，以允許它在實驗室環境內最有效地運作。  

> [!IMPORTANT]  
>  確定您是使用具有 Schema Admins  安全性群組成員身分的帳戶登入架構主機網域控制站。 嘗試使用替代認證將會失敗。  

##### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>使用 extadsch.exe 延伸 Active Directory 架構：  

1.  建立架構主機網域控制站系統狀態的備份。 如需備份主機網域控制站的詳細資訊，請檢閱 [Windows Server 備份](https://technet.microsoft.com/en-us/library/cc770757.aspx)。  

2.  瀏覽至安裝媒體中的 **\SMSSETUP\BIN\X64** 。  

3.  執行 **extadsch.exe**。  

4.  檢閱位於系統磁碟機的根資料夾中的 **extadsch.log** ，確認已成功延伸架構。  

     如需此程序的其他資訊，請檢閱[擴充 System Center Configuration Manager 的 Active Directory 架構](../../core/plan-design/network/extend-the-active-directory-schema.md)。  

###  <a name="BKMK_OtherTasksLab"></a> 其他必要工作  
 您也需要先完成下列工作，再進行安裝。  

 **建立資料夾來儲存所有下載**  

 在這個練習中，將會有安裝媒體之元件所需的多個下載。 開始任何安裝程序之前，除非您想要解除委任您的實驗室，否則請決定不需要您移動這些檔案的位置。 建議使用具有不同子資料夾來儲存這些下載的單一資料夾。  

 **安裝 .NET 並啟動 Windows Communication Foundation**  

 您將需要安裝兩個 .NET Frameworks：依序安裝 .NET 3.5.1 和 .NET 4.5.2+。 您也將需要啟動 Windows Communication Foundation (WCF)。 WCF 設計成提供分散式運算、廣泛互通性以及服務導向之直接支援的可管理方式，並透過服務導向的程式設計模型來簡化已連線應用程式的開發。 如需深入了解 WCF，請檢閱 [何謂 Windows Communication Foundation？](https://technet.microsoft.com/en-us/subscriptions/ms731082\(v=vs.90\).aspx) 。  

##### <a name="to-install-net-and-activate-windows-communication-foundation"></a>安裝 .NET 並啟動 Windows Communication Foundation：  

1.  開啟 **Server Manager**，然後瀏覽至 [管理] 。 按一下 [新增角色及功能]  開啟 [新增角色及功能精靈]  **Wizard.**。  

2.  檢閱 [開始之前]  面板中所提供的資訊，然後按一下 [下一步] 。  

3.  選取 [角色型或功能型安裝] ，然後按一下 [下一步] 。  

4.  從 [伺服器集區] 中選取您的伺服器，然後按一下 [下一步] 。  

5.  檢閱 [伺服器角色]  面板，然後按一下 [下一步] 。  

6.  新增下列 [功能]  ，方法是從清單中選取它們：  

    -   **.NET Framework 3.5 功能**  

        -   **.NET Framework 3.5 (包含 .NET 2.0 和 3.0)**  

    -   **.NET Framework 4.5 功能**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **WCF 服務**  

            -   **HTTP 啟動**  

            -   **TCP 連接埠共用**  

7.  檢閱 [網頁伺服器角色 (IIS)]  和 [角色服務]  畫面，然後按一下 [下一步] 。  

8.  檢閱 [確認]  畫面，然後按一下 [下一步] 。  

9. 按一下 [安裝]  ，並在 [伺服器管理員]  的 [通知] 窗格中確認正確地完成安裝。  

10. 完成 .NET 基底安裝之後，請瀏覽至 [Microsoft 下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=42643) 來取得 .NET Framework 4.5.2 的 Web 安裝程式。 按一下 [下載]  按鈕，然後 [執行]  安裝程式。 它將自動偵測必要的元件並以您選取的語言進行安裝。  

如需其他資訊，請檢閱下列文章中需要這些 .NET Framework 的原因：  

-   [.NET Framework 版本和相依性](https://technet.microsoft.com/en-us/library/bb822049.aspx)  

-   [.NET Framework 4 RTM 應用程式相容性逐步解說](https://technet.microsoft.com/en-us/library/dd889541.aspx)  

-   [如何：將 ASP.NET Web 應用程式升級至 ASP.NET 4](https://technet.microsoft.com/en-us/library/dd483478\(VS.100\).aspx)  

-   [Microsoft .NET Framework 支援週期原則 FAQ](https://support.microsoft.com/en-us/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)  

-   [CLR Inside Out - 同處理序並存](https://msdn.microsoft.com/en-us/magazine/ee819091.aspx)  

**啟用 BITS、IIS 和 RDC**  

[背景智慧型傳送服務 (BITS)](https://technet.microsoft.com/en-us/library/dn282296.aspx) 用於需要在用戶端與伺服器之間非同步傳送檔案的應用程式。 透過計量前景和背景的傳送流程，BITS 會保留其他網路應用程式的回應能力。 如果中斷傳送工作階段，則也會自動繼續檔案傳送。  

因為這個站台伺服器也會用作管理點，所以您將安裝這個實驗室的 BITS。  

Internet Information Services (IIS) 是彈性可擴充的網頁伺服器，可用來在站台上裝載任何項目。 Configuration Manager 將它用於多個站台系統角色。 如需 IIS 的其他資訊，請檢閱 [System Center Configuration Manager 中的站台系統伺服器網站](../../core/plan-design/network/websites-for-site-system-servers.md)。  

[遠端差異壓縮 (RDC)](https://technet.microsoft.com/en-us/library/cc754372.aspx) 是一組 API，應用程式可用來判斷是否已對一組檔案進行任何變更。 RDC 可讓應用程式僅複寫檔案的變更部分，進而保持最小網路流量。  

##### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>啟用 BITS、IIS 和 RDC 站台伺服器角色：  

1.  在站台伺服器上，開啟 **Server Manager**。 瀏覽至 [管理] 。 按一下 [新增角色及功能]  開啟 [新增角色及功能精靈] 。  

2.  檢閱 [開始之前]  面板中所提供的資訊，然後按一下 [下一步] 。  

3.  選取 [角色型或功能型安裝] ，然後按一下 [下一步] 。  

4.  從 [伺服器集區] 中選取您的伺服器，然後按一下 [下一步] 。  

5.  新增下列 [伺服器角色]  ，方法是從清單中選取它們：  

    -   **網頁伺服器 (IIS)**  

        -   **一般 HTTP 功能**  

            -   **預設文件**  

            -   **目錄瀏覽**  

            -   **HTTP 錯誤**  

            -   **靜態內容**  

            -   **HTTP 重新導向**  

        -   **健全狀況及診斷**  

            -   **HTTP 記錄**  

            -   **記錄工具**  

            -   **要求監視器**  

            -   **追蹤**  

    -   **效能**  

        -   **靜態內容壓縮**  

        -   **動態內容壓縮**  

    -   **Security**  

        -   **要求篩選**  

        -   **基本驗證**  

        -   **用戶端憑證對應驗證**  

        -   **IP 及網域限制**  

        -   **URL 授權**  

        -   **Windows 授權**  

    -   **應用程式開發**  

        -   **.NET 擴充性 3.5**  

        -   **.NET 擴充性 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **ISAPI 擴充程式**  

        -   **ISAPI 篩選器**  

        -   **伺服器端包含**  

    -   **FTP 伺服器**  

        -   **FTP 服務**  

    -   **管理工具**  

        -   **IIS 管理主控台**  

        -   **IIS 6 管理相容性**  

            -   **IIS 6 Metabase 相容性**  

            -   **IIS 6 管理主控台**  

            -   **IIS 6 指令碼工具**  

            -   **IIS 6 WMI 相容性**  

        -   **IIS 6 管理指令碼及工具**  

        -   **Management Service**  

6.  新增下列 [功能]  ，方法是從清單中選取它們：  

    -   -   **背景智慧型傳送服務 (BITS)**  

            -   **IIS 伺服器擴充功能**  

        -   **遠端伺服器管理工具**  

            -   **功能管理工具**  

                -   **BITS 伺服器擴充功能工具**  

7.  按一下 [安裝]  ，並在 [伺服器管理員]  的 [通知] 窗格中確認正確地完成安裝。  

根據預設，IIS 會封鎖 HTTP 或 HTTPS 通訊存取數種類型的副檔名和位置。 若要讓這些檔案發佈至用戶端系統，您需要在發佈點上設定 IIS 的要求篩選。 如需詳細資訊，請檢閱[用於發佈點的 IIS 要求篩選](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering)。  

##### <a name="to-configure-iis-filtering-on-distribution-points"></a>在發佈點上設定 IIS 篩選：  

1.  開啟 **IIS Manager** ，然後在資訊看板中選取您的伺服器名稱。 這樣會將您帶到 [首頁]  畫面。  

2.  確認選取 [首頁]  畫面底部的 [功能檢視]  。 瀏覽至 [IIS]  ，並開啟 [要求篩選] 。  

3.  在 [動作]  窗格中，按一下 [允許副檔名]   

4.  將 **.msi** 輸入對話方塊中，然後按一下 [確定] 。  

###  <a name="BKMK_InstallCMLab"></a> 安裝 Configuration Manager  
您將建立[判斷何時使用主要站台](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary)來直接管理用戶端。 這將讓您的實驗室環境支援潛在裝置之[站台系統縮放](/sccm/core/plan-design/configs/size-and-scale-numbers)的管理。  
在這個過程中，您也會安裝 Configuration Manager 主控台，以用來管理您之後的評估裝置。  

開始安裝之前，請在使用 Windows Server 2012 的伺服器上啟動[先決條件檢查程式](/sccm/core/servers/deploy/install/prerequisite-checker)，確認已正確地啟用所有設定。  

##### <a name="to-download-and-install-configuration-manager"></a>下載和安裝 Configuration Manager：  

1.  瀏覽至 [System Center 評估版](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection)頁面來下載 System Center Configuration Manager 的最新評估版。  

2.  將下載媒體解壓縮到預先定義的位置。  

3.  遵循[使用 System Center Configuration Manager 安裝精靈來安裝站台](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)中所列的安裝程序。 在該程序內，您將輸入下列項目：  

    |站台安裝程序中的步驟|選取範圍|  
    |-----------------------------------------|---------------|  
    |步驟 4：[產品金鑰]  頁面|選取 [評估] 。|  
    |步驟 7：  **必要條件下載**|選取 [下載所需檔案]  ，然後指定預先定義的位置。|  
    |步驟 10： **站台和安裝設定**|-   **站台碼：LAB**<br />-   **站台名稱：評估**<br />-   **安裝資料夾：** 指定預先定義的位置。|  
    |步驟 11： **主要站台安裝**|選取 [將主要站台安裝為獨立站台] ，然後按一下 [下一步] 。|  
    |步驟 12： **資料庫安裝**|-   **SQL Server 名稱 (FQDN)：** 在這裡輸入 FQDN。<br />-   **執行個體名稱：** 因為您將使用先前安裝的預設 SQL 執行個體，所以請將這個項目留白。<br />-   **Service Broker 連接埠：** 保留為預設連接埠 4022。|  
    |步驟 13： **資料庫安裝**|請將這些設定保留為預設值。|  
    |步驟 14：**SMS 提供者**|請將這些設定保留為預設值。|  
    |步驟 15： **用戶端通訊設定**|確認未選取 [所有站台系統角色僅能接受用戶端傳來的 HTTPS 通訊]  。|  
    |步驟 16： **站台系統角色**|輸入 FQDN，並確認仍選取 [所有站台系統角色僅能接受用戶端傳來的 HTTPS 通訊]  。|  

###  <a name="BKMK_EnablePubLab"></a> 啟用 Configuration Manager 站台的發行  
每個 Configuration Manager 站台都會將其專屬的站台特定資訊發行至 Active Directory 架構中網域分割內的系統管理容器。 必須開啟 Active Directory 與 Configuration Manager 間通訊的雙向通道，才能處理這個流量。 您也會額外啟用樹系探索，以判斷 Active Directory 及網路基礎結構的某些元件。  

##### <a name="to-configure-active-directory-forests-for-publishing"></a>若要設定 Active Directory 樹系進行發佈：  

1.  在 Configuration Manager 主控台的左下角，按一下 [系統管理]。  

2.  在 [系統管理]  工作區中，展開 [階層組態] ，然後按一下 [探索方法] 。  

3.  選取 [Active Directory 樹系探索]  ，然後按一下 [內容] 。  

4.  在 [內容]  對話方塊中，選取 [啟用 Active Directory 樹系探索] 。 這個項目作用之後，請選取 [探索到 Active Directory 站台界限時自動建立它們] 。 將會出現一個對話方塊，指出 **您是否要盡快執行完整探索?** 按一下 [完成] 。  

5.  在畫面頂端的 [探索方法]  群組中，按一下 [立即執行樹系探索] ，然後瀏覽至資訊看板中的 [Active Directory 樹系]  。 您的 Active Directory 樹系應該會顯示在探索到的樹系清單中。  

6.  瀏覽至畫面頂端的 [一般 ]  索引標籤。  

7.  在 [系統管理]  工作區中，展開 [階層設定] ，然後按一下 [Active Directory 樹系] 。  

##### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>讓 Configuration Manager 站台將站台資訊發行至 Active Directory 樹系：  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  您將設定尚未探索到的新樹系。  

3.  在 [系統管理]  工作區中，按一下 [Active Directory 樹系] 。  

4.  在站台內容的 [發佈]  索引標籤上，選取您已連線的樹系，然後按一下 [確定]  儲存組態。
