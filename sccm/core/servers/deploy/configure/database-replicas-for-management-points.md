---
title: "管理点数据库副本 | Microsoft Docs"
description: "使用数据库副本可减少管理点对站点数据库服务器施加的 CPU 负载。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 130c053c9f2a1817dd85b1f3c01285aab19d59cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="database-replicas-for-management-points-for-system-center-configuration-manager"></a>System Center Configuration Manager 管理点的数据库副本

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 主站点可以使用数据库副本来减少管理点在处理来自客户端的请求时对站点数据库服务器施加的 CPU 负载。  

-   当管理点使用数据库副本时，此管理点会从承载数据库副本的 SQL Server 计算机中请求数据，而不是从站点数据库服务器中请求。  

-   这有助于通过卸载与客户端相关的频繁处理任务来减少站点数据库服务器上的 CPU 处理要求。  客户端的频繁处理任务的示例包括其中存在大量客户端的站点，这些站点频繁请求客户端策略  


##  <a name="bkmk_Prepare"></a> 准备使用数据库副本  
**关于管理点的数据库副本：**  

-   副本是指站点数据库的部分复制，该站点数据库复制到独立的 SQL Server 实例：  

    -   主站点支持站点上的每个管理点的专用数据库副本（辅助站点不支持数据库副本）  

    -   单个数据库副本可用于同一站点的多个管理点  

    -   只要每个数据库副本在独立的 SQL Server 实例中运行，SQL Server 即可承载多个副本以供不同管理点使用  

-   副本按固定计划，从站点数据库服务器以此目的发布的数据中同步站点数据库的副本。  

-   管理点可配置为在安装此管理点时使用副本，或随后通过重新配置先前安装的管理点以使用数据库副本  

-   定期监视站点数据库服务器和各个数据库副本服务器，以确保这两者间发生复制操作，并确保数据库副本服务器的性能足以满足所需的站点和客户端性能  

**数据库副本的先决条件：**  

