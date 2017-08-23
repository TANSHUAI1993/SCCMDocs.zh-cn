---
title: "規劃 SMS 提供者 | Microsoft Docs"
description: "深入了解 SMS 提供者如何協助您管理 System Center Configuration Manager。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 547dc39d5659c7c2e6f1ca670caddc127dbf22c4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>規劃 System Center Configuration Manager 的 SMS 提供者

*適用對象：System Center Configuration Manager (最新分支)*

若要管理 System Center Configuration Manager，可以使用連線至 **SMS 提供者**執行個體的 Configuration Manager 主控台。 根據預設，SMS 提供者會在安裝管理中心站台或主要站台時，一併安裝在站台伺服器上。 


##  <a name="BKMK_PlanSMSProv"></a> 關於 SMS 提供者  
 SMS 提供者是 Windows Management Instrumentation (WMI) 提供者，會指派網站之 Configuration Manager 資料庫的**讀取**與**寫入**權限：  

-   每個管理中心網站和主要網站上至少需要一個 SMS 提供者。 您可以視需要安裝額外的提供者。  
-   **SMS Admins** 安全性群組提供對 SMS 提供者的存取。 Configuration Manager 會自動在站台伺服器上和每部安裝了 SMS 提供者執行個體的電腦上，建立此群組。  

-   次要網站不支援 SMS 提供者。  


Configuration Manager 系統管理員使用 SMS 提供者來存取儲存於資料庫中的資訊。 若要執行此動作，系統管理員可以使用 Configuration Manager 主控台、資源總管、工具以及自訂指令碼。 SMS 提供者不會與 Configuration Manager 用戶端互動。 Configuration Manager 主控台連線至網站時，Configuration Manager 主控台會查詢站台伺服器上的 WMI，以找出要使用的 SMS 提供者執行個體。  

 SMS 提供者會協助強制執行 Configuration Manager 安全性。 它僅會傳回執行 Configuration Manager 主控台之系統管理使用者獲授權可檢視的資訊。  

> [!IMPORTANT]  
>  裝載網站之 SMS 提供者的每一部電腦離線時，Configuration Manager 主控台會無法連線至該網站的資料庫。  

 如需如何管理 SMS 提供者的詳細資訊，請參閱 [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) 中的 [Manage the SMS Provider](../../../core/servers/manage/modify-your-infrastructure.md)。  

## <a name="prerequisites-to-install-the-sms-provider"></a>安裝 SMS 提供者的先決條件  

 支援 SMS 提供者：  

-   電腦所在的網域，必須與站台伺服器和站台資料庫站台系統之間具備雙向信任。  

-   電腦不可擁有來自不同網站的網站系統角色。  

-   電腦不可擁有來自任何網站的 SMS 提供者。  

-   電腦必須執行支援網站伺服器的作業系統。  

