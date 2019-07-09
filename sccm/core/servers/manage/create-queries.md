---
title: 创建查询
titleSuffix: Configuration Manager
description: 了解如何在 System Center Configuration Manager 中创建和导入查询。 包括示例查询和提示。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2356547d01df346b8b5db090ea8690377c8d0dc8
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551032"
---
# <a name="create-queries-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中创建查询

适用范围：  System Center Configuration Manager (Current Branch)

本文介绍了如何在 System Center Configuration Manager 中创建和导入查询。  

##  <a name="BKMK_Create"></a> 创建查询  
 若要在 Configuration Manager 中创建查询，请使用以下过程。  

1.  在 Configuration Manager 控制台中，选择“监视”  。  

2.  在“监视”  工作区中，选择“查询”  。 在“主页”  选项卡上，选择“创建”  组中的“创建查询”  。  

3.  在“创建查询向导”  的“常规”  选项卡中，为查询指定唯一名称和可选注释。  

4.  若要导入现有查询以用作新查询的基础，请选择“导入查询语句”  。 在“浏览查询”  对话框中，依次选择要导入的查询和“确定”  。  

5.  在“对象类型”  列表中，选择希望查询返回的对象类型。 下表列出了一些可搜索的对象类型示例：  

    |对象类型|说明|  
    |-----------------|-----------------|  
    |**系统资源**|用于搜索典型系统特性，如设备的 NetBIOS 名称、客户端版本、客户端 IP 地址和 Active Directory 域服务信息。|  
    |**用户资源**|用于搜索典型用户信息，如用户名、用户组名和安全组名。|  
    |**部署**|用于搜索典型部署特性，如部署名称、计划和部署到的集合。|  

6.  选择“编辑查询语句”  ，以打开“&lt;查询名称\> 语句属性”  对话框。  

7.  在“&lt;查询名称\> 语句属性”  对话框的“常规”  选项卡中，指定此查询返回的特性，以及它们应该如何显示。 选择“新建”  图标，以添加新特性。 也可以选择“显示查询语言”  ，以直接用 WMI 查询语言 (WQL) 输入或编辑查询。 有关 WMI 查询示例，请参阅本文的[示例 WQL 查询](#BKMK_Example)部分。  

    > [!TIP]  
    > 可以参阅下面的参考文档，它们有助于你构造自己的 WQL 查询：  
    >   
    > -   [WQL (SQL for WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [WHERE 子句](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [WQL 运算符：](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  在“&lt;查询名称\> 语句属性”  对话框的“条件”  选项卡中，指定用于优化查询结果的条件。 例如，可以只返回包含站点代码 XYZ  的资源。 可以配置多个查询条件。  

    > [!IMPORTANT]  
    > 如果创建的查询中未包含任何条件，查询将在“所有系统”  集合中返回所有设备。  

9. 在“&lt;查询名称\> 语句属性”  对话框的“联接”  选项卡中，可以将两个不同特性的数据合并到查询结果中。 虽然在为查询结果选择不同的属性时，Configuration Manager 会自动创建查询联接，但“联接”  选项卡提供了更多高级选项。 Configuration Manager 支持下面这些特性类：  

    |联接类型|说明|  
    |---------------|-----------------|  
    |内部|仅显示匹配结果。 始终由自动创建的联接使用。|  
    |左|显示基属性的所有结果，同时，只显示联接属性的匹配结果。|  
    |右|显示联接特性的所有结果，以及基特性的匹配结果。|  
    |完整|显示基特性和联接特性的所有结果。|  

     若要详细了解如何使用联接运算，请参阅 SQL Server 文档。  

10. 选择“确定”  ，以关闭“&lt;查询名称\> 语句属性”  对话框。  

11. 在“创建查询向导”  的“常规”  选项卡中，指定此查询的结果是不限于集合成员、限于指定集合的成员，还是在查询每次运行时提示输入集合。  

12. 完成向导以创建查询。 新查询显示在“监视”  工作区的“查询”  节点中。  

##  <a name="BKMK_Import"></a> 导入查询  
 若要将查询导入 Configuration Manager 中，请使用以下过程。 有关如何导出查询的信息，请参阅[如何在 System Center Configuration Manager 中管理查询](../../../core/servers/manage/manage-queries.md)。  

1.  在 Configuration Manager 控制台中，选择“监视”  。  

2.  在“监视”  工作区中，选择“查询”  。 在“主页”  选项卡上，选择“创建”  组中的“导入对象”  。  

3.  在“导入对象向导”  的“MOF 文件名”  页中，选择“浏览”  ，以选择包含要导入的查询的托管对象格式 (MOF) 文件。  

4.  审阅要导入的查询的相关信息，再完成向导。 新查询显示在“监视”  工作区的“查询”  节点中。  

##  <a name="BKMK_Example"></a> Example WQL queries

此部分收录了示例 WQL 查询，可以在层次结构中使用它们，也可以出于其他目的修改它们。 若要使用这些查询，请依次选择“查询语句属性”  对话框中的“显示查询语言”  。 然后，将查询复制并粘贴到“查询语句”  字段中。  

> [!TIP]  
> 使用 `%` 通配符来表示任何字符串。 例如，`%Visio%` 将返回 Microsoft Office Visio 2010。  

### <a name="computers-that-run-windows-7"></a>运行 Windows 7 的计算机

使用以下查询返回运行 Windows 7 的所有计算机的 NetBIOS 名称和操作系统版本。  

> [!TIP]  
> 若要返回运行 Windows Server 2008 R2 的计算机，请将 `%Workstation 6.1%` 改为 `%Server 6.1%`。  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>安装特定软件包的计算机  

使用以下查询来返回安装了特定软件包的所有计算机的 NetBIOS 名称和软件包名称。 此示例返回已安装 Microsoft Visio 版本的所有计算机。 用想要查询的软件包代替 `Microsoft%Visio%`。  

> [!TIP]  
> 此查询通过使用 Windows 控制面板中程序列表中显示的名称来搜索软件包。  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>特定 Active Directory 域服务组织单位中的计算机

使用以下查询来返回指定组织单位 (OU) 中所有计算机的 NetBIOS 名称和 OU 名称。 用想要查询的 OU 的名称代替文本 `OU Name`。  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>具有特定 NetBIOS 名称的计算机

使用以下查询来返回以指定字符串开头的所有计算机的 NetBIOS 名称。 在本例中，查询会返回 NetBIOS 名称以 `ABC` 开头的所有计算机。  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a>特定类型的设备

设备类型存储在 Configuration Manager 数据库中，在 **sms_r_system** 资源类型和 **AgentEdition** 属性名称下。 若要仅检索与指定设备类型的代理版本匹配的设备，请使用以下查询：  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

对 &lt;设备 ID\> 使用下列值之一：  

|设备类型|AgentEdition 的值|  
|-----------------|---------------------------|  
|Windows 台式机或便携式计算机|0|  
|Windows 基于 ARM 的设备（运行 Windows RT）|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac 计算机|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Intel 片上系统|12|  
|UNIX 和 Linux 服务器|13|  
|Apple macOS (MDM)|14|
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|
|Android for Work|17|

 例如，若要只返回 Mac 计算机，请使用以下查询：  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>后续步骤

[如何管理查询](/sccm/core/servers/manage/manage-queries)
