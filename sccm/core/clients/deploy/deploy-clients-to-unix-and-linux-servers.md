---
title: "部署 UNIX/Linux 用戶端 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中將用戶端部署至 UNIX 或 Linux 伺服器。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d61d53daa5ef3d9c986cba8791d4471fea94d29d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中將用戶端部署至 UNIX 和 Linux 伺服器

*適用於：System Center Configuration Manager (最新分支)*

您必須先在每個 Linux 或 UNIX 伺服器上安裝適用於 Linux 和 UNIX 的 Configuration Manager 用戶端，才能使用 System Center Configuration Manager 管理 Linux 或 UNIX 伺服器。 您可以在每部電腦上手動完成用戶端的安裝，或使用可遠端安裝用戶端的殼層指令碼。 Configuration Manager 不支援使用 Linux 或 UNIX 伺服器的用戶端推入安裝。 您可以選擇性地設定 Runbook for System Center Orchestrator，來自動化 Linux 或 UNIX 伺服器上的用戶端安裝。  

 不論您使用的安裝方法為何，安裝程序都需要使用名為 **install** 的指令碼來管理安裝程序。 您可以下載用戶端的 Linux 和 UNIX 時會包含此指令碼。  

 適用於 Linux 和 UNIX 之 Configuration Manager 用戶端的安裝指令碼支援命令列屬性。 有些則是選擇性需要，有些命令列屬性。 例如，當您安裝用戶端，您必須指定 Linux 或 UNIX 伺服器用於其初次接觸與站台之站台的管理點。 如需命令列屬性的完整清單，請參閱 [在 Linux 和 UNIX 伺服器上安裝用戶端的命令列屬性](#BKMK_CmdLineInstallLnUClient)。  

 安裝用戶端之後，即可在 Configuration Manager 主控台中指定 [用戶端設定] 來設定用戶端代理程式，而設定方式與 Windows 用戶端相同。 如需詳細資訊，請參閱  [Client settings for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU)。  

##  <a name="BKMK_AboutInstallPackages"></a> 有關用戶端安裝封裝和通用的代理程式  
 若要在特定平台上安裝 Linux 和 UNIX 的用戶端，您必須使用安裝用戶端之電腦的適用用戶端安裝封裝。 從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkID=525184)下載的每個用戶端都包含適用的用戶端安裝套件。 除了用戶端安裝封裝之外，用戶端下載還會包括管理每部電腦上用戶端安裝的 **install** 指令碼。  

 當您安裝用戶端時，您可以使用相同的程序和命令列屬性不論您使用用戶端安裝套件。  

 如需每個 Linux 和 UNIX Configuration Manager 用戶端版本所支援之作業系統、平台和用戶端安裝套件的詳細資訊，請參閱 [Linux 和 UNIX 伺服器](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers)。  

##  <a name="BKMK_InstallLnUClient"></a> 在 Linux 和 UNIX 伺服器上安裝用戶端  
 若要安裝用戶端的 Linux 和 UNIX，您可以執行指令碼在每個 Linux 或 UNIX 電腦上。 指令碼名為 **安裝** 和支援修改的安裝行為並參照用戶端安裝封裝的命令列屬性。 安裝指令碼和用戶端安裝套件必須位於用戶端。 用戶端安裝套件包含特定 Linux 或 UNIX 作業系統和平台的 Configuration Manager 用戶端檔案。
每個用戶端安裝套件包含所有必要的檔案以完成用戶端安裝並不像 Windows 電腦將不會下載其他檔案從管理點或其他來源位置。  

 在您安裝 Linux 和 UNIX Configuration Manager 用戶端之後，不需要重新啟動電腦。 只要軟體安裝完成時，用戶端可以運作。 如果您重新啟動電腦，Configuration Manager 用戶端會自動重新啟動。  

 安裝的用戶端會使用根認證執行。 需要有根認證，才能收集硬體清查，並執行軟體部署。  

 下列是命令格式：  

 **./install -mp &lt;電腦\> -sitecode &lt;站台碼\> &lt;屬性 #1> &lt;屬性 #2> &lt;用戶端安裝套件\>**  

-   **安裝** 是安裝適用於 Linux 及 UNIX 用戶端指令碼檔案的名稱。 這個檔案被提供與用戶端軟體。  

