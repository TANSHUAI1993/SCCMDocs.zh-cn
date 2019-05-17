---
title: 站点系统角色选项
titleSuffix: Configuration Manager
description: 可参阅本文以详细了解那些不一定易于理解的 Configuration Manager 站点系统角色。
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a5fb9a553efa634dad314da58298611cdf0bbb58
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498984"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Configuration Manager 中的站点系统角色的配置选项

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 站点系统角色的大多数配置选项都不言自明，或在对其进行配置时于向导或对框中予以了解释。 以下部分介绍站点系统角色，这些角色具有可能需要额外信息的设置。  



##  <a name="BKMK_ApplicationCatalog_Website"></a>应用程序目录网站点  

> [!Note]  
> 从版本 1806 开始，不再需要应用程序目录网站点，但仍受支持。 有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。  
> 
> 应用程序目录网站点的 Silverlight 用户体验不再受支持。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  

 有关如何设置应用程序目录网站点的详细信息，请参阅[规划和配置应用程序管理](/sccm/apps/plan-design/plan-for-and-configure-application-management)。  

 #### <a name="client-connections"></a>客户端连接
 选择“HTTPS”以使用更安全的连接设置，并确定客户端是否从 Internet 进行连接。 此选项需要服务器上的 PKI 证书以向客户端进行服务器身份验证，或用于通过安全套接字层 (SSL) 对数据进行加密。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

 有关服务器证书部署的示例以及有关如何在 Internet Information Services (IIS) 中配置该证书的信息，请参阅[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)。  

 #### <a name="add-application-catalog-website-to-trusted-sites-zone"></a>将应用程序目录网站添加到受信任的站点区域  
 无论当前将“将应用程序目录网站添加到 Internet Explorer 受信任的站点区域”客户端设置设置为“True”，还是“False”，此消息都显示默认客户端设置中的值。 如果使用自定义客户端设置配置此设置，则启用此设置。  

 如果针对完全限定的域名 (FQDN) 设置此站点系统，并且网站不在 Internet Explorer 的受信任的站点区域中，则在用户连接到应用程序目录时会提示用户输入凭据。  

 #### <a name="organization-name"></a>组织名称  

 输入用户在应用程序目录中看到的名称。 此品牌信息有助于用户将此网站识别为受信任的源。  



##  <a name="BKMK_ApplicationCatalog_WebService"></a>应用程序目录 Web 服务点  

> [!Note]  
> 从版本 1806 开始，不再需要应用程序目录 Web 服务点，但仍受支持。 有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。  

 有关如何设置应用程序目录 Web 服务点的详细信息，请参阅[规划和配置应用程序管理](/sccm/apps/plan-design/plan-for-and-configure-application-management)。  

 #### <a name="https"></a>HTTPS

 选择“HTTPS”  以向此应用程序目录 Web 服务点验证应用程序目录网站点。 此选项需要运行应用程序目录网站点的服务器上的 PKI 证书来进行服务器身份验证和通过 SSL 对数据进行加密。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

 有关服务器证书部署的示例以及有关如何在 Internet Information Services (IIS) 中配置该证书的信息，请参阅[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)。  



##  <a name="BKMK_CertificateRegistrationPoint"></a>证书注册点  

 有关如何设置证书注册点的更多详细信息，请参阅[证书配置文件简介](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。  



##  <a name="BKMK_Distribution_Point"></a>分发点  

 若要深入了解如何为内容部署设置分发点，请参阅[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。  

 若要深入了解如何为 PXE 部署设置分发点，请参阅[使用 PXE 通过网络部署 Windows](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)。  

 若要深入了解如何为多播部署设置分发点，请参阅[使用多播通过网络部署 Windows](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)。  

 #### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>在 Configuration Manager 要求的情况下安装和配置 IIS
 选择此选项以让 Configuration Manager 在站点系统上安装和设置 IIS（如果尚未安装）。 必须在所有分发点上安装 IIS，并且你必须选择此设置才能在向导中继续。  

 #### <a name="site-system-installation-account"></a>站点系统安装帐户
 对于站点服务器上安装的分发点，只支持使用站点服务器的计算机帐户作为站点系统安装帐户。 有关详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account)。  

 #### <a name="create-a-self-signed-certificate-or-import-a-pki-client-certificate"></a>创建自签名证书或导入 PKI 客户端证书
 此证书有两个用途：  

1.  在分发点发送状态消息之前，该证书向管理点验证分发点。  

2.  如果选择了“为客户端启用 PXE 支持”，则将证书发送到计算机以启动 PXE。 它们使用此证书在 OS 部署过程中连接到管理点。  

如果针对 HTTP 设置了站点中的所有管理点，请创建自签名证书。 如果针对 HTTPS 设置了管理点，请导入 PKI 客户端证书。  

要导入证书，请浏览到包含 PKI 证书的公钥加密标准 #12 (PKCS #12) 文件，对于 Configuration Manager 有以下要求：  

-   计划的使用必须包括客户端身份验证。  

-   必须设置为可导出私钥。  

对证书“使用者”名称或“使用者可选名称 (SAN)”没有特定要求。 可以将同一个证书用于多个分发点。  

有关证书要求的详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。 

有关此证书的部署示例，请参阅[为分发点部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012)。  

#### <a name="enable-this-distribution-point-for-prestaged-content"></a>为预留的内容启用此分发点
选中此复选框以便为预留内容启用分发点。 如果启用此选项，可在分发内容时设置分发行为。 可选择是始终在分发点上预留内容、为包预留初始内容但在内容有更新时使用正常内容分发过程，还是为包中的内容始终使用正常内容分发过程。 有关详细信息，请参阅[预留内容](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent)。  

#### <a name="boundary-groups"></a>边界组
 你可以将边界组关联到分发点。 在内容部署过程中，客户端必须位于与分发点关联的边界组中，才能将其用作内容的源位置。 设置边界组之间的关系，以检查客户端何时可以开始搜索有效内容源位置的其他边界组。 有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/boundary-groups)。



