---
title: "规划 SMS 提供程序 | Microsoft Docs"
description: "了解 SMS 提供程序如何帮助你管理 System Center Configuration Manager。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 547dc39d5659c7c2e6f1ca670caddc127dbf22c4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>为 System Center Configuration Manager 规划 SMS 提供程序

*适用范围：System Center Configuration Manager (Current Branch)*

若要管理 System Center Configuration Manager，可使用连接到 **SMS 提供程序**的实例的 Configuration Manager 控制台。 默认情况下，当安装管理中心站点或主站点时，SMS 提供程序会安装在站点服务器上。 


##  <a name="BKMK_PlanSMSProv"></a> 关于 SMS 提供程序  
 SMS 提供程序是 Windows Management Instrumentation (WMI) 提供程序，它分配对站点中 Configuration Manager 数据库的“读取”和“写入”访问权限：  

-   每个管理中心站点和主站点上都必须至少具有一个 SMS 提供程序。 你可以根据需要安装其他提供程序。  
-   “SMS 管理员”安全组提供对 SMS 提供程序的访问权限。 Configuration Manager 在站点服务器和安装了 SMS 提供程序实例的每台计算机上自动创建此组。  

-   辅助站点不支持 SMS 提供程序。  


Configuration Manager 管理用户使用 SMS 提供程序访问存储在数据库中的信息。 若要执行此操作，管理员可使用 Configuration Manager 控制台、资源浏览器、工具和自定义脚本。 SMS 提供程序不与 Configuration Manager 客户端交互。 当 Configuration Manager 控制台连接至站点时，Configuration Manager 控制台会查询站点服务器上的 WMI 以查找要使用的 SMS 提供程序的实例。  

 SMS 提供程序帮助强制实施 Configuration Manager 安全性。 它仅返回正在运行 Configuration Manager 控制台的管理用户有权查看的信息。  

> [!IMPORTANT]  
>  当承载站点的 SMS 提供程序的每台计算机都脱机时，Configuration Manager 控制台无法连接到该站点的数据库。  

 若要了解如何管理 SMS 提供程序，请参阅 [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) 中的 [Manage the SMS Provider](../../../core/servers/manage/modify-your-infrastructure.md)。  

## <a name="prerequisites-to-install-the-sms-provider"></a>要安装 SMS 提供程序的先决条件  

 支持 SMS 提供程序：  

-   计算机必须在具有站点服务器和站点数据库站点系统双向信任关系的域中。  

-   计算机不能具有不同站点中的站点系统角色。  

-   计算机不能具有任何站点中的 SMS 提供程序。  

-   计算机必须运行站点服务器支持的操作系统。  

