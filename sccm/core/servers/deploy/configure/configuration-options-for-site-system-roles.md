---
title: "站点系统角色选项 | Microsoft Docs"
description: "可参阅本文以详细了解那些不一定易于理解的 Configuration Manager 站点系统角色。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b4db5d86cc0ed020ed176feb2e8f1f9dc51a2280
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>System Center Configuration Manager 站点系统角色的配置选项

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 站点系统角色的大多数配置选项都不言自明，或在对其进行配置时于向导或对框中予以了解释。 以下部分介绍站点系统角色，这些角色具有可能需要额外信息的设置。  

##  <a name="BKMK_ApplicationCatalog_Website"></a>应用程序目录网站点  
 有关如何为应用程序目录设置应用程序目录网站点的信息，请参阅[规划和配置 System Center Configuration Manager 中的应用程序管理](../../../../apps/plan-design/plan-for-and-configure-application-management.md)。  

 **客户端连接**  

 选择“HTTPS”以使用更安全的连接设置，并确定客户端是否从 Internet 进行连接。 此选项需要服务器上的 PKI 证书以向客户端进行服务器身份验证，或用于通过安全套接字层 (SSL) 对数据进行加密。 有关证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 有关服务器证书部署的示例以及有关如何在 Internet Information Services (IIS) 中配置该证书的信息，请参阅 *System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构*主题中的[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)部分。  

 **将应用程序目录网站添加到受信任的站点区域**  

 无论当前将“将应用程序目录网站添加到 Internet Explorer 受信任的站点区域”客户端设置设置为“True”，还是“False”，此消息都显示默认客户端设置中的值。 如果使用自定义客户端设置配置此设置，必须自行检查此值。  

 如果针对完全限定的域名 (FQDN) 设置此站点系统，并且网站不在 Internet Explorer 的受信任的站点区域中，则在用户连接到应用程序目录时会提示用户输入凭据。  

 **组织名称**  

 输入用户在应用程序目录中看到的名称。 此品牌信息有助于用户将此网站识别为受信任的源。  

##  <a name="BKMK_ApplicationCatalog_WebService"></a>应用程序目录 Web 服务点  
 有关如何为应用程序目录设置应用程序目录 Web 服务点的信息，请参阅[规划和配置 System Center Configuration Manager 中的应用程序管理](../../../../apps/plan-design/plan-for-and-configure-application-management.md)。  

 **HTTPS**  

 选择“HTTPS”  以向此应用程序目录 Web 服务点验证应用程序目录网站点。  此选项需要运行应用程序目录网站点的服务器上的 PKI 证书来进行服务器身份验证和通过 SSL 对数据进行加密。 有关证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 有关服务器证书部署的示例以及有关如何在 IIS 中配置该证书的信息，请参阅 *System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构*主题中的[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)部分。  

