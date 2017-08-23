---
title: "硬體清查 | Microsoft Docs | Linux UNIX "
description: "了解如何在 System Center Configuration Manager 中使用 Linux 及 UNIX 的硬體清查。"
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b6776fbe0cfca23244d767cffd554a2ef4567a2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="hardware-inventory-for-linux-and-unix-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Linux 及 UNIX 的硬體清查

*適用於：System Center Configuration Manager (最新分支)*

Linux 和 UNIX 的 System Center Configuration Manager 用戶端支援硬體清查。 收集硬體清查之後，您可以在資源總管或 Configuration Manager 報告中執行檢視清查，並使用這項資訊來建立啟用下列作業的查詢和集合：  

-   軟體部署  

-   強制維護期間  

-   部署自訂用戶端設定  

 Linux 及 UNIX 伺服器的硬體清查使用標準式通用訊息模型 (CIM) 伺服器。 CIM 伺服器以軟體服務 (或精靈) 的身分執行，並提供以分散式管理任務推動小組 (DMTF) 標準為基礎的管理基礎結構。 CIM 伺服器所提供的功能類似於 Windows 電腦可用的 Windows 管理基礎結構 (WMI) CIM 功能。  

 從累計更新 1 開始，Linux 及 UNIX 的用戶端會使用 **Open Group** 的 1.0.6 版本 **omiserver**開放原始碼。 (在累計更新 1 之前，用戶端將 **nanowbem** 作為其 CIM 伺服器使用)。  

 CIM 伺服器會作為 Linux 及 UNIX 用戶端的一部分安裝。 Linux 及 UNIX 用戶端會直接與 CIM 伺服器通訊，而且不使用 CIM 伺服器的 WS-MAN 介面。 用戶端進行安裝時，會停用 CIM 伺服器上的 WS-MAN 連接埠。 Microsoft 開發出 CIM 伺服器，該伺服器現在作為開放原始碼，可透過 Open Management Infrastructure (OMI) 專案取得。 如需 Open Management Infrastructure 專案的詳細資訊，請參閱 [Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) 網站。  

 Linux 及 UNIX 伺服器上的硬體清查，藉由將現有的 Win32 WMI 類別和屬性對應至 Linux 及 UNIX 伺服器的對等的類別與屬性來運作。 這個一對一的類別及屬性對應，可讓 Linux 及 UNIX 的硬體清查與 Configuration Manager 整合。 Linux 及 UNIX 伺服器的清查資料，會在 Configuration Manager 主控台和報告中和 Windows 電腦中的清查一起顯示。 如此可提供一致的異質管理體驗。  

> [!TIP]  
>  您可以使用 [作業系統]  類別的 **Caption** 值來識別查詢和集合中的不同 Linux 及 UNIX 作業系統。  

##  <a name="BKMK_ConfigHardwareforLnU"></a> 設定 Linux 及 UNIX 伺服器的硬體清查  
 您可以使用預設用戶端設定，或建立自訂用戶端裝置設定來設定硬體清查。 當您使用自訂用戶端裝置設定時，您可以設定只從自己的 Linux 及 UNIX 伺服器中收集想要的類別和屬性。 您也可以指定自訂的排程，指定要在何時從 Linux 及 UNIX 伺服器中收集完整及差異清查。  

 Linux 及 UNIX 的用戶端支援 Linux 及 UNIX 伺服器可用的下列硬體清查類別：  

-   Win32_BIOS  

-   Win32_ComputerSystem  

-   Win32_DiskDrive  

-   Win32_DiskPartition  

-   Win32_NetworkAdapter  

-   Win32_NetworkAdapterConfiguration  

-   Win32_OperatingSystem  

-   Win32_Process  

-   Win32_Service  

-   Win32Reg_AddRemovePrograms  

-   SMS_LogicalDisk  

-   SMS_Processor  

 並非這些清查類別的所有內容都在 Configuration Manager 中為 Linux 及 UNIX 電腦啟用。  

##  <a name="BKMK_OperationsforHardwareforLnU"></a> 硬體清查的作業  
 從 Linux 及 UNIX 伺服器收集硬體清查之後，您可以用和檢視從其他電腦收集來的清查相同的方式，檢視並使用此資訊：  

