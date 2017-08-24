---
title: "为使用 Intune 管理的 Android 和 Samsung KNOX 标准版设备创建配置项 | Microsoft Docs"
description: "使用 System Center Configuration Manager Android 和 Samsung KNOX 标准版配置项目管理设备的设置。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
caps.latest.revision: "17"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: c9961c2e9866199571a1b39a7b185cb6bb96f998
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>如何为没有使用 System Center Configuration Manager 客户端管理的 Android 和 Samsung KNOX 设备创建配置项目

使用 System Center Configuration Manager **Android 和 Samsung KNOX** 配置项目管理在 Microsoft Intune 中注册或者由 Configuration Manager 在本地进行管理的 Android 和 Samsung KNOX 设备的设置。  

#### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>若要创建 Android 和 Samsung KNOX 配置项目  

1. 在 Configuration Manager 控制台中，选择“资产和符合性”。  

2. 在“资产和符合性”工作区中，展开“符合性设置”，然后选择“配置项目”。  

3. 在“主页”选项卡上的“创建”组中，选择“创建配置项目”。  

4. 在“创建配置项目向导”的“常规”页面上，指定配置项目的名称和可选描述。  

5. 在“指定要创建的配置项目类型”下，选择“Android 和 Samsung KNOX”。  

6. 如果创建并分配类别以帮助在 Configuration Manager 控制台中搜索和筛选配置项目，请选择“类别”。  

7. 在向导的“支持的平台”页面上，选择将评估配置项目的特定 Android 或 Samsung KNOXs 平台。  

