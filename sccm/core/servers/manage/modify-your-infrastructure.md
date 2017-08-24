---
title: "修改基础结构 | Microsoft Docs"
description: "了解如何更改所部署的 Configuration Manager 基础结构或执行可对其产生影响的操作。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a5228c4984347be4b115bfa5563791fa2fb7319c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>修改你的 System Center Configuration Manager 基础结构

*适用范围：System Center Configuration Manager (Current Branch)*

安装一个或多个站点后，你可能需要修改配置，或采取会影响你部署的基础结构的操作。  


##  <a name="BKMK_ManageSMSprovider"></a>管理 SMS 提供程序  
 SMS 提供程序（一个动态链接库文件：smsprov.dll）为一个或多个 Configuration Manager 控制台提供管理联系点。 安装多个 SMS 提供程序时，可以提供联系点冗余以管理你的站点和层次结构。  

 在每个 Configuration Manager 站点，均可以重新运行安装程序以实现下列操作：  

-   添加其他 SMS 提供程序（每个 SMS 提供程序的其他实例必须是单独的计算机）的实例  

-   删除 SMS 提供程序实例（要删除站点的最后一个 SMS 提供程序，你必须卸载该站点）。  

 通过查看你运行安装程序的站点服务器的根文件夹中的“ConfigMgrSetup.log”  ，你可以监视 SMS 提供程序的安装或删除。  

 在站点修改 SMS 提供程序之前，熟悉[为 System Center Configuration Manager 规划 SMS 提供程序](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)中的信息。  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>管理站点的 SMS 提供程序配置  

1.  从 **&lt;Configuration Manager 站点安装文件夹 \>\BIN\X64\setup.exe** 运行 **Configuration Manager 安装程序**。  

2.  在“入门”  页上，选择“执行站点维护或重置此站点” ，然后单击“下一步”   

3.  在“站点维护”  页上，选择“修改 SMS 提供程序配置” ，然后单击“下一步” 。  

4.  在“管理 SMS 提供程序”  页上，选择下列选项之一，并通过使用下列选项之一来完成向导：  

    -   在此站点上添加其他 SMS 提供程序：  

         选择“添加新的 SMS 提供程序” ，指定将承载 SMS 提供程序且当前没有承载 SMS 提供程序的计算机的 FQDN，然后单击“下一步” 。  

    -   从服务器中删除 SMS 提供程序：  

         选择“卸载指定的 SMS 提供程序” ，选择要从中删除 SMS 提供程序的计算机的名称，单击“下一步” ，然后确认操作。  

        > [!TIP]  
        >  要在两台计算机之间移动 SMS 提供程序，你必须将 SMS 提供程序安装到新计算机，并从原始位置中删除 SMS 提供程序。 没有专门用于在单一过程中在两台计算机之间移动 SMS 提供程序的选项。  

 安装向导完成后，SMS 提供程序配置即完成。 在站点的“属性”  对话框的“常规”  选项卡上，你可以验证为站点安装了 SMS 提供程序的计算机。  

##  <a name="bkmk_Console"></a>管理 Configuration Manager 控制台  
 以下是可以执行以管理 Configuration Manager 控制台的任务：  

