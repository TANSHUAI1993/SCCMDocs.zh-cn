---
title: "使用证书颁发机构创建 PFX 证书配置文件 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 中的 PFX 文件生成支持加密数据交换的用户特定证书。"
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 43d8b2217763681be69711fce93c020a65da1cd8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>如何使用证书颁发机构创建 PFX 证书配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍如何使用凭据的证书颁发机构创建证书配置文件。

[证书配置文件](../../protect/deploy-use/introduction-to-certificate-profiles.md)提供有关创建和配置证书配置文件的一般信息。 本主题强调了有关与 PFX 证书相关的证书配置文件的一些具体信息。

## <a name="pfx-certificate-profiles"></a>PFX 证书配置文件
借助 System Center Configuration Manager，可以使用证书颁发机构颁发的凭据创建 PFX 证书配置文件。  从版本 1706 开始，可以选择 Microsoft 或 Entrust 作为证书颁发机构。  当部署到用户设备时，个人信息交换 (.pfx) 文件生成用户特定证书，以支持加密的数据交换。

若要从现有证书文件导入证书凭据，请参阅[如何通过导入证书详细信息创建 PFX 证书配置文件](../../mdm/deploy-use/import-pfx-certificate-profiles.md)。

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>创建和部署个人信息交换 (PFX) 证书配置文件  

### <a name="get-started"></a>入门

1.  在 System Center Configuration Manager 控制台中，选择“资产和符合性”。  
2.  在“资产和符合性” 工作区中，选择“符合性设置” &gt;“公司资源访问”&gt;“证书配置文件”。  

3.  在“主页” 选项卡上的“创建” 组中，选择“创建证书配置文件” 。

4.  在“创建证书配置文件”向导的“常规”  页上  ，指定下列信息：  

    -   **名称**：输入证书配置文件的唯一名称。 最多可以使用 256 个字符。  

    -   **说明**：提供对证书配置文件进行概述，以及可帮助在 System Center Configuration Manager 控制台中识别该证书配置文件的其他相关信息的描述。 最多可以使用 256 个字符。  

    -   在“指定想要创建的证书配置文件的类型”中，选择“个人信息交换 -- PKCS #12 (PFX)设置 -- 创建”，然后从下拉列表中选择证书颁发机构。  从版本 1706 开始，可以选择 Microsoft 或 Entrust。

### <a name="select-supported-platforms"></a>选择支持的平台

“支持的平台”页面标识证书配置文件支持的操作系统和设备。  

证书配置文件可能支持多个操作系统和设备，但某些操作系统或设备组合可能需要不同的设置。  在这些情况下，最好为每组独特的设置创建单独的配置文件。  

从版本 1706 开始，可以使用以下选项：

- Windows 10
    - 所有 Windows 10（64 位）
    - 所有 Windows 10（32 位）
    - 所有 Windows 10 全息企业版及更高版本
    - 所有 Windows 10 全息版及更高版本
    - 所有 Windows 10 协同版及更高版本
    - 所有 Windows 10 移动版及更高版本
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> 目前不支持 MacOS/OSX 设备。  

未选中任何其他选项时，“全选”复选框会选中所有可用选项。  当选中一个或多个选项时，“全选”会清除现有选择。 

1.  选择证书配置文件支持的一个或多个平台。

1.  选择“下一步”以继续。  


### <a name="configure-certification-authorities"></a>配置证书颁发机构

此处选择证书注册点 (CRP) 来处理 PFX 证书。  

1.  从“主站点”列表中，选择包含 CA 的 CRP 角色的服务器。
1.  从“证书颁发机构”列表中，通过在左列中设置选中标记来选择相关 CA。
1.  准备好继续时，选择“下一步”。

要了解详细信息，请参阅[证书基础结构](../../protect/deploy-use/certificate-infrastructure.md)。


### <a name="configure-certificate-settings-for-microsoft-ca"></a>配置 Microsoft CA 的证书设置

在将 Microsoft 用作 CA 时配置证书设置：

1.  从“证书模板名称”下拉列表中选择证书模板。

1.  启用“证书用途”复选框，将证书配置文件用于 S/MIME 签名或加密。

    在将 Microsoft 用作 CA 时检查此选项，与目标用户关联的所有 PFX 证书都会传递给用户注册的所有设备。  未选中此复选框时，每个设备都会收到一个唯一的证书。  

