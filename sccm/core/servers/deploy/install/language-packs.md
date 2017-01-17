---
title: "语言包 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中可用的语言支持。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 35d1008752a3275febef46b8817e97afdb91d580


---
# <a name="language-packs-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的语言包

*适用范围：System Center Configuration Manager (Current Branch)*

本主题提供有关 System Center Configuration Manager 中的语言支持的技术详细信息。  

##  <a name="a-namebkmksuplanguagepacksa-supported-operating-system-languages"></a><a name="BKMK_SupLanguagePacks"></a>支持的操作系统语言  
 通过在管理中心站点和主站点中安装 **服务器语言包** 或 **客户端语言包** ，可以安装支持下列显示语言的功能。 在将安装程序作为先决条件和可再发行文件的下载的一部分运行时，会下载语言包。 在运行安装程序之前，你还可以使用 [Setup Downloader](setup-downloader.md) 来下载这些文件。 在安装站点期间，你从可用的语言包文件中选择要在该站点支持的服务器和客户端语言。  

 使用下表将区域设置 ID 对应到你要在服务器或客户端上支持的语言。 有关区域设置 ID 的详细信息，请参阅 MSDN 联机库中的 [Locale IDs Assigned by Microsoft（Microsoft 指定的区域设置 ID）](http://go.microsoft.com/fwlink/p/?LinkId=252609) 。  

### <a name="server-languages"></a>服务器语言  

|服务器语言|区域设置 ID (LCID)|三个字母的代码|  
|---------------------|------------------------|-----------------------|  
|英语（默认）|0409|ENU|  
|中文（繁体，香港特别行政区）|0c04|ZHH|  
|中文（简体）|0804|CHS|  
|中文（繁体，台湾）|0404|CHT|  
|捷克语|0405|CSY|  
|荷兰语 - 荷兰|0413|NLD|  
|法语|040c|FRA|  
|德语|0407|DEU|  
|匈牙利语|040e|HUN|  
|意大利语 - 意大利|0410|ITA|  
|日语|0411|JPN|  
|朝鲜语|0412|KOR|  
|波兰语|0415|PLK|  
|葡萄牙语 - 巴西|0416|PTB|  
|葡萄牙语 - 葡萄牙|0816|PTG|  
|俄语|0419|RUS|  
|西班牙语 - 西班牙|0c0a|ESN|  
|瑞典语|041d|SVE|  
|土耳其语|041f|TRK|  

### <a name="client-languages"></a>客户端语言  

|客户端语言|区域设置 ID (LCID)|三个字母的代码|  
|---------------------|------------------------|-----------------------|  
|英语（默认）|0409|ENG|  
|中文（繁体，香港特别行政区）|0c04|ZHH|  
|中文 - 简体|0804|CHS|  
|中文（繁体，台湾）|0404|CHT|  
|捷克语|0405|CSY|  
|丹麦语|0406|DAN|  
|荷兰语 - 荷兰|0413|NLD|  
|芬兰语|040b|FIN|  
|法语|040c|FRA|  
|德语|0407|DEU|  
|希腊语|0408|ELL|  
|匈牙利语|040e|HUN|  
|意大利语 - 意大利|0410|ITA|  
|日语|0411|JPN|  
|朝鲜语|0412|KOR|  
|挪威语|0414|NOR|  
|波兰语|0415|PLK|  
|葡萄牙语（巴西）|0416|PTB|  
|葡萄牙语（葡萄牙）|0816|PTG|  
|俄语|0419|RUS|  
|西班牙语 - 西班牙|0c0a|ESN|  
|瑞典语|041d|SVE|  
|土耳其语|041f|TRK|  

### <a name="mobile-device-client-languages"></a>移动设备客户端语言  
 在添加对移动设备语言的支持时，会将所有移动设备客户端语言都包括在内。 对于移动设备支持，你无法选择个别语言包。  

### <a name="how-to-identify-installed-language-packs"></a>如何识别已安装的语言包  
对于运行 Configuration Manager 客户端的计算机，通过在其注册表中查看已安装的语言包的区域设置 ID (LCID)，可以识别在此计算机上安装的语言包。 此信息位于下列位置：  

-   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

可以使用硬件清单来收集此信息，然后创建自定义报表以查看语言详细信息。 有关收集自定义硬件清单的信息，请参阅[如何在 System Center Configuration Manager 中配置硬件清单](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)。 有关创建报表的信息，请参阅 [System Center Configuration Manager 中报表的操作和维护](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md)主题中的[管理 Configuration Manager 报表](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports)部分。  



<!--HONumber=Dec16_HO3-->