-   **修改 Configuration Manager 控制台中显示的语言** - 若要修改已安装的语言，请参阅本主题中的[管理 Configuration Manager 控制台语言](#BKMK_ManageConsoleLanguages)。  

-   **安装其他控制台** - 若要安装其他控制台，请参阅[安装 System Center Configuration Manager 控制台](/sccm/core/servers/deploy/install/install-consoles)。  

-   **配置 DCOM** - 若要配置 DCOM 权限以允许远离站点服务器的控制台连接，请参阅本主题中的[为远程 Configuration Manager 控制台配置 DCOM 权限](#BKMK_ConfigDCOMforRemoteConsole)。  

-   **修改权限以限制管理用户可以在控制台中看到的内容** - 若要修改限制用户在控制台中所看到的内容和可以进行的操作的管理权限，请参阅[修改管理用户的管理作用域](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser)。     

###  <a name="BKMK_ManageConsoleLanguages"></a>管理 Configuration Manager 控制台语言  
 安装站点服务器期间，Configuration Manager 控制台安装文件和站点的支持语言包将复制到站点服务器上的 **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup** 子文件夹中。  

-   在站点服务器上从此文件夹中启动 Configuration Manager 控制台安装时，会将 Configuration Manager 控制台和支持的语言包文件复制到此计算机中  

-   当语言包可用于计算机上的当前语言设置时，会以该语言打开 Configuration Manager 控制台  

-   如果关联的语言包无法用于 Configuration Manager 控制台，则以英文打开控制台  

例如，假设有这样一种情况：从支持英文、德文和法文的站点服务器安装 Configuration Manager 控制台。 如果在配置了法语设置的计算机上打开 Configuration Manager 控制台，则将以法文打开控制台。 如果在配置了日语的计算机上打开 Configuration Manager 控制台，则将以英文打开控制台，因为日文语言包不可用。  

 每次打开 Configuration Manager 控制台时，它都会确定计算机的配置语言设置，并验证关联的语言包是否可用于 Configuration Manager 控制台，然后使用合适的语言包打开控制台。 如果想要用英文打开 Configuration Manager 控制台而不考虑计算机上配置的语言设置，则必须手动删除或重命名该计算机上的语言包文件。  

 使用以下过程用英文启动 Configuration Manager 控制台而不考虑计算机上配置的区域设置。  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>在计算机上安装纯英文版的 Configuration Manager 控制台  

1.  在 Windows 资源管理器中，浏览到 **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup\LanguagePack**  

2.  重命名 **.msp** 和 **.mst** 文件。 例如，你可以将 **&lt;file name\>.MSP** 更改为 **&lt;file name\>.MSP.disabled**。  

3.  在计算机上安装 Configuration Manager 控制台。  

    > [!IMPORTANT]  
    >  当为站点服务器配置新服务器语言时，.msp 和 .mst 文件会再次复制到 **LanguagePack** 文件夹中，并且必须重复此过程以安装纯英文的新 Configuration Manager 控制台。  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>对现有的 Configuration Manager 控制台安装临时禁用控制台语言  

1.  在运行 Configuration Manager 控制台的计算机上，关闭 Configuration Manager 控制台。  

2.  在 Windows 资源管理器中，浏览到 Configuration Manager 控制台计算机上的 &lt;*ConsoleInstallationPath*>\Bin\。  

3.  针对在计算机上配置的语言重命名相应的语言文件夹。 例如，为德文设置了计算机语言设置，则可以将“de”  文件夹重命名为“de.disabled” 。  

4.  若要以为计算机配置的语言打开 Configuration Manager 控制台，请将此文件夹重命名为原始名称。 例如，将“de.disabled”  重命名为“de” 。  

##  <a name="BKMK_ConfigDCOMforRemoteConsole"></a>为远程 Configuration Manager 控制台配置 DCOM 权限  
 运行 Configuration Manager 控制台的用户帐户需要权限以使用 SMS 提供程序来访问站点数据库。 但是，使用远程 Configuration Manager 控制台的管理用户也需要以下位置的**远程激活** DCOM 权限：  

-   站点服务器计算机  

-   托管 SMS 提供程序实例的每个计算机  

 名为 **SMS 管理员** 的安全组授予计算机上的 SMS 提供程序的访问权限，并且还可用于授予所需的 DCOM 权限。 （如果 SMS 提供程序在成员服务器上运行，此组是计算机的本地组，如果 SMS 提供程序在域控制器上运行，则此组是域本地组。）  

> [!IMPORTANT]  
>  Configuration Manager 控制台使用 Windows Management Instrumentation (WMI) 连接到 SMS 提供程序，并且 WMI 在内部使用 DCOM。 因此，如果 Configuration Manager 控制台在 SMS 提供程序计算机之外的其他计算机上运行，则 Configuration Manager 需要权限以在 SMS 提供程序计算机上激活 DCOM 服务器。 默认情况下，只会为内置“管理员”组的成员授予“远程激活”。 如果允许“SMS 管理员”组具有远程激活权限，则此组的成员可能会尝试对 SMS 提供程序计算机进行 DCOM 攻击。 此配置还会增大计算机的受攻击面。 为了减轻此威胁，请仔细监视“SMS 管理员”组的成员身份。  

 使用下列过程来配置每个管理中心站点、主站点服务器以及每台安装 SMS 提供程序的计算机，以便为管理用户授予远程 Configuration Manager 控制台访问权限。  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>若要为远程 Configuration Manager 控制台连接配置 DCOM 权限  

1.  通过运行  **Dcomcnfg.exe** 打开“组件服务” 。  

2.  在“组件服务”中，单击“控制台根” >  “组件服务” > “计算机”，然后单击“我的计算机” 在“操作”  菜单上，单击“属性” 。  

3.  在“我的电脑属性”  对话框中“COM 安全”  选项卡上的“启动和激活权限”  部分，单击“编辑限制” 。  

4.  在“启动和激活权限”  对话框中，单击“添加” 。  

5.  在“选择用户、计算机、服务帐户或组”  对话框中，在“输入要选择的对象名称(示例)”  框中键入 **SMS Admins**，然后单击“确定” 。  

    > [!NOTE]  
    >  你可能必须更改“从此位置中”  的设置以查找“SMS 管理员”组。 如果 SMS 提供程序运行在成员服务器上，此组是计算机的本地组，如果 SMS 提供程序运行在域控制器上，则此组是域本地组。  

6.  在“SMS 管理员的权限”  部分，请选中“远程激活”  复选框以允许远程激活。  

7.  单击“确定”  并再次单击“确定”  ，然后关闭“计算机管理” 。 计算机现在已配置为允许“SMS 管理员”组的成员远程访问 Configuration Manager 控制台。  

 在每台可能支持远程 Configuration Manager 控制台的 SMS 提供程序计算机上重复此过程。  

##  <a name="bkmk_dbconfig"></a>修改站点数据库配置  
 安装站点之后，你可以通过在管理中心站点服务器或主站点服务器上运行安装程序来修改站点数据库和站点数据库服务器的配置。 你可以将站点数据库转移到同一计算机上的新 SQL Server 实例，或转移到运行支持的 SQL Server 版本的其他计算机。 对于辅助站点的数据配置，不支持这些更改和相关更改。  

 有关支持的限制的详细信息，请参阅 [Configuration Manager 环境中手动数据库更改的支持策略](https://support.microsoft.com/kb/3106512)。  

> [!NOTE]  
>  当修改站点的数据库配置时，Configuration Manager 将在站点服务器和与数据库通信的远程站点系统服务器上重启或重新安装 Configuration Manager 服务。  

**要修改数据库配置**，你必须在站点服务器上运行安装程序，并选择“执行站点维护或重置此站点” 选项。 接着，选择“修改 SQL Server 配置”  选项。 你可以更改下列站点数据库配置：  

-   承载数据库的基于 Windows 的服务器。  

-   承载 SQL Server 数据库的服务器上使用的 SQL Server 实例。  

-   数据库名称。  

-   Configuration Manager 正在使用的 SQL Server 端口  

-   Configuration Manager 正在使用的 SQL Server Service Broker 端口  

**如果转移站点数据库，必须进行下列配置：**  

-   “配置访问权限” ：在将站点数据库转移到新计算机时，将站点服务器的计算机帐户添加到运行 SQL Server 的计算机上的“本地管理员”  组。 如果为站点数据库使用 SQL Server 群集，你必须将该计算机帐户添加到每台 Windows Server 群集节点计算机的“本地管理员”  组。  

-   **启用公共语言运行时 (CLR) 集成：**  在将数据库转移到 SQL Server 上的新实例或新 SQL Server 计算机时，你必须启用公共语言运行时 (CLR) 集成。 若要启用 CLR，请使用“SQL Server Management Studio”连接到承载站点数据库的 SQL Server 实例，并以查询形式运行以下存储过程：**sp_configure 'clr enabled',1; reconfigure**。  
-  **确保新的 SQL Server 具有访问备份位置的权限：**数据库移到新的服务器（包括 SQL Server AlwaysOn 可用性组或 SQL Server 群集）后，将 UNC 用于存储站点数据库备份时，应确保新 SQL Server 的计算机帐户具有对 UNC 位置的**写入**权限。  


> [!IMPORTANT]  
>  在转移具有一个或多个管理点数据库副本的数据库之前，你必须先删除数据库副本。 完成数据库转移后，你可以重新配置数据库副本。 有关详细信息，请参阅 [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

##  <a name="bkmk_SPN"></a>管理站点数据库服务器的 SPN  
你可为站点数据库选择运行 SQL 服务的帐户：  

-   当使用计算机系统帐户运行服务时，将为你自动注册 SPN。  

-   当使用域本地用户帐户运行服务时，必须手动注册 SPN 以确保 SQL 客户端和其他站点系统可执行 Kerberos 身份验证。 若未进行 Kerberos 身份验证，与数据库的通信可能失败。  

SQL 服务器文档可帮助你 [手动注册 SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx)，并提供有关 SPN 和 Kerberos 连接的其他背景信息。  

> [!IMPORTANT]  
>  -   在为群集 SQL Server 创建 SPN 时，你必须指定 SQL Server 群集的虚拟名称作为 SQL Server 计算机名  
> -   用于为 SQL Server 命名实例注册 SPN 的命令与你在为默认实例注册 SPN 时使用的命令相同，只是端口号必须与命名实例使用的端口匹配  

可通过使用 **Setspn** 工具来为站点数据库服务器的 SQL Server 服务帐户注册 SPN。 你必须在位于 SQL Server 的域中的计算机上运行 Setspn 工具，并且该工具必须使用域管理员凭据才能运行。  

 使用下列过程作为如何为在 Windows Server 2008 R2 上使用 Setspn 工具的 SQL Server 服务帐户管理 SPN 的示例。 有关 Setspn 的具体指引，请参阅 [Setspn Overview（Setspn 概述）](http://go.microsoft.com/fwlink/p/?LinkId=226343)或特定于你的操作系统的类似文档。  

> [!NOTE]  
>  下列过程引用 Setspn 命令行工具。 在通过产品 CD 或 [Microsoft Download Center（Microsoft 下载中心）](http://go.microsoft.com/fwlink/p/?LinkId=100114)安装 Windows Server 2003 支持工具时，将包括 Setspn 命令行工具。 有关如何通过产品 CD 安装 Windows 支持工具的详细信息，请参阅 [安装 Windows 支持工具](http://go.microsoft.com/fwlink/p/?LinkId=62270)。  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>为 SQL Server 服务帐户手动创建域用户服务主体名称 (SPN)  

1.  在“开始”  菜单上，单击“运行” ，然后在“运行”对话框中输入“cmd”  。  

2.  在命令行中，导航到 Windows Server 支持工具安装目录。 默认情况下，这些工具位于 **C:\Program Files\Support Tools** 目录中。  

3.  输入有效的命令以创建 SPN。 要创建 SPN，你可以使用运行 SQL Server 的计算机的 NetBIOS 名称或完全限定的域名 (FQDN)。 但是，你必须为 NetBIOS 名称和 FQDN 都创建 SPN。  

    > [!IMPORTANT]  
    >  在为群集 SQL Server 创建 SPN 时，你必须指定 SQL Server 群集的虚拟名称作为 SQL Server 计算机名。  

    -   要为 SQL Server 计算机的 NetBIOS 名称创建 SPN，请键入下列命令：**setspn -A MSSQLSvc/&lt;SQL Server computer name\>:1433 &lt;Domain\Account>**  

    -   要为 SQL Server 计算机的 FQDN 创建 SPN，请键入下列命令：**setspn -A MSSQLSvc/&lt;SQL Server FQDN\>:1433 &lt;Domain\Account>**  

    > [!NOTE]  
    >  用于为 SQL Server 命名实例注册 SPN 的命令与你在为默认实例注册 SPN 时使用的命令相同，只是端口号必须与命名实例使用的端口匹配。  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>通过使用 Setspn 命令验证是否已正确注册了域用户 SPN  

1.  在“开始”  菜单上，单击“运行” ，然后在“运行”  对话框中输入“cmd”  。  

2.  在命令提示符处，输入以下命令：**setspn -L &lt;domain\SQL Service Account>**。  

3.  查看注册的“ServicePrincipalName”  ，确保已为 SQL Server 创建了有效的 SPN。  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>在使用 ADSIEdit MMC 控制台时验证是否已正确注册了域用户 SPN  

1.  在“开始”  菜单上，单击“运行” ，然后输入“adsiedit.msc”  以启动 ADSIEdit MMC 控制台。  

2.  如有必要，连接到站点服务器的域。  

3.  在控制台窗格中，依次展开站点服务器的域、“DC=&lt;服务器可分辨名称\>”展开“CN=Users”右击“CN=&lt;Service Account User\>”，然后单击“属性”。  

4.  在“CN=&lt;服务帐户用户\>属性”对话框中，查看 **servicePrincipalName** 值，以确保创建了有效的 SPN 并且已与正确的 SQL Server 计算机关联。  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>将 SQL Server 服务帐户从本地系统更改为域用户帐户  

1.  创建或选择要用作 SQL Server 服务帐户的域或本地系统用户帐户。  

2.  打开“SQL Server 配置管理器” 。  

3.  单击“SQL Server 服务”，然后双击“SQL Server &lt;INSTANCE NAME\>”。  

4.  在“登录”  选项卡上，选择“此帐户” ，然后输入在步骤 1 中创建的域用户帐户的用户名和密码，或单击“浏览”  查找 Active Directory 域服务中的用户帐户，然后单击“应用” 。  

5.  在“确认帐户更改”  对话框中单击“是”  以确认服务帐户更改并重启 SQL Server 服务。  

6.  在成功更改服务帐户后单击“确定”  。  

##  <a name="bkmk_reset"></a>运行站点重置  
 当在管理中心站点或主站点中运行站点重置时，站点将：  

-   重新应用默认 Configuration Manager 文件和注册表权限  

-   重新安装该站点上的所有站点组件和所有站点系统角色  

辅助站点不支持站点重置。  

你可以选择手动运行站点重置，但是在你修改站点配置后也可以自动运行。  

例如，如果已更改为 Configuration Manager 组件使用的帐户，应当考虑手动进行站点重置以确保站点组件更新使用新的帐户详细信息。 但是，如果修改站点上的客户端或服务器语言，Configuration Manager 将自动运行站点重置，因为必须进行重置，然后站点才能使用此更改。  

> [!NOTE]  
>  站点重置不会重置对非 Configuration Manager 对象的访问权限。  

运行站点重置时：  

1.  安装程序会停止并重启“SMS_SITE_COMPONENT_MANAGER”  服务和“SMS_EXECUTIVE”  服务的线程组件。  

2.  安装程序会删除本地计算机和远程站点系统计算机上的站点系统共享文件夹和“SMS Executive”  组件，然后再重新创建。  

3.  安装程序重启了“SMS_SITE_COMPONENT_MANAGER”  服务，此服务会安装“SMS_EXECUTIVE”  和“SMS_SQL_MONITOR”  服务。  

此外，站点重置会还原下列对象：  

-   “SMS”  或“NAL”  注册表项，以及这些项下的任何默认子项。  

-   Configuration Manager 文件目录树，以及此文件目录树中的任何默认文件或子目录。  

**运行站点重置时需满足的先决条件**  

用于执行站点重置的帐户必须具有下列权限：  

-   用于执行站点重置的帐户必须具有下列权限：  

    -   **管理中心站点**：您用于在此站点中运行站点重置的帐户必须是管理中心站点服务器上的本地管理员，而且必须具有与“完全权限管理员”  这个基于角色的管理安全角色等效的权限。  

    -   **主站点**：您用于在此站点中运行站点重置的帐户必须是主站点服务器上的本地管理员，而且必须具有与“完全权限管理员”  这个基于角色的管理安全角色等效的权限。 如果主站点位于具有管理中心站点的层次结构中，则此帐户还必须是管理中心站点服务器上的本地管理员。  

**站点重置的限制**
  - 从版本 1602 开始，只要主要层次结构配置为支持[在预生产集合中测试客户端升级](/sccm/core/clients/manage/upgrade/test-client-upgrades)，则不能使用站点重置来更改安装在站点的服务器或客户端语言包。

#### <a name="to-perform-a-site-reset"></a>执行站点重置  

1.  从 **&lt;Configuration Manager 站点安装文件夹 \>\BIN\X64\setup.exe** 运行 **Configuration Manager 安装程序**。  

    > [!TIP]  
    >  也可以通过启动站点服务器计算机上或 Configuration Manager 源媒体上的“开始”菜单上的 Configuration Manager 安装程序运行站点重置。  

2.  在“入门”  页上，选择“执行站点维护或重置此站点” ，然后单击“下一步” 。  

3.  在“站点维护”  页上，选择“重置站点而不更改配置” ，然后单击“下一步” 。  

4.  单击“是”  以开始站点重置。  

在站点重置完成时，单击“关闭”  以完成本过程。  

##  <a name="bkmk_sitelang"></a>管理站点上的语言包  
安装站点后，你可以更改正在使用的服务器和客户端语言包：  

**服务器语言包：**  

-   **适用于：**  

     Configuration Manager 控制台安装  

     适用的站点系统角色的新安装  

-   **详细信息：**  

     更新站点中的服务器语言包之后，可以将语言包支持添加到 Configuration Manager 控制台。  

     若要向 Configuration Manager 控制台添加服务器语言包支持，必须从站点服务器的 **ConsoleSetup** 文件夹安装 Configuration Manager 控制台，其中该站点服务器包括想使用的语言包。 如果已安装 Configuration Manager 控制台，则必须先卸载它，以使新安装能够识别当前支持的语言包的列表。  

**客户端语言包：**  

-   **适用于：**  

     对客户端语言包进行更改将更新客户端安装源文件，这样新客户端安装和升级会添加对客户端语言已更新列表的支持。  

-   **详细信息：**  

     更新站点中的客户端语言包之后，必须使用包含客户端语言包的源文件来安装将使用这些语言包的每个客户端。  

有关 Configuration Manager 支持的客户端和服务器语言的信息，请参阅 [System Center Configuration Manager 中的语言包](../../../core/servers/deploy/install/language-packs.md)  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>修改站点支持的语言包  

1.  在站点服务器上，从 **&lt;Configuration Manager 站点安装文件夹\>\BIN\X64\setup.exe.** 运行 Configuration Manager 安装程序  

2.  在“入门”  页上，选择“执行站点维护或重置此站点” ，然后单击“下一步” 。  

3.  在“站点维护”  页上，选择“修改语言配置” ，然后单击“下一步” 。  

4.  在“先决条件下载”  页上，选择“下载所需文件”  以获取语言包的更新，或者选择“使用以前下载的文件”  ，以使用以前下载的包含要添加到站点的语言包的文件。 单击“下一步”  以验证文件并继续。  

5.  在“服务器语言选择”  页上，选中此站点支持的服务器语言的复选框，然后单击“下一步” 。  

6.  在“客户端语言选择”  页上，选中此站点支持的客户端语言的复选框，然后单击“下一步” 。  

7.  单击“下一步” 以修改站点的语言支持。  

    > [!NOTE]  
    >  Configuration Manager 会启动站点重置（也会在该站点重新安装所有站点系统角色）。  

8.  单击“关闭”  以完成本过程。  

##  <a name="BKMK_ModDBAlert"></a>修改数据库服务器警报阈值  
 默认情况下，当站点数据库服务器上的可用磁盘空间不足时，Configuration Manager 会生成警报。 默认值设置为当可用磁盘空间为 10 GB 或更少时生成警告，当可用磁盘空间为 5 GB 或更少时生成严重警报。 可以为每个站点修改这些值或禁用警报。  

 更改这些设置：  

1.  在“管理”  工作区中，展开“站点配置” ，然后单击“站点” 。  

2.  选择想要配置的站点并打开该站点的“属性” 。  

3.  在该站点的“属性”对话框中，选择“警报”选项卡，然后编辑设置。  

4.  单击“确定”  以关闭站点属性对话框。  