-   **-mp &lt;電腦>** 指定用戶端使用的初始管理點。  

     範例︰smsmp.contoso.com  

-   **-sitecode &lt;站台碼\>** 指定指派給用戶端的站台碼。  

     範例：S01  

-   &lt;屬性 #1> &lt;屬性 #2> 指定與安裝指令碼搭配使用的命令列屬性。  

    > [!NOTE]  
    >  如需詳細資訊，請參閱 [在 Linux 和 UNIX 伺服器上安裝用戶端的命令列屬性](#BKMK_CmdLineInstallLnUClient)  

-   **用戶端安裝套件** 是這個電腦作業系統、版本和 CPU 架構的用戶端安裝 .tar 套件名稱。 用戶端安裝.tar 檔案必須指定上一次。  

     範例：ccm-Universal-x64.&lt;組建\>.tar  

###  <a name="BKMK_ToInstallLnUClinent"></a> 在 Linux 和 UNIX 伺服器上安裝 Configuration Manager 用戶端  

1.  在 Windows 電腦上，為您想要管理的電腦 [下載適用於 Linux 或 UNIX 伺服器的用戶端檔案](http://go.microsoft.com/fwlink/?LinkID=525184) 。  

2.  執行 Windows 電腦的自我解壓縮 .exe 檔案，解壓縮安裝指令碼和用戶端安裝 .tar 檔案。  

3.  將 **安裝** 指令碼和 .tar 檔案複製到要管理的伺服器資料夾中。  

4.  在 UNIX 或 Linux 伺服器上，執行下列命令，將指令碼當成程式執行： **chmod +x install**  

    > [!IMPORTANT]  
    >  您必須安裝用戶端使用根認證。  

5.  接下來，執行下列命令以安裝 Configuration Manager 用戶端：**./install -mp &lt;主機名稱\> -sitecode &lt;代碼\> ccm-Universal-x64.&lt;組建\>.tar**  

     當您輸入這個命令時，使用您所需要的其他命令列屬性。  如需命令列屬性清單，請參閱 [在 Linux 和 UNIX 伺服器上安裝用戶端的命令列屬性](#BKMK_CmdLineInstallLnUClient)。  

6.  指令碼執行之後，請檢閱 **/var/opt/microsoft/scxcm.log** 檔案來驗證安裝。 此外，您還可以在 Configuration Manager 主控台之 [資產與相容性] 工作區的 [裝置] 節點中檢視用戶端詳細資料，確認已安裝用戶端，而且用戶端正在與站台通訊。  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> 在 Linux 和 UNIX 伺服器上安裝用戶端的命令列屬性  
 下列屬性可用於修改安裝指令碼的行為︰  

> [!NOTE]  
>  使用屬性 **-h** 顯示這份支援的屬性。  

-   **-mp &lt;伺服器 FQDN\>**  

     必要。 指定由用戶端會將它當成連絡人的起始點的管理點伺服器的 FQDN。  

    > [!IMPORTANT]  
    >  這個屬性並未指定用戶端在安裝後變成指派的管理點。  

    > [!NOTE]  
    >  當您使用 **-mp** 屬性指定設定成只接受 HTTPS 用戶端連線的管理點時，也必須使用 **-UsePKICert** 屬性。  

-   **-sitecode &lt;站台碼\>**  

     必要。 指定要將 Configuration Manager 用戶端指派過去的 Configuration Manager 主要站台。  

     範例：-sitecode S01  

-   **-fsp &lt;伺服器_FQDN>**  

     選擇性。 指定由用戶端用來將狀態訊息提交回溯狀態點伺服器的 FQDN。  

     如需後援狀態點的詳細資訊，請參閱 [Determine Whether You Require a Fallback Status Point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point) 。  


-   **-dir &lt;目錄\>**  

     選擇性。 指定安裝 Configuration Manager 用戶端檔案的替代位置。  

     根據預設，用戶端會安裝到下列位置： **/opt/microsoft**。  

-   **-nostart**  

     選擇性。 防止在用戶端安裝完成之後自動啟動 Configuration Manager 用戶端服務 **ccmexec.bin**。  

     用戶端安裝之後，您必須手動啟動用戶端服務。  

     根據預設，用戶端服務會啟動用戶端安裝完成之後，以及每次電腦重新啟動。  

-   **-初始狀態**  

     選擇性。 在新的安裝作業開始之前指定 Linux 和 UNIX，移除所有的用戶端檔案和資料從先前安裝的用戶端。 這會移除用戶端的資料庫和憑證存放區。  

-   **-keepdb**  

     選擇性。 指定本機用戶端資料庫會保留，而當您重新安裝用戶端時重複使用。 根據預設，當您重新安裝用戶端時就會刪除此資料庫。  

-   **-UsePKICert &lt;參數\>**  

     選擇性。 指定 X.509 PKI 憑證的完整路徑和檔案名稱中的公用金鑰憑證標準 (PKCS #12) 格式。 此憑證用於用戶端驗證。 如果未在安裝期間指定憑證，而且需要新增或變更憑證，請使用 **certutil** 公用程式。 如需 certutil 的相關資訊，請參閱 [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) 。  

     當您使用 **-UsePKICert**時，也必須使用 **-certpw** 命令列參數來提供與 PKCS#12 檔案相關聯的密碼。  

     如果您不使用這個屬性來指定 PKI 憑證，用戶端會使用自我簽署的憑證和站台系統的所有通訊都都透過 HTTP。  

     如果您在上指定無效的憑證用戶端安裝命令列，不會傳回錯誤。 這是因為在用戶端安裝之後，就會發生憑證驗證。 當用戶端啟動時，憑證會驗證和管理點而如果驗證失敗的憑證會出現下列訊息 **scxcm.log**, ，Unix 和 Linux Configuration Manager 用戶端記錄檔: **失敗驗證的憑證管理點**。 預設記錄檔位置為：  **/var/opt/microsoft/scxcm.log**。  

    > [!NOTE]  
    >  如果您安裝用戶端，並使用 **-mp** 屬性來指定設定為只接受 HTTPS 用戶端連線的管理點，則必須指定這個屬性。  

     範例：-UsePKICert &lt;完整路徑和檔名\> -certpw &lt;密碼\>  

-   **-certpw &lt;參數\>**  

     選擇性。 指定使用與您所指定的 PKCS #12 檔案相關聯的密碼 **-UsePKICert** 屬性。  

     範例：-UsePKICert &lt;完整路徑和檔名\> -certpw &lt;密碼\>  

-   **-NoCRLCheck**  

     選擇性。 指定用戶端應該不檢查憑證撤銷清單 (CRL) 所使用的 PKI 憑證透過 HTTPS 通訊時。 當未指定此選項時，用戶端會建立 HTTPS 連線所使用的 PKI 憑證之前檢查 CRL。 如需有關用戶端 CRL 檢查的詳細資訊，請參閱 PKI 憑證撤銷的規劃。  

     範例：-UsePKICert &lt;完整路徑和檔名\> -certpw &lt;密碼\> -NoCRLCheck  

-   **-rootkeypath &lt;檔案位置\>**  

     選擇性。 指定 Configuration Manager 受信任根金鑰的完整路徑和檔案名稱。 Configuration Manager 受信任根金鑰提供一種機制，讓 Linux 和 UNIX 用戶端用來確認它們是否連線到屬於正確階層的站台系統。  

     如果您未在命令列上指定受信任根金鑰，則用戶端會信任與其通訊的第一個管理點，並從該管理點自動擷取受信任根金鑰。  

     如需詳細資訊，請參閱  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

     範例︰-rootkeypath &lt;完整路徑和檔名\>  

-   **-httpport &lt;連接埠\>**  

     選擇性。 指定在用戶端會使用透過 HTTP 進行通訊來管理點時的管理點設定的連接埠。 如果未指定連接埠，會使用預設值 80。  

     範例：-httpport 80  

-   **-httpsport &lt;連接埠\>**  

     選擇性。 指定在用戶端會使用透過 HTTPS 管理點來進行通訊時的管理點設定的連接埠。 如果未指定連接埠，會使用 443 的預設值。  

     範例：-UsePKICert &lt;完整路徑和憑證名稱\> -httpsport 443  

-   **-ignoreSHA256validation**  

     選擇性。 指定用戶端安裝略過 sha-256 驗證。 如果在未與支援 SHA-256 之 OpenSSL 版本一起發行的作業系統上安裝用戶端，請使用這個選項。 如需詳細資訊，請參閱 [About Linux and UNIX Operating Systems That do not Support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256)。  

-   **-rootkeypath &lt;檔案位置\>**  

     選擇性。 指定完整路徑和 **.cer** 站台伺服器上的匯出自我簽署憑證的檔案名稱。 如果無 PKI 憑證可用，則 Configuration Manager 站台伺服器會自動產生自我簽署憑證。  

     這些憑證用來驗證從管理點下載用戶端原則從預定的站台所送出。 如果未在安裝期間指定自我簽署憑證，或者需要變更憑證，請使用 **certutil** 公用程式。 如需 certutil 的相關資訊，請參閱 [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) 。  

     這個憑證可以透過 [SMS]  憑證存放區擷取、主體名稱為 [站台伺服器]  ，而易記名稱為 [站台伺服器簽署憑證] 。  

     如果在安裝期間沒有指定這個選項，Linux 和 UNIX 用戶端會信任這些通訊並自動將來自該管理點擷取的簽章憑證的第一個管理點。  

     範例︰-signcertpath &lt;完整路徑和檔名\>  

-   **-rootcerts**  

     選擇性。 指定其他要匯入不是管理點憑證授權單位 (CA) 階層的一部分的 PKI 憑證。 如果您在命令列中指定多個憑證，它們應該以逗號分隔。  

     如果您使用鏈結至您的網站管理點所信任的根 CA 憑證的 PKI 用戶端憑證，使用此選項。 如果用戶端憑證未鏈結至站台憑證簽發者清單中的受信任根憑證，則管理點將拒絕用戶端。  

     如果您不使用此選項，Linux 和 UNIX 用戶端會確認使用中的憑證信任階層 **-UsePKICert** 選項。  

     範例︰-rootcerts &lt;完整路徑和檔名\>,&lt;完整路徑和檔名\>  

###  <a name="BKMK_UninstallLnUClient"></a> 從 Linux 和 UNIX 伺服器解除安裝用戶端  
 若要解除安裝 Linux 和 UNIX Configuration Manager 用戶端，請使用解除安裝公用程式 **uninstall**。 根據預設，這個檔案位於 **/選擇/microsoft/configmgr/bin/** 用戶端電腦上的資料夾。 這在解除安裝命令不支援任何命令列參數，而且將會移除從伺服器到用戶端軟體相關的所有檔案。  

 若要解除安裝用戶端，請使用下列命令列: **/opt/microsoft/configmgr/bin/uninstall**  

 在您解除安裝 Linux 和 UNIX Configuration Manager 用戶端之後，不需要重新啟動電腦。  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> 設定 Linux 和 UNIX 用戶端要求連接埠  
 與 Windows 用戶端類似，Linux 和 UNIX Configuration Manager 用戶端會使用 HTTP 和 HTTPS 來與 Configuration Manager 站台系統通訊。 Configuration Manager 用戶端用來通訊的連接埠稱為要求連接埠。  

 當您安裝 Linux 和 UNIX Configuration Manager 用戶端時，可以指定 **-httpport** 和 **-httpsport** 安裝內容來變更用戶端預設要求連接埠。 當您未指定安裝在屬性和自訂的值時，用戶端會使用預設值。 預設值為 **80** HTTP 流量和 **443** 的 HTTPS 流量。  

 安裝用戶端之後，您無法變更其要求的連接埠組態。 相反地，若要變更連接埠組態必須重新安裝用戶端並指定新的連接埠組態。 當您重新安裝用戶端變更要求的連接埠號碼時，執行 **安裝** 命令類似於新的用戶端安裝，但使用的其他命令列屬性 **-keepdb**。 此參數會指示要保留的用戶端資料庫和檔案包括用戶端 GUID 和憑證存放區安裝。  

 如需用戶端通訊連接埠號碼的詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端通訊連接埠](../../../core/clients/deploy/configure-client-communication-ports.md)。  

##  <a name="BKMK_ConfigClientMP"></a> 設定用於 Linux 和 UNIX 找出管理點的用戶端  
 安裝 Linux 和 UNIX Configuration Manager 用戶端時，必須指定作為初始連絡點使用的管理點。  

 Linux 和 UNIX Configuration Manager 用戶端會在用戶端安裝時連絡這個管理點。 如果用戶端無法連絡管理點，則用戶端軟體會繼續重試，直到成功為止。  

 如需用戶端如何找到管理點的詳細資訊，請參閱 [Locating Management Points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points)。
