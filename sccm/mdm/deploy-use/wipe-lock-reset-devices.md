---
title: "使用 System Center Configuration Manager，通过远程擦除、锁定或密码重置功能保护数据 | Microsoft Docs"
description: "使用 System Center Configuration Manager，通过完全擦除、选择性擦除、远程锁定或密码重置功能保护设备数据。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
caps.latest.revision: "18"
caps.handback.revision: "0"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 351fdc6328dd0859d60e00b128963df738e69f81
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-by-using-system-center-configuration-manager"></a>使用 System Center Configuration Manager，通过远程擦除、锁定或密码重置功能保护数据

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 提供选择性擦除、完全擦除、远程锁定以及密码重置功能。 移动设备可以存储敏感的公司数据并提供对许多公司资源的访问。 为了保护设备，你可以发出以下命令：  

- 用于将设备还原为其出厂默认设置的完全擦除命令。  

- 只删除公司数据的选择性擦除命令。  

- 用于帮助保护设备安全的远程锁定可能会丢失。  

- 重置设备密码。  

## <a name="full-wipe"></a>完全擦除  
如果需要保护遗失设备的安全或者停用正在使用的设备，你可以向设备发出擦除命令。  

向设备发出“完全擦除”  命令以将设备还原为其出厂默认值。 这将删除所有公司及用户数据和设置。 可以在 Windows Phone、iOS、Android 和 Windows 10 上执行完全擦除。  

> [!NOTE]
> 擦除版本早于 1511，且 RAM 小于 4 GB 的 Windows 10 设备可能会使该设备不响应。 [了解详细信息](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram)。

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台启动远程擦除  

1. 在 Configuration Manager 控制台中，选择“资产和符合性”，然后选择“设备”。 或者，可以选择“设备集合”并选择一个集合。  

2. 选择需停用/擦除的设备。  

3. 选择“设备组”中的“远程设备操作”，然后选择“停用/擦除”。  

## <a name="selective-wipe"></a>选择性擦除  
向设备发出“选择性擦除”  命令以仅删除公司数据。 下表按平台描述了将删除什么数据，以及执行选择性擦除后对设备上保留的数据的影响。  

**Android**  

|注销设备时删除的内容|iOS|  
|--------------------------------------------|---------|  
|使用 Configuration Manager 和 Intune 安装的公司应用及关联数据|卸载应用。 删除公司应用数据。|  
|VPN 和 Wi-Fi 配置文件|删除。|  
|证书|删除并吊销。|  
|设置|已删除，除了：**允许语音漫游**、**允许数据漫游**和**允许漫游时自动同步**。|  
|管理代理|删除管理配置文件。|  
|电子邮件配置文件|对于由 Intune 设置的电子邮件配置文件，将删除电子邮件帐户和电子邮件。|  

**Android 和 Android Samsung KNOX 标准版**  

|注销设备时删除的内容|Android|Samsung KNOX 标准版|  
|--------------------------------------------|-------------|------------------|  
|使用 Configuration Manager 和 Intune 安装的公司应用及关联数据|保留已安装的应用和数据。|卸载应用。|  
|VPN 和 Wi-Fi 配置文件|删除。|删除。|  
|证书|吊销。|吊销。|  
|设置|删除要求。|删除要求。|  
|管理代理|撤销设备管理员权限。|撤销设备管理员权限。|  
|电子邮件配置文件|不适用。|对于由 Intune 设置的电子邮件配置文件，将删除电子邮件帐户和电子邮件。|  

**Android for Work**

在 Android for Work 设备上执行选择性擦除将删除该设备上的工作配置文件以及工作配置文件中的的所有数据、应用和设置。 这将在 Configuration Manager 和 Intune 中停用对该设备的管理。 Android for Work 不支持完全擦除。

 **Windows 10、Windows 8.1、Windows RT 8.1 和 Windows RT**  

|注销设备时删除的内容|Windows 10、Windows 8.1 和 Windows RT 8.1|  
|---------------------------------|-------------|
|使用 Configuration Manager 和 Intune 安装的公司应用及关联数据|将卸载应用并删除旁加载密钥。 使用 Windows 选择性擦除的应用将吊销加密密钥，并且数据将不再可访问。|  
|VPN 和 Wi-Fi 配置文件|删除。|  
|证书|删除并吊销。|  
|设置|删除要求。|
|管理代理|不适用。 管理代理为内置。|  
|电子邮件配置文件|删除启用了 EFS 的电子邮件，包括 Windows 电子邮件和附件的邮件应用。|  

 **Windows 10 移动版、Windows Phone 8.0 和 Windows Phone 8.1**

|注销设备时删除的内容|Windows 10 移动版、Windows Phone 8 和 Windows Phone 8.1|  
|-|-|
|使用 Configuration Manager 和 Intune 安装的公司应用及关联数据|卸载应用。 删除公司应用数据。|  
|VPN 和 Wi-Fi 配置文件|已针对 Windows 10 移动版和 Windows Phone 8.1 删除。|  
|证书|从 Windows Phone 8.1 中删除。|  
|管理代理|不适用。 管理代理为内置。|  
|电子邮件配置文件|已删除（除 Windows Phone 8.0 外）。|  

还从 Windows 10 移动版和 Windows Phone 8.1 设备删除了以下设置：  

