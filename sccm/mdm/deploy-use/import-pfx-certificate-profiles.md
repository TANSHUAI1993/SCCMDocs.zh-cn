---
title: "通过导入证书详细信息创建 PFX 证书配置文件 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 中的 PFX 文件生成支持加密数据交换的用户特定证书。"
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: c8346d04c7cd9761291824f5d30f09fab9acbcf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>如何通过导入证书详细信息创建 PFX 证书配置文件

*适用范围：System Center Configuration Manager (Current Branch)*


本文介绍如何通过从外部证书导入凭据来创建证书配置文件。  

[证书配置文件](../../protect/deploy-use/introduction-to-certificate-profiles.md)提供有关创建和配置证书配置文件的一般信息。 本主题强调了有关与 PFX 证书相关的证书配置文件的一些具体信息。

-  Configuration Manager 可管理各种适用于不同设备和操作系统的证书存储。  其中包括:

 -   iOS 和 MacOS/OSX
 -   Android 和 Android for Work
 -   Windows 10，包括 Windows 10 移动版。

若要了解详细信息，请参阅[证书配置文件先决条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)。

## <a name="pfx-certificate-profiles"></a>PFX 证书配置文件
System Center Configuration Manager 允许导入证书凭据，然后将个人信息交换 (.pfx) 文件导入到用户设备。 PFX 文件可以用于生成特定于用户的证书以支持加密数据交换。

> [!TIP]  
>  描述此过程的分步演练会出现在 [如何在 Configuration Manager 中创建和部署 PFX 证书配置文件](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)。  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>创建、导入和部署个人信息交换 (PFX) 证书配置文件  

### <a name="get-started"></a>入门

1.  在 System Center Configuration Manager 控制台中，单击“资产和符合性”。  
2.  在“资产和符合性”  工作区中，展开“符合性设置” ，展开“公司资源访问” ，然后单击“证书配置文件” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建证书配置文件” 。

4.  在“创建证书配置文件”向导的“常规”  页上  ，指定下列信息：  

    -   **名称**：输入证书配置文件的唯一名称。 最多可以使用 256 个字符。  

    -   **说明**：提供对证书配置文件进行概述，以及可帮助在 System Center Configuration Manager 控制台中识别该证书配置文件的其他相关信息的描述。 最多可以使用 256 个字符。  

    -   **指定想要创建的证书配置文件的类型**：对于 PFX 证书，请选择以下选项之一：  

        -   **个人信息交换 PKCS #12 (PFX) 设置 - 导入**：通过以编程方式导入现有证书的信息来创建证书配置文件。  

        -   **个人信息交换 - PKCS #12 (PFX) 设置 - 创建**：使用证书颁发机构提供的凭据来创建 PFX 证书配置文件。  若要了解详细信息，请参阅[如何使用证书颁发机构创建 PFX 证书配置文件](../../mdm/deploy-use/create-pfx-certificate-profiles.md)。


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>为导入的凭据创建 PFX 证书配置文件

要导入 PFX 证书，需要使用 Configuration Manager SDK 部署创建 PFX 脚本。 

稍后将导入的证书部署到注册的设备。

1. 在“创建证书配置文件向导”的“PFX 证书”页上，指定设备密钥存储提供程序的位置：
    -   **如果存在受信任的平台模块 (TPM) 则安装到该处**  
    -   **安装到受信任的平台模块 (TPM)，否则失败** 
    -   **安装到 Windows Hello 企业版，否则失败** 
    -   **安装到软件密钥存储提供程序** 
2. 单击“下一步” 。 
3. 在向导的“支持的平台”页上，选择支持的设备平台，然后单击“下一步”。

### <a name="finish-the-profile"></a>完成配置文件

1.  单击“下一步” ，查看“摘要”  页，然后关闭向导。  
2.  “证书配置文件”  工作区现在推出包含 PFX 文件的证书配置文件。 
3.  要部署配置文件，请在“资产和符合性”工作区中打开“符合性设置”  > “公司资源访问” > “证书配置文件”，右键单击所需的证书，然后单击“部署”。 

### <a name="deploy-a-create-pfx-script"></a>部署创建 PFX 脚本

使用 [Configuration Manager SDK](http://go.microsoft.com/fwlink/?LinkId=613525) 部署创建 PFX 脚本。 

Configuration Manager 2012 SP2 中添加的创建 PFX 脚本向该 SDK 添加 SMS_ClientPfxCertificate 类。 此类包括以下方法：  

    -   `ImportForUser`  

    -   `DeleteForUser`  

下面的示例将凭据导入 PFX 证书配置文件。

``` powershell
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

若要使用此示例，请更新以下脚本变量：  

   -   **blob**\ - PFX base64 加密的 blob  
   -   **$Password** - PFX 文件的密码  
   -   **$ProfileName** - PFX 配置文件的名称  
   -   **ComputerName** - 主机名   

## <a name="see-also"></a>另请参阅
[创建新的证书配置文件](../../protect/deploy-use/create-certificate-profiles.md)，此文档将引导你完成创建证书配置文件向导。

[如何通过导入证书详细信息创建 PFX 证书配置文件](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

[部署 Wi-Fi、VPN、电子邮件和证书配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)介绍了如何部署证书配置文件。