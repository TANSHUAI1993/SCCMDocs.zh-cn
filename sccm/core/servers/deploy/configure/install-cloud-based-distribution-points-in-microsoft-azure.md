---
title: "安装基于云的分发点 | Microsoft Docs"
description: "了解在 Microsoft Azure 中，开始使用基于云的分发点需要执行的操作。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 39b35cccf78bba4e69a7de0ca3a5a8dc516201e3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>在 Microsoft Azure 中安装 System Center Configuration Manager 基于云的分发点

*适用范围：System Center Configuration Manager (Current Branch)*

可以在 Microsoft Azure 中安装 System Center Configuration Manager 基于云的分发点。 如果不熟悉基于云的分发点，继续操作前请先参阅[使用基于云的分发点](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)。

 开始安装前，请确保具有必需的证书文件：  

-   已导出为 .cer 文件和 .pfx 文件的 Microsoft Azure 管理证书。  

-   已导出到 .pfx 文件的 Configuration Manager 基于云的分发点服务证书。  

    > [!TIP]
    >   有关这些证书的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)主题中有关基于云的分发点部分。 有关基于云的分发点服务证书的部署示例，请参阅 [System Center Configuration Manager PKI 证书的分步部署示例：Windows Server 2008 证书认证](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)中的“部署基于云的分发点服务证书”。  


 安装基于云的分发点后，Azure 将自动为服务生成 GUID，并将其附加到 **cloudapp.net** 的 DNS 后缀上。 使用此 GUID 时，必须配置带 DNS 别名的 DNS（CNAME 记录）。 由此，你可将在 Configuration Manager 基于云的分发点服务证书中定义的服务名称映射到自动生成的 GUID。  

 如果使用代理 Web 服务器，你可能必须配置代理设置以实现与承载分发点的云服务的通信。  

##  <a name="BKMK_ConfigWindowsAzureandInstallDP"></a>设置 Azure 并安装的基于云的分发点  
 使用以下过程设置 Azure 以支持分发点，然后在 Configuration Manager 中安装基于云的分发点。  

### <a name="to-set-up-a-cloud-service-in-azure-for-a-distribution-point"></a>在 Azure 中为分发点设置云服务  

1.  打开 Web 浏览器，转到 Azure 门户（网址为 https://manage.windowsazure.com），并访问你的帐户。  

2.  单击“托管服务、存储帐户和 CDN”，然后选择“管理证书”。  

3.  右键单击你的订阅，然后选择“添加证书” 。  

4.  对于“证书文件”，请指定 .cer 文件并单击“确定”；其中该文件包含要用于此云服务的已导出 Azure 管理证书。  

管理证书随即加载到 Azure 中，此时即可安装基于云的分发点。  

### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>为 Configuration Manager 安装基于云的分发点  

1.  完成前面过程中的步骤，在 Azure 中使用管理证书设置云服务。  

2.  在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后选择“云分发点”。 在“主页”选项卡上，单击“创建云分发点”。  

3.  在创建云分发点向导的“常规”页上，设置以下各项：  

    -   指定 Azure 帐户的“订阅 ID”。  

        > [!TIP]  
        >  可在 Azure 门户中找到 Azure 订阅 ID。  

    -   指定“管理证书” 。 单击“浏览”指定 .pfx 文件，然后输入证书密码；其中该文件包含已导出的 Azure 管理证书。 （可选）可指定 Azure SDK 1.7 中的版本 1 .publishsettings 文件。  

4.  单击“下一步” 。 Configuration Manager 将连接到 Azure 以验证管理证书。  

5.  在“设置”页上，完成以下设置，然后单击“下一步”：  

    -   对于“区域”，选择要在其中创建承载此分发点的云服务的 Azure 区域。  

    -   对于“证书文件”，请指定 .pfx 文件（其中包含已导出的 Configuration Manager 基于云的分发点服务）。 然后输入密码。  

        > [!NOTE]  
        >  将在“服务 FQDN”框中自动填写证书使用者名称。 多数情况下，无需编辑该名称。 在测试环境中使用通配证书的情况除外。 例如，该情况下可能未指定主机名，因此具有相同 DNS 后缀的多台计算机均可使用该证书。 此情况下，证书使用者具有类似于 **CN=\*.contoso.com** 的值，并且 Configuration Manager 将显示消息指示必须指定正确的 FQDN。 单击“确定”  关闭消息，然后在 DNS 后缀前输入特定名称以提供完整的 FQDN。 例如，可以添加 **clouddp1** 以指定 **clouddp1.contoso.com**的完整服务 FQDN。 域中的服务 FQDN 必须唯一，且与所有加入域的设备均不匹配。  
        >   
        >  仅支持在测试环境中使用通配证书。  

