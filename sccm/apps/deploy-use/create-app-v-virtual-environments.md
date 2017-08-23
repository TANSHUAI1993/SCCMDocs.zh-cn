---
title: "建立 App-V 虛擬環境 | Microsoft Docs"
description: "使用 Microsoft Application Virtualization 建立虛擬環境，讓應用程式可以彼此共用資料。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 377ed9732fb16b062f53e78504aea394acdb7462
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中建立 App-V 虛擬環境

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager (Configuration Manager) 的 Microsoft Application Virtualization (App-V) 虛擬環境中，已部署的虛擬應用程式可以在用戶端 Windows 電腦上共用同一個檔案系統和登錄。 不同於標準的虛擬應用程式，這些應用程式可以互相共用資料。 當已安裝應用程式或是在用戶端下次評估已安裝的應用程式時，用戶端電腦上便會建立或修改虛擬環境。 您可以排序這些應用程式，當有多個應用程式嘗試修改檔案系統或登錄值時，順序最高的應用程式便會優先修改。  

> [!IMPORTANT]  
>  請勿完全依賴 App-V 虛擬環境所提供的安全性保護，例如防範惡意程式碼。  

 請使用以下程序在 Configuration Manager 中建立 App-V 虛擬環境。  

## <a name="create-an-app-v-virtual-environment"></a>建立 App-V 虛擬環境  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [App-V 虛擬環境]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立虛擬環境]。  

4.  在 [建立虛擬環境] 對話方塊中，輸入下列資訊：  

    -   **名稱**。  輸入虛擬環境的唯一名稱 (長度上限為 128 個字元)。  

    -   **描述**。 (選擇性) 輸入虛擬環境的描述。  

5.  若要將新的部署類型新增至該虛擬環境，請選擇 [新增]。 您至少必須新增一種部署類型。  

6.  在 [新增應用程式] 對話方塊中，指定 「群組名稱」 (長度上限為 128 個字元)。 您將使用此名稱來表示新增至虛擬環境的應用程式群組。  

7.  選擇 [新增]，選取要新增至該群組的 App-V 5 應用程式及部署類型，然後選擇 [確定]。  

8.  如果有多個應用程式嘗試修改同一個虛擬環境中的檔案系統或登錄設定，您可以在 [新增應用程式] 對話方塊中選取 [升序] 或 [降序] 以設定應用程式的的優先順序。  

9. 若要返回 [建立虛擬環境] 對話方塊，請選擇 [確定]。  

10. 完成新增群組之後，選擇 [確定] 建立虛擬環境。 新的虛擬環境會顯示在 Configuration Manager 主控台的 [APP-V 虛擬環境] 節點中。 您可以使用 [App-V 虛擬環境狀態]報告來監視虛擬環境的狀態。  

    > [!NOTE]  
    >  當已安裝應用程式或是在用戶端下次評估已安裝的應用程式時，便會在用戶端電腦上新增或修改該虛擬環境。  
