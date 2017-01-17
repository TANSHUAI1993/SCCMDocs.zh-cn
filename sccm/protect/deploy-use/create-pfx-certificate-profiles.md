---
title: "创建 PFX 证书配置文件 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 中的 PFX 文件生成支持加密数据交换的用户特定证书。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0185ab18-663d-468a-ba54-4f3f232fd4d2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 36c20af00e5a83be7038c3a0c01a33c546011427


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中创建 PFX 证书配置文件

*适用范围：System Center Configuration Manager (Current Branch)*


System Center Configuration Manager 允许你将个人信息交换 (.pfx) 文件设置到用户设备。 PFX 文件可以用于生成特定于用户的证书以支持加密数据交换。 可在 Configuration Manager 中创建 PFX 证书或将其导入。 通过 System Center Configuration Manager，可将导入或新建的 PFX 证书部署到 iOS、Android 和 Windows 10 设备。 然后可将这些文件部署到多个设备，以支持基于用户的 PKI 通信。  

> [!TIP]  
>  描述此过程的分步演练会出现在 [如何在 Configuration Manager 中创建和部署 PFX 证书配置文件](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)。  

## <a name="create-and-deploy-personal-information-exchange-pfx-certificate-profiles"></a>创建和部署个人信息交换 (PFX) 证书配置文件  

#### <a name="how-to-create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>如何创建和部署个人信息交换 (PFX) 证书配置文件  

1.  在 System Center Configuration Manager 控制台中，单击“资产和符合性”。  

2.  在“资产和符合性”  工作区中，展开“符合性设置” ，展开“公司资源访问” ，然后单击“证书配置文件” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建证书配置文件” 。 “创建证书配置文件”  向导打开。  

4.  在“创建证书配置文件”向导的“常规”  页上  ，指定下列信息：  

    -   **名称**：输入证书配置文件的唯一名称。 最多可以使用 256 个字符。  

    -   **说明**：提供对证书配置文件进行概述，以及可帮助在 System Center Configuration Manager 控制台中识别该证书配置文件的其他相关信息的描述。 最多可以使用 256 个字符。  

    -   **指定想要创建的证书配置文件类型**：选择下列证书配置文件类型之一：  

        -   **受信任的 CA 证书**：如果要部署受信任的根证书颁发机构 (CA) 或中间 CA 证书以在用户或设备必须验证另一台设备时形成证书信任链，请选择此证书配置文件类型。 例如，设备可能是远程身份验证拨入用户服务 (RADIUS) 服务器或虚拟专用网 (VPN) 服务器。 你还必须配置受信任的 CA 证书配置文件，然后才能创建 SCEP 证书配置文件。 在这种情况下，受信任的 CA 证书必须是将向用户或设备颁发证书的 CA 的受信任的根证书。  

        -   **简单证书注册协议 (SCEP) 设置**：如果要通过使用简单证书注册协议和网络设备注册服务角色服务为用户或设备请求证书，请选择此证书配置文件类型。  

        -   **个人信息交换 PKCS #12 (PFX) 设置导入**：选择此项以导入 PFX 证书。  

5.  在“创建证书配置文件”  向导的“证书属性”窗口  中，指定 PFX 证书将储存在目标设备上的什么位置。  

    -   **如果存在受信任的平台模块 (TPM) 则安装到该处**  

    -   **安装到受信任的平台模块 (TPM)，否则失败**  

    -   **安装到软件密钥存储提供程序**  

     单击“下一步” 。  

6.  在“创建证书配置文件”  向导的“支持的平台”  窗口中，指定可接收导入的 PFX 文件的操作系统或平台。  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  单击“下一步” ，查看“摘要”  页，然后关闭向导。  

8.  “证书配置文件”  工作区现在推出包含 PFX 文件的证书配置文件。 在  工作区中，转至“符合性设置”  >  >  ，右键单击将新证书部署到用户集合。  

9. 使用从下载中心 ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525)获得的适用于 Windows 8.1 的 SDK，部署创建 PFX 脚本。 Configuration Manager 2012 SP2 中添加的创建 PFX 脚本向该 SDK 添加 SMS_ClientPfxCertificate 类。 此类包括以下方法：  

    -   ImportForUser  

    -   DeleteForUser  

     示例脚本：  

    ```  
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  

    ```  

     必须为你的脚本修改以下脚本变量：  

    -   <blob\> = PFX base64 加密的 blob  

    -   $Password = PFX 文件的密码  

    -   $ProfileName = PFX 配置文件的名称  

    -   ComputerName = 主机名  



<!--HONumber=Dec16_HO3-->