6.  在“警报”页上，设置存储配额、传输配额以及希望 Configuration Manager 在达到这些配额的百分之几时生成警报。 然后单击 **“下一步”**。  

7.  完成向导。  

向导将为基于云的分发点创建一个新的托管服务。 关闭向导后，可在 Configuration Manager 控制台中监视基于云的分发点的安装进度。 还可监视主站点服务器上的 **CloudMgr.log** 文件。 可在 Azure 门户中监视云服务的预配情况。  

> [!NOTE]  
>  在 Azure 中设置新的分发点最多可能需要 30 分钟。 以下消息将在 **CloudMgr.log** 文件中重复出现，直到预配了存储帐户为止：**Waiting for check if container exists。Will check again in 10 seconds**（正在等待检查容器是否存在。将在 10 秒内再次检查）。 然后将创建并配置服务。  

 你可以通过使用以下方法来确定基于云的分发点安装已完成：  

-   在 Azure 门户中，基于云的分发点的“部署”显示“就绪”状态。  

-   在 Configuration Manager 控制台中，访问“层次结构”工作区 >“层次结构配置”>“云”节点，可发现基于云的分发点显示“就绪”状态。  

-   Configuration Manager 显示 SMS_CLOUD_SERVICES_MANAGER 组件的状态消息 ID **9409** 。  

##  <a name="BKMK_ConfigDNSforCloudDPs"></a>为基于云的分发点设置名称解析  
 客户端必须能够将基于云的分发点的名称解析为 Azure 管理的 IP 地址，然后才能访问基于云的分发点。 客户端分两个阶段执行此操作：  

1.  客户端会将随 Configuration Manager 基于云的分发点服务证书一起提供的服务名称映射到 Azure 服务 FQDN。 此 FQDN 包含 GUID 和 **cloudapp.net**的 DNS 后缀。 GUID 是在安装基于云的分发点之后自动生成的。 若要在 Azure 门户中查看完整 FQDN，可参考云服务仪表板中的“站点 URL”。 站点 URL 的示例为“http://d1594d4527614a09b934d470.cloudapp.net” 。  

2.  客户端将 Azure 服务 FQDN 解析为 Azure 分配的 IP 地址。 此 IP 地址还可通过 Azure 门户的云服务仪表板查看，并命名为“公共虚拟 IP 地址(VIP)”。  

若要将随 Configuration Manager 基于云的分发点服务证书一起提供的服务名称（如 **clouddp1.contoso.com**）映射到 Azure 服务 FQDN（如 **d1594d4527614a09b934d470.cloudapp.net**），Internet 上的 DNS 服务器必须具有 DNS 别名（CNAME 记录）。 然后，客户端可通过 Internet 上的 DNS 服务器将 Azure 服务 FQDN 解析为 IP 地址。  

##  <a name="BKMK_ConfigProxyforCloud"></a>为管理云服务的主站点设置代理设置  
 将云服务与 Configuration Manager 结合使用时，管理基于云的分发点的主站点必须能够连接到 Azure 门户。 该站点使用主站点计算机的**系统**帐户进行连接。 此连接通过使用默认 Web 浏览器在主站点服务器计算机上进行。  

 在管理基于云的分发点的主站点服务器上，可能必须设置代理设置，才可使主站点访问 Internet 和 Azure。  

 在 Configuration Manager 控制台中使用下列过程为主站点服务器设置代理设置。  

> [!TIP]  
>  通过“添加站点系统角色向导”在主站点服务器上安装新站点系统角色时，也可设置代理服务器。  

#### <a name="to-set-up-proxy-settings-for-the-primary-site-server"></a>为主站点服务器设置代理设置  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，并单击“服务器和站点系统角色” 。 然后选择用于管理基于云的分发点的主站点服务器。  

3.  在详细信息窗格中，右键单击“站点系统” ，然后单击“属性” 。  

4.  在“站点系统属性”中，选择“代理”选项卡，然后设置此主站点服务器的代理设置。  

5.  单击“确定”以保存设置。  
