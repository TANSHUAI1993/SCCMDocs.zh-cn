---
title: "適用性規則 | Microsoft Docs"
description: "管理 System Center Updates Publisher 的適用性規則"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 2925abda07abaa46ad56b9b433ce003c22aede5e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>管理 Updates Publisher 中的適用性規則

*適用於：System Center Updates Publisher*

透過 Updates Publisher，適用性規則可定義裝置在可以安裝更新之前，必須符合的需求。 這些規則也用來判斷電腦是否已安裝特定更新。 包含多個部分的複雜適用性規則稱為規則集。

更新配套不會使用適用性規則。

## <a name="overview-of-applicability-rules"></a>適用性規則概觀
您可從 [規則工作區] 管理適用性規則。 當您建立規則時，會指定一或多個條件。 指定多個條件時，您可以設定條件之間的關係，以依序評估這些條件，或是將它們合併為邏輯 **And** 或 **Or** 陳述式。

例如，以下是包含三個規則的規則集。 第一項規則會確認 *MyFile* 檔案是否存在，而第二和第三項規則會確認 Windows 作業系統的語言為英文或日文。

    And  
      File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
      Or  
        Windows Language is English   
        Windows Language is Japanese

所有更新都需要至少一個適用性規則。 匯入的更新皆已套用適用性規則，而當您建立自己的更新時，必須將一或多個規則新增至這些更新。 您可以在 Updates Publisher 中修改和擴展任何更新的規則。

若要檢視您已建立的規則，請在 [規則工作區] 中，從 [我的已儲存規則] 清單選取規則。 該規則的個別條件和邏輯作業會顯示在主控台的 [適用性規則] 窗格中。 您所匯入之更新的規則，僅可在編輯該更新時進行檢視與修改。

您可以在 Updates Publisher 中的兩個位置建立規則：

-   您可以在 [規則工作區] 中建立規則集，並「儲存」已供稍後使用。 編輯或建立更新時，您可以選取 [已儲存規則] 做為 [規則類型]，然後從預先建立的規則集清單中選取。

-   您也可以在建立或編輯更新時建立新的規則。 以這種方式建立的規則，將不會儲存以供日後使用。

## <a name="create-applicability-rule"></a>建立適用性規則
下列資訊與您從[建立更新精靈](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard)中建立規則的方式類似。 但與精靈不同的是，您可以儲存規則集以供日後使用。

1.  在 [規則工作區] 中，選擇 [建立] 以開啟 [建立規則] 精靈。

2.  指定規則的名稱，然後按一下 [新規則]![](media/newrule.png)。 這會開啟可以設定規則的 [適用性規則] 頁面。

3.  針對 [規則類型]，請選取下列其中一項。 您必須設定的選項會視每個類型而有所不同：

    -   **檔案** – 使用此規則來要求裝置必須有屬性符合您所指定之一或多個準則的檔案，才能安裝此更新。

    -   **登錄 –** 使用此類型來指定在裝置能安裝此更新之前，必須存在的登錄詳細資料。

    -   **系統 –** 此規則會使用系統詳細資料來判斷適用性。 您可以選擇定義 Windows 版本、Windows 語言或處理器架構，或是指定 WMI 查詢來識別裝置的作業系統。

    -   **Windows Installer -** 使用此規則類型，根據已安裝的 .MSI 或 Windows Installer 修補程式 (.MSP) 來判斷適用性。 做為需求的一部分，您也可以判斷是否已安裝特定的元件或功能。

       > [!IMPORTANT]   
       > 在受管理的裝置上，Windows Update 代理程式無法偵測針對個別使用者安裝的 Windows Installer 套件。 當您使用此規則類型時，請設定其他的適用性規則 (例如檔案版本或登錄機碼值)，以正確地偵測到 Windows Installer 套件，無論它是否針對個別使用者或個別系統進行安裝。

    -   **已儲存規則** – 此選項可讓您尋找和使用先前所設定與儲存的規則。

4.  請視需要繼續新增與設定其他規則。

5.  使用邏輯作業按鈕來針對不同的規則進行排序和分組，以建立更複雜的必要條件檢查。

6.  規則集完成後，請按一下 [確定] 來儲存它。 規則集現在會出現在 [我的已儲存規則] 清單中。

## <a name="edit-applicability-rule-sets"></a>編輯適用性規則集
若要編輯適用性規則，請在 [規則工作區] 中，選取已儲存在 [我的已儲存規則] 清單中的任何規則，然後從功能區選擇 [編輯]。 這會開啟 [編輯規則] 精靈。

[編輯規則] 精靈會顯示規則集的目前規則。 編輯規則的方式與使用 [建立規則] 精靈建立新規則的方式相同。 您可以使用此精靈來重新命名規則集、刪除規則、重新排序規則和關係，或新增新的規則。

完成變更之後，請選擇 [確定] 來儲存變更並關閉精靈。

如需有關使用規則精靈的詳細資料，請參閱[建立更新精靈](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard)的「步驟 7」適用性頁面。

## <a name="delete-applicability-rules"></a>刪除適用性規則
若要刪除已儲存的適用性規則，請從 [規則工作區] 的 [我的已儲存規則] 清單中選取規則或規則集，然後從功能區選擇 [刪除]。 這會從 Updates Publisher 移除已儲存規則或規則集。

若要刪除特定更新中的規則，您必須[編輯更新](/sccm/sum/tools/manage-updates-with-updates-publisher#edit-updates-and-bundles)。
