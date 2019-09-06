---
title: 将客户端部署到 Mac 的准备工作
titleSuffix: Configuration Manager
description: 将 Configuration Manager 客户端部署到 Mac 计算机前的配置任务。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3718661af1bae7dbf0984e29d95736b9f86104dc
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70378372"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>将客户端软件部署到 Mac 的准备工作

适用范围：  System Center Configuration Manager (Current Branch)

按照下列步骤，请确保已准备好[将 Configuration Manager 客户端部署到 Mac 计算机](/sccm/core/clients/deploy/deploy-clients-to-macs)。



## <a name="mac-prerequisites"></a>Mac 先决条件

Mac 客户端安装包未与 Configuration Manager 媒体一同提供。 可从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkID=525184)下载适用于其他操作系统的客户端  。  

有关支持的版本列表，请参阅[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#mac-computers)。



## <a name="certificate-requirements"></a>证书要求

在 Mac 计算机上安装和管理客户端需要公钥基础结构 (PKI) 证书。 PKI 证书通过使用手动身份验证和加密的数据传输来保护 Mac 计算机和 Configuration Manager 站点之间的通信的安全。 Configuration Manager 可以请求并安装用户客户端证书。 它将证书服务与企业证书颁发机构以及 Configuration Manager 注册点和注册代理点一起使用。 你还可以独立于 Configuration Manager 请求和安装计算机证书。 此证书必须满足 Configuration Manager 证书要求。  

Configuration Manager Mac 客户端始终执行证书吊销检查。 不能禁用此功能。  

如果 Mac 客户端找不到证书吊销列表 (CRL)，则无法连接到 Configuration Manager 站点系统。 特别是对于与发布证书颁发机构不同的林中的 Mac 客户端，请检查 CRL 设计。 确保 Mac 客户端可以找到并下载 CRL。  

在 Mac 计算机上安装 Configuration Manager 客户端之前，请决定安装客户端证书的方式：  

-   通过使用 [CMEnroll 工具](/sccm/core/clients/deploy/deploy-clients-to-macs#client-and-certificate-automation-with-cmenroll)注册 Configuration Manager。 注册过程不支持自动证书续订。 在证书过期之前重新注册 Mac 计算机。  

-   [使用与 Configuration Manager 无关的证书请求和安装方法](/sccm/core/clients/deploy/deploy-clients-to-macs#bkmk_external)。  

有关 Mac 客户端证书要求的详细信息，请参阅 [Configuration Manager 的 PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

会自动将 Mac 客户端分配给对其进行管理的 Configuration Manager 站点。 即使仅与 Intranet 通信，Mac 客户端也可安装为仅 Internet 的客户端。 此配置意味着它们与分配的站点中启用 Internet 的管理点和分发点进行通信。 Mac 计算机不会与为其分配的站点范围外的站点系统进行通信。  

> [!IMPORTANT]  
>  适用于 macOS 的 Configuration Manager 客户端不能用于连接到配置为使用[数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)的管理点。  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>将 Web 服务器证书部署到站点系统服务器  

如果这些站点系统不具有 Web 服务器证书，请将该证书部署到具有这些站点系统角色的计算机：  

-   管理点  

-   分发点  

-   注册点  

-   注册代理点  

Web 服务器证书必须包含在站点系统属性中指定的 Internet FQDN。 但不可通过 Internet 访问的服务器也支持 Mac 计算机。 如果不需要基于 Internet 的客户端管理，可为 Internet FQDN 指定 Intranet FQDN 值。  

可在管理点、分发点和注册代理点的 Web 服务器证书中指定站点系统的 Internet FQDN 值。

有关示例部署的详细信息，请参阅[为运行 IIS 的站点系统部署 Web 服务器证书。](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>将客户端身份验证证书部署到站点系统服务器  

如果这些站点系统没有客户端身份验证证书，请向托管以下站点系统角色的计算机部署客户端身份验证证书：  

-   管理点  

-   分发点  

有关创建和安装管理点的客户端证书的示例部署，请参阅[为 Windows 计算机部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012)。  

有关创建和安装分发点的客户端证书的示例部署，请参阅[为分发点部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012)。  

> [!IMPORTANT]  
>  要将客户端部署到运行 macOS Sierra 的设备上，必须正确配置管理点证书的使用者名称。 例如，使用管理点服务器的 FQDN。  



## <a name="prepare-the-client-certificate-template-for-macs"></a>为 Mac 准备客户端证书模板  

对于在 Mac 计算机上注册证书的用户帐户，证书模板必须具有“读取”和“注册”权限   。  

有关详细信息，请参阅[为 Mac 计算机部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_MacClient_SP1)。  



## <a name="configure-the-management-point-and-distribution-point"></a>配置管理点和分发点  

为下列选项配置管理点：  

-   HTTPS  

-   允许来自 Internet 的客户端连接。 管理 Mac 计算机需要该配置值。 但是，它并不意味着站点系统服务器必须可从 Internet 中访问。  

-   允许移动设备和 Mac 计算机使用此管理点  

安装 Mac 客户端不需要分发点。 如果要在安装客户端后将软件部署到这些计算机，请配置分发点以允许来自 Internet 的客户端连接。  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>配置管理点和分发点以支持 Mac  

在开始此过程之前，请确保使用 Internet FQDN 配置管理点和分发点。 如果这些服务器不支持基于 Internet 的客户端管理，则可将 Intranet FQDN 指定为 Internet FQDN 值。

这些站点系统角色必须位于主站点中。  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“服务器和站点系统角色”节点    。 然后选择具有正确站点系统角色的服务器。  

2.  在细节窗格中选择“管理点”角色，然后选择功能区中的“属性”   。 在“管理点属性”窗口中，配置以下选项：   

    1.  选择“HTTPS”  。  

    2.  选择“仅允许 Internet 客户端连接”或“允许 Intranet 和 Internet 客户端连接”   。 这些选项需要 Internet 或 Intranet FQDN。  

    3.  选择“允许移动设备和 Mac 计算机使用此管理点”  。  

    4. 选择“确定”以保存此配置  。  

3.  在“服务器和站点系统角色”节点的细节窗格中，选择“分发点”角色，然后在功能区中选择“属性”   。 在“分发点属性”窗口中，配置以下选项：   

    -   选择“HTTPS”  。  

    -   选择“仅允许 Internet 客户端连接”或“允许 Intranet 和 Internet 客户端连接”   。 这些选项需要 Internet 或 Intranet FQDN。  

    -   选择“导入证书”  ，浏览到导出的客户端分发点证书文件，然后指定密码。  

4.  对管理 Mac 计算机的主站点中的所有管理点和分发点重复此过程。  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>配置注册代理点和注册点  

在同一站点中安装这两个角色。 不必将它们安装在同一站点系统服务器上或安装在同一 Active Directory 林中。  

有关站点系统角色布局和注意事项的详细信息，请参阅[站点系统角色](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles#bkmk_planroles)。  

这些过程配置站点系统角色以支持 Mac 计算机：   

-   [新建站点系统服务器](/sccm/core/servers/deploy/configure/install-site-system-roles#to-install-site-system-roles-on-a-new-site-system-server)  

-   [现有站点系统服务器](/sccm/core/servers/deploy/configure/install-site-system-roles#bkmk_Install)    

在任一情况下，在“系统角色选择”页上，从可用角色列表中选择“注册代理点”和“注册点”    。  



## <a name="install-the-reporting-services-point"></a>安装 Reporting Services 点  

有关详细信息，请参阅[安装 Reporting Services 点](/sccm/core/servers/manage/configuring-reporting)。  



## <a name="next-steps"></a>后续步骤

[将 Configuration Manager 客户端部署到 Mac 计算机](/sccm/core/clients/deploy/deploy-clients-to-macs)  
