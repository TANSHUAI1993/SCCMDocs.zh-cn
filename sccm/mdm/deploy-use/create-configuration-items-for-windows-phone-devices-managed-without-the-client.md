---
title: "如何为使用 Intune 管理的 Windows Phone 设备创建配置项 | Microsoft Docs"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df10dc4d-c9ff-4574-bb33-8d30eb14cfe3
caps.latest.revision: "13"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: bcb2d14ef097afc2915932fe09f6d83c968aecf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-windows-phone-devices-managed-without-the-system-center-configuration-manager-client"></a>如何为未使用 System Center Configuration Manager 客户端管理的 Windows Phone 设备创建配置项目
使用 System Center Configuration Manager **Windows Phone** 配置项目，为已在 Microsoft Intune 中注册或通过 Configuration Manager 本地管理的 Windows Phone 设备管理设置。  
  
### <a name="to-create-a-windows-phone-configuration-item"></a>创建 Windows Phone 配置项目  
  
1.  在 Configuration Manager 控制台中，单击“资产和符合性”。  
  
2.  在“资产和符合性”  工作区中，展开“符合性设置” ，然后单击“配置项目” 。  
  
3.  在“主页”  选项卡上的“创建”  组中，单击“创建配置项目” 。  
  
4.  在“创建配置项目向导”  的“常规” 页面上，指定配置项目的名称和可选描述。  
  
5.  在“指定要创建的配置项目的类型” 下，选择“Windows Phone” 。  
  
6.  如果创建并分配类别以帮助在 Configuration Manager 控制台中搜索和筛选配置项目，请单击“类别”。  
  
7.  在向导的“支持的平台”  页面上，选择评估配置项目的特定 Windows Phone 平台。  
  
