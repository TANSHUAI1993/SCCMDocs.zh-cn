---
title: 安装云分发点
titleSuffix: Configuration Manager
description: 使用以下步骤在 Configuration Manager 中设置云分发点。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a2d39617db7f2ea9a61e73a3c21cc2509fed2f07
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456611"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>为 Configuration Manager 安装云分发点

*适用范围：System Center Configuration Manager (Current Branch)*

本文详细介绍了在 Microsoft Azure 中安装 Configuration Manager 云分发点的步骤。 它包括以下部分：
- [在开始之前](#bkmk_before) 
- [设置](#bkmk_setup)
- [配置 DNS](#bkmk_dns)
- [设置站点服务器代理](#bkmk_proxy)
- [分发内容并配置客户端](#bkmk_client)
- [管理和监视](#bkmk_monitor)
- [修改](#bkmk_modify)
- [高级故障排除](#bkmk_tshoot) 



## <a name="bkmk_before"></a> 在开始之前

首先阅读[使用云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)一文。 该文章可帮助你规划和设计云分发点。 

使用以下清单确保具有创建云分发点所需的信息和先决条件：  

- 站点服务器可连接到 Azure。 如果网络使用代理，则[配置站点系统角色](#bkmk_proxy)。  

- 要使用的 Azure 环境。 例如，Azure 公有云或 Azure 美国政府云。  

- 从版本 1806 开始（建议使用），请使用 Azure 资源管理器部署。 有以下要求：<!--1322209-->  

    - 与 [Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard) 集成以实现云管理。 不需要 Azure AD 用户发现。  

    - Azure 订阅 ID。  

    - Azure 资源组。  

    - 订阅管理帐户需要在向导期间登录。  

- 如果计划使用 Azure 经典服务部署，则需满足以下要求：  
    > [!Important]  
    > 从版本 1810 开始，Configuration Manager 已弃用 Azure 的经典服务部署。 开始使用适用于云管理网关的 Azure 资源管理器部署。 有关详细信息，请参阅 [CMG 规划](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)。  

    - Azure 订阅 ID。  

    - Azure 管理证书，同时导出为 .CER 和 .PFX 文件。 Azure 订阅管理员需要将 .CER 管理证书添加到 [Azure 门户](https://portal.azure.com)中的订阅。  

- 导出为 .PFX 文件的服务器身份验证证书。  

- 云分发点的全局唯一服务名称。  

    > [!TIP]  
    > 在请求使用此服务名称的服务器身份验证证书之前，请确认所需的 Azure 域名是唯一的。 例如，WallaceFalls.CloudApp.Net。 登录 [Microsoft Azure 门户](https://portal.azure.com)。 依次选择“创建资源”、“计算”类别，以及“云服务”。 在“DNS 名称”字段中，键入所需的前缀，例如 WallaceFalls。 界面将反映域名是否可用，或是否已被其他服务使用。 不要在门户中创建服务，仅使用此流程检查名称可用性。  
 
- 此部署所在的 Azure 区域。  



##  <a name="bkmk_setup"></a>设置   

在站点上执行此过程以托管由[设计](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_topology)确定的云分发点。  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“云分发点”。 在功能区中，选择“创建云分发点”。  

2.  在创建云分发点向导的“常规”页上，配置以下设置：  

    1. 首先指定 Azure 环境。  

    2. 从版本 1806 开始（建议使用），请选择 Azure 资源管理器部署作为部署方法。 选择“登录”以使用 Azure 订阅管理员帐户进行身份验证。 向导使用 Azure AD 集成先决条件过程中存储的 信息，自动填充其余字段。 如果拥有多个订阅，请选择要使用的所需订阅的**订阅 ID**。  

    > [!Note]  
    > 从版本 1810 开始，Configuration Manager 已弃用 Azure 的经典服务部署。 
    > 
    > 如果需要使用经典服务部署，请在此页面上选择该选项。 首先输入 Azure 订阅 ID。 然后选择“浏览”并选择 .PFX 文件作为 Azure 管理证书。  

3.  选择“下一步”。 等待站点测试与 Azure 的连接。  

4.  在“设置”页上，指定以下设置，然后单击“下一步”：  

    - **区域**：选择要在其中创建云分发点的 Azure 区域。  

    - **资源组**（仅限 Azure 资源管理器部署方法）  

        - **使用现有项**：从下拉列表中选择现有资源组。  

        - **创建新项**：输入要在 Azure 订阅中创建的新资源组名称。  

    - **主站点**：选择要将内容分发到此分发点的主站点。

    - **证书文件**：选择“浏览”并选择 .PFX 文件作为此云分发点的服务器身份验证证书。 来自此证书的公用名称将填充“服务 FQDN”和“服务名称”必填字段。  

        > [!NOTE]  
        > 云分发点服务器身份验证证书支持通配符。 如果使用通配符证书，请将“服务 FQDN”字段中的星号 (*) 替换为服务所需的主机名。  

5. 在“警报”页上，设置存储配额、传输配额以及希望 Configuration Manager 在达到这些配额的百分之几时生成警报。 然后选择“下一步”。  

6. 完成向导。  


### <a name="monitor-installation"></a>监视安装  

该站点开始为云分发点创建新的托管服务。 关闭向导后，在 Configuration Manager 控制台中监视云分发点的安装进度。 还可监视主站点服务器上的 CloudMgr.log 文件。 如有必要，请监视 Azure 门户中的云服务预配情况。  

> [!NOTE]  
>  在 Azure 中设置新的分发点最多可能需要 30 分钟。 在预配存储帐户之前，CloudMgr.log 文件会重复以下消息：  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> 在预配存储帐户后，将创建并配置服务。  


### <a name="verify-installation"></a>验证安装

使用以下方法验证云分发点安装已完成：  

- 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“云服务”，然后选择“云分发点”节点。 在列表中查找新的云分发点。 “状态”列应为“就绪”。  

- 在 Configuration Manager 控制台中，转到“监视”工作区。 展开“系统状态”，然后选择“组件状态”节点。 显示 SMS_CLOUD_SERVICES_MANAGER 组件中的所有消息，并查找状态消息 ID 9409。  

- 如有必要，请转到 Azure 门户。 云分发点的“部署”显示“就绪”状态。  



##  <a name="bkmk_dns"></a>配置 DNS  

客户端必须能够将云分发点的名称解析为 Azure 管理的 IP 地址，然后才能使用云分发点。 管理点为它们提供云分发点的服务 FQDN。 云分发点在 Azure 中作为服务名称存在。 请在云分发点属性的“设置”选项卡上查看这些值。 

> [!Note]  
> 控制台中的“云分发点”节点包含名为“服务名称”的列，但实际上显示了“服务 FQDN”值。 要查看这两个值，请打开云分发点的“属性”，然后切换到“设置”选项卡。  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

服务器身份验证证书公用名称应包含域名。 从公共提供程序购买证书时，此名称是必需的。 从 PKI 颁发此证书时，建议使用此名称。 例如，`WallaceFalls.contoso.com`。 在“创建云分发点向导”中指定此证书时，公用名称将填充“服务 FQDN”属性 (`WallaceFalls.contoso.com`)。 “服务名称”采用相同主机名 (`WallaceFalls`)，并将其附加到 Azure 域名 `cloudapp.net`。 在此方案中，客户端需要将域的服务 FQDN (`WallaceFalls.contoso.com`) 解析为 Azure 服务名称 (`WallaceFalls.cloudapp.net`)。 创建 CNAME 别名以映射这些名称。


### <a name="create-cname-alias"></a>创建 CNAME 别名

在组织的面向 Internet 的公共 DNS 中创建规范名称记录 (CNAME)。 此记录为客户端接收的云分发点的服务 FQDN 属性创建别名，别名为 Azure 服务名称。 例如，为 `WallaceFalls.contoso.com` 到 `WallaceFalls.cloudapp.net` 创建新的 CNAME 记录。  


### <a name="client-name-resolution-process"></a>客户端名称解析过程

以下过程显示客户端如何解析云分发点的名称：  

1. 客户端获取内容源列表中云分发点的服务 FQDN。 例如，`WallaceFalls.contoso.com`。  

2. 它查询 DNS，它使用 Azure 服务名称的 CNAME 别名解析服务 FQDN。 例如，`WallaceFalls.cloudapp.net`。  

3. 再次查询 DNS，将 Azure 服务名称解析为 Azure 公共 IP 地址。   

4. 客户端使用此 IP 地址开始与云分发点进行通信。   

5. 云分发点将服务器身份验证证书提供给客户端。 客户端使用证书的信任链进行验证。  



## <a name="bkmk_proxy"></a>设置站点服务器代理  

管理云分发点的主站点服务器需要与 Azure 通信。 如果组织使用代理服务器控制 Internet 访问，请将主站点服务器配置为使用此代理。   

有关详细信息，请参阅[代理服务器支持](/sccm/core/plan-design/network/proxy-server-support)。  



## <a name="bkmk_client"></a>分发内容并配置客户端

将内容分发到与任何其他本地分发点相同的云分发点。 管理点不会将云分发点包括在内容位置列表中，除非它有客户端请求的内容。 有关详细信息，请参阅[分发和管理内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content)。 

管理与任何其他本地分发点相同的云分发点。 这些操作包括将其分配给分发点组以及管理内容包。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points)。

默认客户端设置自动启用客户端以使用云分发点。 使用以下客户端设置控制对层次结构中所有云分发点的访问：  

   - 在“云设置”组中，修改设置“允许访问云分发点”。  

       - 默认情况下，此设置设为“是”。  

       - 修改并为用户和设备部署此设置。  



## <a name="bkmk_monitor"></a>管理和监视  

监视分发到云分发点的与任何其他本地分发点相同的内容。 有关详细信息，请参阅[监视内容](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed)。 

### <a name="bkmk_alerts"></a> 警报  

Configuration Manager 定期检查 Azure 服务。 如果服务未处于活动状态，或出现订阅或证书问题，Configuration Manager 会发出警报。 

配置要存储在云分发点上的数据量的阈值，以及客户端从分发点下载的数据量。 使用这些阈值的警报可帮助你决定何时停止或删除云服务，调整存储在云分发点上的内容，或修改哪些客户端可使用该服务。 

- **存储警报阈值**：存储警报阈值设置你希望存储在云分发点上的数据或内容量上限（以 GB 为单位）。 默认情况下，此阈值为 2,000 GB。 Configuration Manager 可以在剩余可用空间达到指定的水平时生成警告和关键警报。 默认情况下，达到阈值的 50% 和 90% 时出现这些警报。  

- **每月传输警报阈值**：每月传输警报阈值帮助你监视 30 天内从分发点传输到客户端的内容量。 默认情况下，此阈值为 10,000 GB。 当传输达到定义的值时，该站点会发出警告和关键警报。 默认情况下，达到阈值的 50% 和 90% 时出现这些警报。  

    > [!IMPORTANT]  
    >  Configuration Manager 监视数据传输，但在数据传输量超出指定的传输警报阈值时不会停止数据传输。  

在安装期间为每个云分发点指定阈值，或使用云分发点属性的“警报”选项卡。  

> [!NOTE]  
>  云分发点的警报视 Azure 提供的使用量统计信息而定，且可能需要最多 24 小时才能变得可用。 有关 Azure 存储分析的详细信息，请参阅[存储分析](https://docs.microsoft.com/rest/api/storageservices/storage-analytics)。  

在每小时周期中，监视云分发点的主站点从 Azure 下载事务数据。 它将此事务数据存储在站点服务器上的 `CloudDP-<ServiceName>.log` 文件中。 Configuration Manager 会依据每个云分发点的存储和传输配额评估此信息。 在数据传输量达到或超过为警告性警报或关键警报指定的数量时，Configuration Manager 会生成相应的警报。  

> [!WARNING]  
>  因为该站点每小时从 Azure 下载有关数据传输的信息，因此，在 Configuration Manager 可以访问此数据并发出警报之前，使用量可能已超过警告阈值或关键阈值。  



## <a name="bkmk_modify"></a>修改

还可以在 Configuration Manager 控制台的“管理”工作区中的“云服务”下的“云分发点”节点中，查看有关分发点的高级信息。 选择分发点，然后选择“属性”以查看更多详细信息。  

编辑云分发点的属性时，以下选项卡包括要编辑的设置：  

#### <a name="settings"></a>设置  

- **描述**  

- **证书文件**：在服务器身份验证证书过期之前，颁发具有相同公用名称的新证书。 然后在此处添加新证书，开始使用该服务。 如果证书过期，客户端将不信任该服务且不会使用该服务。  

#### <a name="alerts"></a>警报
调整存储和每月传输警报的数据阈值。  

#### <a name="content"></a>Content
管理与本地分发点相同的内容。  


### <a name="redeploy-the-service"></a>重新部署服务

较重大的更改（例如以下配置）需要重新部署服务：
- 经典部署方法改为 Azure 资源管理器部署方法
- 订阅
- 服务名称
- 专用于公有 PKI
- Azure 区域

从版本 1806 开始，如果经典部署方法上已有现有云分发点，要使用 Azure 资源管理器部署方法，需要部署新的云分发点。 共有两个选项：

- 如果要重新使用相同的服务名称：  

    1. 首先删除经典云分发点。 如果没有其他云分发点，客户端可能无法获取内容。  

    2. 使用资源管理器部署创建新的云分发点。 重新使用相同的服务器身份验证证书。  

    3. 将必要的软件包内容分发到新的云分发点。  

- 如果要使用新的服务名称：  

    1. 使用资源管理器部署创建新的云分发点。 使用新的服务器身份验证证书。  

    2. 将必要的软件包内容分发到新的云分发点。  

    3. 删除经典云分发点。

> [!Tip]  
> 确定云分发点的当前部署模型：<!--SCCMDocs issue #611-->  
> 1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“云分发点”节点。  
> 2. 将“部署模型”属性作为列添加到列表视图中。 对于资源管理器部署，该属性为“Azure 资源管理器”。  


### <a name="stop-or-start-the-cloud-service-on-demand"></a>按需停止或启动云服务

在 Configuration Manager 控制台中随时停止云分发点。 此操作立即阻止客户端从此服务下载更多内容。 从 Configuration Manager 控制台重新启动云服务以还原客户端的访问权限。 例如，在达到数据阈值时停止云服务。  

停止云分发点时，云服务不会从存储帐户中删除内容。 它也不会阻止站点服务器将其他内容传输到云分发点。 管理点仍将云分发点作为有效内容源返回给客户端。 

使用以下过程停止云分发点：  

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“云服务”，然后选择“云分发点”节点。  

2. 选择云分发点。 要停止在 Azure 中运行的云服务，请选择功能区中的“停止服务”。  

3. 选择“启动服务”以重启云分发点。  


### <a name="delete-a-cloud-distribution-point"></a>删除云分发点

若要卸载云分发点，请在 Configuration Manager 控制台中选择该分发点，然后选择“删除”。  

从层次结构中删除云分发点时，Configuration Manager 会从 Azure 中的云服务中删除内容。 

手动删除 Azure 中的任何组件都会导致系统不一致。 此状态会留下孤立的信息，并且可能发生意外的行为。



## <a name="bkmk_tshoot"></a>高级故障排除

如果需要从 Azure VM 收集诊断日志记录以帮助解决云分发点的问题，请使用以下 PowerShell 示例为订阅启用服务诊断扩展：<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using 
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using 

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script. 
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate 
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```


以下示例是上述 PowerShell 脚本中 public_config 变量中引用的示例 diagnostics.wadcfgx 文件。 有关详细信息，请参阅 [Azure 诊断扩展配置架构](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema)。  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

