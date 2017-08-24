---
title: "配置资产智能 | Microsoft Docs"
description: "在 System Center Configuration Manager 中设置资产智能"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d2704e0f93ad9748f7eb06d714b3754463cb3bdb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中配置资产智能

*适用范围：System Center Configuration Manager (Current Branch)*

资产智能列出清单，并管理软件许可证使用情况。   

## <a name="steps-to-configure-asset-intelligence"></a>配置资产智能的步骤  
   

- **步骤 1**：若要收集资产智能报表所需的清单数据，则必须启用硬件清单客户端代理，如[如何在 System Center Configuration Manager 中扩展硬件清单](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)中所述。
- **步骤 2**：[启用资产智能硬件清单报表类](#BKMK_EnableAssetIntelligence)。  
- **步骤 3**：[安装资产智能同步点](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **步骤 4**：[启用成功登录事件的审核](#BKMK_EnableSuccessLogonEvents)  
- **步骤 5**：[导入软件许可证信息](#BKMK_ImportSoftwareLicenseInformation)  
- **步骤 6**：[配置资产智能维护任务](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 要在 Configuration Manager 站点中启用资产智能，必须启用一个或多个资产智能硬件清单报表类。 可以在“资产智能”  主页上，或者在在“管理”  工作区的“客户端设置”  节点中的客户端设置属性中启用这些类。 使用以下过程之一。  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>若要从资产智能主页启用资产智能硬件清单报表类  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “资产智能”。  

3.  在“主页”选项卡上的“资产智能”组中，选择“编辑清单类”。   

4.  若要启用资产智能报表，请选择“启用所有资产智能报表类”或“仅启用选择的资产智能报表类”，然后从显示的类中选择至少一个报表类。  

    > [!NOTE]  
    >  在客户端扫描并返回硬件清单之前，依赖于使用此过程启用的硬件清单类的资产智能报表不会显示数据。  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>通过客户端设置属性启用资产智能硬件清单报表类  

1.  在 Configuration Manager 控制台中，选择“管理” >  “客户端设置” > “默认客户端代理设置”。 如果已创建自定义客户端设置，则可以改为选择自定义客户端设置。  

3.  在“主页”选项卡 >“属性”组中，选择“属性”。   

4.  选择“硬件清单” > “设置类”。 。  

5.  选择“按类别筛选” > “资产智能报表类”。 类的列表仅使用资产智能硬件清单报表类进行刷新。  

6.  从列表中至少选择一个报表类。  

    > [!NOTE]  
    >  在客户端扫描并返回硬件清单之前，依赖于使用此过程启用的硬件清单类的资产智能报表不会显示数据。  
  

###  <a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

资产智能同步点站点系统角色用于将 Configuration Manager 站点与 System Center Online 连接以同步资产智能目录信息。 只能将资产智能同步点安装在位于 Configuration Manager 层次结构顶层站点中的站点系统上，并且需要使用 TCP 端口 443 访问 Internet 以与 System Center Online 进行同步。

除了下载新的资产智能目录信息之外，资产智能同步点还可以将自定义软件标题信息上载到 System Center Online 以进行分类。 Microsoft 将所有已上传的软件标题视为公用信息。 请确保自定义软件标题不包含机密或专有信息。 有关请求软件标题分类的详细信息，请参阅[为未分类的软件标题请求目录更新](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate)。  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>安装资产智能同步点站点系统角色  

1.  在 Configuration Manager 控制台中，选择“管理”> “站点配置” > “服务器和站点系统角色”。  

3.  将资产智能同步点站点系统角色添加到新的或现有的站点系统服务器：  

    -  对于**新站点系统服务器**：在“主页”选项卡上的“创建”组中，选择“创建站点系统服务器”以启动向导。   

        > [!NOTE]  
        >  默认情况下，当 Configuration Manager 安装站点系统角色时，安装文件将安装在具有最多可用空闲硬盘空间的第一个可用 NTFS 格式的硬盘驱动器上。 要防止 Configuration Manager 安装在特定驱动器上，请在安装站点系统服务器之前创建一个名为 No_sms_on_drive.sms 的空文件，并将该文件复制到驱动器的根文件夹。  

    -  对于**现有站点系统服务器**：选择要在其中安装资产智能同步点站点系统角色的服务器。 选择服务器时，会在详细信息窗格中显示服务器上已经安装的站点系统角色的列表。  

         在“主页”选项卡上的“服务器”组中，选择“添加站点系统角色”以启动向导。  

4.  完成“常规”页。 向现有站点系统服务器添加资产智能同步点时，请验证以前配置的值。  

5.  在“系统角色选择”页上，从可用角色列表中选择“资产智能同步点”。  

6.  在“资产智能同步点连接设置”页上，选择“下一步”。  

     默认情况下，“使用此资产智能同步点”  设置处于选择状态，不能在此页上进行配置。 System Center Online 仅通过 TCP 端口 443接受网络流量，因此“SSL 端口号”  设置不能在向导的此页上进行配置。  

7.  （可选）可以指定指向 System Center Online 身份验证证书 (.pfx) 文件的路径。 通常不会指定证书的路径，因为连接证书已在站点角色安装期间自动设置。  

8.  在“代理服务器设置”页上，指定资产智能同步点在连接到 System Center Online 时是否使用代理服务器同步目录，以及是否要使用凭据连接到代理服务器。  

    > [!WARNING]  
    >  如果代理服务器需要连接到 System Center Online，则在为代理服务器身份验证配置的帐户的用户帐户密码过期时，连接证书也可能会删除。  

9. 在“同步计划”  页上，指定是否按计划同步资产智能目录。 启用同步计划时，会指定简单或自定义同步计划。 在计划同步期间，资产智能同步点会连接到 System Center Online，以检索资产智能目录。 可以手动从 Configuration Manager 控制台中的资产智能节点同步资产智能目录。 关于手动同步资产智能目录的步骤，请参阅 [System Center Configuration Manager 中的资产智能操作](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)中的[手动同步资产智能目录](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog)部分。  

10. 完成向导 

###  <a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 四个资产智能报表显示从客户端计算机上的 Windows 安全事件日志收集的信息。 下面介绍了如何配置计算机安全策略登录设置以启用对成功登录事件的审核。  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>使用本地安全策略启用成功登录事件日志记录  

1.  在 Configuration Manager 客户端计算机上，选择“启动” > “管理工具” > “本地安全策略”。  

2.  在“本地安全策略”对话框中的“安全设置”下，展开“本地策略”，然后选择“审核策略”。  

3.  在结果窗格中，双击“审核登录事件”，确保选中“成功”复选框，然后选择“确定”。  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>若要使用 Active Directory 域安全策略启用成功登录事件日志记录  

1.  在域控制器计算机上，选择“开始”，指向“管理工具”，然后选择“域安全策略”。  

2.  在“本地安全策略”对话框中的“安全设置”下，展开“本地策略”，然后选择“审核策略”。  

3.  在结果窗格中，双击“审核登录事件”，确保选中“成功”复选框，然后选择“确定”。  

###  <a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 以下部分描述了使用导入软件许可证向导将 Microsoft 和常规软件许可证信息导入 Configuration Manager 站点数据库中所需的过程。 在将软件许可证信息从许可证声明文件导入站点数据库中时，站点服务器计算机帐户需要 NTFS 文件系统对用于导入软件许可证信息的文件共享的“完全控制”  权限。  

> [!IMPORTANT]  
>  在将软件许可证信息导入站点数据库时，现有软件许可证信息将被覆盖。 确保与导入软件许可证向导一起使用的软件许可证信息文件包含所有必需软件许可证信息的完整列表。  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>将软件许可证信息导入到资产智能目录  

1.  在“资产和符合性”工作区中，选择“资产智能”。  

2.  在“主页”选项卡上的“资产智能”组中，选择“导入软件许可证”。   

4.  在“导入”  页上，指定是导入 Microsoft 批量许可 (MVLS) 文件（.xml 或 .csv）还是常规许可证声明文件 (.csv)。 有关创建常规许可证声明文件的详细信息，请参阅本主题后面的 [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) 。  

    > [!WARNING]  
    >  要下载可以导入资产智能目录的 .csv 格式的 MVLS 文件，请参阅 [Microsoft 批量许可服务中心](http://go.microsoft.com/fwlink/p/?LinkId=226547)。 要访问此信息，必须在网站上具有注册的帐户。 必须与 Microsoft 客户代表联系以了解有关如何获取 .xml 格式的 MVLS 文件的信息。  

5.  输入许可证声明文件的 UNC 路径，或选择“浏览”以选择网络共享文件夹和文件。  

    > [!NOTE]  
    >  应对共享文件夹采取正确的保护措施，以防止未经授权访问许可信息文件，正在运行向导的计算机的计算机帐户必须对包含许可证导入文件的共享具有完全控制权限。  

6. 完成向导。  

###  <a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 还可以使用以逗号分隔 (.csv) 文件格式手动创建的许可证导入文件将常规许可证声明导入资产智能目录中。  

> [!NOTE]  
>  只有当“名称” 、“发布者” 、“版本” 和“有效数量”  字段需要包含数据时，才必须在许可证导入文件的首行输入所有字段。 所有日期字段都应采用以下格式显示：月/日/年，例如 08/04/2008。  

资产智能使用产品名称和产品版本（而不是发布者名称）对常规许可证声明中指定的产品进行匹配。 你必须在常规许可证声明中使用与站点数据库中存储的产品名称完全匹配的产品名称。 资产智能采用常规许可证声明中提供的“有效数量”数字，将该数字与 Configuration Manager 清单中找到的已安装产品数进行比较。  

> [!TIP]  
>  要获取 Configuration Manager 站点数据库中存储的产品名称的完整列表，可以在站点数据库上运行以下查询：SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE。  

 可以为产品指定精确版本，或指定部分版本，如仅指定主要版本。 以下示例提供针对特定产品的常规许可证声明版本条目的生成版本匹配项。  

|常规许可证声明条目|匹配的站点数据库条目|  
|-------------------------------------|------------------------------------|  
|名称：“MySoftware”，ProductVersion0：“2”|ProductName0：“Mysoftware”，ProductVersion0：“2.01.1234”<br /><br /> ProductName0：“MySoftware”，ProductVersion0：“2.02.5678”<br /><br /> ProductName0：“MySoftware”，ProductVersion0：“2.05.1234”<br /><br /> ProductName0：“MySoftware”，ProductVersion0：“2.05.5678”<br /><br /> ProductName0：“MySoftware”，ProductVersion0：“2.05.3579.000”<br /><br /> ProductName0：“MySoftware”，ProductVersion0：“2.10.1234”|  
|Name：“MySoftware”，Version“2.05”|ProductName0：“MySoftware”，ProductVersion0：“2.05.1234”<br /><br /> ProductName0：“MySoftware”，ProductVersion0：“2.05.5678”<br /><br /> ProductName0：“MySoftware”，ProductVersion0：“2.05.3579.000”|  
|名称：“Mysoftware”，Version“2”<br /><br /> 名称：“Mysoftware”，Version“2.05”|导入过程中出错。 当多个条目与相同产品版本匹配时，导入失败。|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>若要使用 Microsoft Excel 创建常规许可证声明导入文件  

1.  打开 Microsoft Excel 并创建新的电子表格。  

2.  在新电子表格的首行输入所有软件许可证数据字段名称。  

3.  在新电子表格的第二行及后续各行中，根据需要输入软件许可证信息。 确保为要导入的每个软件许可证在后续行中至少输入所有必需的软件许可证数据字段。 在电子表格中输入的软件标题名称必须与运行硬件清单后资源浏览器中为每个客户端计算机显示的软件标题相同。  

4.  以 .csv 格式保存文件。  

5.  将该 .csv 文件复制到用于将软件许可证信息导入资产智能目录中的文件共享。  

6.  在 Configuration Manager 控制台中，使用导入软件许可证向导来导入新创建的 .csv 文件。  

7.  运行资产智能“许可证 15A - 第三方软件对帐报表”，验证许可信息是否已成功导入资产智能目录。  

> [!NOTE]  
>  有关可用于测试目的的常规软件许可证文件的示例，请参阅 [System Center Configuration Manager 中的资产智能常规许可证导入文件示例](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md)。  

#### <a name="sample-table-to-describe-software-licenses"></a>用于描述软件许可证的示例表  
 在创建常规许可证声明导入文件时，下表中的信息可用于描述要导入资产智能目录中的软件许可证。  

|列名称|数据类型|必需|示例|  
|-----------------|---------------|--------------|-------------|  
|名称|最多 255 个字符|是|软件标题|  
|发布服务器|最多 255 个字符|是|软件发布者|  
|版本|最多 255 个字符|是|软件标题版本|  
|语言|最多 255 个字符|是|软件标题语言|  
|首行|整数值|是|购买的许可证数|  
|PO 编号|最多 255 个字符|否|订单信息|  
|经销商名称|最多 255 个字符|否|经销商信息|  
|购买日期|日期值格式如下：MM/DD/YYYY|否|许可证的购买日期|  
|购买的支持|位值|否|0 或 1：如果“是”，则输入 0；如果为“否”，则输入 1|  
|支持到期日期|日期值格式如下：MM/DD/YYYY|否|购买的支持的结束日期|  
|注释|最多 255 个字符|否|可选备注|  

###  <a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 以下维护任务可用于资产智能：  

-   **将应用程序标题与清单信息进行核对**：检查软件清单中报告的软件标题是否与资产智能目录中的软件标题一致。 默认情况下，此任务处于启用状态并计划在星期六凌晨 12:00 之后 到凌晨 5:00 之前运行。 此维护任务只能在 Configuration Manager 层次结构中的顶层站点上使用。  

-   **汇总已安装软件的数据**：提供“资产和符合性”工作区中“资产智能”节点下面的“已列出清单的软件”节点中显示的信息。 该任务运行时，Configuration Manager 会收集主站点上所有已列出清单的软件标题的计数。 默认情况下，此任务处于启用状态并计划在每天凌晨 12:00 之后 到凌晨 5:00 之前运行。 此维护任务只能在主站点上使用。  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>若要配置资产智能维护任务  

1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” > “站点”。  

3.  选择要对其配置资产智能维护任务的站点。  

4.  在“主页”选项卡上的“设置”组中，选择“站点维护”。 选择一项任务，然后选择“编辑”，以修改设置。 

    我们建议将时间段设置为该站点的非高峰期。 时间段是可以在其间运行任务的时间间隔。 时间段由在“任务属性”  对话框中指定的“在下列时间之后开始”  和“最晚开始时间”  定义。  

    可以通过选择当前日期并将“在下列时间之后开始”  设置为当前时间之后的几分钟，来立即启动任务。  

7.  选择“确定”保存设置。 任务现在会根据其计划运行。  

    > [!NOTE]  
    >  如果初次尝试时任务无法运行，Configuration Manager 会尝试重新运行任务，直至任务成功运行，或直至可以在其间运行任务的时间段已过去。  
