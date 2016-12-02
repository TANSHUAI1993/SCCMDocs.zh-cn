---
title: "部署 PKI 证书 | System Center Configuration Manager"
description: "按照分步示例，了解创建和部署 System Center Configuration Manager 使用的 PKI 证书的过程。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 49dfa303453b26a64c1495a1259674e0d8a6bde2


---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构

*适用范围：System Center Configuration Manager (Current Branch)*

此分步示例部署使用 Windows Server 2008 证书颁发机构 (CA)，介绍了创建和部署 System Center Configuration Manager 使用的公钥基础结构 (PKI) 证书的过程。 这些过程使用企业证书颁发机构 (CA) 和证书模板。 这些步骤仅适用于网络测试，作为对概念的验证。  

 由于部署所需的证书不止有一种方法，你必须查阅特定 PKI 部署文档，获取为特定生产环境部署所需证书必需的过程和最佳方案。 有关证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

> [!TIP]  
>  除了“测试网络要求”部分中描述的操作系统外，本主题中的说明可轻松适用于其他操作系统。 但是，如果在 Windows Server 2012 上运行颁发 CA，将不会提示你提供证书模板版本。 请改为在模板属性的“兼容性”  选项卡上指定这一点，如下所示：  
>   
>  -   **证书颁发机构**： **Windows Server 2003**  
> -   **证书接收者**： **Windows XP/Server 2003**  

