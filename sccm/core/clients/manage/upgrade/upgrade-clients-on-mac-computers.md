---
title: "升級 macOS 用戶端 - Configuration Manager | Microsoft Docs"
description: "在 System Center Configuration Manager 中升級 Mac 電腦上的用戶端。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 502116b66fc14914ca0606ae416e82202824de7a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>如何升級 System Center Configuration Manager 中 Mac 電腦上的用戶端

*適用於：System Center Configuration Manager (最新分支)*

請遵循下面所述的高階步驟，使用 System Center Configuration Manager 應用程式來升級 Mac 電腦用戶端。 另外，您也可以下載 Mac 用戶端安裝檔案，將其複製到共用的網路位置或 Mac 電腦上的本機資料夾，然後指示使用者手動執行安裝。  

> [!NOTE]  
>  請先確定您的 Mac 電腦符合必要條件，再執行這些步驟。 請參閱 [Mac 電腦的支援作業系統](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)。  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>步驟 1：從 Microsoft 下載中心下載最新 Mac 用戶端安裝檔案  
 Configuration Manager 安裝媒體上並不提供用於 Configuration Manager 的 Mac 用戶端，此用戶端必須從 Microsoft 下載中心下載。 Mac 用戶端安裝檔案包含在名稱為 ConfigmgrMacClient.msi 的 Windows Installer 檔案中。  

 您可以從 [Microsoft Download Center (Microsoft 下載中心)](http://go.microsoft.com/fwlink/p/?LinkId=525184)下載此檔案。  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>步驟 2：執行下載的安裝檔案以建立 Mac 用戶端安裝檔案  
 在執行 Windows 的電腦上，執行您下載的 **ConfigmgrMacClient.msi** 以解壓縮名稱為 **Macclient.dmg**的 Mac 用戶端安裝檔案。 根據預設，解壓縮檔案後，您可在 Windows 電腦上的 **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** 資料夾中找到此檔案。  

## <a name="step-3-extract-the-client-installation-files"></a>步驟 3：解壓縮用戶端安裝檔案  
 將 Macclient.dmg 檔案複製到網路共用或 Mac 電腦上的本機資料夾。 接著從 Mac 電腦掛接並且開啟 Macclient.dmg 檔案，然後複製檔案到 Mac 電腦上的資料夾。  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>步驟 4：建立可用來建立應用程式的 .cmmac 檔案  

1.  使用 [CMAppUtil]  工具 (在 Mac 用戶端安裝檔案的 [Tools]  資料夾中) 從用戶端安裝套件建立 .cmmac 檔。 此檔案將用來建立 Configuration Manager 應用程式。  

2.  將新檔案 **CMClient.pkg.cmmac** 複製到執行 Configuration Manager 主控台之電腦可用的位置。  

 如需詳細資訊，請參閱[建立和部署 Mac 電腦的應用程式補充程序](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers)。  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**步驟 5：**建立和部署含有 Mac 用戶端檔案的應用程式  

1.  在 Configuration Manager 主控台中，從含有用戶端安裝檔案的 **CMClient.pkg.cmmac** 檔案建立應用程式。  

2.  將此應用程式部署到階層中的 Mac 電腦。  

 如需詳細資訊，請參閱[使用 System Center Configuration Manager 建立 Mac 電腦應用程式](../../../../apps/get-started/creating-mac-computer-applications.md)。  

## <a name="step-6-users-install-the-latest-client"></a>步驟 6：使用者安裝最新的用戶端  
 Mac 用戶端的使用者將會收到已有 Configuration Manager 用戶端可用更新而且必須安裝的提示。 在安裝用戶端之後，使用者必須重新啟動 Mac 電腦。  

 電腦重新啟動後，[電腦註冊精靈] 會自動執行以要求新的使用者憑證。  

 如果您不要使用 Configuration Manager 註冊，而要在不透過 Configuration Manager 的情況下獨立安裝用戶端憑證，請參閱[將升級的用戶端設定為使用現有憑證](#BKMK_UpgradingClient_MachineEnrollment)。  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure the upgraded client to use an existing certificate  
 執行下列程序以防止 [電腦註冊精靈] 執行，並且將升級的用戶端設定為使用現有的用戶端憑證。  

-   在 Configuration Manager 主控台中，建立 **Mac OS X** 類型的設定項目。  

-   在此設定項目中新增 [指令碼] 類型的設定。  

-   將下列指令碼新增至設定：  

    ```  
    #!/bin/sh  
    echo "Starting script\n"  
    echo "Changing directory to MAC Client\n"  
    cd /Users/Administrator/Desktop/'MAC Client'/  
    echo "Import root cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
    echo "Using openssl to convert pfx to a crt\n"  
    /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
    echo "Adding trust to root cert\n"  
    /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
    echo "Import client cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
    echo "Executing ccmclient with MP\n"  
    sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
    echo "Editing Plist file\n"  
    sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
    echo "Changing directory to CCM\n"  
    cd /Library/'Application Support'/Microsoft/CCM/  
    echo "Making connection to the server\n"  
    sudo open ./CCMClient  
    echo "Ending Script\n"  
    exit  

    ```  

-   將設定項目新增至設定基準，然後將設定基準部署至所有安裝獨立於 Configuration Manager 之憑證的 Mac 電腦。  

 如需如何建立和部署 Mac 電腦設定項目的詳細資訊，請參閱[如何為 System Center Configuration Manager 用戶端所管理的 Mac OS X 裝置建立設定項目](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)和[如何在 System Center Configuration Manager 中部署設定基準](../../../../compliance/deploy-use/deploy-configuration-baselines.md)。  