-   電腦的可用磁碟空間至少必須要有 650 MB，才可支援隨 SMS 提供者一併安裝的 Windows 自動化部署套件 (Windows ADK) 元件。 如需 Windows ADK 與 SMS 提供者的詳細資訊，請參閱本主題中的 [SMS 提供者的作業系統部署需求](#BKMK_WAIKforSMSProv) 一節。  

##  <a name="bkmk_location"></a> SMS 提供者位置  
 安裝站台時，會自動安裝該站台的第一個 SMS 提供者。 您可以為 SMS 提供者指定以下任何一個受支援的位置：  

-   網站伺服器電腦  

-   網站資料庫電腦  

-   未裝載 SMS 提供者或網站系統角色來自不同網站的伺服器等級的電腦。  


若要檢視站台上所安裝每個 SMS 提供者位置，請從站台 [內容] 對話方塊中選取 [一般] 索引標籤。  

 每個 SMS 提供者支援來自多個請求的同時連線。 這些連線的唯一限制是 SMS 提供者電腦上可用伺服器連線的數目，以及 SMS 提供者電腦上的可用資源以服務連線請求。  

 安裝網站後，您可以再次在網站伺服器上執行安裝程式，以變更現有 SMS 提供者的位置，或在該網站上安裝其他 SMS 提供者。 您在一台電腦上只能安裝一個 SMS 提供者，並且電腦上不能安裝來自一個以上網站的 SMS 提供者。  

 請參考下列資訊來了解在每個受支援位置上安裝「SMS 提供者」的優缺點：  

 **Configuration Manager 站台伺服器**  

-   **優點：**  

    -   SMS 提供者不使用網站資料庫電腦的系統資源。  

    -   除了網站伺服器或網站資料庫電腦外，此位置也可提供比位於電腦上的 SMS 提供者更好的效能。  

-   **缺點：**  

    -   SMS 提供者會使用網站伺服器操作專用的系統和網路資源。  


**裝載網站資料庫的 SQL Server**  

-   **優點：**  

    -   SMS 提供者並不使用網站伺服器上的網站系統資源。  

    -   若有足夠伺服器資源可以使用，此位置可提供三個位置中最佳的效能。  

-   **缺點：**  

    -   SMS 提供者會使用網站資料庫操作專用的系統和網路資源。  

    -   當站台資料庫裝載於 SQL Server 的叢集執行個體上時，即無法使用此位置。  


**網站伺服器或網站資料庫電腦以外的電腦**  

-   **優點：**  

    -   SMS 提供者不使用網站伺服器或網站資料庫電腦資源。  

    -   此類型的位置可讓您部署額外 SMS 提供者，以提供高使用性的連線。  

-   **缺點：**  

    -   SMS 提供者效能可能會因為協調站台伺服器與站台資料庫電腦所需的額外網路活動而降低。  

    -   必須讓站台資料庫電腦與所有安裝 Configuration Manager 主控台的電腦一直都能存取此伺服器。  

    -   此位置可使用其他服務專用的系統資源。  

##  <a name="BKMK_SMSProvLanguages"></a> 關於 SMS 提供者語言  
 SMS 提供者操作時顯示的語言可與安裝該 SMS 提供者之電腦的語言不同。  

 系統管理使用者或 Configuration Manager 使用 SMS 提供者處理請求時，SMS 提供者會嘗試傳回格式符合提出請求之電腦的作業系統語言的資料。

其方式是嘗試比對語言是否為間接。 SMS 提供者不會將資訊從一種語言翻譯成另一種語言。 相反地，傳回的資料在 Configuration Manager 主控台上顯示時，資料顯示的語言會根據物件來源和儲存類型而定。  

 當物件的資料儲存在資料庫時，可用的語言會依據以下項目而定：  

-   Configuration Manager 建立的物件會使用多國語言的支援，儲存在資料庫中。 儲存物件時使用的語言，是您執行安裝程式時在建立物件的網站上所設定的語言。 這些物件在 Configuration Manager 主控台中顯示時，會以提出請求之電腦的顯示語言顯示 (若物件可使用該語言)。 若不能以提出請求之電腦的顯示語言來顯示物件，則會以預設語言顯示，亦即英文。  

-   系統管理使用者建立的物件會使用用來建立物件的語言，儲存在資料庫中。 這些物件會在 Configuration Manager 主控台中以相同語言顯示。 SMS 提供者無法翻譯這些物件，並且也沒有多個語言選項。  

##  <a name="BKMK_MultiSMSProv"></a> 使用多重 SMS 提供者  
 網站完成安裝後，您可以為網站安裝額外的 SMS 提供者。 若要安裝額外的 SMS 提供者，請在站台伺服器上執行 Configuration Manager 安裝程式。 若以下任何一項為真，請考慮安裝額外的 SMS 提供者：  

-   您會有許多執行 Configuration Manager 主控台的系統管理使用者，且會同時連線到站台。  

-   您將使用可能引入經常呼叫 SMS 提供者的 Configuration Manager SDK 或其他產品。  

-   您想要確保 SMS 提供者的高可用性。  


站台上安裝多個 SMS 提供者，並提出連線要求時，站台會隨機指派每個新連線要求，以便使用安裝的 SMS 提供者。 您無法指定 SMS 提供者位置搭配使用特定的連線工作階段。  

> [!NOTE]  
>  請考慮每個 SMS 提供者位置的優缺點。 請在您的資訊是無法控制要為每個新連線使用哪個 SMS 提供者的情況，在這些考量之間取得平衡。  

例如，首次將 Configuration Manager 主控台連線到某個站台時，連線會查詢站台伺服器上的 WMI，以找出主控台將使用的 SMS 提供者執行個體。 在 Configuration Manager 主控台工作階段結束前，Configuration Manager 主控台會持續使用這個特定的 SMS 提供者執行個體。 若因 SMS 提供者電腦在網路上無法使用，而導致工作階段結束，則當您重新連線 Configuration Manager 主控台時，站台只會重複找出 SMS 提供者要連線的執行個體工作。 其可能會指派給無法使用的相同 SMS 提供者電腦。 若發生這種狀況，您可以嘗試重新連線 Configuration Manager 主控台，直到指派可用的 SMS 提供者電腦為止。  

##  <a name="BKMK_AboutSMSAdmins"></a> 關於 SMS Admins 群組  
 您可使用 SMS Admin 群組提供 SMS 提供者系統管理使用者存取權限。 網站安裝時，會在網站伺服器上以及安裝 SMS 提供者的每台電腦上，自動建立群組。 以下是關於 SMS Admins 群組的其他資訊：  

-   當電腦是成員伺服器時，會將 SMS Admins 群組建立為本機群組。  

-   當電腦是網域控制站時，會將 SMS Admins 群組建立為網域本機群組。  

-   在電腦上解除安裝 SMS 提供者時，不會將 SMS Admins 群組從電腦中移除。  


使用者帳戶必須是 SMS Admins 群組的成員，然後使用者才能成功連線至 SMS 提供者。 您在 Configuration Manager 主控台中設定的每個系統管理使用者，會自動新增到每部站台伺服器上的 SMS Admins 群組，以及階層中的每部 SMS 提供者電腦。 從 Configuration Manager 主控台刪除系統管理使用者時，該使用者會從每部站台伺服器上的 SMS Admins 群組與階層中每部 SMS 提供者電腦中移除。  

使用者成功連線至 SMS 提供者後，以角色為基礎的系統管理會決定使用者可以存取或管理的 Configuration Manager 資源。  

您可以使用 WMI 控制 MMC 嵌入式管理單元來檢視和設定 SMS Admins 群組權限。 根據預設，[所有人]  都具有 [執行方法] 、[提供者寫入] 和 [啟用帳戶]  的權限。 使用者連線至 SMS 提供者後，會根據以角色區分的系統管理安全性權限 (如 Configuration Manager 主控台中所定義)，授與該使用者存取站台資料庫中資料的權限。 為 SMS Admins 群組明確授與在 **Root\SMS** 命名空間上的 **啟用帳戶** 和 **遠端啟用**權限。  

> [!NOTE]  
>  每位使用遠端 Configuration Manager 主控台的系統管理使用者，在站台伺服器電腦和 SMS 提供者電腦上都需要 [遠端啟用 DCOM] 權限。 雖然可將這些權限授與任何使用者或群組，但最好是將這些權限授與 SMS Admins 群組，以簡化系統管理。 如需詳細資訊，請參閱 [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) 主題中的 [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) 一節。  


##  <a name="BKMK_SMSProvNamespace"></a> 關於 SMS 提供者命名空間  
WMI 架構會定義 SMS 提供者的結構。 架構命名空間會描述 SMS 提供者架構內 Configuration Manager 資料的位置。 下表包含 SMS 提供者所使用的一些常見命名空間。  

|命名空間|說明|  
|---------------|-----------------|  
|Root\SMS\site_&lt;站台碼\>|SMS 提供者，廣泛為 Configuration Manager 主控台、資源總管、Configuration Manager 工具以及指令碼所用。|  
|Root\SMS\SMS_ProviderLocation|站台 SMS 提供者電腦的位置。|  
|Root\CIMv2|清查硬體與軟體時，清查 WMI 命名空間資訊的位置。|  
|Root\CCM|Configuration Manager 用戶端設定原則和用戶端資料。|  
|root\CIMv2\SMS|由清查用戶端代理程式收集的清查回報類別的位置。 這些設定由用戶端在評估電腦原則時所準備，且會以電腦的用戶端設定配置為基礎。|  

##  <a name="BKMK_WAIKforSMSProv"></a> SMS 提供者的作業系統部署需求  
安裝 SMS 提供者執行個體的電腦，必須具備目前使用之 Configuration Manager 版本所需的 Windows ADK 必要版本。  

 -   例如，Configuration Manager 1511 版需要 Windows 10 RTM (10.0.10240) 版本的 Windows ADK。  

 -   如需此需求的詳細資訊，請參閱[作業系統部署的基礎結構需求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

管理作業系統部署時，Windows ADK 允許 SMS 提供者可完成各式工作，像是：  

-   檢視 WIM 檔案詳細資料。  

-   新增驅動程式檔案至現有開機映像。  

-   建立開機 .ISO 檔。  


Windows ADK 安裝可能在每台安裝 SMS 提供者的電腦上，最多會需要 650 MB 的可用磁碟空間。 這個大量的磁碟空間是 Configuration Manager 安裝 Windows PE 開機映像的必要條件。  