## <a name="in-this-section"></a>本节内容  
 下列部分用示例介绍了创建和部署可用于 System Center Configuration Manager 的以下证书的分步说明：  

 [测试网络要求](#BKMK_testnetworkenvironment)  

 [证书的概述](#BKMK_overview2008)  

 [为运行 IIS 的站点系统部署 Web 服务器证书](#BKMK_webserver2008_cm2012)  

 [为基于云的分发点部署服务证书](#BKMK_clouddp2008_cm2012)  

 [为 Windows 计算机部署客户端证书](#BKMK_client2008_cm2012)  

 [为分发点部署客户端证书](#BKMK_clientdistributionpoint2008_cm2012)  

 [为移动设备部署注册证书](#BKMK_mobiledevices2008_cm2012)  

 [为 AMT 部署证书](#BKMK_AMT2008_cm2012)  

 [部署 Mac 计算机的客户端证书](#BKMK_MacClient_SP1)  

##  <a name="a-namebkmktestnetworkenvironmenta-test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> 测试网络要求  
 分步说明具有以下要求：  

-   测试网络运行 Windows Server 2008 的 Active Directory 域服务并且是作为单个域、单个林安装的。  

-   具有运行 Windows Server 2008 Enterprise Edition 的成员服务器，它上面安装了 Active Directory 证书服务角色，并配置为企业根证书颁发机构 (CA)。  

-   具有一台安装了 Windows Server 2008（Standard Edition 或 Enterprise Edition、R2 或更高版本）并指定为成员服务器的计算机，并在该计算机上安装了 Internet Information Services (IIS)。 此计算机将是你将使用 Intranet FQDN（以支持 Intranet 上的客户端连接）和 Internet FQDN（如果必须支持由 Internet 上的 System Center Configuration Manager 和客户端注册的移动设备）进行配置的 System Center Configuration Manager 站点系统服务器。  

-   具有一个安装了最新 Service Pack 的 Windows Vista 客户端，并且此计算机配置了由 ASCII 字符组成的计算机名称并加入到域。 此计算机将作为 System Center Configuration Manager 客户端计算机。  

-   您可以使用根域管理员帐户或企业域管理员帐户登录，然后使用此帐户来完成本示例部署中的所有过程。  

##  <a name="a-namebkmkoverview2008a-overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> 证书的概述  
 下表列出了 System Center Configuration Manager 可能需要的 PKI 证书类型，并描述了这些证书的使用方式。  

|证书要求|证书描述|  
|-----------------------------|-----------------------------|  
|运行 IIS 的站点系统的 Web 服务器证书|此证书用于对数据进行加密以及向客户端验证服务器。 此证书必须安装在站点系统服务器（运行 IIS 且在 System Center Configuration Manager 中配置为使用 HTTPS）上 System Center Configuration Manager 的外部。<br /><br /> 有关配置和安装此证书的步骤，请参阅本主题中的 [为运行 IIS 的站点系统部署 Web 服务器证书](#BKMK_webserver2008_cm2012) 。|  
|客户端用于连接到基于云的分发点的服务证书|有关配置和安装此证书的步骤，请参阅本主题中的 [为基于云的分发点部署服务证书](#BKMK_clouddp2008_cm2012) 。<br /><br /> **重要说明：** 此证书与 Windows Azure 管理证书结合使用。 有关管理证书的详细信息，请参阅 MSDN 库的“Windows Azure 平台”部分中的 [How to Create a Management Certificate（如何创建管理证书）](http://go.microsoft.com/fwlink/p/?LinkId=220281) 和 [如何将管理证书添加到 Windows Azure 订阅](http://go.microsoft.com/fwlink/?LinkId=241722) 。|  
|Windows 计算机的客户端证书|此证书用于向配置为使用 HTTPS 的站点系统验证 System Center Configuration Manager 客户端计算机。 如果管理点和状态迁移点已配置为使用 HTTPS，也可以为管理点和状态迁移点使用此证书来监视其操作状态。 此证书必须安装在计算机上 System Center Configuration Manager 的外部。<br /><br /> 有关配置和安装此证书的步骤，请参阅本主题中的 [为 Windows 计算机部署客户端证书](#BKMK_client2008_cm2012) 。|  
|分发点的客户端证书|此证书有两个用途：<br /><br /> 在分发点发送状态消息之前，此证书向启用 HTTPS 的管理点验证分发点。<br /><br /> 如果选择了“为客户端启用 PXE 支持”  分发点选项，则会将证书发送到通过 PXE 方式启动的计算机，以便它们能够在操作系统部署过程中连接到启用 HTTPS 的管理点。<br /><br /> 有关配置和安装此证书的步骤，请参阅本主题中的 [为分发点部署客户端证书](#BKMK_clientdistributionpoint2008_cm2012) 。|  
|移动设备的注册证书|此证书用于向配置为使用 HTTPS 的站点系统验证 System Center Configuration Manager 移动设备客户端。 此证书必须作为 System Center Configuration Manager 中的移动设备注册的一部分进行安装，并且选择配置的证书模板作为移动设备客户端设置。<br /><br /> 有关配置此证书的步骤，请参阅本主题中的 [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) 。|  
|Intel AMT 的证书|有三个与基于 Intel AMT 的计算机的带外管理相关的证书：AMT 设置证书、AMT Web 服务器证书以及（可选）适用于 802.1X 有线或无线网络的客户端身份验证证书。<br /><br /> AMT 预配证书必须安装在带外服务点计算机上 System Center Configuration Manager 的外部，然后才能在带外服务点属性中选择安装的证书。 AMT Web 服务器证书和客户端身份验证证书在 AMT 设置和管理过程中安装，并且你在带外管理组件属性中选择配置的证书模板。<br /><br /> 有关配置这些证书的步骤，请参阅本主题中的 [为 AMT 部署证书](#BKMK_AMT2008_cm2012) 。|  
|Mac 计算机的客户端证书|在使用 System Center Configuration Manager 注册并选择配置的证书模板作为移动设备客户端设置时，可以从 Mac 计算机中请求并安装此证书。<br /><br /> 有关配置此证书的步骤，请参阅本主题中的 [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) 。|  

##  <a name="a-namebkmkwebserver2008cm2012a-deploying-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> 为运行 IIS 的站点系统部署 Web 服务器证书  
 此证书部署包含以下过程：  

-   在证书颁发机构创建和颁发 Web 服务器证书模板  

-   申请 Web 服务器证书  

-   将 IIS 配置为使用 Web 服务器证书  

###  <a name="a-namebkmkwebserver22008a-creating-and-issuing-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> 在证书颁发机构创建和颁发 Web 服务器证书模板  
 此过程为 System Center Configuration Manager 站点系统创建证书模板并将其添加到证书颁发机构。  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>在证书颁发机构创建和颁发 Web 服务器证书模板  

1.  创建一个名为“ConfigMgr IIS 服务器”的安全组（其中包含成员服务器），用于安装将运行 IIS 的 System Center Configuration Manager 站点系统。  

2.  在安装了证书服务的成员服务器上，在“证书颁发机构”控制台中右键单击“证书模板”  ，并单击“管理”  以加载“证书模板”  控制台。  

3.  在结果窗格中，右键单击在“模板显示名称”  列中显示“Web 服务器” 的条目，然后单击“复制模板” 。  

4.  在“复制模板”  对话框中，确保已选择“Windows 2003 Server，Enterprise Edition”  ，然后单击“确定” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” 。  

5.  在  “新模板的属性”对话框中的  “常规”选项卡上，输入生成将在 Configuration Manager 站点系统上使用的 Web 证书所需的模板名称，例如 **ConfigMgr Web 服务器证书**。  

6.  单击“使用者名称”  选项卡，并确保选择了“在请求中提供”  。  

7.  单击“安全”  选项卡，并从安全组“域管理员”  和“企业管理员”  中删除“注册” 权限。  

8.  单击“添加” ，在文本框中输入 **ConfigMgr IIS 服务器** ，然后单击“确定” 。  

9. 为此组选择“注册”  权限，并且不要清除“读取”  权限。  

10. 单击“确定” ，然后关闭“证书模板控制台” 。  

11. 在证书颁发机构控制台中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

12. 在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr Web 服务器证书” ，然后单击“确定” 。  

13. 如果不需要创建和颁发任何其他证书，请关闭“证书颁发机构” 。  

###  <a name="a-namebkmkwebserver32008a-requesting-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> 申请 Web 服务器证书  
 此过程允许你指定将在站点系统服务器属性中配置的 Intranet 和 Internet FQDN 值，然后将 Web 服务器证书安装到运行 IIS 的成员服务器上。  

##### <a name="to-request-the-web-server-certificate"></a>申请 Web 服务器证书  

1.  重启运行 IIS 的成员服务器，以确保计算机可访问你通过使用所配置的“读取”  和“注册”  权限创建的证书模板。  

2.  单击“开始”，再单击“运行”，然后键入“mmc.exe”。 在空白控制台中，单击“文件” ，然后单击“添加/删除管理单元” 。  

3.  在“添加/删除管理单元”  对话框中，从“可用的管理单元”  列表中选择“证书” ，然后单击“添加” 。  

4.  在“证书管理单元”  对话框中，选择“计算机帐户” ，然后单击“下一步” 。  

5.  在  “选择计算机”对话框中，确保选中“本地计算机: (运行此控制台的计算机)”  ，然后单击“完成” 。  

6.  在“添加/删除管理单元”  对话框中，单击“确定” 。  

7.  在控制台中展开“证书（本地计算机）” ，然后单击“个人” 。  

8.  右键单击“证书” ，单击“所有任务” ，然后单击“申请新证书” 。  

9. 在“开始之前”  页面上，单击“下一步” 。  

10. 如果您看到“选择证书注册策略”  页，请单击“下一步” 。  

11. 在“申请证书”页面上，从显示的证书列表中找到“ConfigMgr Web 服务器证书”，然后单击“注册此证书需要更多信息”**。单击这里以配置设置”**。  

12. 在“证书属性”  对话框中的“使用者”  选项卡上，不要对“使用者名称” 进行任何更改。 这意味着“使用者名称”  部分的“值”  框保留为空白。 作为替代，请从“备用名称”  部分单击“类型”  下拉列表，然后选择“DNS” 。  

13. 在“值”框中，指定将在 System Center Configuration Manager 站点系统属性中指定的 FQDN 值，然后单击“确定”关闭“证书属性”对话框。  

     例如：  

    -   如果站点系统将仅接受来自 Intranet 的客户端连接，并且站点系统服务器的 Intranet FQDN 为 **server1.internal.contoso.com**：键入 **server1.internal.contoso.com**，然后单击“添加” 。  

    -   如果站点系统将接受来自 Intranet 和 Internet 的客户端连接，并且站点系统服务器的 Intranet FQDN 为 **server1.internal.contoso.com** ，站点系统服务器的 Internet FQDN 为 **server.contoso.com**：  

        1.  键入 **server1.internal.contoso.com**，然后单击“添加” 。  

        2.  键入 **server.contoso.com**，然后单击“添加” 。  

        > [!NOTE]  
        >  按什么顺序为 System Center Configuration Manager指定 FQDN 并不重要。 但是，请检查将使用证书的所有设备（例如移动设备和代理 Web 服务器）是否可使用证书 SAN 和 SAN 中的多个值。 如果设备对证书中的 SAN 值的支持有限，你可能必须更改 FQDN 的顺序或改用“使用者”值。  

14. 在“申请证书”  页面上，从显示的证书列表中选择“ConfigMgr Web 服务器证书”  ，然后单击“注册” 。  

15. 在“证书安装结果”  页面中，等待证书安装完成，然后单击“完成” 。  

16. 关闭“证书（本地计算机）” 。  

###  <a name="a-namebkmkwebserver42008a-configuring-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> 将 IIS 配置为使用 Web 服务器证书  
 此过程将安装的证书绑定到 IIS 的“默认网站” 。  

##### <a name="to-configure-iis-to-use-the-web-server-certificate"></a>将 IIS 配置为使用 Web 服务器证书  

1.  在安装了 IIS 的成员服务器上，依次单击“开始” 、“程序” 、“管理工具” ，然后单击“Internet 信息服务 (IIS) 管理器” 。  

2.  展开“站点” ，右键单击“默认网站” ，然后选择“编辑绑定” 。  

3.  单击“https”  条目，然后单击“编辑” 。  

4.  在“编辑网站绑定”  对话框中，使用“ConfigMgr Web 服务器证书”模板选择您申请的证书，然后单击“确定” 。  

    > [!NOTE]  
    >  如果您不确定哪一个是正确的证书，请选择一个证书，然后单击“查看” 。 这允许你将所选证书的详细信息与证书单元显示的证书进行比较。 例如，证书单元显示用于申请证书的证书模板。 然后，您可以将使用“ConfigMgr Web 服务器证书”模板申请的证书的证书指纹与当前在“编辑网站绑定”  对话框中选择的证书的证书指纹进行比较。  

5.  在“编辑网站绑定”  对话框中单击“确定”  ，然后单击“关闭” 。  

6.  关闭“Internet Information Services (IIS) 管理器” 。  

 成员服务器现在已预配 System Center Configuration Manager Web 服务器证书。  

> [!IMPORTANT]  
>  在此计算机上安装 System Center Configuration Manager 站点系统服务器时，请确保在站点系统属性中指定与请求证书时所指定的 FQDN 相同的 FQDN。  

##  <a name="a-namebkmkclouddp2008cm2012a-deploying-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> 为基于云的分发点部署服务证书  

> [!NOTE]  
>  基于云的分发点的服务证书适用于 System Center Configuration Manager SP1 和更高版本。  

 此证书部署包含以下过程：  

-   [在证书颁发机构创建和颁发自定义 Web 服务器证书模板](#BKMK_clouddpcreating2008)  

-   [申请自定义 Web 服务器证书](#BKMK_clouddprequesting2008)  

-   [为基于云的分发点导出自定义 Web 服务器证书](#BKMK_clouddpexporting2008)  

###  <a name="a-namebkmkclouddpcreating2008a-creating-and-issuing-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> 在证书颁发机构创建和颁发自定义 Web 服务器证书模板  
 此过程创建基于 Web 服务器证书模板的自定义证书模板。 此证书适用于 System Center Configuration Manager 基于云的分发点，并且私钥必须可导出。 创建了证书模板后，会将其添加到证书颁发机构。  

> [!NOTE]  
>  此过程使用的证书模板与你为运行 IIS 的站点系统所创建的 Web 服务器证书模板不同，因为尽管两个证书都需要服务器身份验证功能，但基于云的分发点的证书要求你为“使用者名称”输入自定义值，并且私钥必须可导出。 最佳安全方案是，除非此配置为必需，否则不要配置证书模板以允许导出私钥。 基于云的分发点之所以需要此配置，原因是你必须以文件形式导入证书，而不是从证书存储中选择证书。  
>   
>  通过为此证书创建新证书模板，你可以限制哪些计算机可申请允许导出私钥的证书。 在生产网络上，你还可以考虑为此证书增加以下修改之处：  
>   
>  -   要求批准来安装证书以提高安全性。  
> -   增长证书有效期。 由于每次证书到期之前你都必须导出并导入证书，因此增长有效期可减少你必须重复此过程的频率。 但是，如果增长有效期，则会降低证书的安全性，因为攻击者将有更多的时间来对私钥进行解密并窃取证书。  
> -   在证书的使用者备用名称 (SAN) 中使用自定义值来帮助从用于 IIS 的标准 Web 服务器证书中识别此证书。  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>在证书颁发机构创建和颁发自定义 Web 服务器证书模板  

1.  创建一个名为“ConfigMgr 站点服务器”的安全组（其中包含成员服务器），用于安装将管理基于云的分发点的 System Center Configuration Manager 主站点服务器。  

2.  在运行“证书颁发机构”控制台的成员服务器上，右键单击“证书模板” ，然后单击“管理”  以加载“证书模板”管理控制台。  

3.  在结果窗格中，右键单击在“模板显示名称”  列中显示“Web 服务器” 的条目，然后单击“复制模板” 。  

4.  在“复制模板”  对话框中，确保已选择“Windows 2003 Server，Enterprise Edition”  ，然后单击“确定” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” 。  

5.  在  “新模板的属性”对话框中的  “常规”选项卡上，输入生成基于云分发点的 Web 服务器证书所需的模板名称，例如， **ConfigMgr 基于云的分发点证书**。  

6.  单击“请求处理”  选项卡，然后选择“允许导出私钥” 。  

7.  单击“安全”  选项卡，并从“企业管理员”  安全组中删除“注册”  权限。  

8.  单击“添加” ，在文本框中输入 **ConfigMgr 站点服务器** ，然后单击“确定” 。  

9. 为此组选择“注册”  权限，并且不要清除“读取”  权限。  

10. 单击“确定”  ，然后关闭“证书模板控制台” 。  

11. 在证书颁发机构控制台中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

12. 在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr 基于云的分发点证书” ，然后单击“确定” 。  

13. 如果不必创建和颁发任何其他证书，请关闭“证书颁发机构” 。  

###  <a name="a-namebkmkclouddprequesting2008a-requesting-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> 申请自定义 Web 服务器证书  
 此过程将申请自定义 Web 服务器证书并随后将其安装到将运行站点服务器的成员服务器上。  

##### <a name="to-request-the-custom-web-server-certificate"></a>申请自定义 Web 服务器证书  

1.  在创建和配置“ConfigMgr 站点服务器”  安全组后重启成员服务器，以确保计算机可访问你通过使用所配置的“读取”  和“注册”  权限创建的证书模板。  

2.  单击“开始”，再单击“运行”，然后键入“mmc.exe”。 在空白控制台中，单击“文件” ，然后单击“添加/删除管理单元” 。  

3.  在“添加/删除管理单元”  对话框中，从“可用的管理单元”  列表中选择“证书” ，然后单击“添加” 。  

4.  在“证书管理单元”  对话框中，选择“计算机帐户” ，然后单击“下一步” 。  

5.  在  “选择计算机”对话框中，确保选中“本地计算机: (运行此控制台的计算机)”  ，然后单击“完成” 。  

6.  在“添加/删除管理单元”  对话框中，单击“确定” 。  

7.  在控制台中展开“证书（本地计算机）” ，然后单击“个人” 。  

8.  右键单击“证书” ，单击“所有任务” ，然后单击“申请新证书” 。  

9. 在“开始之前”  页面上，单击“下一步” 。  

10. 如果您看到“选择证书注册策略”  页，请单击“下一步” 。  

11. 在“申请证书”页面上，从显示的证书列表中找到“ConfigMgr 基于云的分发点证书”，然后单击“注册此证书需要更多信息”**。单击这里以配置设置”**。  

12. 在“证书属性”  对话框中的“使用者”  选项卡上，为“使用者名称” 选择“公用名”  作为“类型” 。  

13. 在“值”  框中，使用 FQDN 格式指定你选择的服务名称和域名。 例如： **clouddp1.contoso.com**。  

    > [!NOTE]  
    >  你指定什么服务名称并不重要，只要该名称在命名空间中唯一即可。 你将使用 DNS 创建别名（CNAME 记录）以从 Windows Azure 中将此服务名称映射到自动生成的标识符 (GUID) 和 IP 地址。  

14. 单击“添加” ，并单击“确定”  关闭“证书属性”  对话框。  

15. 在“申请证书”  页上，从显示的证书列表中选择“ConfigMgr 基于云的分发点证书”  ，然后单击“注册” 。  

16. 在“证书安装结果”  页面中，等待证书安装完成，然后单击“完成” 。  

17. 关闭“证书（本地计算机）” 。  

###  <a name="a-namebkmkclouddpexporting2008a-exporting-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> 为基于云的分发点导出自定义 Web 服务器证书  
 此过程将自定义 Web 服务器证书导出为文件，以便在创建基于云的分发点时可将其导入。  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>为基于云的分发点导出自定义 Web 服务器证书  

1.  在“证书(本地计算机)”  控制台中，右键单击刚刚安装的证书，选择“所有任务” ，然后单击“导出” 。  

2.  在证书导出向导中，单击“下一步” 。  

3.  在“导出私钥”  页上，选择“是，导出私钥” ，然后单击“下一步” 。  

    > [!NOTE]  
    >  如果此选项不可用，则表明在创建证书时没有选择导出私钥。 在这种情况下，您无法按要求的格式导出证书。 你必须重新配置证书模板以允许导出私钥，然后再次申请证书。  

4.  在“导出文件格式”  页上，确保“个人信息交换 - PKCS #12(.PFX)”  选项处于选定状态。  

5.  在“密码”  页上，指定一个用于保护导出的证书及其私钥的强密码，然后单击“下一步” 。  

6.  在“要导出的文件”  页上，指定你要导出的文件的名称，然后单击“下一步” 。  

7.  要关闭向导，请在“证书导出向导”  页中单击“完成”  ，并在确认对话框中单击“确定”  。  

8.  关闭“证书（本地计算机）” 。  

9. 安全地存储文件，确保可以从 System Center Configuration Manager 控制台访问该文件。  

 证书现在已准备好，可在你创建基于云的分发点时导入。  

##  <a name="a-namebkmkclient2008cm2012a-deploying-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> 为 Windows 计算机部署客户端证书  
 此证书部署包含以下过程：  

-   在证书颁发机构创建和颁发工作站身份验证证书模板  

-   使用组策略配置工作站身份验证模板的自动注册  

-   自动注册工作站身份验证证书并验证其在计算机上的安装  

###  <a name="a-namebkmkclient02008a-creating-and-issuing-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> 在证书颁发机构创建和颁发工作站身份验证证书模板  
 此过程为 System Center Configuration Manager 客户端计算机创建证书模板并将其添加到证书颁发机构。  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>在证书颁发机构创建和颁发工作站身份验证证书模板  

1.  在运行“证书颁发机构”控制台的成员服务器上，右键单击“证书模板” ，然后单击“管理”  以加载“证书模板”管理控制台。  

2.  在结果窗格中，右键单击在“模板显示名称”  列中显示“工作站身份验证” 的条目，然后单击“复制模板” 。  

3.  在“复制模板”  对话框中，确保已选择“Windows 2003 Server，Enterprise Edition”  ，然后单击“确定” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” 。  

4.  在  “新模板的属性”对话框中的  “常规”选项卡上，输入生成在 Configuration Manager 客户端计算机上使用的客户端证书所需的模板名称，例如 **ConfigMgr 客户端证书**  

5.  单击“安全”  选项卡，选择“域计算机”  组，然后选择其他权限“读取”  和“自动注册” 。 不要清除“注册” 。  

6.  单击“确定”  ，然后关闭“证书模板控制台” 。  

7.  在证书颁发机构控制台中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

8.  在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr 客户端证书” ，然后单击“确定” 。  

9. 如果不需要创建和颁发任何其他证书，请关闭“证书颁发机构” 。  

###  <a name="a-namebkmkclient12008a-configuring-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> 使用组策略配置工作站身份验证模板的自动注册  
 此过程将配置组策略以在计算机上自动注册客户端证书。  

##### <a name="to-configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>使用组策略配置工作站身份验证模板的自动注册  

1.  在域控制器上，依次单击“开始” 、“管理工具” ，然后单击“组策略管理” 。  

2.  导航到您的域，右键单击域，然后选择“在这个域中创建 GPO 并在此处链接” 。  

    > [!NOTE]  
    >  此步骤使用为自定义设置创建新的组策略这一最佳方案，而不是编辑随 Active Directory 域服务安装的默认域策略。 通过在域级别分配此组策略，您会将它应用到域中的所有计算机。 但是在生产环境中，您可以通过在组织单位级别分配组策略来限制自动注册，以便它仅在选择的计算机上注册，或者您也可以使用安全组筛选域组策略，以便它仅应用于组中的计算机。 如果限制自动注册，请记住包括配置为管理点的服务器。  

3.  在“新建 GPO”  对话框中，输入新组策略的名称（如 **自动注册证书**），然后单击“确定” 。  

4.  在结果窗格的“链接的组策略对象”  选项卡上，右键单击新的组策略，然后单击“编辑” 。  

5.  在“组策略管理编辑器”中，展开“计算机配置”下的“策略”，然后导航到“Windows 设置”/“安全设置”/“公钥策略”。  

6.  右键单击名为“证书服务客户端 - 自动注册”的对象类型，然后单击“属性”。  

7.  从“配置型号”  下拉列表中，依次选择“已启用” 、“续订过期证书、更新未决证书并删除吊销的证书” 、“更新使用证书模板的证书” ，然后单击“确定” 。  

8.  关闭“组策略管理” 。  

###  <a name="a-namebkmkclient22008a-automatically-enrolling-the-workstation-authentication-certificate-and-verifying-its-installation-on-computers"></a><a name="BKMK_client22008"></a> 自动注册工作站身份验证证书并验证其在计算机上的安装  
 此过程在计算机上安装客户端证书，并验证安装。  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>自动注册工作站身份验证证书并验证其在客户端计算机上的安装  

1.  重新启动工作站计算机，并等待几分钟再登录。  

    > [!NOTE]  
    >  重新启动计算机是确保证书注册成功最可靠的方法。  

2.  使用具有管理特权的帐户登录。  

3.  在搜索框中，键入 **mmc.exe.**，然后按 **Enter**。  

4.  在空管理控制台中，单击“文件” ，然后单击“添加/删除管理单元” 。  

5.  在“添加/删除管理单元”  对话框中，从“可用的管理单元”  列表中选择“证书” ，然后单击“添加” 。  

6.  在“证书管理单元”  对话框中，选择“计算机帐户” ，然后单击“下一步” 。  

7.  在  “选择计算机”对话框中，确保选中“本地计算机: (运行此控制台的计算机)”  ，然后单击“完成” 。  

8.  在“添加/删除管理单元”  对话框中，单击“确定” 。  

9. 在控制台中展开“证书（本地计算机）” ，展开“个人” ，然后单击“证书” 。  

10. 在结果窗格中，确认显示证书，并且在“预期目的  ”列中显示“客户端身份验证”  ，在“证书模板”  列中显示“ConfigMgr 客户端证书”  。  

11. 关闭“证书（本地计算机）” 。  

12. 对成员服务器重复步骤 1 至 11，以验证将被配置为管理点的服务器是否也具有客户端证书。  

 计算机现在已预配 System Center Configuration Manager 客户端证书。  

##  <a name="a-namebkmkclientdistributionpoint2008cm2012a-deploying-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> 为分发点部署客户端证书  

> [!NOTE]  
>  由于证书要求相同，此证书还可用于不使用 PXE 启动的媒体映像。  

 此证书部署包含以下过程：  

-   在证书颁发机构创建和颁发自定义工作站身份验证证书模板  

-   申请自定义工作站身份验证证书  

-   为分发点导出客户端证书  

###  <a name="a-namebkmkclientdistributionpoint02008a-creating-and-issuing-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> 在证书颁发机构创建和颁发自定义工作站身份验证证书模板  
 此过程为 System Center Configuration Manager 分发点创建一个允许导出私钥的自定义证书模板，并将该证书模板添加到证书颁发机构。  

> [!NOTE]  
>  此过程使用的证书模板与你为客户端计算机创建的证书模板不同，因为尽管两个证书都需要客户端身份验证功能，但分发点的证书要求导出私钥。 最佳安全方案是，除非此配置为必需，否则不要配置证书模板以允许导出私钥。 分发点之所以需要此配置，原因是你必须以文件形式导入证书，而不是从证书存储中选择证书。  
>   
>  通过为此证书创建新证书模板，你可以限制哪些计算机可申请允许导出私钥的证书。 在我们的示例部署中，这将是你之前为运行 IIS 的 System Center Configuration Manager 站点系统服务器创建的安全组。 在分发 IIS 站点系统角色的生产网络上，考虑为运行分发点的服务器创建一个新安全组，以便能够将证书限制为仅供这些站点系统服务器使用。 你还可以考虑为此证书增加以下修改之处：  
>   
>  -   要求批准来安装证书以提高安全性。  
> -   增长证书有效期。 由于每次证书到期之前你都必须导出并导入证书，因此增长有效期可减少你必须重复此过程的频率。 但是，如果增长有效期，则会降低证书的安全性，因为攻击者将有更多的时间来对私钥进行解密并窃取证书。  
> -   在证书的“使用者”字段或使用者备用名称 (SAN) 中使用自定义值来帮助从标准客户端证书中识别此证书。 如果你将为多个分发点使用同一证书，则这一点可能特别有用。  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>在证书颁发机构创建和颁发自定义工作站身份验证证书模板  

1.  在运行“证书颁发机构”控制台的成员服务器上，右键单击“证书模板” ，然后单击“管理”  以加载“证书模板”管理控制台。  

2.  在结果窗格中，右键单击在“模板显示名称”  列中显示“工作站身份验证” 的条目，然后单击“复制模板” 。  

3.  在“复制模板”  对话框中，确保已选择“Windows 2003 Server，Enterprise Edition”  ，然后单击“确定” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” 。  

4.  在  “新模板的属性”对话框中的  “常规”选项卡上，输入生成分发点的客户端身份验证所需的模板名称，例如 **ConfigMgr Web 客户端分发点证书**。  

5.  单击“请求处理”  选项卡，然后选择“允许导出私钥” 。  

6.  单击“安全”  选项卡，并从“企业管理员”  安全组中删除“注册”  权限。  

7.  单击“添加” ，在文本框中输入 **ConfigMgr IIS 服务器** ，然后单击“确定” 。  

8.  为此组选择“注册”  权限，并且不要清除“读取”  权限。  

9. 单击“确定”  ，然后关闭“证书模板控制台” 。  

10. 在证书颁发机构控制台中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

11. 在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr 客户端分发点证书” ，然后单击“确定” 。  

12. 如果不必创建和颁发任何其他证书，请关闭“证书颁发机构” 。  

###  <a name="a-namebkmkclientdistributionpoint12008a-requesting-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> 申请自定义工作站身份验证证书  
 此过程申请自定义客户端证书，然后将其安装到运行 IIS 并将配置为分发点的成员服务器上。  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>申请自定义工作站身份验证证书  

1.  单击“开始”，再单击“运行”，然后键入“mmc.exe”。 在空白控制台中，单击“文件” ，然后单击“添加/删除管理单元” 。  

2.  在“添加/删除管理单元”  对话框中，从“可用的管理单元”  列表中选择“证书” ，然后单击“添加” 。  

3.  在“证书管理单元”  对话框中，选择“计算机帐户” ，然后单击“下一步” 。  

4.  在  “选择计算机”对话框中，确保选中“本地计算机: (运行此控制台的计算机)”  ，然后单击“完成” 。  

5.  在“添加/删除管理单元”  对话框中，单击“确定” 。  

6.  在控制台中展开“证书（本地计算机）” ，然后单击“个人” 。  

7.  右键单击“证书” ，单击“所有任务” ，然后单击“申请新证书” 。  

8.  在“开始之前”  页面上，单击“下一步” 。  

9. 如果您看到“选择证书注册策略”  页，请单击“下一步” 。  

10. 在“申请证书”  页上，从显示的证书列表中选择“ConfigMgr 客户端分发点证书”  ，然后单击“注册” 。  

11. 在“证书安装结果”  页面中，等待证书安装完成，然后单击“完成” 。  

12. 在结果窗格中，确认证书已显示，并且在“预期目的”  列中显示“客户端身份验证”  ，在“证书模板”  列中显示“ConfigMgr 客户端分发点证书”  。  

13. 不要关闭“证书（本地计算机）” 。  

###  <a name="a-namebkmkexportclientdistributionpoint22008a-exporting-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> 为分发点导出客户端证书  
 此过程将自定义工作站身份验证证书导出为文件，以便可将其导入分发点属性。  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>为分发点导出客户端证书  

1.  在“证书(本地计算机)”  控制台中，右键单击刚刚安装的证书，选择“所有任务” ，然后单击“导出” 。  

2.  在证书导出向导中，单击“下一步” 。  

3.  在“导出私钥”  页上，选择“是，导出私钥” ，然后单击“下一步” 。  

    > [!NOTE]  
    >  如果此选项不可用，则表明在创建证书时没有选择导出私钥。 在这种情况下，您无法按要求的格式导出证书。 你必须重新配置证书模板以允许导出私钥，然后再次申请证书。  

4.  在“导出文件格式”  页上，确保“个人信息交换 - PKCS #12(.PFX)”  选项处于选定状态。  

5.  在“密码”  页上，指定一个用于保护导出的证书及其私钥的强密码，然后单击“下一步” 。  

6.  在“要导出的文件”  页上，指定你要导出的文件的名称，然后单击“下一步” 。  

7.  要关闭向导，请在“证书导出向导”  页中单击“完成”  ，并在确认对话框中单击“确定”  。  

8.  关闭“证书（本地计算机）” 。  

9. 安全地存储文件，确保可以从 System Center Configuration Manager 控制台访问该文件。  

 证书现在已准备好，可在你配置分发点时导入。  

> [!TIP]  
>  在为不使用 PXE 启动的操作系统部署配置媒体映像，并且用于安装映像的任务序列必须与需要 HTTPS 客户端连接的管理点联系时，你可以使用同一证书文件。  

##  <a name="a-namebkmkmobiledevices2008cm2012a-deploying-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> 为移动设备部署注册证书  
 此证书部署包含一个用于在证书颁发机构创建和颁发注册证书模板的单一过程。  

### <a name="creating-and-issuing-the-enrollment-certificate-template-on-the-certification-authority"></a>在证书颁发机构创建和颁发注册证书模板  
 此过程为 System Center Configuration Manager 移动设备创建注册证书模板并将其添加到证书颁发机构。  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>在证书颁发机构创建和颁发注册证书模板  

1.  创建一个安全组，其中包含将在 System Center Configuration Manager 中注册移动设备的用户。  

2.  在安装了证书服务的成员服务器上，在“证书颁发机构”控制台中右键单击“证书模板” ，然后单击“管理”  以加载“证书模板”管理控制台。  

3.  在结果窗格中，右键单击在“模板显示名称”  列中显示“经过身份验证的会话” 的条目，然后单击“复制模板” 。  

4.  在“复制模板”  对话框中，确保已选择“Windows 2003 Server，Enterprise Edition”  ，然后单击“确定” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” 。  

5.  在“新模板的属性”对话框中的“常规”选项卡上，输入模板名称以便为要由 System Center Configuration Manager 管理的移动设备生成注册证书，例如“ConfigMgr 移动设备注册证书”。  

6.  单击“使用者名称”  选项卡，确保选中“用此 Active Directory 信息生成”  ，再为“使用者名称格式:”  选择“公用名”  ，然后从“将这个信息包括在另一个使用者名称中”  取消选择“用户主体名称(UPN)” 。  

7.  单击“安全”  选项卡，选择安全组（其中包含拥有要注册的移动设备的用户），并选择“注册” 的其他权限。 不要清除“读取” 。  

8.  单击“确定”  ，然后关闭“证书模板控制台” 。  

9. 在证书颁发机构控制台中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

10. 在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr 移动设备注册证书” ，然后单击“确定” 。  

11. 如果不需要创建和颁发任何其他证书，请关闭“证书颁发机构”控制台。  

 移动设备注册证书模板现在已准备好，当你在客户端设置中配置移动设备注册配置文件时即可选择。  

##  <a name="a-namebkmkamt2008cm2012a-deploying-the-certificates-for-amt"></a><a name="BKMK_AMT2008_cm2012"></a> 为 AMT 部署证书  
 此证书部署包含以下过程：  

-   创建、颁发和安装 AMT 设置证书  

-   为基于 AMT 的计算机创建和颁发 Web 服务器证书  

-   为 802.1X 基于 AMT 的计算机创建和颁发客户端身份验证证书  

###  <a name="a-namebkmkamtprovisioning2008a-creating-issuing-and-installing-the-amt-provisioning-certificate"></a><a name="BKMK_AMTprovisioning2008"></a> Creating, Issuing, and Installing the AMT Provisioning Certificate  
 在通过内部根 CA 的证书指纹配置基于 AMT 的计算机时，使用内部 CA 创建设置证书。 如果不是这种情况，并且必须使用外部证书颁发机构，请使用颁发 AMT 设置证书的公司提供的说明，这些说明通常涉及到从公司的公共网站中申请证书。 还可以在 Intel vPro Expert Center 找到所选外部 CA 的详细说明：Microsoft vPro Manageability 网站 ([http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001))（页面可能为英文）。  

> [!IMPORTANT]  
>  外部 CA 可能不支持 Intel AMT 设置对象标识符。 In diesem Fall können Sie das OU-Attribut **Intel(R) Client Setup Certificate**verwenden.  

 当你从外部 CA 申请 AMT 设置证书时，请将该证书安装到承载带外服务点的成员服务器上的计算机个人证书存储中。  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>申请和颁发 AMT 设置证书  

1.  创建一个安全组，其中包含将运行带外服务点的站点系统服务器的计算机帐户。  

2.  在安装了证书服务的成员服务器上，在“证书颁发机构”控制台中右键单击“证书模板” ，然后单击“管理”  以加载“证书模板”  控制台。  

3.  在结果窗格中，右键单击在“模板显示名称”  列中显示“Web 服务器”  的条目，然后单击“复制模板” 。  

4.  在“复制模板”  对话框中，确保已选择“Windows 2003 Server，Enterprise Edition”  ，然后单击“确定” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” 。  

5.  在  “新模板的属性”对话框中的“常规”  选项卡上，输入 AMT 设置证书模板的模板名称，如 **ConfigMgr AMT 设置**。  

6.  单击“使用者名称”  选项卡，选择“用 Active Directory 中的信息生成” ，然后选择“公用名” 。  

7.  单击“扩展”  选项卡，确保选择“应用程序策略”  ，然后单击“编辑” 。  

8.  在“编辑应用程序策略扩展”  对话框中，单击“添加” 。  

9. 在“添加应用程序策略”  对话框中，单击“新建” 。  

10. 在“新建应用程序策略”对话框中，在“名称”字段键入“AMT 设置”，然后为“对象标识符”键入以下数字：**2.16.840.1.113741.1.2.3**。  

11. 单击“确定” ，然后单击“添加应用程序策略”  对话框中的“确定”  。  

12. 单击“编辑应用程序策略扩展”  对话框中的“确定”  。  

13. 现在，在“新模板的属性”  对话框中，您会看到如“应用程序策略”  描述中所列的下列内容：“服务器身份验证”  和“AMT 设置” 。  

14. 单击“安全”  选项卡，并从安全组“域管理员”  和“企业管理员”  中删除“注册” 权限。  

15. 单击“添加” ，输入包含带外服务点站点系统角色的计算机帐户的安全组的名称，然后单击“确定” 。  

16. 为此组选择“注册”  权限，并且不要清除“读取”  权限。  

17. 单击“确定” ，然后关闭“证书模板”  控制台。  

18. 在“证书颁发机构” 中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

19. 在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr AMT 设置” ，然后单击“确定” 。  

    > [!NOTE]  
    >  如果不能完成步骤 18 或 19，请检查你是否正在使用 Windows Server 2008 Enterprise Edition。 虽然可以使用 Windows Server Standard Edition 和证书服务配置模板，但是只有使用 Windows Server 2008 Enterprise Edition 时才能使用修改的证书模板部署证书。  

20. 不要关闭“证书颁发机构” 。  

 来自内部 CA 的 AMT 设置证书现在已准备好，可安装在带内服务点计算机上。  

##### <a name="to-install-the-amt-provisioning-certificate"></a>安装 AMT 设置证书  

1.  重启运行 IIS 的成员服务器，确保它可以使用配置的权限访问证书模板。  

2.  单击“开始”，再单击“运行”，然后键入“mmc.exe”。 在空白控制台中，单击“文件” ，然后单击“添加/删除管理单元” 。  

3.  在“添加/删除管理单元”  对话框中，从“可用的管理单元”  列表中选择“证书” ，然后单击“添加” 。  

4.  在“证书管理单元”  对话框中，选择“计算机帐户” ，然后单击“下一步” 。  

5.  在  “选择计算机”对话框中，确保选中“本地计算机: (运行此控制台的计算机)”  ，然后单击“完成” 。  

6.  在“添加/删除管理单元”  对话框中，单击“确定” 。  

7.  在控制台中展开“证书（本地计算机）” ，然后单击“个人” 。  

8.  右键单击“证书” ，单击“所有任务” ，然后单击“申请新证书” 。  

9. 在“开始之前”  页面上，单击“下一步” 。  

10. 如果您看到“选择证书注册策略”  页，请单击“下一步” 。  

11. 在“申请证书”  页上，从显示的证书列表中选择“AMT 设置”  ，然后单击“注册” 。  

12. 在“证书安装结果”  页面中，等待证书安装完成，然后单击“完成” 。  

13. 关闭“证书（本地计算机）” 。  

 来自内部 CA 的 AMT 设置证书现已安装并准备好，可在带外服务点属性中选择。  

### <a name="creating-and-issuing-the-web-server-certificate-for-amt-based-computers"></a>为基于 AMT 的计算机创建和颁发 Web 服务器证书  
 使用下列过程为基于 AMT 的计算机准备 Web 服务器证书。  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>创建和颁发 Web 服务器证书模板  

1.  创建一个空白的安全组，以包含 System Center Configuration Manager 在 AMT 设置期间创建的 AMT 计算机帐户。  

2.  在安装了证书服务的成员服务器上，在“证书颁发机构”控制台中右键单击“证书模板” ，然后单击“管理”  以加载“证书模板”  控制台。  

3.  在结果窗格中，右键单击在“模板显示名称”  列中显示“Web 服务器” 的条目，然后单击“复制模板” 。  

4.  在“复制模板”  对话框中，确保已选择“Windows 2003 Server，Enterprise Edition”  ，然后单击“确定” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” **。**  

5.  在  “新模板的属性”对话框的  “常规”选项卡上，输入生成用于在 AMT 计算机上进行带外管理的 Web 证书所需的模板名称，例如 **ConfigMgr AMT Web 服务器证书**。  

6.  单击“使用者名称”  选项卡，单击“用 Active Directory 中的信息生成” ，为“使用者名称格式”  选择“公用名” ，然后为使用者可选名称清除“用户主体名称(UPN)”  。  

7.  单击“安全”  选项卡，并从安全组“域管理员”  和“企业管理员”  中删除“注册” 权限。  

8.  单击“添加”  ，然后输入为 AMT 设置所创建的安全组的名称。 然后单击“确定” 。  

9. 为此安全组选择下列“允许”  权限：“读取”  和“注册” 。  

10. 单击“确定” ，然后关闭“证书模板”  控制台。  

11. 在“证书颁发机构”  控制台中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

12. 在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr AMT Web 服务器证书” ，然后单击“确定” 。  

13. 如果不必创建和颁发任何其他证书，请关闭“证书颁发机构” 。  

 现在，AMT Web 服务器模板已准备好利用 Web 服务器证书来设置基于 AMT 的计算机。 在带外管理组件属性中选择该证书模板。  

### <a name="creating-and-issuing-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>为 802.1X 基于 AMT 的计算机创建和颁发客户端身份验证证书  
 如果基于 AMT 的计算机将对经过 802.1X 身份验证的有线或无线网络使用客户端证书，请使用下列过程。  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>在 CA 上创建和颁发客户端身份验证证书模板的步骤  

1.  在安装了证书服务的成员服务器上，在“证书颁发机构”控制台中右键单击“证书模板” ，然后单击“管理”  以加载“证书模板”  控制台。  

2.  在结果窗格中，右键单击在“模板显示名称”  列中显示“工作站身份验证” 的条目，然后单击“复制模板” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” **。**  

3.  在  “新模板的属性”对话框的  “常规”选项卡上，输入生成用于在 AMT 计算机上进行带外管理的客户端证书所需的模板名称，例如 **ConfigMgr AMT 802.1X 客户端证书**。  

4.  单击“使用者名称”  选项卡，单击“用 Active Directory 中的信息生成”  ，然后为“使用者名称格式”  选择“公用名” 。 为使用者可选名称清除“DNS 名称”  ，然后选择“用户主体名称(UPN)” 。  

5.  单击“安全”  选项卡，并从安全组“域管理员”  和“企业管理员”  中删除“注册” 权限。  

6.  单击“添加”  ，然后输入你将在带外管理组件属性中指定的安全组的名称，以包含基于 AMT 的计算机的计算机帐户。 然后单击“确定” 。  

7.  为此安全组选择下列“允许”  权限：“读取”  和“注册” 。  

8.  单击“确定”，关闭“证书模板”管理控制台，“certtmpl - [证书模板]”。  

9. 在“证书颁发机构”  管理控制台中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

10. 在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr AMT 802.1X 客户端身份验证证书” ，然后单击“确定” 。  

11. 如果不需要创建和颁发任何其他证书，请关闭“证书颁发机构” 。  

 客户端身份验证证书模板现在已准备好向基于 AMT 的计算机颁发用于 802.1X 客户端身份验证的证书。 在带外管理组件属性中选择该证书模板。  

##  <a name="a-namebkmkmacclientsp1a-deploying-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> 部署 Mac 计算机的客户端证书  

> [!NOTE]  
>  Mac 计算机的客户端证书适用于 System Center Configuration Manager SP1 和更高版本。  

 此证书部署包含一个用于在证书颁发机构创建和颁发注册证书模板的单一过程。  

###  <a name="a-namebkmkmacclientcreatingissuinga-creating-and-issuing-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> 在证书颁发机构创建和颁发 Mac 客户端证书模板  
 本过程为 System Center Configuration Manager Mac 计算机创建自定义证书模板，并将该证书模板添加到证书颁发机构。  

> [!NOTE]  
>  本过程使用的证书模板不同于你可能已为 Windows 客户端计算机或分发点创建的证书模板。  
>   
>  通过为此证书创建新证书模板，你可以指定只有授权用户才能提出证书请求。  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>在证书颁发机构创建和颁发 Mac 客户端证书模板  

1.  创建一个安全组，以包含将使用 System Center Configuration Manager 在 Mac 计算机上注册证书的管理用户的用户帐户。  

2.  在运行“证书颁发机构”控制台的成员服务器上，右键单击“证书模板” ，然后单击“管理”  以加载“证书模板”管理控制台。  

3.  在结果窗格中，右键单击在“模板显示名称”  列中显示“经过身份验证的会话” 的条目，然后单击“复制模板” 。  

4.  在“复制模板”  对话框中，确保已选择“Windows 2003 Server，Enterprise Edition”  ，然后单击“确定” 。  

    > [!IMPORTANT]  
    >  不要选择“Windows 2008 Server，Enterprise Edition” 。  

5.  在  “新模板的属性”对话框中的“常规”  选项卡上，输入生成 Mac 客户端证书所需的模板名称，如 **ConfigMgr Mac 证书**。  

6.  单击“使用者名称”  选项卡，确保选中“用此 Active Directory 信息生成”  ，再为“使用者名称格式:”  选择“公用名”  ，然后从“将这个信息包括在另一个使用者名称中”  取消选择“用户主体名称(UPN)” 。  

7.  单击“安全”  选项卡，并从“域管理员”  和“企业管理员”  安全组中删除“注册”  权限。  

8.  单击“添加” ，指定你在步骤一中创建的安全组，然后单击“确定” 。  

9. 为此组选择“注册”  权限，并且不要清除“读取”  权限。  

10. 单击“确定”  ，然后关闭“证书模板控制台” 。  

11. 在证书颁发机构控制台中，右键单击“证书模板” ，单击“新建” ，然后单击“要颁发的证书模板” 。  

12. 在“启用证书模板”  对话框中，选择刚创建的新模板“ConfigMgr Mac 客户端证书” ，然后单击“确定” 。  

13. 如果不必创建和颁发任何其他证书，请关闭“证书颁发机构” 。  

 现在，在你为注册配置客户端设置时，可以选择 Mac 客户端证书模板。



<!--HONumber=Nov16_HO1-->


