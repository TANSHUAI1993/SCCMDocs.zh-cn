---
title: "设置云管理网关 | Microsoft Docs"
description: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 04/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
translationtype: Human Translation
ms.sourcegitcommit: 2bcc5d9dde1f1a2d9c33575d6c463e281ac818e8
ms.openlocfilehash: 61b8cd8458718b9a54edb129739c619f947ac380
ms.lasthandoff: 12/16/2016

---

# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>为 Configuration Manager 设置云管理网关

*适用范围：System Center Configuration Manager (Current Branch)*

从 1610 版开始，在 Configuration Manager 中设置云管理网关的过程包括以下步骤：

## <a name="step-1-create-a-custom-ssl-certificate"></a>步骤 1：创建自定义 SSL 证书

采用针对基于云的分发点的同一方法，为云管理网关创建自定义 SSL 证书。 按照[为基于云的分发点部署服务证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012)中的说明，但以不同方式执行以下操作：

-   在设置新证书模板时，向为 Configuration Manager 服务器设置的安全组提供**读取**和**注册**权限。

-  请求自定义 Web 服务器证书时，为以 **cloudapp.net** 结尾的证书公用名称提供 FQDN（以便在 Azure 公有云上使用云管理网关），或为以 **usgovcloudapp.net** 结尾的证书公用名词提供 FQDN（以便用于 Azure 政府云）。

## <a name="step-2-export-the-client-certificates-root"></a>步骤 2：导出客户端证书的根

导出网络上所用的客户端证书根的最简捷的方法就是打开已加入域且有客户端证书的一台计算机上的客户端证书并进行复制。

> [!NOTE] 
>
> 希望通过云管理网关管理的任何计算机以及托管云管理网关连接点的站点系统服务器都需要客户端证书。 如果需要将客户端证书添加到任何这类计算机上，请参阅[为 Windows 计算机部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012)。

1.  在“运行”窗口中，键入 **mmc**，然后按“Return”。

2.  在“文件”菜单中，选择“添加/删除管理单元...”。

3.  在“添加或删除管理单元”对话框中，选择“证书” > “添加 &gt;” > “计算机帐户” > “下一步” > “本地计算机” > “完成”。 

4.  转到“证书”&gt;“个人”&gt;“证书”。

5.  双击计算机上用于客户端身份验证的证书，选择“证书路径”选项卡，然后双击根颁发机构（位于路径顶部）。

6.  在“详细信息”选项卡上，选择“复制到文件...”。

