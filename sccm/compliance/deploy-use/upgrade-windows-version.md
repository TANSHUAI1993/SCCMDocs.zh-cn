---
title: "使用 Configuration Manager 將 Windows 裝置升級至不同的版本 | Microsoft Docs"
description: "使用 Configuration Manager 自動將執行 Windows 10 桌面版、Windows 10 行動裝置版或 Windows 10 全像攝影版的裝置升級至不同的版本。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: cd8c644d07dab0010dc211df8ce4f2dc6e1fa7ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中使用版本升級原則升級 Windows 裝置

*適用於：System Center Configuration Manager (最新分支)*


System Center Configuration Manager **版本升級原則**可讓您自動將執行下列其中一個 Windows 10 版本的裝置升級至不同的版本：

- Windows 10 Desktop
- Windows 10 Mobile
<!-- - Windows 10 Holographic -->

下列是支援的升級路徑：

- 從 Windows 10 專業版到 Windows 10 企業版
- 從 Windows 10 家用版到 Windows 10 教育版
- 從 Windows 10 行動裝置版到 Windows 10 行動裝置企業版
<!-- - From Windows 10 Holographic Pro to Windows 10 Holographic Enterprise -->

裝置必須註冊於 Microsoft Intune 或執行 Configuration Manager 用戶端軟體。 此原則目前與內部部署 MDM 所管理的電腦不相容。

## <a name="before-you-start"></a>開始之前  
 在開始將裝置升級至最新版本之前，您需要下列其中一項：  

-   可以在您以原則設為目標的所有裝置上 (適用於桌面作業系統)，安裝新版本 Windows 的有效產品金鑰  

-   來自 Microsoft 的授權檔案，其中包含在您以原則設定為目標的所有裝置上 (適用於 Windows 10 行動裝置版 <!-- and Windows 10 Holographic-->) 安裝新版本 Windows 的授權資訊。

- 若要建立和部署此原則類型，您必須已獲指派 Configuration Manager「系統高權限管理員」安全性角色。

## <a name="configure-the-edition-upgrade-policy"></a>設定版本升級原則  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [Windows 10 版本升級]。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立版本升級原則] 。  

4.  按一下 [建立原則] 。  

5.  在 [建立版本升級原則精靈]  的 [一般] 頁面上，指定下列資訊：  

    -   **名稱** - 輸入版本升級原則的名稱。  

    -   **描述** (選用) - 選擇性地輸入可協助您在 Intune 主控台中識別該原則的描述。  

    -   **升級裝置用的 SKU** - 從下拉式清單選取您想將目標裝置升級到的 Windows 10 Desktop、<!-- Windows 10 Holographic,--> 或 Windows 10 行動裝置版版本。  

    -   **授權資訊** - 選取其中一個：  

        -   **產品金鑰** - 輸入有效的 Windows 10 產品金鑰，它將會用來升級執行 Windows 10 Desktop 作業系統的目標裝置。  

            > [!NOTE]  
            >  建立包含產品金鑰的原則之後，您便無法在稍後編輯產品金鑰。 這是因為金鑰基於安全性考量而隱藏。 若要變更產品金鑰，您必須重新輸入完整金鑰。  

        -   **授權檔** - 按一下 [瀏覽] 以選取 XML 格式的有效授權檔案，它將用來升級執行 <!--Windows 10 Holographic and --> Windows 10 行動裝置版作業系統的目標裝置。  

6.  完成精靈。  

新原則會顯示在 [資產與相容性]  工作區的 [Windows 10 版本升級]  節點中。  

## <a name="deploy-the-edition-upgrade-policy"></a>部署版本升級原則  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [Windows 10 版本升級]。  

3.  選取您想要部署的 Windows 10 版本升級原則，然後在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署] 。  

4.  在 [部署 Windows 10 版本升級] 對話方塊中，選擇您要部署原則的目標集合，以及原則的評估排程，然後按一下 [確定]。 針對使用 Configuration Manager 用戶端所管理的電腦，您必須將原則部署到裝置集合。 針對已向 Intune 註冊的電腦，您可以將原則部署到使用者或裝置集合。 



## <a name="next-steps"></a>後續步驟

當您從 [監視] 工作區的 [部署] 節點監視剛剛建立的部署時，可能會看見指出部署並未成功的錯誤，像是：
- **不適用於此裝置**
- **資料類型轉換失敗**

這些錯誤並不表示部署失敗。 確認在目標電腦上的升級執行成功。

原則到達目標的 Windows 電腦並進行評估之後，電腦便會在兩個小時內重新啟動以套用升級。 確定通知任何您要部署原則的使用者，或排程在非使用者工作時間執行原則。
