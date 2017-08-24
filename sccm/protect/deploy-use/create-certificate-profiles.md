---
title: "如何创建 SCEP 证书配置文件 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用证书配置文件为受管理设备预配所需的证书。"
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 1e00804d27ecef2aadd8bfa395db1919c46243ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-certificate-profiles"></a>创建证书配置文件

*适用范围：System Center Configuration Manager (Current Branch)*


使用 Configuration Manager (SCCM) 中的证书配置文件，为受管理设备预配访问公司资源所需的证书。 创建证书配置文件前，请按照 [Set up certificate infrastructure for System Center Configuration Manager](certificate-infrastructure.md)（设置 System Center Configuration Manager 的证书基础结构）中所述的内容设置证书基础结构。  

本主题介绍如何创建受信任的根和 SCEP 证书配置文件。 若要创建 PFX 证书配置文件，请参阅 [Create PFX certificate profiles](../../protect/deploy-use/create-pfx-certificate-profiles.md)（创建 PFX 证书配置文件）。

创建证书配置文件：

1.  启动“创建证书配置文件向导”。
1.  提供有关证书的一般信息。
1.  配置受信任证书颁发机构 (CA) 的证书。  
1.  配置 SCEP 证书信息（仅针对 SCEP 证书）。  
1.  为证书配置文件指定支持的平台。


## <a name="start-the-create-certificate-profile-wizard"></a>启动“创建证书配置文件向导”  

1.  在 System Center Configuration Manager 控制台中，单击“资产和符合性”。  

2.  在“资产和符合性”  工作区中，展开“符合性设置” ，展开“公司资源访问” ，然后单击“证书配置文件” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建证书配置文件” 。  

## <a name="provide-general-information-about-the-certificate-profile"></a>提供有关证书配置文件的一般信息  

在“创建证书配置文件向导”的“常规”  页上，指定下列信息：  

-   **名称**：输入证书配置文件的唯一名称。 最多可以使用 256 个字符。  

-   **说明**：提供对证书配置文件进行概述，以及可帮助在 System Center Configuration Manager 控制台中识别该证书配置文件的其他相关信息的描述。 最多可以使用 256 个字符。  

-   **指定想要创建的证书配置文件类型**：选择下列证书配置文件类型之一：  

-   **受信任的 CA 证书**：如果要部署受信任的根证书颁发机构 (CA) 或中间 CA 证书以在用户或设备必须验证另一台设备时形成证书信任链，请选择此证书配置文件类型。 例如，设备可能是远程身份验证拨入用户服务 (RADIUS) 服务器或虚拟专用网 (VPN) 服务器。 你还必须配置受信任的 CA 证书配置文件，然后才能创建 SCEP 证书配置文件。 在这种情况下，受信任的 CA 证书必须是将向用户或设备颁发证书的 CA 的受信任的根证书。  

-   **简单证书注册协议 (SCEP) 设置**：如果要通过使用简单证书注册协议和网络设备注册服务角色服务为用户或设备请求证书，请选择此证书配置文件类型。

-   **个人信息交换 PKCS #12 (PFX) 设置 - 导入**：选择此项可导入 PFX 证书。 若要了解有关 PFX 证书创建的详细信息，请参阅[导入 PFX 证书配置文件](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md)。

-   **个人信息交换 PKCS #12 (PFX) 设置 - 创建**：选择此项可使用证书颁发机构处理 PFX 证书。 若要了解有关 PFX 证书创建的详细信息，请参阅 [Create PFX certificate profiles](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md)（创建 PFX 证书配置文件）。


## <a name="configure-a-trusted-ca-certificate"></a>配置受信任的 CA 证书  

> [!IMPORTANT]  
>  你至少必须配置一个受信任的 CA 证书配置文件，然后才能创建 SCEP 证书配置文件。    
>  
>  如果在部署证书后更改这些值中的任何一个值，则需要请求新的证书：
>  -  密钥存储提供
>  -  证书模板名称
>  -  证书类型
>  -  使用者名称格式
>  -  使用者可选名称
>  -  证书有效期
>  -  密钥用法
>  -  密钥大小
>  -  扩展密钥用法
>  -  根 CA 证书

1.  在“创建证书配置文件向导”的“受信任的 CA 证书”  页上，指定下列信息：  

 -   **证书文件**：单击“导入”  ，然后浏览到要使用的证书文件。  

 -   **目标存储区**：对于具有多个证书存储区的设备，选择存储证书的位置。 对于仅有一个存储区的设备，则忽略此设置。  

2.  使用“证书指纹”  值来验证是否导入了正确的证书。  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>配置 SCEP 证书信息（仅针对 SCEP 证书）  

1.  在“创建证书配置文件向导”的“SCEP 服务器”  页上，指定将通过 SCEP 颁发证书的 NDES 服务器的 URL。 你可以选择基于证书注册点站点系统服务器的配置自动分配 NDES URL，也可以手动添加 URL。  

