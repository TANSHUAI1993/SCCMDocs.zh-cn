---
title: "维护 Mac 客户端 | Microsoft Docs"
description: "Configuration Manager Mac 客户端的维护任务。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3bf6651f58dc0c2aa4773f77115c3fbcd4a33221
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="maintain-mac-clients"></a>维护 Mac 客户端
*适用范围：System Center Configuration Manager (Current Branch)*

以下是用于卸载 Mac 客户端和续订其证书的步骤。

##  <a name="uninstalling-the-mac-client"></a>卸载 Mac 客户端  

1.  在 Mac 计算机上，打开终端窗口并导航到包含 **macclient.dmg** 的文件夹。  

2.  导航到“工具”文件夹并输入以下命令行：  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  **-c** 属性指示客户端卸载也会删除客户端崩溃日志和日志文件。 如果要稍后重新安装该客户端，建议使用此命令。  

3.  如果需要，手动删除 Configuration Manager 所使用的客户端身份验证证书，或将其吊销。 CMUnistall 不会删除或吊销此证书。  

##  <a name="renewing-the-mac-client-certificate"></a>续订 Mac 客户端证书  
 使用下列方法之一续订 Mac 客户端证书：  

-   [续订证书向导](#renew-certificate-wizard)  

-   [手动续订证书](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>续订证书向导  

1.  在 ccmclient.plist 文件中将以下值配置为字符串，以控制续订证书向导的打开时间：  

 -   **RenewalPeriod1** - 指定用户可以在其中续订证书的第一个续订期间（以秒为单位）。 默认值为 3,888,000 秒（45 天）。 不得将值配置为小于 300 秒，否则该期间将恢复为默认值。 

 -   **RenewalPeriod2** - 指定用户可以在其中续订证书的第二个续订期间（以秒为单位）。 默认值为 259,200 秒（3 天）。 如果将此值配置为大于或等于 300 秒且小于或等于“RenewalPeriod1”，则将使用该值。 如果“RenewalPeriod1”  大于 3 天，则“RenewalPeriod2” 将使用的值为 3 天。  如果“RenewalPeriod1”  小于 3 天，则“RenewalPeriod2”  设置为与“RenewalPeriod1” 相同的值。  

 -   **RenewalReminderInterval1** - 指定在第一个续订期间将向用户显示续订证书向导的频率（以秒为单位）。 默认值为 86,400 秒（1 天）。 如果“RenewalReminderInterval1”  大于 300 秒且小于为“RenewalPeriod1” 配置的值，则将使用配置的值。 否则，将使用默认值，即 1 天。  

 -   **RenewalReminderInterval2** - 指定在第二个续订期间将向用户显示续订证书向导的频率（以秒为单位）。 默认值为 28,800 秒（8 小时）。 如果“RenewalReminderInterval2”  大于 300 秒、小于等于“RenewalReminderInterval1”  且小于等于“RenewalPeriod2” ，则将使用配置的值。 否则，将使用的值为 8 小时。  

     **示例：** 如果将各值保留为其默认值，则在证书到期前 45 天，将每 24 小时打开该向导。  在证书到期前 3 天内，将每隔 8 小时打开该向导。  

     **示例：** 使用以下命令行或脚本将第一个续订期间设置为 20 天。  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  当预订证书向导打开时，通常将预先填充“用户名”和“服务器名称”字段，用户只需输入密码即可续订证书。  

    > [!NOTE]  
    >  如果向导未打开或者你无意中关闭了向导，请单击“Configuration Manager”  首选项页中的“续订”  以打开向导。  

###  <a name="renew-certificate-manually"></a>手动续订证书  
 Mac 客户端证书的有效期通常为 1 年。 Configuration Manager 不自动续订其在注册过程中请求的用户证书，因此你必须使用以下程序来手动续订证书。  

> [!IMPORTANT]  
>  如果证书过期，你必须卸载、重新安装并随后重新注册 Mac 客户端。  

 此过程会删除为相同 Mac 计算机请求新证书所需的 SMSID。 如果删除和替换客户端 SMSID，则从 Configuration Manager 控制台中删除客户端之后会删除诸如清单之类的任何存储的客户端历史记录。  

1.  为必须续订用户证书的 Mac 计算机创建和填充设备集合。  

    > [!WARNING]  
    >  Configuration Manager 不监视它为 Mac 计算机注册的证书的有效期。 你必须独立于 Configuration Manager 监视此有效期，以标识要添加到此集合中的 Mac 计算机。  

2.  在“资产和符合性”  工作区中，启动“创建配置项目向导” 。  

3.  在“常规”  页面上，指定下列信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **类型：Mac OS X**  

4.  在“支持的平台”页上，确保选择所有的 Mac OS X 版本。  

5.  在“设置”页上，选择“新建”，然后在“创建设置”对话框中指定以下信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **设置类型：脚本**  

    -   **数据类型：字符串**  

6.  在“创建设置”对话框中，对于“发现脚本”，请选择“添加脚本”以指定发现配置有 SMSID 的 Mac 计算机的脚本。  

7.  在“编辑发现脚本”  对话框中，输入以下外壳脚本：  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  选择“确定”以关闭“编辑发现脚本”对话框。  

9. 在“创建设置”对话框中，对于“修正脚本(可选)”，请选择“添加脚本”以指定在 Mac 计算机上发现 SMSID 时将其删除的脚本。  

10. 在“创建修正脚本”  对话框中，输入以下外壳脚本：  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. 选择“确定”以关闭“创建修正脚本”对话框。  

12. 在向导的“符合性规则”  页上，单击“新建” ，然后在“创建规则”  对话框中指定以下信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **选择的设置：**选择“浏览”，然后选择先前指定的发现脚本。  

    -   在**“以下值”** 字段中，输入 **“域/默认值对 (com.microsoft.ccmclient, SMSID) 不存在”**。  

    -   启用“当此设置不符合时运行指定的修正脚本” 选项。  

13. 完成“创建配置项目向导”。  

14. 创建一个包含刚刚创建的配置项目的配置基线，然后将其部署到步骤 1 中创建的设备集合。  

     有关如何创建和部署配置基线的详细信息，请参阅[如何在 System Center Configuration Manager 中创建配置基线](../../../compliance/deploy-use/create-configuration-baselines.md)和[如何在 System Center Configuration Manager 中部署配置基线](../../../compliance/deploy-use/deploy-configuration-baselines.md)。  

15. 在删除了 SMSID 的 Mac 计算机上，运行以下命令以安装新证书：  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     出现提示时，提供超级用户帐户的密码以运行命令，然后提供 Active Directory 用户帐户的密码。  

16. 若要将注册的证书限制在 Configuration Manager 范围内，请在 Mac 计算机上打开终端窗口并进行以下更改：  

    a.  输入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  在“密钥链访问”对话框中的“密钥链”部分中，选择“系统”，然后在“类别”部分中，选择“密钥”。  

    c.  展开密钥以查看客户端证书。 标识了具有刚才安装的私钥的证书后，双击密钥。  

    d.  在“访问控制”选项卡上，选择“在允许访问前确认”。  

    e.  浏览到 **/Library/Application Support/Microsoft/CCM**，选择“CCMClient”，然后选择“添加”。  

    f.  选择“保存更改”并关闭“密钥链访问”对话框。  

17. 重新启动 Mac 计算机。  

