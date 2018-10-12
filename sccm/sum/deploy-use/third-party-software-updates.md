---
title: 启用第三方更新
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中启用第三方更新
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbcf7a7d76146cc11dd4bb57b86fe4752c694e02
ms.sourcegitcommit: 1e782268d6c0211bd854b5860de72cfd6c6985c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "44697032"
---
# <a name="enable-third-party-updates"></a>启用第三方更新 

适用范围：System Center Configuration Manager 版本 1806

从版本 1806 开始，Configuration Manager 控制台中的“第三方软件更新目录”节点允许订阅第三方目录，将其更新发布到软件更新点 (SUP)，然后将它们部署到客户端。  <!--1357605, 1352101, 1358714-->



## <a name="prerequisites"></a>先决条件 
- 顶级软件更新点的 WSUSContent 文件夹上有足够的磁盘空间来存储第三方软件更新的源二进制内容。
    - 所需的存储空间根据供应商、更新类型和发布用于部署的特定更新而有所不同。
    - 如果需要将 WSUSContent 文件夹移到另一个具有更多可用空间的驱动器，请参阅 [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/)（如何更改 WSUS 在本地存储更新的位置）博客文章。
- 第三方软件更新同步服务需要 Internet 访问。
    - 要获取合作伙伴目录列表，需通过 HTTPS 端口 443 访问 download.microsoft.com。 
    -  对任何第三方目录和更新内容文件的 Internet 访问。 可能需要除 443 以外的其他端口。
    - 第三方更新使用与 SUP 相同的代理设置。

## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>SUP 远离顶级站点服务器时的其他要求 

