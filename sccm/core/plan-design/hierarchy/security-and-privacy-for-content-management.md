---
title: 内容管理安全和隐私
titleSuffix: Configuration Manager
description: 优化 Configuration Manager 中内容管理的安全和隐私。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f665ea8315266e89e5ed94918823fc1b97becea
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136426"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Configuration Manager 中内容管理的安全和隐私

适用范围：System Center Configuration Manager (Current Branch)

本文包括有关 Configuration Manager 中内容管理的安全和隐私的信息。 



##  <a name="BKMK_Security_ContentManagement"></a> 内容管理的最佳安全方案  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>用于 Intranet 分发点的 HTTPS 或 HTTP 的优缺点
对于 Intranet 上的分发点，请考虑使用 HTTPS 和 HTTP 的优点和缺点。 在大多数情况下，相对于使用包含加密但未包含授权的 HTTPS，为授权使用 HTTP 和包访问帐户更加安全。 但是，如果内容中有你希望在传输过程加密的敏感数据，请使用 HTTPS。  

-   如果为分发点使用 HTTPS，则 Configuration Manager 不会使用包访问帐户来授予内容访问权限，但在通过网络传输内容时会对内容进行加密。  

-   如果为分发点使用 HTTP，可使用包访问帐户来进行授权，但在通过网络传输内容时不会对内容进行加密。  

自版本 1806 开始，请考虑为站点启用“增强型 HTTP”。 通过此功能，客户端可使用 Azure Active Directory 身份验证与 HTTP 分发点进行安全通信。 有关详细信息，请参阅[增强型 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。

#### <a name="protect-the-client-authentication-certificate-file"></a>保护客户端身份验证证书文件
如果为分发点使用 PKI 客户端身份验证证书（而不是自签名证书），请使用强密码保护证书文件 (.pfx)。 如果将文件存储在网络上，请在将文件导入 Configuration Manager 中时保护网络通道的安全。

若需要密码来导入分发点用来与管理点通信的客户端身份验证证书，此配置可帮助保护证书免受攻击者的攻击。 在网络位置和站点服务器之间使用服务器消息块 (SMB) 签名或 IPsec 防止攻击者篡改证书文件。  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>从站点服务器中删除分发点角色
默认情况下，Configuration Manager 安装程序会在站点服务器上安装分发点。 客户端无需直接与站点服务器进行通信。 若要减少攻击面，请将分发点角色分配给其他站点系统，并将其从站点服务器中删除。  

#### <a name="secure-content-at-the-package-access-level"></a>包访问级别的安全内容
分发点共享允许所有用户以“读取”方式访问。 要限制可访问内容的用户，请在为 HTTP 配置了分发点时使用包访问帐户。 此配置不适用于不支持包访问帐户的云分发点。 有关详细信息，请参阅[包访问帐户](/sccm/core/plan-design/hierarchy/accounts#package-access-account)。

#### <a name="configure-iis-on-the-distribution-point-role"></a>在分发点角色上配置 IIS
如果在你添加分发点站点系统角色时 Configuration Manager 安装 IIS，请在分发点安装完成时删除 HTTP 重定向或 IIS 管理脚本和工具。 分发点不需要 HTTP 重定向或 IIS 管理脚本和工具。 为了减少攻击面，请为 Web 服务器角色删除这些角色服务。  有关分发点 Web 服务器角色的角色服务的详细信息，请参阅[站点和站点系统要求](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>在创建包时设置访问权限
由于只有在你重新分发包时，对包文件上的访问帐户所做的更改才会生效，因此请在第一次创建包时小心设置包访问权限。 当包很大或分发到许多分发点时，以及当用于内容分发的网络带宽容量有限时，该配置很重要。  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>实现访问控制来保护包含预留内容的媒体
预留内容已压缩但未加密。 攻击者可读取和修改下载到设备的文件。 Configuration Manager 客户端会拒绝被篡改的内容，但仍将进行下载。  

#### <a name="import-prestaged-content-with-extractcontent"></a>使用 ExtractContent 导入预留内容
仅使用 ExtractContent.exe 命令行工具导入预留内容。 为了避免篡改和提升特权，请仅使用 Configuration Manager 附带的已授权命令行工具。  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>保护站点服务器和包源位置之间的信道的安全
创建应用程序和包时，在站点服务器和包源位置之间使用 IPsec 或 SMB 签名。 此配置可帮助防止攻击者篡改源文件。  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>使用分发点角色删除自定义网站的默认虚拟目录
如果在安装分发点角色之后更改站点配置选项以使用自定义网站（而不是默认网站），请删除默认虚拟目录。 从默认网站转换为自定义网站时，Configuration Manager 不会删除旧虚拟目录。 删除以下 Configuration Manager 最初在默认网站下创建的虚拟目录：  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>对于云分发点，请保护 Azure 订阅详细信息和证书
在使用云分发点时，请保护以下高价值的项目：
- Azure 订阅的用户名和密码
- Azure 管理证书 
- 云分发点服务证书

安全地存储证书。 如果在配置云分发点时通过网络浏览到这些证书，请在站点系统服务器和源位置之间使用 IPsec 或 SMB 签名。  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>对于服务持续性，请监视云分发点证书的到期日期
当云分发点的导入证书即将到期时，Configuration Manager 不会向你发出警告。 独立于 Configuration Manager 监视到期日期。 请确保在到期日之前续订并导入新证书。 如果从外部公共提供程序获取服务器身份验证证书，则此操作很重要，因为你可能需要更多时间来获取续订的证书。  

 如果任一证书到期，云服务管理器将生成状态消息 ID“9425”。 CloudMgr.log 文件包含一个条目，指示证书“处于过期状态”，并且到期日期也以 UTC 格式记录于其中。  



## <a name="security-considerations-for-content-management"></a>内容管理的安全注意事项  

在规划内容管理时，请考虑以下几点：  

-   客户端不会在下载内容之前对其进行验证。  

     Configuration Manager 客户端仅在将内容下载到其客户端缓存后才会对内容进行哈希验证。 如果攻击者篡改要下载的文件列表或篡改内容本身，则下载进程可能仅会占用客户端的大量网络带宽，并随后会在遇到无效哈希时丢弃内容。  

-   使用云分发点时，对内容的访问权限将自动限于你的企业。 而不能进一步将其限制到选定的用户或组。  

-   使用云分发点时，客户端将通过管理点进行验证，然后使用 Configuration Manager 令牌来访问云分发点。 令牌的有效期为 8 小时。 此行为意味着，如果你因客户端不再受信任而将其阻止，则在此令牌的有效期到期之前，该客户端可继续从云分发点下载内容。 此时，管理点将不会为该客户端发出其他令牌，因为该客户端已被阻止。  

     为避免被阻止的客户端在此八小时的时段内下载内容，请停止云服务。 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“云分发点”节点。  



##  <a name="BKMK_Privacy_ContentManagement"></a> 内容管理的隐私信息  

 Configuration Manager 不会在内容文件中包括任何用户数据（虽然管理用户可能会选择执行该操作）。  



## <a name="see-also"></a>另请参阅

- [内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  

- [应用程序管理的安全和隐私](/sccm/apps/plan-design/security-and-privacy-for-application-management)  

- [软件更新的安全和隐私](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

- [OS 部署的安全和隐私](/sccm/osd/plan-design/security-and-privacy-for-operating-system-deployment)  
