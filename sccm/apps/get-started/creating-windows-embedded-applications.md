---
title: "建立 Windows Embedded 應用程式 | Microsoft Docs"
description: "查看在您建立和部署 Windows Embedded 裝置的應用程式時，必須考慮的事項。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
caps.latest.revision: "7"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: cb0c22f3060ba654778dca958d620f1e1725b93c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-embedded-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 Windows Embedded 應用程式

*適用於：System Center Configuration Manager (最新分支)*

建立和部署 Windows Embedded 裝置的應用程式時，除了建立應用程式的其他 System Center Configuration Manager 需求和程序之外，還必須考慮下列項目。  

## <a name="general-considerations"></a>一般考量  

-   當您將應用程式部署至啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定是否要應用程式部署期間停用裝置上的寫入篩選器。 然後，您可以選擇在應用程式部署之後重新啟動寫入篩選器。 如果未停用寫入篩選器，即會將軟體部署為暫時重疊。 這表示，除非其他部署強制保留變更，否則將不再於重新啟動裝置時安裝軟體。  

-   當您將應用程式部署至 Windows Enbedded 裝置時，請確定裝置是已設定維護期間之集合的成員。 如此可讓您管理何時停用和啟用寫入篩選器，以及何時重新啟動裝置。  

-   控制寫入篩選器行為的設定，是一個名為 [在到期時或在維護期間認可變更 (需要重新啟動)] 的核取方塊。  

## <a name="tips-for-deploying-applications"></a>部署應用程式的秘訣  

**針對已啟用寫入篩選器的 Windows Embedded 裝置使用必要的應用程式，而不是可用的應用程式。** 因為使用者無法在已啟用寫入篩選器之 Windows Embedded 裝置的軟體中心安裝應用程式，所以一律會將具有**必要**部署用途的應用程式部署至這些裝置，而不是部署**可用**的應用程式。 通常這是可行的作法，因為執行 Windows Embedded 作業系統的電腦經常執行必須以相同方式對多位使用者執行的單一應用程式。 因此，這些裝置受到 IT 部門的高度管理及鎖定。 必要的應用程式非常適合這種情況。

 不過，如果使用者確實在啟用寫入篩選器時於嵌入式裝置上執行多個應用程式，請讓使用者瞭解下列限制：  

-   使用者無法從軟體中心安裝必要的軟體。  

-   使用者無法變更軟體中心的 [選項] 索引標籤中的工作時間。  

-   使用者無法延後必要應用程式的安裝。  

此外，如果 Configuration Manager 正在認可軟體安裝及更新的變更，低權限的使用者就無法在維護期間登入。 在此期間，使用者會看見一則訊息，說明裝置無法使用，因為正在維修。  

**如果應用程式需要使用者接受授權條款，則不要將應用程式部署到已啟用寫入篩選器的 Windows Embedded 裝置。** 停用寫入篩選器，讓 Configuration Manager 能夠在嵌入式裝置上安裝軟體時，低權限的使用者無法登入該裝置。 如果安裝需要使用者接受授權條款，就會無法進行且安裝將失敗。 如果安裝需要使用者互動，請確定未將軟體部署到 Windows Embedded 裝置。 您可以使用 [可用平台] 清單篩選這些作業系統。  