7.  使用默认证书格式完成证书导出向导。 记下创建的根证书的名称和位置。 需要在[后面的步骤](#step-4-set-up-cloud-management-gateway)中使用它来配置云管理网关。

## <a name="step-3-upload-the-management-certificate-to-azure"></a>步骤 3：将管理证书上传到 Azure

Configuration Manager 需要 Azure 管理证书来访问 Azure API 和配置云管理网关。 有关如何上传管理证书的详细信息和说明，请参阅 Azure 文档中的以下文章：

- [Azure 云服务证书概述](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [上传 Azure 管理 API 管理证书](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>请确保复制与管理证书关联的订阅 ID。 在[下一步](#step-4-set-up-cloud-management-gateway)中需要使用此 ID 在 Configuration Manager 控制台中配置云管理网关。

### <a name="subordinate-ca-certificates-and-azure"></a>从属 CA 证书和 Azure

如果证书由从属 CA (subCA) 颁发，并且企业 PKI 基础结构不在 Internet 中，则使用此过程将证书上传到 Azure。 

1. 在 Azure 门户中设置云管理网关后，找到云管理网关服务并转到“证书”选项卡。 在此选项卡中上传 subCA 证书。 如果有多个 subCA 证书，则需要全部上传。 
2. 证书上传完成后，记录其指纹。 
3. 使用此脚本将指纹添加到站点数据库：
    
```

    DIM serviceCName
    DIM subCAThumbprints

    ' Verify arguments
    IF WScript.Arguments.Count <> 2 THEN
    WScript.StdOut.WriteLine "Usage: CScript UpdateSubCAThumbprints.vbs <ServiceCName> <SubCA cert thumbprints, separated by ;>"
    WScript.Quit 1
    END IF

    'Get arguments
    serviceCName = WScript.Arguments.Item(0)
    subCAThumbprints = WScript.Arguments.Item(1)

    'Find SMS Provider
    WScript.StdOut.WriteLine "Searching for SMS Provider for local site..."
    SET objSMSNamespace = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms")
    SET results = objSMSNamespace.ExecQuery("SELECT * From SMS_ProviderLocation WHERE ProviderForLocalSite = true")

    'Process the results
    FOR EACH var in results
    siteCode = var.SiteCode
    NEXT

    IF siteCode = "" THEN
    WScript.StdOut.WriteLine "Failed to locate SMS provider."
    WScript.Quit 1
    END IF

    WScript.StdOut.WriteLine "SiteCode = " & siteCode 

    ' Connect to the SMS namespace
    SET objWMIService = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms\site_" & siteCode)

    'Get instance of SMS_AzureService
    DIM query
    query = "SELECT * From SMS_AzureService WHERE ServiceType = 'CloudProxyService' AND ServiceCName = '" & serviceCName & "'"
    WScript.StdOut.WriteLine "Run WQL query: " &  query
    SET objInstances = objWMIService.ExecQuery(query)

    IF IsNull(objInstances) OR (objInstances.Count = 0) THEN
    WScript.StdOut.WriteLine "Failed to get Azure_Service instance."
    WScript.Quit 1
    END IF

    FOR EACH var IN objInstances
    SET azService = var
    NEXT

    WScript.StdOut.WriteLine "Update [SubCACertThumbprint] to " & subCAThumbprints

    'Update SubCA cert thumbprints
    azService.Properties_.item("SubCACertThumbprint") = subCAThumbprints

    'Save data back to provider
    azService.Put_

    WScript.StdOut.WriteLine "[SubCACertThumbprint] is updated successfully."
```


## <a name="step-4-set-up-cloud-management-gateway"></a>步骤 4：设置云管理网关

>[!NOTE]
>在 1610 版中，云管理网关是一项预发行功能。 若要启用此功能，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

1. 在 Configuration Manager 控制台中，转到“管理” > “云服务” > “云管理网关”。
2. 选择“创建云管理网关”。

3. 在“创建云管理网关”向导中，输入 Azure 订阅 ID（从 Azure 管理门户复制），然后浏览到作为 Azure 管理证书上传的证书文件。 选择“下一步”，然后等待一段时间以使控制台连接到 Azure。

4. 在向导中填写其他详细信息：

    - 指定将在 Azure 中运行的服务的名称。 服务名称必须是字母数字字符，且长度为 3-24 个字符。

    - 选择要在其中运行服务的 Azure 区域。

    - 指定要用于该服务的虚拟机数量。 默认值为 1，但服务最多可以运行 16 个虚拟机。

    >[!NOTE]
    >如果将 Internet 代理用于云管理网关连接点，需要根据使用的虚拟机数量增加代理上的端口数量，从端口 10124 开始。

    - 指定从自定义 SSL 证书中导出的私钥（.pfx 文件）。

    - 指定从客户端证书导出的根证书。

    -   指定创建新证书模板时使用的同一服务名称 FQDN。 必须根据使用的 Azure 云，为 FQDN 服务名称指定以下其中一种后缀：

    Azure 云 | FQDN 前缀
    --------------|-------------
    公有（商用）云 | .cloudapp.net    
    政府云 | .usgovcloudapp.net

  - 清除“验证客户端证书吊销”旁边的复选框（除非要公开发布 CRL 信息）。

  - 完成后选择“下一步”。

5. 如果想要通过 14 天阈值监视云管理网关通信，请选择打开阈值警报的复选框。 然后，指定阈值，以及引发不同警报级别所依据的百分比。 完成后选择“下一步”。

6. 检查设置，然后选择“下一步”。 Configuration Manager 开始设置服务。 关闭向导后，需花费 5 到 15 分钟时间在 Azure 中完整配置该服务。 检查新设置的云管理网关的“状态”，以确定服务是否已准备就绪。

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>步骤 5：配置客户端证书身份验证的主站点

1. 在 Configuration Manager 控制台中，转到“管理” > “站点配置” > “站点”。

2. 选择希望通过云管理网关管理的客户端的主站点，然后选择“属性”。

3. 在主站点属性表的“客户端计算机通信”选项卡上，选中“在可用时使用 PKI 客户端证书(客户端身份验证)”。

4. 请确保清除“客户端检查站点系统的证书吊销列表 (CRL)”。 仅当公开发布 CRL 时才需选择此选项。


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>步骤 6：添加云管理网关连接点

云管理网关连接点是一种用于与云管理网关进行通信的新站点系统角色。 若要添加云管理网关连接点，请按照[添加 System Center Configuration Manager 的站点系统角色](/sccm/core/servers/deploy/configure/add-site-system-roles)中的说明操作。

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>步骤 7：为云管理网关通信配置角色

设置云管理网关的最后一步是配置站点系统角色以接受云管理网关通信。 对于 Tech Preview 1606，云管理网关只支持管理点、分发点和软件更新点角色。 必须分别配置每个角色。

1. 在 Configuration Manager 控制台中，转到“管理” > “站点配置” > “服务器和站点系统角色”。

2. 选择要为云管理网关通信配置的角色的站点系统服务器。

3. 选择“角色”，然后选择“属性”。

4. 在角色属性表中的“客户端连接”下，选择“HTTPS”，选中“允许 Configuration Manager 云管理网关通信”旁边的复选框，然后选择“确定”。 为其余角色重复这些步骤。

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>步骤 8：配置云管理网关的客户端

在完整配置云管理网关和站点系统角色并进行运行之后，客户端将在下一位置请求中自动获取云管理网关服务的位置。 客户端必须位于公司网络，才能接收云管理网关服务的位置。 位置请求的轮询周期为 24 小时。 如果不想等待按正常计划执行的位置请求，可以通过重新启动计算机上的 SMS 代理主机服务 (ccmexec.exe) 强制执行该请求。

在客户端上配置云管理网关服务的位置后，它可自动确定是在 Intranet 还是 Internet 上。 如果客户端可以联系域控制器或本地管理点，该客户端会将其用于与 Configuration Manager 进行通信；否则，它会认为位于 Internet 上，并使用云管理网关的位置来进行通信。

>[!NOTE]
> 可以强制客户端始终使用云管理网关，不管它是位于 Intranet 还是 Internet 上。 若要执行该操作，请在客户端计算机上设置以下注册表项：\
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

若要验证客户端是否可以联系 Configuration Manager，可在客户端计算机上运行以下 PowerShell 命令：

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

此命令会显示客户端可以联系的管理点，包括云管理网关服务。

## <a name="next-steps"></a>后续步骤

[监视云管理网关的客户端](monitor-clients-cloud-management-gateway.md)

