---
title: "资产智能简介 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中的资产智能简介。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 879dc3f04f361af955afbc4db180d097073e8d41
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-asset-intelligence-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的资产智能简介

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的资产智能允许使用资产智能目录清查和管理整个企业中的软件许可证使用情况。 许多硬件清单 Windows Management Instrumentation (WMI) 类扩大了收集的有关所用硬件和软件标题的信息的广度。 超过 60 个报表以易于使用的格式显示此信息。 这些报表有很多链接至更具针对性的报表，在其中可以查询常规信息和钻取至更详细的信息。 可以将自定义信息添加到资产智能目录，如自定义软件类别、软件家族、软件标签和硬件要求。 还可以连接到 System Center Online，用最新的可用信息动态更新资产智能目录。 Microsoft 客户可以通过将软件许可证信息导入 Configuration Manager 站点数据库中，来协调企业软件许可证与已购买并正在使用的软件许可证的使用。  

##  <a name="BKMK_AssetIntelligenceCatalog"></a> 资产智能目录  

 Configuration Manager 资产智能目录是存储在站点数据库中的一组数据库表，它们包含超过 300,000 个软件标题和版本的分类和标识信息。 这些数据库表也用于管理特定软件标题的硬件要求。  

 资产智能目录提供所使用的软件标题的软件许可证信息（属于 Microsoft 和非 Microsoft 软件）。 资产智能目录中提供了软件标题的一组预定义硬件要求，可以创建新的用户定义的硬件要求信息以满足自定义要求。 此外，可以自定义资产智能目录中的信息，并且可以将软件标题信息上载到 System Center Online 以进行分类。  

 包含新发布软件的资产智能目录更新可供定期下载以执行批量目录更新。 或者，可以使用资产智能同步点站点系统角色动态更新目录。  