-   使用資源總管檢視關於 Linux 及 UNIX 伺服器之硬體清查的詳細資訊。  

-   建立以特定硬體設定為基礎的查詢  

-   建立以特定硬體設定為基礎的查詢式集合  

-   執行報告，其顯示硬體設定的特定詳細資料  

 Linux 或 UNIX 伺服器上的硬體清查會根據您在用戶端設定中所設定的排程執行。 根據預設，每七天執行一次。 Linux 及 UNIX 的用戶端支援完整的清查週期和差異清查週期。  

 您也可以在 Linux 或 UNIX 伺服器上強制用戶端立即執行硬體清查。 若要執行硬體清查，在用戶端使用 **根** 認證執行下列命令以啟動硬體清查週期： **/opt/microsoft/configmgr/bin/ccmexec cd-r hinv**  

 在用戶端記錄檔中，輸入硬體清查動作 [scxcm.log] 。  

##  <a name="BKMK_CustomHINVforLinux"></a> 如何使用 Open Management Infrastructure 來建立自訂硬體清查。  
 Linux 及 UNIX 的用戶端支援您使用 Open Management Infrastructure (OMI) 所建立的自訂硬體清查。 若要執行此作業，請使用下列步驟：  

1.  使用 OMI 原始檔建立自訂清查提供者  

2.  將電腦設定成使用新的提供者以回報清查  

3.  允許 Configuration Manager 支援新的提供者  

###  <a name="BKMK_LinuxProvider"></a> 建立 Linux 及 UNIX 電腦的自訂硬體清查提供者：  
 若要建立 Linux 及 UNIX Configuration Manager 用戶端的自訂硬體清查提供者，請使用 **OMI 原始檔 - v.1.0.6** 並遵循 OMI 快速入門指南的指示。 此程序包括建立受管理物件格式 (MOF) 檔案，該檔案定義新提供者的結構描述。 稍後，您將 MOF 檔案匯入 Configuration Manager 中，以啟用新自訂清查類別的支援。  

 OMI 原始檔 - v.1.0.6 及 OMI 入門指南可從 [Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) 網站下載。 您可以在 OpenGroup.org 網站上下列網頁的 [文件]  索引標籤中找到這些下載項目： [Open Management Infrastructure (OMI)](http://go.microsoft.com/fwlink/p/?LinkId=286805)。  

###  <a name="BKMK_AddProvidertoLinux"></a> 使用自訂硬體清查提供者來設定每部執行 Linux 或 UNIX 的電腦：  
 建立自訂清查提供者之後，您必須在每部您要在其中收集清查的電腦上，複製並登錄提供者程式庫檔案。  

1.  將提供者程式庫複製到每部您要在其中收集清查的 Linux 及 UNIX 電腦。 提供者程式庫的名稱類似如下所示： **XYZ_MyProvider.so**  

2.  接下來，在每部 Linux 及 UNIX 電腦上，以 OMI 伺服器登錄提供者程式庫。 當您安裝 Linux 與 UNIX 的 Configuration Manager 用戶端時，電腦上也會安裝 OMI 伺服器，但是您必須手動登錄自訂提供者。 使用下列命令列登錄提供者： **/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so**  

3.  登錄新的提供者之後，使用 **omicli** 工具測試提供者。 當您安裝 Linux 及 UNIX的 Configuration Manager 用戶端時，**omicli** 工具會安裝在每部 Linux 和 UNIX 電腦上。 例如，在您所建立的提供者名稱為 **XYZ_MyProvider** 之處，在電腦上執行下列命令： **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     如需有關 **omicli** 的資訊及測試自訂提供者，請參閱 OMI 快速入門指南。  

> [!TIP]  
>  使用軟體發佈以部署自訂提供者，並登錄每部 Linux 及 UNIX 用戶端電腦上的自訂提供者。  

###  <a name="BKMK_AddLinuxProvidertoCM"></a> 啟用 Configuration Manager 中新的清查類別：  
 您必須先匯入定義自訂提供者之結構描述的受管理物件格式 (MOF) 檔案，Configuration Manager 才能報告 Linux 及 UNIX 電腦上新提供者所報告的清查報告。  

 若要自訂的 MOF 檔案匯入 Configuration Manager，請參閱[如何在 System Center Configuration Manager 中設定硬體清查](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)。  
