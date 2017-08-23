---
title: "建立查詢 | Microsoft Docs"
description: "探索如何在 System Center Configuration Manager 中建立和匯入查詢。 包含範例查詢和秘訣。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9f38d86ff6227bb6ea88c358a3d61242372d449e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中建立查詢

適用於：System Center Configuration Manager (最新分支)

您可以使用本主題來協助在 System Center Configuration Manager 中建立或匯入查詢。  

##  <a name="BKMK_Create"></a> 如何建立查詢  
 使用這個程序，協助您在 Configuration Manager 中建立查詢。  

#### <a name="to-create-a-query"></a>建立查詢  

1.  在 Configuration Manager 主控台中，選擇 [監視]。  

2.  在 [監視] 工作區中，選擇 [查詢]。 接著，在 [常用] 索引標籤的 [建立] 群組中，選擇 [建立查詢]。  

3.  在 [建立查詢精靈]  的 [一般] 索引標籤上，指定查詢的唯一名稱和選擇性註解。  

4.  如果您想要匯入現有的查詢來作為新查詢的基礎，請選擇 [匯入查詢陳述式]。 在 [瀏覽查詢] 對話方塊中，選取您要匯入的現有查詢，然後選擇 [確定]。  

5.  在 [物件類型] 清單中，選取您要查詢傳回的物件類型。 下表描述您可以搜尋之物件類型的一些範例：  

    |物件型別|說明|  
    |-----------------|-----------------|  
    |**系統資源**|用來搜尋一般系統屬性，例如裝置的 NetBIOS 名稱、用戶端版本、用戶端 IP 位址和 Active Directory 網域服務資訊。|  
    |**使用者資源**|用來搜尋一般使用者資訊，例如使用者名稱、使用者群組名稱和安全性群組名稱。|  
    |**部署**|用來搜尋部署的一般屬性，例如部署名稱、排程和所部署的目標集合。|  

6.  選擇 [編輯查詢陳述式] 以開啟 [&lt;查詢名稱\> 陳述式內容] 對話方塊。  