-   **SQL Server 要求：**  

    -   承载数据库副本的 SQL Server 必须满足与站点数据库服务器相同的要求。 但只要副本服务器运行受支持的 SQL Server 版本，就无需运行与站点数据库服务器相同版本的 SQL Server。 有关信息，请参阅[对 System Center Configuration Manager 的 SQL Server 版本的支持](../../../../core/plan-design/configs/support-for-sql-server-versions.md)  

    -   承载副本数据库的计算机上的 SQL Server 服务必须以 **系统** 帐户形式运行。  

    -   承载站点数据库和承载数据库副本的这两个 SQL Server 均必须安装有“SQL Server 复制”  。  

    -   站点数据库必须 **发布** 数据库副本，且每个远程数据库副本服务器必须 **订阅** 已发布的数据。  

    -   承载站点数据库和承载数据库副本的这两个 SQL Server 均必须配置为支持 2 GB 的“最大文本替换大小”  。 有关如何为 SQL Server 2012 配置此项的示例，请参阅 [Configure the max text repl size Server Configuration Option（配置最大文本替换大小服务器配置选项）](http://go.microsoft.com/fwlink/p/?LinkId=273960)。  

-   **自签名证书：** 若要配置数据库副本，必须在数据库副本服务器上创建自签名证书，并将此证书提供给将使用该数据库副本服务器的每个管理点。  

    -   证书会自动提供给数据库副本服务器上安装的管理点。  

    -   若要将此证书提供给远程管理点，则必须导出证书，然后将其添加到远程管理点上的 **受信任人** 证书存储中。  

-   **客户端通知：** 若要支持包含管理点数据库副本的客户端通知，你必须针对 **SQL Server Service Broker**配置站点数据库服务器和数据库副本服务器之间的通信。 这要求：  

    -   使用其他数据库的相关信息配置每个数据库  

    -   在两个数据库间交换证书以确保安全通信  

**使用数据库副本时的限制：**  

-   当站点配置为发布数据库副本时，应使用以下过程代替常规指导：  

    -   [卸载发布数据库副本的站点服务器](#BKMK_DBReplicaOps_Uninstall)  

    -   [移动发布数据库副本的站点服务器数据库](#BKMK_DBReplicaOps_Move)  

-   **升级到 System Center Configuration Manager**：将站点从 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager 之前，必须对管理点禁用数据库副本。  站点升级之后，可以为管理点重新配置数据库副本。  

-   **单个 SQL Server 上的多个副本：**如果将数据库副本服务器配置为承载管理点的多个数据库副本（每个副本必须位于单独的实例上），则必须使用修改后的配置脚本（从下一节的第 4 步开始）来防止此服务器上先前配置的数据库副本覆盖当前使用的自签名证书。  

##  <a name="BKMK_DBReplica_Config"></a> 配置数据库副本  
若要配置数据库副本，需要以下步骤：  

-   [第 1 步 - 配置站点数据库服务器以发布数据库副本](#BKMK_DBReplica_ConfigSiteDB)  

-   [第 2 步 – 配置数据库副本服务器](#BKMK_DBReplica_ConfigSrv)  

-   [第 3 步 - 将管理点配置为使用数据库副本](#BKMK_DBReplica_ConfigMP)  

-   [第 4 步 - 配置数据库副本服务器的自签名证书](#BKMK_DBReplica_Cert)  

-   [第 5 步 - 为数据库副本服务器配置 SQL Server Service Broker](#BKMK_DBreplica_SSB)  

###  <a name="BKMK_DBReplica_ConfigSiteDB"></a> 第 1 步 - 配置站点数据库服务器以发布数据库副本  
 使用下列过程作为示例，了解如何在 Windows Server 2008 R2 计算机上将站点数据库服务器配置为发布数据库副本。 如果具有不同的操作系统版本，请参阅操作系统文档，并根据需要调整此过程中的步骤。  

##### <a name="to-configure-the-site-database-server"></a>配置站点数据库服务器  

1.  在站点数据库服务器上，将 SQL Server 代理设置为自动启动。  

2.  在站点数据库服务器上，用 **ConfigMgr_MPReplicaAccess**名称创建本地用户组。 必须将要在此站点使用的每个数据库副本服务器的计算机帐户添加到此组中，以使那些数据库副本服务器能够与发布的数据库副本同步。  

3.  在站点数据库服务器上，配置名为 **ConfigMgr_MPReplica**的文件共享。  

4.  将以下权限添加到“ConfigMgr_MPReplica”  共享中：  

    > [!NOTE]  
    >  如果 SQL Server 代理使用的帐户不是本地系统帐户，请将“系统”替换为以下列表中的该帐户名称。  

    -   **共享权限**：  

        -   系统： **写**  

        -   ConfigMgr_MPReplicaAccess： **读取**  

    -   **NTFS 权限**：  

        -   系统： **完全控制**  

        -   ConfigMgr_MPReplicaAccess：“读取”、“读取和执行”、“列表文件夹内容”  

5.  使用“SQL Server Management Studio”  连接到站点数据库，并以查询形式运行以下存储过程： **spCreateMPReplicaPublication**  

当存储过程完成后，站点数据库服务器被配置为发布数据库副本。  

###  <a name="BKMK_DBReplica_ConfigSrv"></a> 第 2 步 – 配置数据库副本服务器  
数据库副本服务器是运行 SQL Server 的计算机，它承载了站点数据库副本以供管理点使用。 数据库副本服务器按照固定计划将其数据库副本与站点数据库服务器发布的数据库副本同步。  

数据库副本服务器必须满足站点数据库服务器应满足的要求。 但是，数据库副本服务器运行的 SQL Server 版本可以与站点数据库服务器使用的版本不同。 有关支持的 SQL Server 版本的信息，请参阅[对 System Center Configuration Manager 的 SQL Server 版本的支持](../../../../core/plan-design/configs/support-for-sql-server-versions.md)主题。  

> [!IMPORTANT]  
>  承载副本数据库的计算机上的 SQL Server 服务必须以系统帐户形式运行。  

使用下列过程作为示例，了解如何在 Windows Server 2008 R2 计算机上配置数据库副本服务器。 如果具有不同的操作系统版本，请参阅操作系统文档，并根据需要调整此过程中的步骤。  

##### <a name="to-configure-the-database-replica-server"></a>配置数据库副本服务器  

1.  在数据库副本服务器上，将 SQL Server 代理设置为自动启动。  

2.  在数据库副本服务器上，使用“SQL Server Management Studio”  连接到本地服务器，浏览到“复制”  文件夹，单击“本地订阅”，并选择“新建订阅”  以启动“新建订阅向导” ：  

    1.  在“发布”  页上的“发布者”  列表框中，选择“查找 SQL Server 发布者” ，输入站点数据库服务器的名称，然后单击“连接” 。  

    2.  选择“ConfigMgr_MPReplica” ，然后单击“下一步” 。  

    3.  在“分发代理位置”  页上，选择“在其订阅服务器上运行每个代理(请求订阅)” ，然后单击“下一步” 。  

    4.  在“订阅服务器”  页上，执行下列操作之一：  

        -   从数据库副本服务器上选择要用于数据库副本的现有数据库，然后单击“确定” 。  

        -   选择“新建数据库”  以为该数据库副本创建新数据库。 在“新建数据库”  页上，指定数据库名称，然后单击“确定” 。  

    5.  单击 **“下一步”** 以继续。  

    6.  在“分发代理安全性”页上，单击对话框的“订阅服务器连接”行中的属性按钮“(.…)”，然后配置连接的安全设置。  

        > [!TIP]  
        >  属性按钮“(....)”在显示框的第四列中。  

        **安全设置：**  

        -   配置运行分发代理进程（进程帐户）的帐户：  

            -   如果 SQL Server 代理作为本地系统运行，请选择“在 SQL Server 代理服务帐户下运行(这不是我们推荐的最佳安全配置)”   

            -   如果 SQL Server 代理使用其他帐户运行，请选择“在以下 Windows 帐户下运行” ，然后配置该帐户。 你可以指定 Windows 帐户或某个 SQL Server 帐户。  

            > [!IMPORTANT]  
            >  你必须以请求订阅的形式向运行分发代理的帐户授予对发布者的权限。 有关配置这些权限的信息，请参阅 SQL Server TechNet 库中的 [分发代理安全性](http://go.microsoft.com/fwlink/p/?LinkId=238463) 。  

        -   对于“连接到分发服务器” ，请选择“通过模拟进程帐户” 。  

        -   对于“连接到订阅服务器” ，请选择“通过模拟进程帐户” 。  

         在配置连接安全设置之后，请单击“确定”  以保存它们，然后单击“下一步” 。  

    7.  在“同步计划”  页上的“代理计划”  列表框中，选择“定义计划” ，然后配置“新建作业计划” 。 将频率设置为“每日” 发生，并且每“5 分钟” 重复一次，并将持续时间设置为“无结束日期” 。 单击“下一步”  以保存计划，然后再单击“下一步”  。  

    8.  在“向导操作”  页上，选中“创建订阅” 的复选框，然后单击“下一步” 。  

    9. 在“完成向导”  页上，单击“完成” ，然后单击“关闭”  以完成向导。  

3.  完成新建订阅向导之后，立即使用“SQL Server Management Studio”连接到数据库副本服务器数据库并运行以下查询以启用 TRUSTWORTHY 数据库属性：`ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4.  查看同步状态以验证订阅是否成功：  

    -   在订阅服务器计算机上：  

        -   在“SQL Server Management Studio” 中，连接到数据库副本服务器，并展开“复制” 。  

        -   展开“本地订阅” ，右键单击站点数据库发布订阅，然后选择“查看同步状态” 。  

    -   在发布服务器计算机上：  

        -   在“SQL Server Management Studio” 中，连接到站点数据库计算机，右键单击“复制”  文件夹，然后选择“启动复制监视器” 。  

5.  要为数据库副本启用公共语言运行时 (CLR) 集成，请使用“SQL Server Management Studio”  连接到数据库副本服务器上的数据库副本，并以查询形式运行以下存储过程： **exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE**  

6.  对于使用数据库副本服务器的每个管理点，请将该管理点计算机帐户添加到该数据库副本服务器上的本地“管理员”  组中。  

    > [!TIP]  
    >  数据库副本服务器上运行的管理点不需要此步骤。  

 现在管理点可以使用数据库副本了。  

###  <a name="BKMK_DBReplica_ConfigMP"></a> 第 3 步 - 将管理点配置为使用数据库副本  
 可以将主站点上的管理点配置为在安装管理点角色时使用数据库副本，或者可以将现有管理点重新配置为使用数据库副本。  

 使用下列信息将管理点配置为使用数据库副本：  

-   **配置新的管理点：** 在用于安装管理点的“管理点数据库”  页上，选择“使用数据库副本” ，然后指定承载数据库副本的计算机的 FQDN。 接着，对于“ConfigMgr 站点数据库名称” ，请指定该计算机上数据库副本的数据库名称。  

-   **配置以前安装的管理点**：打开管理点的属性页，选择“管理点数据库”  选项卡，再选择“使用数据库副本” ，然后指定承载数据库副本的计算机的 FQDN。 接着，对于“ConfigMgr 站点数据库名称” ，请指定该计算机上数据库副本的数据库名称。  

-   **对于使用数据库副本的每个管理点**，必须将管理点服务器的计算机帐户手动添加到该数据库副本的 **db_datareader** 角色。  

除了将管理点配置为使用数据库副本服务器之外，必须在管理点上的“IIS”  中启用“Windows 身份验证”  ：  

1.  打开“Internet Information Services (IIS)管理器” 。  

2.  选择管理点使用的网站，并打开“身份验证” 。  

3.  将“Windows 身份验证”  设置为“启用” ，然后关闭“Internet Information Services (IIS)管理器” 。  

###  <a name="BKMK_DBReplica_Cert"></a> 第 4 步 - 配置数据库副本服务器的自签名证书  
 必须在数据库副本服务器上创建自签名证书，并将此证书提供给将使用该数据库副本服务器的每个管理点。  

 证书会自动提供给数据库副本服务器上安装的管理点。 但是，要将此证书提供给远程管理点，则必须导出证书，然后将其添加到远程管理点上的可信人员证书存储中。  

 使用下列过程作为示例，了解如何在 Windows Server 2008 R2 计算机的数据库副本服务器上配置自签名证书。 如果具有不同的操作系统版本，请参阅操作系统文档，并根据需要调整这些过程中的步骤。  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>配置数据库副本服务器的自签名证书  

1.  在数据库副本服务器上，使用管理权限打开 PowerShell 命令提示符，然后运行下列命令： **set-executionpolicy UnRestricted**  

2.  复制以下 PowerShell 脚本，并用 **CreateMPReplicaCert.ps1**名称将其保存为文件。 将此文件的副本放入数据库副本服务器的系统分区的根文件夹中。  

    > [!IMPORTANT]  
    >  如果你正在单个 SQL Server 上配置多个数据库副本，则对于配置的每个后续副本，必须对此步骤使用此脚本的修改版本。 请参阅  [单个 SQL Server 上附加数据库副本的补充脚本](#bkmk_supscript)  

    ```  
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  在数据库副本服务器上，运行下列适用于 SQL Server 配置的命令：  

    -   对于 SQL Server 的默认实例：右键单击文件“CreateMPReplicaCert.ps1”  ，并选择“使用 PowerShell 运行” 。 运行脚本时，它会创建自签名证书，并将 SQL Server 配置为使用该证书。  

    -   对于 SQL Server 的命名实例：使用 PowerShell 运行命令 **%path%\CreateMPReplicaCert.ps1 xxxxxx** ，其中 **xxxxxx** 是 SQL Server 实例的名称。  

    -   脚本完成之后，验证 SQL Server 代理是否正在运行。 如果未在运行，请重启 SQL Server 代理。  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>配置远程管理点以使用数据库副本服务器的自签名证书  

1.  在数据库副本服务器上执行下列步骤以导出该服务器的自签名证书：  

    1.  单击“启动” ，再单击“运行” ，然后键入 **mmc.exe**。 在空白控制台中，单击“文件”，然后单击“添加/删除管理单元”。  

    2.  在“添加/删除管理单元”对话框中，从“可用的管理单元”列表中选择“证书”，然后单击“添加”。  

    3.  在“证书管理单元”对话框中，选择“计算机帐户”，然后单击“下一步”。  

    4.  在“选择计算机”对话框中，确保选中“本地计算机: (运行此控制台的计算机)”，然后单击“完成”。  

    5.  在“添加/删除管理单元”  对话框中，单击“确定” 。  

    6.  在控制台中展开“证书(本地计算机)” ，展开“个人” ，并选择“证书” 。  

    7.  右键单击友好名称为“ConfigMgr SQL Server 标识证书” 的证书，单击“所有任务” ，然后选择“导出” 。  

    8.  通过使用默认选项完成“证书导出向导”  ，并使用“.cer”  文件扩展名保存证书。  

2.  在管理点计算机上执行以下步骤，将数据库副本服务器的自签名证书添加到管理点上的“受信任人”证书存储：  

    1.  重复前面 1.a 到 1.e 的步骤 在管理点计算机上的 MMC 中配置**证书**管理单元。  

    2.  在控制台中，展开“证书(本地计算机)”，展开“受信任人”，右键单击“证书”，选择“所有任务”，然后选择“导入”以启动“证书导入向导”。  

    3.  在“要导入的文件”页上，选择在步骤 1.h 中保存的证书，然后单击“下一步”。  

    4.  在“证书存储”  页上，选择“将所有的证书放入下列存储” （“证书存储”  设置为“受信任人” ），然后单击“下一步” 。  

    5.  单击“完成”  关闭向导并在管理点上完成证书配置。  

###  <a name="BKMK_DBreplica_SSB"></a> 第 5 步 - 为数据库副本服务器配置 SQL Server Service Broker  
要支持包含管理点的数据库副本的客户端通知，你必须针对 SQL Server Service Broker 配置站点数据库服务器和数据库副本服务器之间的通信。 这要求你配置包含有关其他数据库的信息的每个数据库，并在两个数据库之间交换证书以实现安全通信。  

> [!NOTE]  
>  数据库副本服务器必须成功完成与站点数据库服务器的初始同步，然后你才能使用下列过程。  

 以下过程不会修改在 SQL Server 中为站点数据库服务器或数据库副本服务器配置的 Service Broker 端口。 作为替代，此过程将每个数据库配置为使用正确的 Service Broker 端口与其他数据库通信。  

 使用以下过程来为站点数据库服务器和数据库副本服务器配置 Service Broker。  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>为数据库副本配置 Service Broker  

1.  使用“SQL Server Management Studio”连接到数据库副本服务器数据库，然后运行以下查询以在数据库副本服务器上启用 Service Broker：**ALTER DATABASE &lt;副本数据库名称\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2.  接着，在数据库副本服务器上，为客户端通知配置 Service Broker，并导出 Service Broker 证书。 为此，请运行 SQL Server 存储过程，该存储过程只需一次操作便可配置 Service Broker 并导出证书。 在运行该存储过程时，你必须指定数据库副本服务器的 FQDN、数据库副本数据库的名称，并指定证书文件的导出位置。  

     运行以下查询在数据库副本服务器上配置所需的详细信息，并导出数据库副本服务器的证书：**EXEC sp_BgbConfigSSBForReplicaDB '&lt;副本 SQL Server FQDN\>', '&lt;副本数据库名称\>', '&lt;证书备份文件路径\>'**  

    > [!NOTE]  
    >  如果数据库副本服务器不在 SQL Server 的默认实例上，则对于此步骤，除了指定副本数据库名称之外，你还必须指定实例名称。 为此，请将**&lt;副本数据库名称\>**替换为**实例名称&lt;\\副本数据库名称\>**。  

     从数据库副本服务器中导出证书后，将证书的副本放在主站点数据库服务器上。  

3.  使用“SQL Server Management Studio”  连接到主站点数据库。 连接到主站点数据库后，运行查询以导入证书，并指定数据库副本服务器上正在使用的 Service Broker 端口、数据库副本服务器的 FQDN，以及数据库副本数据库的名称。 这会将主站点数据库配置为使用 Service Broker 与数据库副本服务器的数据库通信。  

     运行以下查询以从数据库副本服务器导入证书并指定所需的详细信息：**EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '&lt;SQL Service Broker 端口\>', '&lt;证书文件路径\>', '&lt;副本 SQL Server FQDN\>', '&lt;副本数据库名称\>'**  

    > [!NOTE]  
    >  如果数据库副本服务器不在 SQL Server 的默认实例上，则对于此步骤，除了指定副本数据库名称之外，你还必须指定实例名称。 为此，请将 **&lt;副本数据库名称\>** 替换为 **\实例名称\\副本数据库名称\>**。  

4.  接着，在站点数据库服务器上，运行以下命令来导出站点数据库服务器的证书：**EXEC sp_BgbCreateAndBackupSQLCert '&lt;证书备份文件路径\>'**  

     从站点数据库服务器中导出证书后，将证书的副本放在数据库副本服务器上。  

5.  使用“SQL Server Management Studio”  连接到数据库副本服务器数据库。 连接到数据库副本服务器数据库后，运行查询以导入证书，并指定主站点的站点代码和站点数据库服务器上正在使用的 Service Broker 端口。 这会将数据库副本服务器配置为使用 Service Broker 与主站点的数据库通信。  

     运行以下查询以从站点数据库服务器导入证书：**EXEC sp_BgbConfigSSBForRemoteService '&lt;站点代码\>', '&lt;SQL Service Broker 端口\>', '&lt;证书文件路径\>'**  

 在你完成站点数据库和数据库副本数据库的配置几分钟后，主站点上的通知管理器将为客户端通知设置从主站点数据库到数据库副本的 Service Broker 对话。  

###  <a name="bkmk_supscript"></a> 单个 SQL Server 上附加数据库副本的补充脚本  
 当你使用第 4 步中的脚本在 SQL Server 上配置数据库副本服务器的自签名证书（其中 SQL Server 已具有你计划继续使用的数据库副本）时，必须使用原始脚本修改后的版本。 以下修改使脚本无法删除服务器上的现有证书，并创建具有唯一友好名称的后续证书。  编辑原始脚本，如下所示：  

-   注释掉（阻止运行）脚本条目 **# Delete existing cert if one exists** 和 **# Create the new cert**之间的每一行。 若要如此，请添加“#”  **#**  作为每个适用行的第一个字符。  

-   对于使用此脚本配置的每个后续数据库副本，请更新证书的友好名称。  若要如此，请编辑行 **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** 并将 **ConfigMgr SQL Server Identification Certificate** 替换为新名称，如  **ConfigMgr SQL Server Identification Certificate1**。  

##  <a name="BKMK_DBReplicaOps"></a> 管理数据库副本配置  
 在站点上使用数据库副本时，请使用下列部分中的信息对卸载数据库副本、卸载使用数据库副本的站点或将站点数据库转移到新安装 SQL Server 的过程进行补充。 在使用下列部分中的信息删除发布时，请使用有关为用于数据库副本的 SQL Server 版本删除事务复制的指引。 例如，如果使用 SQL Server 2008 R2，请参阅 [如何：删除发布（复制 Transact-SQL 编程）](http://go.microsoft.com/fwlink/p/?LinkId=273934)。  

> [!NOTE]  
>  还原为数据库副本配置的站点数据库之后，你必须重新配置每个数据库副本（从而重新创建发布和订阅），然后才能使用数据库副本。  

###  <a name="BKMK_UninstallDbReplica"></a> 卸载数据库副本  
 如果为管理点使用数据库副本，你可能需要卸载数据库副本一段时间，然后再重新配置它以供使用。 例如，你必须在将 Configuration Manager 站点升级到新的 Service Pack 之前删除数据库副本。 站点升级完成后，你可以还原数据库副本以供使用。  

 使用以下步骤来卸载数据库副本。  

1.  在 Configuration Manager 控制台的“管理”工作区中，展开“站点配置”，选择“服务器和站点系统角色”，然后在详细信息窗格中选择承载管理点的站点系统服务器，其中该管理点使用将卸载的数据库副本。  

2.  在“站点系统角色”  窗格中，右键单击“管理点”  并选择“属性” 。  

3.  在“管理点数据库”  选项卡上，选择“使用站点数据库”  将管理点配置为使用站点数据库，而不是数据库副本。 然后，单击“确定”  保存配置。  

4.  接着，使用“SQL Server Management Studio”  执行下列任务：  

    -   从站点服务器数据库中删除数据库副本的发布。  

    -   从数据库副本服务器中删除数据库副本的订阅。  

    -   从数据库副本服务器中删除副本数据库。  

    -   在站点数据库服务器上禁用发布和分发。 要禁用发布和分发，请右键单击“复制”文件夹，然后单击“禁用发布和分发” 。  

5.  在你删除发布、订阅、副本数据库并在站点数据库服务器上禁用发布之后，即会卸载数据库副本。  

###  <a name="BKMK_DBReplicaOps_Uninstall"></a> 卸载发布数据库副本的站点服务器  
 在卸载发布数据库副本的站点之前，请使用下列步骤清理发布和任何订阅。  

1.  使用“SQL Server Management Studio”  从站点服务器数据库中删除数据库副本发布。  

2.  使用“SQL Server Management Studio”  从承载此站点的数据库副本的每个远程 SQL Server 中删除数据库副本订阅。  

3.  卸载站点。  

###  <a name="BKMK_DBReplicaOps_Move"></a> 移动发布数据库副本的站点服务器数据库  
 将站点数据库转移到新计算机时，请使用下列步骤：  

1.  使用“SQL Server Management Studio”  从站点服务器数据库中删除数据库副本发布。  

2.  使用“SQL Server Management Studio”  从此站点的每个数据库副本服务器中删除数据库副本订阅。  

3.  将数据库转移到新的 SQL Server 计算机。 有关详细信息，请参阅 [Modify the site database configuration](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) 主题中的 [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md) 部分。  

4.  在站点数据库服务器上重新创建数据库副本的发布。 有关详情，请参阅本主题中的 [第 1 步 - 配置站点数据库服务器以发布数据库副本](#BKMK_DBReplica_ConfigSiteDB) 。  

5.  在每个数据库副本服务器上重新创建数据库副本的订阅。 有关详情，请参阅本主题中的 [第 2 步 – 配置数据库副本服务器](#BKMK_DBReplica_ConfigSrv) 。  
