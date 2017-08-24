---
title: "部署 Mac 客户端 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中将客户端部署到 Mac 计算机。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6ce212c6745b70a47553891e5dbc124b4c4e50fa
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

*适用范围：System Center Configuration Manager (Current Branch)*

本主题介绍在 Mac 计算机上部署和维护 Configuration Manager 客户端的方法。 若要了解将客户端部署到 Mac 计算机之前需要配置的内容，请参阅[将客户端软件部署到 Macs 的准备工作](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)。

当你为 Mac 计算机安装新客户端时，你可能还需要安装 Configuration Manager 更新以反映 Configuration Manager 控制台中的新客户端信息。

在这些过程中，有两个选项可用于安装客户端证书。 在[将客户端软件部署到 Macs 的准备工作](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements)中阅读用于 Macs 的客户端证书的相关详细信息。  

-   通过使用 [CMEnroll 工具](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac)注册 Configuration Manager。 注册过程不支持自动证书续订，因此你必须在安装的证书过期之前重新注册 Mac 计算机。    

-   [使用与 Configuration Manager 无关的证书请求和安装方法](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager)。 

>[!IMPORTANT]
>  若要将客户端部署到运行 macOS Sierra 的设备上，必须正确配置管理点证书的使用者名称（例如，使用管理点服务器的 FQDN）。


## <a name="configure-client-settings-for-enrollment"></a>配置客户端设置以进行注册  
 必须使用[默认客户端设置](../../../core/clients/deploy/about-client-settings.md)来为 Mac 计算机配置注册；无法使用自定义客户端设置。  

 Configuration Manager 需要此步骤以便在 Mac 上请求和安装证书。  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>为 Configuration Manager 配置默认客户端设置以便为 Mac 注册证书  

1.  在 Configuration Manager 控制台中，选择“管理” >  “客户端设置” > “默认客户端设置”。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  选择“注册”部分，然后配置以下设置：  

    1.  **允许用户注册移动设备和 Mac 计算机：是**  

    2.  “注册配置文件：”选择“设置配置文件”。  

6.  在“移动设备注册配置文件”对话框中，选择“创建”。  

7.  在“创建注册配置文件”  对话框中，输入此注册配置文件的名称，然后配置“管理站点代码” 。 选择包含将管理 Mac 计算机的管理点的 Configuration Manager 主站点。  

    > [!NOTE]  
    >  如果无法选择站点，则检查是否将站点中的至少一个管理点配置为支持移动设备。  

8.  选择“添加”。  

9. 在“添加移动设备证书颁发机构”对话框中，选择将向 Mac 计算机颁发证书的证书颁发机构 (CA) 服务器。  

10. 在“创建注册配置文件”对话框中，选择在步骤 3 中创建的 Mac 计算机证书模板。  

