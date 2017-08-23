---
title: "建立 Android 應用程式 | Microsoft Docs"
description: "查看在您建立和部署 Android 裝置的應用程式時，必須考慮的事項。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3a89abc81cd70f4e499bf4e3087fd53915377c44
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 Android 應用程式

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 應用程式有一或多種部署類型。 部署類型包含將軟體部署到裝置所需的安裝檔案和資訊。 部署類型也包含指定部署軟體之時間和方法的規則。  

 您可以使用下列兩種方式建立應用程式：  

-   透過讀取應用程式安裝檔案的方式自動建立應用程式和部署類型。  
-   手動建立應用程式並在之後新增部署類型。  
-   從檔案匯入應用程式。  

如需建立 Configuration Manager 應用程式與部署類型的必要步驟，請參閱[啟動建立應用程式精靈](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)。 此外，當您建立和部署 Android 裝置的應用程式時，請記住下列考量。  

## <a name="general-considerations-for-android-apps"></a>Android 應用程式的一般考量

Configuration Manager 支援部署下列適用於 Android 的應用程式類型：

|裝置類型|支援的檔案|
|-|-|
|Android|.apk|

支援下列部署動作：

|裝置類型|支援的動作|
|-|-|
|Android|**可用**、**必要**：使用者必須同意安裝和解除安裝。|
|Android for Work | **必要** |

## <a name="approve-and-deploy-android-for-work-apps"></a>核准和部署 Android for Work 應用程式
身為 Configuration Manager 系統管理員，您也可以在 [Play for Work 網站](https://play.google.com/work)中核准應用程式，並將這些應用程式部署到受管理的 Android for Work 裝置。

遵循下列步驟來核准 Play for Work 市集中的應用程式，並將它們與 Configuration Manager 主控台同步，然後將它們部署至受管理 Android for Work 裝置。 若要將應用程式部署至使用者的工作設定檔，您需要核准 Play for Work 市集中的應用程式，然後將應用程式與 Configuration Manager 主控台同步。

1. 開啟瀏覽器並前往︰https://play.google.com/work。
2. 使用您已繫結至 Intune 租用戶的 Google 管理帳戶登入。
3. 瀏覽您要在環境中部署的應用程式，然後對各個應用程式選擇 [核准]，讓 Android for Work 可以使用應用程式。
4. 在 Configuration Manager 主控台中，移至 [系統管理員] > [概觀] > [雲端服務] > [Android for Work]，然後選擇 [同步]。
5. 等待 10 分鐘讓應用程式同步處理，然後移至 [軟體程式庫] > [概觀] > [應用程式管理] > [市集應用程式的授權資訊]。
6. 選擇從 Play for Work 同步處理的應用程式，然後選擇 [建立應用程式]。
7. 完成精靈，然後選擇 [關閉]。
8. 移至 [軟體程式庫] > [概觀] > [應用程式管理] > [應用程式]，再選擇 Android for Work 應用程式，然後如常部署。

若要將 Play for Work 應用程式與 Configuration Manager 同步，您必須先至少核准 Play for Work 網站上的一個應用程式。
