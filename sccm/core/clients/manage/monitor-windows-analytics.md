---
title: "監視用戶端 - 搭配使用 Windows Analytics 與 Configuration Manager | Microsoft Docs"
description: "Windows Analytics 是在 Operations Management Suite 上執行的一組解決方案，可讓您利用環境中裝置所回報的 Windows 遙測資料，取得針對環境目前狀態的珍貴深入解析。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: "23"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-windows-analytics-with-configuration-manager"></a>搭配使用 Windows Analytics 與 Configuration Manager

適用於：System Center Configuration Manager (最新分支)

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) 是在 [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) 上執行的一組解決方案。 此解決方案可讓您產生針對環境目前狀態的深入解析。 您環境中的裝置會回報 Windows 遙測資料。 此資料可透過 [Operations Management Suite 入口網站](https://mms.microsoft.com)中的解決方案進行存取及分析。 在[更新整備小幫手](/sccm/core/clients/manage/upgrade/upgrade-analytics)的案例中，您也能透過將更新整備小幫手連線至 Configuration Manager，直接從 Configuration Manager 主控台的監視節點中取得該資料。

Windows Analytics 使用的 Windows 遙測資料不會直接傳送到 Configuration Manager 站台伺服器。 用戶端電腦會將 Windows 遙測資料傳送到遙測服務。 相關資料接著會傳送到您組織其中一個 OMS 工作區所裝載的 Windows Analytics 解決方案。 然後，Configuration Manager 可透過內容相關連結將您直接引導至入口網站中的相關資料，或是直接顯示已連線至 Configuration Manager 之解決方案中的資料。 您也可以直接從 Operation Management Suite 入口網站查詢該資料。

>[!Important]
>從 Configuration Manager 站台伺服器回報給 Microsoft 的 [Configuration Manager 診斷和使用方式資料](../../plan-design/diagnostics/diagnostics-and-usage-data.md)，為完全獨立於 Windows Analytics 和 Windows 遙測。

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>設定用戶端以回報資料給 Windows Analytics

若要讓用戶端裝置將資料回報給 Windows Analytics，該裝置必須使用與裝載您組織 Windows Analytics 資料的 Operations Management Suite 工作區相關聯的商業識別碼金鑰進行設定。 該裝置也必須加以設定，來以適合您要使用之特定解決方案的遙測層級回報遙測。 

### <a name="configure-windows-analytics-client-settings"></a>設定 Windows Analytics 用戶端設定
若要設定 Windows Analytics，請在 Configuration Manager 主控台中選擇 [系統管理] > [用戶端設定]，按兩下 [建立自訂裝置用戶端設定]，然後選取 [Windows Analytics]。  

移至 [Windows Analytics] 設定索引標籤之後，請設定下列項目：
  -  **商業識別碼**  
商業識別碼索引鍵會將您所管理裝置的資訊，對應至裝載組織 Windows Analytics 資料的 OMS 工作區。 如果您已設定商業識別碼索引鍵以供「升級整備」之用，請使用該識別碼。 如果您還沒有商業識別碼索引鍵，請參閱[產生商業識別碼索引鍵 (英文)]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key)。

  -  **Windows 10 裝置的遙測層級**   
如需每個 Windows 10 遙測層級所收集項目的資訊，請參閱[設定組織的 Windows 遙測 (英文)](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels)。

  -  **加入 Windows 7、8 和 8.1 裝置上的商業資料收集**   
如需在您選擇加入後這些作業系統所收集資料的資訊，請參閱及下載 Microsoft 的 PDF 檔案 [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Windows 7、Windows 8 和 Windows 8.1 評鑑員遙測事件和欄位)。

  -  **設定網際網路探索資料收集**  
在執行 Windows 8.1 或更舊版本的裝置上，Internet Explorer 資料收集可讓「更新整備小幫手」偵測 Web 應用程式的不相容性，以便能夠順利地升級至 Windows 10。 您可以依照網際網路區域，決定是否啟用 Internet Explorer 資料收集。 如需網際網路區域的詳細資訊，請參閱[關於 URL 安全性區域 (英文)](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx)。

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>使用更新整備小幫手來識別 Windows 10 相容性問題

更新整備小幫手 (先前稱為 Upgrade Analytics) 可讓您分析裝置針對 Windows 10 的整備程度及相容性。 這項評估可讓您更順暢地升級。 將 Configuration Manager 連線到更新整備小幫手之後，您可以直接在 Configuration Manager 主控台中存取用戶端升級相容性資料。 您接著可以從裝置清單中設定要升級或修復的目標裝置。

如需如何設定和連線到更新整備小幫手的詳細資訊，請參閱[更新整備小幫手](../../clients/manage/upgrade/upgrade-analytics.md)。

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>使用 Windows Analytics 來識別 Windows 資訊保護原則中的缺口

使用 [Windows 資訊保護](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) 原則設定的 Windows 10 1703 版和更新版本的裝置，會回報在您環境中存取公司資料，但並未納入 WIP 原則應用程式規則之應用程式的遙測。 這些可能是環境中使用者需要用來保持生產力，但是被封鎖存取的應用程式，因此知道它們會存取公司資料，對於維護 Configuration Manager 中的 Windows 資訊保護原則可能會很有幫助。 

此 Windows 資訊保護資料可使用此 [Operations Management Suite 查詢](https://go.microsoft.com/fwlink/?linkid=849952) \(英文\) 存取。