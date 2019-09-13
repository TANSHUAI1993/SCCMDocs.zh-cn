---
title: 查找每应用 VPN 的包系列名称 (PFN)
titleSuffix: Configuration Manager
description: 了解两种查找包系列名称的方式，以便可以配置每应用 VPN。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 546cf0178993a364a4e1121e8236372162ab8481
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892314"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>查找每应用 VPN 的包系列名称 (PFN)

*适用范围：System Center Configuration Manager (Current Branch)*


有两种查找 PFN 的方式，以便可以配置每应用 VPN。

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>为安装在 Windows 10 计算机上的应用查找 PFN

如果要使用的应用已安装在 Windows 10 计算机中，可使用 [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) PowerShell cmdlet 获取 PFN。

Get-appxpackage 的语法是：

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> 可能需要以管理员身份运行 PowerShell 才能检索 PFN

例如，若要获取有关计算机上安装的所有通用应用的信息，可使用 `Get-AppxPackage`。

若要获得知道其名称或部分名称的应用的信息，可使用 `Get-AppxPackage *<app_name>`。 记下通配符的使用方法，这在不确定应用的完整名称时特别有用。 例如，若要获得 OneNote 的信息，可使用 `Get-AppxPackage *OneNote`。


下面是检索到的 OneNote 的信息：

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



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>如果计算机上未安装此应用，查找 PFN

1. 转到 https://www.microsoft.com/store/apps
2. 在搜索栏中输入应用的名称。 在本示例中，搜索 OneNote。
3. 单击应用的链接。 请注意，访问的 URL 末尾有一串字母。 在本示例中，URL 如下所示：`https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. 在不同的选项卡上，粘贴以下 URL `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`，将 `<app id>` 替换为从 https://www.microsoft.com/store/apps 获取的应用 ID，即步骤 3 中 URL 末尾的一串字母。 在本示例（OneNote 的示例）中，将粘贴：`https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`。

在 Microsoft Edge 中，将显示所需信息；在 Internet Explorer 中，单击“打开”，  查看信息。 第一行提供 PFN 值。 本示例的结果如下所示：

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```
