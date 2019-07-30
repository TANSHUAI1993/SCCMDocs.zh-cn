---
title: 部署 Mac 客户端
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中将客户端部署到 Mac 计算机。
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e686f9cdbece2ceb652ecd2e0f3c6d5eca420caf
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677817"
---
# <a name="how-to-deploy-clients-to-macs"></a>如何将客户端部署到 Mac

适用范围：  System Center Configuration Manager (Current Branch)

本文介绍在 Mac 计算机上部署和维护 Configuration Manager 客户端的方法。 若要了解将客户端部署到 Mac 计算机之前需要配置的内容，请参阅[将客户端软件部署到 Macs 的准备工作](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)。

当你为 Mac 计算机安装新客户端时，你可能还需要安装 Configuration Manager 更新以反映 Configuration Manager 控制台中的新客户端信息。

在这些过程中，有两个选项可用于安装客户端证书。 在[将客户端软件部署到 Macs 的准备工作](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements)中阅读用于 Macs 的客户端证书的相关详细信息。  

- 通过使用 [CMEnroll 工具](#bkmk_enroll)注册 Configuration Manager。 注册过程不支持自动证书续订。 在已安装证书过期之前重新注册 Mac 计算机。    

- [使用与 Configuration Manager 无关的证书请求和安装方法](#bkmk_external)。  

> [!IMPORTANT]  
> 若要将客户端部署到运行 macOS Sierra 的设备上，必须正确配置管理点证书的使用者名称  。 例如，使用管理点服务器的 FQDN。



## <a name="configure-client-settings"></a>配置客户端设置  

使用[默认客户端](/sccm/core/clients/deploy/about-client-settings)为 Mac 计算机配置注册。 不能使用自定义客户端设置。 若要请求和安装证书，适用于 Mac 的 Configuration Manager 客户端需要默认客户端设置。  

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 选择“客户端设置”节点，并选择“默认客户端设置”   。  

2. 在功能区“主页”选项卡的“属性”组中，选择“属性”    。  

3. 选择“注册”部分，然后配置下列设置  ：  

    1. **允许用户注册移动设备和 Mac 计算机**：“是”   

    2. **注册配置文件：** 选择“设置配置文件”  。  

4. 在“移动设备注册配置文件”  对话框中，选择“创建”  。  

5. 在“创建注册配置文件”对话框中，输入此注册配置文件的名称  。 然后配置“管理站点代码”  。 选择包含这些 Mac 计算机管理点的 Configuration Manager 主站点。  

    > [!NOTE]  
    >  如果无法选择站点，请确保在站点中至少配置一个管理点以支持移动设备。  

6. 选择“添加”  。  

7. 在“添加移动设备证书颁发机构”窗口中，选择向 Mac 计算机颁发证书的证书颁发机构服务器  。  

8. 在“创建注册配置文件”对话框中，选择之前创建的 Mac 计算机证书模板  。  

9. 选择“确定”以关闭“注册配置文件”对话框，然后关闭“默认客户端设置”对话框    。  

    > [!TIP]  
    > 如果想要更改客户端策略间隔，请使用“客户端策略”  客户端设置组中的“客户端策略轮询间隔”  。  

下一次设备下载客户端策略时，Configuration Manager 为所有用户应用这些设置。 若要为单个客户端启动策略检索，请参阅[为 Configuration Manager 客户端启动策略检索](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval)。  

除了注册客户端设置之外，请确保配置了以下客户端设备设置：  

- **硬件清单**：如果想要从 Mac 和 Windows 客户端计算机中收集硬件清单，请启用和配置此功能。 有关详细信息，请参阅[如何扩展硬件清单](/sccm/core/clients/manage/inventory/extend-hardware-inventory)。  

- **符合性设置**：如果想要评估和修正 Mac 和 Windows 客户端计算机上的设置，请启用和配置此功能。 有关详细信息，请参阅[规划和配置符合性设置](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings)。  

有关详细信息，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。  



## <a name="bkmk_download"></a> 下载 Mac 客户端  

1. 请从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=47719)下载 Mac OS X 客户端文件包。 将 ConfigmgrMacClient.msi 保存到运行 Windows 的计算机  。 文件不在 Configuration Manager 安装介质上。  

2. 在 Windows 计算机上运行安装程序。 将 Mac 客户端包 Macclient.dmg 提取到本地磁盘上的文件夹中  。 默认路径为 `C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client`。  

3. 将 Macclient.dmg 文件复制到 Mac 计算机上的文件夹中  。  

4. 在 Mac 计算机上，运行 Macclient.dmg 将文件提取到本地磁盘上的文件夹中  。  

5. 在文件夹中，请确保包含以下文件： 

    - **Ccmsetup**：使用 CMClient.pkg 在 Mac 计算机上安装 Configuration Manager 客户端   

    - **CMDiagnostics**：在 Mac 计算机上收集与 Configuration Manager 客户端相关的诊断信息  

    - **CMUninstall**：从 Mac 计算机上卸载客户端  

    - **CMAppUtil**：将 Apple 应用程序包转换为可部署为 Configuration Manager 应用程序的格式  

    - **CMEnroll**：请求和安装 Mac 计算机的客户端证书，以便以后可以安装 Configuration Manager 客户端  



## <a name="bkmk_enroll"></a> 注册 Mac 客户端  

使用 [Mac 计算机注册向导](#enroll-the-client-with-the-mac-computer-enrollment-wizard)注册单个客户端。

若要自动为多个客户端注册，请使用 [CMEnroll 工具](#client-and-certificate-automation-with-cmenroll)。   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>使用“Mac 计算机注册向导”注册客户端  

1. 客户端安装完成后，将打开“计算机注册向导”。 若要手动启动此向导，请从 Configuration Manager 首选项页中选择“注册”   。  

2. 在向导的第二页上，提供下列信息：  

   - **用户名**：用户名可以是以下格式：  

     - `domain\name`。 例如：`contoso\mnorth`  

     - `user@domain`。 例如：`mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  使用电子邮件地址填充“用户名”字段时，Configuration Manager 会自动填充“服务器名称”字段   。 它使用注册代理点服务器的默认名称和电子邮件地址的域名。 如果这些名称和注册代理点服务器的名称不匹配，请在注册过程中修复“服务器名称”  。  

       用户名和对应的密码必须与拥有 Mac 客户端证书模板的“读取”和“注册”权限的 Active Directory 用户帐户匹配   。  

   - **服务器名称**：注册代理点服务器的名称。  


### <a name="client-and-certificate-automation-with-cmenroll"></a>使用 CMEnroll 实现的客户端和证书自动化  

使用此过程，借助 CMEnroll 工具，实现客户端安装以及客户端证书请求和注册的自动化。 若要运行此工具，必须拥有 Active Directory 用户帐户。

1. 在 Mac 计算机上，导航到在其中提取 Macclient.dmg 文件内容的文件夹  。  

2. 输入以下命令：`sudo ./ccmsetup`  

3. 请一直等到看到“已完成安装”  消息。 虽然安装程序显示一条表明现在必须重启的消息，但请不要重启，而是继续进行下一步。  

4. 从 Mac 计算机上的“工具”文件夹中，键入以下命令：`sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`   

    客户端安装后，Mac 计算机注册向导将在客户端安装后打开，以帮助你注册 Mac 计算机。 有关详细信息，请参阅[使用 Mac 计算机注册向导注册客户端](#bkmk_enroll)。  

     例如：如果注册代理点服务器名为 server02.contoso.com，并且向 contoso\mnorth 授予对 Mac 客户端证书模板的权限，请键入以下命令：`sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`    

    > [!NOTE]  
    > 如果用户名包含以下任何字符，则注册失败：`<>"+=,`。 使用带有不包含这些字符用户名的带外证书。  
    >  
    > 为了获取更加无缝的用户体验，请编写安装步骤的脚本。 然后用户只需提供其用户名和密码。  

5. 键入 Active Directory 用户帐户的密码。 输入此命令时，系统会提示两个密码。 第一个密码用于超级用户帐户来运行命令。 第二个提示用于 Active Directory 用户帐户。 提示看起来相同，因此请确保按正确的顺序指定它们。  

6. 请一直等到看到“已成功注册”  消息。  

7. 若要将注册的证书限制在 Configuration Manager 范围内，请在 Mac 计算机上打开终端窗口并进行以下更改：  

    1. 输入命令 `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. 在“密匙链访问”窗口的“密匙链”部分中，选择“系统”    。 然后在“类别”部分中，选择“密匙”   。  

    3. 展开密钥以查看客户端证书。 使用安装的私钥查找证书，然后打开密匙。  

    4. 在“访问控制”  选项卡上，选择“在允许访问前确认”  。  

    5. 浏览到 **/Library/Application Support/Microsoft/CCM**，选择“CCMClient”  ，然后选择“添加”  。  

    6. 选择“保存更改”  并关闭“密钥链访问”  对话框。  

8. 重新启动 Mac 计算机。  

若要验证客户端安装是否成功，请在 Mac 计算机上的“系统首选项”中打开“Configuration Manager”项来验证   。 也可在 Configuration Manager 控制台中更新和查看“所有系统”集合  。 确认 Mac 计算机作为托管客户端显示在此集合中。  

> [!TIP]  
> 若要帮助排除故障 Mac 客户端，请使用 Mac 客户端包中包含的 CMDiagnostics 工具  。 使用它来收集以下诊断信息：  
>   
> - 运行的进程的列表  
> - Mac OS X 操作系统版本  
> - 与 Configuration Manager 客户端相关的 Mac OS X 故障报告包括 **CCM\*.crash** 和 **System Preference.crash**。  
> - Configuration Manager 客户端安装创建的物料清单 (BOM) 文件和属性列表 (.plist) 文件。  
> - /Library/Application Support/Microsoft/CCM/Logs 文件夹的内容  。  
>   
> CmDiagnostics 收集的信息会添加到一个 zip 文件中，该文件将保存到计算机的桌面上并且命名为 `cmdiag-<hostname>-<datetime>.zip`



## <a name="bkmk_external"></a> 管理 Configuration Manager 的外部证书

可以使用与 Configuration Manager 无关的证书请求和安装方法。 使用相同的常规过程，但包括以下附加步骤： 

- 安装 Configuration Manager 客户端时，请使用 MP 和 SubjectName 命令行选项   。 输入以下命令：`sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`。 证书使用者名称区分大小写，因此请键入与证书详细信息中显示的值完全相同的值。  

     例如：管理点的 Internet FQDN 为 server03.contoso.com  。 Mac 客户端证书的 FQDN 为 mac12.contoso.com ，作为证书使用者中的通用名  。 请使用以下命令：`sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- 如果有多个包含同一使用者值的证书，请指定证书序列号以用于 Configuration Manager 客户端。 请使用以下命令：`sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`。  

     例如：`sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>续订 Mac 客户端证书  

此过程删除了 SMSID。 适用于 Mac 的 Configuration Manager 客户端需要一个新 ID 以使用新的或续订证书。  

> [!IMPORTANT]  
> 替换客户端 SMSID 后，删除 Configuration Manager 控制台中的旧资源时，也可以删除任何存储的客户端历史记录。 例如，该客户端的硬件清单历史记录。  


1. 为必须续订计算机证书的 Mac 计算机创建和填充设备集合。  

2. 在“资产和符合性”  工作区中，启动“创建配置项目向导”  。  

3. 在向导的“常规”  页上，指定下列信息：  

    - **名称**：**删除 Mac 的 SMSID**  

    - **类型**：**Mac OS X**  

4. 在“支持的平台”页上，选择所有的 Mac OS X 版本  。  

5. 在“设置”页上，选择“新建”   。 在“创建设置”窗口中，指定以下信息  ：  

    - **名称**：**删除 Mac 的 SMSID**  

    - **设置类型**：**脚本**  

    - **数据类型**：**字符串**  

6. 在“创建设置”窗口中，对于“发现脚本”，选择“添加脚本”    。 此操作指定脚本以发现配置有 SMSID 的 Mac 计算机。  

7. 在“编辑发现脚本”窗口中，输入以下 shell 脚本  ：  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. 选择“确定”以关闭“编辑发现脚本”窗口   。  

9. 在“创建设置”窗口中，对于“修正脚本(可选)”，选择“添加脚本”    。 此操作指定脚本在 Mac 计算机上发现 SMSID 时将其删除。  

10. 在“创建修正脚本”窗口中，输入以下 shell 脚本  ：  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. 选择“确定”以关闭“创建修正脚本”窗口   。  

12. 在”符合性规则”页上，选择“新建”   。 然后在“创建规则”窗口中，指定以下信息  ：  

    - **名称**：**删除 Mac 的 SMSID**  

    - **选定的设置**：选择“浏览”，然后选择先前指定的发现脚本  。  

    - 在**以下值**字段中：“域/默认值对 (com.microsoft.ccmclient, SMSID) 不存在”  。  

    - 启用“当此设置不符合时运行指定的修正脚本”选项  。  

13. 完成向导。  

14. 创建包含此配置项目的配置基线。 将基线部署到目标集合。  

     有关详细信息，请参阅[如何创建配置基线](/sccm/compliance/deploy-use/create-configuration-baselines)。  

15. 在删除了 SMSID 的 Mac 计算机上安装了新证书后，运行以下命令，以便将客户端配置为使用此新证书：  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>另请参阅

[将客户端部署到 Mac 的准备工作](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)

[维护 Mac 客户端](/sccm/core/clients/manage/maintain-mac-clients)
