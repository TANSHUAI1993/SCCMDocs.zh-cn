---
title: "配置资产智能 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中设置资产智能"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 43e04a447b03885286c6c7201afb4d1b7a10aa91


---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中配置资产智能

*适用范围：System Center Configuration Manager (Current Branch)*

必须先完成一些配置步骤，然后才能使用 System Center Configuration Manager 中的资产智能清查和管理整个企业中的软件许可证使用情况。  

## <a name="steps-to-configure-asset-intelligence"></a>配置资产智能的步骤  
 要收集资产智能报表所需的清单数据，必须启用硬件清单客户端代理。 有关启用硬件清单客户端代理的信息，请参阅[如何在 System Center Configuration Manager 中扩展硬件清单](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

|步骤|详细信息|更多信息|  
|----------|-------------|----------------------|  
|**步骤 1**：启用资产智能硬件清单报表类|第一次安装 Configuration Manager 时，不会启用资产智能信息收集。 要启用资产智能，必须至少启用资产智能报表所依赖的必需硬件清单报表类之一。|有关详细信息，请参阅本主题中的以下过程： [Enable Asset Intelligence hardware inventory reporting classes](#BKMK_EnableAssetIntelligence)。|  
|**步骤 2**：安装资产智能同步点|资产智能同步点站点系统角色用于将 Configuration Manager 站点与 System Center Online 连接以同步资产智能目录信息。 只能将资产智能同步点安装在位于 Configuration Manager 层次结构顶层站点中的站点系统上，并且需要使用 TCP 端口 443 访问 Internet 以与 System Center Online 进行同步。<br /><br /> 除了下载新的资产智能目录信息之外，资产智能同步点还可以将自定义软件标题信息上载到 System Center Online 以进行分类。 Microsoft 将所有上载到 System Center Online 进行分类的软件标题信息视为公用信息。 因此，您应该确保自定义软件标题不包含机密或专有信息。 有关请求软件标题分类的详细信息，请参阅[为未分类的软件标题请求目录更新](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate)。|有关详细信息，请参阅本主题中的以下过程： [Install an Asset Intelligence Synchronization Point](#BKMK_InstallAssetIntelligenceSynchronizationPoint)。|  
|**步骤 3**：启用成功登录事件的审核|四个资产智能报表显示从客户端计算机上的 Windows 安全事件日志收集的信息。 如果安全事件日志未配置为记录所有成功登录事件，则即使启用了适当的硬件清单报表类，这些报表也不包含任何数据。 要使硬件清单客户端代理能够列出支持这些报表所需的信息，必须先在客户端上将 Windows 安全事件日志设置修改为记录所有成功登录事件，并启用 **SMS_SystemConsoleUser** 硬件清单报表类。|有关详细信息，请参阅本主题中的以下过程： [Enable auditing of success logon events](#BKMK_EnableSuccessLogonEvents)。|  
|**步骤 4**：导入软件许可证信息|导入软件许可证向导用于将 Microsoft 批量授权 (MVLS) 信息和常规许可证声明导入资产智能目录中。<br /><br /> MVLS 许可证声明包含有关 Microsoft 产品的许可授权或已购买许可证数的信息。<br /><br /> 常规许可证声明包含有关任何发布者的已购买许可证的信息。|有关详细信息，请参阅本主题中的以下过程： [Import software license information](#BKMK_ImportSoftwareLicenseInformation)。|  
|**步骤 5**：配置资产智能维护任务|以下维护任务与资产智能相关联。 默认情况下，这两项维护任务已启用并按默认计划进行配置。<br /><br /> **将应用程序标题与清单信息进行核对**：此维护任务检查软件清单中报告的软件标题是否与资产智能目录中的软件标题一致。<br /><br /> **汇总已安装软件的数据**：此维护任务提供“资产和符合性”  工作区中“资产智能”  节点下面的“已列出清单的软件”  节点中显示的信息。 该任务运行时，Configuration Manager 会收集主站点上所有已列出清单的软件标题的计数。|有关详细信息，请参阅本主题中的以下过程： [Configure Asset Intelligence maintenance tasks](#BKMK_ConfigureMaintenanceTasks)。|  

> [!NOTE]  
>  “汇总已安装软件的数据”  维护任务只能在主站点上使用。  

## <a name="supplemental-procedures-for-configuring-asset-intelligence"></a>配置资产智能的补充过程  
 请将以下信息用于上表中的步骤。  

###  <a name="a-namebkmkenableassetintelligencea-enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> 启用资产智能硬件清单报表类  
 要在 Configuration Manager 站点中启用资产智能，必须启用一个或多个资产智能硬件清单报表类。 可以在“资产智能”  主页上，或者在在“管理”  工作区的“客户端设置”  节点中的客户端设置属性中启用这些类。 使用以下过程之一可启用资产智能硬件清单报表类。  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>若要从资产智能主页启用资产智能硬件清单报表类  

1.  在 Configuration Manager 控制台中，单击“资产和符合性”。  

2.  在“资产和符合性”  工作区中，单击“资产智能” 。  

3.  在“主页”  选项卡上的“资产智能”  组中，单击“编辑清单类” 。 “编辑清单类”  对话框随即打开。  

4.  要启用资产智能报表，请选择“启用所有资产智能报表类”  或选择“仅启用选择的资产智能报表类” ，然后从显示的类中选择至少一个报表类。  

    > [!NOTE]  
    >  在客户端扫描并返回硬件清单之前，依赖于使用此过程启用的硬件清单类的资产智能报表不会显示数据。  

5.  单击“确定”  以启用所选资产智能硬件清单报表类。  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>通过客户端设置属性启用资产智能硬件清单报表类  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“客户端设置” ，然后选择“默认客户端代理设置” 。  

    > [!NOTE]  
    >  如果已创建自定义客户端设置，则可以选择自定义客户端设置而不是默认客户端设置。  

3.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。 “客户端设置属性”  对话框随即打开。  

4.  单击“硬件清单” ，然后单击“设置类” 。 “硬件清单类”  对话框随即打开。  

5.  单击“按类别筛选” ，然后单击“资产智能报表类” 。 类的列表仅使用资产智能硬件清单报表类进行刷新。  

6.  从资产智能报表类的列表中选择至少一个报表类。  

    > [!NOTE]  
    >  在客户端扫描并返回硬件清单之前，依赖于使用此过程启用的硬件清单类的资产智能报表不会显示数据。  

7.  单击“确定”  以启用所选资产智能硬件清单报表类。  

###  <a name="a-namebkmkinstallassetintelligencesynchronizationpointa-install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> 安装资产智能同步点  
 使用下列过程安装资产智能同步点站点系统角色。  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>安装资产智能同步点站点系统角色  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，然后单击“服务器和站点系统角色” 。  

3.  使用关联的步骤将资产智能同步点站点系统角色添加到新的或现有的站点系统服务器：  

    -   **新建站点系统服务器**：在“主页”  选项卡上的“创建”  组中，单击“创建站点系统服务器” 。 创建站点系统服务器向导将会打开。  

        > [!NOTE]  
        >  默认情况下，当 Configuration Manager 安装站点系统角色时，安装文件将安装在具有最多可用空闲硬盘空间的第一个可用 NTFS 格式的硬盘驱动器上。 要防止 Configuration Manager 安装在特定驱动器上，请在安装站点系统服务器之前创建一个名为 No_sms_on_drive.sms 的空文件，并将该文件复制到驱动器的根文件夹。  

    -   **现有站点系统服务器**：单击要在其中安装资产智能同步点站点系统角色的服务器。 单击服务器时，会在详细信息窗格中显示服务器上已经安装的站点系统角色的列表。  

         在“主页”  选项卡上的“服务器”  组中，单击“添加站点系统角色” 。 添加站点系统角色向导将会打开。  

4.  在“常规”  页上，指定站点系统服务器的一般设置。 向现有站点系统服务器添加资产智能同步点时，请验证以前配置的值。  

5.  在“系统角色选择”  页上，从可用角色列表中选择“资产智能同步点”  ，然后单击“下一步” 。  

6.  在“资产智能同步点连接设置”  页上，单击“下一步” 。  

     默认情况下，“使用此资产智能同步点”  设置处于选择状态，不能在此页上进行配置。 System Center Online 仅通过 TCP 端口 443接受网络流量，因此“SSL 端口号”  设置不能在向导的此页上进行配置。  

7.  （可选）可以指定指向 System Center Online 身份验证证书 (.pfx) 文件的路径，然后单击“下一步” 。 通常不会指定证书的路径，因为连接证书已在站点角色安装期间自动设置。  

8.  在“代理服务器设置”  页上，指定资产智能同步点在连接到 System Center Online 时是否使用代理服务器同步目录，以及是否要使用凭据连接到代理服务器，然后单击“下一步” 。  

    > [!WARNING]  
    >  如果代理服务器需要连接到 System Center Online，则在为代理服务器身份验证配置的帐户的用户帐户密码过期时，连接证书也可能会删除。  

9. 在“同步计划”  页上，指定是否按计划同步资产智能目录。 启用同步计划时，会指定简单或自定义同步计划。 在计划同步期间，资产智能同步点会连接到 System Center Online，以检索资产智能目录。 可以手动从 Configuration Manager 控制台中的资产智能节点同步资产智能目录。 关于手动同步资产智能目录的步骤，请参阅 [System Center Configuration Manager 中的资产智能操作](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)中的[手动同步资产智能目录](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog)部分。  

10. 在新建站点角色向导的“摘要”  页上，检查指定的设置以确保它们正确，然后再继续操作。 要对任何设置进行更改，请单击“上一步”  直到返回适当的页，进行更改，然后返回“摘要”  页。  

###  <a name="a-namebkmkenablesuccesslogoneventsa-enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> 启用对成功登录事件的审核  
 使用以下过程可配置计算机安全策略登录设置以启用成功登录事件的审核。  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>使用本地安全策略启用成功登录事件日志记录  

1.  在 Configuration Manager 客户端计算机上，单击“开始”，指向“管理工具”，然后单击“本地安全策略”。  

2.  在“本地安全策略”  对话框中的“安全设置” 下，展开“本地策略” ，然后单击“审核策略” 。  

3.  在结果窗格中，双击“审核登录事件” ，确保选中“成功”  复选框，然后单击“确定” 。  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>若要使用 Active Directory 域安全策略启用成功登录事件日志记录  

1.  在域控制器计算机上，单击“开始” ，指向“管理工具” ，然后单击“域安全策略” 。  

2.  在“本地安全策略”  对话框中的“安全设置” 下，展开“本地策略” ，然后单击“审核策略” 。  

3.  在结果窗格中，双击“审核登录事件” ，确保选中“成功”  复选框，然后单击“确定” 。  

###  <a name="a-namebkmkimportsoftwarelicenseinformationa-import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> 导入软件许可证信息  
 以下部分描述了使用导入软件许可证向导将 Microsoft 和常规软件许可证信息导入 Configuration Manager 站点数据库中所需的过程。 在将软件许可证信息从许可证声明文件导入站点数据库中时，站点服务器计算机帐户需要 NTFS 文件系统对用于导入软件许可证信息的文件共享的“完全控制”  权限。  

> [!IMPORTANT]  
>  在将软件许可证信息导入站点数据库时，现有软件许可证信息将被覆盖。 确保与导入软件许可证向导一起使用的软件许可证信息文件包含所有必需软件许可证信息的完整列表。  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>将软件许可证信息导入到资产智能目录  

1.  在“资产和符合性”  工作区中，单击“资产智能” 。  

2.  在“主页”  选项卡上的“资产智能”  组中，单击“导入软件许可证” 。 导入软件许可证向导随即打开。  

3.  在“欢迎”  页上，单击“下一步” 。  

4.  在“导入”  页上，指定是导入 Microsoft 批量许可 (MVLS) 文件（.xml 或 .csv）还是常规许可证声明文件 (.csv)。 有关创建常规许可证声明文件的详细信息，请参阅本主题后面的 [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) 。  

    > [!WARNING]  
    >  要下载可以导入资产智能目录的 .csv 格式的 MVLS 文件，请参阅 [Microsoft 批量许可服务中心](http://go.microsoft.com/fwlink/p/?LinkId=226547)。 要访问此信息，必须在网站上具有注册的帐户。 必须与 Microsoft 客户代表联系以了解有关如何获取 .xml 格式的 MVLS 文件的信息。  

5.  输入许可证声明文件的 UNC 路径，或单击“浏览”  以选择网络共享文件夹和文件。  

    > [!NOTE]  
    >  应对共享文件夹采取正确的保护措施，以防止未经授权访问许可信息文件，正在运行向导的计算机的计算机帐户必须对包含许可证导入文件的共享具有完全控制权限。  

6.  在“摘要”  页上，查看指定的信息以确保其正确无误，然后再继续操作。 要进行更改，请单击“上一步”  返回到“导入”  页。  

###  <a name="a-namebkmkcreategenerallicensestatementa-create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> 创建常规许可证声明信息文件以便导入  
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

 以下过程描述了可用于使用 Microsoft Excel 创建常规许可证声明导入文件的过程。  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>若要使用 Microsoft Excel 创建常规许可证声明导入文件  

1.  打开 Microsoft Excel 并创建新的电子表格。  

2.  在新电子表格的首行输入所有软件许可证数据字段名称。  

3.  在新电子表格的第二行及后续各行中，根据需要输入软件许可证信息。 确保为要导入的每个软件许可证在后续行中至少输入所有必需的软件许可证数据字段。 在电子表格中输入的软件标题名称必须与运行硬件清单后资源浏览器中为每个客户端计算机显示的软件标题相同。  

4.  在“文件”  菜单上，单击“另存为” ，然后将文件保存为 .csv 格式。  

5.  将该 .csv 文件复制到用于将软件许可证信息导入资产智能目录中的文件共享。  

6.  在 Configuration Manager 控制台中，使用导入软件许可证向导来导入新创建的 .csv 许可证信息文件。  

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

###  <a name="a-namebkmkconfiguremaintenancetasksa-configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> 配置资产智能维护任务  
 以下维护任务可用于资产智能：  

-   **将应用程序标题与清单信息进行核对**：此维护任务检查软件清单中报告的软件标题是否与资产智能目录中的软件标题一致。 默认情况下，此任务处于启用状态并计划在星期六凌晨 12:00 之后 到凌晨 5:00 之前运行。 此维护任务只能在 Configuration Manager 层次结构中的顶层站点上使用。  

-   **汇总已安装软件的数据**：此维护任务提供“资产和符合性”  工作区中“资产智能”  节点下面的“已列出清单的软件”  节点中显示的信息。 该任务运行时，Configuration Manager 会收集主站点上所有已列出清单的软件标题的计数。 默认情况下，此任务处于启用状态并计划在每天凌晨 12:00 之后 到凌晨 5:00 之前运行。 此维护任务只能在主站点上使用。  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>若要配置资产智能维护任务  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，然后单击“站点” 。  

3.  选择要对其配置资产智能维护任务的站点。  

    > [!NOTE]  
    >  “汇总已安装软件的数据”  维护任务只能在主站点上使用。  

4.  在“主页”  选项卡上的“设置”  组中，单击“站点维护” 。 所有可用站点维护任务的列表随即出现。  

5.  选择所需维护任务，然后单击“编辑”  以修改设置。  

6.  启用和配置维护任务。 为了最大程度减少对站点操作的干扰，建议将时间段设置为站点的非高峰时间。 时间段是可以在其间运行任务的时间间隔。 时间段由在“任务属性”  对话框中指定的“在下列时间之后开始”  和“最晚开始时间”  定义。  

    > [!WARNING]  
    >  可以通过选择当前日期并将“在下列时间之后开始”  设置为当前时间之后的几分钟，来立即启动任务。  

7.  单击“确定”  保存设置。 任务现在会根据其计划运行。  

    > [!NOTE]  
    >  如果初次尝试时任务无法运行，Configuration Manager 会尝试重新运行任务，直至任务成功运行，或直至可以在其间运行任务的时间段已过去。  



<!--HONumber=Nov16_HO1-->


