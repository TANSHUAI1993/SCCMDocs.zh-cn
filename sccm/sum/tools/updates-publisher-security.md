---
title: 证书和安全
titleSuffix: Configuration Manager
description: 管理 System Center Updates Publisher 中的证书和安全性
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: db60b7cf6332e778279b494b2922cd621983c20c
ms.sourcegitcommit: 4981a796e7886befb7bdeeb346dba32be82aefd6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67516294"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>管理 Updates Publisher 中的证书和安全性

*适用范围：System Center Configuration Manager (Current Branch)*

下面的过程展示了如何在更新服务器上配置证书存储、如何在客户端计算机上配置自签名证书，以及如何将组策略配置为允许计算机上的 Windows 更新代理扫描已发布的更新。

## <a name="configure-the-certificate-store-on-the-update-server"></a>在更新服务器上配置证书存储
 Updates Publisher 使用数字证书对其发布的目录中的更新进行签名。 证书必须位于更新服务器上的证书存储中，以及 Updates Publisher 计算机的证书存储中（如果此计算机远离更新服务器的话），才能将目录发布到更新服务器中。

下面的过程是将证书添加到更新服务器上证书存储的几种可行方法之一。

### <a name="to-configure-the-certificate-store"></a>如何配置证书存储
1.  在有权访问 Updates Publisher 计算机和更新服务器的计算机上，依次单击“开始”  和“运行”  ，在文本框中键入“MMC”  ，然后单击“确定”  ，打开 Microsoft 管理控制台 (MMC)。

2.  依次单击“文件”  、“添加/删除管理单元”  、“添加”  、“证书”  和“添加”  ，选择“计算机帐户”  ，然后单击“下一步”  。

3.  选择“另一台计算机”  ，键入更新服务器的名称或单击“浏览”  找到更新服务器计算机，然后依次单击“完成”  、“关闭”  和“确定”  。

4.  依次展开“证书(更新服务器名称)”和“WSUS”，然后单击“证书”    。

5.  在结果窗格中，右键单击相应证书，然后依次单击“所有任务”  和“导出”  。

6.  在“证书导出向导”中，使用默认设置，创建包含向导中指定的名称和位置的导出文件。 此文件必须对更新服务器可用，然后才能继续执行下一步。

7.  右键单击“受信任的发布者”  ，然后依次单击“所有任务”  和“导入”  。 使用第 6 步中的导出文件完成“证书导入向导”。

8.  如果使用的是自签名证书（如“WSUS 发布者自签名”  ），请右键单击“受信任的根证书颁发机构”  ，然后依次单击“所有任务”  和“导入”  。 使用第 6 步中的导出文件完成“证书导入向导”。

9.  右键单击“证书(更新服务器名称)”，单击“连接到另一台计算机”，输入 Updates Publisher 计算机的计算机名称，然后单击“确定”    。

10. 如果 Updates Publisher 计算机远离更新服务器，请重复执行第 7-9 步，将证书导入 Updates Publisher 计算机上的证书存储。



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>在客户端计算机上配置自签名证书
在客户端计算机上，Windows 更新代理 (WUA) 会扫描目录中的更新。 如果代理在本地计算机上的“受信任的发布者”证书存储中找不到相应的数字证书时，将无法通过此过程安装更新。 如果发布更新目录时使用的是自签名证书（如“WSUS 发布者自签名”  ），证书还必须位于本地计算机上的“受信任的根证书颁发机构”证书存储中，这样代理才能验证证书的有效性。

在客户端计算机上配置证书的方法有多种，如使用组策略和“证书导入向导”  ，或使用 CertUtil 工具和软件分发。可以使用其中一种。

下面的示例展示了如何在客户端计算机上配置签名证书。

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>如何在客户端计算机上配置自签名证书
1. 在有权访问更新服务器的计算机上，依次单击“开始”  和“运行”  ，在文本框中键入“MMC”  ，然后单击“确定”  ，打开 Microsoft 管理控制台 (MMC)。

2. 依次单击“文件”  、“添加/删除管理单元”  、“添加”  、“证书”  和“添加”  ，选择“计算机帐户”  ，然后单击“下一步”  。

3. 选择“另一台计算机”  ，键入更新服务器的名称或单击“浏览”  找到更新服务器计算机，然后依次单击“完成”  、“关闭”  和“确定”  。

4. 依次展开“证书(更新服务器名称)”和“WSUS”，然后单击“证书”    。

5. 右键单击结果窗格中的证书，然后依次单击“所有任务”  和“导出”  。 使用默认设置完成“证书导出向导”  ，创建包含向导中指定的名称和位置的导出证书文件。

6. 使用下面的方法之一，将用于对更新目录进行签名的证书添加到每个使用 WUA 扫描目录中更新的客户端计算机中。 在客户端计算机上添加证书，如下所述：

   -   对于自签名证书：将证书添加到“受信任的根证书颁发机构”  和“受信任的发布者”  证书存储中。

   -   对于证书颁发机构 (CA) 颁发的证书：将证书添加到“受信任的发布者”  证书存储中。

   > [!NOTE]
   > WUA 还会检查本地计算机上是否启用了“允许来自 Intranet Microsoft 更新服务位置的签名内容”  组策略设置。 必须为 WUA 启用此策略设置，以扫描使用 Updates Publisher 创建和发布的更新。 若要详细了解如何启用此组策略设置，请参阅[如何在客户端计算机上配置组策略](https://docs.microsoft.com/previous-versions/bb530967(v=technet.10))。



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>将组策略配置为允许计算机上的 WUA 扫描已发布的更新
必须先启用“允许来自 Intranet Microsoft 更新服务位置的签名内容”策略设置，然后计算机上的 Windows 更新代理 (WUA) 才能扫描使用 Updates Publisher 创建和发布的更新。 启用此策略设置后，如果更新已在本地计算机上的“受信任的发布者”证书存储中进行过签名，WUA 会接受通过 Intranet 位置收到的更新  。 在环境中的计算机上配置组策略的方法有多种。

对于不在域中的计算机，可以配置注册表项设置，从而允许来自 Intranet Microsoft 更新服务位置的签名内容。

下面的过程展示了为域中的计算机配置组策略，以及为不在域中的计算机配置注册表项值的基本步骤。

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>如何将组策略配置为允许 WUA 扫描已发布的更新
1.  以拥有配置组策略的相应安全权限的用户身份，打开组策略对象编辑器 Microsoft 管理控制台 (MMC) 管理单元。

2.  单击“浏览”  ，然后选择域、OU 或与网站相关联的 GPO（已配置的组策略在网站中传播到相应客户端计算机）。 依次单击“确定”  、“完成”  、“关闭”  和“确定”  。

3.  在控制台树中依次展开选定策略设置、“计算机配置”  、“管理模板”  和“Windows 组件”  ，然后单击“Windows 更新”  。

4.  在结果窗格中，右键单击“允许来自 Intranet Microsoft 更新服务位置的签名内容”  ，然后依次单击“属性”  、“已启用”  和“确定”  。
