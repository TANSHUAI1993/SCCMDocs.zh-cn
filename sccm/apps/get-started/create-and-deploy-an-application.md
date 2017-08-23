---
title: "建立和部署應用程式 | Microsoft Docs"
description: "建立和部署包含商務營運應用程式的應用程式，並了解如何有效地管理應用程式。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: "15"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: bbbf278f5d31c51bfe061dd44e170f7ab1ca70ad
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立和部署應用程式

*適用於︰System Center Configuration Manager (最新分支)*

在本主題中，您將直接使用 System Center Configuration Manager 建立應用程式。 在此範例中，您將建立和部署一個應用程式，其中包含適用於 Windows 電腦的企業營運應用程式 (稱為 **Contoso.msi**)，而此應用程式必須安裝在公司內執行 Windows 10 的所有電腦上。 您將在這整個過程中了解有效管理應用程式的事項。  

 這個程序旨在提供如何建立和部署 Configuration Manager 應用程式的概觀。 不過，它未涵蓋所有設定選項，或是如何建立和部署其他平台之應用程式的方法。  

 如需與每個平台相關的特定詳細資料，請參閱下列其中一個主題：  

-   [建立 Windows 應用程式](../../apps/get-started/creating-windows-applications.md)  
-   [建立 iOS 應用程式](../../apps/get-started/creating-ios-applications.md)  
-   [建立 Android 應用程式](../../apps/get-started/creating-android-applications.md)  
-   [建立 Windows Phone 應用程式](../../apps/get-started/creating-windows-phone-applications.md)  
-   [建立 Mac 電腦應用程式](../../apps/get-started/creating-mac-computer-applications.md)  
-   [建立 Linux 和 UNIX 伺服器應用程式](../../apps/get-started/creating-linux-and-unix-server-applications.md)
-   [建立 Windows Embedded 應用程式](../../apps/get-started/creating-windows-embedded-applications.md)


如果您已經熟悉 Configuration Manager 應用程式，則可以略過這個主題。 不過，您可以檢閱[建立應用程式](../../apps/deploy-use/create-applications.md)，來了解建立和部署應用程式時可用的所有選項。  

## <a name="before-you-start"></a>開始之前  

請確定您已檢閱[應用程式管理簡介](/sccm/apps/understand/introduction-to-application-management)中的資訊，以備妥您的站台來安裝應用程式，而且您了解本主題中所使用的術語。  

 也請確定 **Contoso.msi** 應用程式的安裝檔案位於網路上可存取的位置。  

## <a name="create-the-configuration-manager-application"></a>建立 Configuration Manager 應用程式  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>啟動建立應用程式精靈以及建立應用程式  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，按一下 [建立應用程式]。  

