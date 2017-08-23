---
title: "選取 Configuration Manager 的探索方法 | Microsoft Docs"
description: "檢閱考量以決定要使用的方法以及執行這些方法的站台。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4b6be888be2ad6c1f5e7c0be33d9830bb870114e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>選取在 System Center Configuration Manager 使用的探索方法

*適用對象：System Center Configuration Manager (最新分支)*

若要順利有效地使用 System Center Configuration Manager 探索，您必須考慮要使用的方法以及執行這些方法的站台。  

 由於探索作業會產生大量的網路流量，且產生的探索資料記錄 (DDR) 會在處理期間耗用龐大的 CPU 資源，因此請只使用達成目標所需的探索方法。 您可以從只使用一或兩個探索方法開始，之後再以節制的方式啟用其他方法來延伸您環境中的探索層級。 本主題中的資訊可以協助您做出明智的決策。  

 如需不同探索方法的相關資訊，請參閱[關於 System Center Configuration Manager 的探索方法](../../../../core/servers/deploy/configure/about-discovery-methods.md)。  

## <a name="select-methods-to-discover-different-things"></a>選取探索不同項目的方法  
 若要探索潛在的 Configuration Manager 用戶端電腦或使用者資源，您必須啟用適當的探索方法。 您可以使用不同的探索方法組合來尋找不同的資源，以及探索與這些資源有關的其他資訊。 您使用的探索方法會決定已探索的資源類型，以及在探索程序中使用哪些 Configuration Manager 服務和代理程式。 同時會決定與可探索之資源相關的資訊類型。  

### <a name="discover-computers"></a>探索電腦   
當您要探索電腦時，您可以使用「Active Directory 系統探索」或「網路探索」。  

 例如，如果您要在使用用戶端推入安裝之前探索可安裝 Configuration Manager 用戶端的資源，您可執行 Active Directory 系統探索。 使用這種方法，您不只會探索資源，還會探索基本資訊，甚至是來自 Active Directory 網域服務探索的額外資訊。 此資訊將有助於建立複雜的查詢與集合，以用來指派用戶端設定或內容部署。

或者，您也可以執行網路探索並使用其選項來探索資源的作業系統 (稍後使用用戶端推入安裝時需要)。 網路探索可提供您使用其他探索方法無法取得之網路拓撲的相關資訊。 不過，此方法不會提供任何與您的 Active Directory 環境有關的資訊。

 還有一種方法稱為「活動訊號探索」。 您可以只使用活動訊號探索來強制探索使用用戶端推入安裝以外的方法所安裝的用戶端。 不過，與其他探索方法不同的是，活動訊號探索無法探索沒有作用中 Configuration Manager 用戶端的電腦。 它會傳回一組有限的資訊，目的在於維護現有資料庫記錄，而非作為該記錄的基礎。 活動訊號探索提交的資訊可能不足以建立複雜的查詢或集合。  

 如果您使用「Active Directory 群組探索」來探索指定群組的成員資格，您可以探索有限的系統或電腦資訊。 這並不會取代電腦的完整探索，但可提供基本資訊。 此資訊並不足以執行用戶端推入安裝。  

### <a name="discover-users"></a>探索使用者   
當您要探索與使用者有關的資訊時，請使用「Active Directory 使用者探索」。 與 Active Directory 系統探索類似，此方法會探索 Active Directory 的使用者。 它包含除了延伸 Active Directory 資訊以外的基本資訊。 您可以使用此資訊來建立與電腦應用類似的複雜查詢和集合。  

### <a name="discover-group-information"></a>探索群組資訊   
當您要探索與群組和群組成員資格有關的資訊時，請使用「Active Directory 群組探索」。 此探索方法會建立安全性群組的資源記錄。  

 您可以使用此方法來搜尋特定的 Active Directory 群組，以便在該群組內的任何巢狀群組外還能識別該群組的成員。 您也可以使用此方法來搜尋群組的 Active Directory 位置，並以遞迴方式在 Active Directory 網域服務中搜尋該位置的每個子容器。  

 此探索方法也可搜尋發佈群組的成員資格。 並可識別使用者及電腦的群組關係。  

 當您探索群組時，您也可以探索與其成員相關的有限資訊。 不過，這不會取代 Active Directory 系統或使用者探索方法。 通常不足以建置複雜查詢和集合，也無法作為用戶端推入安裝的基礎。  

### <a name="discover-infrastructure"></a>探索基礎結構   
您可以使用兩種方法來探索網路基礎結構，分別是「Active Directory 樹系探索」和「網路探索」。  

 使用 Active Directory 樹系探索來搜尋 Active Directory 樹系，以尋找與子網路和 Active Directory 站台設定有關的資訊。 然後這些設定會自動輸入至 Configuration Manager 作為界限位置。  

 當您想要探索網路拓撲時，可使用網路探索。 雖然其他探索方法會傳回與 Active Directory 網域服務相關的資訊並可識別用戶端的目前網路位置，但不提供以子網路和網路路由器拓撲為基礎的基礎結構資訊。  

##  <a name="bkmk_shared"></a> 站台間可共用探索資料  
 在 Configuration Manager 將探索資料新增至資料庫時，會在階層內的所有站台間快速共用這些資料。 由於在階層的多個站台中探索相同的資訊通常沒有好處，因此請考慮為您用於在單一站台上執行的各個探索方法設定單一執行個體。 最好是這麼做，而不是在不同站台上執行單一方法的多個執行個體。  

 不過，多個站台指派相同的探索方法，但每個方法皆使用不同的設定和排程，對有些環境可能很有用。 例如，使用網路探索時，您可能會想要引導每個站台探索其本機網路，而不是嘗試透過 WAN 探索所有網路位置。