1. 当 SUP 为远程时必须在 SUP 上启用 SSL。 这需要从内部证书颁发机构或通过公共提供程序生成的服务器身份验证证书。
    - [在 WSUS 上配置 SSL](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL)
        - 在 WSUS 上配置 SSL 时，请注意某些 Web 服务和虚拟目录始终是 HTTP 而不是 HTTPS。 
        - Configuration Manager 通过 HTTP 从 WSUS 内容目录下载软件更新包的第三方内容。   
    - [在 SUP 上配置 SSL](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. 将第三方更新 WSUS 签名证书配置设置为软件更新点组件属性中的 Configuration Manager 管理更新时，需要以下配置才能创建自签名 WSUS 签名证书： 
   - 应在 SUP 服务器上启用远程注册表。
   -  WSUS 服务器连接帐户应具有 SUP/WSUS 服务器上的远程注册表权限。 


3. 在 Configuration Manager 站点服务器上创建以下注册表项： 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`，创建名为 EnableSelfSignedCertificates 的新 DWORD，其值为 `1`。 

4. 在远程 SUP 服务器上向受信任的发布者和受信任的根存储安装自签名 WSUS 签名证书：
   - WSUS 服务器连接帐户应具有 SUP 服务器上的远程管理权限。

    如果无法使用此项，请将证书从本地计算机的 WSUS 存储导出到受信任的发布者和受信任的根存储中。 

> [!NOTE] 
>可以通过查看 SUP 的站点系统角色属性上的“代理和帐户设置”选项卡来识别 WSUS 服务器连接帐户。 如果未指定帐户，则使用站点服务器的计算机帐户。

## <a name="enable-third-party-updates-on-the-sup"></a>在 SUP 上启用第三方更新
如果启用此选项，则可以在 Configuration Manager 控制台中订阅第三方更新目录。 然后，可以将这些更新发布到 WSUS 并将它们部署到客户端。 每个层次结构应运行一次以下步骤，以启用和设置要使用的功能。 如果曾经替换过顶级 SUP 的 WSUS 服务器，则可能需要重新运行这些步骤。 

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“站点配置”，然后选择“站点”节点。
2. 选择层次结构中的顶层站点。 在功能区中，单击“配置站点组件”，然后选择“软件更新点”。
3. 切换到“第三方更新”选项卡。选择“启用第三方软件更新”选项。

    ![第三方更新 SUP 属性屏幕截图](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>配置 WSUS 签名证书
需要决定是希望 Configuration Manager 使用自签名证书自动管理第三方 WSUS 签名证书，还是需要手动配置证书。 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>自动管理 WSUS 签名证书
如果不要求使用 PKI 证书，可以选择自动管理第三方更新的签名证书。 WSUS 证书管理是作为同步周期的一部分进行的，并记录在 `wsyncmgr.log` 中。 

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“站点配置”，然后选择“站点”节点。
2. 选择层次结构中的顶层站点。 在功能区中，单击“配置站点组件”，然后选择“软件更新点”。
3. 切换到“第三方更新”选项卡。选择“由 Configuration Manager 管理证书”选项。 
4. 在“管理”工作区中“安全”下的“证书”节点中会创建一个“第三方 WSUS 签名”类型的新证书。  

### <a name="manually-manage-the-wsus-signing-certificate"></a>手动管理 WSUS 签名证书
如果需要手动配置证书（例如需要使用 PKI 证书），则需要使用 [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) 或其他工具来执行此操作。  

1. 使用 [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) 配置签名证书。
2. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“站点配置”，然后选择“站点”节点。
3. 选择层次结构中的顶层站点。 在功能区中，单击“配置站点组件”，然后选择“软件更新点”。
4. 切换到“第三方更新”选项卡。选择“手动管理证书”选项。


## <a name="enable-third-party-updates-on-the-clients"></a>在客户端上启用第三方更新
在客户端设置中启用客户端上的第三方更新。 该设置会设置[允许 Intranet Microsoft 更新服务位置的签名更新](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#BKMK_comp3)的 Windows 更新代理策略。 此客户端设置还会将 WSUS 签名证书安装到客户端上受信任的发布者存储中。 证书管理日志记录可在客户端上的 `updatesdeployment.log` 中查看。  对要用于第三方更新的每个自定义客户端设置运行这些步骤。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#Enable-third-party-software-updates)一文。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，然后选择“客户端设置”节点。
2. 选择现有的自定义客户端设置或创建新的客户端设置。 
3. 选择左侧的“软件更新”选项卡。 如果没有此选项卡，请确保已启用“软件更新”框。
4. 将“启用第三方软件更新”设置为“是”。 


## <a name="add-a-custom-catalog"></a>添加自定义目录
合作伙伴目录是已向 Microsoft 注册其信息的软件供应商目录。 可以通过合作伙伴目录订阅它们，而无需指定任何其他信息。 添加的目录称为自定义目录。 可以将来自第三方更新供应商的自定义目录添加到 Configuration Manager。 自定义目录必须使用 https，并且更新必须以数字方式签名。 

1. 转到“软件更新库”工作区，展开“软件更新”，然后选择“第三方软件更新目录”节点。 
   
     ![第三方更新节点屏幕截图](media/third-party-updates-node.PNG)
2. 单击功能区中的“添加自定义目录”。 

     ![第三方更新添加自定义目录](media/third-party-updates-custom-catalog.png)
1. 在“常规”页面上，指定以下各项： 
    - **下载 URL**：自定义目录的有效的 HTTPS 地址。
    - **发行商**：发布目录的组织的名称。 
    - **名称**：要在 Configuration Manager 控制台中显示的目录的名称。 
    - **描述**：目录描述。 
    - **支持 URL**（可选）：用于获取目录相关帮助的网站的有效 HTTPS 地址。 
    - **支持联系人**（可选）：用于获取目录相关帮助的联系人信息。 
2. 单击“下一步”以查看目录摘要，并继续完成“第三方软件更新自定义目录向导”。


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>订阅第三方目录并同步更新
在 Configuration Manager 控制台中订阅第三方目录时，目录中每个更新的元数据都会同步到 SUP 的 WSUS 服务器中。 元数据的同步使客户端能够确定是否有任何更新适用。 对要订阅的每个第三方目录执行以下步骤：  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区。 展开“软件更新”，然后选择“第三方软件更新目录”节点。  
2. 选择要订阅的目录，然后单击功能区中的“订阅目录”。 
    ![第三方更新添加自定义目录](media/third-party-updates-subscribe.png)
1. 查看并批准目录证书。  
    >[!NOTE]
    
    > 当订阅第三方软件更新目录时，将你在向导中查看并批准的证书添加到站点。 此证书的类型是“第三方软件更新目录”。 可以从“管理”工作区中“安全”下的“证书”节点管理它。  
2. 完成向导。 初始订阅后，目录应该会在几分钟内开始下载。 
    - 目录每 7 天自动同步一次。
    - 单击功能区中的“立即同步”以强制同步。
3. 下载目录后，需要将产品元数据从 WSUS 数据库同步到 Configuration Manager 数据库。 [手动启动软件更新同步](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization)以同步产品信息。
4. 同步产品信息后，[配置 SUP 以将所需产品同步](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize)到 Configuration Manager 中。  
5. [手动启动软件更新同步](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization)，以将新产品的更新同步到 Configuration Manager 中。  
6. 同步完成后，可以在“所有更新”节点中查看第三方更新。 这些更新将作为“仅元数据”更新发布，直到选择发布它们为止。 
     - 带有蓝色箭头的图标表示仅元数据软件更新。 ![“仅元数据软件更新”图标](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>发布和部署第三方软件更新 
第三方更新在“所有更新”节点中后，可以选择应发布哪些更新以进行部署。 发布更新时，二进制文件将从供应商处下载并置于顶级 SUP 上的 WSUSContent 目录中。 

1. 在 Configuration Manager 控制台中，转到“软件库”工作区。 展开“软件更新”，然后选择“所有软件更新”节点。
2. 单击“添加条件”以筛选更新列表。 例如，为 HP 添加供应商。 查看 HP 的所有更新。  
3. 选择组织所需的更新。 单击“发布第三方软件更新内容”。
    - 此操作将从供应商处下载更新二进制文件，然后将它们存储在顶级软件更新点上的 WSUSContent 文件夹中。 
4. [手动启动软件更新同步](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization)，以将已发布更新的状态从仅元数据更改为包含内容的可部署更新。 
    >[!NOTE]
    >当发布第三方软件更新内容时，用于对内容进行签名的任何证书都将添加到该站点。 这些证书的类型都是“第三方软件更新内容”。 可以从“管理”工作区中“安全”下的“证书”节点管理它们。  

5. 在 SMS_ISVUPDATES_SYNCAGENT.log 中查看进度。 该日志位于站点系统“日志”文件夹中的顶级软件更新点上。
6. 使用[部署软件更新](../deploy-use/deploy-software-updates.md)过程部署更新。 
7. 在部署软件更新向导的“下载位置”页上，选择默认选项以“从 Internet 下载软件更新”。 在本方案中，内容已发布到软件更新点，用于下载部署包的内容。
8. 客户端需要先运行扫描并评估更新，然后才能看到符合性结果。  可以通过运行“软件更新扫描周期”，从客户端上的 Configuration Manager 控制面板手动触发此周期。


## <a name="monitoring-progress-of-third-party-software-updates"></a>监视第三方软件更新的进度 

第三方软件更新的同步由顶级默认软件更新点上的 SMS_ISVUPDATES_SYNCAGENT 组件处理。 可以通过此组件查看状态消息，也可以在 SMS_ISVUPDATES_SYNCAGENT.log 中查看更详细的状态。 此日志位于站点系统“日志”文件夹中的顶级软件更新点上。 此路径默认为 C:\Program Files\Microsoft Configuration Manager\Logs。 有关监视常规软件更新管理进程的详细信息，请参阅[监视软件更新](../deploy-use/monitor-software-updates.md) 

## <a name="known-issues"></a>已知问题

- 运行控制台的计算机用于从 WSUS 下载更新并将其添加到更新包。 WSUS 签名证书必须在控制台计算机上受到信任。 如果不是，则可能会在第三方更新的下载过程中出现签名检查问题。 
- 第三方软件更新同步服务无法将内容发布到由其他应用程序、工具或脚本（如 SCUP）添加到 WSUS 中的仅元数据更新。 “发布第三方软件更新内容”操作对于这些更新均失败。 如果需要部署此功能尚不支持的第三方更新，请充分使用现有的进程来部署这些更新。  
-  Configuration Manager 具有目录 cab 文件格式的新版本。 新版本包含供应商二进制文件的证书。 批准并信任目录后，这些证书会添加到“管理”工作区中“安全”下的“证书”节点中。  
     - 只要下载 URL 为 https 且更新已签名，便仍然可以使用旧的目录 cab 文件版本。 由于二进制文件的证书不在 cab 文件中且还未获批准，因此内容将无法发布。 可以通过在“证书”节点中查找证书，取消阻止它，然后再次发布更新来解决此问题。 如果要发布使用不同证书签名的多个更新，需要取消阻止所使用的每个证书。
     - 有关详细信息，请参阅以下状态消息表中的状态消息 11523 和 11524。
-  当顶级软件更新点上的第三方软件更新同步服务要求使用代理服务器进行 Internet 访问时，数字签名检查可能会失败。 若要缓解此问题，请在站点系统上配置 WinHTTP 代理设置。 有关详细信息，请参阅 [WinHTTP 的 Netsh 命令](https://go.microsoft.com/fwlink/p/?linkid=199086)。

## <a name="status-messages"></a>状态消息

| 消息 ID       | 严重性           | 说明 | 可能的原因| 可能的解决方案
| ------------- |-------------| -----|----|----|
| 11516     | 错误 |未能发布更新“更新 ID”的内容，因为内容未签名。  只能发布含有效签名的内容。  |Configuration Manager 不允许发布未签名的更新。| 以其他方式发布更新。 </br></br>查看供应商是否有可用的已签名更新。|
| 11523  | 警告 |  目录“X”不包括内容签名证书，在添加和批准内容签名证书之前，尝试从此目录发布更新的更新内容可能会失败。 | 导入使用较旧版本的 cab 文件格式的目录时，可能会出现此消息。|联系目录提供程序以获取包含内容签名证书的已更新目录。 </br> </br> 二进制文件的证书未包含在 cab 文件中，因此内容将无法发布。 可以通过在“证书”节点中查找证书，取消阻止它，然后再次发布更新来解决此问题。 如果要发布使用不同证书签名的多个更新，需要取消阻止所使用的每个证书。|
| 11524| 错误  | 由于缺少更新元数据，因此未能发布更新“ID”。 | 此更新可能已经在 Configuration Manager 外同步到 WSUS。| 在尝试发布更新内容之前，请将更新与 Configuration Manager 同步。  </br> </br>如果使用了外部工具将更新作为“仅元数据”发布，则使用相同的工具发布更新内容。|



## <a name="working-with-third-party-updates-video"></a>使用第三方更新视频
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>下一步
> [!div class="nextstepaction"]
> [部署软件更新](./deploy-software-updates.md)
