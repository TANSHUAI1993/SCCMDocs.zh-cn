---
title: 软件更新的先决条件
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager 中软件更新的先决条件。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 334854072e5c724f2c76432e7a7372c02cab3d54
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892269"
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager 中软件更新的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

本文列出了 System Center Configuration Manager 中软件更新的先决条件。 对于这些先决条件中的每一个，在不同的表格中列出了外部依赖关系和内部依赖关系。  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Configuration Manager 外部的软件更新依赖关系  
 以下部分列出了软件更新的外部依赖关系。  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) 必须安装在站点系统服务器上才可运行软件更新点、管理点和分发点。 有关详细信息，请参阅[站点系统角色的先决条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

### <a name="windows-server-update-services"></a>Windows Server 更新服务  
 软件更新同步和在客户端上进行的软件更新适用性扫描都需要使用 Windows Server Update Services (WSUS)。 在创建软件更新点角色之前，必须安装 WSUS 服务器。 软件更新点支持以下版本的 WSUS：  

- WSUS 10.0.14393（Windows Server 2016 中的角色）
- WSUS 10.0.17763（Windows Server 2019 中的角色）（需要使用 Configuration Manager 1810 或更高版本）
- WSUS 6.2 和 6.3（Windows Server 2012 和 Windows Server 2012 R2 中的角色）
  - 如果部署 Windows 10 升级，WSUS 6.2 和6.3 需要[kb 3095113 和 kb 3159706 （或等效更新）](#BKMK_wsus2012) 。

> [!NOTE]
> - 从版本 1702 开始，软件更新点角色不支持 Windows Server 2008 R2。 有关详细信息，请参阅[站点系统服务器支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_2008r2sp1)。
> - 如果在一个站点上有多个软件更新点，请确保它们全都运行相同版本的 WSUS。

### <a name="wsus-administration-console"></a>WSUS 管理控制台  
当软件更新点位于远程站点系统服务器上，且该站点服务器并未安装 WSUS 时，Configuration Manager 站点服务器上需要安装 WSUS 管理控制台。  

> [!IMPORTANT]  
> - 站点服务器上的 WSUS 版本必须与在软件更新点上运行的 WSUS 版本相同。
> - 不要使用 WSUS 管理控制台配置 WSUS 设置。 Configuration Manager 连接到在软件更新点上运行的 WSUS 的实例，并配置适当的设置。  


### <a name="windows-update-agent"></a>Windows 更新代理  
 需要在客户端上安装 Windows 更新代理 (WUA) 客户端，这样客户端才能连接到 WSUS 服务器。 WUA 检索为实现符合性而必须扫描的软件更新列表。  

 安装 Configuration Manager 时，会下载 WUA 的最新版本。 之后，安装 Configuration Manager 客户端时，如有必要会升级 WUA。 如果安装失败，必须使用另一种方法升级 WUA。  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Configuration Manager 内部的软件更新依赖关系  
 以下部分列出了 Configuration Manager 中软件更新的内部依赖关系。  

### <a name="management-points"></a>管理点  
 管理点在客户端计算机和 Configuration Manager 站点之间传输信息。 管理点对于软件更新是必需的。  

### <a name="software-update-points"></a>软件更新点  
 必须在 WSUS 服务器上安装软件更新点，才能在 Configuration Manager 中部署软件更新。 有关详细信息，请参阅[安装和配置软件更新点](../get-started/install-a-software-update-point.md)。

### <a name="distribution-points"></a>分发点  
 需要使用分发点来存储软件更新的内容。 有关如何安装分发点和管理内容的详细信息，请参阅[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="client-settings-for-software-updates"></a>软件更新的客户端设置  
客户端默认会启用软件更新。 还可以使用其他一些设置来控制客户端评估软件更新符合性的方法和时间，以及控制软件更新的安装方式。  

 有关详细信息，请参阅下列文章：  

- [软件更新的客户端设置](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [软件更新客户端设置](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Reporting Services 点  
 Reporting Services 点站点系统角色可以显示软件更新的报表。 此角色是可选的，但建议使用它。 有关 Reporting Services 点创建方法的详细信息，请参阅[配置报表](../../core/servers/manage/configuring-reporting.md)。  

## <a name="BKMK_wsus2012"></a>WSUS 6.2 和6.3 上需要哪些更新？

同步 WSUS 6.2 和6.3 中的**升级**分类需要两个更新。 有时，如果在安装 KB3095113 和 KB3159706 之前已同步升级，则可能会出现下载或部署升级错误。 有关可能的问题的信息在下一部分。  

- 必须在你的软件更新点和站点服务器上安装 2015 年 10 月发布的 [ 3095113](https://support.microsoft.com/kb/3095113)，然后再同步“升级”  分类。
  - 此更新启用 "**升级**" 分类。
- 若要为 Windows 10 版本1607及更高版本服务，必须安装和配置[KB 3159706](https://support.microsoft.com/en-us/help/3159706)。 3159706年 5 2016 月发布了 KB。
  - 此更新可让 WSUS 以本机方式解密用于升级 Windows 10 版本1607及更高版本的文件。

>[!IMPORTANT]
> 从7月2017开始，**每月安全质量汇总**中都包含了 kb 3095113 和 kb 3159706。 这意味着，如果已安装更新，可能不会看到 KB 3095113 和 KB 3159706，因为这些更新可能已安装了汇总。 但是，如果需要这些更新中的任何一种，我们建议安装10月2017日后发布的**安全每月质量汇总**，因为它们包含其他 wsus 更新以减少 wsus clientwebservice 的内存使用率。

## <a name="BKMK_RecoverUpgrades"></a>下载 Windows 10 升级失败并出现 "错误：无效的证书签名" 或0xc1800118

本部分中所述的更新和问题仅适用于在 Windows Server 2012 或 Windows Server 2012 R2 计算机上运行的 WSUS （WSUS 6.2 和6.3）。 通常，如果你在7月2017之前安装了 WSUS，并且最近启用了**升级**分类，则你将仅看到本部分中所述的问题。 但是，也可以在其他情况下查看这些问题。

### <a name="historical-information-about-kb-3095113"></a>有关 KB 3095113 的历史信息

 [KB 3095113](https://support.microsoft.com/kb/3095113)已[作为修补程序](https://blogs.technet.microsoft.com/wsus/2015/12/03/important-update-for-wsus-4-0-kb-3095113/)在 10 2015 月发布，以添加对 WSUS 的 Windows 10 升级支持。 此更新使 WSUS 能够在 Windows 10 的**升级**分类中同步和分发更新。

如果未先安装 [KB 3095113](https://support.microsoft.com/kb/3095113) 就同步任何升级，则会使用不可用数据填充 WSUS 数据库 (SUSDB)。 必须先清除该数据，才能正确部署升级。 无法使用下载软件更新向导下载处于此状态的 Windows 10 升级。

下载软件更新向导的 "完成" 页上显示类似于以下内容的错误：

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

此外，在 Patchdownloader.log 文件中记录了类似于下面的错误：

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

在过去，当发生这些错误时，可以通过对 WSUS 执行修改后的版本[步骤](https://blogs.technet.microsoft.com/wsus/2016/01/29/how-to-delete-upgrades-in-wsus/)来解决这些错误。 由于这些步骤类似于未执行 KB 3159706 安装后需要执行的手动步骤，我们已将这两组步骤合并为以下部分中的一个解决方案：

- [在安装 KB 3095113 或 KB 3159706 之前从同步升级中恢复](#bkmk_fix-upgrades)。

### <a name="historical-information-about-kb-3159706"></a>有关 KB 3159706 的历史信息

3148812 2016 年4月发布了 KB，使得 WSUS 能够以本机方式解密用于升级 Windows 10 包的 esd 文件。 [Kb 3148812 导致某些客户出现问题](https://blogs.technet.microsoft.com/wsus/2016/05/05/the-long-term-fix-for-kb3148812-issues/)，已被替换为[kb 3159706](https://support.microsoft.com/en-us/help/3159706)。 需要在你的所有软件更新点和站点服务器上安装 KB 3159706，然后才能为 Windows 10 版本1607和更高版本的设备服务。 但是，如果在安装后没有意识到需要执行以下手动步骤，则可能会出现问题：

1. 从提升的命令提示符运行 `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`。
1. 在所有 WSUS 服务器上重新启动 WSUS 服务。

如果你不知道 KB 3159706 在安装后需要手动步骤，或在安装 KB 3159706 之前在 Windows 10 1607 升级中进行了同步，则会遇到连接到 WSUS 控制台并分别部署升级的问题。 当客户端下载升级文件时，会收到[ **0xC1800118**错误代码](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus)。

由于解决方法步骤类似于在安装 KB 3095113 之前同步升级的解决方案，因此我们将两组步骤合并到下一部分的一个解决方案中。
 

### <a name="bkmk_fix-upgrades"></a>在安装 KB 3095113 或 KB 3159706 之前从同步升级中恢复

请按照以下步骤解决0xc1800118 错误和 "错误：无效的证书签名"：

1. 禁用 WSUS 和 Configuration Manager 中的 "**升级**" 分类。 在按照这些说明进行操作之前，不需要进行同步。  
   - 在顶级站点的软件更新点组件属性中取消选中“升级”分类  。
     - 有关详细信息，请参阅[配置分类和产品](../get-started/configure-classifications-and-products.md)。
   - 在 " [**选项**" 页](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations)上的 "**产品和分类**" 下取消选中 "**升级**" 分类，或使用 "以管理员身份运行 PowerShell ISE"。
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq “Upgrades”} | Set-WsusClassification -Disable
      ```  
     - 如果在多个 WSUS 服务器之间共享 WSUS 数据库，则只需取消选中每个数据库的**升级**一次。  
1. 在每个 WSUS 服务器上，从提升的命令提示符`"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`运行：。 然后，在所有 WSUS 服务器上重新启动 WSUS 服务。
   -  WSUS 会将数据库置于[单用户模式](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode)，然后检查是否需要维护。 服务运行或不基于检查结果运行。 然后，将数据库恢复到多用户模式。 
   - 如果在多个 WSUS 服务器之间共享 WSUS 数据库，只需为每个数据库执行一次此服务。
1. 使用以管理员身份运行的 PowerShell ISE 从每个 WSUS 数据库中删除所有 Windows 10 升级。
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. 从软件更新点所使用的每个 WSUS 数据库的 tbFile 表中删除文件。 在 WSUS 数据库上，从 SQL Server Management Studio 运行以下命令：
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. 在 Configuration Manager 中的顶层站点上启动软件更新同步，并等待其完成。 发生完全同步的原因是我们在删除**升级**时 Configuration Manager 了分类的更改。 有关详细信息，请参阅[同步软件更新](../get-started/synchronize-software-updates.md)。
1. 在软件更新点组件属性中选择“升级”分类  。 然后，启动另一个软件更新同步，将**升级**恢复到 WSUS 并 Configuration Manager。 你不必在 WSUS 中启用**升级**分类，因为 Configuration Manager 将为你执行此操作。
1. 如果客户端在下载升级时收到**0xC1800118**错误代码，则需要删除 Windows 更新代理使用的数据存储。 还可能需要删除设备上的隐藏 ~ BT 文件夹。 下次客户端扫描时，它将对 WSUS 服务器而不是增量进行完全扫描。 可使用类似于下面的示例脚本的 PowerShell 脚本：  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>后续步骤
[准备软件更新管理](../get-started/prepare-for-software-updates-management.md)