7.  在 [&lt;查詢名稱\> 陳述式內容] 對話方塊的 [一般] 索引標籤上，指定這個查詢會傳回的屬性及其顯示方式。 選擇**新增**圖示以新增新屬性。 您也可以選擇 [顯示查詢語言]，直接以 WMI 查詢語言 (WQL) 輸入或編輯查詢。 如需 WMI 查詢的範例，請參閱本主題中的 [Example WQL queries](#BKMK_Example) 一節。  

    > [!TIP]  
    > 您可以使用下列 MSDN 參考文件，來協助您建構自己的 WQL 查詢：  
    >   
    > -   [WQL (適用於 WMI 的 SQL)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [WHERE 子句](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [WQL 運算子](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  在 [&lt;查詢名稱\> 陳述式內容] 對話方塊的 [準則] 索引標籤上，指定用來縮小查詢結果的準則。 例如，您可以在查詢結果中，只傳回具有 **XYZ** 之站台碼的資源。 您可以設定查詢的多項準則。  

    > [!IMPORTANT]  
    > 如果您建立未包含任何準則的查詢，此查詢會傳回 [所有系統]  集合中的所有裝置。  

9. 在 [&lt;查詢名稱\> 陳述式內容] 對話方塊的 [聯結] 索引標籤上，可以將來自兩個不同屬性的資料結合為您的查詢結果。 雖然當您為查詢結果選擇不同的屬性時，Configuration Manager 便會自動建立查詢聯結，不過 [聯結] 索引標籤提供更進階的選項。 下表顯示 System Center 2012 Configuration Manager 所支援的屬性類別：  

    |聯結類型|說明|  
    |---------------|-----------------|  
    |內部|只顯示相符的結果，自動建立的聯結一律會使用。|  
    |左方|顯示基底屬性的所有結果，但只顯示聯結屬性的相符結果。|  
    |右方|顯示聯結屬性的所有結果，但只顯示基底屬性的相符結果。|  
    |完整|顯示基底屬性和聯結屬性的所有結果。|  

     如需如何使用聯結作業的詳細資訊，請參閱您的 SQL Server 文件。  

10. 選擇 [確定] 關閉 [&lt;查詢名稱\> 陳述式內容] 對話方塊。  

11. 在 [建立查詢精靈] 的 [一般] 索引標籤上，指定這個查詢的結果是否不限於集合的成員、是否限於指定集合的成員，或是否要在每次執行查詢時提示輸入集合。  

12. 完成精靈以建立查詢。 新的查詢會顯示在 [監視]  工作區的 [查詢]  節點中。  

##  <a name="BKMK_Import"></a> 如何匯入查詢  
 使用這個程序，協助您將查詢匯入 Configuration Manager 中。 如需如何匯出查詢的相關資訊，請參閱[如何在 System Center Configuration Manager 中管理查詢](../../../core/servers/manage/manage-queries.md)。  

#### <a name="to-import-a-query"></a>匯入查詢  

1.  在 Configuration Manager 主控台中，選擇 [監視]。  

2.  在 [監視] 工作區中，選擇 [查詢]。 在 [常用] 索引標籤的 [建立] 群組中，選擇 [匯入物件]。  

3.  在 [匯入物件精靈] 的 [MOF 檔案名稱] 頁面上，選擇 [瀏覽] 以選取包含您要匯入之查詢的受管理物件格式 (MOF) 檔案。  

4.  檢閱要匯入之查詢的相關資訊，然後完成精靈。 新的查詢會顯示在 [監視] 工作區的 [查詢] 節點中。  

##  <a name="BKMK_Example"></a> Example WQL queries

本節包含範例 WMI 查詢，您可以在階層中使用，或針對其他目的進行修改。 若要使用這些查詢，請選擇 [查詢陳述式內容] 對話方塊中的 [顯示查詢語言]。 然後，將查詢複製並貼入 [查詢陳述式] 欄位。  

> [!TIP]  
> 使用萬用字元 `%` 來代表任何字元字串。 例如，`%Visio%` 會傳回 Microsoft Office Visio 2010。  

### <a name="computers-that-run-windows-7"></a>執行 Windows 7 的電腦

使用下列查詢可傳回執行 Windows 7 之所有電腦的 NetBIOS 名稱和作業系統版本。  

> [!TIP]  
> 若要傳回執行 Windows Server 2008 R2 的電腦，請將 `%Workstation 6.1%` 變更為 `%Server 6.1%`。  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>已安裝特定軟體套件的電腦  

使用下列查詢可傳回已安裝特定軟體封裝之所有電腦的 NetBIOS 名稱和軟體封裝名稱。 這個範例會顯示已安裝 Microsoft Visio 版本的所有電腦。 請以您要查詢的軟體套件取代 `%Visio%`。  

> [!TIP]  
> 這個查詢會使用 Windows 控制台之程式清單中所顯示的名稱，來搜尋軟體封裝。  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit"></a>位於特定 Active Directory Domain Services 組織單位的電腦

使用下列查詢以傳回指定 OU 中所有電腦的 NetBIOS 名稱和組織單位 (OU) 名稱。 請以您要查詢的 OU 名稱取代文字 `OU Name`。  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>具有特定 NetBIOS 名稱的電腦

使用下列查詢可傳回開頭為特定字元字串之所有電腦的 NetBIOS 名稱。 在這個範例中，此查詢會傳回 NetBIOS 名稱開頭為 `ABC` 的所有電腦。  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> 特定類型的裝置

裝置類型會儲存在 Configuration Manager 資料庫中的資源類別 **sms_r_system** 和屬性名稱 **AgentEdition** 底下。 針對符合您所指定裝置類型代理程式版本的裝置，使用下列查詢來擷取這些裝置：  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

使用下列其中一個 *&lt;裝置識別碼\>* 值：  

|裝置類型|AgentEdition 的值|  
|-----------------|---------------------------|  
|Windows 桌上型電腦或膝上型電腦|0|  
|Windows ARM 型裝置 (執行 Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac 電腦|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Intel 晶片式系統|12|  
|UNIX 和 Linux 伺服器|13|  

 例如，如果您要讓查詢只傳回 Mac 電腦，請使用下列查詢：  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>請參閱  
 [System Center Configuration Manager 中查詢的作業和維護](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
