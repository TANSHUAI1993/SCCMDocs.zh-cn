---
title: OS 部署的安全和隐私
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的 OS 部署的安全和隐私最佳做法。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b37bcf8fc1079ff1eaaa3d70cb3c1c8297a2685
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340367"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>在 Configuration Manager 中的 OS 部署的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

本文包含 Configuration Manager 中 OS 部署功能的安全和隐私信息。  



##  <a name="bkmk_security"></a>OS 部署的安全最佳做法  

在使用 Configuration Manager 部署操作系统时，请使用以下最佳安全方案：  


### <a name="implement-access-controls-to-protect-bootable-media"></a>实现访问控制来保护可启动媒体

创建可启动媒体时，请始终分配密码来帮助保护该媒体。 即使使用密码，也只是对包含敏感信息的文件进行加密，并且可以覆盖所有文件。  

请控制对媒体的物理访问，以阻止攻击者使用密码攻击获取客户端身份验证证书。  

为了阻止客户端安装已被篡改的内容或内容策略，内容将进行哈希处理并与原始策略一起使用。 如果内容哈希失败，或者关于内容是否与策略匹配的检查失败，则客户端将不使用可启动的媒体。 只对内容进行哈希处理。 该策略未进行哈希处理，但在指定密码时会对其进行加密和保护。 此行为使攻击者更难以成功修改策略。  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>创建 OS 映像媒体时使用安全的位置

如果未经授权的用户有权访问该位置，他们则可以篡改你创建的文件。 他们还可以使用所有可用磁盘空间，从而导致创建媒体失败。  


### <a name="protect-certificate-files"></a>保护证书文件 

使用强密码保护证书文件 (.pfx)。 如果将文件存储在网络上，请在将它们导入 Configuration Manager 中时保护网络通道的安全

当你需要密码来导入用于可启动的媒体的客户端身份验证证书时，此配置可帮助保护证书免受攻击者的攻击。  

在网络位置和站点服务器之间使用 SMB 签名或 IPsec 以防止攻击者篡改证书文件。  


### <a name="block-or-revoke-any-compromised-certificates"></a>阻止或撤消任何受到破坏的证书 

如果客户端证书已泄露，请从 Configuration Manager 阻止此证书。 如果是 PKI 证书，请将其撤销。  

若要使用可启动的媒体和 PXE 启动来部署 OS，必须指定一个具有私钥的客户端身份验证证书。 如果泄露了该证书，请在“管理”  工作区“安全”  节点内“证书”  节点中阻止该证书。  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>保护站点服务器与 SMS 提供程序之间的信道

当 SMS 提供程序远离站点服务器时，请保护通信通道的安全以保护启动映像。

如果修改了启动映像，并且 SMS 提供程序在非站点服务器的服务器上运行，则启动映像易受到攻击。 使用 SMB 签名或 IPsec 保护这些计算机之间的网络通道。  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>只在安全的网络段上为 PXE 客户端通信启用分发点

当客户端发送 PXE 启动请求时，你无法确保启用 PXE 的有效分发点可满足请求。 此方案有下列安全风险：  

- 响应 PXE 请求的恶意分发点可能会向客户端提供篡改过的映像。  

- 攻击者可能会针对 PXE 使用的 TFTP 协议发起中间人攻击。 此攻击可能会发送带有 OS 文件的恶意代码。 攻击者还可能会创建一个流氓客户端，直接向分发点发出 TFTP 请求。  

- 攻击者可以使用恶意客户端对分发点启动拒绝服务攻击。  

使用深度防御来保护网络段，客户端将在这些网络段中访问启用 PXE 的分发点。  

> [!WARNING]  
>  由于这些安全风险的缘故，当分发点在不受信任的网络（如外围网络）中时，请不要为 PXE 通信启用该分发点。  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>将启用 PXE 的分发点配置为仅在指定的网络接口上响应 PXE 请求  

如果允许分发点在所有网络接口上响应 PXE 请求，则此配置可能会向不受信任的网络公开 PXE 服务  


### <a name="require-a-password-to-pxe-boot"></a>PXE 启动需要密码

如果你要求提供密码来进行 PXE 启动，则此配置会为 PXE 启动过程额外添加一层安全保护。 此配置可以帮助预防恶意客户端加入 Configuration Manager 层次结构。  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>限制用于 PXE 启动或多播的 OS 映像中的内容

请勿将包含敏感数据的业务线应用程序或软件纳入到用于 PXE 启动或多播的映像。  

