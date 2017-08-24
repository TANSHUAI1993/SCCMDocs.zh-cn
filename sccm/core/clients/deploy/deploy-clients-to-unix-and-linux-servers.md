---
title: "部署 UNIX/Linux 客户端 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中将客户端部署到 UNIX 或 Linux 服务器。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d61d53daa5ef3d9c986cba8791d4471fea94d29d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中如何将客户端部署到 UNIX 和 Linux 服务器

*适用范围：System Center Configuration Manager (Current Branch)*

在可以用 System Center Configuration Manager 管理 Linux 或 UNIX 服务器之前，你必须在每个 Linux 或 UNIX 服务器上安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端。 可以在每台计算机上手动完成客户端安装，或远程使用安装客户端的 shell 脚本。 Configuration Manager 不支持对 Linux 或 UNIX 服务器使用客户端请求安装。 （可选）你可以为 System Center orchestrator 配置 Runbook 来自动执行 Linux 或 UNIX 服务器上的客户端安装。  

 无论你使用何种安装方法，在安装过程要求使用名为 **install** 的脚本来管理安装过程。 此脚本时，包含您下载适用于 Linux 和 UNIX 的客户端。  

 安装脚本 Configuration Manager 适用于 Linux 和 UNIX 的客户端支持的命令行属性。 某些命令行属性是必需的其他一些是可选。 例如，在安装客户端时，您必须指定由其与该站点的初始联系 Linux 或 UNIX 服务器的站点中的管理点。 有关命令行属性的完整列表，请参阅 [在 Linux 和 UNIX 服务器上安装客户端的命令行属性](#BKMK_CmdLineInstallLnUClient)。  

 安装客户端后，在 Configuration Manager 控制台指定客户端设置，从而用和配置基于 Windows 的客户端相同的方式配置客户端代理。 有关详细信息，请参阅  [Client settings for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU)。  

##  <a name="BKMK_AboutInstallPackages"></a> 有关客户端安装包和通用代理  
 若要在特定平台上安装适用于 Linux 和 UNIX 的客户端，你必须对要安装客户端的计算机使用合适的客户端安装包。 合适的客户端安装包是从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=525184)下载的每个客户端的一部分。 除了客户端安装包，客户端下载内容还包括在每台计算机上管理客户端安装的 **install** 脚本。  

 在安装客户端时，可以使用相同的过程和命令行属性而不考虑您使用的客户端安装包。  

 有关适用于 Linux 和 UNIX 的每个版本的 Configuration Manager 客户端支持的操作系统、平台和客户端安装包的详细信息，请参阅 [Linux 和 UNIX 服务器](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers)。  

##  <a name="BKMK_InstallLnUClient"></a> 在 Linux 和 UNIX 服务器上安装客户端  
 若要安装适用于 Linux 和 UNIX 的客户端，请在每个 Linux 或 UNIX 的计算机上运行脚本。 该脚本命名为 **安装** ，同时支持命令行属性，修改安装行为和引用客户端安装包。 安装脚本和客户端安装包必须位于客户端上。 客户端安装程序包中包含针对特定 Linux 或 UNIX 的操作系统和平台的 Configuration Manager 客户端文件。
每个客户端安装包包含所有必需的文件以完成客户端安装并与不同的是基于 Windows 的计算机，不会下载其他文件从管理点或其他源位置。  

 安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端后，你不需要重新启动计算机。 一旦软件安装完成后，客户端所操作。 如果重新启动计算机，Configuration Manager 客户端将自动重新启动。  

 使用根凭据运行安装的客户端。 要求根凭据收集硬件清单信息并执行软件部署。  

 以下为命令格式：  

 **./install -mp &lt;computer\> -sitecode &lt;sitecode\> &lt;property #1> &lt;property #2> &lt;client installation package\>**  

-   **安装** 安装适用于 Linux 和 UNIX 的客户端的脚本文件的名称。 此文件提供的客户端软件。  

