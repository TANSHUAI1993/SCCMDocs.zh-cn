---
title: "如何为使用 Intune 管理的 Android for Work 设备创建配置项"
ms.custom: na
ms.date: 2017-07-31
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
caps.latest.revision: "17"
caps.handback.revision: "0"
author: robstackmsft
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: 87b34f0a3cce87f6e2ba813957a69b743648c1ca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>如何为使用 Intune 管理的 Android for Work 设备创建配置项

 使用 System Center Configuration Manager **Android for Work** 配置项目管理在 Microsoft Intune 中注册或者由 Configuration Manager 进行本地管理的 Android for Work 设备的设置。  

### <a name="to-create-an-android-for-work-configuration-item"></a>创建 Android for Work 配置项目  

1.  在 Configuration Manager 控制台中，单击“资产和符合性”。  

2.  在“资产和符合性”  工作区中，展开“符合性设置” ，然后单击“配置项目” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建配置项目” 。  

4.  在“创建配置项目向导”  的“常规” 页面上，指定配置项目的名称和可选描述。  

5.  在“指定要创建的配置项目类型” 下，选择“Android for Work” 。  

6.  如果创建并分配类别以帮助在 Configuration Manager 控制台中搜索和筛选配置项目，请选择“类别”。  

  单击“下一步” 。

7.  在向导的“设备设置”页上，选择要配置的设置组。 若要了解详细信息，请参阅 [Android for Work 配置项目设置](#android-for-work-configuration-item-settings-reference)，然后单击“下一步”。  

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

##  <a name="android-for-work-configuration-item-settings-reference"></a>Android for Work 配置项目设置参考  

### <a name="password"></a>Password  

|设置|详细信息|  
|-------------|-------------|  
|**设备上需要密码设置**|支持的设备上需要密码。|  
|**最短密码长度（字符）**|密码的最短长度。|  
|**密码过期天数**|必须更改密码前的天数。|  
|**记住的密码数**|防止重复使用最近用过的密码。|  
|**擦除设备前的失败登录尝试次数**|如果此数目的登录尝试均失败，则擦除该设备。|  
|**锁定设备前的空闲时间**|在设备锁定之前选择设备未使用的时间量。|
|**密码质量**|选择所需的密码复杂性级别以及是否可以使用生物识别设备。|  
|**允许 Smart Lock 和其他信任代理**|让你控制兼容的 Android 设备上的 Smart Lock 功能。 如果设备处于可信位置（例如当它连接到特定蓝牙设备时，或者在 NFC 标记附近时），则此手机功能（有时称为信任代理）使你可以禁用或绕过设备锁屏界面密码。 可以使用此设置防止最终用户配置 Smart Lock。|
|**解锁指纹**|&nbsp;|

###  <a name="work-profile"></a>工作配置文件  
 这些设置仅适用于 Samsung KNOX 设备。  

|设置名|详细信息|  
|------------------|-------------|  
|**允许在工作和个人配置文件之间共享数据**|选择：<br>- **未配置**<br>- 默认共享限制<br>- 工作配置文件中的应用可以处理来自个人配置文件的请求<br>- 个人配置文件中的应用可以处理来自工作配置文件的请求<br><br>（另请参阅使用自定义 URI 进行[复制-粘贴设置](#copy-paste-configuration-item-settings)）|  
|**在设备处于锁定状态时隐藏工作配置文件通知 (Android 6.0 +)**||
|**设置默认应用程序权限策略 (Android 6.0 +)**|选择：<br>- **未配置**<br>- **始终提示**<br>- **自动授予**<br>- **自动拒绝**|

### <a name="copy-paste-configuration-item-settings"></a>复制-粘贴配置项目设置
没有任何“允许工作和个人配置文件间的数据共享”选项可阻止复制-粘贴行为。 使用可配置为阻止复制-粘贴的自定义设置。 这可以通过自定义 URI 来设置。

- OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- 值类型：布尔

设置 DisallowCrossProfileCopyPaste，以确实阻止 Android for Work 个人和工作配置文件之间的复制粘贴行为。

## <a name="see-also"></a>另请参阅  
 [未使用 System Center Configuration Manager 客户端管理的设备的配置项目](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