8. 在向导的“设备设置”页面上，选择要配置的设置组。 请参阅本主题中的 [Android 和 Samsung KNOX 配置项目设置参考](#BKMK_setref)以了解详细信息，然后选择“下一步”。  

    > [!TIP]  
    >  如果所需设置未列出，请选中“配置默认设置组以外的其他设置”框。  

9. 在每个设置页上，配置所需的设置。 此外，选择是否要在它们在设备上不符合要求时进行修正（如果支持这样做）。  

10. 对于每个设置组，还可以配置在发现配置项目不符合要求时将要报告的严重性：  

    - **不报告**。 对于 Configuration Manager 报表，不符合此符合性规则的设备不报告故障严重性。  

    - **信息**。 对于 Configuration Manager 报表，不符合此符合性规则的设备将故障严重性报告为**信息**。  

    - **警告**。 对于 Configuration Manager 报表，不符合此符合性规则的设备将故障严重性报告为**警告**。  

    - **严重**。 对于 Configuration Manager 报表，不符合此符合性规则的设备将故障严重性报告为**严重**。  

    - **严重事件**。 对于 Configuration Manager 报表，不符合此符合性规则的设备将故障严重性报告为**严重**。 应用程序事件日志中也会以 Windows 事件的形式记录此严重性级别。  

11. 在向导的“平台适用性”页面上，查看任何与先前选择的受支持平台不兼容的设置。 你可以返回并删除这些设置，也可以继续。  

    > [!TIP]  
    >  不会对不受支持的设置评估符合性。  

12. 完成该向导。  

 可以在“资产和符合性”  工作区的“配置项目”  节点中查看新配置项目。  

## <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Android 和 Samsung KNOX 配置项目设置参考  

### <a name="password"></a>Password  
这些设置适用于 Android 和 Samsung KNOX 设备。  

|设置|详细信息|  
|-------------|-------------|  
|**设备上需要密码设置**|支持的设备上需要密码。|  
|**最短密码长度（字符）**|指定密码的最短长度。|  
|**密码过期天数**|指定必须更改密码前的天数。|  
|**记住的密码数**|防止重复使用以前用过的密码。|  
|**擦除设备前的失败登录尝试次数**|如果此数目的登录尝试均失败，则擦除该设备。|  
|**锁定设备前的空闲时间**|指定在未使用设备的情况下设备锁定前的时间。|
|**密码质量**|指定所需的密码复杂性级别以及是否可以使用生物识别设备。|  
|**允许 Smart Lock 和其他信任代理**|让你能够控制兼容的 Android 设备上的 Smart Lock 功能。 如果设备处于可信位置（例如当它连接到特定蓝牙设备时，或者在 NFC 标记附近时），则此手机功能使你可以禁用或绕过设备锁屏界面密码。 可以使用此设置防止用户配置 Smart Lock。|
|**用于解锁的指纹 (KNOX 5.0+)**|允许使用指纹解锁兼容设备。|

### <a name="device"></a>设备   

|设置|详细信息|  
|------------------|-------------|  
|**语音拨号**|启用或禁用设备上的语音拨号功能。|
|**语音助手**|允许在设备上使用语音助手软件。|
|**屏幕捕获**|允许用户以图像形式捕捉屏幕内容。|
|**诊断数据提交**|允许设备向 Google 提交诊断信息。|
|**地理位置**|允许设备使用位置信息。|
|**复制和粘贴**|允许设备上的复制和粘贴功能。|
|**恢复出厂设置**|允许用户对设备执行恢复出厂设置。|  |
|**应用程序之间的剪贴板共享**|允许用户使用剪贴板在应用之间进行复制和粘贴。|  |
|**蓝牙**|允许在设备上使用蓝牙。|

### <a name="store"></a>存储

|设置|详细信息|  
|------------------|-------------|  
|**应用商店**|允许用户在设备上访问 Google Play 商店。|

### <a name="browser"></a>浏览器

|设置|详细信息|  
|------------------|-------------|  
|**允许使用 Web 浏览器**|允许使用设备的默认 Web 浏览器。|
|**自动填充**|允许使用 Web 浏览器的自动填充功能。|
|**活动脚本**|允许设备的 Web 浏览器使用活动脚本。|
|**弹出窗口阻止程序**|允许在 Web 浏览器中使用弹出窗口阻止程序。|
|**Cookie**|允许设备的 Web 浏览器使用 cookie。|

### <a name="cloud"></a>云  

|设置|详细信息|  
|-------------|-------------|  
|**Google 备份**|允许使用 Google 备份。|  
|**Google 帐户自动同步**|允许 Google 帐户设置自动同步。|  

### <a name="security"></a>安全  

|设置|详细信息|  
|-------------|-------------|  
|**SMS 和 MMS 消息**|允许在设备上使用 SMS 和 MMS 消息。|
|**可移动存储**|允许设备使用可移动存储，如 SD 卡。|
|**照相机**|允许使用设备相机。<br /><br /> 适用于 Android 和 Samsung KNOX 设备。|
|**近场通信 (NFC)**|允许使用近场通信的任务（如果设备支持）。|
|**YouTube**|允许在设备上使用 YouTube 应用。<br /><br /> 仅适用于 Samsung KNOX 设备。|  
|**关机**|允许设备关机。<br /><br /> 仅适用于 Samsung KNOX 设备。|  

### <a name="roaming"></a>漫游

|设置|详细信息|  
|-------------|-------------|  
|语音漫游|设备位于移动电话网络时，允许语音漫游。|
|数据漫游|设备位于移动电话网络时，允许数据漫游。|


### <a name="encryption"></a>加密  
 这些设置适用于 Android 和 Samsung KNOX 设备。  

|设置|详细信息|  
|-------------|-------------|  
|**存储卡加密**|要求设备存储卡加密。|
|**设备上的文件加密**|要求对移动设备上的文件进行加密。|  

### <a name="wireless-communications"></a>无线通信

|设置|详细信息|  
|-------------|-------------|  
|**无线网络连接**|允许使用设备的 Wi-Fi 功能。|
|**Wi-Fi Tethering**|允许在设备上使用 Wi-Fi Tethering。|


### <a name="compliant-and-noncompliant-apps-android"></a>符合和不符合应用 (Android)  
你可以指定公司中符合或不符合的 Android 应用的列表。 然后可使用报表来显示安装了不符合应用的设备和关联的用户。  

不能在同一配置项目中同时指定符合和不符合应用。  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>指定符合和不符合应用列表  

在  “符合和不符合应用 (Android)”页上，指定以下信息：  

|设置|更多信息|  
|-------------|----------------------|  
|**不符合应用列表**|指定如果用户安装，将报告为不符合应用的应用列表。|  
|**符合应用列表**|指定允许用户安装的应用列表。 安装的任何其他应用将报告为不相容。|  
|**添加**|将应用添加到选定的列表。 在应用商店中指定你选择的名称（可选择使用应用发布者）和应用的 URL。<br /><br /> 若要从 [Google Play 应用部分](https://play.google.com/store/apps)指定 URL，请搜索想要使用的应用。<br /><br /> 打开应用页面，并将该 URL 复制到剪贴板。 你现在可以在符合或不符合要求的应用列表中使用这个 URL。<br /><br /> **示例：** 在 Google Play 中搜索 **Microsoft Office Mobile**。 你使用的 URL 将为 **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**。|  
|**编辑**|使你能够编辑选定应用的名称、发布者和 URL。|  
|**移除**|从列表中删除选定的应用。|  
|**导入**|导入你已在逗号分隔值文件中指定的应用列表。 在文件中使用格式应用程序名称、发布者和应用 URL。|  

## <a name="android-for-work-configuration-items"></a>Android for Work 配置项
Android for Work 具有配置项的两个设置组：

- **密码**。 与 Android“经典”的设置相同。

- **工作配置文件**。 启用以下 Android for Work 设置：
  - **允许在工作和个人配置文件之间共享数据**
  - **在设备处于锁定状态时隐藏工作配置文件通知** (Android 6.0 +)
  - **设置默认应用权限策略** (Android 6.0+)

要在 Android 工作配置文件中创建配置项目，请在“常规”页上选择“Android for Work”，并配置每个设置组的设置。 像往常一样将配置项添加到基准并进行部署。 这些设置仅适用于注册为 Android for Work 的设备，不适用于注册为 Android 的设备。

### <a name="kiosk-mode-samsung-knox-only"></a>站台模式（仅限 Samsung KNOX）  
可以使用展台模式锁定设备以只允许某些功能工作。 例如，可以让设备只运行一个指定的托管应用，也可以禁用设备上的音量按钮。 这些设置可用于设备的演示模型。 也可将其用于专门执行一个功能的设备（如销售点设备）。  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>为 Samsung KNOX 设备配置展台模式  

1. 在“创建配置项目向导”的“为 Samsung KNOX 设备配置展台模式设置”页上，指定以下信息：  

   |设置|更多信息|  
   |-------------|----------------------|  
   |**选择应用**|选择“浏览”以选择 Configuration Manager Android 应用程序（扩展名为 **.apk**），当设备处于展台模式时将允许该应用程序运行。 不允许在设备上运行其他应用。|  
   |**音量按钮**|启用或禁用设备上的音量按钮。|  
   |**屏幕睡眠和唤醒按钮**|启用或禁用设备上的屏幕睡眠唤醒按钮。|  

2. 完成后，请选择“下一步”。  

## <a name="reports-for-monitoring"></a>监视报表
你可以使用以下任一报表监视符合和不符合应用：  

- **指定用户的不符合应用和设备的列表**。 显示有关安装了不符合指定策略的应用的用户和设备的信息。  

- **具有不符合应用的用户的摘要**。 显示有关安装了不符合指定策略的应用的用户的信息。  

有关如何使用报表的信息，请参阅 [System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)。  

## <a name="see-also"></a>另请参阅  
[未使用 System Center Configuration Manager 客户端管理的设备的配置项目](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
