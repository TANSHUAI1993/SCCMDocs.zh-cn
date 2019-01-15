---
title: 规划 SMS 提供程序
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的 SMS 提供程序站点系统角色。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d59e5e5bc1dfdf962517b4c364b74aa0df6b650a
ms.sourcegitcommit: 94bf7d5b5beb9628cc1fdfe75451d33b5de26f8a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54152445"
---
# <a name="plan-for-the-sms-provider"></a>规划 SMS 提供程序 

适用范围：System Center Configuration Manager (Current Branch)

若要管理 Configuration Manager，可使用连接到 **SMS 提供程序**的实例的 Configuration Manager 控制台。 默认情况下，当安装管理中心站点或主站点时，SMS 提供程序会安装在站点服务器上。 



##  <a name="BKMK_PlanSMSProv"></a> 关于 SMS 提供程序  

SMS 提供程序是 Windows Management Instrumentation (WMI) 提供程序，它分配对站点中 Configuration Manager 数据库的**读取**和**写入**访问权限。  

- 每个管理中心站点和主站点上都必须至少具有一个 SMS 提供程序。 你可以根据需要安装其他提供程序。  

- “SMS 管理员”安全组提供对 SMS 提供程序的访问权限。 Configuration Manager 在站点服务器和安装了 SMS 提供程序实例的每台计算机上自动创建此组。 有关详细信息，请参阅 [SMS 管理员](/sccm/core/plan-design/hierarchy/accounts#sms-admins)。  

- 辅助站点不支持 SMS 提供程序角色。  

Configuration Manager 管理用户使用 SMS 提供程序访问存储在数据库中的信息。 若要执行此操作，管理员可使用 Configuration Manager 控制台、资源浏览器、工具和自定义脚本。 SMS 提供程序不与 Configuration Manager 客户端交互。 当 Configuration Manager 控制台连接至站点时，它会查询站点服务器上的 WMI，以查找要使用的 SMS 提供程序的实例。  

SMS 提供程序帮助强制实施 Configuration Manager 安全性。 它仅返回控制台用户有权查看的信息。  

> [!IMPORTANT]  
>  当站点的 SMS 提供程序的每个实例都处于脱机状态时，Configuration Manager 控制台无法连接到该站点。  

 有关如何管理 SMS 提供程序的详细信息，请参阅[管理 SMS 提供程序](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider)。  



## <a name="installation-prerequisites"></a>安装先决条件  

 若要支持 SMS 提供程序，目标服务器必须满足以下先决条件：  

-   位于具有站点服务器和站点数据库站点系统双向信任关系的域中  

-   不能具有不同站点中的站点系统角色  

-   不能已经拥有任何站点中的 SMS 提供程序  

-   运行受支持的 OS 版本  

-   至少有 650 MB 可用磁盘空间用于支持 Windows ADK 组件。 有关 Windows ADK 和 SMS 提供程序的详细信息，请参阅 [OS 部署要求](#BKMK_WAIKforSMSProv)。  



##  <a name="bkmk_location"></a>位置  

安装站点时，会为站点自动安装第一个 SMS 提供程序。 你可以为 SMS 提供程序指定以下任何支持的位置：  

-   站点服务器  

-   站点数据库服务器  

-   另一台服务器（满足[安装先决条件](#installation-prerequisites)）  


若要查看站点的每个 SMS 提供程序的位置，请执行以下操作： 

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。  

2. 从列表中选择所需的站点，然后选择功能区中的“属性”。  

3. 在站点“属性”的“常规”选项卡中，查看“SMS 提供程序位置”字段。    


每个 SMS 提供程序支持多个请求中的同时连接。 对这些连接仅有的限制是 Windows 可用的服务器连接数量，以及服务器上满足连接请求的可用资源。  

安装站点后，可再次在站点服务器上运行 Configuration Manager 安装程序。 使用安装程序更改现有 SMS 提供程序的位置，或者在该站点上安装其他 SMS 提供程序。 在一台计算机上仅安装一个 SMS 提供程序。 一台计算机不能托管多个站点的 SMS 提供程序。  


### <a name="choosing-a-location"></a>选择位置 

以下各部分介绍在每个支持的位置上安装 SMS 提供程序的优缺点：  

#### <a name="configuration-manager-site-server"></a>Configuration Manager 站点服务器

- **优点：**  

    -   SMS 提供程序不使用站点数据库计算机的系统资源。  

    -   与位于除站点服务器或站点数据库计算机之外的其他计算机上的 SMS 提供程序相比，此位置提供的性能更佳。  

- **缺点：**  

    -   SMS 提供程序使用可以专门用于站点服务器操作的系统和网络资源。  


#### <a name="sql-server-that-hosts-the-site-database"></a>托管站点数据库的 SQL Server

- **优点：**  

    -   SMS 提供程序不使用站点服务器上的系统资源。  

    -   如果有足够的服务器资源可用，则在这三个位置当中，此位置可以提供最佳性能。  

- **缺点：**  

    -   SMS 提供程序使用可以专门用于站点数据库操作的系统和网络资源。  

    -   当站点数据库托管于 SQL Server 的群集实例上时，不能使用此位置。  


#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>非站点服务器或站点数据库服务器的计算机

- **优点：**  

    -   SMS 提供程序不使用站点服务器或站点数据库系统资源。  

    -   此类型的位置允许你部署其他 SMS 提供程序，以为连接提供高可用性。  

- **缺点：**  

    -   SMS 提供程序的性能可能会下降。 此行为是因为与站点服务器和站点数据库计算机协调需要额外的网络活动。  

    -   此服务器必须始终可供站点数据库服务器以及安装了 Configuration Manager 控制台的所有计算机访问。  

    -   此位置可以使用以其他方式专供其他服务使用的系统资源。  



## <a name="bkmk_auth"></a>身份验证
<!--1357013-->

从版本 1810 开始，可以为管理员指定访问 Configuration Manager 站点的最低身份验证级别。 此功能强制管理员以要求的级别登录到 Windows。 它适用于访问 SMS 提供程序的所有组件。 例如，Configuration Manager 控制台、SDK 方法和 Windows PowerShell cmdlet。 


### <a name="configure-authentication"></a>配置身份验证

若要配置此设置，请首先使用预期的身份验证级别登录到 Windows。 

> [!Important]  
> 此配置是层次结构范围的设置。 更改此设置前，请确保所有 Configuration Manager 管理员都能够使用所需的身份验证级别登录到 Windows。 

若要配置此设置，请使用以下步骤：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。  

2. 选择功能区中的“层次结构设置”。  

3. 切换到“身份验证”选项卡。选择所需的[“身份验证级别”](#authentication-levels)，然后选择“确定”。  

    - 仅在必要时选择“添加”以排除特定用户或组。 有关详细信息，请参阅[排除](#exclusions)。  


### <a name="authentication-levels"></a>身份验证级别

可用的级别如下：

- **Windows 身份验证**：要求使用 Active Directory 域凭据进行身份验证。 此设置是以前的行为，也是当前的默认设置。 更新站点时，身份验证级别没有更改。  

- **证书身份验证**：要求使用由受信任的 PKI 证书颁发机构颁发的有效证书进行身份验证。 你没有在 Configuration Manager 中配置此证书。 Configuration Manager 要求管理员使用 PKI 登录到 Windows.  

- **Windows Hello 企业版身份验证**：要求使用与设备关联并采用生物识别或 PIN 的强双因素身份验证进行身份验证。 有关详细信息，请参阅 [Windows Hello 企业版](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)。   


### <a name="exclusions"></a>排除

从层次结构设置的“身份验证”选项卡中，也可以排除某些用户或组。 请谨慎使用此选项。 例如，当特定用户要求访问 Configuration Manager 控制台但无法使用要求的级别对 Windows 进行身份验证时。 对于在系统帐户的上下文下运行的自动化或服务，它可能也是必需的。



##  <a name="BKMK_SMSProvLanguages"></a> 关于 SMS 提供程序语言  

SMS 提供程序的运行与安装它的服务器的显示语言无关。  

当管理用户或 Configuration Manager 使用 SMS 提供程序处理请求数据时，它会尝试返回格式与请求计算机的 OS 语言格式匹配的数据。

它通过间接方式尝试匹配语言。 SMS 提供程序不会将信息从一种语言翻译成另一种语言。 当它返回要在 Configuration Manager 控制台中显示的数据时，数据的显示语言取决于对象的源和存储类型。  

当 Configuration Manager 在数据库中存储某个对象的数据时，可用的语言取决于以下因素：  

-   Configuration Manager 使用多语言支持存储其创建的对象。 它以运行安装程序时为站点配置的语言在站点数据库中存储对象。 如果请求计算机的显示语言可用于对象，则 Configuration Manager 控制台以该语言显示这些对象。 如果控制台无法以请求计算机的显示语言来显示对象，它会以默认语言（英语）显示该对象。  

-   Configuration Manager 使用用于创建对象的语言存储管理用户创建的对象。 这些对象以此相同的语言在 Configuration Manager 控制台中显示。 SMS 提供程序无法翻译这些对象，并且它们不具有多个语言选项。  



##  <a name="BKMK_MultiSMSProv"></a> 使用多个 SMS 提供程序  

 站点完成安装后，你可以为站点安装其他 SMS 提供程序。 若要安装其他 SMS 提供程序，请在站点服务器上运行 Configuration Manager 安装程序。 

如果满足以下任意条件，请考虑安装其他 SMS 提供程序：  

- 许多管理用户需要在使用 Configuration Manager 控制台的同时连接到站点。  

- 使用可能会带来对 SMS 提供程序的频繁调用的 Configuration Manager SDK 或其他产品。  

- 对 SMS 提供程序的高可用性存在业务要求。  

在站点上安装多个 SMS 提供程序并发出连接请求时，站点会对每个新连接请求使用的已安装 SMS 提供程序进行随机分配。 无法指定要用于特定连接会话的 SMS 提供程序。  

> [!NOTE]  
>  请考虑每个 SMS 提供程序位置的优缺点。 有关详细信息，请参阅[位置](#bkmk_location)。 由于无法控制用于每个新连接的 SMS 提供程序，请就这些注意事项进行权衡。  

首次将 Configuration Manager 控制台连接到站点时，连接会查询站点服务器上的 WMI。 此查询可确定控制台使用的 SMS 提供程序的实例。 在会话结束前，控制台会一直使用 SMS 提供程序的此特定实例。 如果会话因为 SMS 提供程序服务器在网络上不可用而结束，则将控制台重新连接到站点时，它会重复初始查询。 站点有可能分配同一不可用的 SMS 提供程序实例。 如果出现此行为，请尝试重新连接控制台，直到站点返回可用的 SMS 提供程序。  



##  <a name="BKMK_SMSProvNamespace"></a> 关于 SMS 提供程序命名空间  

Configuration Manager WMI 架构定义 SMS 提供程序的结构。 架构命名空间描述 SMS 提供程序架构内 Configuration Manager 数据的位置。 下表包含 SMS 提供程序使用的一些常见命名空间：  

|Namespace|说明|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|Configuration Manager 控制台、资源浏览器、Configuration Manager 工具和脚本广泛使用的 SMS 提供程序。|  
|`Root\SMS\SMS_ProviderLocation`|站点的 SMS 提供程序计算机的位置。|  
|`Root\CIMv2`|清点硬件和软件期间针对 WMI 命名空间信息清点的位置。|  
|`Root\CCM`|Configuration Manager 客户端配置策略和客户端数据。|  
|`Root\CIMv2\SMS`|清单客户端代理收集的清单报告类的位置。 客户端在计算机策略评估期间编译这些设置。 这些设置基于计算机的客户端设置配置。|  



##  <a name="BKMK_WAIKforSMSProv"></a>OS 部署要求

安装 SMS 提供程序实例的计算机需要 Windows ADK 的受支持版本。  

有关此要求的详细信息，请参阅 [OS 部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10)和 [Windows 10 支持](/sccm/core/plan-design/configs/support-for-windows-10)。  

在管理 OS 部署时，Windows ADK 允许 SMS 提供程序完成各种任务，例如：  

-   查看 WIM 文件详细信息  

-   将驱动程序文件添加到现有的启动映像中  

-   创建启动 ISO 文件  


在安装 SMS 提供程序的每台计算机上，安装 Windows ADK 可能需要最多 650 MB 的可用磁盘空间。 Configuration Manager 需要如此高的磁盘空间来安装 Windows PE 启动映像。  