###  <a name="BKMK_SoftwareCategories"></a> 软件类别  
 资产智能软件类别可用于对已列出清单的软件标题进行广泛的分类，也可用作更具体的软件家族的高级别分组。 例如，软件类别可以是能源公司，而该软件类别中的软件家族可以是石油和天然气或水力电气。 在资产智能目录中预定义了许多软件类别，并且可以创建用户定义的类别以额外定义已列出清单的软件。 所有预定义的软件类别的验证状态始终为“已验证” ，而添加到资产智能目录的自定义软件类别信息是“用户定义” 。 有关如何管理软件类别的详细信息，请参阅[在 System Center Configuration Manager 中配置资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

> [!NOTE]  
>  存储在资产智能目录中的预定义软件类别信息是只读的，无法更改或删除。 管理用户可以添加、修改或删除用户定义的软件类别。  

###  <a name="BKMK_SoftwareFamilies"></a> 软件家族  
 资产智能软件家族可用于定义软件类别中的已列出清单的软件标题。 在资产智能目录中预定义了许多软件家族，并且可以创建用户定义的类别以额外定义已列出清单的软件。 所有预定义的软件家族的验证状态始终为“已验证” ，而添加到资产智能目录的自定义软件家族信息是“用户定义” 。 有关如何管理软件家族的详细信息，请参阅[在 System Center Configuration Manager 中配置资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

> [!NOTE]  
>  预定义软件家族信息是只读的，无法更改。 管理用户可以添加、修改或删除用户定义的软件家族。  

###  <a name="BKMK_CustomLabels"></a> 软件标签  
 资产智能自定义软件标签使你可以创建筛选器，可使用它们对软件标题进行分组并使用资产智能报表查看它们。 可以使用软件标签创建共享公共属性的软件标题的用户定义组。 例如，可以创建一个名为“共享件”的软件标签，将该软件标签与已列出清单的共享件标题相关联，然后运行报表以显示具有关联“共享件”软件标签的所有软件标题。 未预定义软件标签。 软件标签的验证状态始终是“用户定义” 。 有关如何管理软件标签的详细信息，请参阅[在 System Center Configuration Manager 中配置资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

###  <a name="BKMK_HardwareRequirements"></a> 硬件要求  
 对软件标题进行软件部署前，可以使用硬件要求来验证计算机是否满足软件标题的硬件要求。 可以在“资产和符合性”  工作区中的“资产智能”  节点下的“硬件要求”  节点下，管理软件标题的硬件要求。 资产智能目录中预定义了许多硬件要求，你可以创建新的用户定义的硬件要求信息以满足自定义要求。 所有预定义硬件要求的验证状态始终为“已验证” ，而添加到资产智能目录的用户定义硬件要求是“用户定义” 。 有关如何管理硬件要求的详细信息，请参阅[在 System Center Configuration Manager 中配置资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

> [!NOTE]  
>  Configuration Manager 控制台中显示的硬件要求均从资产智能目录检索，并且不基于 System Center 2012 Configuration Manager 客户端的已列出清单的软件标题信息。 硬件要求信息不作为 System Center Online 同步过程的一部分进行更新。 你可以为没有关联硬件要求的清单软件创建用户定义的硬件要求。  

 默认情况下，为列出的每项硬件要求显示下列信息：  

-   **软件标题**：指定与硬件要求相关联的软件标题。  

-   **最低 CPU (MHz)**：指定软件标题所需的最低处理器速度，以兆赫 (MHz) 为单位。  

-   **最小 RAM (KB)**：指定软件标题所需的最小 RAM，以 KB 为单位。  

-   **最小磁盘空间(KB)**：指定软件标题所需的最小可用硬盘空间，以 KB 为单位。  

-   **最小磁盘大小 (KB)**：指定软件标题所需的最小硬盘大小，以 KB 为单位。  

-   **验证状态**：指定硬件要求的验证状态。  

 存储在资产智能目录中的预定义硬件要求是只读的，无法删除。  管理用户可以添加、修改或删除未存储在资产智能目录中的软件标题的用户定义硬件要求。  

##  <a name="BKMK_InventoriedSoftwareTitles"></a> 已列出清单的软件标题  
 可以在“资产和符合性”  工作区中的“资产智能”  节点下的“已列出清单的软件”  节点下，查看已列出清单的软件标题信息。 硬件清单客户端代理基于存储在资产智能目录中的软件标题，从 Configuration Manager 客户端收集已列出清单的软件信息。  

> [!WARNING]  
>  硬件清单客户端代理基于启用的资产智能硬件清单报表类收集清单。 有关如何启用报表类的详细信息，请参阅[在 System Center Configuration Manager 中配置资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

 默认情况下，为每个已列出清单的软件标题显示下列信息：  

-   **名称**：指定已列出清单的软件标题的名称。  

-   **供应商**：指定开发已列出清单的软件标题的供应商名称。  

-   **版本**：指定已列出清单的软件标题的产品版本。  

-   **类别**：指定已列出清单的软件标题当前所分配的软件类别。  

-   **家族**：指定已列出清单的软件标题当前所分配的软件家族。  

-   **标签** [“1”、“2” 和“3” ]：指定与软件标题关联的自定义标签。 已列出清单的软件标题可以与最多三个自定义标签关联。  

-   **计数**：指定对软件标题列出清单的 Configuration Manager 客户端数。  

-   **状态**：指定已列出清单的软件标题的验证状态。  

> [!NOTE]  
>  只能在层次结构中的顶层站点上为已列出清单的软件更改分类信息（产品名称、供应商、软件类别和软件家族）。 修改预定义软件的分类信息之后，软件的验证状态会从“已验证”  更改为“用户定义” 。  

##  <a name="AssetIntelligenceSycnronizationPoint"></a> 资产智能同步点  
 资产智能同步点是一个用于连接到 System Center Online（使用 TCP 端口 443）以管理动态资产智能目录信息更新的 Configuration Manager 站点系统角色。 此站点角色只能安装在层次结构的顶层站点上。 必须使用连接到顶层站点的 Configuration Manager 控制台配置所有资产智能目录自定义。 虽然所有更新都必须在顶层站点上配置，但是资产智能目录信息会复制到层次结构中的其他站点。 使用资产智能同步点站点角色可以请求与 System Center Online 进行按需目录同步或者计划自动目录同步。 除了下载新的资产智能目录信息之外，资产智能同步点还可以将自定义软件标题信息上载到 System Center Online 以进行分类。 Microsoft 将所有上载到 System Center Online 进行分类的软件标题信息视为公用信息。 因此，应确保自定义软件标题不包含机密或专有信息。  

> [!NOTE]  
>  提交了未分类的软件标题，并且客户对相同软件标题至少进行了 4 次分类请求之后，System Center Online 研究人员会进行标识、分类，然后将软件标题分类信息提供给正在使用联机服务的所有客户。 表示最多分类请求的软件标题会收到最高优先级以进行分类。 自定义软件和业务线应用程序不大可能接收类别，作为最佳做法，不应将这些软件标题发送给 Microsoft 进行分类。  

> [!NOTE]  
>  需要资产智能同步点站点系统角色才能连接到 System Center Online。 有关如何安装资产智能同步点的信息，请参阅[在 System Center Configuration Manager 中配置资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

##  <a name="BKMK_AssetIntelligenceHomePage"></a> “资产智能”主页  
 “资产和符合性”工作区中的“资产智能”节点是 Configuration Manager 中的资产智能主页。 “资产智能”  主页显示资产智能目录信息的摘要仪表板视图。  

> [!NOTE]  
>  在查看“资产智能”  主页时，它不会自动更新。  

 “资产智能”  主页包含以下部分：  

-   **目录同步**：提供有关是否启用资产智能和资产智能同步点当前状态的信息。 该部分还提供同步计划、是否导入客户许可证声明、上次更新状态的时间和下一个计划更新的时间以及安装资产智能同步点站点系统之后发生的更改数。  

    > [!NOTE]  
    >  如果安装了资产智能同步点站点系统角色，则仅显示“资产智能”  主页的“资产智能目录同步”部分。  

-   **清单软件状态**：提供已列出清单的软件、软件类别以及由 Microsoft 标识、由管理员标识、等待联机标识或未标识并且未等待的软件家族的计数和百分比。 以表格式显示的信息显示每种对象的计数，以图表显示的信息显示每个对象的百分比。  

##  <a name="BKMK_AssetIntelligenceReports"></a> 资产智能报表  
 资产智能报表位于 Configuration Manager 控制台中，在“监视”工作区中“报表”节点下的“资产智能”文件夹中。 这些报表提供有关硬件、许可证管理和软件的信息。 有关 Configuration Manager 中报表的详细信息，请参阅 [System Center Configuration Manager 中的报表](../../../../core/servers/manage/reporting.md)。  

> [!NOTE]  
>  资产智能报表中显示的已安装软件标题和许可证信息的数量的准确性可能会与安装的软件标题或环境中使用的许可证的实际数量不同。 形成这种差异的原因是为企业环境中安装的软件标题清点软件许可证信息所涉及的复杂依赖关系和限制。 请勿将资产智能报表用作确定所购买软件许可证符合性的唯一来源。  

###  <a name="BKMK_HardwareReports"></a> 资产智能硬件报表  
 资产智能硬件报表提供有关组织中硬件资产的信息。 使用硬件清单信息（例如速度、内存、外围设备等），资产智能硬件报表可以显示有关 USB 设备、必须升级的硬件乃至未准备好执行特定软件升级的计算机的信息。  

> [!NOTE]  
>  资产智能硬件报表中的一些用户数据是从系统安全事件日志收集的。 为实现更好的报表准确性，建议在将计算机重新分配给新用户时清除此日志。  

###  <a name="BKMK_LicenseManagementReports"></a> 资产智能许可证管理报表  
 资产智能许可证管理报表提供有关正在使用的许可证的数据。 “许可证分类帐”报表以与 Microsoft 许可证声明 (MLS) 一致的格式列出已安装的 Microsoft 应用程序。 这提供了将购买的许可证与使用的许可证配对的简便方法。 其他许可证管理报表提供有关充当针对操作系统激活统计信息运行密钥管理服务 (KMS) 的服务器的计算机的信息。  

> [!IMPORTANT]  
>  有几个资产智能许可证管理报表可提供有关 KMS（一种管理批量许可的方法）的功能的信息。 如果尚未实施 KMS 服务器，某些报表可能不返回任何数据。 有关 KMS 的详细信息，请在 [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225)上搜索 KMS。  

###  <a name="BKMK_SoftwareReports"></a> 资产智能软件报表  
 资产智能软件报表提供有关组织中计算机上安装的软件家族、类别和特定软件标题的信息。 软件报表可显示有关浏览器帮助程序对象、自动启动的软件等的信息。 这些报表可用于识别广告软件、间谍软件和其他恶意软件，并且可以标识软件冗余，从而有助于简化软件购买和支持。  

###  <a name="BKMK_SoftwareIdTagReports"></a> 资产智能软件标识标记报表  
 资产智能软件标识标记报表提供有关包含符合 ISO/IEC 19770-2 标准的软件标识标记的软件的信息。 软件标识标记提供用于标识安装的软件的授权信息。 启用 SMS_SoftwareTag 硬件清单报表类时，Configuration Manager 会收集有关具有软件标识标记的软件的信息。 以下报表提供有关软件的信息：  

-   **软件 14A - 搜索启用软件标识标记的软件**：此报表提供启用了软件标识标记的已安装软件的计数。  

-   **软件 14B - 安装有启用特定软件标识标记的软件的计算机**：此报表列出安装了启用特定软件标识标记的软件的所有计算机。  

-   **软件 14C - 特定计算机上所安装的启用软件标识标记的软件**：此报表列出特定计算机上启用了特定软件标识标记的所有已安装软件。  

###  <a name="BKMK_ReportingLImitations"></a> 资产智能报表限制  
 资产智能报表可以提供有关安装的软件标题及已购买且正在使用的软件许可证的大量信息。 然而，不应该将这些信息用作确定所购买软件许可证符合性的唯一来源。  

####  <a name="BKMK_ExampleDependencies"></a> 示例依赖关系  
 资产智能报表中显示的已安装软件标题和许可证信息的数量的准确性可能会与当前使用的实际数量不同。 形成这种差异的原因是为企业环境中使用的软件标题清点软件许可证信息所涉及的复杂依赖关系。 以下举例演示了在使用资产智能的企业中，对可能影响资产智能报表准确性的已安装软件列出清单所涉及的依赖关系：  

 **客户端硬件清单依赖关系**  
 资产智能安装的软件报表基于通过扩展硬件清单启用资产智能报表，从 Configuration Manager 客户端收集的数据。 因为对硬件清单报表的这种依赖关系，资产智能报表将仅反映来自在启用了必需的资产智能 WMI 报表类的情况下，成功完成硬件清单进程的 Configuration Manager 客户端的数据。 另外，因为 Configuration Manager 客户端根据管理用户所定义的计划来执行硬件清单进程，所以在数据报表中可能出现延迟，此延迟会影响资产智能报表的准确性。 例如，已列出清单的受许可软件标题可能会在客户端完成成功的硬件清单周期之后卸载。 但是，该软件标题会在资产智能报表中显示为已安装，直到客户端的下一个计划硬件清单报表周期。  

 **软件封装依赖关系**  
 因为资产智能报表基于使用标准 Configuration Manager 客户端硬件清单进程收集的已安装软件标题数据，所以可能未正确收集某些软件标题数据。 例如，不符合标准安装流程的软件安装或者在安装之前更改的软件安装可能导致资产智能报表不准确。  

####  <a name="BKMK_LegalLimitations"></a> 法律限制  
 资产智能报表中显示的信息受诸多限制影响，其中显示的信息不表示法律、会计或其他专业建议。 资产智能报表提供的信息仅供参考，并且不应用作确定软件许可证使用情况符合性的唯一信息来源。  

 以下举例说明了在使用资产智能的企业中，对可能影响资产智能报表准确性的已安装软件和许可证使用情况列出清单所涉及的限制：  

 **Microsoft 许可证使用情况数量限制**  
 -   购买的 Microsoft 软件许可证的数量基于管理员提供的信息，并且应进行严密评审以确保提供正确的软件许可证数量。  

-   报告的 Microsoft 软件许可证数量仅包含有关通过批量许可计划获取的 Microsoft 软件许可证的信息，不反映通过零售、OEM 或其他软件许可证销售渠道获取的软件许可证的信息。  

-   由于软件经销商报表要求和计划，最近 45 天内获取的软件许可证可能未包括在所报告的 Microsoft 软件许可证数量中。  

-   由于公司合并或收购而导致的软件许可证转让不会反映在 Microsoft 软件许可证数量中。  

-   Microsoft 批量许可 (MVLS) 协议中的非标准条款和条件可能会影响所报告的软件许可证数量，因此，可能需要 Microsoft 代表进行附加评审。  

 **安装的软件标题数量限制**  
 Configuration Manager 客户端必须成功完成资产智能报表的硬件清单报表周期才能准确报告已安装软件标题的数量。 另外，如果在成功硬件清单报表周期之后安装或卸载已许可的软件标题，则可能存在延迟，因此在客户端报告它的下一个计划的硬件清单之前，该软件标题将不会反映在运行的资产智能报表中。  

 **许可证对帐限制**  
 通过将由管理员指定的许可证数量与根据管理员所设置的计划从 Configuration Manager 客户端硬件清单收集的已安装软件标题数量进行比较，来计算安装的软件标题数量与购买的软件许可证数量的对帐。 此比较并不表示许可证位置的最终 Microsoft 结论。 实际的许可证位置取决于特定软件标题许可证以及许可条款所授予的使用权限。  

##  <a name="BKMK_ValidationStates"></a> 资产智能验证状态  
 资产智能验证状态表示资产智能目录信息的源验证状态和当前验证状态。 下表显示可能的资产智能验证状态以及可能导致这些状态的管理员操作。  

|**状态**|**定义**|**管理员操作**|**注释**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Validated**|System Center Online 研究人员定义了目录项目。|无。|最佳状态。|  
|**User Defined**|System Center Online 研究人员尚未定义目录项目。|自定义了本地目录信息。|此状态显示在资产智能报表中。|  
|**挂起**|System Center Online 研究人员尚未定义目录项目，但是该项目已提交给 System Center Online 进行分类。|从 System Center Online 请求进行分类。|在 System Center Online 研究人员对项目进行分类和资产智能目录同步之前，目录项目一直保持此状态。|  
|**可更新**|在后续目录同步期间，System Center Online 以不同的方式对用户定义的目录项目进行分类。|自定义了本地资产智能目录，以将项目归类为用户定义。|可以使用“解决冲突”操作来决定是使用新分类信息还是以前的用户定义值。 有关如何解决冲突的详细信息，请参阅 [System Center Configuration Manager 中的资产智能操作](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)。|  
|**未分类**|System Center Online 研究人员尚未定义目录项目，项目尚未提交给 System Center Online 进行分类，并且管理员尚未分配用户定义的分类值。|无。|请求分类或自定义本地目录信息。<br /><br /> 有关请求分类的详细信息，请参阅 [System Center Configuration Manager 中的资产智能操作](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)。<br /><br /> 有关如何更改软件标题类别的详细信息，请参阅 [System Center Configuration Manager 中的资产智能操作](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md)。|  

> [!NOTE]  
>  提交给 System Center Online 进行分类的目录项目在管理中心站点上具有验证状态“挂起”  ，但在子主站点上会继续显示为具有验证状态“未分类”  。  

> [!NOTE]  
>  在分类冲突解决后，项目不会再次验证为存在冲突，除非以后的分类更新引入了有关项目的新信息。  

 有关验证状态何时可能会从一个状态转换到另一个状态的示例，请参阅 [System Center Configuration Manager 中的资产智能验证状态转换示例](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md)。  