- **需要密码才可解锁移动设备**  
- **允许简单密码**  
- **最短密码长度**  
- **所需的密码类型**
- **密码过期（天数）**  
- **记住密码历史**  
- **擦除设备前允许的重复登录失败次数**  
- **需要提供密码之前处于非活动状态的分钟数**  
- **所需密码类型 - 最小字符集数**  
- **允许照相机**
- **需要对移动设备加密**  
- **允许使用可移动存储**  
- **允许使用 Web 浏览器**  
- **允许应用程序商店**  
- **允许屏幕捕获**  
- **允许使用地理位置**  
- **允许 Microsoft 帐户**  
- **允许复制和粘贴**  
- **允许使用 Wi-Fi tethering**  
- **允许自动连接到免费 Wi-Fi 热点**  
- **允许 Wi-Fi 热点报告**  
- **允许恢复出厂设置**
- **允许使用蓝牙**  
- **允许使用 NFC**
- **允许 Wi-Fi**

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台启动远程擦除  

1. 在 Configuration Manager 控制台中，选择“资产和符合性”，然后选择“设备”。 或者，可以选择“设备集合”并选择一个集合。  

2. 选择需停用/擦除的设备。  

3. 选择“设备组”中的“远程设备操作”，然后选择“停用/擦除”。  

## <a name="wiping-efs-enabled-content"></a>擦除启用了 EFS 的内容  
Windows 8.1 和 Windows RT 8.1 支持选择性擦除加密文件系统 (EFS) 加密的内容。 下列各项适用于启用 EFS 的内容的选择性擦除：  

- 仅选择性擦除由 EFS 通过与 Intune 帐户相同的 Internet 域保护的应用和数据。 有关详细信息，请参阅 [设备数据管理的 Windows 选择性擦除](http://technet.microsoft.com/library/dn486874.aspx)。  

- 如果对与 EFS 关联的域进行了任何更改，则更改可能要花费长达 48 小时，之后才能对使用新域的应用和数据进行选择性擦除。  

- 向 Intune 注册的每个域均为将擦除的域。  

EFS 选择性擦除当前支持的数据和应用：  

- Windows 相关邮件应用。  

- 工作文件夹。

- 使用 EFS 加密的文件和文件夹。 有关详细信息，请参阅 [加密文件系统的最佳方案](http://support.microsoft.com/kb/223316)。  

### <a name="best-practices-for-selective-wipe"></a>选择性擦除的最佳方案  

- 为 iOS 和 Windows Phone 8.1 设备设置电子邮件配置文件，以便成功擦除电子邮件。  

- 确保通过移动设备应用管理分发了应用，以便成功擦除应用。  

- 对于 iOS，将设置“允许备份到 iCloud”配置为“不允许”，以使用户无法使用 iCloud 还原内容。  

- 如果帐户已停用一年，那么 Intune 将停用该帐户，并将执行选择性擦除。  

##  <a name="passcode-reset"></a>密码重置  
如果用户忘记密码，则你可以删除设备中的密码，或者在设备上强制使用新的临时密码，从而帮助用户解决问题。 下表列出了在不同移动平台上重置密码的方法。  

|平台|密码重置|  
|--------------|--------------------|  
|iOS|支持以便清除设备中的密码。 不创建新的临时密码。|
|macOS| 不支持。|
|Android|支持并且创建临时密码。|
|Android for Work | 不支持。|
|Windows 10 电脑|不支持。|  
|Windows 10 移动版|支持，已加入 Azure AD 的设备除外。|
|Windows Phone 8.1|支持。|  
|Windows RT 8.1 |不支持。|  
|Windows 8.1 电脑 |不支持。|  

#### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>在 Configuration Manager 中远程重置移动设备上的密码  

1. 在 Configuration Manager 控制台中，选择“资产和符合性”，然后选择“设备”。 或者，可以选择“设备集合”并选择一个集合。  

2. 选择要重置密码的一台或多台设备。  

3. 选择“设备组”中的“远程设备操作”，然后选择“密码重置”。  

#### <a name="to-show-the-state-of-the-passcode-reset"></a>显示密码重置状态  

1. 在 Configuration Manager 控制台中，选择“资产和符合性”，然后选择“设备”。 或者，可以选择“设备集合”并选择一个集合。  

2. 选择要显示密码重置状态的一台或多台设备。  

3. 选择“设备组”中的“远程设备操作”，然后选择“显示密码状态”。  

## <a name="remote-lock"></a>远程锁定  
如果用户丢失其设备，你可以远程锁定该设备。 下表列出了是如何在不同的移动平台上进行远程锁定的。  

|平台|远程锁定|  
|--------------|-----------------|  
|iOS|支持。|  
|Android|支持。|  
|Windows 10|此时不受支持。|  
|Windows Phone 8 和 Windows Phone 8.1|支持。|  
|Windows RT 8.1 |如果设备的当前用户是注册设备的相同用户，则支持。|  
|Windows 8.1|如果设备的当前用户是注册设备的相同用户，则支持。|  

#### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>通过 Configuration Manager 控制台远程锁定移动设备  

1. 在 Configuration Manager 控制台中，选择“资产和符合性”，然后选择“设备”。 或者，可以选择“设备集合”并选择一个集合。  

2. 选择要锁定的一台或多台设备。  

3. 选择“设备组”中的“远程设备操作”，然后选择“远程锁定”。  

#### <a name="to-show-the-state-of-the-remote-lock"></a>显示远程锁定状态  

1. 在 Configuration Manager 控制台中，选择“资产和符合性”，然后选择“设备”。 或者，可以选择“设备集合”并选择一个集合。  

2. 选择要显示远程锁定状态的设备。  

3. 选择“设备组”中的“远程设备操作”，然后选择“显示远程锁定状态”。  

### <a name="see-also"></a>另请参阅  
[Windows Selective Wipe for Device Data Management](http://technet.microsoft.com/library/dn486874.aspx)（设备数据管理的 Windows 选择性擦除）   