8.  在向导的“设备设置”  页面上，选择要配置的设置组。 请参阅本主题中的 [Windows Phone 配置项目设置参考](#BKMK_Setref) 以了解详细信息，然后单击“下一步” 。  
  
    > [!TIP]  
    >  如果所需设置未列出，请选中“配置默认设置组以外的其他设置” 复选框。  
  
9. 在每个设置页面上，配置所需设置，以及是否要在它们在设备上不符合要求时修正它们（如果支持这样做）。  
  
10. 对于每个设置组，还可以配置在发现配置项目不符合要求时将要报告的严重性：  
  
    -   **不报告** - 对于 Configuration Manager 报表，不符合此合规性规则的设备不报告故障严重性。  
  
    -   **信息** - 对于 Configuration Manager 报表，不符合此合规性规则的设备将报告“信息”这一故障严重性。  
  
    -   **警告** - 对于 Configuration Manager 报表，不符合此合规性规则的设备将报告“警告”这一故障严重性。  
  
    -   **严重** - 对于 Configuration Manager 报表，不符合此合规性规则的设备将报告“严重”这一故障严重性。  
  
    -   **事件严重** - 对于 Configuration Manager 报表，不符合此合规性规则的设备将报告“严重”这一故障严重性。 应用程序事件日志中也会以 Windows 事件的形式记录此严重性级别。  
  
11. 在向导的“平台适用性”  页面上，查看任何与先前选择的受支持平台不兼容的设置。 你可以返回并删除这些设置，也可以继续。  
  
    > [!TIP]  
    >  不会对不受支持的设置评估符合性。  
  
12. 完成向导。  
  
 可以在“资产和符合性”  工作区的“配置项目”  节点中查看新配置项目。  
  
##  <a name="windows-phone-configuration-item-settings-reference"></a>Windows Phone 配置项目设置参考  
  
### <a name="password"></a>Password  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**设备上需要密码设置**|支持的设备上需要密码。|  
|**最短密码长度（字符）**|密码的最短长度。|  
|**密码过期天数**|必须更改密码前的天数。|  
|**记住的密码数**|防止重复使用以前用过的密码。|  
|**擦除设备前的失败登录尝试次数**|如果此数目的登录尝试均失败，则擦除该设备。|  
|**密码复杂性**|选择是否可以指定一个如“1234”的 PIN，或是否必须提供一个强密码。|  
|**将密码恢复 PIN 发送到 Exchange Server**||  
  
### <a name="device"></a>设备  
  
|设置|详细信息|  
|-------------|-------------|  
|**屏幕捕获**|允许用户捕获设备显示的屏幕截图。<br /><br /> （仅 Windows Phone 8.1）|  
|**诊断数据提交**|允许提交应用日志文件。|  
|**地理位置**|允许设备使用位置服务信息。<br /><br /> （仅 Windows Phone 8.1）|  
|**复制和粘贴**|使用复制和粘贴在应用之间传输数据。<br /><br /> （仅 Windows Phone 8.1）|  
|**蓝牙**|允许使用设备的蓝牙功能。|  
  
### <a name="email-management"></a>电子邮件管理  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**POP 和 IMAP 电子邮件**|允许连接到使用 POP 和 IMAP 标准的电子邮件帐户。|  
|**保留电子邮件的最长时间**|电子邮件从服务器中删除之前可保留的时间长度。|  
|**允许的消息格式**|指定用户电子邮件是否可以是 HTML 或仅是纯文本。|  
|**（自动下载）纯文本电子邮件的最大大小**|控制自动下载的纯文本电子邮件的最大大小。|  
|**（自动下载）HTML 电子邮件的最大大小**|控制自动下载的 HTML 电子邮件的最大大小。|  
|**（自动下载）附件的最大大小**|配置将自动下载的最大大小的电子邮件。|  
|**日历同步**||  
|**自定义电子邮件帐户**|允许在设备上使用非 Microsoft 帐户。|  
|**在 Windows Mail 应用中将 Microsoft 帐户设为可选**|不需要使用 Microsoft 帐户登录到 Windows Mail。|  
  
### <a name="store"></a>存储  
 这些设置仅适用于 Windows Phone 8.1 设备。  
  
|设置|详细信息|  
|-------------|-------------|  
|**应用商店**|允许在设备上访问应用商店。|  
  
### <a name="browser"></a>浏览器  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**允许使用 Web 浏览器**|启用或禁用默认 Internet 浏览器。|  
|**自动填充**|用户可以更改浏览器中的自动完成设置。|  
|**活动脚本**|浏览器可以运行脚本，如 Active X 脚本。|  
|**插件**|用户可以向 Internet Explorer 添加插件。|  
|**弹出窗口阻止程序**|启用或禁用浏览器弹出窗口阻止程序。|  
|**欺诈警告**|启用或禁用对潜在欺诈网站的警告。|  
  
### <a name="internet-explorer"></a>Internet Explorer  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**始终发送“不跟踪”标题**|防止浏览信息被发送到第三方站点。|  
|**Intranet 安全区域**||  
|**Internet 区域的安全级别**|配置 Internet 区域的安全级别。|  
|**Intranet 区域的安全级别**|配置 Intranet 区域的安全级别。|  
|**受信任的站点区域的安全级别**|配置受信任的站点区域的安全级别。|  
|**受限制的站点区域的安全级别**|配置受限制的站点区域的安全级别。|  
|**Intranet 区域的命名空间**||  
|**转至 Intranet 站点以获取单字条目**|启用或禁用以下设置：如果输入的有效站点名称前没有“HTTP:”，则允许 Internet Explorer 自动转至 Intranet 站点|  
|**企业模式菜单选项**|允许用户从 Internet Explorer 的“工具”  菜单中激活和停用企业模式。|  
|**记录报告位置 (URL)**|指定启用企业模式时将登录的受访网站的 URL。|  
|**企业模式站点列表位置 (URL)**|指定活动状态下将使用企业模式的网站列表的位置。|  
  
### <a name="cloud"></a>云  
  
|设置|详细信息|  
|-------------|-------------|  
|**设置同步**|允许设备之间的设置同步。|  
|**凭据同步**|允许设备之间的凭据同步。|  
|**Microsoft 帐户**|允许在设备上使用 Microsoft 帐户。<br /><br /> （仅 Windows Phone 8.1）|  
|**通过按流量计费的连接进行设置同步**|允许在 Internet 连接按流量计费时进行设置同步。|  
  
### <a name="security"></a>安全  
  
|设置|详细信息|  
|-------------|-------------|  
|**未签名的文件安装**|允许加载未签名的文件。|  
|**未签名的应用程序**|允许加载未签名的应用。|  
|**SMS 和 MMS 消息**|允许设备中的 SMS 和 MMS 消息。|  
|**可移动存储**|允许在设备上使用可移动存储，如 SD 卡。|  
|**照相机**|允许使用设备的照相机。|  
|**近场通信 (NFC)**|允许在设备上使用 NFC 进行通信。<br /><br /> （仅 Windows Phone 8.1）|  
|**允许使用 USB 连接**|允许外围设备通过 USB 连接到此设备。|
  
### <a name="peak-synchronization"></a>峰值同步  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**指定高峰时段**|指定将用于以下两个设置的时间窗口。|  
|**峰值同步频率**|选择设备在你指定的峰值时间期间的同步频率。|  
|**非峰值同步频率**|选择设备在你指定的峰值时间以外的同步频率。|  
  
### <a name="roaming"></a>漫游  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**漫游时的设备管理**|允许设备在漫游时由 Configuration Manager 管理。|  
|**漫游时的软件下载**|允许在漫游时下载应用和软件。|  
|**漫游时的电子邮件下载**|允许在漫游时下载电子邮件。|  
|**数据漫游**|允许在访问数据时进行网络之间的漫游。|  
  
### <a name="encryption"></a>加密  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**存储卡加密**|要求对设备使用的任何存储卡进行加密。|  
|**设备上的文件加密**|要求对移动设备上的文件进行加密。|  
|**需要电子邮件签名**|发送电子邮件前需签名。|  
|**签名算法**|选择用来签名电子邮件的算法。|  
|**需要电子邮件加密**|发送电子邮件前需加密。|  
|**加密算法**|选择用来加密电子邮件的算法。|  
  
###  <a name="wireless-communications"></a>无线通信  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置名|详细信息|  
|------------------|-------------|  
|**无线网络连接**|启用或禁用设备的 Wi-fi 功能。|  
|**Wi-Fi Tethering**|使用户可以将自己的设备用作移动热点。|  
|**可能时，将数据卸载到 Wi-fi**||  
|**Wi-Fi 热点报告**||  
  
##### <a name="to-configure-a-wireless-network-connection"></a>配置无线网络连接  
  
1.  在“配置移动设备无线通信设置”  页上，单击“添加” 。  
  
2.  在“无线网络连接”  对话框中，在移动设备上指定有关要设置的无线连接的以下信息：  
  
|设置|更多信息|  
|-------------|----------------------|  
|**网络名称 (SSID)**||  
|**网络连接**|从“Internet”  或“工作” 中选择。|  
|**身份验证**|从以下各项选择无线连接的身份验证方法：<br><br> - **打开**<br> - **共享**<br> - **WPA**<br> - **WPA-PSK**<br> - **WPA2**<br> - **WPA2-PSK**|  
|**数据加密**|选择此连接使用的加密方法。 根据所选“身份验证”  方法，可选取的值将有所不同：<br><br> - **已禁用**<br> - **WEP**<br> - **TKIP**<br> - **AES**|  
|**密钥索引**|选择“1”  到“4”  的将与“WEP”  的“数据加密” 设置一起使用的密钥索引。|  
|**此网络连接到 Internet**|如果要提供使通过无线连接的移动设备连接到 Internet 的代理设置，请选择此选项。|  
|**代理服务器设置**|根据需要为“HTTP”  、“WAP”  和“套接字” 指定“服务器”  和“端口” 设置。|  
|**启用 802.1X 网络访问**|如果要通过指定一种 EAP 类型来保护连接，请选择此选项。|  
|**EAP 类型**|选择要使用的 EAP 类型：<br><br> - **PEAP**<br> - **智能卡或证书**|  
    
  
###  <a name="certificates"></a>证书  
 让你导入证书以安装在移动设备上。  
  
 单击“导入” ，然后指定以下值：  
  
-   “证书文件” – 单击“浏览”  ，然后选择要导入的带有“”扩展名  的证书文件。  
  
-   “目标存储区” – 选择导入的证书文件将从其添加到移动设备的一个或多个目标存储区：  
  
    -   **根**  
  
    -   **CA**  
  
    -   **普通**  
  
    -   **特权**  
  
    -   **SPC**  
  
    -   **对等**  
  
-   “角色” – 若选择“”  （软件发行者证书）作为目标存储区，则选择以下将与证书关联的角色：  
  
    -   **移动运营商**  
  
    -   **管理员**  
  
    -   **通过身份验证的用户**  
  
    -   **IT 管理员**  
  
    -   **未通过身份验证的用户**  
  
    -   **受信任的设置服务器**  
  
### <a name="system-security"></a>系统安全  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**用户帐户控制**|启用或禁用设备上的 Windows 用户帐户控制。|  
|**网络防火墙**|启用或禁用 Windows 防火墙。|  
|**更新**|选择将 Windows 软件更新下载至计算机的方式。 例如，可以自动下载更新，但让用户选择何时进行安装。|  
|**更新的最小分类**|选择要下载到 Windows 计算机的更新的最小分类：“无” 、“重要” 或“推荐” 。|  
|**SmartScreen**|启用或禁用 Windows 智能屏幕。|  
|**病毒保护**|确保设备受防病毒软件保护|  
|**病毒保护签名为最新**|确保防病毒软件签名已是最新版本。|
|**允许手动取消注册**|让用户从 MDM 中删除设备。|  
  
### <a name="windows-server-work-folders"></a>Windows Server 工作文件夹  
 这些设置适用于 Windows Phone 8 和 Windows Phone 8.1。  
  
|设置|详细信息|  
|-------------|-------------|  
|**工作文件夹 URL**|配置用户可从自己的设备连接的 Windows Server 工作文件夹的位置。|  
  
### <a name="allowed-and-blocked-apps-list-windows-phone-81-only"></a>允许的应用和阻止的应用列表（仅 Windows Phone 8.1）  
 使你能够指定公司中符合或不符合 Windows Phone 应用的列表。 用户无法安装你指定为阻止的应用。 如果指定允许的应用列表，则用户仅可安装此列表中的应用。  
  
 不能在同一配置项目中同时指定允许的和阻止的应用。  
  
> [!IMPORTANT]  
>  如果指定允许的应用列表，则必须确保公司门户应用和已部署到 Windows Phone 8.1 设备的任何应用均在“允许”  应用列表中。  
  
##### <a name="to-specify-an-allowed-or-blocked-apps-list"></a>指定允许的或阻止的应用列表  
  
1.  在  “允许的和阻止的应用列表 (Windows Phone 8.1)”页上，指定以下信息：  
  
|||  
|-|-|  
|设置|更多信息|  
|**阻止的应用列表**|如果想要指定不允许用户安装的应用的列表，则选择此选项。|  
|**允许的应用列表**|如果想要指定允许用户安装的应用的列表，则选择此选项。|  
|**添加**|将应用添加到选定的列表。 在应用商店中指定你选择的名称（可选择使用应用发布者）和应用的 URL。<br /><br /> 若要从 Windows Phone 商店页面指定 URL，请搜索想要使用的应用。<br /><br /> **示例** ：在应用商店中搜索“Skype”  应用。 你使用的 URL 将为 http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51。<br /><br /> 对于公司门户应用或业务线应用，无需指定完整的 URL，指定应用 GUID 即可。|  
|**编辑**|允许你编辑选定应用的名称、发布者和 URL。|  
|**移除**|从列表中删除选定的应用。|  
|**导入**|导入你已在逗号分隔值文件中指定的应用列表。 在文件中使用格式、应用程序名称、发布者和应用 URL。|  
  
## <a name="see-also"></a>另请参阅  
 [未使用 System Center Configuration Manager 客户端管理的设备的配置项目](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)