##  <a name="BKMK_Enrollment_Point"></a>注册点  

注册点用于安装 macOS 计算机，并用于注册通过本地移动设备管理来进行管理的设备。 有关详细信息，请参阅下列文章：  

-   [如何将客户端部署到 Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  

-   [用户如何向本地 MDM 注册设备](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

#### <a name="allowed-connections"></a>允许的连接
 HTTPS 设置是自动选择的，并且需要服务器上的 PKI 证书以向注册代理点和带外服务点进行服务器身份验证，以及通过 SSL 对数据进行加密。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

 有关服务器证书部署的示例以及有关如何在 IIS 中配置该证书的信息，请参阅[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)。  



##  <a name="BKMK_Enrollment_Proxy_Point"></a>注册代理点  

若要深入了解如何为移动设备设置注册代理点，请参阅[用户如何向本地 MDM 注册设备](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)。  

#### <a name="client-connections"></a>客户端连接
 HTTPS 设置是自动选择的。 它需要在服务器上使用以下 PKI 证书： 
- 用于向注册了 Configuration Manager 的移动设备和 Mac 计算机进行服务器身份验证 
- 通过安全套接字层 (SSL) 对数据进行加密

有关证书要求的详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

 有关服务器证书部署的示例以及有关如何在 IIS 中配置该证书的信息，请参阅[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)。  



##  <a name="BKMK_Fallback_Status_Point"></a>回退状态点  

#### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>“状态消息数量”和“限制间隔(秒)”
这些选项的默认设置为 10,000 条状况消息和 3,600 秒的限制间隔。 虽然这些设置对于大多数情况已经足够，但你可能需要在以下条件都成立时更改它们：  

-   回退状态点仅接受来自 Intranet 的连接。  

-   在多台计算机的客户端部署转出过程中，你使用回退状态点。  

在这种情况下，持续的状态消息流可能会造成状态消息积压，从而导致站点服务器上的处理器高使用率持续很长一段时间。 此外，你可能无法在 Configuration Manager 控制台和客户端部署报表中看到有关客户端部署的最新信息。  

这些回退状态点设置针对在客户端部署过程中生成的状态消息进行设置。 这些设置不针对客户端通信问题（例如 Internet 上的客户端无法连接到其基于 Internet 的管理点）进行设置。 由于回退状态点无法将这些设置仅应用于在客户端部署过程中生成的状态消息，因此，如果回退状态点接受来自 Internet 的连接，请不要配置这些设置。  

成功安装 Configuration Manager 客户端的每台计算机都会向回退状态点发送下列四条状态消息：  

-   客户端部署已启动  

-   客户端部署成功  

-   客户端分配已启动  

-   客户端分配成功  

无法安装的计算机或无法分配 Configuration Manager 客户端的计算机还会发送额外状态消息。  

例如，如果将 Configuration Manager 客户端部署到 20,000 台计算机，则部署可能会向回退状态点发送 80,000 条状态消息。 由于默认限制配置允许每 3,600 秒（1 小时）向回退状态点发送 10,000 条状况消息，状况消息可能在回退状态点囤积。 还要考虑回退状态点和站点服务器之间的可用网络带宽，以及站点服务器处理多条状态消息的处理能力。  

为了帮助避免这些问题，请考虑增加状态消息数并缩短限制间隔。  

如果下列任一条件成立，请重置回退状态点的限制值：  

-   你计算出当前限制值高于处理来自回退状态点的状态消息所需的值。  

-   你发现，当前限制设置会在站点服务器上造成处理器高使用率。  

除非你了解后果，否则请不要更改回退状态点限制设置的设置。 例如，如果将限制设置提高到很高，则站点服务器上的处理器使用率可能会提高到很高，从而减慢所有站点操作的速度。  