如果您設定相同探索方法的多個執行個體在不同站台上執行，請仔細規劃每個站台的設定。 您想要避免有兩個或多個站台探索您網路或 Active Directory 的相同資源。 這樣可能會耗用額外的網路頻寬並建立重複 DDR。

下表說明您可以在哪些站台設定不同的探索方法。  

|探索方法|支援的位置|  
|----------------------|-------------------------|  
|Active Directory 樹系探索|管理中心網站<br /><br /> 主要網站|  
|Active Directory 群組探索|主要網站|  
|Active Directory 系統探索|主要網站|  
|Active Directory 使用者探索|主要網站|  
|活動訊號探索<sup>1</sup>|主要網站|  
|網路探索|主要網站<br /><br /> 次要網站|  

 <sup>1</sup> 次要站台無法設定活動訊號探索，但可以從用戶端接收活動訊號 DDR。  

 當次要站台執行網路探索，或接收活動訊號探索 DDR 時，會經由檔案複寫將 DDR 傳送到其父主要站台。 這是因為只有主要站台和管理中心網站可以處理 DDR。 如需如何處理 DDR 的詳細資訊，請參閱[關於探索資料記錄](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs)。  

## <a name="considerations-for-different-discovery-methods"></a>考量不同的探索方法  
 因為每個站台伺服器和網路環境都不同，所以最好限制探索的初始設定。 接著仔細監視各站台伺服器處理所產生之探索資料的能力。  

當您要針對系統、使用者或群組使用 **Active Directory** 探索方法時：  

-   在採用快速網路與您的網域控制站連線的站台上執行探索。  

-   考慮使用 Active Directory 複寫拓撲以確定探索可存取最新資訊。  

-   考慮探索設定的範圍，並將探索限制在這些 Active Directory 位置，以及您必須探索的群組。  

如果您使用「網路探索」：  

-   使用有限的初始設定來識別您的網路拓撲。  

-   在識別網路拓撲後，請將網路探索設定在您想要進行完全探索之網路區域中央的特定站台上執行。  

由於「活動訊號探索」不會在特定站台執行，因此您不需要在規劃執行探索位置時考慮到它。  

##  <a name="bkmk_best"></a> 探索的最佳作法  
若要獲得探索的最佳結果，建議執行下列動作︰

 - **先執行 Active Directory 系統探索和 Active Directory 使用者探索，再執行 Active Directory 群組探索。**  

 當 Active Directory 群組探索識別出先前未探索到的使用者或電腦為群組的成員時，會嘗試探索使用者或電腦的基本詳細資料。 由於 Active Directory 群組探索並未針對這種探索類型進行最佳化，因此此程序可能會造成它的執行速度過慢。 此外，Active Directory 群組探索只會識別所探索之使用者和電腦的相關基本詳細資料，並不會建立完整的使用者或電腦探索記錄。 當您執行 Active Directory 系統探索和 Active Directory 使用者探索時，可使用各物件類型的其他 Active Directory 屬性。 因此，Active Directory 群組探索可以更有效地執行。  

- **當您設定 Active Directory 群組探索時，只能指定您搭配 Configuration Manager 使用的群組。**  

 若要有效控制 Active Directory 群組探索使用的資源，請在搭配 Configuration Manager 使用時僅指定這些群組。 這是因為 Active Directory 群組探索會以遞迴方式搜尋各個群組，以探索使用者、電腦及巢狀群組。 搜尋各個巢狀群組可能會延伸 Active Directory 群組探索的範圍，並降低效能。 此外，當您設定 Active Directory 群組探索的差異探索時，探索方法會監視各個群組的變更。 這麼做可能會在該方法必須搜尋不必要的群組時，使效能更為降低。  

- **使用完整探索之間較長的間隔時間，以及較頻繁差異探索時間，設定探索方法。**  

 由於差異探索會使用比完整探索週期更少的資源，而且可以識別 Active Directory 中新增或修改的資源，因此您可以將完整探索週期頻率降低為每週執行一次或不到一週執行一次。 Active Directory 系統探索、Active Directory 使用者探索和 Active Directory 群組探索的差異探索，會識別幾乎所有 Active Directory 物件的變更，進而能維持準確的資源探索資料。  

- **在具有最接近 Active Directory 網域控制站之網路位置的主要站台上，執行 Active Directory 探索方法。**  

 若要改善 Active Directory 探索的效能，最好是在採用快速網路與網域控制站連線的主要站台上執行探索。 如果要在多個站台上執行相同的 Active Directory 探索方法，請設定各種探索方法以避免重疊。 和舊版 Configuration Manager 不同的是，站台之間可共用探索資料。 因此，並不需要在多個站台探索相同的資訊。 如需詳細資訊，請參閱[站台之間可共用探索資料](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared)。  

- **當您想要從探索資料自動建立界限時，只能在一個站台上執行 Active Directory 樹系探索。**  

 如果您要在階層的一個以上的站台上執行 Active Directory 樹系探索，則最好只在單一站台啟用自動建立界限的選項。 這是因為當 Active Directory 樹系探索在各個站台執行並建立界限時，Configuration Manager 無法將這些界限合併為單一界限物件。 當您將 Active Directory 樹系探索設定為在多個站台自動建立界限時，可能會在 Configuration Manager 主控台產生重複的界限物件。  