-   计算机至少必须有 650 MB 的可用磁盘空间，以支持与 SMS 提供程序一起安装的 Windows 自动部署工具包 (Windows ADK) 组件。 有关 Windows ADK 和 SMS 提供程序的详细信息，请参阅本主题中的 [针对 SMS 提供程序的操作系统部署要求](#BKMK_WAIKforSMSProv) 。  

##  <a name="bkmk_location"></a> SMS 提供程序位置  
 安装站点时，会为站点自动安装第一个 SMS 提供程序。 你可以为 SMS 提供程序指定以下任何支持的位置：  

-   站点服务器计算机  

-   站点数据库计算机  

-   未承载 SMS 提供程序的服务器类计算机，或者不同站点中的站点系统角色  


要查看站点中安装的每个 SMS 提供程序的位置，请选择站点“属性”对话框的“常规”选项卡。  

 每个 SMS 提供程序支持多个请求中的同时连接。 对这些连接的仅有的限制是 SMS 提供程序计算机上可用的服务器连接数目，以及满足连接请求的 SMS 提供程序计算机上可用资源。  

 安装站点后，你可以在站点服务器上重新运行安装程序，以更改现有 SMS 提供程序的位置，或者在该站点上安装其他 SMS 提供程序。 你只能在计算机上安装一个 SMS 提供程序，并且计算机无法从多个站点中安装 SMS 提供程序。  

 使用以下信息确定在每个支持的位置上安装 SMS 提供程序的优缺点：  

 **Configuration Manager 站点服务器**  

-   **优点：**  

    -   SMS 提供程序不使用站点数据库计算机的系统资源。  

    -   与位于除站点服务器或站点数据库计算机之外的其他计算机上的 SMS 提供程序相比，此位置提供的性能更佳。  

-   **缺点：**  

    -   SMS 提供程序使用可以专门用于站点服务器操作的系统和网络资源。  


**承载站点数据库的 SQL Server**  

-   **优点：**  

    -   SMS 提供程序不使用站点服务器上的站点系统资源。  

    -   如果有足够的服务器资源可用，则在这三个位置当中，此位置可以提供最佳性能。  

-   **缺点：**  

    -   SMS 提供程序使用可以专门用于站点数据库操作的系统和网络资源。  

    -   当站点数据库托管于 SQL Server 的群集实例上时，不能使用此位置。  


**站点服务器或站点数据库计算机之外的计算机**  

-   **优点：**  

    -   SMS 提供程序不使用站点服务器或站点数据库计算机资源。  

    -   此类型的位置允许你部署其他 SMS 提供程序，以为连接提供高可用性。  

-   **缺点：**  

    -   由于与站点服务器和站点数据库计算机协调需要额外的网络活动，因此 SMS 提供程序的性能可能会降低。  

    -   此服务器必须始终可供站点数据库计算机以及安装了 Configuration Manager 控制台的所有计算机访问。  

    -   此位置可以使用以其他方式专供其他服务使用的系统资源。  

##  <a name="BKMK_SMSProvLanguages"></a> 关于 SMS 提供程序语言  
 SMS 提供程序的操作与安装它的计算机的显示语言无关。  

 当管理用户或 Configuration Manager 使用 SMS 提供程序处理请求数据时，SMS 提供程序尝试返回格式与请求计算机的操作系统语言匹配的数据。

它尝试匹配语言的方式颇为间接。 SMS 提供程序未将信息从一种语言翻译成另一种语言。 相反，在 Configuration Manager 控制台中返回要显示的数据时，数据的显示语言取决于对象的源和存储类型。  

 当对象的数据存储在数据库中时，将能够使用的语言取决于下列各项：  

-   系统使用多语言支持将 Configuration Manager 创建的对象存储在数据库中。 系统使用运行安装程序时创建对象所在的站点中配置的语言存储对象。 如果请求计算机的显示语言可用于对象，则在 Configuration Manager 控制台中以该语言显示这些对象。 如果无法用请求计算机的显示语言来显示对象，则以默认语言（英文）显示该对象。  

-   系统使用用于创建对象的语言在数据库中存储管理用户创建的对象。 这些对象以此相同的语言在 Configuration Manager 控制台中显示。 它们无法被 SMS 提供程序转换，并且没有多语言选项。  

##  <a name="BKMK_MultiSMSProv"></a> 使用多个 SMS 提供程序  
 站点完成安装后，你可以为站点安装其他 SMS 提供程序。 要安装其他 SMS 提供程序，请在站点服务器上运行 Configuration Manager 安装程序。 如果满足以下任一条件，请考虑安装其他 SMS 提供程序：  

-   将会有许多管理用户在运行 Configuration Manager 控制台的同时连接到站点。  

-   你将使用可能引入 SMS 提供程序频繁调用的 Configuration Manager SDK 或其他产品。  

-   你想要确保 SMS 提供程序的高可用性。  


在站点上安装多个 SMS 提供程序并且进行连接请求时，站点随机分配每个新连接请求以使用安装的 SMS 提供程序。 你无法指定要用于特定连接会话的 SMS 提供程序位置。  

> [!NOTE]  
>  请考虑每个 SMS 提供程序位置的优缺点。 由于你无法控制哪个 SMS 提供程序用于每个新连接，请在这些因素中做出权衡。  

例如，首次将 Configuration Manager 控制台连接至站点时，连接会查询站点服务器上的 WMI 以查找控制台将使用的 SMS 提供程序的实例。 在 Configuration Manager 控制台会话结束之前，Configuration Manager 控制台仍使用 SMS 提供程序的此特定实例。 如果会话由于 SMS 提供程序计算机在网络上变得不可用而终止，那么在重新连接 Configuration Manager 控制台时，站点会重复识别要连接到的 SMS 提供程序的实例的任务。 可以分配给不可用的同一 SMS 提供程序计算机。 如果出现这种情况，则在分配可用的 SMS 提供程序计算机之前，可以尝试重新连接 Configuration Manager 控制台。  

##  <a name="BKMK_AboutSMSAdmins"></a> 关于 SMS 管理员组  
 你可以使用“SMS 管理员”组为管理用户提供 SMS 提供程序访问权限。 安装站点时会在站点服务器上自动创建此组，并且会在安装 SMS 提供程序的每台计算机上自动创建此组。 以下是关于“SMS 管理员”组的其他信息：  

-   当计算机为成员服务器时，会作为本地组来创建 SMS 管理员组。  

-   当计算机为域控制器时，会作为域本地组来创建 SMS 管理员组。  

-   从计算机中卸载 SMS 提供程序时，不会从计算机中删除 SMS 管理员组。  


在用户成功连接到 SMS 提供程序之前，其用户帐户必须是“SMS 管理员”组的成员。 在 Configuration Manager 控制台中配置的每个管理用户都会自动添加到每个站点服务器上的“SMS 管理员”组中，以及层次结构内的每个 SMS 提供程序计算机中。 从 Configuration Manager 控制台中删除管理用户时，会从每个站点服务器上的“SMS 管理员”组中以及层次结构中的每个 SMS 提供程序计算机上删除该用户。  

当用户成功连接到 SMS 提供程序之后，基于角色的管理会确定用户可以访问或管理的 Configuration Manager 资源。  

你可以使用 WMI 控件 MMC 管理单元来查看和配置 SMS 管理员组权限。 默认情况下，“Everyone”  具有“执行方法” 、“提供程序写入” 和“启用帐户”  权限。 当用户连接到 SMS 提供程序之后，会根据 Configuration Manager 控制台中定义的基于角色的管理安全权限向用户授予对站点数据库中的数据的访问权限。 SMS 管理员组被明确授予对 **Root\SMS** 命名空间的“启用帐户”和“远程启用”权限。  

> [!NOTE]  
>  使用远程 Configuration Manager 控制台的每个管理用户需要站点服务器计算机和 SMS 提供程序计算机上的“远程激活”DCOM 权限。 虽然可以将这些权限授予任何用户或组，但建议将这些权限授予“SMS 管理员”组以简化管理。 有关详细信息，请参阅 [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) 主题中的 [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) 部分。  


##  <a name="BKMK_SMSProvNamespace"></a> 关于 SMS 提供程序命名空间  
SMS 提供程序的结构由 WMI 架构来定义。 架构命名空间描述 SMS 提供程序架构内 Configuration Manager 数据的位置。 下表包含 SMS 提供程序使用的一些常见命名空间。  

|Namespace|描述|  
|---------------|-----------------|  
|Root\SMS\site_*&lt;site code\>*|Configuration Manager 控制台、资源浏览器、Configuration Manager 工具和脚本广泛使用的 SMS 提供程序。|  
|Root\SMS\SMS_ProviderLocation|站点的 SMS 提供程序计算机的位置。|  
|Root\CIMv2|清点硬件和软件期间针对 WMI 命名空间信息清点的位置。|  
|Root\CCM|Configuration Manager 客户端配置策略和客户端数据。|  
|root\CIMv2\SMS|清单客户端代理收集的清单报告类别的位置。 这些设置由客户端在计算机策略评估期间编译，而且基于计算机的客户端设置的配置。|  

##  <a name="BKMK_WAIKforSMSProv"></a> 针对 SMS 提供程序的操作系统部署要求  
安装 SMS 提供程序实例的计算机必须具备使用的 Configuration Manager 版本所需的 Windows ADK 版本。  

 -   例如，1511 版本的 Configuration Manager 需要 Windows ADK 的 Windows 10 RTM (10.0.10240) 版本。  

 -   有关此要求的详细信息，请参阅[操作系统部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

在管理操作系统部署时，Windows ADK 允许 SMS 提供程序完成不同的任务，比如：  

-   查看 WIM 文件详细信息。  

-   将驱动程序文件添加到现有的启动映像中。  

-   创建启动 .ISO 文件。  


在安装 SMS 提供程序的每台计算机上，安装 Windows ADK 可能需要最多 650 MB 的可用磁盘空间。 Configuration Manager 需要如此高的磁盘空间来安装 Windows PE 启动映像。  