##  <a name="BKMK_CertificateRegistrationPoint"></a>证书注册点  
 有关如何设置证书注册点的详细信息，请参阅[证书配置文件简介](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。  

##  <a name="BKMK_Distribution_Point"></a>分发点  
 若要深入了解如何为内容部署设置分发点，请参阅[为 System Center Configuration Manager 管理内容和内容基础结构](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

 若要深入了解如何为 PXE 部署设置分发点，请参阅[使用 PXE 与 System Center Configuration Manager 一起通过网络部署 Windows](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

 若要深入了解如何为多播部署设置分发点，请参阅[使用多播与 System Center Configuration Manager 一起通过网络部署 Windows](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

 **在 Configuration Manager 要求的情况下安装和配置 IIS**  
 选择此选项以让 Configuration Manager 在站点系统上安装和设置 IIS（如果尚未安装）。 必须在所有分发点上安装 IIS，并且你必须选择此设置才能在向导中继续。  

 **站点系统安装帐户**  
 对于站点服务器上安装的分发点，只支持使用站点服务器的计算机帐户作为站点系统安装帐户。  

 **创建自签名证书或导入 PKI 客户端证书**  
 此证书有两个用途：  

1.  在分发点发送状态消息之前，该证书向管理点验证分发点。  

2.  如果选择了“为客户端启用 PXE 支持”，则会将证书发送到执行 PXE 启动的计算机，以便这些计算机能够在操作系统部署过程中连接到管理点。  

如果针对 HTTP 设置了站点中的所有管理点，请创建自签名证书。 如果针对 HTTPS 设置了管理点，请导入 PKI 客户端证书。  

要导入证书，请浏览到包含 PKI 证书的公钥加密标准 #12 (PKCS #12) 文件，对于 Configuration Manager 有以下要求：  

-   计划的使用必须包括客户端身份验证。  

-   必须设置为可导出私钥。  

没有针对证书使用者名称或使用者备用名称 (SAN) 的特定要求，并且你可以为多个分发点使用同一证书。  

有关证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。 有关此证书的示例部署，请参阅 [System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)主题中的*为分发点部署客户端证书*部分。  

**为预安排内容启用此分发点**  
选中此复选框以便为预留内容启用分发点。 如果选中此复选框，可在分发内容时设置分发行为。 可选择是始终在分发点上预留内容、为包预留初始内容但在内容有更新时使用正常内容分发过程，还是为包中的内容始终使用正常内容分发过程。  

**边界组**  
 你可以将边界组关联到分发点。 在内容部署过程中，客户端必须位于与分发点关联的边界组中，才能将其用作内容的源位置。
 - 版本 1610 之前，可选中“允许内容源位置回退”复选框，以便在没有其他分发点可用时让这些边界组外部的客户端回退并使用分发点作为内容的源位置。
 - **从 1610 版起**，用户不能再配置“允许内容源位置回退”。  但可以设置边界组之间的关系，以检查客户端何时可以开始搜索有效内容源位置的其他边界组。

##  <a name="BKMK_Enrollment_Point"></a>注册点  
注册点用于安装 Mac 计算机，并用于注册通过本地移动设备管理来进行管理的设备。 有关详细信息，请参阅以下内容：  

-   [如何在 System Center Configuration Manager 中将客户端部署到 Mac](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [用户如何在 System Center Configuration Manager 中向本地移动设备管理注册设备](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**允许的连接**  
 HTTPS 设置是自动选择的，并且需要服务器上的 PKI 证书以向注册代理点和带外服务点进行服务器身份验证，以及通过 SSL 对数据进行加密。 有关证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 有关服务器证书部署的示例以及有关如何在 IIS 中配置该证书的信息，请参阅 *System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构*主题中的[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)部分。  

##  <a name="BKMK_Enrollment_Proxy_Point"></a>注册代理点  
若要深入了解如何为移动设备设置注册代理点，请参阅[用户如何在 System Center Configuration Manager 中向本地移动设备管理注册设备](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)。  

**客户端连接**  
 HTTPS 设置是自动选择的，并且需要服务器上的 PKI 证书以向 Configuration Manager 注册的移动设备和 Mac 计算机进行服务器身份验证，并通过安全套接字层 (SSL) 对数据进行加密。 有关证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 有关服务器证书部署的示例以及有关如何在 IIS 中配置该证书的信息，请参阅 *System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构*主题中的[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)部分。  

##  <a name="BKMK_Fallback_Status_Point"></a>回退状态点  
“状态消息数量”和“限制间隔(秒)”  
尽管这些选项的默认设置（10,000 条状态消息和 3,600 秒的限制间隔）对于大多数情况已经足够，但在以下条件都成立时，你可能必须更改这些设置：  

-   回退状态点仅接受来自 Intranet 的连接。  

-   在多台计算机的客户端部署转出过程中，你使用回退状态点。  

在这种情况下，持续的状态消息流可能会造成状态消息积压，从而导致站点服务器上的中央处理单元 (CPU) 高使用率持续很长一段时间。 此外，你可能无法在 Configuration Manager 控制台和客户端部署报表中看到有关客户端部署的最新信息。  

这些回退状态点设置针对在客户端部署过程中生成的状态消息进行设置。 这些设置不针对客户端通信问题（例如 Internet 上的客户端无法连接到其基于 Internet 的管理点）进行设置。 由于回退状态点无法将这些设置仅应用于在客户端部署过程中生成的状态消息，因此，如果回退状态点接受来自 Internet 的连接，请不要配置这些设置。  

成功安装 System Center 2012 Configuration Manager 客户端的每台计算机都会向回退状态点发送下列四条状态消息：  

-   客户端部署已启动  

-   客户端部署成功  

-   客户端分配已启动  

-   客户端分配成功  

无法安装的计算机或无法分配 Configuration Manager 客户端的计算机还会发送额外状态消息。  

例如，如果将 Configuration Manager 客户端部署到 20,000 台计算机，则部署可能会向回退状态点发送 80,000 条状态消息。 由于默认限制配置允许每 3,600 秒（1 小时）向回退状态点发送 10,000 条状况消息，状况消息可能在回退状态点囤积。 还必须考虑回退状态点和站点服务器之间的可用网络带宽，以及站点服务器处理多条状态消息的处理能力。  

为了帮助避免这些问题，请考虑增加状态消息数并缩短限制间隔。  

如果下列任一条件成立，请重置回退状态点的限制值：  

-   你计算出当前限制值高于处理来自回退状态点的状态消息所需的值。  

-   你发现，当前限制设置会在站点服务器上造成 CPU 高使用率。  

除非你了解后果，否则请不要更改回退状态点限制设置的设置。 例如，如果将限制设置提高到很高，则站点服务器上的 CPU 使用率可能会提高到很高，从而减慢所有站点操作的速度。  