2.  完成“创建证书配置文件向导”的“SCEP 注册”页。

 -  **重试**：指定设备向运行网络设备注册服务的服务器自动重试证书请求的次数。 此设置支持 CA 管理程序在证书请求被接受之前必须对其进行批准的方案。 此设置通常用于安全性很高的环境或者你有独立颁发 CA（而不是企业 CA）的情况。 你还可以将此设置用于测试用的，以便能够在颁发 CA 处理证书请求之前检查证书请求选项。 将此设置与“重试延迟(分钟)”  设置一起使用。  

 -   **重试延迟(分钟)**：在颁发 CA 处理证书请求之前，指定在使用 CA 管理程序批准时每次注册尝试之间的间隔（以分钟为单位）。 如果将管理程序批准用于测试目的，你将可能需要指定一个较低的值，以便在批准证书请求之后你不会等待很长时间来让设备重试请求。 但是，如果在生产网络上使用管理程序批准，你将可能需要指定较高的值，以便为 CA 管理员留出足够的时间来检查以及批准或拒绝待定审批。  

 -   **续订阈值(%)**：指定设备请求证书续订之前剩余的证书有效期限的百分比。  

 -   **密钥存储提供程序(KSP)**：指定将存储证书密钥的位置。 可以选择下列值之一：  

   -   **安装到受信任的平台模块(TPM) (如果存在)**：将密钥安装到 TPM。 如果 TPM 不存在，则该密钥将安装到软件密钥的存储提供程序。  

   -   **安装到受信任的平台模块(TPM)，否则失败**：将密钥安装到 TPM。 如果 TPM 模块不存在，则安装将失败。  

   -   **安装到 Windows Hello 企业版，否则安装将失败**：此选项可用于 Windows 10 桌面和移动设备。 此选项将密钥注册到 **Windows Hello 企业版**，如 [System Center Configuration Manager 中的 Windows Hello 企业版设置](../../protect/deploy-use/windows-hello-for-business-settings.md)中所述。 此选项还可用于在向这些设备颁发证书前的注册期间“要求多重身份验证”  。 请参阅 [使用多重身份验证保护 Windows 设备](https://technet.microsoft.com/library/dn889751.aspx) 以获取详细信息。

   > [!NOTE]  
   > 
   > 当用户创建 Windows Hello 企业版 PIN 时，Windows 会发送通知，Configuration Manager 会侦听该通知。 这使 Configuration Manager 可以快速了解哪些用户创建了 Windows Hello PIN。 如果 Windows Hello 在证书配置文件中用作密钥存储提供程序，则 Configuration Manager 随后还可以向这些用户颁发新证书。  

   -   **安装到软件密钥存储提供程序**：将密钥安装到软件密钥的存储提供程序。  

 -   **用于证书注册的设备**：如果将证书配置文件部署到用户集合，请选择是仅允许在用户的主要设备上注册证书，还是在用户登录到的所有设备上注册证书。 如果将证书配置文件部署到设备集合，请选择是仅为设备的主要用户注册证书，还是为登录到该设备的所有用户注册证书。  

3.  在“创建证书配置文件向导”的“证书属性”  页上，指定下列信息：  

 -   **证书模板名称**：单击“浏览”  选择网络设备注册服务配置为使用并且已添加到颁发 CA 的证书模板的名称。 若要成功浏览到证书模板，用于运行 System Center Configuration Manager 控制台的用户帐户必须对证书模板具有“读取”权限。 或者，如果你无法使用“浏览” ，请键入证书模板的名称。  

 > [!IMPORTANT]
 >   
 >  如果证书模板名称包含非 ASCII 字符（例如中文字母中的字符），则将不部署证书。 为了确保部署证书，你必须首先针对 CA 创建证书模板副本，并使用 ASCII 字符重命名副本。  

   根据你是浏览到证书模板还是键入证书名称，请注意以下事项：  

 -   如果你通过浏览来选择证书模板名称，则页面上的某些字段会依据证书模板自动填充。 在某些情况下，除非选择其他证书模板，否则你无法更改这些值。  

 -   如果你键入证书模板的名称，请确保该名称与运行网络设备注册服务的服务器的注册表中所列证书模板名称之一完全匹配。 确保指定证书模板名称，而不是证书模板显示名称。  

   若要查找证书模板的名称，请浏览到以下项：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP。 你将看到作为 **EncryptionTemplate**、 **GeneralPurposeTemplate**和 **SignatureTemplate**的值而列出的证书模板。 默认情况下，所有三个证书模板的值为“IPSECIntermediateOffline” ，映射为模板显示名称“IPSec (脱机请求)” 。  

   > [!WARNING]  
   > 
   >  由于在键入证书模板名称（而不是浏览）时 System Center Configuration Manager 无法验证证书模板的内容，因此可能会选择到证书模板不支持的选项，从而导致证书请求失败。 如果发生这种情况，你将在 CPR.log 文件中看到 w3wp.exe 的错误消息，指出模板名称位于证书签名请求 (CSR) 中，并且质询不匹配。  
   >   
   >  如果键入为“GeneralPurposeTemplate”  值指定的证书模板的名称，你必须为此证书配置文件选择“密钥加密”  和“数字签名”  选项。 但是，如果要仅在此证书配置文件中启用“密钥加密”  选项，请为“EncryptionTemplate”  项指定证书模板名称。 同样，如果要仅在此证书配置文件中启用“数字签名”  选项，请为“SignatureTemplate”  项指定证书模板名称。  

 -   **证书类型**：选择是将证书部署到设备还是用户。  
 -   **使用者名称格式**：从列表中选择 System Center Configuration Manager 自动在证书请求中创建使用者名称的方式。 如果证书用于用户，还可包含使用者名称中的用户电子邮件地址。 
    
   > [!NOTE]  
   > 
   > 选择“IMEI 号码”或“序列号”，可以区分同一用户拥有的不同设备。 例如，这些设备可以共享公用名，但不可共享 IMEI 号码或序列号。 如果设备不报告 IMEI 号码或序列号，则使用公用名颁发证书。

 -   **使用者可选名称**：指定 System Center Configuration Manager 在证书请求中为使用者可选名称 (SAN) 自动创建值的方式。 例如，你选择了用户证书类型，则可以在使用者可选名称中包括用户主体名称 (UPN)。  如果将使用客户端证书向网络策略服务器进行验证，则必须将使用者可选名称设置为 UPN。  

   > [!NOTE]  
   >  - iOS 设备在 SCEP 证书中支持有限的使用者名称格式和使用者可选名称。 如果指定的格式不受支持，则不会在 iOS 设备上注册证书。 当配置要部署到 iOS 设备的 SCEP 证书配置文件时，请为“使用者名称格式”  以及“DNS 名称” 、“电子邮件地址” 或“使用者可选名称”  的“UPN”  使用“公用名” 。  

 -   **证书有效期**：如果对发证 CA 运行允许自定义有效期的 certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE 命令，则可以指定证书过期之前剩余的时间量。 有关此命令的详细信息，请参阅主题 [Certificate infrastructure in System Center Configuration Manager](../../protect/deploy-use/certificate-infrastructure.md)（System Center Configuration Manager 中的证书基础结构）。  

   你可以指定比指定证书模板中的有效期小的值，但不能指定较大的值。 例如，证书模板中的证书有效期为 2 年，则你可以指定值 1 年，但不能指定值 5 年。 该值还必须小于发证 CA 证书的剩余有效期。  

 -   **密钥使用情况**：指定证书的密钥使用情况选项。 可从以下选项中进行选择：  

        -   **密钥加密**：仅在密钥加密时允许交换密钥。  

        -   **数字签名**：仅在数字签名帮助保护密钥时允许交换密钥。  

   如果通过使用“浏览” 选择了证书模板，你可能无法更改这些设置，除非选择其他证书模板。  

   你选择的证书模板必须配置有以上一个或两个密钥用法选项。 否则，你将在证书注册点日志文件“Crp.log”  中看到“CSR 和质询中的密钥用法不匹配” 消息。  


   -   **密钥大小(位)**：选择以位为单位的密钥大小。  

   -   **扩展密钥用法**：单击“选择”为证书的预期目的添加值。 大多数情况下，证书将需要“客户端身份验证”  以便用户或设备能够向服务器进行验证。 但，你可以根据需要添加任何其他密钥用法。  


   -   **哈希算法**：选择要与此证书一起使用的可用哈希算法类型之一。 选择连接设备支持的最高级别安全性。  

   > [!NOTE]  
   > 
   >  **SHA-2** 支持 SHA-256、SHA-384 和 SHA-512。 **SHA-3** 仅支持 SHA-3。  

   -   **根 CA 证书**：单击“选择”  以选择之前配置并部署到用户或设备的根 CA 证书配置文件。 此 CA 证书必须是将颁发在此证书配置文件中配置的证书的 CA 的根证书。  

   > [!IMPORTANT]  
   >  如果指定未部署到用户或设备的根 CA 证书，System Center Configuration Manager 将不会发起在此证书配置文件中配置的证书请求。  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>为证书配置文件指定支持的平台  

1. 在“创建证书配置文件向导”的“支持的平台”  页上，选择将在其中安装证书配置文件的操作系统。 或者，单击“全选”  以将证书配置文件安装到所有可用操作系统。
2. 查看向导的“摘要”页面，并选择“完成”。 
 
 
新的证书配置文件会显示在“资产和符合性”工作区的“证书配置文件”节点中，并已准备好部署到用户或设备，如 [How to deploy profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md)（如何在 System Center Configuration Manager 中部署配置文件）中所述。  