4.  在 [建立應用程式精靈] 的 [一般] 頁面上，選擇 [從安裝檔案自動偵測此應用程式的相關資訊]。 這會利用從安裝 .msi 檔案中擷取的資訊，預先填入精靈中的部分資訊。 接著，指定下列資訊：  

    -   **類型**：選擇 [Windows Installer (\*.msi 檔案)]。  

    -   **位置**：輸入安裝檔 **Contoso.msi** 的位置 (或選擇 [瀏覽] 以選取位置)。 請注意，必須以 \\\Server\Share\File 格式指定位置，Configuration Manager 才能找到安裝檔。  

    您將會得到類似下列的螢幕擷取畫面：  

    ![應用程式管理精靈一般頁面](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  

5.  選擇 [下一步]。 在 [匯入資訊] 頁面上，您會看到應用程式以及已匯入至 Configuration Manager 之任何相關聯檔案的相關資訊。 完成之後，再次選擇 [下一步] 。  

6.  在 [一般資訊] 頁面上，您可以提供應用程式的進一步資訊，協助您在 Configuration Manager 主控台中排序並找到它。  

     此外，[安裝程式] 欄位可讓您指定將用來在電腦上安裝應用程式的完整命令列。 您可以編輯這個檔案來新增自己的屬性 (例如 **/q** 表示自動安裝)。  

    > [!TIP]  
    >  在匯入應用程式安裝檔時，可能已自動填入精靈的這個頁面上的部分欄位。  

     您所得到的畫面將類似下列的螢幕擷取畫面：  

     ![應用程式管理精靈一般資訊頁面](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  

7.  選擇 [下一步]。 在 [摘要] 頁面上，您可以確認應用程式設定，然後完成精靈。  

 您已完成建立應用程式。 若要找到它，請在 [軟體程式庫] 工作區中，展開 [應用程式管理]，然後選擇 [應用程式]。 在這個範例中，您將看到：  

 ![最終應用程式圖形](/sccm/apps/get-started/media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>檢查應用程式和其部署類型的內容  

現在，您已經建立應用程式，可視需要來精簡應用程式設定。 若要查看應用程式內容，請選取應用程式，然後在 [首頁] 索引標籤的 [內容]  群組中選擇 [內容]。  

 在 [<Contoso\> 應用程式內容] 對話方塊中，您將看到許多可設定來精簡應用程式行為的項目。 如需可設定之所有設定的詳細資料，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。 這個範例旨在讓您只變更應用程式部署類型的某些內容。  

 選擇 [部署類型] 索引標籤 > [Contoso 應用程式] 部署類型 > [編輯]。  

您會看到與下列類似的對話方塊：  

![應用程式管理應用程式內容頁面](/sccm/apps/get-started/media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>新增部署類型的需求  
 需求指定必須符合條件才可以在裝置上安裝應用程式。  您可以從內建需求中選擇，也可以建立您自己的需求。 在這個範例中，您要新增應用程式只會在執行 Windows 10 的電腦上安裝的需求。  

1.  從剛開啟的部署類型內容頁面中，選擇 [需求] 索引標籤。  

2.  選擇 [新增] 以開啟 [建立需求] 對話方塊。  

3.  在 [建立需求]  對話方塊中，指定下列資訊：  

    -   **類別**：**裝置**  

    -   **條件**：**作業系統**  

    -   **規則類型**：**值**  

    -   **運算子**：**其中一個**  

    -   從作業系統清單中，選取 [Windows 10] 。  

    最後的對話方塊會像下列對話方塊：  

    ![應用程式管理需求頁面](/sccm/apps/get-started/media/App-management-requirements-page.png)  

4.  選擇 [確定] 以關閉您開啟的每個內容頁。 接著返回 Configuration Manager 主控台中的 [應用程式] 清單。  

> [!TIP]  
>  需求有助於減少您需要的 Configuration Manager 集合數目。 因為您剛才指定應用程式只能安裝在執行 Windows 10 的電腦上，所以稍後可將這個應用程式部署到包含執行許多不同作業系統的電腦集合。 但是，應用程式將只會安裝於 Windows 10 電腦上。  

## <a name="add-the-application-content-to-a-distribution-point"></a>將應用程式內容新增至發佈點  

接下來，若要將應用程式部署到電腦，請確定會將應用程式內容複製到發佈點。 電腦會存取發佈點來安裝應用程式。  

> [!TIP]  
>  若要深入了解 Configuration Manager 中的發佈點和內容管理，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫]。  

2.  在 [軟體程式庫] 工作區中，展開 [應用程式]。 然後，在應用程式清單中，選取您所建立的 [Contoso 應用程式]。  

3.  在 [首頁] 索引標籤的 [部署] 群組中，選擇 [發佈內容]。  

4.  在 [發佈內容精靈] 的 [一般] 頁面上，確認應用程式名稱正確，然後選擇 [下一步]。  

5.  在 [內容] 頁面上，檢閱將複製到發佈點的資訊，然後選擇 [下一步]。  

6.  在 [內容目的地] 頁面上，選擇 [新增]，以選取一或多個發佈點，或要在其上安裝應用程式內容的發佈點群組。  

7.  完成精靈。  

您可以檢查應用程式內容已從 [監視] 工作區 (位於 [發佈狀態] > [內容狀態] 下方) 成功複製到發佈點。  

## <a name="deploy-the-application"></a>部署應用程式  

接下來，將應用程式部署至階層中的裝置集合。 在此範例中，您會將應用程式部署到 [所有系統] 裝置集合。  

> [!TIP]  
>  請記住，因為您先前選取的需求，所以只有 Windows 10 電腦才會安裝應用程式。  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式]。  

3.  從應用程式清單中，選取您先前建立的應用程式 ([Contoso 應用程式])，然後在 [首頁] 索引標籤的 [部署] 群組中，選擇 [部署]。  

4.  在 [部署軟體精靈] 的 [一般] 頁面上，選擇 [瀏覽] 以選取 [所有系統] 裝置集合。  

5.  在 [內容] 頁面上，確認已選取您想要電腦從中安裝應用程式的發佈點。  

6.  在 [部署設定] 頁面上，確認將部署動作設為 [安裝]，並將部署目的設為 [必要]。  

    > [!TIP]  
    >  您可以藉由將部署目的設為 [必要]，來確定應用程式已安裝在符合所設定需求的電腦上。 如果您將此值設為 [可用] ，則使用者可以視需要從軟體中心安裝應用程式。  

7.  在 [排程]  頁面上，您可以設定應用程式的安裝時間。 在此範例中，選取 [可用時間之後越快越好] 。  

8.  在 [使用者體驗] 頁面上，選擇 [下一步] 以接受預設值。  

9. 完成精靈。  

使用下面**監視應用程式**一節中的資訊，來查看您應用程式部署的狀態。  

## <a name="monitor-the-application"></a>監視應用程式  
 在本節中，您將快速查看剛剛所部署應用程式的部署狀態。  

### <a name="to-review-the-deployment-status"></a>檢閱部署狀態  

1.  在 Configuration Manager 主控台中，選擇 [監視] > [部署]。  

3.  從部署清單中，選取 [Contoso 應用程式] 。  

4.  在 [首頁] 索引標籤的 [部署] 群組中，按一下 [檢視狀態]。  

5.  選取下列其中一個索引標籤，以查看更多關於應用程式部署的狀態更新：  

    -   **成功**：已在指定的電腦上成功安裝應用程式。  

    -   **進行中**：應用程式尚未完成安裝。  

    -   **錯誤**：在指定的電腦上安裝應用程式時發生錯誤。 也會顯示錯誤的進一步資訊。  

    -   **不符合需求**：未在指定的裝置上進行任何安裝嘗試，原因是它們不符合您所設定的需求 (在此範例中，原因是它們未執行 Windows 10)。  

    -   **未知**：Configuration Manager 無法報告部署狀態。 請稍後再試。  

> [!TIP]  
>  有數種方式可以監視應用程式部署。 如需完整詳細資訊，請參閱[監視應用程式](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

## <a name="end-user-experience"></a>使用者體驗  

具有由 Configuration Manager 所管理且執行 Windows 10 之電腦的使用者會看到一則訊息，告知他們必須安裝 Contoso 應用程式。 當他們接受安裝之後，即會安裝應用程式。  