由于与 PXE 启动或多播相关的固有安全风险的缘故，因此，如果恶意计算机下载 OS 映像，请减小风险。  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>限制任务序列变量安装的内容

请勿将包含敏感数据的业务线应用程序或软件纳入到使用任务序列变量安装的应用程序包。  

如果使用任务序列变量部署软件，则可以在计算机上或者为无权接收该软件的用户安装该软件。  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>迁移用户状态时保护网络通道的安全

迁移用户状态时，使用 SMB 签名或 IPsec 保护客户端与状态迁移点之间的网络通道。  

通过 HTTP 初次连接后，会使用 SMB 传输用户状态迁移数据。 如果未保护网络通道的安全，则攻击者可能会读取和修改此数据。  


### <a name="use-the-latest-version-of-usmt"></a>使用最新版本的 USMT

使用 Configuration Manager 支持的最新版本的用户状态迁移工具 (USMT)。  

最新版本的 USMT 提供了安全增强功能，并且加强了对用户状态数据的迁移时间的控制。  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>对状态迁移点上的文件夹解除授权后手动删除这些文件夹  

在 Configuration Manager 控制台中的状态迁移点属性上删除状态迁移点文件夹时，该站点不会删除物理文件夹。 为了防止用户状态迁移数据信息泄露，请手动删除网络共享并删除文件夹。  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>请勿将删除策略配置为立即删除用户状态  

如果将状态迁移点上的删除策略配置为立即删除标记为要删除的数据，并且如果攻击者在有效计算机检索用户状态数据之前设法执行了此操作，则将立即删除用户状态数据。 将“在下列时间之后删除”  间隔设置得足够长，以验证是否成功还原了用户状态数据。  


### <a name="manually-delete-computer-associations"></a>手动删除计算机关联项 

在完成并验证了用户状态迁移数据还原之后手动删除计算机关联项。

Configuration Manager 不会自动删除计算机关联项。 通过手动删除不再需要的计算机关联项来帮助保护用户状态数据的标识。  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>在状态迁移点上手动备份用户状态迁移数据  

Configuration Manager 备份未包括站点备份中的用户状态迁移数据。  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>实现访问控制来保护预留的媒体  

请控制对媒体的物理访问，以阻止攻击者使用密码攻击获取客户端身份验证证书和敏感数据。  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>实现访问控制来保护引用计算机映像过程  

请确保用于捕获 OS 映像的引用计算机位于安全的环境中。 使用适当的访问控制，以便无法安装意外或恶意软件，并且不会无意中将其包含在捕获的映像中。 捕获映像时，请确保目标网络位置安全。 此过程有助于确保在捕获图像后图像不会被篡改。  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>始终在引用计算机上安装最新安全更新  

如果引用计算机具有当前安全更新，则它有助于在首次启动新计算机时缩小新计算机的漏洞窗口。  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>在将 OS 部署到未知计算机时实施访问控制

如果必须将 OS 部署到未知计算机，请实现访问控制以防止未授权的计算机连接到网络。  

预配未知计算机提供了一种按需部署新计算机的便捷方法。 但它也可能让攻击者有效地成为网络上的可信客户端。 限制对网络的物理访问，并监视客户端以检测未授权的计算机。 

响应 PXE 启动的 OS 部署的计算机可能会在此过程中销毁所有数据。 此行为可能导致无意中重格式化的系统的可用性损失。  


### <a name="enable-encryption-for-multicast-packages"></a>启用多播包加密  

对于每个 OS 部署包，你都可以在 Configuration Manager 使用多播传输包时启用加密。 此配置有助于防止恶意计算机加入多播会话。 它还有助于防止攻击者篡改传输。  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>监视启用多播的未经授权分发点  

如果攻击者可以访问你的网络，则他们可以将恶意多播服务器配置为欺骗 OS 部署。  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>当你将任务序列导出到网络位置时，请保护该位置和网络通道的安全。

限制可访问网络文件夹的人员。  

在网络位置和站点服务器之间使用 SMB 签名或 IPsec 以防止攻击者篡改导出的任务序列。  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>如果使用任务序列运行方式帐户，请采取额外的安全措施

如果使用[任务序列运行方式帐户](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account)，请采取以下预防措施：  

- 使用具有最低权限的帐户。  

- 请勿将网络访问帐户用于此帐户。  

- 切勿使此帐户成为域管理员。  

- 切勿为此帐户配置漫游配置文件。 在任务序列运行时，它会下载此帐户的漫游配置文件，从而导致很容易就能在本地计算机上访问该配置文件。  

