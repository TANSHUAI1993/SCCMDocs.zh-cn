---
title: "创建自定义报表 | Microsoft Docs"
description: "定义报表模型以满足你的业务需求，然后将报表模型部署到 Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 9951dd9333ebef00c7acd5d72b20a02382e3206c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="creating-custom-report-models-for-system-center-configuration-manager-in-sql-server-reporting-services"></a>在 SQL Server Reporting Services 中的 System Center Configuration Manager 创建自定义报表模型

*适用范围：System Center Configuration Manager (Current Branch)*

示例报表模型包括在 System Center Configuration Manager 中，但也可以定义报表模型来满足自己的业务需求，然后将报表模型部署到 Configuration Manager 以在创建基于模型的新报表时使用。 下表提供了创建和部署基本报表模型的步骤。  

> [!NOTE]  
>  有关创建更高级报表模型的步骤，请参阅本主题中的 [在 SQL Server Reporting Services 中创建高级报表模型的步骤](#AdvancedReportModel) 部分。  

|步骤|描述|更多信息|  
|----------|-----------------|----------------------|  
|验证是否安装了 SQL Server Business Intelligence Development Studio|报表模型是通过使用 SQL Server Business Intelligence Development Studio 设计和构建的。 验证在你创建自定义报表模型的计算机上是否安装了 SQL Server Business Intelligence Development Studio。|有关 SQL Server Business Intelligence Development Studio 的详细信息，请参阅 SQL Server 2008 文档。|  
|创建报表模型项目|报表模型项目包含数据源的定义（.ds 文件）、数据源视图的定义（.dsv 文件）以及报表模型（.smdl 文件）。|有关详细信息，请参阅本主题中的 [创建报表模型项目](#BKMK_CreateReportModelProject) 部分。|  
|为报表模型定义数据源|创建报表模型项目之后，你必须定义一个从中提取业务数据的数据源。 通常情况下，该数据源为 Configuration Manager 站点数据库。|有关详细信息，请参阅本主题中的 [为报表模型定义数据源](#BKMK_DefineReportModelDataSource) 部分。|  
|为报表模型定义数据源视图|定义了在报表模型项目中使用的数据源之后，下一步是为项目定义数据源视图。 数据源视图是基于一个或多个数据源的逻辑数据模型。 数据源视图封装基础数据源包含的物理对象（例如表和视图）的访问权限。 SQL Server Reporting Services 通过数据源视图生成报表模型。<br /><br /> 数据源视图向你提供所指定的数据的有用表示形式，从而简化模型设计过程。 你可以重命名表和字段并在数据源视图中添加聚合字段和派生表，而无需更改基础数据源。 为了提高模型效率，请仅将你打算使用的那些表添加到数据源。|有关详细信息，请参阅本主题中的 [为报表模型定义数据源视图](#BKMK_DefineReportModelDataSourceView) 部分。|  
|创建报表模型|报表模型是数据库的一个层，它标识业务实体、字段和角色。 在发布之后，报表生成器用户可以通过使用这些模型来开发报表，而不必熟悉数据库结构或了解并编写查询。 模型由一同分组在一个友好名称下的几组相关的报表项目组成，包含这些业务项目之间的预定义关系，并包含预定义的计算。 模型是通过使用一种名为语义模型定义语言 (SMDL) 的 XML 语言定义的。 报表模型文件的文件扩展名为 .smdl。|有关详细信息，请参阅本主题中的 [To create the report model](#BKMK_CreateReportModel) 部分。|  
|发布报表模型|要通过使用刚刚创建的模型构建报表，你必须将其发布到报表服务器。 在发布模型时，模型中包括数据源和数据源视图。|有关详细信息，请参阅本主题中的 [发布报表模型以在 SQL Server Reporting Services 中使用](#BKMK_PublishReportModel) 部分。|  
|将报表模型部署到 Configuration Manager|在使用“创建报表向导”中的自定义报表模型创建基于模型的报表之前，必须将报表模型部署到 Configuration Manager。|有关详细信息，请参阅本主题中的 [将自定义报表模型部署到 Configuration Manager](#BKMK_DeployReportModel) 部分。|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>在 SQL Server Reporting Services 中创建基本报表模型的步骤  
 可以使用以下过程创建一个基本报表模型，站点中的用户可使用该模型根据 Configuration Manager 数据库的单一视图中的数据来构建基于特定模型的报表。 你创建一个报表模型，该模型向报表作者呈现有关站点中的客户端计算机的信息。 该信息来自 Configuration Manager 数据库中的 **v_R_System** 视图。  

 在你执行这些过程的计算机上，确保已安装了 SQL Server Business Intelligence Development Studio，并且计算机已通过网络连接到 Reporting Services 点服务器。 有关 SQL Server Business Intelligence Development Studio 的详细信息，请参阅 SQL Server 2008 文档。  

###  <a name="BKMK_CreateReportModelProject"></a> 创建报表模型  

1.  在桌面上，单击“开始” ，单击“Microsoft SQL Server 2008” ，然后单击“SQL Server Business Intelligence Development Studio” 。  

2.  当“SQL Server Business Intelligence Development Studio”  在 Microsoft Visual Studio 中打开后，单击“文件” ，单击“新建” ，然后单击“项目” 。  

3.  在“新建项目”  对话框的“模板”  列表中选择“报表模型项目”  。  

4.  在“名称”  框中，为此报表模型指定一个名称。 对于本例，请键入 **Simple_Model**。  

5.  要创建报表模型项目，请单击“确定” 。  

6.  “Simple_Model”  解决方案将显示在“解决方案资源管理器” 中。  

    > [!NOTE]  
    >  如果看不到“解决方案资源管理器”  窗格，请单击“视图” ，然后单击“解决方案资源管理器” 。  

###  <a name="BKMK_DefineReportModelDataSource"></a> 为报表模型定义数据源  

1.  在“SQL Server Business Intelligence Development Studio”  的“解决方案资源管理器” 窗格中，右键单击“数据源”  以选择“添加新数据源” 。  

2.  在“欢迎使用数据源向导”  页上，单击“下一步” 。  

3.  在“选择如何定义连接”  页上，验证是否选择了“基于现有连接或新连接创建数据源”  ，然后单击“新建” 。  

4.  在“连接管理器”  对话框中，为数据源指定以下连接属性：  

    -   **服务器名称**：键入 Configuration Manager 站点数据库服务器的名称，或在列表中选择该名称。 如果你使用的是命名的实例（而不是默认实例），请键入 &lt;数据库服务器>\\&lt;实例名称>。  

    -   选择“使用 Windows 身份验证” 。  

    -   在“选择或输入数据库名称”列表中，选择 Configuration Manager 站点数据库的名称。  

5.  要验证数据库连接，请单击“测试连接” 。  

6.  如果连接成功，请单击“确定”  关闭“连接管理器”  对话框。 如果连接未成功，请验证你输入的信息是否正确，然后再次单击“测试连接”  。  

7.  在“选择如何定义连接”  页上，验证是否选择了“基于现有连接或新连接创建数据源”  ，验证你刚刚指定的数据源是否在“数据连接” 中处于选定状态，然后单击“下一步” 。  

8.  在“数据源名称” 中，为数据源指定一个名称，然后单击“完成” 。 对于本例，请键入 **Simple_Model**。  

9. 数据源“Simple_Model.ds”  将显示在“解决方案资源管理器”  中的“数据源”  节点下。  

    > [!NOTE]  
    >  要编辑现有数据源的属性，请在“解决方案资源管理器”  窗格的“数据源”  文件夹中双击该数据源，以在数据源设计器中显示数据源属性。  

###  <a name="BKMK_DefineReportModelDataSourceView"></a> 为报表模型定义数据源视图  

1.  在“解决方案资源管理器” 中，右键单击“数据源视图”  以选择“添加新数据源视图” 。  

2.  在“欢迎使用数据源视图向导”  页上，单击“下一步” 。 将显示“选择数据源”  页。  

3.  在“关系数据源”  窗口中，验证“Simple_Model”  数据源是否处于选定状态，然后单击“下一步” 。  

4.  在“选择表和视图”  页上的“可用对象”  列表中选择要在报表模型中使用的以下视图： **v_R_System (dbo)**。  

    > [!TIP]  
    >  为了帮助在“可用对象”  列表中找到视图，请单击列表顶部的“名称”  标题，按字母顺序对对象进行排序。  

5.  选择视图之后，单击“&gt;” **>** 以将对象传输到  。  

6.  如果显示“名称匹配”  页，请接受默认选择，并单击“下一步” 。  

7.  选择了所需的对象后，单击“下一步” ，然后为数据源视图指定一个名称。 对于本例，请键入 **Simple_Model**。  

8.  单击 **“完成”**。 “Simple_Model.dsv”  数据源视图将显示在“解决方案资源管理器”  的“数据源视图” 文件夹中。  

###  <a name="BKMK_CreateReportModel"></a> To create the report model  

1.  在“解决方案资源管理器” 中，右键单击“报表模型”  以选择“添加新报表模型” 。  

2.  在“欢迎使用报表模型向导”  页上，单击“下一步” 。  

3.  在“选择数据源视图”  页上的“可用数据源视图”  列表中选择数据源视图，然后单击“下一步” 。 对于本例，请选择“Simple_Model.dsv” 。  

4.  在“选择报表模型生成规则”  页上，接受默认值，并单击“下一步” 。  

5.  在“收集模型统计信息”  页上，验证是否选择了“在生成前更新模型统计信息”  ，然后单击“下一步” 。  

6.  在“完成向导”  页上，为报表模型指定一个名称。 对于本例，请验证是否显示了“Simple_Model”  。  

7.  要完成向导并创建报表模型，请单击“运行” 。  

8.  要退出向导，请单击“完成” 。 报表模型将显示在“设计”窗口中。  

###  <a name="BKMK_PublishReportModel"></a> 发布报表模型以在 SQL Server Reporting Services 中使用  

1.  在“解决方案资源管理器” 中，右键单击报表模型以选择“部署” 。 对于本例，报表模型为“Simple_Model.smdl” 。  

2.  在“SQL Server Business Intelligence Development Studio”  窗口的左下角检查部署状态。 部署完成后，将显示“部署已成功”  。 如果部署失败，失败原因将显示在“输出”  窗口中。 新报表模型现在可在 SQL Server Reporting Services 网站上找到。  

3.  单击“文件” ，单击“全部保存” ，然后关闭“SQL Server Business Intelligence Development Studio” 。  

###  <a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1.  找到你在其中创建了报表模型项目的文件夹。 例如，%*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\*&lt;项目名称\>。*  

2.  将以下文件从报表模型项目文件夹复制到计算机上的一个临时文件夹。  

    -   *&lt;Model Name\>* **.dsv**  

    -   *&lt;Model Name\>* **.smdl**  

3.  使用文本编辑器（例如记事本）打开前述文件。  

4.  在文件 *&lt;Model Name\>***.dsv** 中，找到文件的第一行，其内容如下所示：  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

     编辑此行以使内容如下所示：  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine" xmlns:xsi="RelationalDataSourceView"\>**  

5.  将文件的整个内容复制到 Windows 剪贴板。  

6.  关闭文件 *&lt;Model Name\>***.dsv**。  

7.  在文件 *&lt;Model Name\>***.smdl** 中，找到文件的最后三行，其内容如下所示：  

     `</Entity>`  

     `</Entities>`  

     `</SemanticModel>`  

8.  将文件 *&lt;Model Name\>***.dsv** 的内容直接粘贴在文件 (**&lt;SemanticModel\>**) 的最后一行之前。  

9. 保存并关闭文件 *&lt;Model Name\>***.smdl**。  

10. 将文件 *&lt;Model Name\>***.smdl** 复制到 Configuration Manager 站点服务器上的文件夹 *%programfiles%*\Microsoft Configuration Manager \AdminConsole\XmlStorage\Other 中。  

    > [!IMPORTANT]  
    >  将报表模型文件复制到 Configuration Manager 站点服务器之后，必须退出并重新启动 Configuration Manager 控制台，然后才能在“创建报表向导”中使用报表模型。  

##  <a name="AdvancedReportModel"></a> 在 SQL Server Reporting Services 中创建高级报表模型的步骤  
 可以使用以下过程创建一个高级报表模型，站点中的用户可使用该模型根据 Configuration Manager 数据库的多个视图中的数据来构建基于特定模型的报表。 你将创建一个报表模型，该报表模型向报表作者呈现有关客户端计算机以及这些计算机上安装的操作系统的信息。 该信息来自 Configuration Manager 数据库中的以下视图：  

-   **V_R_System**：包含有关发现的计算机和 Configuration Manager 客户端的信息。  

-   **V_GS_OPERATING_SYSTEM**：包含有关客户端计算机上所安装的操作系统的信息。  

 会将从前述视图中选择的项目合并为一个列表、为其指定友好名称，然后在报表生成器中呈现给报表作者以包括在特定报表中。  

 在你执行这些过程的计算机上，确保已安装了 SQL Server Business Intelligence Development Studio，并且计算机已通过网络连接到 Reporting Services 点服务器。 有关 SQL Server Business Intelligence Development Studio 的详细信息，请参阅 SQL Server 文档。  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  在桌面上，单击“开始” ，单击“Microsoft SQL Server 2008” ，然后单击“SQL Server Business Intelligence Development Studio” 。  

2.  当“SQL Server Business Intelligence Development Studio”  在 Microsoft Visual Studio 中打开后，单击“文件” ，单击“新建” ，然后单击“项目” 。  

3.  在“新建项目”  对话框的“模板”  列表中选择“报表模型项目”  。  

4.  在“名称”  框中，为此报表模型指定一个名称。 对于本例，请键入 **Advanced_Model**。  

5.  要创建报表模型项目，请单击“确定” 。  

6.  “Advanced_Model”  解决方案将显示在“解决方案资源管理器” 中。  

    > [!NOTE]  
    >  如果看不到“解决方案资源管理器”  窗格，请单击“视图” ，然后单击“解决方案资源管理器” 。  

#### <a name="to-define-the-data-source-for-the-report-model"></a>为报表模型定义数据源  

1.  在“SQL Server Business Intelligence Development Studio”  的“解决方案资源管理器” 窗格中，右键单击“数据源”  以选择“添加新数据源” 。  

2.  在“欢迎使用数据源向导”  页上，单击“下一步” 。  

3.  在“选择如何定义连接”  页上，验证是否选择了“基于现有连接或新连接创建数据源”  ，然后单击“新建” 。  

4.  在“连接管理器”  对话框中，为数据源指定以下连接属性：  

    -   **服务器名称**：键入 Configuration Manager 站点数据库服务器的名称，或在列表中选择该名称。 如果你使用的是命名的实例（而不是默认实例），请键入 &lt;数据库服务器>\\&lt;实例名称>。  

    -   选择“使用 Windows 身份验证” 。  

    -   在“选择或输入数据库名称”列表中，选择 Configuration Manager 站点数据库的名称。  

5.  要验证数据库连接，请单击“测试连接” 。  

6.  如果连接成功，请单击“确定”  关闭“连接管理器”  对话框。 如果连接未成功，请验证你输入的信息是否正确，然后再次单击“测试连接”  。  

7.  在“选择如何定义连接”  页上，验证是否选择了“基于现有连接或新连接创建数据源”  ，验证你刚刚指定的数据源是否在“数据连接”  列表框中处于选定状态，然后单击“下一步” 。  

8.  在“数据源名称” 中，为数据源指定一个名称，然后单击“完成” 。 对于本例，请键入 **Advanced_Model**。  

9. 数据源“Advanced_Model.ds”  将显示在“解决方案资源管理器”  中的“数据源”  节点下。  

    > [!NOTE]  
    >  要编辑现有数据源的属性，请在“解决方案资源管理器”  窗格的“数据源”  文件夹中双击该数据源，以在数据源设计器中显示数据源属性。  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>为报表模型定义数据源视图  

1.  在“解决方案资源管理器” 中，右键单击“数据源视图”  以选择“添加新数据源视图” 。  

2.  在“欢迎使用数据源视图向导”  页上，单击“下一步” 。 将显示“选择数据源”  页。  

3.  在“关系数据源”  窗口中，验证“Advanced_Model”  数据源是否处于选定状态，然后单击“下一步” 。  

4.  在“选择表和视图”  页上的“可用对象”  列表中选择要在报表模型中使用的以下视图：  

    -   **v_R_System (dbo)**  

    -   **v_GS_OPERATING_SYSTEM (dbo)**  

     选择每个视图之后，单击“&gt;” **>** 以将对象传输到  。  

    > [!TIP]  
    >  为了帮助在“可用对象”  列表中找到视图，请单击列表顶部的“名称”  标题，按字母顺序对对象进行排序。  

5.  如果“名称匹配”  对话框出现，请接受默认选择，并单击“下一步” 。  

6.  选择了所需的对象后，单击“下一步” ，然后为数据源视图指定一个名称。 对于本例，请键入 **Advanced_Model**。  

7.  单击 **“完成”**。 “Advanced_Model.dsv”  数据源视图将显示在“解决方案资源管理器”  的“数据源视图” 文件夹中。  

#### <a name="to-define-relationships-in-the-data-source-view"></a>在数据源视图中定义关系  

1.  在“解决方案资源管理器” 中，双击“Advanced_Model.dsv”  以打开“设计”窗口。  

2.  右键单击“v_R_System”  窗口的标题栏以选择“替换表” ，然后单击“使用新建命名查询” 。  

3.  在“创建命名查询”  对话框中，单击“添加表”  图标（通常是功能区中的最后一个图标）。  

4.  在“添加表”  对话框中，单击“视图”  选项卡，在列表中选择“V_GS_OPERATING_SYSTEM”  ，然后单击“添加” 。  

5.  单击“关闭”  以关闭“添加表”  对话框。  

6.  在“创建命名查询”  对话框中，指定以下信息：  

    -   **名称** ：指定查询的名称。 对于本例，请键入 **Advanced_Model**。  

    -   **说明** ：指定查询的说明。 对于本例，请键入 **“示例 Reporting Services 报表模型”**。  

7.  在“v_R_System”  窗口的对象列表中选择要在报表模型中显示的以下项目：  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  在“v_GS_OPERATING_SYSTEM”  框的对象列表中选择要在报表模型中显示的以下项目：  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. 要将这些视图中的对象以一个列表的形式呈现给报表作者，你必须通过使用联接在两个表或视图之间指定关系。 你可以使用两个视图中均出现的“ResourceID” 对象来联接两个视图。  

10. 在“v_R_System”  窗口中，单击并按住“ResourceID”  对象，并将其拖到“v_GS_OPERATING_SYSTEM”  窗口中的“ResourceID”  对象上。  

11. 单击“确定”   

12. “Advanced_Model”  窗口将替换“v_R_System”  窗口，并为报表模型包括“v_R_System”  和“v_GS_OPERATING_SYSTEM”  视图中的所有必要的对象。 你现在可以从数据源视图设计器中删除“v_GS_OPERATING_SYSTEM”  窗口。 右键单击“v_GS_OPERATING_SYSTEM”  窗口的标题栏以选择“从 DSV 中删除表” 。 在“删除对象”  对话框中，单击“确定”  以确认删除。  

13. 单击“文件” ，然后单击“全部保存” 。  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  在“解决方案资源管理器” 中，右键单击“报表模型”  以选择“添加新报表模型” 。  

2.  在“欢迎使用报表模型向导”  页上，单击“下一步” 。  

3.  在“选择数据源视图”  页上的“可用数据源视图”  列表中选择数据源视图，然后单击“下一步” 。 对于本例，请选择“Simple_Model.dsv” 。  

4.  在“选择报表模型生成规则”  页上，不要更改默认值，并单击“下一步” 。  

5.  在“收集模型统计信息”  页上，验证是否选择了“在生成前更新模型统计信息”  ，然后单击“下一步” 。  

6.  在“完成向导”  页上，为报表模型指定一个名称。 对于本例，请验证是否显示了“Advanced_Model”  。  

7.  要完成向导并创建报表模型，请单击“运行” 。  

8.  要退出向导，请单击“完成” 。  

9. 报表模型将显示在“设计”窗口中。  

#### <a name="to-modify-object-names-in-the-report-model"></a>修改报表模型中的对象名称  

1.  在“解决方案资源管理器” 中，右键单击报表模型以选择“视图设计器” 。 对于本例，请选择“Advanced_Model.smdl” 。  

2.  在报表模型的“设计”视图中，右键单击任何对象名称以选择“重命名” 。  

3.  为所选对象键入新名称，然后按 Enter。 例如，你可以重命名对象“CSD_Version_0”  以显示“Windows Service Pack 版本” 。  

4.  完成重命名对象的操作后，单击“文件” ，然后单击“全部保存” 。  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>发布报表模型以在 SQL Server Reporting Services 中使用  

1.  在“解决方案资源管理器” 中，右键单击“Advanced_Model.smdl”  以选择“部署” 。  

2.  在“SQL Server Business Intelligence Development Studio”  窗口的左下角检查部署状态。 部署完成后，将显示“部署已成功”  。 如果部署失败，失败原因将显示在“输出”  窗口中。 新报表模型现在可在 SQL Server Reporting Services 网站上找到。  

3.  单击“文件” ，单击“全部保存” ，然后关闭“SQL Server Business Intelligence Development Studio” 。  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1.  找到你在其中创建了报表模型项目的文件夹。 例如，%*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\*&lt;项目名称\>。*  

2.  将以下文件从报表模型项目文件夹复制到计算机上的一个临时文件夹。  

    -   *&lt;Model Name\>* **.dsv**  

    -   *&lt;Model Name\>* **.smdl**  

3.  使用文本编辑器（例如记事本）打开前述文件。  

4.  在文件 *&lt;Model Name\>***.dsv** 中，找到文件的第一行，其内容如下所示：  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

     编辑此行以使内容如下所示：  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine" xmlns:xsi="RelationalDataSourceView"\>**  

5.  将文件的整个内容复制到 Windows 剪贴板。  

6.  关闭文件 *&lt;Model Name\>***.dsv**。  

7.  在文件 *&lt;Model Name\>***.smdl** 中，找到文件的最后三行，其内容如下所示：  

     `</Entity>`  

     `</Entities>`  

     `</SemanticModel>`  

8.  将文件 *&lt;Model Name\>***.dsv** 的内容直接粘贴在文件 (**&lt;SemanticModel\>**) 的最后一行之前。  

9. 保存并关闭文件 *&lt;Model Name\>***.smdl**。  

10. 将文件 *&lt;Model Name\>***.smdl** 复制到 Configuration Manager 站点服务器上的文件夹 *%programfiles%*\Microsoft Configuration Manager\AdminConsole\XmlStorage\Other 中。  

    > [!IMPORTANT]  
    >  将报表模型文件复制到 Configuration Manager 站点服务器之后，必须退出并重新启动 Configuration Manager 控制台，然后才能在“创建报表向导”中使用报表模型。  
