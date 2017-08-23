---
title: "尋找個別應用程式 VPN 的套件系列名稱 (PFN) | Microsoft Docs"
description: "深入了解兩種方式，以尋找套件系列名稱，以便您可以設定個別應用程式 VPN。"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
caps.latest.revision: "3"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: ce50645155ecb14a82d8b982aa69c0f87dd15fbf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>尋找個別應用程式 VPN 的套件系列名稱 (PFN)

*適用於：System Center Configuration Manager (最新分支)*


有兩種方式可尋找 PFN，以便您可以設定個別應用程式 VPN。

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>為 Windows 10 電腦上已安裝的應用程式尋找 PFN

如果您正在使用的應用程式已經安裝在 Windows 10 電腦上，您可以使用 [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) PowerShell Cmdlet 來取得 PFN。

Get-AppxPackage 的語法是︰

` Parameter Set: __AllParameterSets`
` Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]`

> [!NOTE]
> 您可能必須以管理員身分執行 PowerShell，才能擷取 PFN

例如，若要取得安裝電腦上所有已安裝通用應用程式的資訊，請使用 `Get-AppxPackage`。

若要取得您知道名稱或部分名稱之應用程式的資訊，請使用 `Get-AppxPackage *<app_name>`。 請注意，如果您不確定應用程式的完整名稱，使用萬用字元會特別有幫助。 例如，要取得 OneNote 的資訊，請使用 `Get-AppxPackage *OneNote`。


以下是為 OneNote 所擷取的資訊︰

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>在應用程式未安裝在電腦上的情況下尋找 PFN

1.  請移至 https://www.microsoft.com/en-us/store/apps
2.  在搜尋列中輸入應用程式名稱。 在本例中，搜尋 OneNote。
3.  按一下應用程式的連結。 請注意，您所存取的 URL 在結尾有一系列的字母。 在本例中，URL 看起來像這樣：`https://www.microsoft.com/en-us/store/apps/onenote/9wzdncrfhvjl`
4.  在不同的索引標籤中，貼上下列 URL：`https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`，並將 `<app id>` 取代為您從 https://www.microsoft.com/en-us/store/apps 取得的應用程式識別碼 - 步驟 3 中 URL 結尾的系列字母。 在本 OneNote 範例中，您會貼上︰`https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`。

在 Edge，會顯示您想要的資訊。在 Internet Explorer 中，請按一下 [開啟] 以查看資訊。 PFN 值位於第一行。 以下是我們的範例結果看起來的樣子︰


`{`
`  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",`
`  "packageIdentityName": "Microsoft.Office.OneNote",`
`  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",`
`  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"`
`}`