11. 单击“确定”以关闭“注册配置文件”对话框，然后关闭“默认客户端设置”对话框。  

    > [!TIP]  
    >  如果想要更改客户端策略间隔，请使用“客户端策略”客户端设置组中的“客户端策略轮询间隔”。  

 所有用户下次下载客户端策略时，将使用这些设置进行配置。 要为单个客户端启动策略检索，请参阅[为 Configuration Manager 客户端启动策略检索](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

 除了注册客户端设置之外，请确保配置了以下客户端设备设置：  

-   “硬件清单”：如果要从 Mac 和 Windows 客户端计算机中收集硬件清单，请启用和配置此设置。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中扩展硬件清单](../../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

-   “符合性设置”：如果要评估和修正 Mac 和 Windows 客户端计算机上的设置，请启用和配置此设置。 有关详细信息，请参阅[规划和配置符合性设置](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

> [!NOTE]  
>  有关 Configuration Manager 客户端设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../core/clients/deploy/configure-client-settings.md)。  

## <a name="download-the-client-source-files-for-macs"></a>为 Mac 下载客户端源文件  

1.  下载 Mac OS X 客户端文件包“ConfigmgrMacClient.msi” 并将其保存在运行 Windows 的计算机上。  

     Configuration Manager 安装媒体上不提供此文件。 可以从 [Microsoft Download Center（Microsoft 下载中心）](http://go.microsoft.com/fwlink/?LinkID=525184)下载此文件。  

2.  在 Windows 计算机上运行 **ConfigmgrMacClient.msi**，以将 Mac 客户端包 Macclient.dmg 提取到本地磁盘上的文件夹（默认位置为 **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**）。  

3.  将 Macclient.dmg 文件复制到 Mac 计算机上的文件夹中。  

4.  在 Mac 计算机上，运行 Macclient.dmg 文件以将文件提取到本地磁盘上的文件夹中。  

5.  在此文件夹中，请确保提取 Ccmsetup 和 CMClient.pkg 文件，并且创建一个包含 CMDiagnostics、CMUninstall、CMAppUtil 和 CMEnroll 工具的名称为“工具”的文件夹。

    -  **Ccmsetup**：在 Mac 计算机上安装 Configuration Manager 客户端。  

    -   **CMDiagnostics**：在 Mac 计算机上收集与 Configuration Manager 客户端相关的诊断信息。  

    -   **CMUninstall**：从 Mac 计算机上卸载客户端。  

    -   **CMAppUtil**：将 Apple 应用程序包转换为可部署为 Configuration Manager 应用程序的格式。  

    -   **CMEnroll**：请求和安装 Mac 计算机的客户端证书，以便以后可以安装 Configuration Manager 客户端。   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>在 Mac 上安装客户端，然后注册客户端证书  

可以使用 [Mac 计算机注册向导](#enroll-the-client-with-the-mac-computer-enrollment-wizard)注册单个客户端。

有关可实现注册多个客户端的自动化操作，请使用 [CMEnroll 工具](#client-and-certificate-automation-with-cmenroll)。   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>使用“Mac 计算机注册向导”注册客户端  

1.  安装完客户端后，“计算机注册向导”将打开。 如果向导未打开或者无意中关闭了向导，请单击“Configuration Manager”首选项页中的“注册”以打开向导。  

2.  在向导的第二页上，提供：  

    -   **用户名** - 用户名可以是以下格式：  

        -   “域\名称”。 例如：“contoso\mnorth”  

        -   'user@domain'. 例如：“mnorth@contoso.com”  

            > [!IMPORTANT]  
            >  使用电子邮件地址填充“用户名”字段时，Configuration Manager 将自动使用该电子邮件地址的域名和注册代理点服务器的默认名称填充“服务器名称”字段。 如果此域名和服务器名称与注册代理点服务器的名称不匹配，请告知用户在注册其 Mac 计算机时要使用的正确名称。  

         用户名和对应的密码必须与被授予 Mac 客户端证书模板的“读取”和“注册”权限的 Active Directory 用户帐户匹配。  

    -   **密码** - 为指定的用户名输入对应的密码。  

    -   **服务器名称** - 输入注册代理点服务器的名称。  


### <a name="client-and-certificate-automation-with-cmenroll"></a>使用 CMEnroll 实现的客户端和证书自动化  

使用此过程，借助 CMEnroll 工具，实现客户端安装以及客户端证书请求和注册的自动化。 要运行此工具，必须有 Active Directory 用户帐户。

1.  在相同的 Mac 计算机上，导航到在其中提取 Macclient.dmg 文件内容的文件夹。  

2.  输入以下命令行： **sudo ./ccmsetup**  

3.  请一直等到看到“已完成安装”  消息。 虽然安装程序显示一条表明现在必须重启的消息，但请不要重启，而是继续进行下一步。  

4.  从 Mac 计算机上的工具文件夹中，键入以下内容：**sudo ./CMEnroll -s &lt;注册代理服务器名称> -ignorecertchainvalidation -u &lt;用户名'>**  

    客户端安装后，Mac 计算机注册向导将在客户端安装后打开，以帮助你注册 Mac 计算机。 要用此方法注册客户端，请参见此主题中的 [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) 。  

5. 键入 Active Directory 用户帐户的密码。  输入此命令时，系统会要求输入两个密码：第一个提示用于运行命令的超级用户帐户。 第二个提示用于 Active Directory 用户帐户。 提示看起来相同，因此请确保按正确的顺序指定它们。  

    用户名可以是以下格式：  

    -   “域\名称”。 例如：“contoso\mnorth”  

    -   'user@domain'. 例如：“mnorth@contoso.com”  

     用户名和对应的密码必须与被授予 Mac 客户端证书模板的“读取”和“注册”权限的 Active Directory 用户帐户匹配。  

     示例：如果注册代理点服务器名为 **server02.contoso.com**，并且向 **contoso\mnorth** 用户名授予了对 Mac 客户端证书模板的权限，请键入以下内容： **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  如果用户名包含以下任一字符：**&lt;>"+=,**，则注册将失败。 获取带有不包含这些字符的用户名的带外证书。  
    >  
    >  为了获得更加完美的用户体验，你可以对安装步骤和命令编写脚本，以便用户只须提供其用户名和密码。  

5.  请一直等到看到“已成功注册”  消息。  

6.  若要将注册的证书限制在 Configuration Manager 范围内，请在 Mac 计算机上打开终端窗口并进行以下更改：  

    a.  输入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  在“密钥链访问”对话框中的“密钥链”部分中，选择“系统”，然后在“类别”部分中，选择“密钥”。  

    c.  展开密钥以查看客户端证书。 标识了具有刚才安装的私钥的证书后，双击密钥。  

    d.  在“访问控制”选项卡上，选择“在允许访问前确认”。  

    e.  浏览到 **/Library/Application Support/Microsoft/CCM**，选择“CCMClient”，然后选择“添加”。  

    f.  选择“保存更改”并关闭“密钥链访问”对话框。  

7.  重新启动 Mac 计算机。  

 在 Mac 计算机上的“系统首选项”  中打开“Configuration Manager”  项以验证客户端安装是否成功。 也可以更新和查看“所有系统”  集合，以确认现在 Mac 计算机在此集合中显示为托管客户端。  

> [!TIP]  
>  为了帮助排查 Mac 客户端的问题，可以使用 Mac OS X 客户端包附带的 CMDiagnostics 程序收集以下诊断信息：  
>   
>  -   运行的进程的列表  
> -   Mac OS X 操作系统版本  
> -   与 Configuration Manager 客户端相关的 Mac OS X 故障报告包括 **CCM\*.crash** 和 **System Preference.crash**。  
> -   Configuration Manager 客户端安装创建的物料清单 (BOM) 文件和属性列表 (.plist) 文件。  
> -   /Library/Application Support/Microsoft/CCM/Logs 文件夹的内容。  
>   
>  CmDiagnostics 收集的信息会添加到一个 zip 文件中，该文件将保存到计算机的桌面上并且名为 cmdiag-*<主机名\>***-***&gt;日期和时间\>*.zip。***


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>使用与 Configuration Manager 无关的证书请求和安装方法  

首先，执行[将客户端软件部署到 Macs 的准备工作](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)中的这些特定任务：

1. [将 Web 服务器证书部署到站点系统服务器](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [将客户端身份验证证书部署到站点系统服务器](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [配置管理点和分发点](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [可选：安装 Reporting Services 点](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

然后，执行这些任务：

5. [为 Mac 下载客户端源文件](#download-the-client-source-files-for-macs)。  
6. 请使用所选证书部署方法附带的说明在 Mac 计算机上请求和安装客户端证书。  
7.  导航到文件夹，你在该文件夹中已经提取了从 Microsoft 下载中心下载的 macclient.dmg 文件的内容。  

3.  输入以下命令行：**sudo ./ccmsetup -MP <management point Internet FQDN\> -SubjectName <certificate subject value\>**。  证书使用者值区分大小写，因此请键入与证书详细信息中显示的值完全相同的值。  

     示例：如果站点系统属性中的 Internet FQDN 为 **server03.contoso.com**，并且 Mac 客户端证书以 **mac12.contoso.com** 的 FQDN 作为证书使用者中的公用名，请键入：**sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  请一直等到看到“已完成安装”  消息，然后重启 Mac 计算机。  

5.  要确保 Configuration Manager 可以访问此证书，请在 Mac 计算机上打开终端窗口并进行以下更改：  

    a.  输入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  在“密钥链访问”对话框中的“密钥链”部分中，选择“系统”，然后在“类别”部分中，选择“密钥”。  

    c.  展开密钥以查看客户端证书。 标识了具有刚才安装的私钥的证书后，双击密钥。  

    d.  在“访问控制”选项卡上，选择“在允许访问前确认”。  

    e.  浏览到 **/Library/Application Support/Microsoft/CCM**，选择“CCMClient”，然后选择“添加”。  

    f.  选择“保存更改”并关闭“密钥链访问”对话框。  

6.  如果有多个包含同一使用者值的证书，你必须指定证书序列号以标识要用于 Configuration Manager 客户端的证书。 若要执行此操作，请使用下列命令：**sudo defaults write com.microsoft.ccmclient SerialNumber -data "<序列号\>"**。  

     例如： **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 在 Mac 的“系统首选项”中打开“Configuration Manager”项以验证客户端安装是否成功。 也可以更新和查看“所有系统”集合，以确认 Mac 在此集合中显示为托管客户端。  

## <a name="renewing-the-mac-client-certificate"></a>续订 Mac 客户端证书  
 在 Mac 计算机上续订计算机证书之前，请使用以下过程。  

 此过程会删除客户端在 Mac 计算机上使用新证书或续订的证书所需的 SMSID。  

> [!IMPORTANT]  
>  如果删除和替换客户端 SMSID，则从 Configuration Manager 控制台中删除客户端之后会删除诸如清单之类的任何存储的客户端历史记录。  

### <a name="to-renew-the-mac-client-certificate"></a>要续订 Mac 客户端证书  

1.  为必须续订计算机证书的 Mac 计算机创建和填充设备集合。  

2.  在“资产和符合性”  工作区中，启动“创建配置项目向导” 。  

3.  在向导的“常规”  页上，指定下列信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **类型：Mac OS X**  

4.  在向导的“支持的平台”  页上，确保选择所有的 Mac OS X 版本。  

5.  在向导的“设置”  页上，单击“新建”  ，然后在“创建设置”  对话框中指定以下信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **设置类型：脚本**  

    -   **数据类型：字符串**  

6.  在“创建设置”  对话框中，对于“发现脚本” ，请单击“添加脚本”  以指定发现配置有 SMSID 的 Mac 计算机的脚本。  

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

12. 在向导的“符合性规则”页上，选择“新建”，然后在“创建规则”对话框中指定以下信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **选择的设置：**选择“浏览”，然后选择先前指定的发现脚本。  

    -   在**“以下值”** 字段中，输入 **“域/默认值对 (com.microsoft.ccmclient, SMSID) 不存在”**。  

    -   启用“当此设置不符合时运行指定的修正脚本” 选项。  

13. 完成“创建配置项目向导”。  

14. 创建一个包含你刚刚创建的配置项目的配置基线，然后将它部署到你在步骤 1 中创建的设备集合。  

     有关如何创建和部署配置基线的详细信息，请参阅[如何在 System Center Configuration Manager 中创建配置基线](../../../compliance/deploy-use/create-configuration-baselines.md)。  

15. 在删除了 SMSID 的 Mac 计算机上安装了新的证书后，运行以下命令，以便将客户端配置为使用此新证书：  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. 如果有多个包含同一使用者值的证书，你必须指定证书序列号以标识要用于 Configuration Manager 客户端的证书。 若要执行此操作，请使用下列命令：**sudo defaults write com.microsoft.ccmclient SerialNumber -data "<序列号\>"**。  

     例如： **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. 重启。  


## <a name="see-also"></a>另请参阅

[维护 Mac 客户端](/sccm/core/clients/manage/maintain-mac-clients)
