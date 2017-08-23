---
title: "規劃 Endpoint Protection | Microsoft Docs"
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
caps.latest.revision: "16"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6c4273dae99ec8db2cf827f463b973e876d0d35b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-endpoint-protection-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Endpoint Protection 規劃

*適用於：System Center Configuration Manager (最新分支)*


System Center Configuration Manager 中的 Endpoint Protection 可讓您管理 Configuration Manager 階層中用戶端電腦的反惡意程式碼原則和 Windows 防火牆安全性。  

> [!IMPORTANT]  
>  您必須獲授權才能使用 Endpoint Protection 管理 Configuration Manager 階層中的用戶端。  

搭配使用 Endpoint Protection 與 Configuration Manager 時，具有下列優點：  

-   設定所選電腦群組的反惡意程式碼原則和 Windows 防火牆設定，以及管理其 Windows Defender 進階威脅防護  

-   使用 Configuration Manager 軟體更新來下載最新的反惡意程式碼定義檔，讓用戶端電腦保持最新狀態  

-   傳送電子郵件通知、使用主控台內監視，以及檢視報告，以在用戶端電腦上偵測到惡意程式碼時通知系統管理使用者。  

Windows 10 電腦不需要任何其他用戶端來進行 Endpoint Protection 管理。 在 Windows 8.1 和舊版的電腦上，Endpoint Protection 除了 Configuration Manager 用戶端之外還會安裝自己的用戶端。 Endpoint Protection 用戶端具有下列功能：  

-   惡意程式碼和間諜軟體的偵測與補救  

-   Rootkit 偵測與補救  

-   重大漏洞評估以及自動定義和引擎更新  

-   透過網路檢查系統的網路漏洞偵測  

-   與雲端保護服務整合，以向 Microsoft 報告惡意程式碼。 當您加入這項服務時，如果在電腦上偵測到無法識別的惡意程式碼，則 Windows Defender 或 Endpoint Protection 用戶端可以從惡意程式碼防護中心下載最新定義。  

> [!NOTE]  
>  Endpoint Protection 用戶端可以安裝在執行 Hyper-V 的伺服器上，以及具有所支援作業系統的客體虛擬機器上。 若要避免占用過多的 CPU 使用量，Endpoint Protection 動作具有內建隨機延遲，可使服務不會同時執行。  

  此外，Configuration Manager 中的 Endpoint Protection 可讓您在 Configuration Manager 主控台中管理 Windows 防火牆設定。  

 [範例案例：使用 System Center Endpoint Protection 保護電腦免受 System Center Configuration Manager 中惡意程式碼的威脅](../deploy-use/scenarios-endpoint-protection.md)示範如何設定與管理 Endpoint Protection 和 Windows 防火牆。  

## <a name="managing-malware-with-endpoint-protection"></a>使用 Endpoint Protection 管理惡意程式碼  

Configuration Manager 中的 Endpoint Protection 可讓您建立包含 Endpoint Protection 用戶端設定的反惡意程式碼原則。 您接著可以將這些反惡意程式碼原則部署至用戶端電腦，並在 [監視] 工作區的 [Endpoint Protection 狀態] 節點中加以監視，或透過使用 Configuration Manager 報告。  

 其他資訊：  

-   [在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](../deploy-use/endpoint-antimalware-policies.md) - 使用您可以設定的設定清單，來建立、部署和監視反惡意程式碼原則的設定。  

-   [監視 System Center Configuration Manager 中的 Endpoint Protection](../deploy-use/monitor-endpoint-protection.md) - 監視活動報告、受感染的用戶端電腦等。   

-   [在 System Center Configuration Manager 中管理 Endpoint Protection 的反惡意程式碼原則和防火牆設定](../deploy-use/endpoint-antimalware-firewall.md) - 您可以變更[反惡意程式碼](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies)或[防火牆](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies)的原則優先順序、[補救用戶端電腦上找到的惡意程式碼](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware)，以及其他工作。

## <a name="managing-windows-firewall-with-endpoint-protection"></a>使用 Endpoint Protection 管理 Windows 防火牆  
 Configuration Manager 中的 Endpoint Protection 提供用戶端電腦上的 Windows 防火牆基本管理。 針對每個網路設定檔，您可以設定下列設定：  

-   啟用或停用 Windows 防火牆。  

-   阻擋連入連線 (包括允許之程式清單中的連線)。  

-   當 Windows 防火牆阻擋新程式時通知使用者。  

> [!NOTE]  
>  Endpoint Protection 僅支援管理 Windows 防火牆。  

  如需如何建立和部署 Endpoint Protection 之 Windows 防火牆原則的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的 Windows 防火牆原則](../deploy-use/create-windows-firewall-policies.md)。  

## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender 進階威脅防護

從 Configuration Manager 1606 版 (最新分支) 開始，Endpoint Protection 可以協助管理和監視 Windows Defender 進階威脅防護 (ATP)。 Windows Defender ATP 是新的服務，可協助企業偵測、調查和回應其網路的進階攻擊。 [Windows Defender 進階威脅防護](../deploy-use/windows-defender-advanced-threat-protection.md)。

## <a name="endpoint-protection-workflow"></a>Endpoint Protection 工作流程  
 下圖可協助您了解在 Configuration Manager 階層中實作 Endpoint Protection 的工作流程。  

 ![Endpoint Protection 工作流程](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>適用於 Mac 電腦和 Linux 伺服器的 Endpoint Protection 用戶端  
 System Center 包含適用於 Linux 和 Mac 電腦的 Endpoint Protection 用戶端。 Configuration Manager 未隨附這些用戶端；您必須改由 [Microsoft 大量授權服務中心](https://www.microsoft.com/licensing/servicecenter/default.aspx)下載下列產品。  

> [!IMPORTANT]  
>  您必須是 Microsoft 大量授權客戶，才能下載適用於 Linux 和 Mac 的 Endpoint Protection 安裝檔案。  

 這些產品無法從 Configuration Manager 主控台進行管理。 不過，安裝檔案隨附 System Center Operations Manager 管理組件，可讓您使用 Operations Manager 來管理適用於 Linux 的用戶端。  

 如需如何安裝和管理適用於 Linux 和 Mac 電腦之 Endpoint Protection 用戶端的詳細資訊，請使用這些產品隨附的文件 (位於 [文件]  資料夾中)。

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager 中 Endpoint Protection 的最佳做法  
 使用 System Center 2012 Configuration Manager 中之 Endpoint Protection 的下列最佳做法。  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>設定 Endpoint Protection 的自訂用戶端設定  
 設定 Endpoint Protection 的用戶端設定時，請不要使用預設用戶端設定，因為它們會將設定套用至階層中的所有電腦。 設定自訂用戶端設定而將這些設定指派給您的階層中的電腦集合中。  

 當您設定自訂用戶端設定時，您可以執行下列：  

-   自訂您的組織的不同部分的反惡意程式碼和安全性設定。  
-   先測試對一小組電腦執行 Endpoint Protection 的效果，再將它部署至整個階層。  
-   在一段時間之後，將更多用戶端新增至集合，以分階段部署 Endpoint Protection 用戶端。  

### <a name="distributing-definition-updates-by-using-software-updates"></a>使用軟體更新散發的定義更新檔  
 如果您使用 Configuration Manager 散佈定義更新的軟體更新，請考慮將程式碼定義更新放在不包含其他軟體更新的套件中。 如此一來定義更新封裝的大小較小使得複寫到更快速地發佈點。