1.  将“使用者名称格式”设置为“公用名”或“完全可分辨名称”。  如果不确定使用哪个名称，请与你的证书颁发机构管理员联系。

1.  对于“使用者可选名称”，根据你的 CA 启用“电子邮件地址”和“用户主体名称(UPN)”。

1.  “续订阈值”根据过期前剩余时间的百分比确定证书何时自动续订。

1.  将“证书有效期”设置为证书的生存期。  通过设置数字 (1-100) 和时间段（年、月或天）指定该期限。

1.  当证书注册点指定 Active Directory 凭据时，启用“Active Directory 发布”。  启用该选项，将证书配置文件发布到 Active Directory。

1.  如果在指定支持的平台时选择了一个或多个 Windows 10 平台，则执行以下操作：

    1.  将“Windows 证书存储”设置为“用户”。  （“本地计算机”选项不部署证书，因此不应选择此项。）
    1.  从以下选项之一选择“密钥存储提供程序(KSP)”：

        - **如果存在受信任的平台模块 (TPM) 则安装到该处**  
        - **安装到受信任的平台模块 (TPM)，否则失败** 
        - **安装到 Windows Hello 企业版，否则失败** 
        - **安装到软件密钥存储提供程序** 

1.  完成后，选择“下一步”或“摘要”。

### <a name="configure-certificate-settings-for-entrust-ca"></a>配置 Entrust CA 的证书设置

在将 Entrust 用作 CA 时配置证书设置：

1.  从“数字标识配置”下拉列表中选择该配置文件。  “数字标识配置”选项由 Entrust 管理员创建。

1.  选中时，“证书用途”选项使用证书配置文件进行 S/MIME 签名或加密。

    将 Entrust 用作 CA 时，与目标用户关联的所有 PFX 证书都将传递给用户注册的所有设备。    未选中此选项时，每个设备都会收到一个唯一的证书。  （不同 CA 的行为也不同；要了解详细信息，请参阅相应章节。）

1.  使用“格式”按钮将 Entrust“使用者名称格式”令牌映射到 ConfigMgr 字段。  

    “证书名称格式”对话框列出了 Entrust 数字标识配置变量。  对于每个 Entrust 变量，从关联的下拉列表中选择相应的 LDAP 变量。

1.  使用“格式”按钮将 Entrust“使用者可选名称”令牌映射到支持的 LDAP 变量。  

    “证书名称格式”对话框列出了 Entrust 数字标识配置变量。  对于每个 Entrust 变量，从关联的下拉列表中选择相应的 LDAP 变量。

1.  “续订阈值”根据过期前剩余时间的百分比确定证书何时自动续订。

1.  将“证书有效期”设置为证书的生存期。  通过设置数字 (1-100) 和时间段（年、月或天）指定该期限。

1.  当证书注册点指定 Active Directory 凭据时，启用“Active Directory 发布”。  启用该选项，将证书配置文件发布到 Active Directory。

1.  如果在指定支持的平台时选择了一个或多个 Windows 10 平台，则执行以下操作：

    1.  将“Windows 证书存储”设置为“用户”。  （“本地计算机”选项不部署证书，因此不应选择此项。）
    1.  从以下选项之一选择“密钥存储提供程序(KSP)”：

        - **如果存在受信任的平台模块 (TPM) 则安装到该处**  
        - **安装到受信任的平台模块 (TPM)，否则失败** 
        - **安装到 Windows Hello 企业版，否则失败** 
        - **安装到软件密钥存储提供程序** 

1.  完成后，选择“下一步”或“摘要”。


### <a name="finish-up"></a>完成

1.  在“摘要”页上，查看所选内容并验证选择。

1.  准备就绪时，选择“下一步”创建配置文件。  

1.  “证书配置文件”  工作区现在推出包含 PFX 文件的证书配置文件。 

1.  部署配置文件：

    1. 打开“资产和符合性”工作区。
    1. 选择“符合性设置” > “公司资源访问” > “证书配置文件”
    1. 右键单击所需的证书配置文件，然后选择“部署”。 


## <a name="see-also"></a>另请参阅
[创建新的证书配置文件](../../protect/deploy-use/create-certificate-profiles.md)，此文档将引导你完成创建证书配置文件向导。

[如何通过导入证书详细信息创建 PFX 证书配置文件](../../mdm/deploy-use/import-pfx-certificate-profiles.md)

[部署 Wi-Fi、VPN、电子邮件和证书配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)介绍了如何部署证书配置文件。