- 要限制此帐户的作用域。 例如，为每个任务序列创建不同的任务序列运行方式帐户。 如果一个帐户受到侵害，则只会损害该帐户有权访问的客户端计算机。 如果命令行需要计算机上的管理访问权限，请考虑为任务序列运行方式帐户创建本地管理员帐户。 在运行该任务序列的所有计算机上创建此本地帐户，并在不再需要时立即删除该帐户。  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>限制和监视被授予 OS 部署管理员安全角色的管理用户

被授予“OS 部署管理器”安全角色的管理用户可以创建自签名证书  。 然后，可以使用这些证书模拟客户端并从 Configuration Manager获取客户端策略。  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>使用增强型 HTTP 可减少对网络访问帐户的需求

从 1806 版开始，当启用[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http) 时，多个 OS 部署方案不需要网络访问帐户即可从分发点下载内容。 有关详细信息，请参阅[任务序列和网络访问帐户](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSNetworkAccessAccount)。<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>OS 部署的安全问题  

虽然 OS 部署可能是为网络上的计算机部署最安全操作系统和配置的一种方便的方法，但它具有以下安全风险：  


### <a name="information-disclosure-and-denial-of-service"></a>信息泄露和拒绝服务  

如果攻击者可以获得对 Configuration Manager 基础结构的控件，则可以运行任何任务序列。 此过程可能包括格式化所有客户端计算机的硬盘驱动器。 可以将任务序列配置为包含敏感信息，如有权加入域的帐户和批量许可密钥。  


### <a name="impersonation-and-elevation-of-privileges"></a>特权的模拟和提升  

任务序列可以将计算机加入到域中，这可能会为恶意计算机提供经过身份验证的网络访问权限。 

保护用于可启动的任务序列媒体和 PXE 启动部署的客户端身份验证证书。 捕获客户端身份验证证书时，此过程使攻击者有机会获取证书中的私钥。 此证书允许他们模拟网络上的有效客户端。 在此情况下，恶意计算机可以下载策略，此策略可能包含敏感数据。  

如果客户端使用网络访问帐户来访问存储在状态迁移点上的数据，则这些客户端将有效地共享相同的标识。 他们可以从使用网络访问帐户的其他客户端访问状态迁移数据。 系统会对此数据进行加密，以便只有原始客户端才能读取该数据，但此数据可能会被篡改或删除。  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>通过使用管理点颁发的 Configuration Manager 令牌对连接到状态迁移点的客户端进行身份验证。  

Configuration Manager 不会限制或管理存储在状态迁移点上的数据量。 攻击者可能会填满可用磁盘空间并导致拒绝服务。  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>如果使用集合变量，本地管理员可以读取可能敏感的信息  

虽然集合变量提供了灵活地部署操作系统的方法，但此功能可能会导致信息泄露。  



##  <a name="bkmk_privacy"></a>OS 部署的隐私信息  

Configuration Manager 除可用于将 OS 部署到没有操作系统的计算机之外，它还可用于在计算机之间迁移用户的文件和设置。 管理员配置要转移的信息，包括个人数据文件、配置的设置和浏览器 Cookie。  

Configuration Manager 将信息存储在状态迁移点上，并在传输和存储期间对其进行加密。 只有与状态信息相关联的新计算机可以检索存储的信息。 如果新计算机丢失了用于检索这些信息的密钥，则具有计算机关联实例对象的“查看恢复信息”权限的 Configuration Manager 管理员可以访问这些信息，并将它们与新计算机关联  。 在新计算机还原状态信息后，默认情况下它会在一天后删除这些数据。 你可以配置状态迁移点何时删除标记为要删除的数据。 Configuration Manager 不会将状态迁移信息存储在站点数据库中，也不会将其发送给 Microsoft。  

如果使用启动媒体来部署 OS 映像，请始终使用默认的选项（要设置密码）来保护启动媒体。 密码对任务序列中存储的任何变量进行加密，但不存储在变量中的任何信息可能会容易泄露。  

在部署过程中，OS 部署可以使用任务序列来执行许多不同的任务，包括安装应用程序和软件更新等。 在配置任务序列时，还应注意到安装软件对隐私的影响。  

默认情况下，Configuration Manager 不会实现 OS 部署。 在你收集用户状态信息或者创建任务序列或启动映像之前，它需要执行几个配置步骤。  

在配置 OS 部署之前，请考虑你的隐私要求。  



## <a name="see-also"></a>另请参阅

[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)

[Configuration Manager 安全和隐私](/sccm/core/plan-design/security/security-and-privacy)