-   **-mp &lt;computer** 指定客户端使用的初始管理点。  

     示例：smsmp.contoso.com  

-   **-sitecode &lt;site code\>** 指定将客户端分配到的站点的站点代码。  

     示例：S01  

-   &lt;property #1> &lt;property #2> 指定要与安装脚本搭配使用的命令行属性。  

    > [!NOTE]  
    >  有关详细信息，请参阅 [在 Linux 和 UNIX 服务器上安装客户端的命令行属性](#BKMK_CmdLineInstallLnUClient)  

-   **客户端安装包** 是此计算机的操作系统、版本和 CPU 体系结构的客户端安装 .tar 包的名称。 必须最后指定客户端安装.tar 文件。  

     示例：ccm-Universal-x64.&lt;build\>.tar  

###  <a name="BKMK_ToInstallLnUClinent"></a> 若要在 Linux 和 UNIX 服务器上安装 Configuration Manager 客户端  

1.  在 Windows 计算机上，为你想要管理的 [Linux 或 UNIX 服务器下载合适的客户端文件](http://go.microsoft.com/fwlink/?LinkID=525184) 。  

2.  在 Window 计算机上运行自解压 .exe 文件以提取安装脚本和客户端安装 .tar 文件。  

3.  复制 **安装** 脚本和 .tar 文件到你想要管理的服务器上的文件夹。  

4.  在 UNIX 或 Linux 服务器上，运行以下命令以启用要作为程序运行的脚本： **chmod +x install**  

    > [!IMPORTANT]  
    >  您必须使用根凭据来安装客户端。  

5.  接下来，运行以下命令以安装 Configuration Manager 客户端：**./install -mp &lt;hostname\> -sitecode &lt;code\> ccm-Universal-x64.&lt;build\>.tar**  

     当进入此命令时，使用您所需要的其他命令行属性。  有关命令行属性的列表，请参阅 [在 Linux 和 UNIX 服务器上安装客户端的命令行属性](#BKMK_CmdLineInstallLnUClient)  

6.  脚本运行后，通过查看“/var/opt/microsoft/scxcm.log”  文件验证安装 。 此外，可以通过在 Configuration Manager 控制台中“资产和符合性”工作区的“设备”节点中查看客户端的详细信息，确认客户端是否已安装并与站点通信。  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> 在 Linux 和 UNIX 服务器上安装客户端的命令行属性  
 以下属性可用于修改安装脚本的行为：  

> [!NOTE]  
>  使用属性 **-h** 要显示此列表的受支持的属性。  

-   **-mp &lt;server FQDN\>**  

     必须的。 指定通过 FQDN，客户端将用作初始联系点的管理点服务器。  

    > [!IMPORTANT]  
    >  此属性不会指定安装后为其分配客户端的管理点。  

    > [!NOTE]  
    >  当你使用 **-mp** 属性来指定配置为只接受 HTTPS 客户端连接的管理点时，还必须使用 **-UsePKICert** 属性。  

-   **-sitecode &lt;sitecode\>**  

     必须的。 指定要将 Configuration Manager 客户端分配到的 Configuration Manager 主站点。  

     示例：-sitecode S01  

-   **-fsp &lt;server_FQDN>**  

     可选。 指定通过 FQDN，客户端用于提交状态消息的回退状态点服务器。  

     有关回退状态点的详细信息，请参阅 [Determine Whether You Require a Fallback Status Point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point) 。  


-   **-dir &lt;directory\>**  

     可选。 指定替代位置以安装 Configuration Manager 客户端文件。  

     默认情况下，在客户端安装到以下位置： **/opt/microsoft**。  

-   **-nostart**  

     可选。 客户端安装完成后，阻止自动启动 Configuration Manager 客户端服务 **ccmexec.bin**。  

     在客户端安装后，您必须手动启动客户端服务。  

     默认情况下，客户端服务启动后客户端安装完成后，每次在计算机重新启动。  

-   **-清理**  

     可选。 在新的安装开始之前指定适用于 Linux 和 UNIX 的所有客户端文件和来自以前安装的客户端数据删除。 这会删除客户端的数据库和证书存储。  

-   **-keepdb**  

     可选。 指定本地客户端数据库保留，并重复使用时重新安装客户端。 默认情况下，当你重新安装客户端将删除此数据库。  

-   **-UsePKICert &lt;parameter\>**  

     可选。 公钥证书标准 (PKCS #12) 格式指定完整路径和文件名为 X.509 PKI 证书的名称。 此证书用于客户端身份验证。 如果在安装过程中未指定证书，则你需要添加或更改证书，请使用 **certutil** 实用工具。 有关 certutil 的信息，请参阅 [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) 。  

     当您使用 **-UsePKICert**, ，还必须提供通过使用与 PKCS #12 文件相关联的密码 **-certpw** 命令行参数。  

     如果不使用此属性可指定 PKI 证书，客户端使用自签名的证书和与站点系统的所有通讯都是通过 HTTP。  

     如果您在上指定了无效的证书客户端安装命令行，会返回任何错误。 这是因为客户端安装后会发生的证书验证。 如果客户端启动，证书的验证与管理点并且如果验证失败的证书中将显示以下消息 **scxcm.log**, ，Unix 和 Linux Configuration Manager 客户端的日志文件： **失败验证管理点证书**。 默认的日志文件位置是：  **/var/opt/microsoft/scxcm.log**。  

    > [!NOTE]  
    >  安装客户端时，必须指定此属性并使用 **-mp** 属性指定配置为仅接受 HTTPS 客户端连接的管理点。  

     示例：-UsePKICert &lt;Full path and filename\> -certpw &lt;password\>  

-   **-certpw &lt;parameter\>**  

     可选。 指定通过使用与您指定的 PKCS #12 文件相关联的密码 **-UsePKICert** 属性。  

     示例：-UsePKICert &lt;Full path and filename\> -certpw &lt;password\>  

-   **-NoCRLCheck**  

     可选。 指定客户端应通过使用 PKI 证书通过 HTTPS 通信时检查证书吊销列表 (CRL)。 如果未指定此选项，客户端在通过使用 PKI 证书建立 HTTPS 连接前检查 CRL。 有关客户端 CRL 检查的详细信息，请参阅 PKI 证书吊销的规划。  

     示例：-UsePKICert &lt;Full path and filename\> -certpw &lt;password\> -NoCRLCheck  

-   **-rootkeypath &lt;file location\>**  

     可选。 指定 Configuration Manager 受信任的根密钥的完整路径和文件名。 Configuration Manager 受信任的根密钥提供一种机制，Linux 和 UNIX 客户端使用此机制来确认它们已连接到属于正确的层次结构的站点系统。  

     如果未在命令行上指定受信任的根密钥，客户端将信任其与之通信的第一个管理点，并将从该管理点自动检索受信任的根密钥。  

     有关详细信息，请参阅  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

     示例：-rootkeypath &lt;Full path and filename\>  

-   **-httpport &lt;port\>**  

     可选。 指定在客户端在通过 HTTP 与管理点通信时所使用的管理点配置的端口。 如果未指定端口，使用默认值为 80。  

     示例：-httpport 80  

-   **-httpsport &lt;port\>**  

     可选。 指定在客户端在通过 HTTPS 与管理点通信时所使用的管理点配置的端口。 如果未指定端口，使用默认值 443。  

     示例：-UsePKICert &lt;Full path and certificate name\> -httpsport 443  

-   **-ignoreSHA256validation**  

     可选。 指定客户端安装将 SHA 256 验证跳过。 在操作系统上安装客户端时使用此选项，该操作系统未使用支持 SHA-256 的 OpenSSL 版本发布。 有关详细信息，请参阅 [About Linux and UNIX Operating Systems That do not Support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256)。  

-   **-signcertpath &lt;file location\>**  

     可选。 指定的完整路径和 **.cer** 的站点服务器上的导出自签名证书的文件名。 如果 PKI 证书不可用，Configuration Manager 站点服务器自动生成自签名的证书。  

     这些证书用于验证从管理点下载的客户端策略发送从预期的站点。 如果在安装过程中未指定证书，或者你需要更改证书，请使用 **certutil** 实用工具。 有关 certutil 的信息，请参阅 [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) 。  

     此证书可通过 **SMS** 证书存储检索，并且具有“站点服务器”  使用者名称以及“站点服务器签名证书” 友好名称。  

     如果在安装过程中未指定此选项，Linux 和 UNIX 的客户端将信任它们与通信并将自动检索来自该管理点签名证书的第一个管理点。  

     示例：-signcertpath &lt;Full path and file name\>  

-   **-rootcerts**  

     可选。 指定其他 PKI 证书导入不是管理点证书颁发机构 (CA) 层次结构的一部分。 如果在命令行中指定多个证书，它们应该是以逗号分隔。  

     如果您使用未链接至您的站点管理点信任的根 CA 证书的 PKI 客户端证书，使用此选项。 如果客户端证书未链接到站点的证书颁发者列表中的受信任的根证书，管理点将拒绝此客户端。  

     如果不使用此选项，Linux 和 UNIX 的客户端将验证使用的证书中的信任层次结构 **-UsePKICert** 选项。  

     示例：-rootcerts &lt;Full path and file name\>,&lt;Full path and file name\>  

###  <a name="BKMK_UninstallLnUClient"></a> 从 Linux 和 UNIX 服务器上卸载客户端  
 若要卸载适用于 Linux 和 UNIX 的 Configuration Manager 客户端，请使用卸载实用工具 **uninstall**。 默认情况下，此文件位于 **/选择/microsoft/configmgr/bin/** 客户端计算机上的文件夹。 这将卸载命令不支持任何命令行参数，并且将删除所有从服务器向客户端软件相关的文件。  

 若要卸载客户端，请使用下面的命令行: **/opt/microsoft/configmgr/bin/uninstall**  

 安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端后，你不需要重新启动计算机。  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> 适用于 Linux 和 UNIX 客户端配置请求端口  
 与基于 Windows 的客户端类似，适用于 Linux 和 UNIX 的 Configuration Manager 客户端使用 HTTP 和 HTTPS 与 Configuration Manager 站点系统通信。 Configuration Manager 客户端用于通信的端口称为请求端口。  

 当你安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端时，你可以通过指定 **-httpport** 和 **-httpsport** 安装属性更改客户端默认请求端口 。 当未指定的安装属性和自定义的值时，客户端将使用默认值。 默认值为 **80** 对于 HTTP 流量和 **443** HTTPS 通信。  

 安装客户端后，不能更改其请求端口配置。 相反，若要更改端口配置必须重新安装客户端并指定新的端口配置。 当你重新安装客户端以更改请求端口号时，运行 **安装** 命令类似于新的客户端安装，但使用的其他命令行属性 **-keepdb**。 此开关将指示要保留的客户端数据库和文件包括客户端 GUID 和证书存储区的安装。  

 有关客户端通信端口号的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端通信端口](../../../core/clients/deploy/configure-client-communication-ports.md)。  

##  <a name="BKMK_ConfigClientMP"></a> 配置客户端适用于 Linux 和 UNIX 来查找管理点  
 在安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端时，必须指定用作初始联系点的管理点。  

 适用于 Linux 和 UNIX 的 Configuration Manager 客户端将在客户端安装时联系此管理点。 如果客户端无法联系管理点，客户端软件将不断重试直到成功。  

 有关客户端如何查找管理点的详细信息，请参阅 [Locating Management Points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points)。
