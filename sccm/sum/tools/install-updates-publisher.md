---
title: "安裝 Updates Publisher | Microsoft Docs"
description: "在您的環境中安裝 System Center Updates Publisher"
ms.custom: na
ms.date: 07/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 5c95a8b99b91531773392a77d25377465079b070
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="install-updates-publisher"></a>安裝 Updates Publisher

*適用於：System Center Updates Publisher*

本主題中的資訊可協助您取得、安裝及設定 Updates Publisher 以搭配您的環境使用。


## <a name="prerequisites-and-limitations"></a>先決條件和限制
下列各節會詳細說明安裝及使用 Updates Publisher 的需求，以及其使用上的限制或已知問題。

### <a name="operating-systems"></a>作業系統
請在下列作業系統的 64 位元版本上安裝及執行 Updates Publisher。 沒有任何最低累積更新或 Service Pack 需求。

-   Windows Server 2016 (Standard、Datacenter)
-   Windows Server 2012 R2 (Standard、Datacenter)
-   Windows 10 (專業版、教育版、專業教育版、企業版)
-   Windows 8.1 (專業版、企業版)

### <a name="prerequisites"></a>先決條件
以下是執行 Updates Publisher 之電腦的需求。

-   **64 位元作業系統**：安裝 Updates Publisher 的電腦必須執行 64 位元的作業系統。
-   **WSUS 4.0 或更新版本**：
    -   在 Windows Server 上安裝預設的「管理主控台」以符合此需求。
    -   針對 Windows 10 和 Windows 8.1，請安裝[適用於 Windows 作業系統的遠端伺服器管理工具 (RSAT) (機器翻譯)](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)。 這會安裝使用 Updates Publisher 所需的支援 (「API 和 PowerShell Cmdlet」及「使用者介面管理主控台」)。
-   **權限**：
    -   安裝：本機系統管理員
    -   大部分的作業︰本機使用者
    -   發行或是涉及 WSUS 的作業：WSUS 伺服器上 WSUS Administrators 群組的成員。

### <a name="supported-languages"></a>支援的語言
Updates Publisher 只提供英文版，但可以管理其他語言的更新。 語言支援需視工作 (例如發行、建立或編輯更新) 而定。

在匯出或發行更新時，Updates Publisher 會根據安裝 Updates Publisher 之電腦上的地區設定來顯示軟體更新的標題和描述。

例如，您可以建立具有英文和西班牙文標題的軟體更新。

-   如果您在地區設定是英文的電腦上建立該更新，根據預設您會看到英文的標題和描述。
-   如果您將該更新匯出或發行到地區設定是西班牙文的電腦，您會在該電腦上看到西班牙文的標題和描述。

### <a name="publishing"></a>發佈
當您發行軟體更新時，可以指定軟體更新二進位檔案的語言。 您也可以將二進位檔案指定為非語言相關。 支援下列語言：

-   阿拉伯文
-   中文 (香港特別行政區)
-   中文 (繁體)
-   中文 (簡體)
-   捷克文
-   丹麥文
-   荷蘭文
-   英文
-   芬蘭文
-   法文
-   德文
-   希臘文
-   希伯來文
-   匈牙利文
-   義大利文
-   日文
-   韓文
-   挪威文
-   波蘭文
-   葡萄牙文
-   葡萄牙文 (巴西)
-   俄文
-   西班牙文
-   瑞典文
-   土耳其文

### <a name="software-update-titles-and-descriptions"></a>軟體更新標題和描述
軟體更新標題和描述支援下列語言。

-   中文 (繁體)
-   中文 (簡體)
-   英文
-   法文
-   德文
-   義大利文
-   日文
-   韓文
-   葡萄牙文 (巴西)
-   俄文
-   西班牙文



## <a name="install-updates-publisher"></a>安裝 Updates Publisher
從 [Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=847967)取得用於安裝 System Center Updates Publisher 的 **UpdatesPubliser.msi**。

若要安裝 Updates Publisher，請在符合「先決條件」的裝置上執行 **UpdatesPublisher.msi**。 安裝程式會建立下列資料夾來包含執行 Updates Publisher 所需的檔案：*&lt;path&gt;\Program Files\Microsoft\UpdatesPublisher*。

因為此資料夾包含所有使用 Updates Publisher 所需的檔案，您可以將資料及其內容夾複製到新的位置或電腦，並從該位置執行 Updates Publisher。 不過，新的位置或電腦必須符合執行 Updates Publisher 的先決條件。

安裝完成之後，請執行 [UpdatesPublisher] 資料夾中的 **UpdatesPublisher.exe** 來啟動 Updates Publisher。

## <a name="next-steps"></a>後續步驟
 安裝 Updates Publisher 之後，建議您[設定 Updates Publisher 的選項](updates-publisher-options.md)。 在可以使用 Updates Publisher 的某些功能之前，您必須先設定一些選項。

 不過，如果您想要使用預設值，且沒有計畫要將更新部署到更新伺服器或受管理的裝置，則可以跳至[管理軟體更新類別目錄](updates-publisher-catalogs.md)或[建立軟體更新](create-updates-with-updates-publisher.md)，並建立您自己的更新類別目錄。

