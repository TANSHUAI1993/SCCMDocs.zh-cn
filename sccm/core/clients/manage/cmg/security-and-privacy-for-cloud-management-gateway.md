---
title: CMG 安全和隐私
description: 了解有关云管理网关安全和隐私的指导和建议。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.collection: M365-identity-device-management
ms.openlocfilehash: 013d00fd7c207df45b0f6b7910283c3e8b60b44d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137164"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>云管理网关的安全和隐私

适用范围：System Center Configuration Manager (Current Branch)

本文包含 Configuration Manager 云管理网关 (CMG) 的安全和隐私信息。 有关详细信息，请参阅[规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。

## <a name="cmg-security-details"></a>CMG 安全性详细信息
- CMG 接受并管理来自 CMG 连接点的连接。 它使用证书和连接 ID 进行 SSL 相互身份验证。
- CMG 使用以下方法接受和转发客户端请求：
    - 使用相互 SSL 通过基于 PKI 的客户端身份验证证书或 Azure AD 对连接进行预先身份验证。 
      - CMG VM 实例上的 IIS 根据上载到 CMG 的受信任根证书来验证证书路径。
      - VM 实例上的 IIS 还验证客户端证书吊销（如果启用）。 有关详细信息，请参阅[发布证书吊销列表](#bkmk_crl)。
    - 证书信任列表检查客户端身份验证证书的根。 此外，它还与客户端的管理点执行相同的验证。 有关详细信息，请参阅[查看站点的证书信任列表中的条目](#bkmk_ctl)。
    - 验证并筛选客户端请求 (URL)，以检查是否有任何 CMG 连接点可以处理该请求。  
    - 检查每个发布终结点的内容长度。
    - 使用轮循行为在同一站点中均衡 CMG 连接点的负载。
- CMG 连接点使用以下方法：
    - 针对 CMG 的所有 VM 实例生成一致的 HTTPS/TCP 连接。 它对这些连接每分钟进行一次检查和维护。
    - 使用证书向 CMG 进行 SSL 相互身份验证。
    - 根据 URL 映射转发客户端请求。
    - 报告连接状态，以显示控制台中的服务运行状态。
    - 每五分钟报告一次每个终结点的通信。

### <a name="configuration-manager-client-facing-roles"></a>面向 Configuration Manager 客户端的角色
管理点和软件更新点承载 IIS 中的终结点，用于处理客户端请求。 CMG 不公开所有内部终结点。 发布到 CMG 的每个终结点都有对应的 URL 映射。
  - 外部 URL 是客户端在与 CMG 进行通信时使用的 URL。
  - 内部 URL 是用于将请求转发给内部服务器的 CMG 连接点。

#### <a name="url-mapping-example"></a>URL 映射示例
在管理点上启用 CMG 通信时，Configuration Manager 会为每个管理点服务器创建一组内部 URL 映射。 例如：ccm_system、ccm_incoming 和 sms_mp。 管理点 ccm_system 终结点的外部 URL 可能如下所示：  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
URL 对每个管理点都是唯一的。 然后，Configuration Manager 客户端将启用了 CMG 的管理点的名称放入其 Internet 管理点列表中。 此名称如下所示：  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
站点自动将发布的所有外部 URL 上载到 CMG。 此行为允许 CMG 进行 URL 筛选。 所有 URL 映射都复制到 CMG 连接点。 接着，它根据客户端请求中的外部 URL 将通信转发到内部服务器。



## <a name="security-guidance-for-cmg"></a>CMG 安全指南


<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>发布证书吊销列表

发布 PKI 的证书吊销列表 (CRL)，以供基于 Internet 的客户端访问。 使用 PKI 部署 CMG 时，请在“设置”选项卡上将该服务配置为“验证客户端证书吊销”。此设置会将该服务配置为使用发布的证书吊销列表 (CRL)。 有关详细信息，请参阅[规划 PKI 证书吊销](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs)。



<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>查看站点的证书信任列表中的条目
<!--503739--> 每个 Configuration Manager 站点都包含一个受信任根证书颁发机构列表，即证书信任列表 (CTL)。 通过转到“管理”工作区、展开“站点配置”并选择“站点”，可查看和修改该列表。 选择一个站点，然后单击功能区中的“属性”。 切换到“客户端计算机通信”选项卡，然后单击“受信任的根证书颁发机构”下的“设置”。
 
使用 PKI 客户端身份验证，为具有 CMG 的站点使用限制性更强的 CTL。 否则，客户端注册会自动接受这类客户端：使用由管理点上已存在的任何受信任根颁发的客户端身份验证证书的客户端。

该子集可让管理员更好地控制安全性。 CTL 将服务器限制为仅接受从 CTL 中的证书颁发机构颁发的客户端证书。 例如，Windows 附带许多已知的第三方证书颁发机构 (CA) 证书，如 VeriSign 和 Thawte。 默认情况下，运行 IIS 的计算机信任链接到这些已知 CA 的证书。 如果没有为 IIS 配置 CTL，则会接受具有这些 CA 颁发的客户端证书的任何计算机作为有效的 Configuration Manager 客户端。 如果为 IIS 配置的 CTL 不包含这些 CA，而证书已链接到这些 CA，则会拒绝客户端连接。 


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>后续步骤

- [规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [设置云管理网关](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [有关云管理网关的常见问题解答](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [云管理网关的证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
